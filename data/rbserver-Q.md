## QA REPORT

|      | Issue                                                                                                                                                                                          |
| ---- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [01] | `ChakraSettlementHandler.cross_chain_erc20_settlement` function incorrectly uses `address(this)` as data for `CreatedCrossChainTx` struct's `from_token` when setting `create_cross_txs[txid]` |
| [02] | `ChakraSettlementHandler.cross_chain_erc20_settlement` function incorrectly uses `address(this)` as data for `CrossChainLocked` event when emitting such event                                 |
| [03] | `ChakraSettlement.receive_cross_chain_msg` function incorrectly uses `address(this)` as data for `ReceivedCrossChainTx` struct's `to_handler` when setting `receive_cross_txs[txid]`           |
| [04] | Calling `ChakraSettlement.receive_cross_chain_msg` function reverts for retrying failed `receive_cross_txs[txid]`                                                                              |
| [05] | `ChakraSettlementHandler.cross_chain_erc20_settlement` function does not ensure that `to_chain` input must correspond to a supported chain                                                     |
| [06] | Allowing `ChakraSettlement.send_cross_chain_msg` function to be callable by anyone can spam and poison monitor system that consumes `CrossChainMsg` event                                      |
| [07] | `txid` generated in functions like `ChakraSettlementHandler.cross_chain_erc20_settlement` for two different source chain-destination chain combinations can be same, which breaks an invariant |
| [08] | `SettlementSignatureVerifier.remove_validator` and `SettlementSignatureVerifier.set_required_validators_num` functions can be frontrun                                                         |
| [09] | Floating pragma is used                                                                                                                                                                        |
| [10] | Test code need to be removed                                                                                                                                                                   |

## [01] `ChakraSettlementHandler.cross_chain_erc20_settlement` function incorrectly uses `address(this)` as data for `CreatedCrossChainTx` struct's `from_token` when setting `create_cross_txs[txid]`

### Description
The `ChakraSettlementHandler.cross_chain_erc20_settlement` function sets `create_cross_txs[txid]` by using `address(this)` as the data for the `CreatedCrossChainTx` struct's `from_token`. However, this is incorrect because `address(this)` is the address of the `ChakraSettlementHandler` contract and is not the address of the `from_token`. When there is a need to retrieve `create_cross_txs[txid]`'s `from_token` for a corresponding `txid`, the `ChakraSettlementHandler` contract's address would be mistakenly considered as such `from_token`, which can cause the protocol to misbehave.

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/ChakraSettlementHandler.sol#L111-L223
```solidity
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
@>              address(this),
                to_token,
                amount,
                CrossChainTxStatus.Pending
            );
        }

        ...
    }
```

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/BaseSettlementHandler.sol#L53-L63
```solidity
    struct CreatedCrossChainTx {
        uint256 txid;
        string from_chain;
        string to_chain;
        address from;
        uint256 to;
@>      address from_token;
        uint256 to_token;
        uint256 amount;
        CrossChainTxStatus status;
    }
```

### Recommended Mitigation
The `ChakraSettlementHandler.cross_chain_erc20_settlement` function can be updated to use the `ChakraSettlementHandler` contract's `token` as the data for the `CreatedCrossChainTx` struct's `from_token` when setting `create_cross_txs[txid]`.

## [02] `ChakraSettlementHandler.cross_chain_erc20_settlement` function incorrectly uses `address(this)` as data for `CrossChainLocked` event when emitting such event

### Description
The `ChakraSettlementHandler.cross_chain_erc20_settlement` function emits the `CrossChainLocked` event through using `address(this)` as the data for such event's `from_token`. Yet, `address(this)` is the `ChakraSettlementHandler` contract's address, which is not such `from_token` address. Thus, the `from_token` data emitted for the `CrossChainLocked` event is incorrect. When consuming such `CrossChainLocked` event, the monitor system would incorrectly consider the address of the `ChakraSettlementHandler` contract as the `from_token` address, which causes the protocol to fail to identify the actual `from_token` when needed.

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/ChakraSettlementHandler.sol#L111-L223
```solidity
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
@>          address(this),
            to_token,
            amount,
            mode
        );
    }
```

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/BaseSettlementHandler.sol#L41-L51
```solidity
    event CrossChainLocked(
        uint256 indexed txid,
        address indexed from,
        uint256 indexed to,
        string from_chain,
        string to_chain,
@>      address from_token,
        uint256 to_token,
        uint256 amount,
        SettlementMode mode
    );
```

