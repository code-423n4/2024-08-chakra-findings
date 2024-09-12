# <p align="center"><strong>QA Report</strong></p>

## summary

| Issue ID | Issue Title                                                                                   |
|--------------|-----------------------------------------------------------------------------------------------|
| 01         | The CreatedCrossChainTx parameter is stored incorrectly                                       |
| 02         | The CrossChainLocked event parameters are incorrect                                          |
| 03         | When sending cross-chain messages, check whether the to_handler is on the whitelist.        |
| 04         | An increase in PayloadType can trigger unnecessary changes in the contract state.           |
| 05         | Not checking the allowance before the transfer        |
| 06         | The Cairo program does not check the cross-chain transfer amount         |
| 07        | The receive_cross_chain_msg function will never return false                 |
| 08         | The receive_cross_chain_callback will not return false                      |
| 09 | Improper Manager Permission Control|



## [01] The CreatedCrossChainTx parameter is stored incorrectly
### Link
github:[https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L160](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L160)
github:[https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/BaseSettlementHandler.sol#L59](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/BaseSettlementHandler.sol#L59)
### Description
The `ChakraSettlementHandler` contract incorrectly stores the `from_token` parameter when sending cross-chain messages and recording `CreatedCrossChainTx`. This misstorage creates inconveniences for off-chain tracking and operations.
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
```solidity
    /**
     * @dev Initiates a cross-chain ERC20 settlement
     * @param to_chain The destination chain
     * @param to_handler The destination handler
     * @param to_token The destination token
     * @param to The recipient address
     * @param amount The amount to transfer
     */
    function cross_chain_erc20_settlement(
        string memory to_chain,
        uint256 to_handler,
        uint256 to_token,
        uint256 to,
        uint256 amount
    ) external {
        ...

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

        ...
    }
```
### Recommendation
Correctly record the `from_token` field
```diff

    function cross_chain_erc20_settlement(
        string memory to_chain,
        uint256 to_handler,
        uint256 to_token,
        uint256 to,
        uint256 amount
    ) external {
        ...

        {
            // Save the cross chain tx
            create_cross_txs[txid] = CreatedCrossChainTx(
                txid,
                chain,
                to_chain,
                msg.sender,
                to,
-               address(this),
+               address(token),
                to_token,
                amount,
                CrossChainTxStatus.Pending
            );
        }

        ...
    }
```

## [02] The CrossChainLocked event parameters are incorrect
### Link
github:[https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L218](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L218)
github:[https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/BaseSettlementHandler.sol#L47](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/BaseSettlementHandler.sol#L47)
### Description
When the `CrossChainLocked` event is triggered, the `from_token` is incorrectly set to `address(this)`. Events in cross-chain applications are crucial as they serve as important references for off-chain program execution. This issue may cause some inconvenience for off-chain systems.
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
```solidity
    /**
     * @dev Initiates a cross-chain ERC20 settlement
     * @param to_chain The destination chain
     * @param to_handler The destination handler
     * @param to_token The destination token
     * @param to The recipient address
     * @param amount The amount to transfer
     */
    function cross_chain_erc20_settlement(
        string memory to_chain,
        uint256 to_handler,
        uint256 to_token,
        uint256 to,
        uint256 amount
    ) external {
        ...

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
    }
```
### Recommendation
Correctly set the `from_token` field
```diff
    function cross_chain_erc20_settlement(
        string memory to_chain,
        uint256 to_handler,
        uint256 to_token,
        uint256 to,
        uint256 amount
    ) external {
        ...

        emit CrossChainLocked(
            txid,
            msg.sender,
            to,
            chain,
            to_chain,
-           address(this),
+           address(token),
            to_token,
            amount,
            mode
        );
    }
```
## [03] When sending cross-chain messages, check whether the to_handler is on the whitelist.
### Link
github:[https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L111](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L111)
### Description
When sending cross-chain requests to the target chain, the validity of `to_handler` is not checked. By verifying `to_handler`, it can reduce the occurrence of erroneous message calls and the triggering of incorrect events.  
Additionally, the system currently lacks a robust mechanism for handling refunds in the event of cross-chain message execution failures. Therefore, it is even more crucial to perform parameter validity checks.  
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
        
        ...
    }
```
### Recommendation
Check whether `to_handler` is in the whitelist, as messages will definitely fail if the `to_handler` is not whitelisted.  
```diff
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
+       require(is_valid_handler(to_chain, to_handler), "Invalid target address");
        ...
    }
