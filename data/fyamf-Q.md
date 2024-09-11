## Issue1: Wrong value of `from_token` in the struct `CreatedCrossChainTx`
When saving the cross chain tx, the `from_token` variable in the struct `CreatedCrossChainTx` is set to `address(this)`, while it should be the address of the token which is going to be bridged.
```solidity
    struct CreatedCrossChainTx {
        uint256 txid;
        string from_chain;
        string to_chain;
        address from;
        uint256 to;
        address from_token;
        uint256 to_token;
        uint256 amount;
        CrossChainTxStatus status;
    }
```
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/BaseSettlementHandler.sol#L59
```solidity
        {
            // Save the cross chain tx
            create_cross_txs[txid] = CreatedCrossChainTx(
                txid,
                chain,
                to_chain,
                msg.sender,
                to,
                address(this),
                to_token,
                amount,
                CrossChainTxStatus.Pending
            );
        }
```
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L160

## Issue2: Wrong value of `from_token` in the event `CrossChainLocked`
When emitting the event `CrossChainLocked`, the parameter `from_token` in the event `CrossChainLocked` is set to `address(this)` incorrectly, while it should be the address of the token which is going to be bridged.
```solidity
    event CrossChainLocked(
        uint256 indexed txid,
        address indexed from,
        uint256 indexed to,
        string from_chain,
        string to_chain,
        address from_token,
        uint256 to_token,
        uint256 amount,
        SettlementMode mode
    );
```
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/BaseSettlementHandler.sol#L47
```solidity
        emit CrossChainLocked(
            txid,
            msg.sender,
            to,
            chain,
            to_chain,
            address(this),
            to_token,
            amount,
            mode
        );
```
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L218

## Issue3: Missing `PENDING` status check in `handler_erc20::receive_cross_chain_callback`
https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L138
In the function `handler_erc20::receive_cross_chain_callback`, it does not check that the message status is pending or not. While, on EVM-based code, it enforces that the message status is equal to `PENDING`.
```solidity
        require(
            create_cross_txs[txid].status == CrossChainTxStatus.Pending,
            "invalid CrossChainTxStatus"
        );
```
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L378

## Issue4: Parameter `payload_type` can be manipulated on `settlement::receive_cross_chain_msg` 
In the function `settlement::receive_cross_chain_msg`, the parameter `payload_type` is not used in signatures and it is not enforced to be equal to the supported paylaod type. It is only emitted in the event `CrossChainHandleResult` which can be used for callback on the source chain. So, a malicious user can set this parameter to any unsupported payload type leading to wrong event emission.
```rust
        fn receive_cross_chain_msg(
            ref self: ContractState,
            cross_chain_msg_id: u256,
            from_chain: felt252,
            to_chain: felt252,
            from_handler: u256,
            to_handler: ContractAddress,
            sign_type: u8,
            signatures: Array<(felt252, felt252, bool)>,
            payload: Array<u8>,
            payload_type: u8,
        ) -> bool {
            //....

            // emit event
            self.emit(CrossChainHandleResult{
                cross_chain_settlement_id: cross_chain_msg_id,
                from_chain: to_chain,
                from_handler: to_handler,
                to_chain: from_chain,
                to_handler: from_handler,
                cross_chain_msg_status: status,
                payload_type: payload_type
            });
            return true;
        }
```
https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/settlement.cairo#L335

Please note that the callback on the source chain, currently does not care about the `payload_type` emitted from the destination chain.
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/ChakraSettlement.sol#L256

## Issue5: `to_handler` is not verified when sending message from EVM-based blockchains
When the function `ChakraSettlementHandler::cross_chain_erc20_settlement` is called, the parameter `to_handler` is not enforced to be a supported handler on the destination chain.
```solidity
    function cross_chain_erc20_settlement(
        string memory to_chain,
        uint256 to_handler,
        uint256 to_token,
        uint256 to,
        uint256 amount
    ) external {
        //....
    }
```
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L113

While, when sending a message from Starknet, `to_handler` is enforced to be supported.
```rust
        fn cross_chain_erc20_settlement(ref self: ContractState, to_chain: felt252, to_handler: u256, to_token: u256, to: u256, amount: u256) -> felt252{
            assert(self.support_handler.read((to_chain, to_handler)), 'not support handler');
            //....
        }
```
https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L168

Note that the functions `receive_cross_chain_msg` and `receive_cross_chain_callback` enforce that `from_chain` and `from_handler` are valid set.
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L311

