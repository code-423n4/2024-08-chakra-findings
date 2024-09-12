## [QA-1]: Consider allow specifying managers to the `initialize` function for the `SettlementSignatureVerifier`

Consider allow specifying an array of managers in the `initialize` function to grant the `MANAGER_ROLE` roles to in the `SettlementSignatureVerifier` contract.

```solidity
    /**
     * @dev Function to initialize the verifier
     * @notice Initializes the verifier with owner and required validators
     * @param _owner The owner of the contract
     * @param _required_validators The number of required validators
     */
    function initialize(
        address _owner,
        uint256 _required_validators
    ) public initializer {
        __Ownable_init(_owner);
        __UUPSUpgradeable_init();
        _grantRole(DEFAULT_ADMIN_ROLE, _owner);

        required_validators = _required_validators;
    }
```

## [QA-2] Incorrect type during decoding of `_msg.id`

In `MessageV1Codec.sol`, an incorrect type of `uint64` is used when decoding `id` from the payload.

```solidity
    function id(bytes calldata _msg) internal pure returns (uint64) {
        return uint64(bytes8(_msg[ID_OFFSET:PAYLOAD_TYPE_OFFSET]));
    }
```

The correct type is `uint256` as per the struct:

```solidity
// The Message struct defines the message of corss chain
struct Message {
    // The id of the message
    uint256 id;
    // The type of the payload
    PayloadType payload_type;
    // The payload of the message
    bytes payload;
}
```

## [QA-3]: Incorrect `from_address` can be emitted by the `CrossChainResult` event

In the `CrossChainResult` event, an incorrect `from_address` can be emitted. This is because `get_tx_info().unbox().account_contract_address` is equivalent to `tx.origin`


What this means is that it is possible for another user to provide the required signatures for the `receive_cross_chain_callback`, such that the `get_tx_info().unbox().account_contract_address` is no longer the true `from_address` of the initial `created_tx`.

The solution is to use the initial saved `from_address` in the `created_tx` mapping

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
            assert(self.created_tx.read(cross_chain_msg_id).tx_status == CrossChainMsgStatus::PENDING, 'tx status error');

            let mut message_hash_temp: felt252 = LegacyHash::hash(from_chain, (cross_chain_msg_id, to_chain, from_handler, to_handler));
            let message_hash_final:felt252 = LegacyHash::hash(message_hash_temp, cross_chain_msg_status);
            self.check_chakra_signatures(message_hash_final, signatures);
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

            self.emit(CrossChainResult {
                cross_chain_settlement_id: cross_chain_msg_id,
=>              from_address: get_tx_info().unbox().account_contract_address,
                from_chain: to_chain,
                from_handler: to_handler,
                to_chain: from_chain,
                to_handler: from_handler,
                cross_chain_msg_status: state,
            });
            return true;
        }
```

[QA-4]: The Cairo Settlement does not rely on an external signature verifier

The Cairo Settlement does not rely on an external signature verifier contract which breaks the invariant:

> The contract relies on an external signature verifier (signature_verifier) for validating signatures.

## [QA-5]: The Cairo Settlement and SettlementHandler do not key the nonce by sender.

Breaking the two invariants:

> The nonce for each sender is incremented with each cross-chain transaction to ensure uniqueness of transaction IDs.

> The nonce for each from_address is incremented for every new cross-chain message sent, ensuring uniqueness of transactions.

Instead the nonce is tracked globally in `self.tx_count` variable.

```
        fn send_cross_chain_msg(
            ref self: ContractState, to_chain: felt252, to_handler: u256, payload_type :u8,payload: Array<u8>,
        ) -> felt252 {
            let from_handler = get_caller_address();
            let from_chain = self.chain_name.read();
            let cross_chain_settlement_id = LegacyHash::hash(get_tx_info().unbox().transaction_hash, self.tx_count.read());
            ...
            self.tx_count.write(self.tx_count.read()+1);
```
## [QA-6]: Consider only allowing registered handlers to call `send_cross_chain_msg`

Consider only allowing registered handlers to call `send_cross_chain_msg` as there is currently no access control for both Starknet and EVM chains, the only impact is incrementing the nonce of a user which has no other impact.

```solidity
    function send_cross_chain_msg(
        string memory to_chain,
        address from_address,
        uint256 to_handler,
        PayloadType payload_type,
        bytes calldata payload
    ) external {
        nonce_manager[from_address] += 1;
```

## [QA-7]: Consider removing the `to_handler` checks in the Cairo SettlementHandler
```rust
        fn receive_cross_chain_callback(ref self: ContractState, cross_chain_msg_id: felt252, from_chain: felt252, to_chain: felt252,
        from_handler: u256, to_handler: ContractAddress, cross_chain_msg_status: u8) -> bool{
            assert(to_handler == get_contract_address(),'error to_handler');

            assert(self.settlement_address.read() == get_caller_address(), 'not settlement');

            assert(self.support_handler.read((from_chain, from_handler)) && 
                    self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');
```

Consider removing the `to_handler` checks in the Cairo SettlementHandler and if the admin misconfigures by forgetting the add the `to_chain` and the `to_handler` into the whitelist the cross-chain transaction will fail.