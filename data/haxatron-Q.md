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

## [QA-3] Consider writing PENDING status of the `received_tx` in the settlement before calling the handler.
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
            assert(to_chain == self.chain_name.read(), 'error to_chain');

            // verify signatures
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
            self.check_chakra_signatures(message_hash, signatures);

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
```

Consider writing PENDING status of the `received_tx` in the settlement before calling the `handler.receive_cross_chain_msg`