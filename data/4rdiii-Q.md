
# [L-01] Incorrect Token Handling in `ChakraSettlementHandler::cross_chain_erc20_settlement`  
The SettlementMode.MintBurn should burn the token from origin chain and mint it in destination chain, but instead of burning it uses `_erc20_lock` function which locks the token in handler contract. This inconsistency means that tokens are not being removed from circulation in the source chain as intended, potentially disrupting the balance of token supplies across chains. While the bridging process might still appear to work, this misimplementation could lead to unforeseen consequences in the long run.

## Impact
The tokens will be locked instead of burning. This has several implications:
1. Token supply discrepancy: The total supply of the token across chains becomes inconsistent.
2. Centralized control: Locked tokens are held within the settlement handler contract, potentially centralizing control over these assets.
3. User confusion: Users expecting their tokens to be burned may be confused or concerned when they discover their tokens are locked instead.
4. Potential for misuse: Although unlikely due to cross-chain verification mechanisms, there's a theoretical risk of these locked tokens being accessed or manipulated in unintended ways.

## Proof of Concept
Here's the relevant part of the `cross_chain_erc20_settlement` function, showing the incorrect use of `_erc20_lock` instead of `_erc20_burn` for the MintBurn case:
```javascript
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

@>      if (mode == SettlementMode.MintBurn) {
@>          _erc20_lock(msg.sender, address(this), amount);
        } else if (mode == SettlementMode.LockUnlock) {
            _erc20_lock(msg.sender, address(this), amount);
        } else if (mode == SettlementMode.LockMint) {
            _erc20_lock(msg.sender, address(this), amount);
        } else if (mode == SettlementMode.BurnUnlock) {
            _erc20_burn(msg.sender, amount);
        }
    .
    .
    .
    }

```
## Tools Used
Manual Review

## Recommended Mitigation Steps

Use `_erc20_burn` instead! Replace the line in the MintBurn case with:

```diff
    if (mode == SettlementMode.MintBurn) {
-       _erc20_lock(msg.sender, address(this), amount);
+       _erc20_burn(msg.sender, amount); // Correct implementation
    } else if (mode == SettlementMode.LockUnlock) {
        _erc20_lock(msg.sender, address(this), amount);
    } else if (mode == SettlementMode.LockMint) {
        _erc20_lock(msg.sender, address(this), amount);
    } else if (mode == SettlementMode.BurnUnlock) {
        _erc20_burn(msg.sender, amount);
    }
```
This change ensures that tokens are properly burned in the source chain during MintBurn settlements, maintaining cross-chain consistency and adhering to the expected behavior of the settlement protocol.


# [L-02] Several functions to set `required_validators` across different contracts

There are different functions across ChakraSettlement and SettlementSignatureVerifier contracts to set the required_validators. This duplication could cause inconsistencies and difficulties if different values are set for each of them. To improve consistency and reduce potential errors, it would be better to centralize this functionality in one contract and have the other read from it.

## Impact
The impact of this finding includes:

1. **Consistency Risk**: Different values for `required_validators` in separate contracts could lead to inconsistent behavior across the system, potentially causing unexpected results in cross-chain operations.

2. **Maintenance Complexity**: Having multiple places to update the same parameter increases the complexity of maintenance. It's easier to overlook updating one of the instances, leading to discrepancies.

3. **Potential for Errors**: Manual synchronization of these values across contracts introduces a risk of human error, where one contract might be updated but another forgotten.

