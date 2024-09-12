# The number of validators can be set lower than required_validators

## Links to affected code

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/settlement/contracts/SettlementSignatureVerifier.sol#L143](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/settlement/contracts/SettlementSignatureVerifier.sol#L143)

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/settlement/contracts/BaseSettlement.sol#L125](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/settlement/contracts/BaseSettlement.sol#L125)

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/settlement/contracts/SettlementSignatureVerifier.sol#L66](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/settlement/contracts/SettlementSignatureVerifier.sol#L66)

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/settlement/contracts/BaseSettlement.sol#L72](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/settlement/contracts/BaseSettlement.sol#L72)

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/SettlementSignatureVerifier.sol#L96](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/SettlementSignatureVerifier.sol#L96)

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/settlement/contracts/SettlementSignatureVerifier.sol#L130](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/settlement/contracts/SettlementSignatureVerifier.sol#L130)
[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/settlement/contracts/BaseSettlement.sol#L112](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/settlement/contracts/BaseSettlement.sol#L112)
[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/SettlementSignatureVerifier.sol#L88](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/SettlementSignatureVerifier.sol#L88)
[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L225](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L225)
[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L197](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L197)

## Impact

Even if all validators unanimously agree, verification cannot be performed.

## Proof of Concept

In BaseSettlementHandler and SettlementSignatureVerifier, when setting `required_validators`, it doesn't check if this number is less than or equal to the currently set `validator_count`. If more validators are required than registered, verification cannot be performed even if all validators unanimously agree.

Additionally, when calling `remove_validator` to delete a validator, it doesn't check if `validator_count` becomes less than `required_validators`, which can cause the same issue.

The Cairo version of the Settlement contract has the same problem.

## Tools Used

Manual Review

## Recommended Mitigation Steps

Check if `required_validators` is less than or equal to `validator_count` when changing `required_validators`.

```diff
function set_required_validators_num(
    uint256 _required_validators
) external virtual onlyRole(MANAGER_ROLE) {
+   require(validator_count >= _required_validators);
    uint256 old = required_validators;
    required_validators = _required_validators;
    emit RequiredValidatorsChanged(msg.sender, old, required_validators);
}
```

When removing a validator in `remove_validator`, also check if it would make the `validator_count` less than `required_validators`.

```diff
function remove_validator(
    address validator
) external onlyRole(MANAGER_ROLE) {
    require(validators[validator] == true, "Validator does not exists");
    validators[validator] = false;
    validator_count -= 1;
+   require(validator_count >= required_validators);
    emit ValidatorRemoved(msg.sender, validator);
}
```

# DEFAULT_ADMIN_ROLE remains with the old owner after calling renounceOwnership

## Links to affected code

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/TokenRoles.sol#L27](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/TokenRoles.sol#L27)

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/TokenRoles.sol#L9](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/TokenRoles.sol#L9)

## Impact

When calling `renounceOwnership`, the DEFAULT_ADMIN_ROLE role is not removed.

## Proof of Concept

The TokenRoles contract overrides `transferOwnership` to transfer the DEFAULT_ADMIN_ROLE role when the administrator changes. However, the `renounceOwnership` function in the OwnableUpgradeable contract, which can also change the owner, is not overridden. As a result, when `renounceOwnership` is called, the DEFAULT_ADMIN_ROLE role remains.

## Tools Used

Manual Review

## Recommended Mitigation Steps

Override `renounceOwnership` to remove the DEFAULT_ADMIN_ROLE role when the owner is removed.

# Users cannot retrieve their tokens even if message processing fails on the destination chain

## Links to affected code

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/ChakraSettlementHandler.sol#L391-L393](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/ChakraSettlementHandler.sol#L391-L393)

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/handler_erc20.cairo#L138](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/handler_erc20.cairo#L138)

## Impact

Users cannot retrieve their tokens even if message processing fails on the destination chain.

## Proof of Concept

The MintBurn mode handler first locks tokens in the handler contract when sending a message, and burns the locked tokens in the callback if the message processing is successful on the destination chain.

However, when message processing fails on the destination chain, it does not return the tokens to user. As a result, users lose their tokens if message processing fails.

```solidity
function receive_cross_chain_callback(
    uint256 txid,
    string memory from_chain,
    uint256 from_handler,
    CrossChainMsgStatus status,
    uint8 /* sign_type */, // validators signature type /  multisig or bls sr25519
    bytes calldata /* signatures */
) external onlySettlement returns (bool) {
    ...

@>  if (status == CrossChainMsgStatus.Failed) {
@>      create_cross_txs[txid].status = CrossChainTxStatus.Failed;
    }

    return true;
}
```

## Tools Used

Manual Review

## Recommended Mitigation Steps

If the message fails, return the tokens to user in the callback.

```diff
function receive_cross_chain_callback(
    uint256 txid,
    string memory from_chain,
    uint256 from_handler,
    CrossChainMsgStatus status,
    uint8 /* sign_type */, // validators signature type /  multisig or bls sr25519
    bytes calldata /* signatures */
) external onlySettlement returns (bool) {
    ...

    if (status == CrossChainMsgStatus.Failed) {
        create_cross_txs[txid].status = CrossChainTxStatus.Failed;
+       return_tokens_to_user();
    }

    return true;
}
```

# Incorrect Definition of CrossChainMsgPayloadType

## Links to affected code

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L35-L42](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L35-L42)

## Impact

The PayloadType could be misinterpreted.

## Proof of Concept

When defining `CrossChainMsgPayloadType`, `BTCWithdraw` was omitted.

```rust
pub mod CrossChainMsgPayloadType {
    pub const RAW: u8 = 0;
    pub const BTCDeposit: u8 = 1;
@>  pub const BTCStake: u8 = 2;
@>  pub const BTCUnStake: u8 = 3;
@>  pub const ERC20: u8 = 4;
@>  pub const ERC721: u8 = 5;
}
```

## Tools Used

Manual Review

## Recommended Mitigation Steps

Since CrossChainMsgPayloadType is not used anywhere, either delete it or modify it correctly by adding `BTCWithdraw`.

```diff
pub mod CrossChainMsgPayloadType {
    pub const RAW: u8 = 0;
    pub const BTCDeposit: u8 = 1;
-   pub const BTCStake: u8 = 2;
-   pub const BTCUnStake: u8 = 3;
-   pub const ERC20: u8 = 4;
-   pub const ERC721: u8 = 5;
+   pub const BTCWithdraw: u8 = 2;
+   pub const BTCStake: u8 = 3;
+   pub const BTCUnStake: u8 = 4;
+   pub const ERC20: u8 = 5;
+   pub const ERC721: u8 = 6;
}
```

# Possibility of reentrancy/replay attacks in Starknet's receive_cross_chain_callback

## Links to affected code

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/handler_erc20.cairo#L138-L145](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/handler_erc20.cairo#L138-L145)

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L409-L421](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L409-L421)