### Recommended Mitigation
The `ChakraSettlementHandler.cross_chain_erc20_settlement` function can be updated to use the `ChakraSettlementHandler` contract's `token` as the data for the `CrossChainLocked` event when emitting such event.

## [03] `ChakraSettlement.receive_cross_chain_msg` function incorrectly uses `address(this)` as data for `ReceivedCrossChainTx` struct's `to_handler` when setting `receive_cross_txs[txid]`

### Description
The `ChakraSettlement.receive_cross_chain_msg` function uses `address(this)` as the data for `to_handler` of the `ReceivedCrossChainTx` struct when setting `receive_cross_txs[txid]`, which is incorrect because `address(this)` is the address of the `ChakraSettlement` contract that is not the `to_handler` address. When there is a need to retrieve the `receive_cross_txs[txid]`'s `to_handler` for a `txid`, the `ChakraSettlement` contract's address is incorrectly considered as such `to_handler`; such misleading `to_handler` data can cause the protocol to malfunction.

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/settlement/contracts/ChakraSettlement.sol#L170-L244
```solidity
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
        ...

        receive_cross_txs[txid] = ReceivedCrossChainTx(
            txid,
            from_chain,
            contract_chain_name,
            from_address,
            from_handler,
@>          address(this),
            payload,
            CrossChainMsgStatus.Pending
        );

        ...
    }
```

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/settlement/contracts/ChakraSettlement.sol#L31-L40
```solidity
    struct ReceivedCrossChainTx {
        uint256 txid;
        string from_chain;
        string to_chain;
        uint256 from_address;
        uint256 from_handler;
@>      address to_handler;
        bytes payload;
        CrossChainMsgStatus status;
    }
```

### Recommended Mitigation
The `ChakraSettlement.receive_cross_chain_msg` function can be updated to use its `to_handler` input value as the data for `to_handler` of the `ReceivedCrossChainTx` struct when setting `receive_cross_txs[txid]`.

## [04] Calling `ChakraSettlement.receive_cross_chain_msg` function reverts for retrying failed `receive_cross_txs[txid]`

### Description
When calling the `ChakraSettlement.receive_cross_chain_msg` function, which further calls the `ChakraSettlementHandler.receive_cross_chain_msg` function, the `from_chain`-`from_handler` combination could be temporarily not whitelisted yet but will be whitelisted later after ensuring that such combination is safe. In this case, calling the `ChakraSettlementHandler.receive_cross_chain_msg` function returns `false` though it will return `true` in the future when such `from_chain`-`from_handler` combination becomes whitelisted. This causes `receive_cross_txs[txid].status` to be set to `CrossChainMsgStatus.Failed` in the `ChakraSettlement.receive_cross_chain_msg` function. Since the `ChakraSettlement.receive_cross_chain_msg` function executes `require(receive_cross_txs[txid].status == CrossChainMsgStatus.Unknow, "Invalid transaction status")`, calling the `ChakraSettlement.receive_cross_chain_msg` function for such `txid` will revert even when such `from_chain`-`from_handler` combination becomes whitelisted in the future. Thus, there is no way to retry the failed `receive_cross_txs[txid]`.

Since the `ChakraSettlementHandler` contract on the source chain currently has no refund mechanism, when the `receive_cross_txs[txid]` becomes failed, the tokens that were originally transferred to the source chain's handler cannot be refunded. Moreover, because the failed `receive_cross_txs[txid]` cannot be retried, there is no way to receive the corresponding tokens on the destination chain even when the condition later permits, such as when the `from_chain`-`from_handler` combination becomes whitelisted in the future.

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/settlement/contracts/ChakraSettlement.sol#L170-L244
```solidity
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
            ...

@>          require(
@>              receive_cross_txs[txid].status == CrossChainMsgStatus.Unknow,
                "Invalid transaction status"
            );
        }

        receive_cross_txs[txid] = ReceivedCrossChainTx(
            txid,
            from_chain,
            contract_chain_name,
            from_address,
            from_handler,
            address(this),
            payload,
            CrossChainMsgStatus.Pending
        );

@>      bool result = ISettlementHandler(to_handler).receive_cross_chain_msg(
            txid,
            from_chain,
            from_address,
            from_handler,
            payload_type,
            payload,
            sign_type,
            signatures
        );

        CrossChainMsgStatus status = CrossChainMsgStatus.Failed;
        if (result == true) {
            status = CrossChainMsgStatus.Success;
            receive_cross_txs[txid].status = CrossChainMsgStatus.Success;
@>      } else {
@>          receive_cross_txs[txid].status = CrossChainMsgStatus.Failed;
        }

        ...
    }
```

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/ChakraSettlementHandler.sol#L300-L355
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
@>      if (is_valid_handler(from_chain, from_handler) == false) {
@>          return false;
        }
        ...
    }
