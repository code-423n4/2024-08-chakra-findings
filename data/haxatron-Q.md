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