## Impact

There is a possibility of reentrancy and replay attacks.

## Proof of Concept

In Starknet, the `Handler.receive_cross_chain_callback` function does not check if the transaction is in a Pending state. Therefore, there is a possibility of reentrancy attacks or function recall attacks.

Additionally, since the CEI pattern is not applied (updating `created_tx` at the end), there is a possibility of reentrancy attacks even if the Pending state is checked.

```rust
fn receive_cross_chain_callback(ref self: ContractState, cross_chain_msg_id: felt252, from_chain: felt252, to_chain: felt252,
from_handler: u256, to_handler: ContractAddress, cross_chain_msg_status: u8) -> bool{
@>  assert(to_handler == get_contract_address(),'error to_handler');

@>  assert(self.settlement_address.read() == get_caller_address(), 'not settlement');

@>  assert(self.support_handler.read((from_chain, from_handler)) && 
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

`Settlement.receive_cross_chain_callback` is also vulnerable to reentrancy attacks as it does not apply the CEI pattern.

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
      assert(self.created_tx.read(cross_chain_msg_id).tx_id == cross_chain_msg_id, 'message id error');
      assert(self.created_tx.read(cross_chain_msg_id).from_chain == to_chain, 'from_chain error');
      assert(self.created_tx.read(cross_chain_msg_id).to_chain == from_chain, 'to_chain error');
      assert(self.created_tx.read(cross_chain_msg_id).from_handler == to_handler, 'from_handler error');
      assert(self.created_tx.read(cross_chain_msg_id).to_handler == from_handler, 'to_handler error');
@>    assert(self.created_tx.read(cross_chain_msg_id).tx_status == CrossChainMsgStatus::PENDING, 'tx status error');

      let mut message_hash_temp: felt252 = LegacyHash::hash(from_chain, (cross_chain_msg_id, to_chain, from_handler, to_handler));
      let message_hash_final:felt252 = LegacyHash::hash(message_hash_temp, cross_chain_msg_status);
      self.check_chakra_signatures(message_hash_final, signatures);
      let handler = IHandlerDispatcher{contract_address: to_handler};
@>    let success = handler.receive_cross_chain_callback(cross_chain_msg_id, from_chain, to_chain, from_handler, to_handler , cross_chain_msg_status);
      let mut state = CrossChainMsgStatus::PENDING;
      if success{
          state = CrossChainMsgStatus::SUCCESS;
      }else{
          state = CrossChainMsgStatus::FAILED;
      }
      
@>    self.created_tx.write(cross_chain_msg_id, CreatedTx{
          tx_id:cross_chain_msg_id,
          tx_status:state,
          from_chain: to_chain,
          to_chain: from_chain,
          from_handler: to_handler,
          to_handler: from_handler
      });

      self.emit(CrossChainResult {
          cross_chain_settlement_id: cross_chain_msg_id,
          from_address: get_tx_info().unbox().account_contract_address,
          from_chain: to_chain,
          from_handler: to_handler,
          to_chain: from_chain,
          to_handler: from_handler,
          cross_chain_msg_status: state,
      });
      return true;
  }
```

