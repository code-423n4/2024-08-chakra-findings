## 1. Malicious Users can create DoS Chakra Validators with invalid cross-chain msgs

### Vulnerability
When a user sends a cross chain trx by invoking `cross_chain_erc20_settlement()`, the function first locks (or burns) users' tokens and then calls settlement contract's `send_cross_chain_msg()` function, which further emits an event `CrossChainMsg`. 

The chakra validators pick these `CrossChainMsg` event and then base on that call the receiving function on the destination chain.

The `send_cross_chain_msg()` is meant to be only called by valid handler contracts but it can be invoked by anyone!

Means malicious users can directly invoke `send_cross_chain_msg()` and emit many fake or malicious `CrossChainMsg` events, which will gonna create a lot of traffic for the chakra validators which will create a DoS for the valid cross chain msgs.

##### Tools Used
[Shaheen's Analysis](https://x.com/0x_Shaheen/status/1722664258142650806)

### Recommended Mitigation Steps
Implement Strict access control on the `send_cross_chain_msg()` function, by allowing only handler's ability to call it.

## 2. `MintBurn` mode, tokens burning discrepancy

### Vulnerability
In the `MintBurn` mode, the tokens get burned in the end when `receive_cross_chain_callback()` function gets processed. As the protocol have two implementations contracts, one for the EVM chains (in solidity) and one for Starknet (in cairo), surprisingly the burning mechanism in both of them differs.
In solidity instance, the tokens only get burned when the CrossChainMsgStatus is `SUCCESS`:
```solidity
        if (status == CrossChainMsgStatus.Success) {
            if (mode == SettlementMode.MintBurn) {
                _erc20_burn(address(this), create_cross_txs[txid].amount);
            }

            create_cross_txs[txid].status = CrossChainTxStatus.Settled;
        }
``` 
But in the cairo instance, the tokens get burned anyway, not depending on the tx_status:
```cairo
            if self.mode.read() == SettlementMode::MintBurn{
                erc20.burn_from(get_contract_address(), self.created_tx.read(cross_chain_msg_id).amount);
            }
```
### Recommended Mitigation Steps
The protocol dev team really needs to review this, to make sure that the mechanism is same across implmentations. I believe the solidity one is correct (it makes sense), so cairo one should be changed.

## 3. Cairo contracts are using vulnerable OpenZeppelin contracts version.
### Vulnerability
The cairo contracts uses OZ's `0.14.0` version (esp `OwnableComponent`), which had a vulnerability, which got fixed recently in `0.16.0` release. 

OZ's `OwnableComponent` was vulnerable to late ownership overwrites, which used to not allow pending owners to accept ownership if the prev owner had renounce their ownership: https://github.com/OpenZeppelin/cairo-contracts/releases/tag/v0.16.0

### Recommended Mitigation Steps
Upgrade OZ's version to `0.16.0

## 4. Safe Transfer Invariant Compromised

### Vulnerability
According to the project Readme, one of the invariants of protocol is this:
> The contract uses safe transfer methods to move tokens, checking balances before transfers

This is correctly implemented in the solidity instance but in cairo instance this is compromised/broken.

The cairo instance directly transfers the tokens without making sure the token balances:
```cairo
            }else if self.mode.read() == SettlementMode::BurnUnlock{
                ///@audit-issue L invariant broke: "The contract uses safe transfer methods to move tokens, checking balances before transfers."
                token.transfer(u256_to_contract_address(transfer.to), transfer.amount);
            }else if self.mode.read() == SettlementMode::LockUnlock{
                token.transfer(u256_to_contract_address(transfer.to), transfer.amount);
            }
```

### Recommended Mitigation Steps
Implement the invariant in the cairo instance as well

## 5. `ecdsa.recover_public_key`'s return value, zero check missing
### Vulnerability
The `check_chakra_signatures` function uses escda's `recover_public_key` functionality to recover public keys, but it doesn't check for the return values. Assuming that this work just like `ecrecover`, that means checking that return value is not zero is quite important
```cairo
        fn check_chakra_signatures(
            self: @ContractState, message_hash: felt252, signatures: Array<(felt252, felt252, bool)>
        ){
            let mut pass_count = 0;
            let mut i = 0;
            loop {
                if i > signatures.len()-1{
                    break;
                }
                let (r,s,y) = * signatures.at(i);
                ///@audit-issue L return value zero not checked!
                let pub_key: felt252 = recover_public_key(message_hash,r,s,y).unwrap();
                if self.chakra_validators_pubkey.read(pub_key) > 0{
                    pass_count += 1;
                }
                i += 1;
            };
            assert(pass_count >= self.required_validators_num.read(), 'Not enough validate signatures');
        }
```
### Recommended Mitigation Steps
```diff
                let pub_key: felt252 = recover_public_key(message_hash,r,s,y).unwrap();
+               assert(pub_key != 0, 'Not validate pub key');
```


## 6. `sign_type` check ignored!

### Vulnerability
The cairo instance ignore the `sign_type`, it doesn't make sure that it is passed correctly like the solidity instance:
```solidity
    function verify(
        bytes32 msgHash,
        bytes calldata signatures,
        uint8 sign_type
    ) external view returns (bool) {
        if (sign_type == 0) {
            return verifyECDSA(msgHash, signatures);
        } else {
            return false;
        }
    }
```

### Recommended Mitigation Steps
Don't ignore, it looks quite important

## 7. Signed data is different for EVM and Starknet
### Vulnerability
The signed data variables on Starknet is this:
```cairo
            let mut message_hash: felt252 = LegacyHash::hash(from_chain, (cross_chain_msg_id, to_chain, from_handler, to_handler));
            let payload_span = payload.span();
            let mut i = 0;
            loop {
                if i > payload_span.len()-1{
                    break;
                }
                message_hash = LegacyHash::hash(message_hash, * payload_span.at(i));
                i += 1;
            };
```
But on the EVM, it is this:
```solidity
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
```

it can be a bit problematic to cross-chain msgs between starknet and evm chains, signatures might not work as the data differs.

### Recommended Mitigation Steps
Make sure to have a consistent data vars

## 8. Starknet Field Prime check missing in the `cross_chain_erc20_settlement()`

### Vulnerability
In Starknet, addresses are of the felt type, while on L1 addresses are of the uint160 type. To pass address types during cross-layer messaging, the address variable is typically given as a uint256. However, this may create an issue where an address on L1 maps to the zero address (or an unexpected address) on L2. This is because the primitive type in Cairo is the felt, which lies within the range 0 < x < P, where P is the prime order of the curve. Usually, we have P = 2^251 + 17 * 2^192 + 1.

When sending a message from EVM to Starknet it is important to ensure verification of parameters. 

### Recommended Mitigation Steps
Add this check:
```solidity
require(to != 0 && to < STARKNET_FIELD_PRIME, "invalid address"); // verifies 0 < to < P
```

## 9. `receive_cross_chain_callback` input validations missing
### Vulnerability
The solidity instance's `receive_cross_chain_callback()` is missing some important input validations like cairo instance:
```cairo
            assert(self.created_tx.read(cross_chain_msg_id).tx_id == cross_chain_msg_id, 'message id error');
            assert(self.created_tx.read(cross_chain_msg_id).from_chain == to_chain, 'from_chain error');
            assert(self.created_tx.read(cross_chain_msg_id).to_chain == from_chain, 'to_chain error');
            assert(self.created_tx.read(cross_chain_msg_id).from_handler == to_handler, 'from_handler error');
            assert(self.created_tx.read(cross_chain_msg_id).to_handler == from_handler, 'to_handler error');

```
### Recommended Mitigation Steps
Make sure to add all the important input validations

## 10. `cross_chain_erc20_settlement()` doesn't check that valid handler is given
The solidity instance of  `cross_chain_erc20_settlement()` doesn't check that valid handler is given like in cairo.
```solidity
    function cross_chain_erc20_settlement(
        string memory to_chain,
        uint256 to_handler,
        uint256 to_token,
        uint256 to,
        uint256 amount
    ) external {
        ///@audit-issue L valid handler check missing
        .....
    }
```
### Recommended Mitigation Steps
Implement that check like its implemented in cairo:
```cairo
           assert(self.support_handler.read((to_chain, to_handler)), 'not support handler');
```
