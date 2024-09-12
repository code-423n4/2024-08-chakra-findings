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