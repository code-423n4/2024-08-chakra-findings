## [L-01] `to_token` never used and validated when `cross_chain_erc20_settlement` is called.

When `cross_chain_erc20_settlement` is called, it validates if `to_token` is non-zero but does not check whether `to_token` is a valid token supported by `to_handler`. Additionally, it is saved to `create_cross_txs` and the `ERC20TransferPayload`'s `payload` but is never used.

https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L111-L223

```solidity
    function cross_chain_erc20_settlement(
        string memory to_chain,
        uint256 to_handler,
>>>     uint256 to_token,
        uint256 to,
        uint256 amount
    ) external {
        require(amount > 0, "Amount must be greater than 0");
        require(to != 0, "Invalid to address");
        require(to_handler != 0, "Invalid to handler address");
        require(to_token != 0, "Invalid to token address");

        // ...

        {
            // Save the cross chain tx
            create_cross_txs[txid] = CreatedCrossChainTx(
                txid,
                chain,
                to_chain,
                msg.sender,
                to,
                address(this),
>>>             to_token,
                amount,
                CrossChainTxStatus.Pending
            );
        }

        {
            // Create a new cross chain msg id
            cross_chain_msg_id_counter += 1;
            uint256 cross_chain_msg_id = uint256(
                keccak256(
                    abi.encodePacked(
                        cross_chain_msg_id_counter,
                        address(this),
                        msg.sender,
                        nonce_manager[msg.sender]
                    )
                )
            );
            // Create a erc20 transfer payload
            ERC20TransferPayload memory payload = ERC20TransferPayload(
                ERC20Method.Transfer,
                AddressCast.to_uint256(msg.sender),
                to,
                AddressCast.to_uint256(token),
>>>             to_token,
                amount
            );

            // ...
    }
```

This is also the case on Cairo implementation (`handler_erc20.cairo`) : 

https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L167-L232

### Mitigation

Consider removing `to_token` from these data.

## [L-02] providing wrong `from_token` data to `create_cross_txs` and `CrossChainLocked` when `cross_chain_erc20_settlement` is called.

The `from_token` data inside `create_cross_txs` state and `CrossChainLocked` event is provided with `address(this)` instead of `token`.

https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L160

```solidity
//...
            //  struct CreatedCrossChainTx {
            //     uint256 txid;
            //     string from_chain;
            //     string to_chain;
            //     address from;
            //     uint256 to;
            //     address from_token;
            //     uint256 to_token;
            //     uint256 amount;
            //     CrossChainTxStatus status;
            // }
            // Save the cross chain tx
            create_cross_txs[txid] = CreatedCrossChainTx(
                txid,
                chain,
                to_chain,
                msg.sender,
                to,
>>>             address(this), 
                to_token,
                amount,
                CrossChainTxStatus.Pending
            );
//...
```

https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L218

```solidity
        //  event CrossChainLocked(
        //     uint256 indexed txid,
        //     address indexed from,
        //     uint256 indexed to,
        //     string from_chain,
        //     string to_chain,
        //     address from_token,
        //     uint256 to_token,
        //     uint256 amount,
        //     SettlementMode mode
        // );
        emit CrossChainLocked(
            txid,
            msg.sender,
            to,
            chain,
            to_chain,
>>>         address(this),
            to_token,
            amount,
            mode
        );
```

### Mitigation

provide `token` as `from_token` instead.

## [L-03] `SettlementSignatureVerifier.verifyECDSA` doesn't verify if `required_validators` is 0.

In the case where an admin misconfigures `required_validators` to 0 or fails to trigger initializer, `verifyECDSA` should revert if `required_validators` is set to 0.

https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/SettlementSignatureVerifier.sol#L134
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/SettlementSignatureVerifier.sol#L207

```solidity
    function verifyECDSA(
        bytes32 msgHash,
        bytes calldata signatures
    ) internal view returns (bool) {
        require(
            signatures.length % 65 == 0,
            "Signature length must be a multiple of 65"
        );

        uint256 len = signatures.length;
        uint256 m = 0;
        for (uint256 i = 0; i < len; i += 65) {
            bytes memory sig = signatures[i:i + 65];
            if (
>>>             validators[msgHash.recover(sig)] && ++m >= required_validators
            ) {
                return true;
            }
        }

        return false;
    }
```

### Mitigation

revert if `required_validators` is 0.

```diff
    function verifyECDSA(
        bytes32 msgHash,
        bytes calldata signatures
    ) internal view returns (bool) {
        require(
            signatures.length % 65 == 0,
            "Signature length must be a multiple of 65"
        );
+        require(
+           required_validators != 0,
+            "required_validators is 0"
+        );

        uint256 len = signatures.length;
        uint256 m = 0;
        for (uint256 i = 0; i < len; i += 65) {
            bytes memory sig = signatures[i:i + 65];
            if (
                validators[msgHash.recover(sig)] && ++m >= required_validators
            ) {
                return true;
            }
        }

        return false;
    }
```

## [L-04] `renounceOwnership` of `TokenRoles` doesn't remove `DEFAULT_ADMIN_ROLE` from the `msg.sender`.

`TokenRoles` overrides `transferOwnership` by adding an additional step to revoke `DEFAULT_ADMIN_ROLE` from `msg.sender` and assign it to the `newOwner`. However, when `renounceOwnership` is called, the previous owner will still retain the `DEFAULT_ADMIN_ROLE`.

https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/TokenRoles.sol#L25-L29

```solidity
    function transferOwnership(address newOwner) public override onlyOwner {
        _revokeRole(DEFAULT_ADMIN_ROLE, msg.sender);
        _grantRole(DEFAULT_ADMIN_ROLE, newOwner);
        _transferOwnership(newOwner);
    }
```

