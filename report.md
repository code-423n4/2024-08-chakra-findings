---
sponsor: "Chakra"
slug: "2024-08-chakra"
date: "2025-02-20"
title: "Chakra"
findings: "https://github.com/code-423n4/2024-08-chakra-findings/issues"
contest: 432
---

# Overview

## About C4

Code4rena (C4) is an open organization consisting of security researchers, auditors, developers, and individuals with domain expertise in smart contracts.

A C4 audit is an event in which community participants, referred to as Wardens, review, audit, or analyze smart contract logic in exchange for a bounty provided by sponsoring projects.

During the audit outlined in this document, C4 conducted an analysis of the Chakra smart contract system. The audit took place between August 29—September 12 2024.

## Wardens

109 Wardens contributed reports to Chakra:

  1. [shaflow2](https://code4rena.com/@shaflow2)
  2. [Abdessamed](https://code4rena.com/@Abdessamed)
  3. [fyamf](https://code4rena.com/@fyamf)
  4. [0xAsen](https://code4rena.com/@0xAsen)
  5. [ABAIKUNANBAEV](https://code4rena.com/@ABAIKUNANBAEV)
  6. [SBSecurity](https://code4rena.com/@SBSecurity) ([Slavcheww](https://code4rena.com/@Slavcheww) and [Blckhv](https://code4rena.com/@Blckhv))
  7. [Emmanuel](https://code4rena.com/@Emmanuel)
  8. [AllTooWell](https://code4rena.com/@AllTooWell) ([zhuying](https://code4rena.com/@zhuying) and [0x996](https://code4rena.com/@0x996))
  9. [Tigerfrake](https://code4rena.com/@Tigerfrake)
  10. [said](https://code4rena.com/@said)
  11. [klau5](https://code4rena.com/@klau5)
  12. [Draiakoo](https://code4rena.com/@Draiakoo)
  13. [Daniel\_eth](https://code4rena.com/@Daniel_eth)
  14. [0xNirix](https://code4rena.com/@0xNirix)
  15. [Xor0v0](https://code4rena.com/@Xor0v0)
  16. [b0g0](https://code4rena.com/@b0g0)
  17. [pwnforce](https://code4rena.com/@pwnforce)
  18. [Sabit](https://code4rena.com/@Sabit)
  19. [0x18a6](https://code4rena.com/@0x18a6)
  20. [jesjupyter](https://code4rena.com/@jesjupyter)
  21. [mjcpwns](https://code4rena.com/@mjcpwns)
  22. [rbserver](https://code4rena.com/@rbserver)
  23. [calc1f4r](https://code4rena.com/@calc1f4r)
  24. [haxatron](https://code4rena.com/@haxatron)
  25. [0xb0k0](https://code4rena.com/@0xb0k0)
  26. [Audinarey](https://code4rena.com/@Audinarey)
  27. [0x37](https://code4rena.com/@0x37)
  28. [mojito\_auditor](https://code4rena.com/@mojito_auditor)
  29. [gesha17](https://code4rena.com/@gesha17)
  30. [joicygiore](https://code4rena.com/@joicygiore)
  31. [gajiknownnothing](https://code4rena.com/@gajiknownnothing)
  32. [agent3bood](https://code4rena.com/@agent3bood)
  33. [Drynooo](https://code4rena.com/@Drynooo)
  34. [MrPotatoMagic](https://code4rena.com/@MrPotatoMagic)
  35. [ZdravkoHr](https://code4rena.com/@ZdravkoHr)
  36. [Shaheen](https://code4rena.com/@Shaheen)
  37. [devival](https://code4rena.com/@devival)
  38. [Topmark](https://code4rena.com/@Topmark)
  39. [Coinymous](https://code4rena.com/@Coinymous)
  40. [Respx](https://code4rena.com/@Respx)
  41. [jasonxiale](https://code4rena.com/@jasonxiale)
  42. [m4k2](https://code4rena.com/@m4k2)
  43. [peanuts](https://code4rena.com/@peanuts)
  44. [DPS](https://code4rena.com/@DPS) ([yvuchev](https://code4rena.com/@yvuchev) and [0xJaeger](https://code4rena.com/@0xJaeger))
  45. [avoloder](https://code4rena.com/@avoloder)
  46. [Breeje](https://code4rena.com/@Breeje)
  47. [calfun0x](https://code4rena.com/@calfun0x)
  48. [aldarion](https://code4rena.com/@aldarion)
  49. [Moksha](https://code4rena.com/@Moksha)
  50. [blackpanther](https://code4rena.com/@blackpanther)
  51. [Rhaydden](https://code4rena.com/@Rhaydden)
  52. [franfran20](https://code4rena.com/@franfran20)
  53. [Subroutine](https://code4rena.com/@Subroutine) ([p4y4b13](https://code4rena.com/@p4y4b13) and [Subsix](https://code4rena.com/@Subsix))
  54. [kutugu](https://code4rena.com/@kutugu)
  55. [bhilare\_](https://code4rena.com/@bhilare_)
  56. [LuarSec](https://code4rena.com/@LuarSec) ([GhK3Ndf](https://code4rena.com/@GhK3Ndf) and [lod1n](https://code4rena.com/@lod1n))
  57. [13u9](https://code4rena.com/@13u9)
  58. [Agontuk](https://code4rena.com/@Agontuk)
  59. [Cybrid](https://code4rena.com/@Cybrid)
  60. [DanielArmstrong](https://code4rena.com/@DanielArmstrong)
  61. [IzuMan](https://code4rena.com/@IzuMan)
  62. [0xabhay](https://code4rena.com/@0xabhay)
  63. [0xpetern](https://code4rena.com/@0xpetern)
  64. [NexusAudits](https://code4rena.com/@NexusAudits) ([cheatc0d3](https://code4rena.com/@cheatc0d3) and [Zanna](https://code4rena.com/@Zanna))
  65. [atoko](https://code4rena.com/@atoko)
  66. [tekkac](https://code4rena.com/@tekkac)
  67. [PASCAL](https://code4rena.com/@PASCAL)
  68. [Tonchi](https://code4rena.com/@Tonchi)
  69. [Trooper](https://code4rena.com/@Trooper)
  70. [Tumelo\_Crypto](https://code4rena.com/@Tumelo_Crypto)
  71. [0xHelium](https://code4rena.com/@0xHelium)
  72. [Brene](https://code4rena.com/@Brene)
  73. [Bauchibred](https://code4rena.com/@Bauchibred)
  74. [Taiger](https://code4rena.com/@Taiger)
  75. [0xastronatey](https://code4rena.com/@0xastronatey)
  76. [abhishek\_thaku\_r](https://code4rena.com/@abhishek_thaku_r)
  77. [Inspecktor](https://code4rena.com/@Inspecktor)
  78. [Decap](https://code4rena.com/@Decap)
  79. [0xSolus](https://code4rena.com/@0xSolus)
  80. [0xDemon](https://code4rena.com/@0xDemon)
  81. [10ap17](https://code4rena.com/@10ap17)
  82. [JanuaryPersimmon2024](https://code4rena.com/@JanuaryPersimmon2024)
  83. [BY\_DLIFE](https://code4rena.com/@BY_DLIFE)
  84. [kind\_killerwhale](https://code4rena.com/@kind_killerwhale)
  85. [Kaysoft](https://code4rena.com/@Kaysoft)
  86. [DimaKush](https://code4rena.com/@DimaKush)
  87. [Shubham](https://code4rena.com/@Shubham)
  88. [Omik](https://code4rena.com/@Omik)
  89. [eierina](https://code4rena.com/@eierina)
  90. [minato7namikazi](https://code4rena.com/@minato7namikazi)
  91. [4rdiii](https://code4rena.com/@4rdiii)
  92. [yudan](https://code4rena.com/@yudan)
  93. [Sparrow](https://code4rena.com/@Sparrow)
  94. [biakia](https://code4rena.com/@biakia)
  95. [PolarizedLight](https://code4rena.com/@PolarizedLight) ([ChaseTheLight](https://code4rena.com/@ChaseTheLight) and [Auditor\_Nate](https://code4rena.com/@Auditor_Nate))
  96. [sivanesh\_808](https://code4rena.com/@sivanesh_808)
  97. [Nexarion](https://code4rena.com/@Nexarion)
  98. [King\_](https://code4rena.com/@King_)
  99. [VulnViper](https://code4rena.com/@VulnViper)
  100. [Flare](https://code4rena.com/@Flare)
  101. [Sisi](https://code4rena.com/@Sisi)
  102. [mrjorystewartbaxter](https://code4rena.com/@mrjorystewartbaxter)

This audit was judged by [0xsomeone](https://code4rena.com/@0xsomeone).

Final report assembled by [liveactionllama](https://twitter.com/liveactionllama).

# Summary

The C4 analysis yielded an aggregated total of 26 unique vulnerabilities. Of these vulnerabilities, 14 received a risk rating in the category of HIGH severity and 12 received a risk rating in the category of MEDIUM severity.

Additionally, C4 analysis included 46 reports detailing issues with a risk rating of LOW severity or non-critical.

All of the issues presented here are linked back to their original finding.

# Scope

The code under review can be found within the [C4 Chakra repository](https://github.com/code-423n4/2024-08-chakra), and is composed of 16 smart contracts written in the Solidity programming language (1,357 lines of code) as well as 8 smart contracts written in the Cairo programming language (1,510 lines of code).

# Severity Criteria

C4 assesses the severity of disclosed vulnerabilities based on three primary risk categories: high, medium, and low/non-critical.

High-level considerations for vulnerabilities span the following key areas when conducting assessments:

- Malicious Input Handling
- Escalation of privileges
- Arithmetic
- Gas use

For more information regarding the severity criteria referenced throughout the submission review process, please refer to the documentation provided on [the C4 website](https://code4rena.com), specifically our section on [Severity Categorization](https://docs.code4rena.com/awarding/judging-criteria/severity-categorization).

# High Risk Findings (14)
## [[H-01] Invalid token address used in `ChakraSettlementHandler::cross_chain_erc20_settlement(...)` leading to invalid transaction creation and event emission](https://github.com/code-423n4/2024-08-chakra-findings/issues/380)
*Submitted by [0xb0k0](https://github.com/code-423n4/2024-08-chakra-findings/issues/380), also found by [AllTooWell](https://github.com/code-423n4/2024-08-chakra-findings/issues/621), [rbserver](https://github.com/code-423n4/2024-08-chakra-findings/issues/618), [said](https://github.com/code-423n4/2024-08-chakra-findings/issues/614), [shaflow2](https://github.com/code-423n4/2024-08-chakra-findings/issues/609), [fyamf](https://github.com/code-423n4/2024-08-chakra-findings/issues/604), [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/598), [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/592), [calfun0x](https://github.com/code-423n4/2024-08-chakra-findings/issues/583), [joicygiore](https://github.com/code-423n4/2024-08-chakra-findings/issues/515), [ABAIKUNANBAEV](https://github.com/code-423n4/2024-08-chakra-findings/issues/511), [Coinymous](https://github.com/code-423n4/2024-08-chakra-findings/issues/359), [Audinarey](https://github.com/code-423n4/2024-08-chakra-findings/issues/350), [b0g0](https://github.com/code-423n4/2024-08-chakra-findings/issues/214), [gajiknownnothing](https://github.com/code-423n4/2024-08-chakra-findings/issues/175), [mojito\_auditor](https://github.com/code-423n4/2024-08-chakra-findings/issues/65), [devival](https://github.com/code-423n4/2024-08-chakra-findings/issues/626), and [jasonxiale](https://github.com/code-423n4/2024-08-chakra-findings/issues/589)*

### Lines of code

<https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L160>

<https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L218>

### Impact

The `ChakraSettlementHandler` incorrectly passes the contract address instead of the token one, when creating the `create_cross_txs` transaction and when emitting the `CrossChainLocked` event. The contract depends heavily on correct event emission as the protocol's validators listen for these events and execute state-changing operations based on them.

### Proof of Concept

The `ChakraSettlementHandler::cross_chain_erc20_settlement(...)` function processes incoming cross-chain settlement user requests and sends data to the settlement contract. The method creates `CreatedCrossChainTx` along the way:

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

However, in the current implementation, instead of sending the `from_token` address it sends the actual contract address:

```solidity
create_cross_txs[txid] = CreatedCrossChainTx(
                txid,
                chain,
                to_chain,
                msg.sender,
                to,
@>              address(this), // @audit - this should be the global variable `token`
                to_token,
                amount,
                CrossChainTxStatus.Pending
            );
```

When the transaction is sent to the settlement contract a `CrossChainLocked` is emitted:

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

However, the method, once more sends the incorrect `from_token` address:

```solidity
emit CrossChainLocked(
            txid,
            msg.sender,
            to,
            chain,
            to_chain,
@>          address(this), // @audit - this should be the global variable `token`
            to_token,
            amount,
            mode
        );
```

If we peek into the Cairo implementation we can see that the `from_token` address should indeed be the token address not the handler contract address:

```cairo
fn cross_chain_erc20_settlement(ref self: ContractState, to_chain: felt252, to_handler: u256, to_token: u256, to: u256, amount: u256) -> felt252{
__SNIP__
            let tx: CreatedCrossChainTx = CreatedCrossChainTx{
                    tx_id: tx_id,
                    from_chain: from_chain,
                    to_chain: to_chain,
                    from: get_contract_address(),
                    to: to,
@>                  from_token: self.token_address.read(), // proper token address passed
                    to_token: to_token,
                    amount: amount,
                    tx_status: CrossChainTxStatus::PENDING
                };
__SNIPP

            self.emit(
                    CrossChainLocked{
                        tx_id: tx_id,
                        from: get_caller_address(),
                        to: to,
                        from_chain: get_tx_info().unbox().chain_id,
                        to_chain: to_chain,
                        from_token: self.token_address.read(), // proper token address passed
                        to_token: to_token,
                        amount: amount
                    }
                );
            return tx_id;
        }
```

### Recommended Mitigation Steps

Use the correct `from_token` address in  `ChakraSettlementHandler::cross_chain_erc20_settlement(...)`.

```diff
diff --git a/solidity/handler/contracts/ChakraSettlementHandler.sol b/solidity/handler/contracts/ChakraSettlementHandler.sol
index 5d31ef9..b9cbd6d 100644
--- a/solidity/handler/contracts/ChakraSettlementHandler.sol
+++ b/solidity/handler/contracts/ChakraSettlementHandler.sol
@@ -157,7 +157,7 @@ contract ChakraSettlementHandler is BaseSettlementHandler, ISettlementHandler {
                 to_chain,
                 msg.sender,
                 to,
-                address(this),
+                token,
                 to_token,
                 amount,
                 CrossChainTxStatus.Pending
@@ -215,7 +215,7 @@ contract ChakraSettlementHandler is BaseSettlementHandler, ISettlementHandler {
             to,
             chain,
             to_chain,
-            address(this),
+            token,
             to_token,
             amount,
             mode
```

**[pidb (Chakra) confirmed via duplicate issue \#175](https://github.com/code-423n4/2024-08-chakra-findings/issues/175#event-14332739757)**

**[0xsomeone (judge) increased severity to High and commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/380#issuecomment-2434843302):**
 > The Warden has identified an invalid `event` emission and transaction data storage both of which are imperative to the proper operation of a cross-chain bridge system. 
> 
> The documentation of the project does not adequately detail how those events are consumed, and inspection of the project's `cairo` code as well as the sponsor's own affirmation on [issue \#175](https://github.com/code-423n4/2024-08-chakra-findings/issues/175) confirms the present implementation is incorrect.
> 
> I believe a high-risk issue is acceptable for this submission due to how crucial those components are to the proper operation of a cross-chain bridge.


***

## [[H-02] In Starknet, already processed messages can be re-submitted and by anyone](https://github.com/code-423n4/2024-08-chakra-findings/issues/334)
*Submitted by [Moksha](https://github.com/code-423n4/2024-08-chakra-findings/issues/334), also found by [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/513), [aldarion](https://github.com/code-423n4/2024-08-chakra-findings/issues/495), [ABAIKUNANBAEV](https://github.com/code-423n4/2024-08-chakra-findings/issues/486), [0xAsen](https://github.com/code-423n4/2024-08-chakra-findings/issues/477), [Tigerfrake](https://github.com/code-423n4/2024-08-chakra-findings/issues/467), [0x37](https://github.com/code-423n4/2024-08-chakra-findings/issues/452), [blackpanther](https://github.com/code-423n4/2024-08-chakra-findings/issues/428), [mjcpwns](https://github.com/code-423n4/2024-08-chakra-findings/issues/427), [kutugu](https://github.com/code-423n4/2024-08-chakra-findings/issues/417), [pwnforce](https://github.com/code-423n4/2024-08-chakra-findings/issues/394), [avoloder](https://github.com/code-423n4/2024-08-chakra-findings/issues/388), [Audinarey](https://github.com/code-423n4/2024-08-chakra-findings/issues/372), [jasonxiale](https://github.com/code-423n4/2024-08-chakra-findings/issues/324), [Daniel\_eth](https://github.com/code-423n4/2024-08-chakra-findings/issues/322), [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/303), [0xNirix](https://github.com/code-423n4/2024-08-chakra-findings/issues/270), [Emmanuel](https://github.com/code-423n4/2024-08-chakra-findings/issues/258), [Respx](https://github.com/code-423n4/2024-08-chakra-findings/issues/252), [tekkac](https://github.com/code-423n4/2024-08-chakra-findings/issues/235), [peanuts](https://github.com/code-423n4/2024-08-chakra-findings/issues/221), [b0g0](https://github.com/code-423n4/2024-08-chakra-findings/issues/196), [LuarSec](https://github.com/code-423n4/2024-08-chakra-findings/issues/131), [haxatron](https://github.com/code-423n4/2024-08-chakra-findings/issues/110), [klau5](https://github.com/code-423n4/2024-08-chakra-findings/issues/108), [said](https://github.com/code-423n4/2024-08-chakra-findings/issues/88), [shaflow2](https://github.com/code-423n4/2024-08-chakra-findings/issues/79), [Shaheen](https://github.com/code-423n4/2024-08-chakra-findings/issues/71), [mojito\_auditor](https://github.com/code-423n4/2024-08-chakra-findings/issues/62), [fyamf](https://github.com/code-423n4/2024-08-chakra-findings/issues/42), [devival](https://github.com/code-423n4/2024-08-chakra-findings/issues/233), [ZdravkoHr](https://github.com/code-423n4/2024-08-chakra-findings/issues/6), [Drynooo](https://github.com/code-423n4/2024-08-chakra-findings/issues/580), [Agontuk](https://github.com/code-423n4/2024-08-chakra-findings/issues/473), [AllTooWell](https://github.com/code-423n4/2024-08-chakra-findings/issues/432), and [PASCAL](https://github.com/code-423n4/2024-08-chakra-findings/issues/301)*

### Impact

The impact is high as the adversary can call the `receive_cross_chain_msg` with the already processed and valid parameters and benefit from it. With such parameters, anyone can call not just the validators so it further affects the protocol. Due to the missing check if the `txId` status is `UNKNOW` the attack is very much feasible as shown in the below fork testing local POC. This also breaks the main invariant mentioned in the audit docs/readme that

> A cross-chain message can only be received once. The status of a received transaction in receive\_cross\_txs must be `CrossChainMsgStatus.Unknow` before it can be processed.

### Proof of Concept

Below is the fork testing locally test case snippet and steps where the already deployed contract addresses on the `Sepolia` testnet of Starknet are used due to the nature of the bug, the attacker needs to resubmit the already processed, valid message and signatures of valid/whitelisted operators too. The sponsors have provided a notion document on the audit details page from where the contract address and other details were obtained.

Such details provided by the sponsor can be found [here](https://s3labs.notion.site/Debugging-Cairo-Contracts-34f38875fd84407099c078d84da16294).

The contract address mentioned there is a bit old and got upgraded a few times and deployed new ones too so below code snippet below has the latest one.

Step 1: Get the deployed `settlement_handler.cairo` contract address.

This is the latest one deployed on the sepolia test net starknet chain: <https://sepolia.starkscan.co/contract/0x0449f7dae3a8073aeee71a7203467d686a5227d90a9149a524787ccb0f5de54f#read-write-contract-sub-write>

Step 2: Already made call `receive_cross_chain_msg` to Step 1 contract with necessary parameters like txId, signatures (important), etc. Which succeed too i.e. that returned the `true`

This is the call: <https://sepolia.starkscan.co/call/0x03842b8ffb248e0d2f629828c3af83ff718de72be67b3a6a5acf191ad95f4706_1_1>

The mint/transfer event for the same above call

<https://sepolia.voyager.online/event/163813_0_0>

Call Overview

The call is from the Chakra chain to starknet and the payload says to transfer the chakraBTC (`handler/btc.cairo`) deployed on the testnet chain. In the next step, we would take the same parameter for the chain locally call the `receive_cross-chain_msg` multiple times, and observe the balance increase for the address in this payload. According to the payload, the address to receive is `0x8e0202cd048b6ccb8aa36d5d00ed0aa9b6d9e088` and the amount is `130000` of chakraBTC.

Step 3: Forking the chain to again call the `receive_cross_chain_msg` to `settlement_handler` contract we got in Step 1.<br>
Add the following into the `cairo/handler/Scarb.toml`

    #snip
    [[tool.snforge.fork]]
    name = "AGAINRECEIVE"
    # add the private key or get from sponsor provided ./sn_foundry
    url = "https://starknet-sepolia.g.alchemy.com/v2/private key"
    block_id.tag = "Latest"

Paste the following test snippet in the `cairo/handler/src/tests/test_settlement.cairo`.<br>
Tool version is same as sponsors `snforge: v0.20.0`

<details>

```
#[test]
#[fork("AGAINRECEIVE")]
fn test_multiple_call(){
    // handler/settlement.cairo contract deployed address on starknet sepolia
    let settlement_contract_addrs:ContractAddress= contract_address_const::<0x0449f7dae3a8073aeee71a7203467d686a5227d90a9149a524787ccb0f5de54f>();
    let settlement_dispatcher = IChakraSettlementDispatcher{contract_address: settlement_contract_addrs};
    // These parameters were obtained and transformed according to the types from the block explorer of previous call
    let cross_chain_msg_id:u256 = 82534164209879964599356552878803734303950578526030081111379082455793595623651;
    let from_chain:felt252 = 0x4368616b7261;
    let to_chain:felt252 = 0x537461726b6e6574;
    let from_handler:u256 = 445232236578399690027982039634994002761675653437;
    let to_handler:ContractAddress = contract_address_const::<0x04a399c6ff072ae2e96946af915a731c4875564083df6b39e41e65c2af25f379>();
    let sign_type:u8 = 0;
    let sig_tuple: (felt252,felt252,bool) = (0x6cd261e253b93d5fa4d2d119ce6bb1395427c3daf3560b081bd36b34135048,0x44a123c8a32499c060617121c1b09dfc8afec982dd4abf27d45abd63b88ab4d,false);
    let signatures = array![sig_tuple];
    let payload_type:u8 = 5;
    let payload = array![1, 95, 27, 243, 138, 154, 82, 64, 103, 243, 156, 169, 88, 142, 43, 183, 3, 113, 115, 180, 229, 74, 48, 79, 207, 217, 15, 129, 226, 133, 221, 162, 234, 5, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 30, 108, 62, 237, 83, 45, 74, 57, 55, 251, 225, 120, 144, 151, 57, 230, 10, 50, 126, 25, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 142, 2, 2, 205, 4, 139, 108, 203, 138, 163, 109, 93, 0, 237, 10, 169, 182, 217, 224, 136, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 5, 199, 19, 150, 75, 71, 142, 63, 31, 51, 152, 100, 49, 14, 178, 250, 216, 32, 11, 40, 170, 210, 40, 58, 167, 21, 196, 194, 123, 15, 212, 243, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 251, 208];

    // ERC20 ckr_btc contract deployed address on starkne sepolia
    // The original call or above params does the mints this ckrbtc token, amount 130000 to the address 0x8e0202cd048b6ccb8aa36d5d00ed0aa9b6d9e088
    let chakraSignetBTC_sep_addrs:ContractAddress = contract_address_const::<0x05c713964b478e3f1f339864310eb2fad8200b28aad2283aa715c4c27b0fd4f3>();
    let chakratoken_dispatcher =  IERC20Dispatcher{contract_address: chakraSignetBTC_sep_addrs};
    // balance checking before the first resubmission of same message
    let balance_its = chakratoken_dispatcher.balance_of(contract_address_const::<0x8e0202cd048b6ccb8aa36d5d00ed0aa9b6d9e088>());
    println!("Balance of addrs before calling receive_cross_chain_msg: {}",balance_its);

    // calling receive_cross_chain_msg with necessary parameters
    let return_val = settlement_dispatcher.receive_cross_chain_msg(cross_chain_msg_id,from_chain,to_chain,from_handler,to_handler,sign_type,signatures,payload,payload_type);
    assert(return_val == true,'multiple call fail');

    // balance checking after call should increase
    let chakraSignetBTC_sep_addrs:ContractAddress = contract_address_const::<0x05c713964b478e3f1f339864310eb2fad8200b28aad2283aa715c4c27b0fd4f3>();
    let chakratoken_dispatcher =  IERC20Dispatcher{contract_address: chakraSignetBTC_sep_addrs};
    let balance_its = chakratoken_dispatcher.balance_of(contract_address_const::<0x8e0202cd048b6ccb8aa36d5d00ed0aa9b6d9e088>());
    
    println!("Balance of addrs after calling receive_cross_chain_msg once: {}",balance_its);
    assert!(balance_its == 390000, "no balance inc");

    // Again calling with same parameters. everything is same from above
    let settlement_contract_addrs:ContractAddress= contract_address_const::<0x0449f7dae3a8073aeee71a7203467d686a5227d90a9149a524787ccb0f5de54f>();
    let settlement_dispatcher = IChakraSettlementDispatcher{contract_address: settlement_contract_addrs};
    // would be calling with the same params with using the same signatures and all
    let cross_chain_msg_id:u256 = 82534164209879964599356552878803734303950578526030081111379082455793595623651;
    let from_chain:felt252 = 0x4368616b7261;
    let to_chain:felt252 = 0x537461726b6e6574;
    let from_handler:u256 = 445232236578399690027982039634994002761675653437;
    let to_handler:ContractAddress = contract_address_const::<0x04a399c6ff072ae2e96946af915a731c4875564083df6b39e41e65c2af25f379>();
    let sign_type:u8 = 0;
    let sig_tuple: (felt252,felt252,bool) = (0x6cd261e253b93d5fa4d2d119ce6bb1395427c3daf3560b081bd36b34135048,0x44a123c8a32499c060617121c1b09dfc8afec982dd4abf27d45abd63b88ab4d,false);
    let signatures = array![sig_tuple];
    let payload_type:u8 = 5;
    let payload = array![1, 95, 27, 243, 138, 154, 82, 64, 103, 243, 156, 169, 88, 142, 43, 183, 3, 113, 115, 180, 229, 74, 48, 79, 207, 217, 15, 129, 226, 133, 221, 162, 234, 5, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 30, 108, 62, 237, 83, 45, 74, 57, 55, 251, 225, 120, 144, 151, 57, 230, 10, 50, 126, 25, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 142, 2, 2, 205, 4, 139, 108, 203, 138, 163, 109, 93, 0, 237, 10, 169, 182, 217, 224, 136, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 5, 199, 19, 150, 75, 71, 142, 63, 31, 51, 152, 100, 49, 14, 178, 250, 216, 32, 11, 40, 170, 210, 40, 58, 167, 21, 196, 194, 123, 15, 212, 243, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 251, 208];
    

    let return_val = settlement_dispatcher.receive_cross_chain_msg(cross_chain_msg_id,from_chain,to_chain,from_handler,to_handler,sign_type,signatures,payload,payload_type);
    assert(return_val == true,'again call fail');

    
    let chakraSignetBTC_sep_addrs:ContractAddress = contract_address_const::<0x05c713964b478e3f1f339864310eb2fad8200b28aad2283aa715c4c27b0fd4f3>();
    let chakratoken_dispatcher =  IERC20Dispatcher{contract_address: chakraSignetBTC_sep_addrs};
    let balance_its = chakratoken_dispatcher.balance_of(contract_address_const::<0x8e0202cd048b6ccb8aa36d5d00ed0aa9b6d9e088>());
    
    println!("Balance of addrs after calling receive_cross_chain_msg second call: {}",balance_its);
    assert!(balance_its == 520000, "no balance inc");
}

```

</details>

Run the `snforge test`.<br>
The test case passes and the balance of the receiver does the increase by `130000` every time we call with the same parameters.

```
➜  tests git:(main) ✗ snforge test     
   Compiling settlement_cairo v0.1.0 (/c4a/2024-08-chakra/cairo/handler/Scarb.toml)
    Finished release target(s) in 15 seconds
[WARNING] RPC node with the url https://starknet-sepolia.g.alchemy.com/v2/private_key uses incompatible version 0.6.0. Expected version: 0.7.0


Collected 1 test(s) from settlement_cairo package
Running 1 test(s) from src/
Balance of addrs before calling receive_cross_chain_msg: 260000
Balance of addrs after calling receive_cross_chain_msg once: 390000
Balance of addrs after calling receive_cross_chain_msg second call: 520000
[PASS] settlement_cairo::tests::test_settlement::test_multiple_call (gas: ~1003)
Tests: 1 passed, 0 failed, 0 skipped, 0 ignored, 0 filtered out

Latest block number = 174196 for url = https://starknet-sepolia.g.alchemy.com/v2/private-key

```

Evident from the code the `receive_cross_chain_msg` function in `handler/settlement.cairo` function lacks the validation or invariant mentioned of `CrossChainMsgStatus.Unknow` thus leads to process the already processed valid message again and again resulting in loss to the protocol <br><https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/settlement.cairo#L325-L383>

### Recommended Mitigation Steps

Add check in the `receive_cross_chain_msg` `handler/settlement.cairo` to check the cross chain status of the `txid`.

```
 assert(self.created_tx.read(cross_chain_msg_id.try_into().unwrap()).tx_status == CrossChainMsgStatus::UNKNOW, 'tx status error');

```

**[zvlwwj (Chakra) confirmed via duplicate issue \#131](https://github.com/code-423n4/2024-08-chakra-findings/issues/131#event-14356068177)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/334#issuecomment-2435058189):**
 > The Warden and its duplicates have demonstrated that it is possible to replay transactions in the Chakra system due to a lack of transaction status validation. I believe a high-risk severity rating is appropriate for this submission as it breaches a core invariant of the system and leads to fund loss.


***

## [[H-03] `SettlementSignatureVerifier` is missing check for duplicate validator signatures](https://github.com/code-423n4/2024-08-chakra-findings/issues/310)
*Submitted by [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/310), also found by [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/533), joicygiore ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/522), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/502)), [0xHelium](https://github.com/code-423n4/2024-08-chakra-findings/issues/507), aldarion ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/506), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/491)), [Sabit](https://github.com/code-423n4/2024-08-chakra-findings/issues/496), 0x37 ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/459), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/449)), [Tigerfrake](https://github.com/code-423n4/2024-08-chakra-findings/issues/433), [kutugu](https://github.com/code-423n4/2024-08-chakra-findings/issues/418), [Trooper](https://github.com/code-423n4/2024-08-chakra-findings/issues/412), [BY\_DLIFE](https://github.com/code-423n4/2024-08-chakra-findings/issues/407), [Brene](https://github.com/code-423n4/2024-08-chakra-findings/issues/398), [jasonxiale](https://github.com/code-423n4/2024-08-chakra-findings/issues/390), Coinymous ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/363), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/362), [3](https://github.com/code-423n4/2024-08-chakra-findings/issues/361)), [Cybrid](https://github.com/code-423n4/2024-08-chakra-findings/issues/357), [DanielArmstrong](https://github.com/code-423n4/2024-08-chakra-findings/issues/348), [IzuMan](https://github.com/code-423n4/2024-08-chakra-findings/issues/346), [bhilare\_](https://github.com/code-423n4/2024-08-chakra-findings/issues/341), 0x18a6 ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/331), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/300)), [kind\_killerwhale](https://github.com/code-423n4/2024-08-chakra-findings/issues/319), [0xNirix](https://github.com/code-423n4/2024-08-chakra-findings/issues/317), [Kaysoft](https://github.com/code-423n4/2024-08-chakra-findings/issues/315), calc1f4r ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/314), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/297), [3](https://github.com/code-423n4/2024-08-chakra-findings/issues/296)), [DimaKush](https://github.com/code-423n4/2024-08-chakra-findings/issues/283), [Shubham](https://github.com/code-423n4/2024-08-chakra-findings/issues/267), Respx ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/255), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/253)), [agent3bood](https://github.com/code-423n4/2024-08-chakra-findings/issues/254), b0g0 ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/250), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/202)), Taiger ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/243), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/223), [3](https://github.com/code-423n4/2024-08-chakra-findings/issues/216)), 10ap17 ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/240), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/186)), [Omik](https://github.com/code-423n4/2024-08-chakra-findings/issues/238), [tekkac](https://github.com/code-423n4/2024-08-chakra-findings/issues/237), [jesjupyter](https://github.com/code-423n4/2024-08-chakra-findings/issues/228), [Bauchibred](https://github.com/code-423n4/2024-08-chakra-findings/issues/211), Subroutine ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/203), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/190)), [eierina](https://github.com/code-423n4/2024-08-chakra-findings/issues/191), [minato7namikazi](https://github.com/code-423n4/2024-08-chakra-findings/issues/184), LuarSec ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/132), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/120)), JanuaryPersimmon2024 ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/111), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/105)), [haxatron](https://github.com/code-423n4/2024-08-chakra-findings/issues/91), said ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/87), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/82)), shaflow2 ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/75), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/3)), [mojito\_auditor](https://github.com/code-423n4/2024-08-chakra-findings/issues/61), fyamf ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/40), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/35)), [gesha17](https://github.com/code-423n4/2024-08-chakra-findings/issues/22), klau5 ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/20), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/18)), [4rdiii](https://github.com/code-423n4/2024-08-chakra-findings/issues/7), [ZdravkoHr](https://github.com/code-423n4/2024-08-chakra-findings/issues/4), [yudan](https://github.com/code-423n4/2024-08-chakra-findings/issues/401), [NexusAudits](https://github.com/code-423n4/2024-08-chakra-findings/issues/198), [Sparrow](https://github.com/code-423n4/2024-08-chakra-findings/issues/192), and [biakia](https://github.com/code-423n4/2024-08-chakra-findings/issues/74)*

### Impact

`SettlementSignatureVerifier::verifyECDSA` and `settlement::check_chakra_signatures` lack checks for duplicate validators and allow passing the threshold with a single valid signature.

### Proof of Concept

From the `README`, we see that `validators` aren’t trusted roles, they simply have to perform their duties and in case they are misbehaving `MANAGER` can remove them. It’s not expected they all to decide to perform a sybil attack.

But for this issue single validator can harm the entire protocol because signature verifiers don’t check for duplicated validators and one valid signature is enough to pass the check:

### Solidity

[SettlementSignatureVerifier.sol](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/SettlementSignatureVerifier.sol#L207)

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

As we can see nowhere do we check whether this sig is contained twice in the `signatures` argument.

Knowing that a single validator can call `ChakraSettlement::receive_cross_chain_msg` with arbitrary arguments and drain all the `ChakraSettlementHandler` balances where he is an active validator.

The caller of the function should only give valid chains and handlers, the payload will also be valid so it can be decoded but the `amount` will be the entire balance (this is the max impact, but even 1 wei is considered steal because the caller has not burned or locked any tokens by first calling the `send_cross_chain_msg` function) of the handler.

Furthermore, the entire handler can be blocked because of the missing duplicate signature check:

1.  **Single** validator can sign `message_hash` that has `ERC20TransferPayload` like this, without locking any tokens in the handler on the source chain:

    ```solidity
    ERC20TransferPayload memory payload = ERC20TransferPayload(
        ERC20Method.Transfer,
        AddressCast.to_uint256(msg.sender),
        to,//his own address on the destination chain
        AddressCast.to_uint256(token),
        to_token,
        //if SettlementMode: LockMint or MintBurn
        (type(uint256).max - IERC20(token).totalSupply())
        //if SettlementMode: LockUnlock or BurnUnlock
        IERC20(token).balanceOf(address(from_handler))
    );
    ```

2.  Then he will call the `ChakraSettlement::receive_cross_chain_msg` on the destination and signature validation will pass because he passed his signature to the `signatures` argument enough times so the `signature_verifier.verify` returns **true** (again this happens due to the missing duplicate signatures check):

    For example if the `required_validators` = 3, his `signature` bytes will look like this:

    `[0xf86c0a8502540be400825208944….0xf86c0a8502540be400825208944….0xf86c0a8502540be400825208944….]`, where dots are the remaining bytes but I think you got it ;)

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

3.  `ChakraSettlementHandler::receive_cross_chain_msg` will be executed:

    ```solidity
    bool result = ISettlementHandler(to_handler).receive_cross_chain_msg(
        txid,
        from_chain,
        from_address,
        from_handler,
        payload_type,
        payload,
        sign_type,
        signatures
    );
    ```

4.  Malicious `ERC20TransferPayload` will be encoded and the handler will either mint to the attacker the amount which will make the `totalSupply` of the token = `uint256.max` if the mode is `mint` or the entire balance of the `ChakraSettlementHandler` stealing the locked tokens of the honest users.

### Cairo

The same issue applies to the `Cairo` code as well:

[settlement.cairo](https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/settlement.cairo#L173C7-L173C8)

```rust
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

        let pub_key: felt252 = recover_public_key(message_hash,r,s,y).unwrap();
        if self.chakra_validators_pubkey.read(pub_key) > 0{
            pass_count += 1;
        }
        i += 1;
    };
    assert(pass_count >= self.required_validators_num.read(), 'Not enough validate signatures');
}
```

Here, `settlement::receive_cross_chain_msg` also can be called directly from a single validator and bypass all the checks, stealing the entire balance of the handler.

The caller of the functions should only give valid chains and handlers, the payload will also be valid so it can be decoded but the `amount` will be the entire balance (this is the max impact, even 1 wei is considered steal because the caller has not burned or locked any tokens by first calling the `send_cross_chain_msg` function) of the handler.

*In case both issues are separated because they happen in different places we split this one into two, covering both languages, so it is to be accepted by both.*

***NOTE:*** *Keep in mind that the issue shows that any validator can drain the entire protocol due to a missing duplicate signatures (used) check that allows him to do anything with only 1 signed message. The problem is not only that validators are not trusted, when the problem is fixed as below, even if a validator decides to do something like that, he can't achieve it, that's why `required_validators` is defined at all to protect the protocol from situations like this.*

In the end this single validator doesn’t lose anything, nowhere in the `README` it is mentioned that they are trusted, or any token stake is required from them, the only thing that can lose is their rights to continue signing transactions. On the other hand, they will receive the entire token supply or entire locked token balance.

### Recommended Mitigation Steps

For Solidity:

```diff
+ mapping (bytes32 msgHash => mapping(address validator => bool usedSig)) public isSignatureUsed;

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

+         address validator = msgHash.recover(sig);
          if (
-             validators[msgHash.recover(sig)] && ++m >= required_validators
+             !isSignatureUsed[msgHash][validator] && validators[validator]
          ) {
+             isSignatureUsed[msgHash][validator] = true;
+             m++;
          }

+         if (m >= required_validators) {
+             return true;
+         }
      }

      return false;
  }
```

For Cairo:

```diff
fn check_chakra_signatures(
    self: @ContractState, 
    message_hash: felt252, 
    signatures: Array<(felt252, felt252, bool)>
) {
    let mut pass_count = 0;
    let mut i = 0;
    
    // A set-like structure to keep track of processed public keys.
+   let mut processed_pub_keys: LegacyMap<felt252, u8> = LegacyMap::new();
    
    loop {
        if i > signatures.len() - 1 {
            break;
        }
        
        let (r, s, y) = *signatures.at(i);
        let pub_key: felt252 = recover_public_key(message_hash, r, s, y).unwrap();
-       if self.chakra_validators_pubkey.read(pub_key) > 0{
+       if processed_pub_keys.get(pub_key) == 0 && self.chakra_validators_pubkey.read(pub_key) > 0 {
            pass_count += 1;
+           processed_pub_keys.append(pub_key);
        }
        
        i += 1;
    }
    
    assert(pass_count >= self.required_validators_num.read(), 'Not enough valid signatures');
}
```

**[pidb (Chakra) disputed and commented on duplicate issue \#4](https://github.com/code-423n4/2024-08-chakra-findings/issues/4#issuecomment-2370037803):**
 > We added a nonce to the txid, and then will the txid be included in the signature? I think this can prevent this problem.

**[0xsomeone (judge) increased severity to High and commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/310#issuecomment-2435379419):**
 > The Warden and its duplicates have properly identified that a single signature can be repeated an arbitrary number of times to satisfy the required validator threshold with a single validator.
> 
> I believe a high-risk rating is appropriate for this submission as it represents a significant invariant breach and a compromise of the signature verification system employed within the system.


***

## [[H-04] In `settlement.cairo::receive_cross_chain_msg` - the message will always be marked with `Status::SUCCESS`](https://github.com/code-423n4/2024-08-chakra-findings/issues/167)
*Submitted by [0xAsen](https://github.com/code-423n4/2024-08-chakra-findings/issues/167), also found by [shaflow2](https://github.com/code-423n4/2024-08-chakra-findings/issues/630), [ABAIKUNANBAEV](https://github.com/code-423n4/2024-08-chakra-findings/issues/170), [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/629), and [Sabit](https://github.com/code-423n4/2024-08-chakra-findings/issues/579)*

<https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/settlement/src/settlement.cairo#L356>

<https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/handler_erc20.cairo#L135>

### Impact

When receiving a message via the `settlement.cairo::receive_cross_chain_msg()` function, a call is made to `handler.receive_cross_chain_msg` and the return value of that call is used to mark the message with status `SUCCESS` or `FAILED`

However, the way that the `handler.receive_cross_chain_msg` function is implemented, it'll always return true, therefore marking every message as successful even if the message for some reason was a corrupted one.

And breaking one of the main invariants that states the message statuses should be tracked correctly.

### Proof of Concept

Let's take a look at the code of the `receive_cross_chain_msg` function on the settlement.cairo contract, and specifically at the part where the call to `handler.receive_cross_chain_msg` is made:

```
    fn receive_cross_chain_msg(/*params*/) -> bool {
    //rest of the code

    let success = handler.receive_cross_chain_msg(
                    cross_chain_msg_id, 
                    from_chain, //from_chain
                    to_chain,  //to_chain
                    from_handler, //from_handler
                    to_handler , //to_handler
                    payload     //payload
                );

                let mut status = CrossChainMsgStatus::SUCCESS;

                if success{
                    status = CrossChainMsgStatus::SUCCESS;
                }else{
                    status = CrossChainMsgStatus::FAILED;
                }

    }
```

As you can see, the status of the messages is based on the return value of this line: `success = handler.receive_cross_chain_msg`.

Let's see the `handler.receive_cross_chain_msg` function:

```
            fn receive_cross_chain_msg(
                ref self: ContractState, 
                cross_chain_msg_id: u256, 
                from_chain: felt252, 
                to_chain: felt252,
                from_handler: u256, 
                to_handler: ContractAddress, 
                payload: Array<u8>
                ) -> bool{
                
                assert(to_handler == get_contract_address(),'error to_handler');

                assert(self.settlement_address.read() == get_caller_address(), 'not settlement');

                assert(self.support_handler.read((from_chain, from_handler)) && 
                        self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 
                        'not support handler'); 
                        //i.e (from_chain, to_handler)

                let message :Message= decode_message(payload);
                let payload_type = message.payload_type;
                
                assert(payload_type == PayloadType::ERC20, 'payload type not erc20');
                
                let payload_transfer = message.payload;
                
                let transfer = decode_transfer(payload_transfer);
                
                assert(transfer.method_id == ERC20Method::TRANSFER, 'ERC20Method must TRANSFER');
                
                let erc20 = IERC20MintDispatcher{contract_address: self.token_address.read()};
                let token = IERC20Dispatcher{contract_address: self.token_address.read()};

                // Handle the cross-chain transfer according to the settlement mode set in the contract.

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

As you can see, as long as the function doesn't revert, it'll always return `true`.

This shouldn't be the case and if for some reason the message is a corrupted one, it should get marked as `FAILED` as intended by the protocol.

The functionality is correctly implemented in the solidity version:

<details>

```
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

            if (is_valid_handler(from_chain, from_handler) == false) {
                return false;
            }

            bytes calldata msg_payload = MessageV1Codec.payload(payload);
            require(isValidPayloadType(payload_type), "Invalid payload type");

            if (payload_type == PayloadType.ERC20) {
                {
                    ERC20TransferPayload memory transfer_payload = codec
                        .deocde_transfer(msg_payload);

                    if (mode == SettlementMode.MintBurn) {
                        _erc20_mint(
                            AddressCast.to_address(transfer_payload.to),
                            transfer_payload.amount
                        );

                        return true;
                    } else if (mode == SettlementMode.LockUnlock) {
                        _erc20_unlock(
                            AddressCast.to_address(transfer_payload.to),
                            transfer_payload.amount
                        );

                        return true;
                    } else if (mode == SettlementMode.LockMint) {

                        _erc20_mint(
                            AddressCast.to_address(transfer_payload.to),
                            transfer_payload.amount
                        );
                        return true;
                    } else if (mode == SettlementMode.BurnUnlock) {
                        _erc20_unlock(
                            AddressCast.to_address(transfer_payload.to),
                            transfer_payload.amount
                        );
                        return true;
                    }
                }
            }

            return false;
        }
```

</details>

### Recommended Mitigation Steps

Implement the functionality like in the solidity handler function so it returns `false` if something goes wrong.

**[zvlwwj (Chakra) confirmed](https://github.com/code-423n4/2024-08-chakra-findings/issues/167#event-14356105164)**


***

## [[H-05] `settlement.cairo` doesn't process callback correctly leading to `CrossChainMsgStatus` marked as SUCCESS even if it failed on destination chain](https://github.com/code-423n4/2024-08-chakra-findings/issues/166)
*Submitted by [0xAsen](https://github.com/code-423n4/2024-08-chakra-findings/issues/166), also found by [Tigerfrake](https://github.com/code-423n4/2024-08-chakra-findings/issues/468), [pwnforce](https://github.com/code-423n4/2024-08-chakra-findings/issues/410), [b0g0](https://github.com/code-423n4/2024-08-chakra-findings/issues/189), [ABAIKUNANBAEV](https://github.com/code-423n4/2024-08-chakra-findings/issues/164), and [AllTooWell](https://github.com/code-423n4/2024-08-chakra-findings/issues/575)*

When a cross-chain message is sent it can return a callback with status `FAILED` or `SUCCESS`. The problem is that even if the cross-chain message failed, the original message status on the source chain would be marked as `SUCCESS`.

Let's take a look at the `receive_cross_chain_callback` function on the `settlement.cairo` contract, and more specifically the part that updates the status:

```
    fn receive_cross_chain_callback(
                ref self: ContractState,
                cross_chain_msg_id: felt252,
                from_chain: felt252,
                to_chain: felt252,
                from_handler: u256,
                to_handler: ContractAddress,
                cross_chain_msg_status: u8, <--
                sign_type: u8,
                signatures: Array<(felt252, felt252, bool)>,
            ) -> bool {
    //other functionality

    let success = handler.receive_cross_chain_callback(cross_chain_msg_id, from_chain, to_chain, from_handler, to_handler , cross_chain_msg_status);

                let mut state = CrossChainMsgStatus::PENDING;
                if success{
                    state = CrossChainMsgStatus::SUCCESS;
                }else{
                    state = CrossChainMsgStatus::FAILED;
                }

                self.created_tx.write(cross_chain_msg_id, CreatedTx{
                    tx_id:cross_chain_msg_id,
                    tx_status:state, <--- update the status 
                    from_chain: to_chain,
                    to_chain: from_chain,
                    from_handler: to_handler,
                    to_handler: from_handler
                });
```

The problem is that as long as the call to `handler.receive_cross_chain_callback` function was successful, the message as a whole will be marked in a `SUCCESS` state even though that `cross_chain_msg_status` could be SUCCESS or FAILED depending on if the message failed on the destination chain.

This could lead to a situation where a message fails to get processed on the destination chain, a callback is returned with `cross_chain_msg_status == FAILED` but the message is marked as `SUCCESS`.

That situation could be a user trying to bridge his tokens, the bridging fails so he doesn't receive his tokens on the destination chain, a callback is made and the message is marked as a `SUCCESS` even though it as not successfully executed.

And if we see the code of the `handler.receive_cross_chain_callback` function, we'll see that it'd always return true as long as it doesn't revert:

```
            fn receive_cross_chain_callback(
                ref self: ContractState, 
                cross_chain_msg_id: felt252, 
                from_chain: felt252, 
                to_chain: felt252,
                from_handler: u256, 
                to_handler: ContractAddress, 
                cross_chain_msg_status: u8 
            ) -> bool{

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

The function just performs validation of the handlers, if the settlement contract calls it and returns true. These validation could all be true but the initial message could still be with a FAILED status.

This is not taken into account and could lead to a failed message being marked as a successful one.

The implementation on the solidity contract is correct:

```
        function processCrossChainCallback(
            uint256 txid,
            string memory from_chain,
            uint256 from_handler,
            address to_handler,
            CrossChainMsgStatus status,
            uint8 sign_type,
            bytes calldata signatures
        ) internal {
            require(
                create_cross_txs[txid].status == CrossChainMsgStatus.Pending,
                "Invalid transaction status"
            );

            if (
                ISettlementHandler(to_handler).receive_cross_chain_callback( 
                    txid,
                    from_chain,
                    from_handler,
                    status,
                    sign_type,
                    signatures
                )
            ) {
                create_cross_txs[txid].status = status; <---
            
            } else {
                create_cross_txs[txid].status = CrossChainMsgStatus.Failed;
            }
        }
```

As you can see, even if the call to the handler was successful, the status is updated with the `CrossChainMsgStatus` that was passed to the function and it is not automatically marked with `SUCCESS`.

This should be the case in the cairo function as well but right now the `cross_chain_msg_status` parameter is ignored.

### Recommended Mitigation Steps

Change this line from this:

```
                if success{
                    state = CrossChainMsgStatus::SUCCESS;
```

to this:

```
                if success{
                    state = cross_chain_msg_status;
```

To be consistent with the solidity implementation.

**[zvlwwj (Chakra) confirmed](https://github.com/code-423n4/2024-08-chakra-findings/issues/166#event-14355973121)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/166#issuecomment-2434865809):**
 > The Warden has identified that the status of a cross-chain message is not properly set when a callback is performed on the source chain.
> 
> I believe a severity of high is appropriate, as a failed cross-chain transaction would indicate it was processed successfully when this vulnerability manifests.


***

## [[H-06] Forcing Starknet handlers to be whitelisted on the same chain allows exploit of `BurnUnlock` mode to drain handler funds](https://github.com/code-423n4/2024-08-chakra-findings/issues/162)
*Submitted by [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/162), also found by [ABAIKUNANBAEV](https://github.com/code-423n4/2024-08-chakra-findings/issues/169)*

### Impact

In Cairo contracts, when handling cross-chain messages or callbacks, the contract ensures that the handler on the same chain (Starknet) is whitelisted:

```rs
fn receive_cross_chain_msg(ref self: ContractState, cross_chain_msg_id: u256, from_chain: felt252, to_chain: felt252,
    from_handler: u256, to_handler: ContractAddress, payload: Array<u8>) -> bool{

        assert(to_handler == get_contract_address(),"error to_handler");
        assert(self.settlement_address.read() == get_caller_address(), "not settlement");
        assert(self.support_handler.read((from_chain, from_handler)) && 
>>>            self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), "not support handler");
    // --SNIP
}

fn receive_cross_chain_callback(ref self: ContractState, cross_chain_msg_id: felt252, from_chain: felt252, to_chain: felt252,
    from_handler: u256, to_handler: ContractAddress, cross_chain_msg_status: u8) -> bool{
        
        assert(to_handler == get_contract_address(),"error to_handler");
        assert(self.settlement_address.read() == get_caller_address(), "not settlement");
        assert(self.support_handler.read((from_chain, from_handler)) && 
>>>            self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), "not support handler");
    // --SNIP

}
```

In this context, handlers on Starknet **must** whitelist themselves as supported handlers. However, this introduces a significant vulnerability: since handlers are self-whitelisted, a malicious user could send cross-chain messages to the same chain (Starknet to Starknet) and exploit the `BurnUnlock` mode as follows:

In `BurnUnlock` mode, when a cross-chain message is sent, the user's tokens are burned, and when the message is received, the same amount of tokens is unlocked. This opens the door for malicious actors to repeatedly send cross-chain messages to themselves, resulting in a continuous unlock of tokens:

```rs
fn receive_cross_chain_msg(ref self: ContractState, cross_chain_msg_id: u256, from_chain: felt252, to_chain: felt252,
    from_handler: u256, to_handler: ContractAddress, payload: Array<u8>) -> bool{

        // --SNIP
        let erc20 = IERC20MintDispatcher{contract_address: self.token_address.read()};
        let token = IERC20Dispatcher{contract_address: self.token_address.read()};
        if self.mode.read() == SettlementMode::MintBurn{
            erc20.mint_to(u256_to_contract_address(transfer.to), transfer.amount);
        }else if self.mode.read() == SettlementMode::LockMint{
            erc20.mint_to(u256_to_contract_address(transfer.to), transfer.amount);
        }else if self.mode.read() == SettlementMode::BurnUnlock{
>>>            token.transfer(u256_to_contract_address(transfer.to), transfer.amount);
        }else if self.mode.read() == SettlementMode::LockUnlock{
            token.transfer(u256_to_contract_address(transfer.to), transfer.amount);
        }
}
```

By continuously sending cross-chain messages to the same chain, the malicious user can drain the handler's funds by repeatedly unlocking tokens to their own address. As a result, other legitimate cross-chain ERC20 operations will fail due to the depletion of ERC20 tokens in the handler contract.

### Recommended Mitigation Steps

The self-whitelisting of handlers introduces unnecessary risk and facilitates the aforementioned vulnerability. Consider removing the check that forces handlers to be self-whitelisted:

```diff
fn receive_cross_chain_msg(ref self: ContractState, cross_chain_msg_id: u256, from_chain: felt252, to_chain: felt252,
    from_handler: u256, to_handler: ContractAddress, payload: Array<u8>) -> bool{

        assert(to_handler == get_contract_address(),"error to_handler");
        assert(self.settlement_address.read() == get_caller_address(), "not settlement");
        assert(self.support_handler.read((from_chain, from_handler)) 
-            && self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), "not support handler");
    // --SNIP
}


fn receive_cross_chain_callback(ref self: ContractState, cross_chain_msg_id: felt252, from_chain: felt252, to_chain: felt252,
    from_handler: u256, to_handler: ContractAddress, cross_chain_msg_status: u8) -> bool{
        
        assert(to_handler == get_contract_address(),"error to_handler");
        assert(self.settlement_address.read() == get_caller_address(), "not settlement");
        assert(self.support_handler.read((from_chain, from_handler)) 
-           && self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), "not support handler");
    // --SNIP

}
```

**[zvlwwj (Chakra) confirmed](https://github.com/code-423n4/2024-08-chakra-findings/issues/162#event-14355975825):**

**[0xsomeone (judge) invalidated and commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/162#issuecomment-2434869733):**
 > The Warden has attempted to formulate an exploitation path of a self-cross-chain transfer; however, the assumption that a handler can be arbitrarily introduced to the system is incorrect given that the relevant function enrolling them is owner-controlled.

**[Abdessamed (warden) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/162#issuecomment-2435794246):**
 > Hi @0xsomeone -<br>
> > *“however, the assumption that a handler can be arbitrarily introduced to the system is incorrect given that the relevant function enrolling them is owner-controlled.”*
> 
> This is an incorrect statement because, as seen on the `receive_crosschain_msg`, the function enforces that both `to_chain` and `to_handler` as well as `from_chain` and `from_handler` are supported:
> ```rs
> assert(self.support_handler.read((from_chain, from_handler)) && 
>      self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), "not support handler");
> ```
> So, starknet handlers must be self-whitelisted. A malicious user can exploit this for handlers having the mode `BurnLock` and drain the handler's funds via sending cross-chain messages from starknet to starknet to repeatedly unlock tokens to their own address, as explained in details on the report.

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/162#issuecomment-2449966976):**
 > Hey @Abdessamed, thanks for your follow-up feedback. The term "self-whitelisted" is invalid as the contracts do not expose a mechanism for users to self-whitelist themselves. As whitelisting is an authoritative process (i.e. requires elevated privileges), we can safely assume that registered handlers are trusted implementations rather than arbitrary users.

**[Abdessamed (warden) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/162#issuecomment-2449990556):**
 > Hi @0xsomeone - I see where the confusion is coming from. Let me reformulate:<br>
> In this function, it checks that both `to_chain` and `to_handler` as well as `from_chain` and `from_handler` are supported:
> ```rs
> assert(self.support_handler.read((from_chain, from_handler)) && 
>        self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');
> ```
> 
> This forces the owner to already call `set_support_handler` to add Starknet handlers as supported on the Starknet handler. Otherwise, any call to `handler_erc20::receive_cross_chain_msg` will fail.
> 
> Now, given the above, an attacker makes use of that to make the attack described on the report.

**[0xsomeone (judge) increased severity to High and commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/162#issuecomment-2450034638):**
 > Hey @Abdessamed, thanks for clarifying! I see what the outlined vulnerability presently is, and can confirm it is a valid issue. This is indeed a good finding! I have re-instated a high-risk rating for it, and appreciate the due diligence during the PJQA process. 
> 
> To note, self-whitelisting is the act of whitelisting oneself; might be useful for future submissions!
> 
> Regarding comments about how the Chakra Network operates, in line with other rulings in the audit, we cannot make any assumptions as to what operations those nodes can and cannot filter, so we assume all operations are processed at "face-value" rendering this submission to be valid.


***

## [[H-07] Anyone can manipulate user nonce (`nonce_manager`) in settlement contract](https://github.com/code-423n4/2024-08-chakra-findings/issues/156)
*Submitted by [13u9](https://github.com/code-423n4/2024-08-chakra-findings/issues/156), also found by joicygiore ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/520), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/504)), aldarion ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/493), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/492)), [Agontuk](https://github.com/code-423n4/2024-08-chakra-findings/issues/472), pwnforce ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/456), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/455)), 0x37 ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/453), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/451)), [Daniel\_eth](https://github.com/code-423n4/2024-08-chakra-findings/issues/439), Abdessamed ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/420), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/419)), [kutugu](https://github.com/code-423n4/2024-08-chakra-findings/issues/415), [bhilare\_](https://github.com/code-423n4/2024-08-chakra-findings/issues/376), DPS ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/374), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/332)), jasonxiale ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/370), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/364)), [Cybrid](https://github.com/code-423n4/2024-08-chakra-findings/issues/367), [DanielArmstrong](https://github.com/code-423n4/2024-08-chakra-findings/issues/347), [IzuMan](https://github.com/code-423n4/2024-08-chakra-findings/issues/339), AllTooWell ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/321), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/227)), [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/305), [Draiakoo](https://github.com/code-423n4/2024-08-chakra-findings/issues/294), franfran20 ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/278), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/246)), Subroutine ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/263), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/219)), [0xabhay](https://github.com/code-423n4/2024-08-chakra-findings/issues/225), [0xpetern](https://github.com/code-423n4/2024-08-chakra-findings/issues/137), [LuarSec](https://github.com/code-423n4/2024-08-chakra-findings/issues/90), shaflow2 ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/81), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/77), [3](https://github.com/code-423n4/2024-08-chakra-findings/issues/31)), klau5 ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/56), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/21)), fyamf ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/51), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/37)), [gesha17](https://github.com/code-423n4/2024-08-chakra-findings/issues/24), [ZdravkoHr](https://github.com/code-423n4/2024-08-chakra-findings/issues/2), [mojito\_auditor](https://github.com/code-423n4/2024-08-chakra-findings/issues/608), and [ABAIKUNANBAEV](https://github.com/code-423n4/2024-08-chakra-findings/issues/585)*

### Impact

There is a problem that anyone can increase another handler contract nonce (`nonce_manager`) in settlement contract.

`nonce_manager` is used to make `txid`

<https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L139-L150>

<https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/ChakraSettlement.sol#L122-L133>

```
            {
                // Increment nonce for the sender
                nonce_manager[msg.sender] += 1;
            }

            uint256 txid = uint256(
                keccak256(
                    abi.encodePacked(
                        chain,
                        to_chain,
                        msg.sender, // from address for settlement to calculate txid
                        address(this), //  from handler for settlement to calculate txid
                        to_handler,
                        nonce_manager[msg.sender]
                    )
                )
            );
```

`txid` is generated using several arguments and the `nonce_manager[msg.sender]` value as shown above.

<https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L212-L222>

```
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
```

The handler function emits the corresponding `txid` value as an event.

<https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L203-L209>

```
    ///Handler code
                // Send the cross chain msg
                settlement.send_cross_chain_msg(
                    to_chain,
                    msg.sender,
                    to_handler,
                    PayloadType.ERC20,
                    cross_chain_msg_bytes
                );
```

<https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/ChakraSettlement.sol#L118-L133>

<https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/ChakraSettlement.sol#L146-L155>

    ///Settlement code
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

Before the event emit, the handler function calls `settlement.send_cross_chain_msg`. The `send_cross_chain_msg` function of settlement also creates a `txid` and emits an event using this `txid`.

Through this process, the handler contract and the settlement contract emit the same `txid` event.

The system processes this emitted `txid` to handle the task.

However, there is a vulnerability that allows anyone to manipulate the `nonce_manager` value used when generating `txid` in the settlement contract with someone else's `nonce_manager` value, which can cause confusion in the system.

### Proof of Concept

<https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L139-L150>

```
            uint256 txid = uint256(
                keccak256(
                    abi.encodePacked(
                        chain,
                        to_chain,
                        msg.sender, // from address for settlement to calculate txid
                        address(this), //  from handler for settlement to calculate txid
                        to_handler,
                        nonce_manager[msg.sender]
                    )
                )
            );
```

<https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L203-L209>

```
                // Send the cross chain msg
                settlement.send_cross_chain_msg(
                    to_chain,
                    msg.sender,
                    to_handler,
                    PayloadType.ERC20,
                    cross_chain_msg_bytes
                );
```

When the `cross_chain_erc20_settlement` function is called in the handler contract, a `txid` is generated and the `send_cross_chain_msg` function of the settlement contract is called.

```
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
```

In the `send_cross_chain_msg` function of the settlement contract, the `from_address` argument is set to the address of the user who called the `cross_chain_erc20_settlement` function of the handler set in the handler, the nonce value of the address is increased, and a `txid` is generated.

Here, the `send_cross_chain_msg` function is defined as external, so it is a function that can be called by outsiders, and since there is no other access control when increasing the nonce of `from_address` in `nonce_manager`, anyone can increase the nonce of a specific user's settlement contract.

This can cause an imbalance between the handler's nonce and the settlement's nonce, potentially causing system confusion.

Also, if the same user of another handler calls the `cross_chain_erc20_settlement` function, a mismatch between the user nonce of the handler and the settlement will occur.

### Test

```
        it('Test Manipulate another settlement contract user nonce', async () => {
            const [
                sender,
                receiver,
                attacker,
            ] = await hre.ethers.getSigners();
            const { tokenInstance, tokenOperator, codecInstance, settlmentInstance, tokenOwner, settlementHandlerInstance, settlementHnadlerOwner, messageLibTestInstance } = await loadFixture(deploySettlementHandlerFixtureMintBurn);

            const senderAddress = await sender.getAddress()
            const receiverAddress = await receiver.getAddress()
            const settlementHandlerAddress = await settlementHandlerInstance.getAddress()
            const totalAmount = 1000000;
            await tokenInstance.connect(tokenOperator).mint_to(sender, totalAmount);


            const toChain = "dst"
            const toHandler = 1
            const toToken = 1
            const receiverAddressU256 = hre.ethers.toBigInt(Buffer.from(receiverAddress.slice(2), 'hex'))
            const amount = 1000

            await tokenInstance.connect(sender).approve(settlementHandlerAddress, 1000)

            const tx = await settlementHandlerInstance.connect(sender).cross_chain_erc20_settlement(
                toChain,
                toHandler,
                toToken,
                receiverAddressU256,
                amount
            )
            const nonceBefore = await settlmentInstance.nonce_manager(senderAddress);
            console.log("Nonce value in settlement contract before attack:", nonceBefore.toString());

            const payloadType = 5; // Assuming a payload type, e.g., for an ERC20 transfer
            const payload = "0x616263"; // Example payload data ("abc" in hex)
            await(settlmentInstance.connect(attacker).send_cross_chain_msg(
                toChain,
                senderAddress, // sender address to target
                toHandler,
                payloadType,
                payload,
            ));
            const nonceAfter = await settlmentInstance.nonce_manager(senderAddress);
            console.log("Nonce value in settlement contract after attack:", nonceAfter.toString());

            const handlerNonce = await settlementHandlerInstance.nonce_manager(senderAddress);
            console.log("Handler Contract User Nonce: ", handlerNonce.toString());
            expect(nonceAfter).to.be.not.equal(handlerNonce);

        });
```

<https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/test/ChakraSettlementHandler.ts>

Write test code in `ChakraSettlementHandler.ts` file

This test code tests whether the sender's (user's) nonce value has been manipulated by the Attacker.

**Test log**

```
    ChakraSettlementHandler
        _ Should work in MintBurn mode (1238ms)
    Nonce value in settlement contract before attack: 1
    Nonce value in settlement contract after attack: 2
    Han```dler Contract User Nonce:  1
```

### Recommended Mitigation Steps

Set the nonce value in the settlement contract to be managed by `from_handler`

```
    diff --git a/solidity/settlement/contracts/BaseSettlement.sol b/solidity/settlement/contracts/BaseSettlement.sol
    index 7ac72a2..bd2ce00 100644
    --- a/solidity/settlement/contracts/BaseSettlement.sol
    +++ b/solidity/settlement/contracts/BaseSettlement.sol
    @@ -38,7 +38,8 @@ abstract contract BaseSettlement is
         ISettlementSignatureVerifier public signature_verifier;

         // Mapping for nonce manager and validators
    -    mapping(address => uint256) public nonce_manager;
    +    //mapping(address => uint256) public nonce_manager;
    +    mapping(address => mapping(address => uint256)) public nonce_manager;
         mapping(address => bool) public chakra_validators;
         uint256 public validator_count;

    diff --git a/solidity/settlement/contracts/ChakraSettlement.sol b/solidity/settlement/contracts/ChakraSettlement.sol
    index ad764f2..4c2b0c5 100644
    --- a/solidity/settlement/contracts/ChakraSettlement.sol
    +++ b/solidity/settlement/contracts/ChakraSettlement.sol
    @@ -115,9 +115,10 @@ contract ChakraSettlement is BaseSettlement {
             PayloadType payload_type,
             bytes calldata payload
         ) external {
    -        nonce_manager[from_address] += 1;
    +        // nonce_manager[from_address] += 1;

             address from_handler = msg.sender;
    +        nonce_manager[from_handler][from_address] += 1;

             uint256 txid = uint256(
                 keccak256(
```

Modify `nonce_manager` as in the code above so that the user's `nonce_manager` can increase according to the handler.

This operation prevents an attacker from manipulating someone else's nonce by pretending to be a handler, and also prevents nonce collisions between other normal handlers.

**[pidb (Chakra) confirmed](https://github.com/code-423n4/2024-08-chakra-findings/issues/156#event-14332583975)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/156#issuecomment-2434911617):**
 > The issue class of this submission concerns inconsistencies with regard to the nonce values utilized by the Chakra bridge.
> 
> This submission details how it can be maliciously sabotaged, and the remaining submissions detail how the nonces can naturally deviate. I believe that these issues are identical in nature and consider all to merit a high severity rating.


***

## [[H-08] In `settlement.cairo::receive_cross_chain_msg` - the `payload_type` can be passed by the user, confusing offchain systems](https://github.com/code-423n4/2024-08-chakra-findings/issues/147)
*Submitted by [0xAsen](https://github.com/code-423n4/2024-08-chakra-findings/issues/147), also found by [klau5](https://github.com/code-423n4/2024-08-chakra-findings/issues/617) and [fyamf](https://github.com/code-423n4/2024-08-chakra-findings/issues/605)*

### Impact

In `settlement.cairo::receive_cross_chain_msg` - the `payload_type` can be passed by the user, confusing offchain systems.

The `payload_type` parameter is only used to emit events so that the Chakra nodes can detect and process them.

There is no validation for it and given that it is used in an event to which off-chain systems listen to, the `payload_type` values will be displayed in the explorer, and there may be other extensions in the future, according to the sponsor.

This can lead to incorrect data being displayed and undefined behavior in the future.

### Proof of Concept

Let's see the code of `receive_cross_chain_msg`:

```
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
                payload_type: u8, <---
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

                // emit event
                self.emit(CrossChainHandleResult{
                    cross_chain_settlement_id: cross_chain_msg_id,
                    from_chain: to_chain,
                    from_handler: to_handler,
                    to_chain: from_chain,
                    to_handler: from_handler,
                    cross_chain_msg_status: status,
                    payload_type: payload_type <---
                });
                return true;
            }
```

You can see that the `payload_type` parameter is not used anywhere in the function except for the emission of the event.

So what could happen is:

*   a user or a bot sees the transaction being processed
*   calls the `receive_cross_chain_msg` function before the Chakra off-chain system with all the right parameters except for the `payload_type`
*   since the `payload_type` is not used in the message hash generation, the signatures verification and every other check passes successfully
*   the off-chain systems pick up wrong information from the event leading to corrupted information

### Recommended Mitigation Steps

Include the `payload_type` in the message hash generation thus making sure that it's value cannot be altered.

**[zvlwwj (Chakra) disputed and commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/147#issuecomment-2363431109):**
 > Only validator can call this function.

**[0xsomeone (judge) increased severity to High and commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/147#issuecomment-2434948388):**
 > The Warden has identified a mechanism via which the `payload_type` is not properly validated as having been signed by the Chakra team, permitting cross-chain messages to be received with a different payload type than the actual one.
> 
> I believe that a severity of high is appropriate as it should (in theory) result in a transaction being processed by the Cairo code but considered unfinished by the validator system.


***

## [[H-09] Inconsistent Handler Validation Behavior in Cairo ERC20Handler's Cross-Chain Callback](https://github.com/code-423n4/2024-08-chakra-findings/issues/141)
*Submitted by [0xNirix](https://github.com/code-423n4/2024-08-chakra-findings/issues/141), also found by [shaflow2](https://github.com/code-423n4/2024-08-chakra-findings/issues/611), Draiakoo ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/285), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/143)), [said](https://github.com/code-423n4/2024-08-chakra-findings/issues/99), [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/599), and [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/595)*

### Impact

The `receive_cross_chain_callback` function in the Cairo implementation of ERC20Handler uses an assert statement to validate handlers, which causes the function to revert if a handler is invalid or has been removed from the whitelist. This behavior differs from the Solidity implementation, which returns false for invalid handlers.

This vulnerability can lead to:

1.  Transactions remaining in a Pending state indefinitely in the Cairo implementation
2.  Inconsistent transaction states across different chain implementations
3.  Potential blocking of cross-chain operations
4.  Difficulty in handling and recovering from invalid handler scenarios

### Proof of Concept

Cairo implementation:

```
    fn receive_cross_chain_callback(ref self: ContractState, cross_chain_msg_id: felt252, from_chain: felt252, to_chain: felt252,
        from_handler: u256, to_handler: ContractAddress, cross_chain_msg_status: u8) -> bool{
        assert(to_handler == get_contract_address(),'error to_handler');
        assert(self.settlement_address.read() == get_caller_address(), 'not settlement');
        assert(self.support_handler.read((from_chain, from_handler)) && 
                self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');

        // ... rest of the function
    }
```

Solidity implementation:

```solidity
function receive_cross_chain_callback(
    uint256 txid,
    string memory from_chain,
    uint256 from_handler,
    CrossChainMsgStatus status,
    uint8 /* sign_type */,
    bytes calldata /* signatures */
) external onlySettlement returns (bool) {
    if (is_valid_handler(from_chain, from_handler) == false) {
        return false;
    }

    // ... rest of the function
}
```

```solidity
  function processCrossChainCallback(
        uint256 txid,
        string memory from_chain,
        uint256 from_handler,
        address to_handler,
        CrossChainMsgStatus status,
        uint8 sign_type,
        bytes calldata signatures
    ) internal {
        require(
            create_cross_txs[txid].status == CrossChainMsgStatus.Pending,
            "Invalid transaction status"
        );

        if (
            ISettlementHandler(to_handler).receive_cross_chain_callback(
                txid,
                from_chain,
                from_handler,
                status,
                sign_type,
                signatures
            )
        ) {
            create_cross_txs[txid].status = status;
        } else {
            create_cross_txs[txid].status = CrossChainMsgStatus.Failed;
        }
    }
```

In the Cairo version, if a handler is invalid, the function will revert due to the assert statement, leaving the transaction in its current state (likely Pending). In contrast, the Solidity version returns false, allowing the calling Settlement contract to handle the invalid handler case appropriately.

### Recommended Mitigation Steps

Update the Cairo implementation to check handler validity without using assert.

**[zvlwwj (Chakra) confirmed](https://github.com/code-423n4/2024-08-chakra-findings/issues/141#event-14356705423)**

**[0xsomeone (judge) increased severity to High](https://github.com/code-423n4/2024-08-chakra-findings/issues/141#issuecomment-2434981218)**


***

## [[H-10] `ChakraSettlement.receive_cross_chain_msg` and `ChakraSettlement.receive_cross_chain_callback` functions do not ensure that receiving `ChakraSettlement` contract's `contract_chain_name` must match `to_chain` corresponding to respective `txid` input though they should](https://github.com/code-423n4/2024-08-chakra-findings/issues/118)
*Submitted by [rbserver](https://github.com/code-423n4/2024-08-chakra-findings/issues/118), also found by [rbserver](https://github.com/code-423n4/2024-08-chakra-findings/issues/123), [jasonxiale](https://github.com/code-423n4/2024-08-chakra-findings/issues/391), [avoloder](https://github.com/code-423n4/2024-08-chakra-findings/issues/389), [Moksha](https://github.com/code-423n4/2024-08-chakra-findings/issues/379), [Coinymous](https://github.com/code-423n4/2024-08-chakra-findings/issues/360), [0xNirix](https://github.com/code-423n4/2024-08-chakra-findings/issues/316), [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/307), [Respx](https://github.com/code-423n4/2024-08-chakra-findings/issues/251), [Emmanuel](https://github.com/code-423n4/2024-08-chakra-findings/issues/247), [said](https://github.com/code-423n4/2024-08-chakra-findings/issues/104), [haxatron](https://github.com/code-423n4/2024-08-chakra-findings/issues/89), [Shaheen](https://github.com/code-423n4/2024-08-chakra-findings/issues/72), [mojito\_auditor](https://github.com/code-423n4/2024-08-chakra-findings/issues/58), [fyamf](https://github.com/code-423n4/2024-08-chakra-findings/issues/45), [klau5](https://github.com/code-423n4/2024-08-chakra-findings/issues/27), [ZdravkoHr](https://github.com/code-423n4/2024-08-chakra-findings/issues/5), ABAIKUNANBAEV ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/584), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/469)), and [Rhaydden](https://github.com/code-423n4/2024-08-chakra-findings/issues/447)*

### Impact

Because the `ChakraSettlement.receive_cross_chain_msg` function does not ensure that the receiving `ChakraSettlement` contract's `contract_chain_name` must match the `to_chain` corresponding to its `txid` input, the signatures that should only be used for calling the `ChakraSettlement.receive_cross_chain_msg` function on `to_chain` A can also be allowed to be used on `to_chain` B. As a result, the handler on `to_chain` B can incorrectly mint or transfer tokens to recipients though such recipients should only receive such token amounts on `to_chain` A and not on `to_chain` B.

Similarly, since the `ChakraSettlement.receive_cross_chain_callback` function does not ensure that the receiving `ChakraSettlement` contract's `contract_chain_name` must match the `to_chain` associated with its `txid` input, the signatures that should only be used for calling the `ChakraSettlement.receive_cross_chain_callback` function on `to_chain` A can also be allowed to be used on `to_chain` B. As a result, `to_chain` B's handler's `receive_cross_chain_callback` function logics can be incorrectly triggered, such as burning the corresponding token amount held by such handler on `to_chain` B under the `MintBurn` mode though such token amount should only be burned on `to_chain` A and not on `to_chain` B.

### Proof of Concept

When a validator is deterministically deployed, it can have the same address on different chains. When a handler is deterministically deployed, it can have the same address on different chains. Therefore, it is possible that the validators have the same addresses on two different `to_chain` chains while the number of required validators are the same on both chains, and the handler has the same address on these two `to_chain` chains as well. Moreover, such handler can whitelist the same `from_chain`-`from_handler` combination on both `to_chain` chains.

Suppose such situation occurs for `to_chain` A and B, the validators on `to_chain` A can sign for a cross-chain message in which such signatures should only be used on `to_chain` A and should not be allowed to be used on `to_chain` B. However, since the `ChakraSettlement.receive_cross_chain_msg` function does not ensure that the receiving `ChakraSettlement` contract's `contract_chain_name` must match the `to_chain` corresponding to its `txid` input, the `ChakraSettlement.receive_cross_chain_msg` function on `to_chain` B can be successfully called with the `txid`, `from_chain`, `from_address`, `from_handler`, `to_handler`, and `payload`, which were encoded in the signed message hash for the signatures that should only be used on `to_chain` A.

In this case:

*   `signature_verifier.verify(message_hash, signatures, sign_type)` would return `true` because the corresponding validators, which signed the signatures for `to_chain` A, have the same addresses on both `to_chain` A and B, and both chains have the same number of required validators;
*   `ISettlementHandler(to_handler).receive_cross_chain_msg` would be called successfully because the corresponding `to_handler` that is encoded for the signatures to be used on `to_chain` A also exists on `to_chain` B with the same address;
*   `is_valid_handler(from_chain, from_handler)` would be `true` when further calling the `ChakraSettlementHandler.receive_cross_chain_msg` function because the `from_chain`-`from_handler` combination that is encoded for the signatures to be used on `to_chain` A is also whitelisted by such `to_handler` on `to_chain` B.

Thus, such `ChakraSettlement.receive_cross_chain_msg` function call on `to_chain` B would be successful, which causes such signatures that should only be used for calling the `ChakraSettlement.receive_cross_chain_msg` function on `to_chain` A to also be allowed to be used on `to_chain` B.

<https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/settlement/contracts/ChakraSettlement.sol#L170-L244>

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
            // verify signature
@>          bytes32 message_hash = keccak256(
@>              abi.encodePacked(
@>                  txid,
@>                  from_chain,
@>                  from_address,
@>                  from_handler,
@>                  to_handler,
@>                  keccak256(payload)
@>              )
@>          );

@>          require(
@>              signature_verifier.verify(message_hash, signatures, sign_type),
@>              "Invalid signature"
@>          );

            require(
                receive_cross_txs[txid].status == CrossChainMsgStatus.Unknow,
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
        } else {
            receive_cross_txs[txid].status = CrossChainMsgStatus.Failed;
        }

        emit CrossChainHandleResult(
            txid,
            status,
            contract_chain_name,
            from_chain,
            address(to_handler),
            from_handler,
            payload_type
        );
    }
```

<https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/ChakraSettlementHandler.sol#L300-L355>

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
            return false;
        }
        bytes calldata msg_payload = MessageV1Codec.payload(payload);

        require(isValidPayloadType(payload_type), "Invalid payload type");

        if (payload_type == PayloadType.ERC20) {
            // Cross chain transfer
            {
                // Decode transfer payload
                ERC20TransferPayload memory transfer_payload = codec
                    .deocde_transfer(msg_payload);

                if (mode == SettlementMode.MintBurn) {
                    _erc20_mint(
                        AddressCast.to_address(transfer_payload.to),
                        transfer_payload.amount
                    );
                    return true;
                } else if (mode == SettlementMode.LockUnlock) {
                    _erc20_unlock(
                        AddressCast.to_address(transfer_payload.to),
                        transfer_payload.amount
                    );

                    return true;
                } else if (mode == SettlementMode.LockMint) {
                    _erc20_mint(
                        AddressCast.to_address(transfer_payload.to),
                        transfer_payload.amount
                    );
                    return true;
                } else if (mode == SettlementMode.BurnUnlock) {
                    _erc20_unlock(
                        AddressCast.to_address(transfer_payload.to),
                        transfer_payload.amount
                    );
                    return true;
                }
            }
        }

        return false;
    }
```

Similarly, when the same situation occurs for `to_chain` A and B, the `ChakraSettlement.receive_cross_chain_callback` function on `to_chain` B can also be successfully called with the `txid`, `from_handler`, `to_handler`, and `status`, which were encoded in the signed message hash for the signatures that should only be used on `to_chain` A, because the `ChakraSettlement.receive_cross_chain_callback` function does not ensure that the receiving `ChakraSettlement` contract's `contract_chain_name` must match the `to_chain` associated with its `txid` input.

For the same reasons described for the case involving the `ChakraSettlement.receive_cross_chain_msg` function, calling the `ChakraSettlement.receive_cross_chain_callback` function in this case would cause `signature_verifier.verify(message_hash, signatures, sign_type)` to return `true`, `ISettlementHandler(to_handler).receive_cross_chain_callback` to be called successfully, and `is_valid_handler(from_chain, from_handler)` to be `true` when further calling the `ChakraSettlementHandler.processCrossChainCallback` function. Hence, such `ChakraSettlement.receive_cross_chain_callback` function call on `to_chain` B would be successful, which causes such signatures that should only be used for calling the `ChakraSettlement.receive_cross_chain_callback` function on `to_chain` A to also be allowed to be used on `to_chain` B.

<https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/settlement/contracts/ChakraSettlement.sol#L256-L283>

```solidity
    function receive_cross_chain_callback(
        uint256 txid,
        string memory from_chain,
        uint256 from_handler,
        address to_handler,
        CrossChainMsgStatus status,
        uint8 sign_type,
        bytes calldata signatures
    ) external {
@>      verifySignature(
            txid,
            from_handler,
            to_handler,
            status,
            sign_type,
            signatures
        );
@>      processCrossChainCallback(
            txid,
            from_chain,
            from_handler,
            to_handler,
            status,
            sign_type,
            signatures
        );
        emitCrossChainResult(txid);
    }
```

<https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/settlement/contracts/ChakraSettlement.sol#L285-L301>

```solidity
    function verifySignature(
        uint256 txid,
        uint256 from_handler,
        address to_handler,
        CrossChainMsgStatus status,
        uint8 sign_type,
        bytes calldata signatures
    ) internal view {
        bytes32 message_hash = keccak256(
@>          abi.encodePacked(txid, from_handler, to_handler, status)
        );

        require(
@>          signature_verifier.verify(message_hash, signatures, sign_type),
            "Invalid signature"
        );
    }
```

<https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/settlement/contracts/ChakraSettlement.sol#L303-L331>

```solidity
    function processCrossChainCallback(
        uint256 txid,
        string memory from_chain,
        uint256 from_handler,
        address to_handler,
        CrossChainMsgStatus status,
        uint8 sign_type,
        bytes calldata signatures
    ) internal {
        require(
            create_cross_txs[txid].status == CrossChainMsgStatus.Pending,
            "Invalid transaction status"
        );

        if (
@>          ISettlementHandler(to_handler).receive_cross_chain_callback(
                txid,
                from_chain,
                from_handler,
                status,
                sign_type,
                signatures
            )
        ) {
            create_cross_txs[txid].status = status;
        } else {
            create_cross_txs[txid].status = CrossChainMsgStatus.Failed;
        }
    }
```

<https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/ChakraSettlementHandler.sol#L365-L396>

```solidity
    function receive_cross_chain_callback(
        uint256 txid,
        string memory from_chain,
        uint256 from_handler,
        CrossChainMsgStatus status,
        uint8 /* sign_type */, // validators signature type /  multisig or bls sr25519
        bytes calldata /* signatures */
    ) external onlySettlement returns (bool) {
        //  from_handler need in whitelist
@>      if (is_valid_handler(from_chain, from_handler) == false) {
            return false;
        }

        require(
            create_cross_txs[txid].status == CrossChainTxStatus.Pending,
            "invalid CrossChainTxStatus"
        );

        if (status == CrossChainMsgStatus.Success) {
            if (mode == SettlementMode.MintBurn) {
                _erc20_burn(address(this), create_cross_txs[txid].amount);
            }

            create_cross_txs[txid].status = CrossChainTxStatus.Settled;
        }

        if (status == CrossChainMsgStatus.Failed) {
            create_cross_txs[txid].status = CrossChainTxStatus.Failed;
        }

        return true;
    }
```

### Recommended Mitigation Steps

The `ChakraSettlement.receive_cross_chain_msg` and `ChakraSettlement.receive_cross_chain_callback` functions can be updated to check if the receiving `ChakraSettlement` contract's `contract_chain_name` matches the `to_chain` associated with the respective `txid` input and revert if not matched.

**[0xsomeone (judge) increased severity to High and commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/118#issuecomment-2435157592):**
 > The Warden outlines that replay attacks are possible when receiving funds due to the absence of the `to_chain` variable's validation. This allows the same payload signed by the Chakra validators to be replayed across multiple chains incorrectly, indicating a high-risk vulnerability.


***

## [[H-11] There is no refund mechanism in `ChakraSettlement.processCrossChainCallback` or `ChakraSettlementHandler.receive_cross_chain_callback` function](https://github.com/code-423n4/2024-08-chakra-findings/issues/115)
*Submitted by [rbserver](https://github.com/code-423n4/2024-08-chakra-findings/issues/115), also found by [0xastronatey](https://github.com/code-423n4/2024-08-chakra-findings/issues/537), Abdessamed ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/524), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/519)), [gajiknownnothing](https://github.com/code-423n4/2024-08-chakra-findings/issues/516), [abhishek\_thaku\_r](https://github.com/code-423n4/2024-08-chakra-findings/issues/503), Drynooo ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/490), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/489)), [ABAIKUNANBAEV](https://github.com/code-423n4/2024-08-chakra-findings/issues/485), [Inspecktor](https://github.com/code-423n4/2024-08-chakra-findings/issues/475), [Decap](https://github.com/code-423n4/2024-08-chakra-findings/issues/463), [0xSolus](https://github.com/code-423n4/2024-08-chakra-findings/issues/461), [Daniel\_eth](https://github.com/code-423n4/2024-08-chakra-findings/issues/460), [mjcpwns](https://github.com/code-423n4/2024-08-chakra-findings/issues/438), [0xHelium](https://github.com/code-423n4/2024-08-chakra-findings/issues/425), [kutugu](https://github.com/code-423n4/2024-08-chakra-findings/issues/416), Trooper ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/411), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/400)), [pwnforce](https://github.com/code-423n4/2024-08-chakra-findings/issues/409), blackpanther ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/405), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/404)), [Brene](https://github.com/code-423n4/2024-08-chakra-findings/issues/396), avoloder ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/386), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/358)), [AllTooWell](https://github.com/code-423n4/2024-08-chakra-findings/issues/369), [bhilare\_](https://github.com/code-423n4/2024-08-chakra-findings/issues/365), [0xNirix](https://github.com/code-423n4/2024-08-chakra-findings/issues/335), [DPS](https://github.com/code-423n4/2024-08-chakra-findings/issues/326), [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/309), [Draiakoo](https://github.com/code-423n4/2024-08-chakra-findings/issues/292), [Audinarey](https://github.com/code-423n4/2024-08-chakra-findings/issues/269), Tonchi ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/268), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/231), [3](https://github.com/code-423n4/2024-08-chakra-findings/issues/230)), Tumelo\_Crypto ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/265), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/245)), [jesjupyter](https://github.com/code-423n4/2024-08-chakra-findings/issues/262), franfran20 ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/261), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/260), [3](https://github.com/code-423n4/2024-08-chakra-findings/issues/242), [4](https://github.com/code-423n4/2024-08-chakra-findings/issues/239)), [Respx](https://github.com/code-423n4/2024-08-chakra-findings/issues/249), [0x18a6](https://github.com/code-423n4/2024-08-chakra-findings/issues/244), [0xDemon](https://github.com/code-423n4/2024-08-chakra-findings/issues/220), [Emmanuel](https://github.com/code-423n4/2024-08-chakra-findings/issues/215), [Bauchibred](https://github.com/code-423n4/2024-08-chakra-findings/issues/212), Breeje ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/206), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/205)), [agent3bood](https://github.com/code-423n4/2024-08-chakra-findings/issues/187), [MrPotatoMagic](https://github.com/code-423n4/2024-08-chakra-findings/issues/183), [b0g0](https://github.com/code-423n4/2024-08-chakra-findings/issues/181), [haxatron](https://github.com/code-423n4/2024-08-chakra-findings/issues/128), [said](https://github.com/code-423n4/2024-08-chakra-findings/issues/95), shaflow2 ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/94), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/28)), [mojito\_auditor](https://github.com/code-423n4/2024-08-chakra-findings/issues/64), [klau5](https://github.com/code-423n4/2024-08-chakra-findings/issues/43), [fyamf](https://github.com/code-423n4/2024-08-chakra-findings/issues/36), [gesha17](https://github.com/code-423n4/2024-08-chakra-findings/issues/25), and [ZdravkoHr](https://github.com/code-423n4/2024-08-chakra-findings/issues/17)*

### Impact

Because there is no refund mechanism in the `ChakraSettlement.processCrossChainCallback` or `ChakraSettlementHandler.receive_cross_chain_callback` function, when the cross-chain ERC20 settlement fails, such as due to that the source chain's handler can be removed from the whitelist for the destination chain after the corresponding cross-chain message is initiated on the source chain and before such message is received on the destination chain, the `ChakraSettlementHandler.cross_chain_erc20_settlement` function caller cannot get back and loses the tokens that have been transferred to the source chain's handler or burned on the source chain by such caller.

### Proof of Concept

When the `ChakraSettlementHandler.cross_chain_erc20_settlement` function is called to initiate a cross-chain ERC20 settlement, the function caller can check to ensure that the handler on the source chain is whitelisted on the destination chain. After such function call, the function caller has transferred tokens to the handler on the source chain under the `MintBurn`, `LockUnlock`, or `LockMint` mode or burned tokens on the source chain under the `BurnUnlock` mode.

<https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/ChakraSettlementHandler.sol#L111-L223>

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

@>      if (mode == SettlementMode.MintBurn) {
@>          _erc20_lock(msg.sender, address(this), amount);
@>      } else if (mode == SettlementMode.LockUnlock) {
@>          _erc20_lock(msg.sender, address(this), amount);
@>      } else if (mode == SettlementMode.LockMint) {
@>          _erc20_lock(msg.sender, address(this), amount);
@>      } else if (mode == SettlementMode.BurnUnlock) {
@>          _erc20_burn(msg.sender, amount);
@>      }

        ...
    }
```

Yet, after the corresponding cross-chain message is initiated on the source chain and before such message is received on the destination chain, it is possible that the `ChakraSettlementHandler.remove_handler` function is called on the destination chain, which removes the source chain's handler from the whitelist for the destination chain. This is beyond the control of the `ChakraSettlementHandler.cross_chain_erc20_settlement` function caller because such function caller cannot know this in advance.

<https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/ChakraSettlementHandler.sol#L65-L70>

```solidity
    function remove_handler(
        string memory chain_name,
        uint256 handler
    ) external onlyOwner {
@>      handler_whitelist[chain_name][handler] = false;
    }
```

When the corresponding cross-chain message is received on the destination chain, since the handler on the source chain has been changed to be not whitelisted on the destination chain, the `ChakraSettlementHandler.receive_cross_chain_msg` function would return `false`, which marks the `status` and `receive_cross_txs[txid].status` corresponding to the cross-chain message as failed in the `ChakraSettlement.receive_cross_chain_msg` function.

<https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/ChakraSettlementHandler.sol#L300-L355>

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

<https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/settlement/contracts/ChakraSettlement.sol#L170-L244>

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

@>      CrossChainMsgStatus status = CrossChainMsgStatus.Failed;
        if (result == true) {
            status = CrossChainMsgStatus.Success;
            receive_cross_txs[txid].status = CrossChainMsgStatus.Success;
@>      } else {
@>          receive_cross_txs[txid].status = CrossChainMsgStatus.Failed;
        }

        emit CrossChainHandleResult(
            txid,
            status,
            contract_chain_name,
            from_chain,
            address(to_handler),
            from_handler,
            payload_type
        );
    }
```

Back on the source chain, the `ChakraSettlement.processCrossChainCallback` and `ChakraSettlementHandler.receive_cross_chain_callback` functions are then called with the failed cross-chain message's `status`. This notifies that the corresponding cross-chain ERC20 settlement has failed by marking the corresponding `create_cross_txs[txid].status` as failed in both the `ChakraSettlement` and `ChakraSettlementHandler` contracts. However, such `ChakraSettlement.processCrossChainCallback` and `ChakraSettlementHandler.receive_cross_chain_callback` function calls do not refund the caller of the `ChakraSettlementHandler.cross_chain_erc20_settlement` function the tokens that were transferred to the source chain's handler or burned on the source chain by such caller.

<https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/settlement/contracts/ChakraSettlement.sol#L303-L331>

```solidity
    function processCrossChainCallback(
        uint256 txid,
        string memory from_chain,
        uint256 from_handler,
        address to_handler,
        CrossChainMsgStatus status,
        uint8 sign_type,
        bytes calldata signatures
    ) internal {
        require(
            create_cross_txs[txid].status == CrossChainMsgStatus.Pending,
            "Invalid transaction status"
        );

        if (
@>          ISettlementHandler(to_handler).receive_cross_chain_callback(
                txid,
                from_chain,
                from_handler,
                status,
                sign_type,
                signatures
            )
        ) {
            create_cross_txs[txid].status = status;
@>      } else {
@>          create_cross_txs[txid].status = CrossChainMsgStatus.Failed;
        }
    }
```

<https://github.com/code-423n4/2024-08-chakra/blob/f61c899c22492bdf5bdcb07cdb62ea9b4cd38825/solidity/handler/contracts/ChakraSettlementHandler.sol#L365-L396>

```solidity
    function receive_cross_chain_callback(
        uint256 txid,
        string memory from_chain,
        uint256 from_handler,
        CrossChainMsgStatus status,
        uint8 /* sign_type */, // validators signature type /  multisig or bls sr25519
        bytes calldata /* signatures */
    ) external onlySettlement returns (bool) {
        //  from_handler need in whitelist
        if (is_valid_handler(from_chain, from_handler) == false) {
            return false;
        }

        require(
            create_cross_txs[txid].status == CrossChainTxStatus.Pending,
            "invalid CrossChainTxStatus"
        );

        if (status == CrossChainMsgStatus.Success) {
            if (mode == SettlementMode.MintBurn) {
                _erc20_burn(address(this), create_cross_txs[txid].amount);
            }

            create_cross_txs[txid].status = CrossChainTxStatus.Settled;
        }

@>      if (status == CrossChainMsgStatus.Failed) {
@>          create_cross_txs[txid].status = CrossChainTxStatus.Failed;
        }

        return true;
    }
```

### Recommended Mitigation Steps

The `ChakraSettlementHandler.receive_cross_chain_callback` function can be updated to transfer the failed cross-chain ERC20 settlement's token amount to the corresponding caller of the `ChakraSettlementHandler.cross_chain_erc20_settlement` function under the `MintBurn`, `LockUnlock`, or `LockMint` mode. If possible, such function can also be updated to mint the failed cross-chain ERC20 settlement's token amount to the corresponding caller of the `ChakraSettlementHandler.cross_chain_erc20_settlement` function under the `BurnUnlock` mode; otherwise, if the corresponding token cannot be minted by the protocol, the protocol needs to clearly communicate with its users about the inability of refunding the failed cross-chain ERC20 settlement's token amount under the `BurnUnlock` mode.

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/115#issuecomment-2435474628):**
 > The submission and all its duplicates concern various ways in which the cross-chain system of the Chakra protocol can fail transactions and does not expose a mechanism to issue refunds for those failed transactions.
> 
> This issue class is significantly large, and the lack of documentation as well as insight into the Chakra node system renders it impossible to judge fairly. I believe that a refund mechanism should be set in place, and thus consider all issues related to its missing functionality to be of high severity.
> 
> To note, I believe this is a flaw arising **from the design of the system itself** and thus have grouped these issues based on the design principle they are based on. The Sponsor has expressed that the callback function is not invoked in all cases and is solely invoked in the `MintBurn` mode, indicating that a solution based on the callback mode is not in line with the desires of the Sponsor and cannot be considered the "unopinionated way" to resolve this issue. 
> 
> The lack of documentation renders granular judgments of issues outlining the absence of a refund mechanism impractical to perform as any such distinction would rely on assumptions about the system that cannot be validated.


***

## [[H-12] Handler's `receive_cross_chain_callback()` will always set the `tx_status` to `SETTLED` on source chain & burn the tokens (MintBurn Mode) even when the msg fails on destination](https://github.com/code-423n4/2024-08-chakra-findings/issues/84)
*Submitted by [Shaheen](https://github.com/code-423n4/2024-08-chakra-findings/issues/84), also found by [Tigerfrake](https://github.com/code-423n4/2024-08-chakra-findings/issues/500), [aldarion](https://github.com/code-423n4/2024-08-chakra-findings/issues/494), [0xAsen](https://github.com/code-423n4/2024-08-chakra-findings/issues/465), [0x37](https://github.com/code-423n4/2024-08-chakra-findings/issues/448), ABAIKUNANBAEV ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/445), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/343)), [AllTooWell](https://github.com/code-423n4/2024-08-chakra-findings/issues/434), [pwnforce](https://github.com/code-423n4/2024-08-chakra-findings/issues/429), [DPS](https://github.com/code-423n4/2024-08-chakra-findings/issues/325), [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/311), [0xNirix](https://github.com/code-423n4/2024-08-chakra-findings/issues/274), [Respx](https://github.com/code-423n4/2024-08-chakra-findings/issues/248), [haxatron](https://github.com/code-423n4/2024-08-chakra-findings/issues/113), [mojito\_auditor](https://github.com/code-423n4/2024-08-chakra-findings/issues/59), [klau5](https://github.com/code-423n4/2024-08-chakra-findings/issues/57), [fyamf](https://github.com/code-423n4/2024-08-chakra-findings/issues/48), [ZdravkoHr](https://github.com/code-423n4/2024-08-chakra-findings/issues/14), and [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/330)*

When a validator invokes `Settlement.cairo`'s `receive_cross_chain_callback()`, they will pass the `cross_chain_msg_status` as an input and base on that the msg status should be set on the source chain. Means, if the `cross_chain_msg_status` is given as `SUCCESS` then the msg status on the source chain will be set as `CrossChainTxStatus::SETTLED` and if it is not `SUCCESS` then it should simply set the status to `CrossChainTxStatus::FAILED` but in the cairo implementation, the `cross_chain_msg_status` is completely ignored:

```cairo
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
            ///@audit-issue M cross_chain_msg_status not checked like in the solidity instance, this will always set tx_status as settled and return true and never Failed!
            self.created_tx.write(cross_chain_msg_id, CreatedCrossChainTx{
                tx_id: created_tx.tx_id,
                from_chain: created_tx.from_chain,
                to_chain: created_tx.to_chain,
                from:created_tx.from,
                to:created_tx.to,
                from_token: created_tx.from_token,
                to_token: created_tx.to_token,
                amount: created_tx.amount,
@>              tx_status: CrossChainTxStatus::SETTLED
            });

            return true;
        }
```

The `tx_status` is directly set as `SETTLED`, which means it will be always get marked as `SETTLED` even when the Msg gets failed on the destination chain.

Also, as it doesn't check the `cross_chain_msg_status`, this will always burn the tokens (when the MODE is MintBurn), which is not the case when we look at the solidity instance

```cairo
            if self.mode.read() == SettlementMode::MintBurn{
                erc20.burn_from(get_contract_address(), self.created_tx.read(cross_chain_msg_id).amount);
            }
```

### Impact

Wrong state update and tokens burning.

### Proof of Concept

In the solidity instance both the status is checked and tokens only get burned when the status gets marked as SETTLED:

```solidity
        if (status == CrossChainMsgStatus.Success) {
            if (mode == SettlementMode.MintBurn) {
                _erc20_burn(address(this), create_cross_txs[txid].amount);
            }

            create_cross_txs[txid].status = CrossChainTxStatus.Settled;
        }

        if (status == CrossChainMsgStatus.Failed) {
            create_cross_txs[txid].status = CrossChainTxStatus.Failed;
        }
```

### Tools Used

[Shaheen's Vision](https://x.com/0x_Shaheen/status/1722664258142650806)

### Recommended Mitigation Steps

Make sure to check the given status and mark the `tx_status` base on that.

**[zvlwwj (Chakra) confirmed](https://github.com/code-423n4/2024-08-chakra-findings/issues/84#event-14357113163)**

**[0xsomeone (judge) increased severity to High and commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/84#issuecomment-2435504796):**
 > The submission details how the callback leg of a `MintBurn` mode bridge will always burn the tokens regardless of whether the transaction actually succeeded on the destination chain.
> 
> This indicates a high-risk issue within the codebase that would lead to fund loss if the destination chain's execution fails.


***

## [[H-13] The `LockMint` and `BurnUnlock` modes cannot be used](https://github.com/code-423n4/2024-08-chakra-findings/issues/30)
*Submitted by [shaflow2](https://github.com/code-423n4/2024-08-chakra-findings/issues/30), also found by shaflow2 ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/97), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/33)), [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/578), [Daniel\_eth](https://github.com/code-423n4/2024-08-chakra-findings/issues/443), and Emmanuel ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/195), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/194))*

### Lines of code

<https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L127>

<https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L338>

<https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/handler_erc20.cairo#L127>

### Impact

`LockMint` and `BurnUnlock` modes refer to the following:

*   `LockMint`: Tokens are locked on the source chain and minted on the target chain.
*   `BurnUnlock`: Tokens are burned on the source chain and unlocked on the target chain.

However, because the `ChakraSettlementHandler` protocol is responsible for both processing remote `cross-chain messages` and sending `cross-chain messages` to remote chains, a single mode setting cannot handle both tasks simultaneously. This results in one of the tasks' functionalities being unavailable due to incorrect protocol implementation.

### Proof of Concept

When the `LockMint` mode is used, it means that the source chain employs the `LockUnlock` mode. Therefore, during the receive cross-chain message, tokens should not be minted but rather unlocked.

Similarly, when the `BurnUnlock` mode is used, it means that the source chain employs the `MintBurn` mode. Thus, during the receive cross-chain message, tokens should not be unlocked but rather minted.

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
        ...
        if (payload_type == PayloadType.ERC20) {
            {
                ERC20TransferPayload memory transfer_payload = codec
                    .deocde_transfer(msg_payload);
                if (mode == SettlementMode.MintBurn) {
                    ...
                } else if (mode == SettlementMode.LockUnlock) {
                    ...
                } else if (mode == SettlementMode.LockMint) {
                    _erc20_mint(
                        AddressCast.to_address(transfer_payload.to),
                        transfer_payload.amount
                    );
                    return true;
                } else if (mode == SettlementMode.BurnUnlock) {
                    _erc20_unlock(
                        AddressCast.to_address(transfer_payload.to),
                        transfer_payload.amount
                    );
                    return true;
                }
            }
        }
        ...
    }
```

In the Cairo program, the same issue also exists.

```rust
    #[abi(embed_v0)]
    impl ERC20HandlerImpl of IERC20Handler<ContractState> {
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

### Recommended Mitigation Steps

The following is the correct logic:

```diff
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
        if (is_valid_handler(from_chain, from_handler) == false) {
            return false;
        }
        bytes calldata msg_payload = MessageV1Codec.payload(payload);

        require(isValidPayloadType(payload_type), "Invalid payload type");

        if (payload_type == PayloadType.ERC20) {
            // Cross chain transfer
            {
                // Decode transfer payload
                ERC20TransferPayload memory transfer_payload = codec
                    .deocde_transfer(msg_payload);

                if (mode == SettlementMode.MintBurn) {
                    _erc20_mint(
                        AddressCast.to_address(transfer_payload.to),
                        transfer_payload.amount
                    );
                    return true;
                } else if (mode == SettlementMode.LockUnlock) {
                    _erc20_unlock(
                        AddressCast.to_address(transfer_payload.to),
                        transfer_payload.amount
                    );

                    return true;
                } else if (mode == SettlementMode.LockMint) {
-                   _erc20_mint(
-                       AddressCast.to_address(transfer_payload.to),
-                       transfer_payload.amount
-                   );
+                   _erc20_unlock(
+                       AddressCast.to_address(transfer_payload.to),
+                       transfer_payload.amount
+                   );
                    return true;
                } else if (mode == SettlementMode.BurnUnlock) {
-                   _erc20_unlock(
-                       AddressCast.to_address(transfer_payload.to),
-                       transfer_payload.amount
-                   );
+                   _erc20_mint(
+                       AddressCast.to_address(transfer_payload.to),
+                       transfer_payload.amount
+                   );
                    return true;
                }
            }
        }

        return false;
    }
```

In Cairo:

```diff
    impl ERC20HandlerImpl of IERC20Handler<ContractState> {
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
-               erc20.mint_to(u256_to_contract_address(transfer.to), transfer.amount);
+               token.transfer(u256_to_contract_address(transfer.to), transfer.amount);

            }else if self.mode.read() == SettlementMode::BurnUnlock{
-               token.transfer(u256_to_contract_address(transfer.to), transfer.amount);
+               erc20.mint_to(u256_to_contract_address(transfer.to), transfer.amount);
            }else if self.mode.read() == SettlementMode::LockUnlock{
                token.transfer(u256_to_contract_address(transfer.to), transfer.amount);
            }
            
            return true;
        }
```

**[pidb (Chakra) confirmed](https://github.com/code-423n4/2024-08-chakra-findings/issues/30#event-14332657709)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/30#issuecomment-2435282946):**
 > The Warden and its duplicates outline a **design-related flaw** that is shared across the Solidity and Cairo implementations in relation to how the `LockMint` and `BurnUnlock` systems are defined, disallowing certain configurations from ever functioning properly. These configurations are expected to be a normal likelihood event due to the system's intents to be deployed across multiple chains, rendering this submission and its duplicates to be proper high-risk criticism of the system's design.


***

## [[H-14] Malicious actors can manipulate the `cross_chain_callback` callback](https://github.com/code-423n4/2024-08-chakra-findings/issues/11)
*Submitted by [shaflow2](https://github.com/code-423n4/2024-08-chakra-findings/issues/11), also found by [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/531), [gajiknownnothing](https://github.com/code-423n4/2024-08-chakra-findings/issues/529), [Drynooo](https://github.com/code-423n4/2024-08-chakra-findings/issues/488), [0x37](https://github.com/code-423n4/2024-08-chakra-findings/issues/454), [0xAsen](https://github.com/code-423n4/2024-08-chakra-findings/issues/399), [Audinarey](https://github.com/code-423n4/2024-08-chakra-findings/issues/356), [Draiakoo](https://github.com/code-423n4/2024-08-chakra-findings/issues/291), [b0g0](https://github.com/code-423n4/2024-08-chakra-findings/issues/241), [agent3bood](https://github.com/code-423n4/2024-08-chakra-findings/issues/218), [MrPotatoMagic](https://github.com/code-423n4/2024-08-chakra-findings/issues/188), [fyamf](https://github.com/code-423n4/2024-08-chakra-findings/issues/34), [gesha17](https://github.com/code-423n4/2024-08-chakra-findings/issues/23), and [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/596)*

### Impact

Because the validator's signature message does not include the `from_chain` field, a malicious actor can preemptively execute the validator's transaction with an incorrect `from_chain` field. This can cause the status of `create_cross_txs[txid]` to become a `Failed` state, preventing it from being executed again.

### Proof of Concept

This is the `receive_cross_chain_callback` function

```solidity
    function receive_cross_chain_callback(
        uint256 txid,
        string memory from_chain,
        uint256 from_handler,
        address to_handler,
        CrossChainMsgStatus status,
        uint8 sign_type,
        bytes calldata signatures
    ) external {
        verifySignature(
            txid,
            from_handler,
            to_handler,
            status,
            sign_type,
            signatures
        );
        processCrossChainCallback(
            txid,
            from_chain,
            from_handler,
            to_handler,
            status,
            sign_type,
            signatures
        );
        emitCrossChainResult(txid);
    }
```

In the signature verification process, we found that the signature message does not include the `from_chain` field.

```solidity
    function verifySignature(
        uint256 txid,
        uint256 from_handler,
        address to_handler,
        CrossChainMsgStatus status,
        uint8 sign_type,
        bytes calldata signatures
    ) internal view {
        bytes32 message_hash = keccak256(
            abi.encodePacked(txid, from_handler, to_handler, status)
        );

        require(
            signature_verifier.verify(message_hash, signatures, sign_type),
            "Invalid signature"
        );
    }
```

In this scenario, a malicious actor could execute the following attack steps:

1.  Front-run the caller's transaction, providing correct signatures and other parameters, but with an incorrect `from_chain` field, causing the verifySignature validation to pass.
2.  In the `processCrossChainCallback` function, call `handler::receive_cross_chain_callback`.
3.  Due to the incorrect `from_chain`, the `is_valid_handler` function returns false, which causes `handler::receive_cross_chain_callback` to return false.

```solidity
        if (is_valid_handler(from_chain, from_handler) == false) {
            return false;
        }
```

4.  If `handler::receive_cross_chain_callback returns` false, it will cause `create_cross_txs[txid].status` to be set to `Failed`.

```solidity
        if (
            ISettlementHandler(to_handler).receive_cross_chain_callback(
                txid,
                from_chain,
                from_handler,
                status,
                sign_type,
                signatures
            )
        ) {
            create_cross_txs[txid].status = status;
        } else {
            create_cross_txs[txid].status = CrossChainMsgStatus.Failed;
        }
```

### Recommended Mitigation Steps

```diff
    function receive_cross_chain_callback(
        uint256 txid,
        string memory from_chain,
        uint256 from_handler,
        address to_handler,
        CrossChainMsgStatus status,
        uint8 sign_type,
        bytes calldata signatures
    ) external {
        verifySignature(
            txid,
+           from_chain
            from_handler,
            to_handler,
            status,
            sign_type,
            signatures
        );
        ...
    }
```

```diff
    function verifySignature(
        uint256 txid,
+       string memory from_chain,
        uint256 from_handler,
        address to_handler,
        CrossChainMsgStatus status,
        uint8 sign_type,
        bytes calldata signatures
    ) internal view {
        bytes32 message_hash = keccak256(
-            abi.encodePacked(txid, from_handler, to_handler, status)
+            abi.encodePacked(txid, from_chain, to_handler, status)
        );

        require(
            signature_verifier.verify(message_hash, signatures, sign_type),
            "Invalid signature"
        );
    }
```

**[pidb (Chakra) disputed and commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/11#issuecomment-2360518540):**
 > This `from_chain` parameter is not important, as long as you ensure that the txid unique signature cannot be constructed repeatedly, currently txid satisfies this.
> 
> I think it should be downgraded to Medium risk, because txid can prevent it.

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/11#issuecomment-2435437226):**
 > The Warden has identified a mechanism via which the third leg of a transaction can be blocked via a front-running attack, causing the transaction to indicate a failure status even though it would have normally been executed otherwise.
> 
> I consider this to be a valid high-severity issue as the status of all transactions can be trivially sabotaged to a failure state during their final callback leg.


***
 
# Medium Risk Findings (12)
## [[M-01] Excessive Authority Granted to Managers in the `ckr_btc.cairo` Contract Presents Significant Management Risks](https://github.com/code-423n4/2024-08-chakra-findings/issues/514)
*Submitted by [joicygiore](https://github.com/code-423n4/2024-08-chakra-findings/issues/514), also found by [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/512), [Tigerfrake](https://github.com/code-423n4/2024-08-chakra-findings/issues/483), [m4k2](https://github.com/code-423n4/2024-08-chakra-findings/issues/354), [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/308), [devival](https://github.com/code-423n4/2024-08-chakra-findings/issues/229), [haxatron](https://github.com/code-423n4/2024-08-chakra-findings/issues/107), [said](https://github.com/code-423n4/2024-08-chakra-findings/issues/83), [fyamf](https://github.com/code-423n4/2024-08-chakra-findings/issues/49), and [peanuts](https://github.com/code-423n4/2024-08-chakra-findings/issues/282)*

In the `ckr_btc.cairo` contract, managers possess broad authority and can execute all functions except `upgrade()`. This level of access contrasts with typical Solidity practices, where such functions would require `owner` privileges.

One of the primary concerns is that any existing manager has the ability to add new managers. This unchecked ability to expand the number of managers can lead to an uncontrolled increase in the number of authorized managers, creating a potential security risk. Without additional checks or approval mechanisms, this design flaw could be exploited, leading to a dilution of control and increased risk of unauthorized actions.

Furthermore, managers also have the ability to designate operator roles. Operators, in turn, have the authority to mint and burn tokens, which compounds the risk if these roles are not properly managed. This level of access could easily lead to a situation where control over critical functions is decentralized in a manner that might not have been intended by the original design.

It is unclear whether this design was intentional, but it introduces significant management risks that should be addressed.

```js
        fn add_manager(ref self: ContractState, new_manager: ContractAddress) -> bool {
            let caller = get_caller_address();
@>            assert(self.chakra_managers.read(caller) == 1, Errors::NOT_MANAGER);
            assert(self.chakra_managers.read(new_manager) == 0, Errors::ALREADY_MANAGER);


            self.chakra_managers.write(new_manager, 1);
            self
                .emit(
                    ManagerAdded {
                        operator: caller, new_manager: new_manager, added_at: get_block_timestamp()
                    }
                );
            return self.chakra_managers.read(new_manager) == 1;
        }
        fn add_operator(ref self: ContractState, new_operator: ContractAddress) -> bool {
            let caller = get_caller_address();
@>            assert(self.chakra_managers.read(caller) == 1, Errors::NOT_MANAGER);
            assert(self.chakra_operators.read(new_operator) == 0, Errors::ALREADY_OPERATOR);


            self.chakra_operators.write(new_operator, 1);
            self
                .emit(
                    OperatorAdded { new_operator: new_operator, added_at: get_block_timestamp() }
                );
            return self.chakra_operators.read(new_operator) == 1;
        }

        fn mint_to(ref self: ContractState, to: ContractAddress, amount: u256) -> bool {
            let caller = get_caller_address();
@>            assert(self.chakra_operators.read(caller) == 1, Errors::NOT_OPERATOR);
            let old_balance = self.erc20.balance_of(to);
            self.erc20.mint(to, amount);
            let new_balance = self.erc20.balance_of(to);
            return new_balance == old_balance + amount;
        }
```

### Impact

The excessive authority granted to managers poses a significant management risk. The potential for an uncontrolled expansion of manager roles, coupled with the ability to assign operator roles, could lead to serious security vulnerabilities, including unauthorized minting or burning of tokens.

### Recommended Mitigation Steps

It is recommended to follow best practices as implemented in Solidity contracts, where only the `owner` has the authority to add or remove managers and operators. This can be achieved by modifying the current implementation to enforce `owner` checks when adding new managers or operators.

Example of a safer approach:

```diff
    fn add_manager(ref self: ContractState, new_manager: ContractAddress) -> bool {
            let caller = get_caller_address();
-            assert(self.chakra_managers.read(caller) == 1, Errors::NOT_MANAGER);
+            self.ownable.assert_only_owner();
            assert(self.chakra_managers.read(new_manager) == 0, Errors::ALREADY_MANAGER);


            self.chakra_managers.write(new_manager, 1);
            self
                .emit(
                    ManagerAdded {
                        operator: caller, new_manager: new_manager, added_at: get_block_timestamp()
                    }
                );
            return self.chakra_managers.read(new_manager) == 1;
        }
    fn add_operator(ref self: ContractState, new_operator: ContractAddress) -> bool {
            let caller = get_caller_address();
-            assert(self.chakra_managers.read(caller) == 1, Errors::NOT_MANAGER);
+            self.ownable.assert_only_owner();
            assert(self.chakra_operators.read(new_operator) == 0, Errors::ALREADY_OPERATOR);


            self.chakra_operators.write(new_operator, 1);
            self
                .emit(
                    OperatorAdded { new_operator: new_operator, added_at: get_block_timestamp() }
                );
            return self.chakra_operators.read(new_operator) == 1;
        }
```

**[zvlwwj (Chakra) confirmed via duplicate issue \#107](https://github.com/code-423n4/2024-08-chakra-findings/issues/107#event-14357100777)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/514#issuecomment-2435173920):**
 > The Warden and its duplicates have identified a potential privilege escalation exploitation path whereby a single manager can overtake the system by removing all others and then introducing malicious variants of themselves. I believe that this breaches the documentation of the system and is a form of privilege escalation as managers should collectively authorize operations.


***

## [[M-02] Missing `ERC20Method` validation at destination allows non-transfer tx to be handled as transfers](https://github.com/code-423n4/2024-08-chakra-findings/issues/482)
*Submitted by [Tigerfrake](https://github.com/code-423n4/2024-08-chakra-findings/issues/482), also found by [said](https://github.com/code-423n4/2024-08-chakra-findings/issues/80)*

### Impact

In cross-chain transactions, the integrity and correctness of the transaction must be maintained across different blockchain environments, which might have varying security measures, protocols. However, the missing `ERC20method` validation at destination allows cross-chain tx with a different `ERC20Method` from `Transfer` to be handled as transfer transactions when they actually aren't.

### Proof of Concept

When sending a cross-chain tx, the `sender` locks/burns some amount of tokens at `source` chain. With this, the `recipient` then unlocks or gets minted same amount of tokens at the `destination`. Basically this is similar to `Token Transfer` from one address to another.

As such, [`handler_erc20::receive_cross_chain_msg()`](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/handler_erc20.cairo#L122) checks to ensure that `ERC20Method` is `TRANSFER` at destination before handling tokens:

```solidity
    assert(transfer.method_id == ERC20Method::TRANSFER, 'ERC20Method must TRANSFER');
```

Checking for the `ERC20Method` at the destination is crucial due to the nature of cross-chain transactions and the need for validation and security on both ends of the transaction.

However [`ChakraSettlementHandler::receive_cross_chain_msg()`](https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/solidity/handler/contracts/ChakraSettlementHandler.sol#L318-L330) only decodes the transfer payload and proceeds to handle tokens without actually verifying that the method is transfer.

```solidity
        if (payload_type == PayloadType.ERC20) {
            // Cross chain transfer
            {
                // Decode transfer payload
                ERC20TransferPayload memory transfer_payload = codec
                    .deocde_transfer(msg_payload);
>>              // @audit-info Missing method validation
                if (mode == SettlementMode.MintBurn) {
                    _erc20_mint(
                        AddressCast.to_address(transfer_payload.to),
                        transfer_payload.amount
                    );
                    return true;
                }
                ---SNIP---
            }
            ---SNIP---
        }
```

### Recommended Mitigation Steps

`ERC20Method` should be validated before handling tokens in `receive_cross_chain_msg()`:

```diff
        if (payload_type == PayloadType.ERC20) {
            // Cross chain transfer
            {
                // Decode transfer payload
                ERC20TransferPayload memory transfer_payload = codec
                    .deocde_transfer(msg_payload);
+               require(transfer_payload.method_id == ERC20Method.Transfer, "ERC20Method must TRANSFER");                

                if (mode == SettlementMode.MintBurn) {
                    _erc20_mint(
                        AddressCast.to_address(transfer_payload.to),
                        transfer_payload.amount
                    );
                    return true;
                }
                ---SNIP---
            }
            ---SNIP---
        }
```

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/482#issuecomment-2435205631):**
 > The Solidity counterpart of the Chakra system does not validate that the decoded EIP-20 operation is an `ERC20Method::Transfer` and ignores its status.
> 
> As the Chakra node system is out of the scope of this audit, I am unable to properly deduce the likelihood as well as the feasibility of this variable being any different.
> 
> I consider this submission to be a correct medium-risk issue as a result given that operations other than transfers would be assumed to be transfers.


***

## [[M-03] Inconsistency in sender address when creating cross chain messages on Starknet can lead to loss of funds](https://github.com/code-423n4/2024-08-chakra-findings/issues/327)
*Submitted by [Audinarey](https://github.com/code-423n4/2024-08-chakra-findings/issues/327), also found by [AllTooWell](https://github.com/code-423n4/2024-08-chakra-findings/issues/620), [said](https://github.com/code-423n4/2024-08-chakra-findings/issues/616), [fyamf](https://github.com/code-423n4/2024-08-chakra-findings/issues/607), [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/593), [b0g0](https://github.com/code-423n4/2024-08-chakra-findings/issues/185), [Tigerfrake](https://github.com/code-423n4/2024-08-chakra-findings/issues/174), [mojito\_auditor](https://github.com/code-423n4/2024-08-chakra-findings/issues/60), [Draiakoo](https://github.com/code-423n4/2024-08-chakra-findings/issues/576), and [jasonxiale](https://github.com/code-423n4/2024-08-chakra-findings/issues/590)*

### Lines of code

<https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/handler_erc20.cairo#L188>

<https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/handler_erc20.cairo#L222>

### Impact

*   Funds could get stuck in the `handler_erc20.cairo` contract.
*   Validators can evaluate transactions wrongly.

### Proof of Concept

In the `handler_erc20::cross_chain_erc20_settlement(...)` function, the `tx_id` is saved with the `CreatedCrossChainTx` struct which contains info about the transaction including the sender whose account the token was transferred from.

However, on L188 the `from` value is supposed to be the caller's address, but the `handler_erc20` address is used instead of the `get_caller_address()`.

Moreso, the event that are being used by the validators uses `from: get_caller_address(),`.

```rust
File: handler_erc20.cairo
167:         fn cross_chain_erc20_settlement(ref self: ContractState, to_chain: felt252, to_handler: u256, to_token: u256, to: u256, amount: u256) -> felt252{
168:             assert(self.support_handler.read((to_chain, to_handler)), 'not support handler');
169:             let settlement = IChakraSettlementDispatcher {contract_address: self.settlement_address.read()};
170:             let from_chain = settlement.chain_name();
171:             let token = IERC20Dispatcher{contract_address: self.token_address.read()};
172:             let token_burnable = IERC20MintDispatcher{contract_address: self.token_address.read()};
173:             if self.mode.read() == SettlementMode::MintBurn{
174:                 token.transfer_from(get_caller_address(), get_contract_address(), amount);
SNIP        .......
182:             
183:             let tx_id = LegacyHash::hash(get_tx_info().unbox().transaction_hash, self.msg_count.read());
184:             let tx: CreatedCrossChainTx = CreatedCrossChainTx{
185:                     tx_id: tx_id,
186:                     from_chain: from_chain,
187:                     to_chain: to_chain,
188:     @>              from: get_contract_address(), // @audit 8) wrong address used for sender when creating cc tx SUGG: replace with get_caller_address()
189:                     to: to,
190:                     from_token: self.token_address.read(),
191:                     to_token: to_token,
192:                     amount: amount,
193:                     tx_status: CrossChainTxStatus::PENDING
194:                 };

SNIP        .......

219:             self.emit(
220:                     CrossChainLocked{
221:                         tx_id: tx_id,
222:                         from: get_caller_address(),
223:                         to: to,
224:                         from_chain: get_tx_info().unbox().chain_id,
225:                         to_chain: to_chain,
226:    @>                   from_token: self.token_address.read(),
227:                         to_token: to_token,
228:                         amount: amount
229:                     }
230:                 );
231:             return tx_id;
232:         }

```

The problem is that

*   Since it is not clear from the audit README or the Docs how the validators would use the event, the event contains both the `tx_id` (formed with a wrong `from` value) and the correct `from` value, transactions could be processed erroneously.
*   If the transactions are processed wrongly, then the funds could be stuck in the contract. Without a way to retrieve them, this is a loss to the user.

### Recommended Mitigation Steps

Modify the `handler_erc20::cross_chain_erc20_settlement(...)` function as shown below:

```rust
File: handler_erc20.cairo
167:         fn cross_chain_erc20_settlement(ref self: ContractState, to_chain: felt252, to_handler: u256, to_token: u256, to: u256, amount: u256) -> felt252{
168:             assert(self.support_handler.read((to_chain, to_handler)), 'not support handler');
169:             let settlement = IChakraSettlementDispatcher {contract_address: self.settlement_address.read()};
170:             let from_chain = settlement.chain_name();
171:             let token = IERC20Dispatcher{contract_address: self.token_address.read()};
172:             let token_burnable = IERC20MintDispatcher{contract_address: self.token_address.read()};
173:             if self.mode.read() == SettlementMode::MintBurn{
174:                 token.transfer_from(get_caller_address(), get_contract_address(), amount);
SNIP        .......
182:             
183:             let tx_id = LegacyHash::hash(get_tx_info().unbox().transaction_hash, self.msg_count.read());
184:             let tx: CreatedCrossChainTx = CreatedCrossChainTx{
185:                     tx_id: tx_id,
186:                     from_chain: from_chain,
187:                     to_chain: to_chain,
-188:                    from: get_contract_address(),
+188:                    from: get_caller_address(),
189:                     to: to,
190:                     from_token: self.token_address.read(),
191:                     to_token: to_token,
192:                     amount: amount,
193:                     tx_status: CrossChainTxStatus::PENDING
194:                 };

SNIP        .......

219:             self.emit(
220:                     CrossChainLocked{
221:                         tx_id: tx_id,
222:                         from: get_caller_address(),
223:                         to: to,
224:                         from_chain: get_tx_info().unbox().chain_id,
225:                         to_chain: to_chain,
226:                         from_token: self.token_address.read(),
227:                         to_token: to_token,
228:                         amount: amount
229:                     }
230:                 );
231:             return tx_id;
232:         }


```

**[zvlwwj (Chakra) confirmed via duplicate issue \#174](https://github.com/code-423n4/2024-08-chakra-findings/issues/174#event-14355954117)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/327#issuecomment-2434853076):**
 > The Warden has identified an inconsistency in the way cross-chain message events are emitted and stored when the `handler_erc20::cross_chain_erc20_settlement` function is invoked.
> 
> Given that the documentation of the project is inadequate to properly assess the severity of the event emissions, I believe that estimating this discrepancy as a high-severity issue is appropriate given that events are usually imperative to the proper function of cross-chain bridges.

**[Abdessamed (warden) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/327#issuecomment-2435831766):**
 > This is QA. There is indeed a wrong `from` set on the created struct, **BUT**, this information is not used anywhere else that could result in meaningful impact because:
> 
> - The tokens are [correctly locked or burned](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/handler_erc20.cairo#L173-L181) from the caller, and the Chakra nodes rely on the `to` argument to mint/unlock the tokens on the destination chain.

**[0xsomeone (judge) decreased severity to Medium and commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/327#issuecomment-2449893455):**
 > After re-evaluating this particular submission, I am inclined to downgrade it to medium severity.
> 
> I agree with @Abdessamed in that the event is actually emitted with the correct parameters but the `struct` is stored incorrectly which would normally make it QA, however, we have no way of knowing (nor can we make any assumptions about) how the nodes operate.
> 
> At the very least, off-chain software that attempts to showcase which transactions a user has made will fail to do so properly. In a worst-case scenario, failed transaction refunds (which we all know are nowhere implemented within the code but could theoretically be handled off-chain) would fail to be credited to the correct recipient. In a worst-case scenario, all transactions could fail to be processed due to the off-chain software attempting to validate the event's data with the data stored on the chain.
> 
> I personally believe that the code of the Chakra nodes would hint toward a QA severity rating for this submission, however, I am inclined to consider it a medium-risk issue due to the known impact outlined above and the unknown possibility of a higher severity impact.


***

## [[M-04] Incorrect Decimals Setting for ckrBTC Token May Lead to User Confusion and Inaccurate Transaction Amounts](https://github.com/code-423n4/2024-08-chakra-findings/issues/176)
*Submitted by [Xor0v0](https://github.com/code-423n4/2024-08-chakra-findings/issues/176), also found by [AllTooWell](https://github.com/code-423n4/2024-08-chakra-findings/issues/436) and [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/628)*

### Impact

In the OpenZeppelin library, the decimals of the ERC20 component defaults to 18, which is abnormal for BTC. Incorrect decimal settings may result in users entering incorrect amounts or understanding incorrect balances during transactions. This confusion may lead to property damage or transaction failure, especially when the transaction amount is large.

On the other hand, many tools, applications, or smart contracts related to Bitcoin may rely on an accuracy of 8 decimal places. If the accuracy setting is incorrect, these tools or contracts may not work properly, thereby affecting the operation of the entire ecosystem.

### Proof of Concept

<https://github.com/code-423n4/2024-08-chakra/blob/abef77d95866f2fec93270491fc5abc9ab14f86d/cairo/handler/src/ckr_btc.cairo#L78>

### Recommended Mitigation Steps

Rewrite the decimals to 8 for the ckrBTC token.

**[zvlwwj (Chakra) confirmed](https://github.com/code-423n4/2024-08-chakra-findings/issues/176#event-14356083337)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/176#issuecomment-2434840240):**
 > The Warden has identified that the `ckrBTC` token on the Starknet network has a different number of decimals than on other networks, causing the `ckrBTC` variant of the Starknet network to be consistently overvalued.
> 
> I do not envision any impact from this discrepancy apart from the value per whole unit of `ckrBTC` token on the Starknet network being higher than the value per whole unit of `ckrBTC` token on other networks. As such, I believe a medium-risk rating is acceptable.


***

## [[M-05] Settlement contract is mistakenly used for the handler contract when assigning `ReceivedCrossChainTx` struct](https://github.com/code-423n4/2024-08-chakra-findings/issues/171)
*Submitted by [ABAIKUNANBAEV](https://github.com/code-423n4/2024-08-chakra-findings/issues/171), also found by [AllTooWell](https://github.com/code-423n4/2024-08-chakra-findings/issues/622), [rbserver](https://github.com/code-423n4/2024-08-chakra-findings/issues/619), [said](https://github.com/code-423n4/2024-08-chakra-findings/issues/615), [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/597), [Draiakoo](https://github.com/code-423n4/2024-08-chakra-findings/issues/288), and [0xNirix](https://github.com/code-423n4/2024-08-chakra-findings/issues/587)*

### Impact

`receive_cross_chain_msg()` is located in the Settlement contract and is called after the Chakra network signature verification process. However, when creating `ReceivedCrossChainTx` struct for the new `receive_cross_txs[txid]`, the contract mistakenly uses `address(this)` instead of `to_handler` address.

### Proof of Concept

Currently `receive_cross_txs[txId]` is assigned this way:

<https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/ChakraSettlement.sol#L205-214>

```
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

```

However, `address(this)` should be replaced by `to_handler`:

<https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/ChakraSettlement.sol#L31-40>

```
struct ReceivedCrossChainTx {
        uint256 txid;
        string from_chain;
        string to_chain;
        uint256 from_address;
        uint256 from_handler;
        address to_handler;
        bytes payload;
        CrossChainMsgStatus status;
    }

```

As you can see here, after `from_handler`, there is `to_handler` address but it's mistakenly set as `address(this)` which is an address of the settlement contract in reality.

Therefore, `receive_cross_txs[txid]` has incorrect parameters when creating a new received transaction struct.

### Recommended Mitigation Steps

Change `address(this)` on `to_handler` address in a `receive_cross_txs[txid]` mapping.

**[pidb (Chakra) confirmed](https://github.com/code-423n4/2024-08-chakra-findings/issues/171#event-14332748972)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/171#issuecomment-2434857100):**
 > The Warden has identified that the `ChakraSettlement::receive_cross_chain_msg` function will improperly store a cross-chain message and will specifically store the `to_handler` address incorrectly.
> 
> The impact of this particular submission is not able to be identified properly and, given that the function appears to be invoked as the last step in a cross-chain process, a severity of medium is considered appropriate as it should not impact the actual processing of the cross-chain transaction.


***

## [[M-06] A cross-chain message can be initiated with invalid parameters](https://github.com/code-423n4/2024-08-chakra-findings/issues/168)
*Submitted by [Tigerfrake](https://github.com/code-423n4/2024-08-chakra-findings/issues/168), also found by [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/594), [0xAsen](https://github.com/code-423n4/2024-08-chakra-findings/issues/479), [blackpanther](https://github.com/code-423n4/2024-08-chakra-findings/issues/426), [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/414), [0xb0k0](https://github.com/code-423n4/2024-08-chakra-findings/issues/382), [avoloder](https://github.com/code-423n4/2024-08-chakra-findings/issues/355), [DPS](https://github.com/code-423n4/2024-08-chakra-findings/issues/336), [agent3bood](https://github.com/code-423n4/2024-08-chakra-findings/issues/209), [ABAIKUNANBAEV](https://github.com/code-423n4/2024-08-chakra-findings/issues/499), [peanuts](https://github.com/code-423n4/2024-08-chakra-findings/issues/601), [calfun0x](https://github.com/code-423n4/2024-08-chakra-findings/issues/582), [ZdravkoHr](https://github.com/code-423n4/2024-08-chakra-findings/issues/10), [0xNirix](https://github.com/code-423n4/2024-08-chakra-findings/issues/588), and [haxatron](https://github.com/code-423n4/2024-08-chakra-findings/issues/112)*

### Impact

Anyone can initiate a cross-chain ERC20 settlement with invalid parameters, breaking an invariant due to missing validations.

For example if these values are non-existent or zero values, it would boil down to the following:

*   zero `amount` ---> Only wastes validators resources by signing the `msgHash` at destination only for `zero tokens` to be minted/unlocked to the recipient
*   zero `t0` ---> If this translates to `address(0)`, the transfer mechanism used during unlocking will revert
*   zero `to_token` ---> Recipients will expect to receive tokens at destination but if this token specified is non-existent, they wont receive any.

### Proof of Concept

One of the Main Invariants in Settlement Handler Contract is:

> Cross-chain ERC20 settlements can only be initiated with a valid amount (greater than 0), a valid recipient address, a valid handler address, and a valid token address.

This is enforced in [`ChakraSettlementHandler::cross_chain_erc20_settlement()`](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L118-L121) as follows:

```solidity
        require(amount > 0, "Amount must be greater than 0");
        require(to != 0, "Invalid to address");
        require(to_handler != 0, "Invalid to handler address");
        require(to_token != 0, "Invalid to token address");
```

However, this is not enforced in [`handler_erc20::cross_chain_erc20_settlement()`](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/cairo/handler/src/handler_erc20.cairo#L167-L232):

```solidity
        fn cross_chain_erc20_settlement(ref self: ContractState, to_chain: felt252, to_handler: u256, to_token: u256, to: u256, amount: u256) -> felt252{
            assert(self.support_handler.read((to_chain, to_handler)), 'not support handler');
            let settlement = IChakraSettlementDispatcher {contract_address: self.settlement_address.read()};
            let from_chain = settlement.chain_name();
            let token = IERC20Dispatcher{contract_address: self.token_address.read()};
            let token_burnable = IERC20MintDispatcher{contract_address: self.token_address.read()};
            if self.mode.read() == SettlementMode::MintBurn{
                token.transfer_from(get_caller_address(), get_contract_address(), amount);
            }else if self.mode.read() == SettlementMode::LockMint{
                token.transfer_from(get_caller_address(), get_contract_address(), amount);
            }else if self.mode.read() == SettlementMode::BurnUnlock{
                token_burnable.burn_from(get_caller_address(), amount);
            }else if self.mode.read() == SettlementMode::LockUnlock{
                token.transfer_from(get_caller_address(), get_contract_address(), amount);
            }
            
            ---SNIP---
        }
```

As seen, the function only checks for handler validity but performs no validations for `to_token`, `to`, and `amount`.

### Recommended Mitigation Steps

Add the following checks to the `cross_chain_erc20_settlement()` function in `handler_erc20`:

```diff
+       assert(amount > 0, 'Amount must be greater than 0');
+       assert(to != 0, 'Invalid to address');
+       assert(to_handler != 0, 'Invalid to handler address');
+       assert(to_token != 0, 'Invalid to token address');
```

**[zvlwwj (Chakra) confirmed](https://github.com/code-423n4/2024-08-chakra-findings/issues/168#event-14356497507)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/168#issuecomment-2434861678):**
 > The Warden has identified that the Cairo implementation of the cross-chain EIP-20 settlement function deviates from its specification and Solidity counterpart in the way it validates several input arguments.
> 
> I believe a medium-risk severity rating is appropriate given that no substantial impact has been demonstrated beyond a specification deviation.


***

## [[M-07] Permanent loss of user tokens on both chains if `BurnUnlock` mode fails because of flawed burning pattern](https://github.com/code-423n4/2024-08-chakra-findings/issues/140)
*Submitted by [0x18a6](https://github.com/code-423n4/2024-08-chakra-findings/issues/140), also found by [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/525), [mjcpwns](https://github.com/code-423n4/2024-08-chakra-findings/issues/437), and [jesjupyter](https://github.com/code-423n4/2024-08-chakra-findings/issues/266)*

### Impact

The `BurnUnlock` mode in the `ChakraSettlementHandler` contract has a critical flaw that causes token loss on both chains. This happens because tokens are burned on the source chain before ensuring a successful unlock on the destination chain. This high-risk vulnerability can lead to significant financial loss and damage trust in the cross-chain bridge system.

*Note that the same issue persists in the Cairo code.*

### Vulnerability Details

In the `ChakraSettlementHandler` contract, we got two modes that burns tokens in the bridging process:

*   `MintBurn`: Tokens are burned on the source chain and minted on the destination chain. This mode is used when you want to permenantly move tokens from one chain to another.

*   `BurnUnlock`: Tokens are burned on the source chain and unlocked on the destination chain. This mode is used when you want to move tokens from one chain to another and decrease the supply on the source chain.

We observe two distinct pattern of burning tokens in `MintBurn` vs `BurnUnlock` modes:

**`MintBurn` mode**

*   Source chain (`cross_chain_erc20_settlement`): Tokens are locked instead of burned initially.

[solidity/handler/contracts/ChakraSettlementHandler.sol#L123-L124](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L123-L124)

```js
if (mode == SettlementMode.MintBurn) {
  _erc20_lock(msg.sender, address(this), amount);
}
```

*   Destination chain (`receive_cross_chain_msg`): Tokens are correctly minted on the destination chain. (*the Cairo code is equivalent to this*)

[solidity/handler/contracts/ChakraSettlementHandler.sol#L325-L329](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L325-L329)

```js
if (mode == SettlementMode.MintBurn) {
  _erc20_mint(
    AddressCast.to_address(transfer_payload.to),
    transfer_payload.amount
  );
  return true;
}
```

*   Callaback on the source chain: Tokens are burned only after a successful callback. This is a security measure to ensure that user tokens are only burned when the user has received their tokens on the destination chain. If tokens were burned initially and then the call on the destination chain failed, **the user's tokens would effectively be lost on both chains**. More details on this will be provided later:

[solidity/handler/contracts/ChakraSettlementHandler.sol#L383-L389](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L383-L389)

```js
if (status == CrossChainMsgStatus.Success) {
  if (mode == SettlementMode.MintBurn) {
    _erc20_burn(address(this), create_cross_txs[txid].amount);
  }
  create_cross_txs[txid].status = CrossChainTxStatus.Settled;
}
```

**`BurnUnlock` mode**

*   Source chain (`cross_chain_erc20_settlement`): Tokens are immediately burned on the source chain.

[solidity/handler/contracts/ChakraSettlementHandler.sol#L129-L130](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L129-L130)

```js
if (mode == SettlementMode.BurnUnlock) {
  _erc20_burn(msg.sender, amount);
}
```

*   Destination chain (`receive_cross_chain_msg`): Tokens are correctly unlocked

[solidity/handler/contracts/ChakraSettlementHandler.sol#L344-L348](https://github.com/code-423n4/2024-08-chakra/blob/d0d45ae1d26ca1b87034e67180fac07ce9642fd9/solidity/handler/contracts/ChakraSettlementHandler.sol#L344-L348)

```js
if (mode == SettlementMode.BurnUnlock) {
  _erc20_unlock(
    AddressCast.to_address(transfer_payload.to),
    transfer_payload.amount
  );
  return true;
}
```

*   Callback on the source chain: No specific action for `BurnUnlock` mode in callback.

To summarize, the two distinct pattern for burning tokens is that: `MintBurn` follows a `lock (source) -> mint (dest) -> burn (callback)` and, `BurnUnlock` follows a `burn (source) -> unlock (dest)`.

The problem is that in the `BurnUnlock` mode, if the execution on the destination chain fails (for instance, due to insufficient validator signatures), the user's tokens are lost on both chains. This is because the tokens are burned on the source chain and remain locked on the destination chain, **preventing the user from reclaiming them at first try, and preventing the user from reclaiming them at a latter try because user already burned their equivalant tokens in the source chain**.

Note that the problem doesn't exist in `MintBurn` mode (at least with this particular root cause) because we use the callback pattern. If the call to destination chain fails, the callback simply unlocks the tokens back on the source chain (which it doesn't do in the current implementation, but is a subject of a distinct report since it's a different root cause i.e, not implementing a callback pattern if bridging fails *vs* not unlocking the tokens back in the callback pattern if bridging fails).

### Proof of Concept

Here's a scenario to illustrate:

*   Alice sends 1000 CHKR in `BurnUnlock` mode.
*   1000 CHKR is burned on source chain. Let's assume Alice has 1000 CHKR locked on destination chain.
*   Sending tokens fails for some reasons, e.g, due to insufficient validator signatures. We can even consider an adversarial point of view where a malicious validator intentionally not signing a valid message hash to make it not reach required threshold and fail, with the malicious intent of causing loss of user tokens on both chains. An alternative scenario of failing is when Alice doesn't have enough tokens locked on destination chain (e.g, she sends 1000 CHKR tokens but she only has 800 CHKR tokens locked on destination chain).
*   Because sending tokens failed, Alice now have 0 CHKR on source chain and 1000 CHKR still locked on the destination chain.
*   Alice tries again to send 1000 CHKR in any mode. Because CHKR was initially burned in first try and is now 0, she doesn't have the equivalent CHKR to unlock it on the destination chain and is effectively lost forever on both chains.

### Recommended Mitigation Steps

*   In my opinion, align the `BurnUnlock` mode with the `MintBurn` mode by implementing a lock-then-burn pattern:

```diff
function cross_chain_erc20_settlement(
    string memory to_chain,
    uint256 to_handler,
    uint256 to_token,
    uint256 to,
    uint256 amount
) external {
    // ...
    if (mode == SettlementMode.BurnUnlock) {
+       _erc20_lock(msg.sender, address(this), amount);
-       _erc20_burn(msg.sender, address(this), amount);
    }
    // ...
}
```

*   Implement the callback part, and don't forget to unlock tokens back to the poor Alice on failure:

```diff
function receive_cross_chain_callback(
    uint256 txid,
    string memory from_chain,
    uint256 from_handler,
    CrossChainMsgStatus status,
    uint8 /* sign_type */,
    bytes calldata /* signatures */
) external onlySettlement returns (bool) {
    // ...
    if (status == CrossChainMsgStatus.Success) {
+       if (mode == SettlementMode.BurnUnlock) {
+           _erc20_burn(address(this), create_cross_txs[txid].amount);
+       }
        create_cross_txs[txid].status = CrossChainTxStatus.Settled;
    if (status == CrossChainMsgStatus.Failed) {
+       if (mode == SettlementMode.BurnUnlock) {
+           _erc20_unlock(create_cross_txs[txid].from, create_cross_txs[txid].amount);
+       }
        create_cross_txs[txid].status = CrossChainTxStatus.Failed;
    }
    // ...
}
```

**[pidb (Chakra) disputed and commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/140#issuecomment-2363005878):**
 > Callback only works in MintBurn mode. For BurnUnLock, the token will be burned in the destination chain, so the suggestion here is wrong.

**[0xsomeone (judge) decreased severity to Medium and commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/140#issuecomment-2434989616):**
 > The Warden and its duplicates have identified that the `BurnUnlock` mode is presently insecurely implemented, burning tokens prior to receiving confirmation that they have been unlocked on the destination chain.
> 
> I do not agree with the Sponsor that the callback does not work on the `BurnUnlock` mode as **support for it should be introduced** and the node system is out-of-scope of the audit. I believe a medium-risk rating is appropriate given that this issue should solely manifest in case the cross-chain transactions fail for one reason or another.


***

## [[M-08] The `receive_cross_chain_msg` function has potential replay attack risks](https://github.com/code-423n4/2024-08-chakra-findings/issues/85)
*Submitted by [shaflow2](https://github.com/code-423n4/2024-08-chakra-findings/issues/85)*

### Impact

The `receive_cross_chain_msg` function does not check the execution status of cross-chain messages itself and relies entirely on the checks performed by the settlement contract. If the settlement contract is updated without changes to the validators, this could lead to a risk of previously executed transactions being replayed.

### Proof of Concept

The `settlement_address` contract can be updated by the owner.

```rust
        fn upgrade_settlement(ref self:ContractState, new_settlement: ContractAddress){
            self.ownable.assert_only_owner();
            self.settlement_address.write(new_settlement);
        }
```

If the `settlement_address` contract is updated without changes to the validators, the cross-chain messages that were executed in the original settlement contract will no longer exist in the new settlement contract.

This allows an attacker to replay previously executed transactions from the old settlement contract, potentially leading to financial discrepancies or chaos because the `receive_cross_chain_msg` function does not check the execution status of cross-chain messages itself.

```rust
        fn receive_cross_chain_msg(ref self: ContractState, cross_chain_msg_id: u256, from_chain: felt252, to_chain: felt252,
        from_handler: u256, to_handler: ContractAddress, payload: Array<u8>) -> bool{
            assert(to_handler == get_contract_address(),'error to_handler');

            assert(self.settlement_address.read() == get_caller_address(), 'not settlement');

            assert(self.support_handler.read((from_chain, from_handler)) && 
                    self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');

            ...
            
            return true;
        }
```

### Recommended Mitigation Steps

1.  Make the `settlement_address` unchange.

```diff
-       fn upgrade_settlement(ref self:ContractState, new_settlement: ContractAddress){
-           self.ownable.assert_only_owner();
-           self.settlement_address.write(new_settlement);
-       }
```

2.  The handler stores and verifies the state of cross-chain messages.

```diff
    #[storage]
    struct Storage {
        #[substorage(v0)]
        ownable: OwnableComponent::Storage,
        #[substorage(v0)]
        upgradeable: UpgradeableComponent::Storage,
        settlement_address: ContractAddress,
        token_address: ContractAddress,
        created_tx: LegacyMap<felt252, CreatedCrossChainTx>,
+       receive_tx: LegacyMap<felt252, CrossChainMsgStatus>,
        msg_count: u256,
        support_handler: LegacyMap<(felt252, u256), bool>,
        mode: u8
    }
```

```diff
        fn receive_cross_chain_msg(ref self: ContractState, cross_chain_msg_id: u256, from_chain: felt252, to_chain: felt252,
        from_handler: u256, to_handler: ContractAddress, payload: Array<u8>) -> bool{
            assert(to_handler == get_contract_address(),'error to_handler');

            assert(self.settlement_address.read() == get_caller_address(), 'not settlement');

            assert(self.support_handler.read((from_chain, from_handler)) && 
                    self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');
+           assert(self.receive_tx.read(cross_chain_msg_id) == CrossChainMsgStatus::UNKNOW, 'tx status error');
            ...
            
+           self.receive_tx.wirte(cross_chain_msg_id, CrossChainMsgStatus::SUCCESS);
            return true;
        }
```

**[zvlwwj (Chakra) confirmed](https://github.com/code-423n4/2024-08-chakra-findings/issues/85#event-14357103460)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/85#issuecomment-2435188963):**
 > The submission outlines a potential issue that might arise in an upgrade flow of the system if the validators are not changed. I believe such a scenario is likely, and thus consider this to be an acceptable medium-risk vulnerability as transaction replays would be possible in the edge case described.

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/85#issuecomment-2449935865):**
 > Just to clarify, the upgrade outlined in this submission is an address replacement, not an actual code upgrade. As such, storage will be affected (i.e. the settlement address will have a fresh storage set) and thus this vulnerability is applicable. Alleviating an issue in the settlement implementation will not affect the handler itself as the handler would be pointing to a new settlement implementation if the function outlined by the exhibit is invoked.


***

## [[M-09] Bridging from Starknet to Starknet causes mismatch between minted ckrBTC and BTC transferred to MuSig2](https://github.com/code-423n4/2024-08-chakra-findings/issues/46)
*Submitted by [fyamf](https://github.com/code-423n4/2024-08-chakra-findings/issues/46)*

### Impact

It is possible to bridge assets from Starknet to Starknet by setting `to_chain` and `to_handler` to be the same as `from_chain` and `from_handler`. This violates the core rule of the protocol, which is "The contract maintains a consistent state between locking/burning tokens on the source chain and minting/unlocking on the destination chain, depending on the settlement mode."

For example, this could result in the total supply of `ckrBTC` on Starknet being higher than the amount of BTC transferred to MuSig2 on the Bitcoin network.

### Proof of Concept

When a message is received on Starknet, the `handler_erc20::receive_cross_chain_msg` function is called:<br>
[Link to code](https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L108)

In this function, it checks that both `to_chain` and `to_handler` as well as `from_chain` and `from_handler` are supported:

```rust
assert(self.support_handler.read((from_chain, from_handler)) && 
       self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');
```

[Link to code](https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L115)

`to_chain` must be the Starknet chain name, and `to_handler` must be the contract address of `handler_erc20`.

This check forces the owner to already call `set_support_handler` to add support for `to_chain` and `to_handler`. Otherwise, any call to `handler_erc20::receive_cross_chain_msg` will fail:

```rust
fn set_support_handler(ref self: ContractState, chain_name: felt252, handler: u256, support: bool) {
    self.ownable.assert_only_owner();
    self.support_handler.write((chain_name, handler), support);
}
```

[Link to code](https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L238)

At first glance, this seems redundant. Why should the Starknet chain and its handler be added to the `support_handler` mapping within the same handler? For example, if the chain name is `Starknet` and the handler address is `0xaa`, calling `support_handler.read('Starknet', 0xaa)` returns `1`. This mapping should only record valid destination chains and handler addresses, not its own chain and handler.

This creates a potential attack:

1.  The attacker sends a cross-chain message from Starknet and `handler_erc20` to the same chain and handler. This means the source chain equals the destination chain, and the source handler equals the destination handler. The parameters for `handler_erc20::cross_chain_erc20_settlement` would be:
    *   `to_chain`: Starknet
    *   `to_handler`: the same address as `handler_erc20`
    *   `to_token`: the same token address (`ckrBTC`)
    *   `to`: the recipient address (irrelevant for this vulnerability)
    *   `amount`: the token amount (irrelevant for this vulnerability)
2.  During the bridging process, there is no check that `to_chain` and `to_handler` are different from `from_chain` and `from_handler`.
3.  Once the validators sign the event (the validator implementation is out of scope), the message is received on Starknet, and `settlement::receive_cross_chain_msg` is called. This function does not prevent the attack.

[Link to code](https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/settlement.cairo#L325)

4. Then, `receive_cross_chain_msg::handler_erc20` is called:<br>
[Link to code](https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/settlement.cairo#L354)

5. This function checks if `to_chain` and `to_handler` are supported, and since `to_chain = from_chain` and `to_handler = from_handler`, it passes.<br>
[Link to code](https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L114)

6. Finally, the transfer or mint occurs. If the settlement mode is `LockMint`, the same amount of `ckrBTC` that was locked on Starknet will be minted on Starknet again. In other words, because the source and destination are the same, the locked token on the source is minted again on the same source. For example, if the attacker bridges 1000 `ckrBTC` from Starknet to Starknet, 1000 `ckrBTC` is locked on Starknet, and then 1000 `ckrBTC` is minted again, resulting in a total supply increase of 2000 `ckrBTC` on Starknet (1000 locked and 1000 minted).

This contradicts the core logic of the protocol, as explained:

> "In Chakra liquid staking, users first transfer Bitcoin to a multi-signature address supported by MuSig2. This event is captured by the indexer, which calls the on-chain contract to mint ckrBTC for the user. The Bitcoin in the multi-signature address is staked into Babylon. While holding ckrBTC, users continue to earn rewards from Babylon staking. When users want to end the staking, they can burn ckrBTC."

[Link to source](https://blog.bitlayer.org/BIP-327\_MuSig2\_in_Four_Applications/)

**This means that the amount of `ckrBTC` on Starknet is supposed to match the amount of BTC transferred to MuSig2. However, due to this attack, the amount of `ckrBTC` on Starknet can be maliciously increased and will not match the amount of BTC transferred to MuSig2.**

### Summary

Under normal conditions, a user locks `ckrBTC` on Starknet and receives tokens on another chain, enabling them to use Bitcoin-backed assets in DeFi protocols. But in this attack, the attacker locks `ckrBTC` on Starknet and bridges it to Starknet again to mint `ckrBTC` again. This causes the total supply of `ckrBTC` on Starknet to be higher than the amount of BTC in MuSig2, violating the core rule of the protocol.

### Note

This vulnerability does not depend on owner mistakes. The owner must have already added the source chain and handler to the `support_handler` mapping; otherwise, any call to `handler_erc20::receive_cross_chain_msg` would fail. On the EVM-based code, however, the owner does not need to add the source chain and handler to the `handler_whitelist` mapping, since `ChakraSettlementHandler::receive_cross_chain_msg` only checks that `from_chain` and `from_handler` are whitelisted, not `to_chain` and `to_handler`.

```solidity
if (is_valid_handler(from_chain, from_handler) == false) {
    return false;
}
```

[Link to code](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L311)

### Proof of Concept (PoC)

In the following test, `target_chain`, `target_token`, and `target_handler` are all set to `Starknet`, `ckrBTC`, and `erc20_handler` on Starknet, respectively. This shows that the transaction executes successfully, contrary to expectations.

<details>

```javascript
use core::option::OptionTrait;
use core::traits::TryInto;
use settlement_cairo::ckr_btc::IckrBTCDispatcherTrait;
use openzeppelin::token::erc20::interface::IERC20DispatcherTrait;
use core::result::ResultTrait;
use core::box::BoxTrait;
use snforge_std::{declare, ContractClassTrait, start_prank, CheatTarget, stop_prank};
use starknet::ContractAddress;
use starknet::{get_tx_info, get_caller_address};
use settlement_cairo::interfaces::{IERC20HandlerDispatcher, IERC20HandlerDispatcherTrait, IChakraSettlementDispatcher, IChakraSettlementDispatcherTrait};
use settlement_cairo::codec::{decode_transfer, encode_transfer, ERC20Transfer, Message, decode_message, encode_message};
use settlement_cairo::utils::{u256_to_contract_address, contract_address_to_u256, u256_to_u8_array};
use settlement_cairo::ckr_btc::{IckrBTCDispatcher};
use openzeppelin::token::erc20::interface::IERC20Dispatcher;


#[test]
fn test_lock_mint_self(){
    let source_chain = 'Starknet';
    let target_address = 1;
    let amount = 1000;
    let owner_address = 0x5a9bd6214db5b229bd17a4050585b21c87fc0cadf9871f89a099d27ef800a40;
    let attacker_address = 0x00112233445566778899aabbccddeeff;
    let attacker = attacker_address.try_into().unwrap();


    let settlement_contract = declare("ChakraSettlement");
    let settlement_address = settlement_contract.deploy(@array![owner_address, 1]).unwrap();
    let ckrBTC_contract = declare("ckrBTC");
    let ckrBTC_address = ckrBTC_contract.deploy(@array![owner_address]).unwrap();
    let erc20_handler = declare("ERC20Handler");
    let erc20_handler_address = erc20_handler.deploy(@array![settlement_address.into(),owner_address,ckrBTC_address.into(), 1]).unwrap();
    

    let handler_dispath = IERC20HandlerDispatcher {contract_address: erc20_handler_address};
    let ckrbtc_dispath = IckrBTCDispatcher{contract_address: ckrBTC_address};
    let ckrbtc_erc20_dispath = IERC20Dispatcher{contract_address: ckrBTC_address};
    // support handler
    let owner = owner_address.try_into().unwrap();
    start_prank(CheatTarget::One(erc20_handler_address), owner);
    // add from_chain from_handler
    handler_dispath.set_support_handler(source_chain, contract_address_to_u256(erc20_handler_address),true);

    start_prank(CheatTarget::One(ckrBTC_address), owner);
    ckrbtc_dispath.add_operator(erc20_handler_address);
    ckrbtc_dispath.add_operator(owner);
    // cross_chain_erc20_settlement
    ckrbtc_dispath.mint_to(attacker, amount);
    stop_prank(CheatTarget::One(ckrBTC_address));


    ////////////// attack starts here
    start_prank(CheatTarget::One(ckrBTC_address), attacker);
    ckrbtc_erc20_dispath.approve(erc20_handler_address, amount);
    stop_prank(CheatTarget::One(ckrBTC_address));
    
    start_prank(CheatTarget::One(erc20_handler_address), attacker);
    let target_chain = 'Starknet'; // attacker sets the target chain as source chain
    let target_token = contract_address_to_u256(ckrBTC_address); // attacker sets the target token as source token
    let target_handler = contract_address_to_u256(erc20_handler_address); // attacker sets the target handler as source handler
    handler_dispath.cross_chain_erc20_settlement(target_chain, target_handler, target_token, target_address, amount);
    stop_prank(CheatTarget::One(erc20_handler_address));

    assert(ckrbtc_erc20_dispath.balance_of(attacker) == 0, 'balance error after cross');
    assert(ckrbtc_erc20_dispath.balance_of(erc20_handler_address) == amount, 'handler balance error');

    // receive_cross_chain_msg
    start_prank(CheatTarget::One(erc20_handler_address), settlement_address);

    assert(ckrbtc_erc20_dispath.balance_of(u256_to_contract_address(0x70997970c51812dc3a010c7d01b50e0d17dc79c8)) == 0, 'to_address balance error');
    let message_array_u8 = array! [1, 226, 26, 80, 2, 232, 11, 172, 207, 254, 0, 95, 72, 69, 136, 99, 38, 6, 228, 108, 177, 62, 5, 10, 125, 58, 52, 32, 110, 139, 85, 224, 141, 5, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 243, 159, 214, 229, 26, 173, 136, 246, 244, 206, 106, 184, 130, 114, 121, 207, 255, 185, 34, 102, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 112, 153, 121, 112, 197, 24, 18, 220, 58, 1, 12, 125, 1, 181, 14, 13, 23, 220, 121, 200, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 231, 241, 114, 94, 119, 52, 206, 40, 143, 131, 103, 225, 187, 20, 62, 144, 187, 63, 5, 18, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 144, 247, 155, 246, 235, 44, 79, 135, 3, 101, 231, 133, 152, 46, 31, 16, 30, 147, 185, 6, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 3, 232];
    handler_dispath.receive_cross_chain_msg(1, target_chain, source_chain, target_handler, erc20_handler_address, message_array_u8);
    assert(ckrbtc_erc20_dispath.balance_of(u256_to_contract_address(0x70997970c51812dc3a010c7d01b50e0d17dc79c8)) == 1000, 'transfer error');
}
```

</details>

### Recommended Mitigation Steps

When bridging from Starknet, it should ensure that the source and destination are different.

**[0xsomeone (judge) decreased severity to Medium and commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/46#issuecomment-2434870496):**
 > The Warden has identified a self-cross-chain-transfer exploitation path that will cause the `ckrBTC` token to have an incorrect total supply.
> 
> I believe a medium-risk severity level is better suited as no financial value can be exploited via the vulnerability described. I do commend the ingenuity!


***

## [[M-10] Does not check if `to_chain` and `to_handler` is whitelisted in `cross_chain_erc20_settlement`](https://github.com/code-423n4/2024-08-chakra-findings/issues/44)
*Submitted by [klau5](https://github.com/code-423n4/2024-08-chakra-findings/issues/44), also found by [Moksha](https://github.com/code-423n4/2024-08-chakra-findings/issues/625), [fyamf](https://github.com/code-423n4/2024-08-chakra-findings/issues/606), [NexusAudits](https://github.com/code-423n4/2024-08-chakra-findings/issues/600), [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/526), [gajiknownnothing](https://github.com/code-423n4/2024-08-chakra-findings/issues/523), [Tigerfrake](https://github.com/code-423n4/2024-08-chakra-findings/issues/505), [ABAIKUNANBAEV](https://github.com/code-423n4/2024-08-chakra-findings/issues/501), [0xAsen](https://github.com/code-423n4/2024-08-chakra-findings/issues/480), [pwnforce](https://github.com/code-423n4/2024-08-chakra-findings/issues/441), [Daniel\_eth](https://github.com/code-423n4/2024-08-chakra-findings/issues/435), [atoko](https://github.com/code-423n4/2024-08-chakra-findings/issues/421), [avoloder](https://github.com/code-423n4/2024-08-chakra-findings/issues/387), [AllTooWell](https://github.com/code-423n4/2024-08-chakra-findings/issues/381), [0xNirix](https://github.com/code-423n4/2024-08-chakra-findings/issues/329), [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/304), [Draiakoo](https://github.com/code-423n4/2024-08-chakra-findings/issues/287), [peanuts](https://github.com/code-423n4/2024-08-chakra-findings/issues/210), [rbserver](https://github.com/code-423n4/2024-08-chakra-findings/issues/121), [haxatron](https://github.com/code-423n4/2024-08-chakra-findings/issues/100), [said](https://github.com/code-423n4/2024-08-chakra-findings/issues/76), [mojito\_auditor](https://github.com/code-423n4/2024-08-chakra-findings/issues/67), [shaflow2](https://github.com/code-423n4/2024-08-chakra-findings/issues/610), [bhilare\_](https://github.com/code-423n4/2024-08-chakra-findings/issues/318), [kutugu](https://github.com/code-423n4/2024-08-chakra-findings/issues/280), [devival](https://github.com/code-423n4/2024-08-chakra-findings/issues/627), [Shaheen](https://github.com/code-423n4/2024-08-chakra-findings/issues/613), and [Breeje](https://github.com/code-423n4/2024-08-chakra-findings/issues/602)*

### Impact

The handler does not prevent tokens from being sent to incorrect chains and handlers. If a message is sent to an incorrect handler, the failure cannot be handled through `receive_cross_chain_callback`.

### Proof of Concept

`Handler.cross_chain_erc20_settlement` does not check if `to_chain` and `to_handler` are whitelisted. Therefore, it's possible to send messages to any chains and handlers that aren’t paired with this handler.

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
@>  require(to_handler != 0, "Invalid to handler address");
    require(to_token != 0, "Invalid to token address");

    if (mode == SettlementMode.MintBurn) {
        _erc20_lock(msg.sender, address(this), amount);
    } else if (mode == SettlementMode.LockUnlock) {
        _erc20_lock(msg.sender, address(this), amount);
    } else if (mode == SettlementMode.LockMint) {
        _erc20_lock(msg.sender, address(this), amount);
    } else if (mode == SettlementMode.BurnUnlock) {
        _erc20_burn(msg.sender, amount);
    }
    ...
}
```

If a non-contract address is set as `to_handler`, the transaction will revert when trying to call `Handler.receive_cross_chain_msg` on the destination chain. As a result, it's impossible to emit an event to signal the failure, making failure handling impossible.

```solidity
// Settlement.receive_cross_chain_msg
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

@>  bool result = ISettlementHandler(to_handler).receive_cross_chain_msg( // this will be reverted
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
    } else {
@>      receive_cross_txs[txid].status = CrossChainMsgStatus.Failed;
    }

    emit CrossChainHandleResult(
        txid,
@>      status,
        contract_chain_name,
        from_chain,
        address(to_handler),
        from_handler,
        payload_type
    );
}
```

There's another problem. If a non-whitelisted handler requests a message, `Handler.receive_cross_chain_msg` will return `false` to indicate failure. Validators listen for the `CrossChainHandleResult` event to notify the source chain of the failure through `receive_cross_chain_callback`, allowing the handler to process the failure.

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
@>  if (is_valid_handler(from_chain, from_handler) == false) {
@>      return false;
    }
    ...
}
```

However, `Handler.receive_cross_chain_callback` only allows callback messages from whitelisted chains and handlers. This means that when a message is sent to an incorrect handler and fails, the callback notifies of the failure, but the source chain's handler ignores and cannot handle the failure caused by the incorrect handler.

```solidity
function receive_cross_chain_callback(
    uint256 txid,
    string memory from_chain,
    uint256 from_handler,
    CrossChainMsgStatus status,
    uint8 /* sign_type */, // validators signature type /  multisig or bls sr25519
    bytes calldata /* signatures */
) external onlySettlement returns (bool) {
    //  from_handler need in whitelist
@>  if (is_valid_handler(from_chain, from_handler) == false) {
@>      return false;
    }

    require(
        create_cross_txs[txid].status == CrossChainTxStatus.Pending,
        "invalid CrossChainTxStatus"
    );

    if (status == CrossChainMsgStatus.Success) {
        if (mode == SettlementMode.MintBurn) {
            _erc20_burn(address(this), create_cross_txs[txid].amount);
        }

        create_cross_txs[txid].status = CrossChainTxStatus.Settled;
    }

    if (status == CrossChainMsgStatus.Failed) {
        create_cross_txs[txid].status = CrossChainTxStatus.Failed;
    }

    return true;
}
```

Therefore, `Handler.cross_chain_erc20_settlement` should check that `to_chain` and `to_handler` are whitelisted to prevent message transmission to incorrect handlers in the first place.

### Recommended Mitigation Steps

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
+   require(is_valid_handler(to_chain, to_handler), "not valid destination");

    if (mode == SettlementMode.MintBurn) {
        _erc20_lock(msg.sender, address(this), amount);
    } else if (mode == SettlementMode.LockUnlock) {
        _erc20_lock(msg.sender, address(this), amount);
    } else if (mode == SettlementMode.LockMint) {
        _erc20_lock(msg.sender, address(this), amount);
    } else if (mode == SettlementMode.BurnUnlock) {
        _erc20_burn(msg.sender, amount);
    }
    ...
}
```

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/44#issuecomment-2435263962):**
 > The submission and its duplicates detail how a cross-chain message does not validate that the `to_handler` is a valid address on the `to_chain`, causing transactions to be permanently stuck in a pending state and thus leading to fund loss.
> 
> I believe a medium-severity rating is appropriate given that the user would have to make a mistake when submitting their transaction, however, the documentation of the system and Cairo implementation indicate that validation should occur.


***

## [[M-11] Wrong usage of transaction originator address instead of caller address](https://github.com/code-423n4/2024-08-chakra-findings/issues/41)
*Submitted by [fyamf](https://github.com/code-423n4/2024-08-chakra-findings/issues/41), also found by [AllTooWell](https://github.com/code-423n4/2024-08-chakra-findings/issues/624), [haxatron](https://github.com/code-423n4/2024-08-chakra-findings/issues/612), [ABAIKUNANBAEV](https://github.com/code-423n4/2024-08-chakra-findings/issues/581), [0xb0k0](https://github.com/code-423n4/2024-08-chakra-findings/issues/366), calc1f4r ([1](https://github.com/code-423n4/2024-08-chakra-findings/issues/302), [2](https://github.com/code-423n4/2024-08-chakra-findings/issues/295)), and [Draiakoo](https://github.com/code-423n4/2024-08-chakra-findings/issues/284)*

### Impact

The `from_address` parameter in the events emitted when sending a cross-chain message from Starknet is set to the transaction origin (`tx.origin`) instead of the actual caller (`msg.sender`). This causes incorrect data to be emitted in the event.

### Proof of Concept

When a cross-chain message is sent from Starknet using the function `handler_erc20::cross_chain_erc20_settlement`, the function `settlement::send_cross_chain_msg` is called:

*   See `handler_erc20::cross_chain_erc20_settlement`:
    <https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L216>
*   See `settlement::send_cross_chain_msg`:
    <https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/settlement.cairo#L284>

Within this function, the `CrossChainMsg` event is emitted for validators to pick up:

```rust
            self
                .emit(
                    CrossChainMsg {
                        cross_chain_settlement_id: cross_chain_settlement_id,
                        from_address: get_tx_info().unbox().account_contract_address,
                        from_chain: from_chain,
                        to_chain: to_chain,
                        from_handler: from_handler,
                        to_handler: to_handler,
                        payload_type: payload_type,
                        payload: payload
                    }
                );
```

<https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/settlement.cairo#L299>

The issue is that `from_address` is set to `get_tx_info().unbox().account_contract_address`, which represents "The account contract from which this transaction originates." This is equivalent to `tx.origin` in EVM-based blockchains: <https://github.com/starkware-libs/cairo/blob/main/corelib/src/starknet/info.cairo#L46>

This is incorrect because the address of the original transaction sender is irrelevant. Instead, `from_address` should represent the caller of the `handler_erc20::cross_chain_erc20_settlement` function.

In contrast, the EVM-based code correctly sets `from_address` to the parameter forwarded by the `ChakraSettlementHandler::cross_chain_erc20_settlement` function, which is equivalent to `msg.sender`:

```solidity
            // Send the cross-chain message
            settlement.send_cross_chain_msg(
                to_chain,
                msg.sender,
                to_handler,
                PayloadType.ERC20,
                cross_chain_msg_bytes
            );
```

<https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L205>

```solidity
    function send_cross_chain_msg(
        string memory to_chain,
        address from_address,
        uint256 to_handler,
        PayloadType payload_type,
        bytes calldata payload
    ) external {
        //.....
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

<https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/ChakraSettlement.sol#L113>

By using the transaction originator’s address (`tx.origin`) as `from_address`, the event may include an address that is irrelevant to the cross-chain transaction. This can result in misleading information for any third parties reading the events. Here are two scenarios where an incorrect `from_address` might be used:

Here is the simplified rephrased version of the report:

*   **First Scenario:** Imagine Alice sends an NFT to Bob's contract using the `safe_transfer` function. This function makes an external call to Bob's contract. During this call, if Bob's contract calls `handler_erc20::cross_chain_erc20_settlement` to send a cross-chain message from Starknet to another chain, the `CrossChainMsg` event will show Alice's address as `from_address` because Alice was the original sender of the transaction. This is incorrect because it is actually Bob's contract sending the cross-chain message, so `from_address` should be Bob's contract address, not Alice's.

<https://github.com/OpenZeppelin/cairo-contracts/blob/main/packages/token/src/erc721/erc721.cairo#L571>

```rust
   // This is Bob's contract
   // When Alice transfers NFT to Bob's contract, this function is called.
       fn on_erc721_received(
           self: @ComponentState<TContractState>,
           operator: ContractAddress,
           from: ContractAddress,
           token_id: u256,
           data: Span<felt252>
       ) -> felt252 {
           // Calling `handler_erc20::cross_chain_erc20_settlement`
           //.....
       }
```

*   **Second Scenario:** Consider a scenario where a message is bridged from Ethereum (L1) to Starknet (L2) with Starknet validators managing the bridging process. When the message arrives on Starknet, the function marked with `#[l1_handler]` in the target contract is called by StarknetOS. **In this situation, calling `get_caller_address()` in that function returns zero.** If this function then calls `handler_erc20::cross_chain_erc20_settlement`, the `CrossChainMsg` event will show `from_address` as zero, since the original sender was StarknetOS. This is incorrect because `from_address` should be the target contract's address, not zero.

<https://book.cairo-lang.org/ch16-04-L1-L2-messaging.html?highlight=%23%5Bl1_handler%5D#sending-messages-from-ethereum-to-starknet>

<https://docs.cairo-lang.org/hello_starknet/user_auth.html#getting-the-caller-address>

<https://cairopractice.com/posts/get_caller_address_zero/>

```rust
    // This is the target contract
    // This function is called by StarknetOS
    #[l1_handler]
    fn msg_handler_felt(ref self: ContractState, from_address: felt252, my_felt: felt252) {
        // Calling get_caller_address() here returns zero
        // Calling `handler_erc20::cross_chain_erc20_settlement`
        //.....
    }
```

Additionally, when a callback message is received, the `CrossChainResult` event will show `from_address` as `get_tx_info().unbox().account_contract_address`, which is also incorrect and misleading.

### Recommended Mitigation Steps

Following modifications are recommended:

<details>

```diff
        fn cross_chain_erc20_settlement(ref self: ContractState, to_chain: felt252, to_handler: u256, to_token: u256, to: u256, amount: u256) -> felt252{
            assert(self.support_handler.read((to_chain, to_handler)), 'not support handler');
            let settlement = IChakraSettlementDispatcher {contract_address: self.settlement_address.read()};
            let from_chain = settlement.chain_name();
            let token = IERC20Dispatcher{contract_address: self.token_address.read()};
            let token_burnable = IERC20MintDispatcher{contract_address: self.token_address.read()};
            if self.mode.read() == SettlementMode::MintBurn{
                token.transfer_from(get_caller_address(), get_contract_address(), amount);
            }else if self.mode.read() == SettlementMode::LockMint{
                token.transfer_from(get_caller_address(), get_contract_address(), amount);
            }else if self.mode.read() == SettlementMode::BurnUnlock{
                token_burnable.burn_from(get_caller_address(), amount);
            }else if self.mode.read() == SettlementMode::LockUnlock{
                token.transfer_from(get_caller_address(), get_contract_address(), amount);
            }
            
            let tx_id = LegacyHash::hash(get_tx_info().unbox().transaction_hash, self.msg_count.read());
            let tx: CreatedCrossChainTx = CreatedCrossChainTx{
                    tx_id: tx_id,
                    from_chain: from_chain,
                    to_chain: to_chain,
                    from: get_contract_address(),
                    to: to,
                    from_token: self.token_address.read(),
                    to_token: to_token,
                    amount: amount,
                    tx_status: CrossChainTxStatus::PENDING
                };
            self.created_tx.write(tx_id, tx);
            self.msg_count.write(self.msg_count.read()+1);
            // message id = message count
            let message_id = tx_id;
            let transfer = ERC20Transfer{
                method_id: 1,
                from: contract_address_to_u256(get_caller_address()),
                to: to,
                from_token: contract_address_to_u256(self.token_address.read()),
                to_token: to_token,
                amount: amount
            };

            let message = Message{
                version: 1,
                message_id: message_id.into(),
                payload_type: PayloadType::ERC20,
                payload: encode_transfer(transfer),
            };
            
            // send cross chain msg
-           settlement.send_cross_chain_msg(to_chain, to_handler, PayloadType::ERC20, encode_message(message));
+           settlement.send_cross_chain_msg(to_chain, to_handler, PayloadType::ERC20, encode_message(message), 
+           get_caller_address());
            // emit CrossChainLocked

            self.emit(
                    CrossChainLocked{
                        tx_id: tx_id,
                        from: get_caller_address(),
                        to: to,
                        from_chain: get_tx_info().unbox().chain_id,
                        to_chain: to_chain,
                        from_token: self.token_address.read(),
                        to_token: to_token,
                        amount: amount
                    }
                );
            return tx_id;
        }
```

```diff
        fn send_cross_chain_msg(
            ref self: ContractState, to_chain: felt252, to_handler: u256, payload_type :u8,payload: Array<u8>,
+           from_address: felt252,
        ) -> felt252 {
            let from_handler = get_caller_address();
            let from_chain = self.chain_name.read();
            let cross_chain_settlement_id = LegacyHash::hash(get_tx_info().unbox().transaction_hash, self.tx_count.read());
            self.created_tx.write(cross_chain_settlement_id, CreatedTx{
                tx_id:cross_chain_settlement_id,
                tx_status: CrossChainMsgStatus::PENDING,
                from_chain: from_chain,
                to_chain: to_chain,
                from_handler: from_handler,
                to_handler: to_handler
            });
            
            self
                .emit(
                    CrossChainMsg {
                        cross_chain_settlement_id: cross_chain_settlement_id,
-                       from_address: get_tx_info().unbox().account_contract_address,
+                       from_address: from_address,
                        from_chain: from_chain,
                        to_chain: to_chain,
                        from_handler: from_handler,
                        to_handler: to_handler,
                        payload_type: payload_type,
                        payload: payload
                    }
                );
            self.tx_count.write(self.tx_count.read()+1);
            return cross_chain_settlement_id;
        }
```

<https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/settlement.cairo#L284>

</details>

**[zvlwwj (Chakra) confirmed](https://github.com/code-423n4/2024-08-chakra-findings/issues/41#event-14357164530)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/41#issuecomment-2435271348):**
 > The Warden has outlined how the system will utilize the `tx.origin` when processing cross-chain transaction creations which is incorrect. I believe that this does not result in a material vulnerability and is instead an incorrect system implementation meriting a medium-severity rating.


***

## [[M-12] SettlementSignatureVerifier's `required_validators` is not updated, resulting in a low or high number of signatures being required](https://github.com/code-423n4/2024-08-chakra-findings/issues/8)
*Submitted by [klau5](https://github.com/code-423n4/2024-08-chakra-findings/issues/8), also found by [0x37](https://github.com/code-423n4/2024-08-chakra-findings/issues/444), [Topmark](https://github.com/code-423n4/2024-08-chakra-findings/issues/430), [Draiakoo](https://github.com/code-423n4/2024-08-chakra-findings/issues/264), [jesjupyter](https://github.com/code-423n4/2024-08-chakra-findings/issues/224), [rbserver](https://github.com/code-423n4/2024-08-chakra-findings/issues/122), [gesha17](https://github.com/code-423n4/2024-08-chakra-findings/issues/26), [Breeje](https://github.com/code-423n4/2024-08-chakra-findings/issues/603), [SBSecurity](https://github.com/code-423n4/2024-08-chakra-findings/issues/591), and [0xNirix](https://github.com/code-423n4/2024-08-chakra-findings/issues/586)*

### Impact

The `required_validators` in `SettlementSignatureVerifier` is not updated when updating `BaseSettlement`'s. This results in either fewer or more signatures being required when verified.

### Proof of Concept

The functions `BaseSettlement.add_validator` and `BaseSettlement.remove_validator` in the BaseSettlement contract also update the validators of the SignatureVerifier contract. However, the function `BaseSettlement.set_required_validators_num` does not call `SettlementSignatureVerifier.set_required_validators_num`. Therefore, the number of required validator signatures will not be set.

```solidity
function set_required_validators_num(
    uint256 _required_validators
) external onlyRole(MANAGER_ROLE) {
    uint256 old = required_validators;
    required_validators = _required_validators;
    emit RequiredValidatorsChanged(msg.sender, old, required_validators);
}
```

This is the PoC. You can add it to `solidity/settlement/test/ChakraSettlement.ts` and run it.

```jsx
it('PoC set_required_validators_num', async () => {
    const { settlmentInstance, verifierInstance, manager } = await loadFixture(deploySettlementFixture)
    await settlmentInstance.connect(manager).set_required_validators_num(3);

    expect(await settlmentInstance.required_validators()).to.equal(3);
    expect(await verifierInstance.required_validators()).to.equal(2); // does not changed
});
```

### Recommended Mitigation Steps

Call `SettlementSignatureVerifier.set_required_validators_num` at `BaseSettlement.set_required_validators_num` .

```diff
function set_required_validators_num(
    uint256 _required_validators
) external onlyRole(MANAGER_ROLE) {
+   signature_verifier.set_required_validators_num(_required_validators);
    uint256 old = required_validators;
    required_validators = _required_validators;
    emit RequiredValidatorsChanged(msg.sender, old, required_validators);
}
```

**[pidb (Chakra) disputed](https://github.com/code-423n4/2024-08-chakra-findings/issues/8#event-14333111521)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-08-chakra-findings/issues/8#issuecomment-2435312947):**
 > The Warden and its duplicates have outlined how the `BaseSettlement::set_required_validators_num` function fails to take effect as expected, causing it to be ineffectual in relation to the actual signature validation performed within the `SettlementSignatureVerifier` contract.
> 
> I believe a medium-risk rating is appropriate given that functionality of the system is missing but no exploitable attack path has been defined.


***

# Low Risk and Non-Critical Issues

For this audit, 46 reports were submitted by wardens detailing low risk and non-critical issues. The [report highlighted below](https://github.com/code-423n4/2024-08-chakra-findings/issues/553) by **SBSecurity** received the top score from the judge.

*The following wardens also submitted reports: [AllTooWell](https://github.com/code-423n4/2024-08-chakra-findings/issues/558), [fyamf](https://github.com/code-423n4/2024-08-chakra-findings/issues/55), [ABAIKUNANBAEV](https://github.com/code-423n4/2024-08-chakra-findings/issues/569), [atoko](https://github.com/code-423n4/2024-08-chakra-findings/issues/563), [Abdessamed](https://github.com/code-423n4/2024-08-chakra-findings/issues/550), [NexusAudits](https://github.com/code-423n4/2024-08-chakra-findings/issues/543), [peanuts](https://github.com/code-423n4/2024-08-chakra-findings/issues/540), [rbserver](https://github.com/code-423n4/2024-08-chakra-findings/issues/130), [calfun0x](https://github.com/code-423n4/2024-08-chakra-findings/issues/572), [Rhaydden](https://github.com/code-423n4/2024-08-chakra-findings/issues/566), [PolarizedLight](https://github.com/code-423n4/2024-08-chakra-findings/issues/560), [0xNirix](https://github.com/code-423n4/2024-08-chakra-findings/issues/556), [jasonxiale](https://github.com/code-423n4/2024-08-chakra-findings/issues/555), [sivanesh\_808](https://github.com/code-423n4/2024-08-chakra-findings/issues/546), [devival](https://github.com/code-423n4/2024-08-chakra-findings/issues/544), [Bauchibred](https://github.com/code-423n4/2024-08-chakra-findings/issues/542), [Sparrow](https://github.com/code-423n4/2024-08-chakra-findings/issues/541), [Breeje](https://github.com/code-423n4/2024-08-chakra-findings/issues/539), [Sabit](https://github.com/code-423n4/2024-08-chakra-findings/issues/466), [Tigerfrake](https://github.com/code-423n4/2024-08-chakra-findings/issues/408), [BY\_DLIFE](https://github.com/code-423n4/2024-08-chakra-findings/issues/406), [Nexarion](https://github.com/code-423n4/2024-08-chakra-findings/issues/385), [King\_](https://github.com/code-423n4/2024-08-chakra-findings/issues/368), [DPS](https://github.com/code-423n4/2024-08-chakra-findings/issues/338), [VulnViper](https://github.com/code-423n4/2024-08-chakra-findings/issues/337), [Draiakoo](https://github.com/code-423n4/2024-08-chakra-findings/issues/293), [Audinarey](https://github.com/code-423n4/2024-08-chakra-findings/issues/275), [Flare](https://github.com/code-423n4/2024-08-chakra-findings/issues/271), [jesjupyter](https://github.com/code-423n4/2024-08-chakra-findings/issues/257), [Omik](https://github.com/code-423n4/2024-08-chakra-findings/issues/236), [Sisi](https://github.com/code-423n4/2024-08-chakra-findings/issues/234), [Taiger](https://github.com/code-423n4/2024-08-chakra-findings/issues/232), [MrPotatoMagic](https://github.com/code-423n4/2024-08-chakra-findings/issues/208), [minato7namikazi](https://github.com/code-423n4/2024-08-chakra-findings/issues/179), [mrjorystewartbaxter](https://github.com/code-423n4/2024-08-chakra-findings/issues/163), [Trooper](https://github.com/code-423n4/2024-08-chakra-findings/issues/159), [m4k2](https://github.com/code-423n4/2024-08-chakra-findings/issues/154), [LuarSec](https://github.com/code-423n4/2024-08-chakra-findings/issues/129), [klau5](https://github.com/code-423n4/2024-08-chakra-findings/issues/127), [said](https://github.com/code-423n4/2024-08-chakra-findings/issues/114), [Shaheen](https://github.com/code-423n4/2024-08-chakra-findings/issues/106), [haxatron](https://github.com/code-423n4/2024-08-chakra-findings/issues/96), [shaflow2](https://github.com/code-423n4/2024-08-chakra-findings/issues/92), [mojito\_auditor](https://github.com/code-423n4/2024-08-chakra-findings/issues/69), and [4rdiii](https://github.com/code-423n4/2024-08-chakra-findings/issues/12).*

## [01] Config on `Starknet` allows calling for `to_chain` and `to_handler` at the same chain

### Issue Description

Looking at the assert statement in `handler_erc20::receive_cross_chain_callback` we can see that `to_handler` and `to_chain` are also validated to be in the `support_handler` collection:

[handler_erc20.cairo](https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L144-L145)

```rust

  assert(self.support_handler.read((from_chain, from_handler)) && 
  self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');
```

In reality these 2 should be the same address and same chain on which the execution is happening. Knowing that users can create cross chain transactions for the same chain and spam validators with transactions:

[handler_erc20.cairo](https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L168)

```rust
fn cross_chain_erc20_settlement(ref self: ContractState, to_chain: felt252, to_handler: u256, to_token: u256, to: u256, amount: u256) -> felt252{
          assert(self.support_handler.read((to_chain, to_handler)), 'not support handler');
```

The assert in `cross_chain_erc20_settlement` is intended to validate whether the destination is supported but because of the check above the admin is forced to add the address and chain of the contract that is calling the `cross_chain_erc20_settlement` function.

### Recommendation

Simplify the assert in `receive_cross_chain_callback` and `receive_cross_chain_callback` by removing `to_chain` and `to_handler`.

```diff

-  assert(self.support_handler.read((from_chain, from_handler)) && self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');
+  assert(self.support_handler.read((from_chain, from_handler))), 'not support handler');

```

## [02] `receive_cross_chain_msg` has no access control, users can grief validators with frontrun

### Issue Description

`receive_cross_chain_msg` in both `ChakraSettlement` (Solidity) and `settlement` (Cairo) are missing access control and allow anyone, observing the mempool, to steal the signatures and frontrun the messages gas griefing the trusted entities that should call this function:

[ChakraSettlement.sol](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/ChakraSettlement.sol#L170C5-L197C15)

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
```

[settlement.cairo](https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/settlement.cairo#L325-L350)

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
```

As we can see nowhere caller validation is done, only signatures are checked whether they belong to the current validators.

The grief is basically as ERC20 permit frontrunning, explained [here](https://www.trust-security.xyz/post/permission-denied). Although no harm is done, it affects the honest actors.

### Recommendation

Add access-control allowing only Chakra trusted entities to call these functions.

## [03] Missing check if the `txid` exists in `created_tx`

### Issue Description

`receive_cross_chain_callback` in Cairo and the one in Solidity aren’t the same logic, since the one in Cairo is missing a crucial check ensuring `txId` is created.

[ChakraSettlementHandler.sol#L365-L396](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L365-L396)

```solidity
function receive_cross_chain_callback(
    uint256 txid,
    string memory from_chain,
    uint256 from_handler,
    CrossChainMsgStatus status,
    uint8 /* sign_type */, // validators signature type /  multisig or bls sr25519
    bytes calldata /* signatures */
) external onlySettlement returns (bool) {
    //  from_handler need in whitelist
    if (is_valid_handler(from_chain, from_handler) == false) {
        return false;
    }

    require(
        create_cross_txs[txid].status == CrossChainTxStatus.Pending,  <--------------------------------
        "invalid CrossChainTxStatus"
    );

    if (status == CrossChainMsgStatus.Success) {
        if (mode == SettlementMode.MintBurn) {
            _erc20_burn(address(this), create_cross_txs[txid].amount);
        }

        create_cross_txs[txid].status = CrossChainTxStatus.Settled;
    }

    if (status == CrossChainMsgStatus.Failed) {
        create_cross_txs[txid].status = CrossChainTxStatus.Failed;
    }

    return true;
}
```

[handler_erc20.cairo#L138-L167](https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L138-L167)

```rust
fn receive_cross_chain_callback(ref self: ContractState, cross_chain_msg_id: felt252, from_chain: felt252, to_chain: felt252,
from_handler: u256, to_handler: ContractAddress, cross_chain_msg_status: u8) -> bool{
    assert(to_handler == get_contract_address(),'error to_handler');

    assert(self.settlement_address.read() == get_caller_address(), 'not settlement');

    assert(self.support_handler.read((from_chain, from_handler)) && 
            self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');

    // AUDIT - missing created_tx check
    assert(self.created_tx.read(cross_chain_msg_id).tx_status == CrossChainTxStatus::PENDING, 'tx status error');

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

This missing check will make the problem mentioned in one of our reports [”`send_cross_chain_msg` in Settlement must have `onlyHandler` modifier”] a little different for Cairo, the problem will just not revert when `receive_cross_chain_callback` is called, but will take 0s for each `created_tx` field and will burn 0 from the contract, finalizing the cross-chain transaction and marking the non-existent `txId` as SETTLED, while assuming that the contract acted valid.

### Recommendation

Add the same check in Cairo's `receive_cross_chain_callback`.

```diff
fn receive_cross_chain_callback(ref self: ContractState, cross_chain_msg_id: felt252, from_chain: felt252, to_chain: felt252,
from_handler: u256, to_handler: ContractAddress, cross_chain_msg_status: u8) -> bool{
    assert(to_handler == get_contract_address(),'error to_handler');

    assert(self.settlement_address.read() == get_caller_address(), 'not settlement');

    assert(self.support_handler.read((from_chain, from_handler)) && 
            self.support_handler.read((to_chain, contract_address_to_u256(to_handler))), 'not support handler');

+   assert(self.created_tx.read(cross_chain_msg_id).tx_status == CrossChainTxStatus::PENDING, 'tx status error');

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

## [04] `ERC20TransferPayload` encoding/decoding can be simplified

### Issue Description

`deocde_transfer` can be simplified because in `ERC20CodecV1` because none of the params of the `ERC20TransferPayload` struct are of dynamic type (string or bytes). Encoding/decoding can be easily simplified because it doesn’t matter whether the encoding is packed or not, the output bytes will be always the same, due to the types of properties:

[ERC20CodecV1.sol](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ERC20CodecV1.sol#L36C5-L46C11)

```solidity
function encode_transfer(
      ERC20TransferPayload memory _payload
  ) external pure returns (bytes memory encodedPaylaod) {
      encodedPaylaod = abi.encodePacked(
          _payload.method_id,
          _payload.from,
          _payload.to,
          _payload.from_token,
          _payload.to_token,
          _payload.amount
      );
  }
```

Additionally, the decoding is also heavily complicated; it can simply decode to the `ERC20TransferPayload` directly instead of manually parsing and slicing the array:

[ERC20CodecV1.sol](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ERC20CodecV1.sol#L65C5-L74C6)

```solidity
function deocde_transfer(
        bytes calldata _payload
    ) external pure returns (ERC20TransferPayload memory transferPayload) {
        transferPayload.method_id = ERC20Method(uint8(_payload[0]));
        transferPayload.from = abi.decode(_payload[1:33], (uint256));
        transferPayload.to = abi.decode(_payload[33:65], (uint256));
        transferPayload.from_token = abi.decode(_payload[65:97], (uint256));
        transferPayload.to_token = abi.decode(_payload[97:129], (uint256));
        transferPayload.amount = abi.decode(_payload[129:161], (uint256));
    }
```

### Recommendation

`encode_transfer` should be modified like this:

```diff
function encode_transfer(
      ERC20TransferPayload memory _payload
  ) external pure returns (bytes memory encodedPaylaod) {
-     encodedPaylaod = abi.encodePacked(
+     encodedPaylaod = abi.encode(
          _payload.method_id,
          _payload.from,
          _payload.to,
          _payload.from_token,
          _payload.to_token,
          _payload.amount
      );
  }
```

`deocde_transfer` should look like this:

```solidity
function deocde_transfer(
        bytes calldata _payload
    ) external pure returns (ERC20TransferPayload memory transferPayload) {
	     return abi.decode(_payload, (ERC20TransferPayload));
}
```

## [05] Superfluous checks in `receive_cross_chain_msg`

### Issue Description

`ChakraSettlementHandler::receive_cross_chain_msg` contains 2 identical checks regarding the payload type and one of them is redundant:

[ChakraSettlementHandler.sol](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L316-L318)

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
if (is_valid_handler(from_chain, from_handler) == false) {
    return false;
}
bytes calldata msg_payload = MessageV1Codec.payload(payload);

require(isValidPayloadType(payload_type), "Invalid payload type");

if (payload_type == PayloadType.ERC20) {
    // Cross chain transfer
    {
    // Decode transfer payload
            ERC20TransferPayload memory transfer_payload = codec
                .deocde_transfer(msg_payload);

            if (mode == SettlementMode.MintBurn) {
                _erc20_mint(
                    AddressCast.to_address(transfer_payload.to),
                    transfer_payload.amount
                );
                return true;
            } else if (mode == SettlementMode.LockUnlock) {
                _erc20_unlock(
                    AddressCast.to_address(transfer_payload.to),
                    transfer_payload.amount
                );

                return true;
            } else if (mode == SettlementMode.LockMint) {
                _erc20_mint(
                    AddressCast.to_address(transfer_payload.to),
                    transfer_payload.amount
                );
                return true;
            } else if (mode == SettlementMode.BurnUnlock) {
                _erc20_unlock(
                    AddressCast.to_address(transfer_payload.to),
                    transfer_payload.amount
                );
                return true;
            }
        }
    }

    return false;
}
```

As we can see the first require `isValidPayloadType` is redundant because the if check below does the same. As a result when the payload type is not `ERC20` we will revert, without even entering the check in the if statement. 

### Recommendation

Remove the require statement and add else statement, so when the other payload types are supported it will be easier to upgrade the contracts:

```diff
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
if (is_valid_handler(from_chain, from_handler) == false) {
    return false;
}
bytes calldata msg_payload = MessageV1Codec.payload(payload);

- require(isValidPayloadType(payload_type), "Invalid payload type");

if (payload_type == PayloadType.ERC20) {
    // Cross chain transfer
    {
    // Decode transfer payload
            ERC20TransferPayload memory transfer_payload = codec
                .deocde_transfer(msg_payload);

            if (mode == SettlementMode.MintBurn) {
                _erc20_mint(
                    AddressCast.to_address(transfer_payload.to),
                    transfer_payload.amount
                );
                return true;
            } else if (mode == SettlementMode.LockUnlock) {
                _erc20_unlock(
                    AddressCast.to_address(transfer_payload.to),
                    transfer_payload.amount
                );

                return true;
            } else if (mode == SettlementMode.LockMint) {
                _erc20_mint(
                    AddressCast.to_address(transfer_payload.to),
                    transfer_payload.amount
                );
                return true;
            } else if (mode == SettlementMode.BurnUnlock) {
                _erc20_unlock(
                    AddressCast.to_address(transfer_payload.to),
                    transfer_payload.amount
                );
                return true;
            }
        }
    }
+ else {
+	   revert("Currently unsupported");
+ }

    return false;
}
```

## [06] `receive_cross_chain_msg` has unnecessary if clause

### Issue Description

There is a redundant status assignment in the `ChakraSettlement::receive_cross_chain_msg`:

[ChakraSettlement.sol](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/ChakraSettlement.sol#L227-L233)

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
    ...MORE CODE

    bool result = ISettlementHandler(to_handler).receive_cross_chain_msg(
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
    } else {
        receive_cross_txs[txid].status = CrossChainMsgStatus.Failed;
    }

    emit CrossChainHandleResult(
        txid,
        status,
        contract_chain_name,
        from_chain,
        address(to_handler),
        from_handler,
        payload_type
    );
}
```

When `ISettlementHandler(to_handler).receive_cross_chain_msg` is called we need the returned value in order to determine the status of the transaction and emit the event which will trigger the callback, but the `result` variable contains redundant `else` statement:

```solidity
else {
        receive_cross_txs[txid].status = CrossChainMsgStatus.Failed;
    }
```

We can simply assign the default `status` to `Failed` and only have `if`  statement which will change the status to `Success`.

Same if check is observed in `settlement` contract:

[settlement.cairo](https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/settlement.cairo#L356-L361)

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

					...MORE CODE
            // call handler receive_cross_chain_msg
            let handler = IHandlerDispatcher{contract_address: to_handler};
            let success = handler.receive_cross_chain_msg(cross_chain_msg_id, from_chain, to_chain, from_handler, to_handler , payload);

            let mut status = CrossChainMsgStatus::SUCCESS;
            if success{
                status = CrossChainMsgStatus::SUCCESS;
            }else{
                status = CrossChainMsgStatus::FAILED;
            }
```

Here we also want to check what is the status of the execution of `handler_erc20` and emit even with the right status. Now the if is redundant because it won’t change the status.

### Recommendation

Remove the else statement and leave only the if check:

```diff
    CrossChainMsgStatus status = CrossChainMsgStatus.Failed;
    if (result == true) {
        status = CrossChainMsgStatus.Success;
-       receive_cross_txs[txid].status = CrossChainMsgStatus.Success;
    } 
-   else {
-       receive_cross_txs[txid].status = CrossChainMsgStatus.Failed;
-   }

+   receive_cross_txs[txid].status = status;
```

And in `Cairo`:

```diff

            // call handler receive_cross_chain_msg
            let handler = IHandlerDispatcher{contract_address: to_handler};
            let success = handler.receive_cross_chain_msg(cross_chain_msg_id, from_chain, to_chain, from_handler, to_handler , payload);

-           let mut status = CrossChainMsgStatus::SUCCESS;
-           if success{
-               status = CrossChainMsgStatus::SUCCESS;
-           }else{
-               status = CrossChainMsgStatus::FAILED;
-           }

+           let mut status = CrossChainMsgStatus::FAILED;
+           if success{
+               status = CrossChainMsgStatus::SUCCESS;
+           }
```

## [07] `verifyECDSA` can have strict equality

### Issue Description

Function which is used to check the validator signatures uses **greater than or equal to (`≥`)** when comparing to the validator threshold number. Indeed such check is not needed because the for loop is terminated as long as the `m` == `required_validators` :

[SettlementSignatureVerifier.sol](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/SettlementSignatureVerifier.sol#L207)

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

The set of signatures are considered valid when there are valid signatures, equal to the threshold we don’t need to continue to check the others.

### Recommendation

Replace the `≥` sign with simply ==:

```diff
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
-             validators[msgHash.recover(sig)] && ++m >= required_validators
+             validators[msgHash.recover(sig)] && ++m == required_validators
          ) {
              return true;
          }
      }

      return false;
  }
```

## [08] `set_required_validators_num` should have check if `req_validator` \< `validator_count`

### Issue Description

`set_required_validators_num` should check whether the `_required_validators` argument isn’t higher than the current `validator_count`. Otherwise contracts can end up in a state where, even if all the validators are active and provide signatures, they also won’t be enough to validate cross-chain transaction. Currently such check is not presented and manager can intentionally, or not pass higher number than the number of current validators and DoS the cross-chain functionality until another manager doesn’t decrease the value:

[BaseSettlement.sol](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/BaseSettlement.sol#L121-L127)

```solidity
function set_required_validators_num(
        uint256 _required_validators
    ) external virtual onlyRole(MANAGER_ROLE) {
        uint256 old = required_validators;
        required_validators = _required_validators;
        emit RequiredValidatorsChanged(msg.sender, old, required_validators);
    }
```

### Recommendation

Add a check to prevent even the managers from passing `_required_validators` higher than the number of the validators:

```diff
function set_required_validators_num(
        uint256 _required_validators
    ) external virtual onlyRole(MANAGER_ROLE) {
+       require(_required_validators <= validator_count, "req exceeds current number of validators");
        uint256 old = required_validators;
        required_validators = _required_validators;
        emit RequiredValidatorsChanged(msg.sender, old, required_validators);
    }
```

## [09] missing `disableInitializers` in `SettlementSignatureVerifier`

### Issue Description

`SettlementSignatureVerifier` is missing `disableInitializers` call and due to the usage of a proxy upgradeable contract without calling this function in the constructor of the logic contract. This oversight introduces a severe risk, allowing potential attackers to initialize the implementation contract itself.

### Recommendation

Call `disableInitializers`: include a call to `disableInitializers` in the constructor of the logic contract as recommended by OpenZeppelin.

[SettlementSignatureVerifier.sol](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/SettlementSignatureVerifier.sol#L16)

```diff
+	constructor() external {
+		disableInitializers()
+	}
```

## [10] `txId` is generated differently on Starknet

### Issue Description

`tx_id` in `handler_erc20` is generated differently, compared to `ChakraSettlementHandler`.

In Cairo it contains the following params:

- `transaction_hash`
- `msg_count`

[ChakraSettlementHandler.sol](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/ChakraSettlementHandler.sol#L139C9-L150C11)

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

    if (mode == SettlementMode.MintBurn) {
        _erc20_lock(msg.sender, address(this), amount);
    } else if (mode == SettlementMode.LockUnlock) {
        _erc20_lock(msg.sender, address(this), amount);
    } else if (mode == SettlementMode.LockMint) {
        _erc20_lock(msg.sender, address(this), amount);
    } else if (mode == SettlementMode.BurnUnlock) {
        _erc20_burn(msg.sender, amount);
    }

    {
        // Increment nonce for the sender
        nonce_manager[msg.sender] += 1;
    }

    // Create a new cross chain tx
    uint256 txid = uint256(
        keccak256(
            abi.encodePacked(
                chain,
                to_chain,
                msg.sender, // from address for settlement to calculate txid
                address(this), //  from handler for settlement to calculate txid
                to_handler,
                nonce_manager[msg.sender]
            )
        )
  );
```

In Solidity it contains the following params:

- `chain`
- `to_chain`
- `msg.sender`
- `address(this)`
- `to_handler`
- `nonce of caller`

[handler_erc20.cairo](https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/handler_erc20.cairo#L167C9-L183C105)

```rust
fn cross_chain_erc20_settlement(ref self: ContractState, to_chain: felt252, to_handler: u256, to_token: u256, to: u256, amount: u256) -> felt252{
			...MORE CODE
      
      let tx_id = LegacyHash::hash(get_tx_info().unbox().transaction_hash, self.msg_count.read());
```

As we can see both `tx_ids` are completely different from each other. But the intentions of the team is to construct hashes in the same way on both chains. Making the management of the transactions across different chains, `Starknet` and `EVM` in particular easier. Now they will have to have different signing logic, depending on the chain that the transaction comes.

Furthermore, the approach used in `Cairo` can potentially lead to duplicate `tx_ids`, because only 2 values are being used, both of simple types. If such scenario happens, the second user will break the invariant defined in the projects because of the active checks, preventing replays in the `receive_cross_chain_callback` functions:

> The contract maintains a consistent state between locking/burning tokens on the source chain and minting/unlocking on the destination chain, depending on the settlement mode.

### Recommendation

Modify the `handler_erc20` contract to compute the `tx_id` in the same way as in `ChakraSettlementHandler`:

```diff
fn cross_chain_erc20_settlement(ref self: ContractState, to_chain: felt252, to_handler: u256, to_token: u256, to: u256, amount: u256) -> felt252{
			...MORE CODE
      
-      let tx_id = LegacyHash::hash(get_tx_info().unbox().transaction_hash, self.msg_count.read());
+      let tx_id = LegacyHash::hash(self.chain_name.read(), (to_chain, get_caller_address(), get_contract_address(), to_handler, self.msg_count.read());
```

## [11] Message.id wrongly downcasted to uint64

### Issue Description

In `MessageV1Codec` library `id` is wrongly decoded to `uint64`, instead of the original size when being encoded - `uint256`. The `_msg` that this function expects is the `Message` struct that looks like this:

[Message.sol](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/libraries/Message.sol#L32-L39)

```solidity
struct Message {
    // The id of the message
    uint256 id;
    // The type of the payload
    PayloadType payload_type;
    // The payload of the message
    bytes payload;
}
```

As we can see, the id is of type `uint256` but in `MessageV1Codec::id` it’s downcasted and will return only the rightmost bits:

[MessageV1Codec.sol](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/handler/contracts/libraries/MessageV1Codec.sol#L57)

```solidity
function id(bytes calldata _msg) internal pure returns (uint64) {
      return uint64(bytes8(_msg[ID_OFFSET:PAYLOAD_TYPE_OFFSET]));
  }
```

### Recommendation

Apply the following changes to this function in order to return the original id that the `Message` struct is encoded with:

```diff
- function id(bytes calldata _msg) internal pure returns (uint64) {
+ function id(bytes calldata _msg) internal pure returns (uint256) {
-     return uint64(bytes8(_msg[ID_OFFSET:PAYLOAD_TYPE_OFFSET]));
+     return uint256(bytes32(_msg[ID_OFFSET:PAYLOAD_TYPE_OFFSET]));
   }
```

## [12] Whole system is missing pausability

### Issue Description

All the contracts in scope are missing pausability mechanism and in case of a failure will not be able to be stopped. This poses significant risk especially in cross-chain protocols where `handlers` (`ChakraSettlementHandler` and `handler_erc20`) are in complete control over the locked funds of the users or can be used to mint the entire supply of the Chakra token in this scenario.

By having `pause/unpause` functions and `whenNotPaused` modifiers applied you will minimize the risk in case there is an issue in your contracts. When paused you can think of a plan to rescue the funds. Pausing is also beneficial when upgrade is performed, that way you will eliminate the risk of failing cross-chain transactions when, for example, important variable is being changed. 

Without a way to pause `cross_chain_erc20_settlement`, you can’t stop users from spamming transactions when contracts are malfunctioning. 

### Recommendation

In order to fix this you should:

1. import the `PausableUpgradeable` contract from `OpenZeppelin`:

https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/blob/master/contracts/utils/PausableUpgradeable.sol

2. expose `onlyOwner` public `pause/unpause` functions 
3. add the `whenNotPaused` modifier to any of the critical functions, such as `cross_chain_erc20_settlement` and in `ChakraToken's` `mint`, `burn`, `burn_from`, `mint_to`.

## [13] Wrong `message_hash` in `receive_cross_chain_msg` on  Starknet compared to EVM

### Issue Description

`message_hash` of `receive_cross_chain_msg`, constructed in `ChakraSettlement.sol` is completely different from the `message_hash` in `settlement.cairo` .

In Solidity it’s constructed from:

- `txid`
- `from_chain`
- `from_address`
- `from_handler`
- `to_handler`
- `hash of payload`

[ChakraSettlement.sol](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/ChakraSettlement.sol#L183C12-L192C15)

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
```

In Cairo it’s constructed from:

- `from_chain`
- `cross_chain_msg_id` (txid)
- `to_chain`
- `from_handler`
- `to_handler`
- `hash of payload`

[settlement.cairo](https://github.com/code-423n4/2024-08-chakra/blob/main/cairo/handler/src/settlement.cairo#L325C8-L349C15)

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
```

As we can see the order is different and there is `to_chain` instead of `from_address` in `Cairo`. But the intentions of the team is to construct hashes in the same way on both chains. Making the signing of the messages easier and the same for all validators.

### Recommendation

Modify the `message_hash` in Cairo by adding `from_address` like the one in Solidity and use the `chain_name` storage variable instead of allowing users to pass it as an argument:

```diff
- let mut message_hash: felt252 = LegacyHash::hash(from_chain, (cross_chain_msg_id, to_chain, from_handler, to_handler));
+ let mut message_hash: felt252 = LegacyHash::hash(cross_chain_msg_id, (from_chain, chain_name, from_handler, to_handler));
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
```

Or if the Starknet one is better (as we don't know what is the correct intention of the developers), in Solidity you just have to replace the `from_address` with `contract_chain_name`:

```diff
 bytes32 message_hash = keccak256(
                abi.encodePacked(
                    txid,
                    from_chain,
-                   from_address,
+                   contract_chain_name,
                    from_handler,
                    to_handler,
                    keccak256(payload)
                )
            );

```

## [14] Protocol hashes do not use `EIP712`

### Issue Description

Signatures that validators provide in order to validate the messages are not compliant with the `EIP712`, as a result they will be unreadable by wallets as `Metamask` and can pose some difficulties for the signers.

The most crucial discrepancies are the fact that there is no `domainSeparator` (that includes the version, chainId, address of the verifying contract and salt, used to prevent replays), `hashStruct` (the hashed struct, in Chakra’s case - `message_hash`, it has to have defined struct and it’s signature should be hashed) and `encodeData` (that included the message that should be signed, in Chakra’s case the `message_hash` itself which contains all the params that make sense for the logical execution).

That will make the whole message signing easier and more readable. Currently we are expecting sign `bytes` array that is manually processed from the validators:

[ChakraSettlement.sol](https://github.com/code-423n4/2024-08-chakra/blob/main/solidity/settlement/contracts/ChakraSettlement.sol#L285C5-L301C6)

```solidity
function verifySignature(
        uint256 txid,
        uint256 from_handler,
        address to_handler,
        CrossChainMsgStatus status,
        uint8 sign_type,
        bytes calldata signatures
    ) internal view {
        bytes32 message_hash = keccak256(
            abi.encodePacked(txid, from_handler, to_handler, status)
        );

        require(
            signature_verifier.verify(message_hash, signatures, sign_type),
            "Invalid signature"
        );
    }
```

### Recommendation

Add the [EIP712](https://eips.ethereum.org/EIPS/eip-712#definition-of-hashstruct) support, in order to make the process of signing easier and displaying signatures in a more readable format as well. 

- New message data struct that contains all the important params (the ones that are used from the `message_hash` currently).


***

# Disclosures

C4 is an open organization governed by participants in the community.

C4 audits incentivize the discovery of exploits, vulnerabilities, and bugs in smart contracts. Security researchers are rewarded at an increasing rate for finding higher-risk issues. Audit submissions are judged by a knowledgeable security researcher and developer and disclosed to sponsoring developers. C4 does not conduct formal verification regarding the provided code but instead provides final verification.

C4 does not provide any guarantee or warranty regarding the security of this project. All smart contract software should be used at the sole risk and responsibility of users.