```

### Recommended Mitigation
The `ChakraSettlement.receive_cross_chain_msg` function can be updated to allow the failed `receive_cross_txs[txid]` to be retried.

## [05] `ChakraSettlementHandler.cross_chain_erc20_settlement` function does not ensure that `to_chain` input must correspond to a supported chain

### Description
In the `ChakraSettlementHandler.cross_chain_erc20_settlement` function, the `amount`, `to`, `to_handler`, and `to_token` inputs are all validated. However, the `to_chain` input is not validated. If the specified `to_chain` is for `address(0)` or an unsupported chain, the cross-chain message and the corresponding tokens cannot be received on such `to_chain`. As a result, the tokens sent to the corresponding `ChakraSettlementHandler` contract when the `ChakraSettlementHandler.cross_chain_erc20_settlement` function is called are spent for nothing in return and are essentially lost.

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/ChakraSettlementHandler.sol#L111-L223
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

### Recommended Mitigation
The `ChakraSettlementHandler.cross_chain_erc20_settlement` function can be updated to add a validation for ensuring that the `to_chain` input must correspond to a supported chain.

## [06] Allowing `ChakraSettlement.send_cross_chain_msg` function to be callable by anyone can spam and poison monitor system that consumes `CrossChainMsg` event

### Description
The `ChakraSettlement.send_cross_chain_msg` function can be callable by anyone. Therefore, an address that is not a whitelisted handler can call this function repeatedly to emit the `CrossChainMsg` event for many times. In this case, these emitted `CrossChainMsg` events would be meaningless due to that such function caller is not whitelisted and its cross-chain messages would not be received successfully. As a result, the monitor system that consumes such `CrossChainMsg` event would be spammed and poisoned.

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/settlement/contracts/ChakraSettlement.sol#L111-L156
```solidity
    function send_cross_chain_msg(
        string memory to_chain,
        address from_address,
        uint256 to_handler,
        PayloadType payload_type,
        bytes calldata payload
    ) external {
        nonce_manager[from_address] += 1;

        address from_handler = msg.sender;

        uint256 txid = uint256(
            keccak256(
                abi.encodePacked(
                    contract_chain_name, // from chain
                    to_chain,
                    from_address, // msg.sender address
                    from_handler, // settlement handler address
                    to_handler,
                    nonce_manager[from_address]
                )
            )
        );

        create_cross_txs[txid] = CreatedCrossChainTx(
            txid,
            contract_chain_name,
            to_chain,
            from_address,
            from_handler,
            to_handler,
            payload,
            CrossChainMsgStatus.Pending
        );

        emit CrossChainMsg(
            txid,
            from_address,
            contract_chain_name,
            to_chain,
            from_handler,
            to_handler,
            payload_type,
            payload
        );
    }