This means that it is possible to send a message from EVM-based `chainA` to any arbitrary address (here is `to_handler`) on the destination chain.

## Issue6: `sign_type` is not used
The parameter `sign_type` is not used when the function `settlement::receive_cross_chain_msg` is called.
```rust
        fn receive_cross_chain_msg(
            ref self: ContractState,
            cross_chain_msg_id: u256,
            from_chain: felt252,
            to_chain: felt252,
            from_handler: u256,
            to_handler: ContractAddress,
            sign_type: u8,
            signatures: Array<(felt252, felt252, bool)>,
            payload: Array<u8>,
            payload_type: u8,
        ) -> bool {
            //.....
        }
```
https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/settlement.cairo#L332

## Issue7: Wrong field `from` in the struct `CreatedCrossChainTx`
The field `from` should be the address of the caller. So, it should be replaced by `get_caller_address()`.
```rust
    pub struct CreatedCrossChainTx {
       tx_id : felt252,
       from_chain: felt252,
       to_chain: felt252,
       from: ContractAddress,
       to: u256,
       from_token: ContractAddress,
       to_token: u256,
       amount: u256,
       tx_status: u8
    }
```
https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L98
```rust
            let tx: CreatedCrossChainTx = CreatedCrossChainTx{
                    tx_id: tx_id,
                    from_chain: from_chain,
                    to_chain: to_chain,
                    from: get_contract_address(),
                    to: to,
                    from_token: self.token_address.read(),
                    to_token: to_token,
                    amount: amount,
                    tx_status: CrossChainTxStatus::PENDING
                };
```
https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L188

## Issue8: `to_token` is not used
The parameter `to_token` in `ChakraSettlementHandler::cross_chain_erc20_settlement` is not enforced on the destination chain to be equal to the supporting token there.
```solidity
    function cross_chain_erc20_settlement(
        string memory to_chain,
        uint256 to_handler,
        uint256 to_token,
        uint256 to,
        uint256 amount
    ) external {
        //....
    }
```
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L114
https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L124

The same applies to the parameter `to_token` in `handler_erc20:cross_chain_erc20_settlement` where it can be any arbitrary value.
https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L167

## Issue9: If `to` is higher than `ContractAddress` size, it panics on Starknet
The paremter `to` can be arbitrarily set by the user in `ChakraSettlementHandler::cross_chain_erc20_settlement`.
```solidity
    function cross_chain_erc20_settlement(
        string memory to_chain,
        uint256 to_handler,
        uint256 to_token,
        uint256 to,
        uint256 amount
    ) external {
        //....
    }
```
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L115

On the destination chain (here Starknet), `to` is converted first to `felt252`, and then it is converted to `ContractAddress`.
```rust
            if self.mode.read() == SettlementMode::MintBurn{
                erc20.mint_to(u256_to_contract_address(transfer.to), transfer.amount);
            }else if self.mode.read() == SettlementMode::LockMint{
                erc20.mint_to(u256_to_contract_address(transfer.to), transfer.amount);
            }else if self.mode.read() == SettlementMode::BurnUnlock{
                token.transfer(u256_to_contract_address(transfer.to), transfer.amount);
            }else if self.mode.read() == SettlementMode::LockUnlock{
                token.transfer(u256_to_contract_address(transfer.to), transfer.amount);
            }
```
https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L126
```rust
pub fn u256_to_contract_address(contract_u256 : u256) -> ContractAddress{
    let contract_felt252: felt252 = contract_u256.try_into().unwrap();
    let contract_: ContractAddress = contract_felt252.try_into().unwrap();
    return contract_;
}
```
https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/utils.cairo#L467

The value range of type `ContractSize` is `[0, 2**251)`, so if a user sets parameter `to` more than this value, during conversion on Starknet, it panics with `Option::unwrap failed.`.
It should be implemented as:
```rust
pub fn u256_to_contract_address(contract_u256 : u256) -> Result<u8, ContractAddress>{
    let mut result: bool = false;
    let contract_felt252: felt252 = match contract_u256.try_into() {
        Option::Some(value) => value,
        Option::None => {
            result = false;
            0
        },
    };
    if(result == false){
        return Result::Err('Invalid integer');
    }
    let contract_: ContractAddress = match contract_felt252.try_into() {
        Option::Some(value) => value,
        Option::None => {
            result = false;
            0
        },
    };
    if(result == false){
        return Result::Err('Invalid integer');
    } else {
        return Result::Ok(contract_);
    }
}
```

## Issue10: Not used
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/BaseSettlementHandler.sol#L100-L111
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L27