4. **Code Duplication**: Maintaining identical functions in multiple contracts violates the DRY (Don't Repeat Yourself) principle, potentially leading to inconsistencies if future updates are not applied uniformly.

5. **Difficulty in Auditing**: With multiple sources of truth for the same parameter, auditing becomes more challenging as auditors need to verify consistency across multiple contracts.

## Proof of Concept

The functions in both contracts are identical except for the `virtual` keyword in the verifier contract:

```javascript
// ChakraSettlement.sol
function set_required_validators_num(uint256 _required_validators) external onlyRole(MANAGER_ROLE) {
    uint256 old = required_validators;
    required_validators = _required_validators;
    emit RequiredValidatorsChanged(msg.sender, old, required_validators);
}

// SettlementSignatureVerifier.sol
function set_required_validators_num(uint256 _required_validators) external virtual onlyRole(MANAGER_ROLE) {
    uint256 old = required_validators;
    required_validators = _required_validators;
    emit RequiredValidatorsChanged(msg.sender, old, required_validators);
}
```

## Tools Used
Manual Review

## Recommended Mitigation Steps
To address this issue, we recommend the following approach:

1. Designate one contract (preferably the base contract) as the single source of truth for `required_validators`.

2. Modify the other contract(s) to read the value from the designated source instead of maintaining their own copy.

3. Remove the redundant `set_required_validators_num` function from the secondary contract(s).

4. If necessary, create a getter function in the secondary contract(s) that calls the designated source contract's getter.

Example implementation:

```javascript
// In the base contract (e.g., SettlementSignatureVerifier.sol):
function set_required_validators_num(uint256 _required_validators) external virtual onlyRole(MANAGER_ROLE) {
    uint256 old = required_validators;
    required_validators = _required_validators;
    emit RequiredValidatorsChanged(msg.sender, old, required_validators);
}

function get_required_validators() external view returns(uint256) {
    return required_validators;
}

// In the derived contract (e.g., ChakraSettlement.sol):
contract ChakraSettlement is SettlementSignatureVerifier {
    // Remove the set_required_validators_num function

    function get_required_validators() external view override returns(uint256) {
        return super.get_required_validators();
    }
}
```

This approach ensures that there's only one place to update the `required_validators` value, reducing the risk of inconsistencies and simplifying maintenance and auditing processes.


# [L-03] No gap is considered when inheriting contracts with storage variables inside a uups upgradable contract
In both ChakraSettlement and ChakraSettlementHandler contracts the Base contract has storage variable but didnt consider adding a gap[50] in case of future upgrades. 
Handler Contract:
```javascript
contract ChakraSettlementHandler is BaseSettlementHandler, ISettlementHandler {
    mapping(string => mapping(uint256 => bool)) public handler_whitelist;
    .
    .
    .
}
/// It's Base Contract
abstract contract BaseSettlementHandler is
    OwnableUpgradeable,
    UUPSUpgradeable,
    AccessControlUpgradeable
{
    .
    .
    .
    // =============== Contracts ============================================================
    SettlementMode public mode;
    /**
     * @dev The address of the token contract
     */
    address public token;

    /**
     * @dev The address of the verify contract
     */
    ISettlementSignatureVerifier public verifier;

    /**
     * @dev The address of the settlement contract
     */
    ISettlement public settlement;

    // =============== Storages ============================================================
    mapping(address => uint256) public nonce_manager;
    mapping(uint256 => CreatedCrossChainTx) public create_cross_txs;
    uint64 public cross_chain_msg_id_counter;
    /**
     * @dev The chain name
     */
    string public chain;
    mapping(uint256 => HandlerTransaction) public handler_transactions;
    .
    .
    .
}
```
ChakraSettlement: 
```javascript
contract ChakraSettlement is BaseSettlement {
    mapping(uint256 => CreatedCrossChainTx) public create_cross_txs;
    mapping(uint256 => ReceivedCrossChainTx) public receive_cross_txs;
    .
    .
    .
}
/// It's Base Contract:
abstract contract BaseSettlement is
    OwnableUpgradeable,
    UUPSUpgradeable,
    AccessControlUpgradeable
{
    .
    .
    .

    // Constant for the manager role
    bytes32 public constant MANAGER_ROLE = keccak256("MANAGER_ROLE");

    // The chain id of the settlement contract
    uint256 public chain_id;
    string public contract_chain_name;

    // The number of required validators
    uint256 public required_validators;
    // The signature verifier contract
    ISettlementSignatureVerifier public signature_verifier;

    // Mapping for nonce manager and validators
    mapping(address => uint256) public nonce_manager;
    mapping(address => bool) public chakra_validators;
    uint256 public validator_count;
    .
    .
    .
}
```
## Impact
For upgradeable contracts, there must be storage gap to "allow developers to freely add new state variables in the future without compromising the storage compatibility with existing deployments". Otherwise it may be very difficult to write new implementation code. Without storage gap, the variable in child contract might be overwritten by the upgraded base contract if new variables are added to the base contract. This could have unintended and very serious consequences to the child contracts.

## Tools Used
Manual Review

## Recommended Mitigation Steps
Recommend adding appropriate storage gap at the end of upgradeable contracts such as the below. Please reference OpenZeppelin upgradeable contract templates.

```javascript
uint256[50] private __gap;

```