```


## [04] An increase in `PayloadType` can allow malicious actors to manipulate the `receive_cross_chain_msg` function.
### Link
github:[https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/settlement/contracts/ChakraSettlement.sol#L183](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/settlement/contracts/ChakraSettlement.sol#L183)
github:[https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L286](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L286)
### Description

The receive_cross_chain_msg function does not verify `payload_type` during signature verification.  
```solidity
    /**
     * @dev Function to receive cross-chain message
     * @param txid The transaction id
     * @param from_chain The chain the message is from
     * @param from_address The address the message is from
     * @param from_handler The handler the message is from
     * @param to_handler The handler to handle the message
     * @param payload_type The type of the payload
     * @param payload The payload of the message
     * @param sign_type The type of the signature
     * @param signatures The signatures of the message
     */
    function receive_cross_chain_msg(
        uint256 txid,
        string memory from_chain,
        uint256 from_address,
        uint256 from_handler,
        address to_handler,
        PayloadType payload_type,
        bytes calldata payload,
        uint8 sign_type, // validators signature type /  multisig or bls sr25519
        bytes calldata signatures // signature array
    ) external {
        {
            // verify signature
            bytes32 message_hash = keccak256(
                abi.encodePacked(
                    txid,
                    from_chain,
                    from_address,
                    from_handler,
                    to_handler,
                    keccak256(payload)
                )
            );

            require(
                signature_verifier.verify(message_hash, signatures, sign_type),
                "Invalid signature"
            );

            ...
    }

```

In the current system, this does not pose a risk because the only valid `payload_type` is `PayloadType.ERC20`.  
Therefore, any input that is not `PayloadType.ERC20` will cause the transaction to revert, so there is no risk of attackers manipulating the `PayloadType`.  
```solidity
    /**
     * @dev Checks if the payload type is valid
     * @param payload_type The payload type to check
     * @return bool True if valid, false otherwise
     */
    function isValidPayloadType(
        PayloadType payload_type
    ) internal pure returns (bool) {
        return (payload_type == PayloadType.ERC20);
    }
```
However, as the number of acceptable `PayloadType` values increases, malicious actors could preemptively craft inputs with different `PayloadType` values to bypass the validation in `receive_cross_chain_msg`, potentially manipulating transactions.  
### Recommendation
It is recommended to include `PayloadType` in the signed message. This ensures that the `receive_cross_chain_msg` function can validate the `PayloadType` and prevent unauthorized manipulation or invalid payloads from affecting transaction integrity.  
```diff
    function receive_cross_chain_msg(
        uint256 txid,
        string memory from_chain,
        uint256 from_address,
        uint256 from_handler,
        address to_handler,
        PayloadType payload_type,
        bytes calldata payload,
        uint8 sign_type, // validators signature type /  multisig or bls sr25519
        bytes calldata signatures // signature array
    ) external {
        {
            // verify signature
            bytes32 message_hash = keccak256(
                abi.encodePacked(
                    txid,
                    from_chain,
                    from_address,
                    from_handler,
                    to_handler,
+                   payload_type
                    keccak256(payload)
                )
            );

            require(
                signature_verifier.verify(message_hash, signatures, sign_type),
                "Invalid signature"
            );

            ...
    }
```

## [05] Not checking the allowance before the transfer
### Link
github:[https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L257](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L257)

### Description
The README file states:
  
"The contract must ensure sufficient token balance before performing transfers, burns, or unlocks. The contract uses a secure transfer method to transfer tokens and checks the balance before the transfer."  
  
However, when the contract uses `transferFrom` to transfer tokens on behalf of someone else, it only checks the balance of `from` and does not verify if the `allowance` is sufficient. In this case, even if `from` has enough balance, the transfer may still fail if the allowance is insufficient.  
```solidity
    function _safe_transfer_from(
        address from,
        address to,
        uint256 amount
    ) internal {
        require(
            IERC20(token).balanceOf(from) >= amount,
            "Insufficient balance"
        );

        // transfer tokens
        IERC20(token).transferFrom(from, to, amount);
    }
```

### Recommendation
Perform the check of allowance before the transfer
```diff
    function _safe_transfer_from(
        address from,
        address to,
        uint256 amount
    ) internal {
        require(
            IERC20(token).balanceOf(from) >= amount,
            "Insufficient balance"
        );
+       require(
+           IERC20(token).allowance(from, address(this)) >= amount,
+           "Insufficient allowance"
+       );
        // transfer tokens
        IERC20(token).transferFrom(from, to, amount);
    }
```
## [06] The Cairo program does not check the cross-chain transfer amount
### Link
github:[https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/handler_erc20.cairo#L167](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/handler_erc20.cairo#L167)
### Description
The README file mentions that cross-chain ERC20 settlements can only be initiated with a valid amount (greater than 0), a valid recipient address, a valid handler address, and a valid token address.  
However, the Cairo program does not check whether the amount is valid (greater than 0) when sending cross-chain transactions.  
```rust
        fn cross_chain_erc20_settlement(ref self: ContractState, to_chain: felt252, to_handler: u256, to_token: u256, to: u256, amount: u256) -> felt252{
            assert(self.support_handler.read((to_chain, to_handler)), 'not support handler');
            ...
        }
```
This allows malicious actors to send a large number of invalid transactions, thereby increasing the network's burden.
### Recommendation
Check if the `amount` is greater than 0.
```diff
        fn cross_chain_erc20_settlement(ref self: ContractState, to_chain: felt252, to_handler: u256, to_token: u256, to: u256, amount: u256) -> felt252{
            assert(self.support_handler.read((to_chain, to_handler)), 'not support handler');
+           assert(amount > 0, 'Amount must be greater than 0')
            ...
        }
```

## [07] The receive_cross_chain_msg function will never return false
## Link
github:[https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/settlement.cairo#L354](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/settlement.cairo#L354)
github:[https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/handler_erc20.cairo#L108C12-L108C35](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/handler_erc20.cairo#L108C12-L108C35)
### Description
When a cross-chain message is received, the settlement contract calls the `receive_cross_chain_msg` function of the `handler_erc20` to process the message. The execution status is set based on the result of `receive_cross_chain_msg`: if `receive_cross_chain_msg` returns `true`, the status is set to success; if it returns `false`, the status is set to failure.
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
               
            ...
            // call handler receive_cross_chain_msg
            let handler = IHandlerDispatcher{contract_address: to_handler};
            let success = handler.receive_cross_chain_msg(cross_chain_msg_id, from_chain, to_chain, from_handler, to_handler , payload);

            let mut status = CrossChainMsgStatus::SUCCESS;
            if success{
                status = CrossChainMsgStatus::SUCCESS;
            }else{
                status = CrossChainMsgStatus::FAILED;
            }

            self.received_tx.write(cross_chain_msg_id, ReceivedTx{
                tx_id:cross_chain_msg_id,
                from_chain: from_chain,
                from_handler: from_handler,
                to_chain: to_chain,
                to_handler: to_handler,
                tx_status: status
            });

            ...
        }
```
However, the `receive_cross_chain_msg` function will never return false.
If an error occurs, it will cause a revert.
```rust
       fn receive_cross_chain_msg(ref self: ContractState, cross_chain_msg_id: u256, from_chain: felt252, to_chain: felt252,
        from_handler: u256, to_handler: ContractAddress, payload: Array<u8>) -> bool{
            assert(to_handler == get_contract_address(),'error to_handler');

            assert(self.settlement_address.read() == get_caller_address(), 'not settlement');

            assert(self.support_handler.read((from_chain, from_handler)) && 
                    self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');

            let message :Message= decode_message(payload);
            let payload_type = message.payload_type;
            assert(payload_type == PayloadType::ERC20, 'payload type not erc20');
            let payload_transfer = message.payload;
            let transfer = decode_transfer(payload_transfer);
            assert(transfer.method_id == ERC20Method::TRANSFER, 'ERC20Method must TRANSFER');
            let erc20 = IERC20MintDispatcher{contract_address: self.token_address.read()};
            let token = IERC20Dispatcher{contract_address: self.token_address.read()};
            if self.mode.read() == SettlementMode::MintBurn{
                erc20.mint_to(u256_to_contract_address(transfer.to), transfer.amount);
            }else if self.mode.read() == SettlementMode::LockMint{
                erc20.mint_to(u256_to_contract_address(transfer.to), transfer.amount);
            }else if self.mode.read() == SettlementMode::BurnUnlock{
                token.transfer(u256_to_contract_address(transfer.to), transfer.amount);
            }else if self.mode.read() == SettlementMode::LockUnlock{
                token.transfer(u256_to_contract_address(transfer.to), transfer.amount);
            }
            
            return true;
        }
```
This means that the cross-chain message status will never be set to failure. In such cases, the message might get stuck and never execute, potentially leading to loss of user funds.
### Recommendation
It is recommended to return `false` for permanent failures during message execution instead of reverting the transaction.

```diff
       fn receive_cross_chain_msg(ref self: ContractState, cross_chain_msg_id: u256, from_chain: felt252, to_chain: felt252,
        from_handler: u256, to_handler: ContractAddress, payload: Array<u8>) -> bool{
            assert(to_handler == get_contract_address(),'error to_handler');

            assert(self.settlement_address.read() == get_caller_address(), 'not settlement');

-           assert(self.support_handler.read((from_chain, from_handler)) && 
-                  self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');
+           if(!self.support_handler.read((from_chain, from_handler) || !self.support_handler.read((to_chain, contract_address_to_u256(to_handler)))) {
+               return false;
+           }
            let message :Message= decode_message(payload);
            let payload_type = message.payload_type;
            assert(payload_type == PayloadType::ERC20, 'payload type not erc20');
            let payload_transfer = message.payload;
            let transfer = decode_transfer(payload_transfer);
            assert(transfer.method_id == ERC20Method::TRANSFER, 'ERC20Method must TRANSFER');
            let erc20 = IERC20MintDispatcher{contract_address: self.token_address.read()};
            let token = IERC20Dispatcher{contract_address: self.token_address.read()};
            if self.mode.read() == SettlementMode::MintBurn{
                erc20.mint_to(u256_to_contract_address(transfer.to), transfer.amount);
            }else if self.mode.read() == SettlementMode::LockMint{
                erc20.mint_to(u256_to_contract_address(transfer.to), transfer.amount);
            }else if self.mode.read() == SettlementMode::BurnUnlock{
                token.transfer(u256_to_contract_address(transfer.to), transfer.amount);
            }else if self.mode.read() == SettlementMode::LockUnlock{
                token.transfer(u256_to_contract_address(transfer.to), transfer.amount);
            }
            
            return true;
        }
```


## [08]The receive_cross_chain_callback will not return false
### Link
github:[https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/settlement.cairo#L393](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/settlement.cairo#L393)
github:[https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/handler_erc20.cairo#L138](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/handler_erc20.cairo#L138)
### Description
When a cross-chain message callback is triggered, the settlement contract calls the `receive_cross_chain_callback` function of `handler_erc20` to handle the callback. The execution status is determined based on the result of `receive_cross_chain_callback`: if it returns `true`, the status is set to success; if it returns `false`, the status is set to failure.
```rust
        fn receive_cross_chain_callback(
            ref self: ContractState,
            cross_chain_msg_id: felt252,
            from_chain: felt252,
            to_chain: felt252,
            from_handler: u256,
            to_handler: ContractAddress,
            cross_chain_msg_status: u8,
            sign_type: u8,
            signatures: Array<(felt252, felt252, bool)>,
        ) -> bool {
            ...
            let handler = IHandlerDispatcher{contract_address: to_handler};
            let success = handler.receive_cross_chain_callback(cross_chain_msg_id, from_chain, to_chain, from_handler, to_handler , cross_chain_msg_status);
            let mut state = CrossChainMsgStatus::PENDING;
            if success{
                state = CrossChainMsgStatus::SUCCESS;
            }else{
                state = CrossChainMsgStatus::FAILED;
            }
            
            self.created_tx.write(cross_chain_msg_id, CreatedTx{
                tx_id:cross_chain_msg_id,
                tx_status:state,
                from_chain: to_chain,
                to_chain: from_chain,
                from_handler: to_handler,
                to_handler: from_handler
            });

            ...
            return true;
        }
```

However, the receive_cross_chain_callback function will never return false. If an error is encountered, it will cause a revert instead.
```rust
        fn receive_cross_chain_callback(ref self: ContractState, cross_chain_msg_id: felt252, from_chain: felt252, to_chain: felt252,
        from_handler: u256, to_handler: ContractAddress, cross_chain_msg_status: u8) -> bool{
            assert(to_handler == get_contract_address(),'error to_handler');

            assert(self.settlement_address.read() == get_caller_address(), 'not settlement');

-           assert(self.support_handler.read((from_chain, from_handler)) && 
-                  self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');
+           if(!self.support_handler.read((from_chain, from_handler) || !self.support_handler.read((to_chain, contract_address_to_u256(to_handler)))) {
+               return false;
+           }

            let erc20 = IERC20MintDispatcher{contract_address: self.token_address.read()};
            if self.mode.read() == SettlementMode::MintBurn{
                erc20.burn_from(get_contract_address(), self.created_tx.read(cross_chain_msg_id).amount);
            }
            let created_tx = self.created_tx.read(cross_chain_msg_id);
            self.created_tx.write(cross_chain_msg_id, CreatedCrossChainTx{
                tx_id: created_tx.tx_id,
                from_chain: created_tx.from_chain,
                to_chain: created_tx.to_chain,
                from:created_tx.from,
                to:created_tx.to,
                from_token: created_tx.from_token,
                to_token: created_tx.to_token,
                amount: created_tx.amount,
                tx_status: CrossChainTxStatus::SETTLED
            });

            return true;
        }
```
This means that exceptions in the cross-chain callback checks will not set the message status to failure. As a result, the message might get stuck and never execute, potentially leading to a loss of user funds.

### Recommendation
It is recommended to return `false` for permanent failures during message execution instead of reverting the transaction.
```diff
        fn receive_cross_chain_callback(ref self: ContractState, cross_chain_msg_id: felt252, from_chain: felt252, to_chain: felt252,
        from_handler: u256, to_handler: ContractAddress, cross_chain_msg_status: u8) -> bool{
            assert(to_handler == get_contract_address(),'error to_handler');

            assert(self.settlement_address.read() == get_caller_address(), 'not settlement');

            assert(self.support_handler.read((from_chain, from_handler)) && 
                    self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');

            let erc20 = IERC20MintDispatcher{contract_address: self.token_address.read()};
            if self.mode.read() == SettlementMode::MintBurn{
                erc20.burn_from(get_contract_address(), self.created_tx.read(cross_chain_msg_id).amount);
            }
            let created_tx = self.created_tx.read(cross_chain_msg_id);
            self.created_tx.write(cross_chain_msg_id, CreatedCrossChainTx{
                tx_id: created_tx.tx_id,
                from_chain: created_tx.from_chain,
                to_chain: created_tx.to_chain,
                from:created_tx.from,
                to:created_tx.to,
                from_token: created_tx.from_token,
                to_token: created_tx.to_token,
                amount: created_tx.amount,
                tx_status: CrossChainTxStatus::SETTLED
            });

            return true;
        }
```

## [09] Improper Manager Permission Control
### Link
github:[https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/settlement.cairo#L246](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/settlement.cairo#L246)
### Description
There are issues with manager permission control; a manager can add new managers and also remove other managers.  
This issue means that if a manager adds a malicious manager, this malicious manager could remove all other managers, including themselves. As a result, there would be no managers left in the system, making it impossible to add new managers.  
```rust
        // Managers related operations
        fn add_manager(ref self: ContractState, new_manager: ContractAddress) -> bool {
            let caller = get_caller_address();
            assert(self.chakra_managers.read(caller) == 1, 'Caller is not a manager');
            assert(caller != new_manager, 'Caller is a manager already');
            self.chakra_managers.write(new_manager, 1);
            self
                .emit(
                    ManagerAdded {
                        operator: caller, new_manager: new_manager, added_at: get_block_timestamp()
                    }
                );
            return self.chakra_managers.read(new_manager) == 1;
        }

        fn remove_manager(ref self: ContractState, old_manager: ContractAddress) -> bool {
            let caller = get_caller_address();
            assert(self.chakra_managers.read(caller) == 1, 'Caller is not a manager');
            self.chakra_managers.write(old_manager, 0);
            self
                .emit(
                    ManagerRemoved {
                        operator: caller,
                        old_manager: old_manager,
                        removed_at: get_block_timestamp()
                    }
                );
            return self.chakra_managers.read(old_manager) == 0;
        }
```

### Recommendation
Assign the authority to add and remove managers to a higher-level owner rather than to peers at the same manager level  