## Issue11: hardcoded version in `codec.cairo` does not follow the to-be-encoded message

The version is hardcoded to `1` in `codec.cairo`, so it is independent of the message which is going to be encoded.
```rust
pub fn encode_message(message: Message) -> Array<u8>{
    let mut array_u8 = ArrayTrait::new();
    let version: u8 = 1;
    array_u8.append(version);
    //....
}
```
https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/codec.cairo#L95

While, the version should be encoded based on the version forwarded by the message. In other words, the version which is forwarded as parameter during `cross_chain_erc20_settlement` should be the reference. So, if `handler_erc20` is upgraded, so that its version is changed, then the encoded message will automatically uses the new version.
```rust
        fn cross_chain_erc20_settlement(ref self: ContractState, to_chain: felt252, to_handler: u256, to_token: u256, to: u256, amount: u256) -> felt252{
            //....
            let message = Message{
                version: 1,
                message_id: message_id.into(),
                payload_type: PayloadType::ERC20,
                payload: encode_transfer(transfer),
            };
            
            // send cross chain msg
            settlement.send_cross_chain_msg(to_chain, to_handler, PayloadType::ERC20, encode_message(message));
            // emit CrossChainLocked

            //...
        }
```
https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L209

### Recommended Mitigation Steps
Following is recommended:

```diff
pub fn encode_message(message: Message) -> Array<u8>{
    let mut array_u8 = ArrayTrait::new();
-    let version: u8 = 1;
-    array_u8.append(version);
+    array_u8.append(message.version);
    let message_id_array: Array<u8> = u256_to_u8_array(message.message_id);
    let mut i = 0;
    loop{
        if i > message_id_array.len() -1 {
            break;
        }
        array_u8.append(* message_id_array.span().at(i));
        i += 1;
    };
    let payload_type: u8 = message.payload_type;
    array_u8.append(payload_type);
    let mut i = 0;
    loop{
        if i > message.payload.len() -1{
            break;
        }
        array_u8.append(* message.payload.span().at(i));
        i += 1;
    };
    return array_u8;
}
```

## Issue12: If `to` on Starknet is more than 20 bytes, it reverts on EVM-based destinations
When sending a message from Starknet, the parameter `to` is of type `u256`.
https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L202
If the destination chain is EVM-based, then during casting `to` to `address`, it reverts.
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L327

## Issue13: `from_chain` is wrong when emitting `CrossChainLocked` on Starknet
When sending a message from Starknet, in the function `cross_chain_erc20_settlement`, the event `CrossChainLocked` is emitted.
```rust
            self.emit(
                    CrossChainLocked{
                        tx_id: tx_id,
                        from: get_caller_address(),
                        to: to,
                        from_chain: get_tx_info().unbox().chain_id,
                        to_chain: to_chain,
                        from_token: self.token_address.read(),
                        to_token: to_token,
                        amount: amount
                    }
                );
```
https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L219

The parameter `from_chain` is set wrongly to `get_tx_info().unbox().chain_id` while `from_chain` in all other events (including the EVM-based code) is the name of the chain, not its chain id.
https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/settlement.cairo#L304
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L216
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/ChakraSettlement.sol#L149

So, there is an inconsistency in the emitted events.

## Issue14: Zero token bridging is possible from Starknet to other chains
It is not possible to bridge 0 token from EVM-based blockchain to other blockchains because of the following restriction:
```solidity
require(amount > 0, "Amount must be greater than 0");
```
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L118

But, it is possible to bridge zero token from Starknet as this restriction is missing.
https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L167

## Issue15: Sending to address zero can be bypassed
When sending a cross chain message, there is a check that `to` to be nonzero.
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
        //....
    }
```
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L119

But if both source and destination chain are EVM-based block chains, then by setting the value of `to` equal to any value equal or higher than `2^160` (while 128-lower-bit are zero), when downcasting on the destination chain, it would discard the higher bits, and it would consider it as address zero:
```
2^^160 = 0x0000000000000000000000010000000000000000000000000000000000000000 ==> downcastin to address type = 0x00
2^^252 = 0x1000000000000000000000000000000000000000000000000000000000000000 ==> downcastin to address type = 0x00
```
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L327
```solidity
    function to_address(
        bytes32 _address
    ) internal pure returns (address result) {
        result = address(uint160(uint256(_address)));
    }
```
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/libraries/AddressCast.sol#L14

The same can happen also for the parameter `to_handler` and `to_token`.
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L113-L114
https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L120-L121