```

### Recommended Mitigation
The `ChakraSettlement.send_cross_chain_msg` function can be updated to only be callable by the whitelisted handlers.

## [07] `txid` generated in functions like `ChakraSettlementHandler.cross_chain_erc20_settlement` for two different source chain-destination chain combinations can be same, which breaks an invariant

### Description
When `txid` needs to be generated, the `abi.encodePacked` function is currently used, which can cause `txid` to be the same for different source chain-destination chain combinations. For example, because the `ChakraSettlementHandler.cross_chain_erc20_settlement` function uses the `abi.encodePacked` function for setting `txid`, the `txid` for two different `chain`-`to_chain` combinations can be the same if `msg.sender`, `address(this)`, `to_handler`, and `nonce_manager[msg.sender]` are the same when calling such function on these two `chain` chains. This is because, for example, `abi.encodePacked("x", "yz")` when `chain` is `x` and `to_chain` is `yz` and `abi.encodePacked("xy", "z")` when `chain` is `xy` and `to_chain` is `z` would return the same bytes. Therefore, the invariant, `Cross-chain transaction IDs are uniquely generated based on the source and destination chain information, sender, handler addresses, and nonce`, listed in https://github.com/code-423n4/2024-08-chakra?tab=readme-ov-file#main-invariants can be broken.

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/ChakraSettlementHandler.sol#L111-L223
```solidity
    function cross_chain_erc20_settlement(
        string memory to_chain,
        uint256 to_handler,
        uint256 to_token,
        uint256 to,
        uint256 amount
    ) external {
        ...

        // Create a new cross chain tx
@>      uint256 txid = uint256(
@>          keccak256(
@>              abi.encodePacked(
@>                  chain,
@>                  to_chain,
@>                  msg.sender, // from address for settlement to calculate txid
@>                  address(this), //  from handler for settlement to calculate txid
@>                  to_handler,
@>                  nonce_manager[msg.sender]
@>              )
@>          )
@>      );

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

### Recommended Mitigation
When `txid` needs to be generated, such as in the `ChakraSettlementHandler.cross_chain_erc20_settlement` function, the `abi.encode` function can be used instead of the `abi.encodePacked` function.

## [08] `SettlementSignatureVerifier.remove_validator` and `SettlementSignatureVerifier.set_required_validators_num` functions can be frontrun

### Description
When the `SettlementSignatureVerifier.remove_validator` function is called, the signatures signed by the removed validators can become invalid. Similarly, when the `SettlementSignatureVerifier.set_required_validators_num` function is called to increase the number of required validators, the signatures signed by too few validators can become invalid. For using these signatures that should become invalid, users can frontrun the `SettlementSignatureVerifier.remove_validator` or `SettlementSignatureVerifier.set_required_validators_num` transaction by calling the `SettlementSignatureVerifier.verifyECDSA` function. After such frontrunning, such signatures can be used successfully, because they would be verified against the validators that should be removed or the lower number of required validators that should be higher, even though they should not be allowed to be used.

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/settlement/contracts/SettlementSignatureVerifier.sol#L125-L132
```solidity
    function remove_validator(
        address validator
    ) external onlyRole(MANAGER_ROLE) {
        require(validators[validator] == true, "Validator does not exists");
        validators[validator] = false;
        validator_count -= 1;
        emit ValidatorRemoved(msg.sender, validator);
    }
```

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/settlement/contracts/SettlementSignatureVerifier.sol#L139-L145
```solidity
    function set_required_validators_num(
        uint256 _required_validators
    ) external virtual onlyRole(MANAGER_ROLE) {
        uint256 old = required_validators;
        required_validators = _required_validators;
        emit RequiredValidatorsChanged(msg.sender, old, required_validators);
    }
```

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/settlement/contracts/SettlementSignatureVerifier.sol#L193-L214
```solidity
    function verifyECDSA(
        bytes32 msgHash,
        bytes calldata signatures
    ) internal view returns (bool) {
        require(
            signatures.length % 65 == 0,
            "Signature length must be a multiple of 65"
        );

        uint256 len = signatures.length;
        uint256 m = 0;
        for (uint256 i = 0; i < len; i += 65) {
            bytes memory sig = signatures[i:i + 65];
            if (
                validators[msgHash.recover(sig)] && ++m >= required_validators
            ) {
                return true;
            }
        }

        return false;
    }
```

### Recommended Mitigation
As a mitigation, flashbots can be utilized to prevent frontrunning.

## [09] Floating pragma is used

### Description
The `^0.8.24` floating pragma, such as in the `ChakraSettlement` and `ChakraSettlementHandler` contracts, is used throughout this protocol. Yet, using floating pragma can allow contracts to be deployed with Solidity versions that are not thoroughly tested, which can cause contracts to malfunction due to compiler bugs that are not detected or fixed yet.

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/settlement/contracts/ChakraSettlement.sol#L2
```solidity
pragma solidity ^0.8.24;
```

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/ChakraSettlementHandler.sol#L2
```solidity
pragma solidity ^0.8.24;
```

### Recommended Mitigation
This protocol's contracts can be updated to use a fixed pragma, which has been thoroughly tested.

## [10] Test code need to be removed

### Description
Test code can still be found in the protocol's production codebase; for example, the `ChakraSettlementHandler` contract still imports `hardhat/console.sol`. Such test code would waste gas and can introduce unexpected bugs if not removed.

https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/ChakraSettlementHandler.sol#L4
```solidity
import "hardhat/console.sol";
```

### Recommended Mitigation
All test code in the production codebase need to be found and removed.