 # Table of findings

| Id | Title |
| --- | --- |
| L-1 | Managers should only be added by owner, not other managers |
| L-2 | Checking `support_handler` for `to_chain` and `to_handler` is unnecessary in `receive_cross_chain_msg()` |
| L-3 | Anyone can increase `nonce_manager[]` of any address |
| L-4 | Unsafe cast function `to_address()` |
| L-5 | Payload length is not checked when decoding |
| N-1 | Mismatch `receive_cross_chain_msg()` between Cairo and Solidity when checking `is_valid_handler()`
| N-2 | Typos |
| N-3 | Unused `AccessControlUpgradeable` |


# L-1. Managers should only be added by owner, not other managers

[ckr_btc.cairo#L136](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/ckr_btc.cairo#L136)

[settlement.cairo#L199](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L199)

[settlement.cairo#L248](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/settlement.cairo#L248)

## Detail
Currently, in ckr_btc contract, manager could grant other addresses as manager. As a result, if a manager is compromised, the attacker could repeatedly grant manager role to different addresses, making it impossible to stop the attack. Because when you try to revoke the manager role from an address, it already granted the manager role to another one.

```rust
fn add_manager(ref self: ContractState, new_manager: ContractAddress) -> bool {
    let caller = get_caller_address();
    assert(self.chakra_managers.read(caller) == 1, Errors::NOT_MANAGER); // @audit should be onlyOwner
    assert(self.chakra_managers.read(new_manager) == 0, Errors::ALREADY_MANAGER);
```

Similarly in settlement.cairo contract.

---

# L-2. Checking `support_handler` for `to_chain` and `to_handler` is unnecessary in `receive_cross_chain_msg()` 

[handler_erc20.cairo#L115](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/handler_erc20.cairo#L115)

## Detail
This function is called in the handler contract of destination chain. So `to_handler == get_contract_address()`, making it unnecessary to check for the `support_handler[][]`.
```rust
fn receive_cross_chain_msg(ref self: ContractState, cross_chain_msg_id: u256, from_chain: felt252, to_chain: felt252,
from_handler: u256, to_handler: ContractAddress, payload: Array<u8>) -> bool{
    assert(to_handler == get_contract_address(),'error to_handler');

    assert(self.settlement_address.read() == get_caller_address(), 'not settlement');

    assert(self.support_handler.read((from_chain, from_handler)) && 
            self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler'); // @audit unnecessary since this is the handler
```

---

# L-3. Anyone can increase `nonce_manager[]` of any address

[ChakraSettlement.sol#L118](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/settlement/contracts/ChakraSettlement.sol#L118)

## Details
The function `send_cross_chain_msg()` is public and allow anyone to increase the `nonce_manager[]` of any address.

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

---

# L-4. Unsafe cast `to_address()`

[AddressCast.sol](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/settlement/contracts/libraries/AddressCast.sol#L22-L36)

## Details
Unsafe casting in `to_adrress()` function. The cast from `uint256 -> uint160` does not check if the value overflow uint160, thus the value might be truncate, resulting in invalid address convert to a valid EVM address after using `to_address()`.
```solidity
function to_address(
    bytes32 _address
) internal pure returns (address result) {
    result = address(uint160(uint256(_address))); // @audit unsafe cast from uint256 -> uint160
}

function to_address(
    uint256 _address
) internal pure returns (address result) {
    result = address(uint160(_address)); // @audit unsafe cast
}
```

---

# L-5. Payload length is not checked when decoding

[codec.cairo#L54](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/codec.cairo#L54)

[codec.cairo#L29](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/codec.cairo#L29)

## Details
Decode functions in Cairo take in a `u8` array and try to decode it into some values.

It does a while loop that will just sequencially decode the value based on data type of `version`, `message_id_array`, ... However, it does not check if the `payload` has appropriate length. For example, a payload might have length < 32 still be able to decode to a message, but with empty `payload_type` and empty `message_payload`.

```rust
pub fn decode_message(payload: Array<u8>) -> Message{
    let mut version = 0;
    let mut payload_type = 0;
    let mut message_id_array = ArrayTrait::new();
    let mut message_payload = ArrayTrait::new();
    let mut i = 0;
    loop{ // @audit no check length of payload
        if i <= 0{
            version = * payload.span().at(i);
        }else if i<= 32{
            message_id_array.append(* payload.span().at(i));
        }else if i <= 33{
            payload_type = * payload.span().at(i);
        }else if i <= payload.span().len()-1{
            message_payload.append(* payload.span().at(i));
        }else{
            break;
        }
        i+=1;
    };
```

---

# N-1. Mismatch `receive_cross_chain_msg()` between Cairo and Solidity when checking `is_valid_handler()`

[ChakraSettlementHandler.sol](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/ChakraSettlementHandler.sol#L311)

## Details
Solidity version only check `from_handler` is whitelisted. 
```solidity
function receive_cross_chain_msg(
    uint256 /**txid */,
    string memory from_chain,
    uint256 /**from_address */,
    uint256 from_handler,
    PayloadType payload_type,
    bytes calldata payload,
    uint8 /**sign type */,
    bytes calldata /**signaturs */
) external onlySettlement returns (bool) {
    //  from_handler need in whitelist
    if (is_valid_handler(from_chain, from_handler) == false) { // @audit not check to_handler like cairo
        return false;
    }
```

While Cairo version check both `from_handler` and `to_handler`

```rust
fn receive_cross_chain_msg(ref self: ContractState, cross_chain_msg_id: u256, from_chain: felt252, to_chain: felt252,
from_handler: u256, to_handler: ContractAddress, payload: Array<u8>) -> bool{
    // ...

    assert(self.support_handler.read((from_chain, from_handler)) && 
            self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');

```

---

# N-2. Typos

[ERC20CodecV1.sol#L39](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/ERC20CodecV1.sol#L39)

## Detail
```solidity
encodedPaylaod = abi.encodePacked( // @audit typo payload
```

---

# N-3. Unused `AccessControlUpgradeable`

[BaseSettlementHandler.sol#L21](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/BaseSettlementHandler.sol#L21)

## Detail
The Handler contract in Solidity version inherits `AccessControlUpgradeable` but never used

```solidity
abstract contract BaseSettlementHandler is
    OwnableUpgradeable,
    UUPSUpgradeable,
    AccessControlUpgradeable // @audit never used
{
```

---