### Mitigation

overrides `renounceOwnership` to also revoke the `DEFAULT_ADMIN_ROLE`.

## [L-05] Unsafe downcasting occurs when `AddressCast.to_address` is called.

When `AddressCast.to_address` is called, it unsafely casts `bytes32` or `uint256` to the `address` type without checking if `_address` contains data greater than 20 bytes.

https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/libraries/AddressCast.sol#L14-L24
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/libraries/AddressCast.sol#L18-L36

```solidity
    function to_address(
        bytes32 _address
    ) internal pure returns (address result) {
        result = address(uint160(uint256(_address)));
    }

    function to_address(
        uint256 _address
    ) internal pure returns (address result) {
        result = address(uint160(_address));
    }
```

### Mitigation

Check the size of `_address` before cast it to `address` type.

## [L-06] `cross_chain_erc20_settlement` doesn't verify the size of `to` according to the destination chain.

`to` address should be checked according to the address size requirements of the destination chain. For instance, on an EVM-compatible chain, it should not exceed 20 bytes. while for StarkNet, it should not be greater than the maximum value of `felt252`, otherwise, execution will fail on the StarkNet chain.

https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L111-L117

```solidity
    function cross_chain_erc20_settlement(
        string memory to_chain,
        uint256 to_handler,
        uint256 to_token,
        uint256 to,
        uint256 amount
    ) external {
        require(amount > 0, "Amount must be greater than 0");
        require(to != 0, "Invalid to address");
        require(to_handler != 0, "Invalid to handler address");
        require(to_token != 0, "Invalid to token address");
       // ...
     }
```

### Mitigation

Add the `to` size check, especially for StarkNet

## [L-07] `nonce_manager` of users can be incremented by anyone by calling `send_cross_chain_msg` on `ChakraSettlement`.

Anyone can increase another user's `nonce_manager` by calling `send_cross_chain_msg`. While this would require a large number of requests to eventually reach the maximum value, it could still disrupt users' expectations if they rely on this value when integrating with the Chakra Network.

https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/ChakraSettlement.sol#L118

```solidity
    function send_cross_chain_msg(
        string memory to_chain,
        address from_address,
        uint256 to_handler,
        PayloadType payload_type,
        bytes calldata payload
    ) external {
        nonce_manager[from_address] += 1;
      // ...
    }
```

### Mitigation

consider to restrict `send_cross_chain_msg` for only valid `from_handler` so `nonce_manager` can only be increased by proper interaction.

## [L-08] provided wrong data to `ReceivedCrossChainTx.to_handler` when `receive_cross_chain_msg` on `ChakraSettlement`.

`address(this)` provided as `to_handler` instead of `to_handler`.

https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/ChakraSettlement.sol#L211

```solidity
// ...
        // struct ReceivedCrossChainTx {
        //     uint256 txid;
        //     string from_chain;
        //     string to_chain;
        //     uint256 from_address;
        //     uint256 from_handler;
        //     address to_handler;
        //     bytes payload;
        //     CrossChainMsgStatus status;
        // }
        receive_cross_txs[txid] = ReceivedCrossChainTx(
            txid,
            from_chain,
            contract_chain_name,
            from_address,
            from_handler,
>>>         address(this), 
            payload,
            CrossChainMsgStatus.Pending
        );
// ..
```

### Mitigation

provide `to_handler` to ReceivedCrossChainTx.to_handler`.

## [L-09] hardcoded `version` is provided when `coded.cairo` 's `encode_message` is called.

`version` is hardcoded instead of just accessing `message.version` from the params.

https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/codec.cairo#L95

```cairo
pub fn encode_message(message: Message) -> Array<u8>{
    
    // let message = Message{
    //     version: 1, 
    //     message_id: message_id.into(),
    //     payload_type: PayloadType::ERC20,
    //     payload: encode_transfer(transfer),
    // };
    let mut array_u8 = ArrayTrait::new();

>>> let version: u8 = 1;
    // ..
}
```

### Mitigation

use `message.version` from the params instead.

## [L-10] `cross_chain_erc20_settlement` of `handler_erc20.cairo` doesn't validate if `amount` provided is 0.

The invariant states that `amount` should be non-zero, but `cross_chain_erc20_settlement` allows users to provide 0 as the value for `amount`.

https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L167-L232

### Mitigation

revert when `amount` is 0.

## [L-11] provided wrong data to `CreatedCrossChainTx.from` when `cross_chain_erc20_settlement` on `handler_erc20.cairo`.

`get_contract_address()` provided as `from` instead of `get_caller_address()`.

https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L188

```cairo
            // pub struct CreatedCrossChainTx {
            //     tx_id : felt252,
            //     from_chain: felt252,
            //     to_chain: felt252,
            //     from: ContractAddress,
            //     to: u256,
            //     from_token: ContractAddress,
            //     to_token: u256,
            //     amount: u256,
            //     tx_status: u8
            //  }
            // @audit - (DONE) - compare with L1 struct doesnt matter
            let tx: CreatedCrossChainTx = CreatedCrossChainTx{
                    tx_id: tx_id,
                    from_chain: from_chain,
                    to_chain: to_chain,
>>>                 from: get_contract_address(),
                    to: to,
                    from_token: self.token_address.read(),
                    to_token: to_token, 
                    amount: amount,
                    tx_status: CrossChainTxStatus::PENDING
                };
```

### Mitigation

provide `get_caller_address()` to `CreatedCrossChainTxfrom`.