## Tools Used

Manual Review

## Recommended Mitigation Steps

1. Check if the `tx_status` is in a Pending state in `Handler.receive_cross_chain_callback`.
2. Apply the CEI pattern in `Handler.receive_cross_chain_callback` to prevent reentrancy.
3. In `Settlement.receive_cross_chain_callback`, first store the `tx_status` as Failed, then call `Handler.receive_cross_chain_callback`, and finally store the result. This applies the CEI pattern to prevent reentrancy.

# Emitting an event using unverified parameter `payload_type`

## Links to affected code

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L340](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L340)

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L380](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L380)

## Impact

Can emit event with wrong information.

## Proof of Concept

An event is emitted using an unverified parameter `payload_type`.

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
@>  payload_type: u8,
) -> bool {
    assert(to_chain == self.chain_name.read(), 'error to_chain');

    // verify signatures
@>  let mut message_hash: felt252 = LegacyHash::hash(from_chain, (cross_chain_msg_id, to_chain, from_handler, to_handler));
    let payload_span = payload.span();
    let mut i = 0;
    loop {
        if i > payload_span.len()-1{
            break;
        }
        message_hash = LegacyHash::hash(message_hash, * payload_span.at(i));
        i += 1;
    };
    self.check_chakra_signatures(message_hash, signatures);

    ...

    // emit event
    self.emit(CrossChainHandleResult{
        cross_chain_settlement_id: cross_chain_msg_id,
        from_chain: to_chain,
        from_handler: to_handler,
        to_chain: from_chain,
        to_handler: from_handler,
        cross_chain_msg_status: status,
@>      payload_type: payload_type
    });
    return true;
}
```

## Tools Used

Manual Review

## Recommended Mitigation Steps

Use the parsed value of the payload instead of the `payload_type` parameter.

# Delete unused TxStatus enum

## Links to affected code

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/constant.cairo#L18](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/constant.cairo#L18)

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/ChakraSettlementHandler.sol#L27](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/ChakraSettlementHandler.sol#L27)

## Impact

There is an unused enum.

## Proof of Concept

The `TxStatus` enum is defined but not used anywhere.

## Tools Used

Manual Review

## Recommended Mitigation Steps

Delete the unused `TxStatus` enum.

# Tokens can be stolen by front-running required_validators_num initialization

## Links to affected code

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L178-L189](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L178-L189)

[https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L162-L166](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L162-L166)

## Impact

If the handler is set before`required_validators_num`is initialized, it's possible to call`Settlement.receive_cross_chain_msg`with dummy signatures, bypassing the Validator signatures check and receiving tokens.

## Proof of Concept

When verifying signatures with `Settlement.check_chakra_signatures` on Starknet, if `required_validators_num` is 0, the function will process normally with dummy `signatures`. (In the case of EVM contracts, signatures check is not passed when `required_validators_num` is 0.)

```rust
fn check_chakra_signatures(
    self: @ContractState, message_hash: felt252, signatures: Array<(felt252, felt252, bool)>
){
    let mut pass_count = 0;
    let mut i = 0;
    loop {
@>      if i > signatures.len()-1{
            break;
        }
        let (r,s,y) = * signatures.at(i);
        let pub_key: felt252 = recover_public_key(message_hash,r,s,y).unwrap();
        if self.chakra_validators_pubkey.read(pub_key) > 0{
            pass_count += 1;
        }
        i += 1;
    };
@>  assert(pass_count >= self.required_validators_num.read(), 'Not enough validate signatures');
}
```

The constructor of Settlement does not initialize `required_validators_num`. Therefore, the initial value of `required_validators_num` is 0.

```rust
#[constructor]
fn constructor(ref self: ContractState, owner: ContractAddress, chain_name: felt252) {
    self.ownable.initializer(owner);
    self.chakra_managers.write(owner, 1);
    self.chain_name.write(chain_name);
}
```

If the handler is set before `required_validators_num` is initialized, it's possible to call `Settlement.receive_cross_chain_msg` with dummy signatures, bypassing the Validator signatures check and receiving tokens.

## Tools Used

Manual Review

## Recommended Mitigation Steps

Initialize `required_validators_num` in the constructor.