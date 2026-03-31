# Aave - weETH (Ethereum Core Market) Risk Rating

**Rating Date**: 2026-03-16
**Final Grade**: BBB+
**Total Score**: 835.6/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-alpha

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 342.9/360 (95.2%)

**NOTE: All Security scores are IDENTICAL to the Aave WETH, USDT, and wstETH ratings. Same contracts, same governance, same key management.**

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. Aave: 30+ audits from Tier-0/1 firms (OpenZeppelin, Trail of Bits, Sigma Prime, Certora, PeckShield, Sherlock, Oxorio, MixBytes, Pashov). weETH underlying (ether.fi): 28 audit reports from Certora (continuous through Jan 2026), Zellic (Tier-0), Halborn (Tier-1), Nethermind (Tier-1), Omniscia (Tier-1), Paladin, Decurity, CertiK, Hats Finance. All reports public. | 9 | 9 | - | [P1] [Aave Security](https://aave.com/security), [P1] [ether.fi Audits](https://github.com/etherfi-protocol/smart-contracts/tree/master/audits) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Aave V3.4 (June 2025): Certora (Tier-0). ether.fi Jan 2026: Certora (Tier-0) reaudit of core contracts. Multiple Tier-0 auditors on latest versions for both Aave and ether.fi. | 9 | 9 | - | [P1] [Aave Security](https://aave.com/security), [P1] [ether.fi Certora Jan 2026](https://github.com/etherfi-protocol/smart-contracts/tree/master/audits) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Every Aave version (V3.0-V3.6) audited. ether.fi maintains continuous Certora audits: EigenLayer slashing (Apr 2025), V3.Prelude (Aug 2025), Pectra features (Sep 2025), weETH adapter (Oct 2025), reaudit core (Jan 2026). | 9 | 9 | - | [P1] [Aave Security](https://aave.com/security), [P1] [ether.fi Audits GitHub](https://github.com/etherfi-protocol/smart-contracts/tree/master/audits) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. Aave Nov 2023 critical vulnerability patched immediately. ether.fi Certora provides formal verification with continuous reaudits. Hats Finance audit found medium reentrancy bug -- resolved. No outstanding critical/high findings. | 9 | 9 | - | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P1] [ether.fi Audits](https://github.com/etherfi-protocol/smart-contracts/tree/master/audits) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Aave: Upgradeable via transparent proxy with DAO governance + 1-7 day timelock. Two 5-of-9 Guardian multisigs can veto. weETH contract itself is non-upgradeable (simple wrapper). | 9 | 9 | - | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P0] [Etherscan weETH](https://etherscan.io/address/0xCd5fE23C85820F7B72D0926FC9b05b43E359b7ee) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No user fund losses on weETH reserve. March 2026 CAPO incident affected wstETH only. ether.fi had a Sep 2024 domain account takeover attempt -- no fund loss. Aave core protocol has never been exploited for user funds. | 9 | 9 | - | [P1] [ether.fi Sep 2024 Incident](https://etherfi.gitbook.io/etherfi/security/sep-24-incident-attempted-domain-account-takeover), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events for Aave or ether.fi. Aave founded 2017 (8+ year track record). ether.fi founded 2023 with publicly identified team. | 9 | 9 | - | [P1] [Aave Security](https://aave.com/security), [P1] [ether.fi docs](https://etherfi.gitbook.io/etherfi/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. Standard proposals maintain 1-day delay, critical changes require 7-day delay. Guardian system provides additional veto layer. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Aave: Immunefi bounty up to $1M. ether.fi: Immunefi bounty program active. Both on established platform with meaningful scope. | 9 | 9 | - | [P1] [Aave Immunefi](https://immunefi.com/bug-bounty/aave/), [P1] [ether.fi Immunefi](https://immunefi.com/bug-bounty/etherfi/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. DDoS protection, DNSSEC, intrusion detection documented. Chaos Labs Risk Stewards with 1,100+ automated parameter adjustments. However, CAPO oracle monitoring insufficient -- wstETH misconfiguration went undetected for a month before March incident. | 9 | 9 | - | [P1] [Aave Security](https://aave.com/security), [P2] [Chaos Labs Slope2 Oracle](https://chaoslabs.xyz/posts/introducing-the-aave-slope2-risk-oracle) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Yes. Protocol Emergency Guardian (5-of-9) can pause markets. V3.3 bad debt verification. Slope2 Risk Oracle auto-adjusts rates. However, no automatic circuit breaker prevented CAPO-triggered wstETH liquidations. | 9 | 9 | - | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |

**Smart Contract Security Subtotal: 180.0/180 (100.0%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | DAO governance via AAVE/stkAAVE/aAAVE token voting. All changes require on-chain vote with quorum, then 1-7 day timelock. Two 5-of-9 Guardian multisigs. Risk Stewards (Chaos Labs) adjust parameters within preset bounds. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Requires DAO vote + timelock. Guardians can only pause/veto, not move funds. Protocol is non-custodial with permissionless withdrawals. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Protocol Emergency Guardian: 5-of-9 (Chaos Labs, LlamaRisk, Karpatkey, TokenLogic, Certora, BGD Labs, ACI, 2 delegates). Governance Emergency Guardian: 5-of-9 (Zapper, ParaSwap, Standard Crypto, DeFi Saver, Balancer, Chainlink, Lido, security firms). Note: BGD Labs and ACI are departing, requiring Guardian signer rotation. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [Guardian Renewal](https://governance.aave.com/t/arfc-renewal-of-aave-guardian-2024/17523) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause limited to Guardians via 5-of-9 multisig. No address-level blocking capability. Withdrawals are permissionless via Pool contract based on available liquidity. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user weETH deposits held in Pool V3 contract (0x87870Bca3F3fD6335C3F4ce8392D69350B4fA4E2). aEthweETH (0xBdfa7b7893081B35Fb54027489e2Bc7A38275129) represents user positions. | 9 | 9 | - | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P0] [Etherscan weETH](https://etherscan.io/address/0xCd5fE23C85820F7B72D0926FC9b05b43E359b7ee) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation: Pool V3 contract holds all user funds. DAO treasury managed separately by Karpatkey. Collector at 0x464C71f6c2F760DdA6093dCB91C24c39e5d6e18c. | 9 | 9 | - | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P0] [Etherscan Collector](https://etherscan.io/address/0x464C71f6c2F760DdA6093dCB91C24c39e5d6e18c) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- Aave is a lending protocol, not a vault. Users deposit assets directly to pools. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | **Partial.** March 2026 CAPO incident demonstrated rapid emergency response. However, no comprehensive public playbook for key rotation or signer replacement. Especially critical given BGD Labs and ACI departures requiring Guardian signer rotation. | 3 | 9 | **Improvable** | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |

**Key Management Subtotal: 162.9/180 (90.5%)**
- 6 questions at score 9 = 54 points
- 1 question at score 3 = 3 points
- 1 question N/A (S-KM-07)
- Raw: 57/63, Weighted: (57/63) x 180 = 162.857 = 162.9

---

### **Security Total: 342.9/360 (95.2%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 180.0 | 180 | 100.0% |
| Key Management | 162.9 | 180 | 90.5% |
| **Security Total** | **342.9** | **360** | **95.2%** |

---

### STRATEGY (30% Weight) -- Score: 236.7/270 (87.7%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | For weETH suppliers: yield from Aave borrower interest is negligible (<0.01% APY) due to near-zero utilization. weETH inherently accrues ether.fi staking + EigenLayer restaking rewards (~3-6% APR). Primary use case is collateral for borrowing WETH/stablecoins via E-Mode. All yield organic. | 9 | 9 | - | [P0] Reserve data: Supply APY <0.01%, Utilization 0.02%. [P1] [ether.fi eETH](https://etherfi.gitbook.io/etherfi/staking/eeth) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail scenarios: smart contract exploit, severe oracle failure (CAPO), or EigenLayer slashing event causing weETH exchange rate decline. Umbrella provides first-loss coverage. CAPO vulnerability exists (demonstrated on wstETH) but weETH was not directly impacted. EigenLayer slashing risk is socialized across eETH holders. | 9 | 9 | - | [P1] [Umbrella Docs](https://aave.com/docs/aave-v3/umbrella), [P1] [EigenLayer Slashing](https://docs.eigenlayer.xyz/eigenlayer/concepts/slashing) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No protocol-level leverage. Users can construct leveraged positions (weETH/WETH loop via E-Mode at up to 93% LTV, ~14x max). This is user-initiated. Protocol itself operates at 1:1. weETH involves EigenLayer restaking (a form of rehypothecation of staked ETH), but this is inherent to the underlying asset, not Aave's doing. | 9 | 9 | - | [P1] [E-Mode Docs](https://aave.com/help/borrowing/e-mode), [P1] [ether.fi Technical Docs](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/technical-documentation) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | Yes. Variable liquidation close factor (50% at HF 0.95-1.0, 100% at HF <0.95). Supply/borrow caps via CapAutomator. E-Mode parameters for correlated assets. CAPO oracle provides exchange rate validation for weETH (same system that failed for wstETH). Current LTV 77.5% well below 80% liquidation threshold. | 9 | 9 | - | [P1] [Aave V3 Features](https://github.com/aave-dao/aave-v3-origin/blob/main/docs/3.3/Aave-v3.3-features.md), [P0] Reserve data: LTV 77.5%, LT 80.0% |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | **Yes -- close variant.** March 2026 CAPO incident affected wstETH on the same Aave V3 contract ($27.78M in wrongful liquidations across 34 accounts). weETH was not directly impacted but uses the identical CAPO oracle architecture with different parameters. The "close variant" clause applies: same codebase, same oracle system, same E-Mode structure. ether.fi itself has no loss events, but the shared CAPO vulnerability means the same type of misconfiguration could affect weETH. | 3 | 3 | **Non-Improvable** | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Chaos Labs and LlamaRisk provide continuous risk analysis. weETH-specific: E-Mode parameters, supply/borrow caps documented. Risk parameter adjustment proposals published (ARFC). Over 1,100 automated parameter updates since late 2024. | 9 | 9 | - | [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters), [P2] [weETH Risk Parameter Adjustment](https://governance.aave.com/t/arfc-weeth-risk-parameter-adjustment/20167) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. weETH supply APY on Aave is negligible (<0.01%) -- users supply weETH primarily as collateral. weETH inherently accrues ether.fi staking + EigenLayer restaking rewards. No emissions required on Aave side. ether.fi rewards include ETH staking (~3-4%), EigenLayer AVS rewards, and loyalty points (ETHFI). | 9 | 9 | - | [P0] Reserve data: Supply APY <0.01%. [P1] [ether.fi eETH](https://etherfi.gitbook.io/etherfi/staking/eeth) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes. weETH withdrawal from Aave depends on available pool liquidity. With near-zero utilization (0.02%), essentially all supplied weETH is available for withdrawal. weETH itself has deep secondary market liquidity ($2.8B+ TVL on ether.fi) and can be unwrapped to eETH on-chain or swapped on DEXs. | 9 | 9 | - | [P0] Pool: utilization 0.02%. [P3] [DeFiLlama ether.fi](https://defillama.com/protocol/ether.fi-stake) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. Aave lending yield is from borrower interest (negligible for weETH). The weETH/eETH exchange rate is monotonically increasing by design. No invertible spread. EigenLayer restaking rewards are additive. | 9 | 9 | - | [P1] [ether.fi Technical Docs](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/technical-documentation) |

**Protocol Mechanics Subtotal: 41.7/45 (92.7%)**
- 8 questions at score 9 = 72, 1 question at score 3 = 3
- Raw: 75/81, Weighted: (75/81) x 45 = 41.667 = 41.7

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | weETH is used as collateral to borrow WETH and stablecoins. Standard LTV 77.5%, E-Mode ETH-correlated 93% LTV. Aave governance explicitly noted weETH is "a higher-risk asset in various ways: architectural, economic, governance, access control, and dependency" vs wstETH. Risk-tiered with lower default LTV than wstETH. Established large-cap asset ($4.95B on Aave, $2.8B+ ether.fi TVL). | 9 | 9 | - | [P2] [weETH Risk Parameters](https://governance.aave.com/t/arfc-weeth-risk-parameter-adjustment/20167), [P0] Reserve data: LTV 77.5%, E-Mode 93% |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | **Untested under token-specific stress.** weETH has maintained its exchange rate to eETH through generic market crashes (Feb 2025, Feb 2026), but has never been through a token-specific stress event comparable to Lido's July 2025 mass exit (235k+ stETH queued, 0.3-0.6% depeg, 16+ day withdrawal queues). The weETH/eETH rate increases monotonically by design, but secondary market liquidity under severe redemption pressure is untested. ether.fi launched 2023 vs Lido 2020 -- significantly less battle-testing history. Per scoring principles: demonstrated resilience must score higher than untested. | 3 | 3 | **Non-Improvable** | [P1] [ether.fi Technical Docs](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/technical-documentation), [P3] [DeFiLlama ether.fi](https://defillama.com/protocol/ether.fi-stake), [P4] [Etherfi eETH Rating](../ratings/Etherfi-eETH-Rating.md) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | **weETH carries additional EigenLayer restaking slashing risk beyond ETH consensus slashing.** ether.fi uses DVT (Distributed Validator Technology) operators registered in a role registry. EigenLayer slashing (launched April 2025) means if AVS validators misbehave, restaked ETH can be slashed -- losses socialized across eETH holders. ether.fi has Certora audit specifically for EigenLayer slashing (Apr 2025). Operator diversification exists but less mature than Lido's 600+ operators. Conservative LTV (77.5% standard vs wstETH's 78.5%) partly accounts for this extra risk layer. | 3 | 3 | **Non-Improvable** | [P1] [ether.fi Technical Docs](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/technical-documentation), [P1] [Certora EigenLayer Slashing Audit Apr 2025](https://github.com/etherfi-protocol/smart-contracts/tree/master/audits), [P1] [EigenLayer Slashing](https://docs.eigenlayer.xyz/eigenlayer/concepts/slashing) |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | weETH is a native Ethereum wrapped representation of eETH -- no bridge risk. Wrapping is an on-chain operation via ether.fi's LiquidityPool contract. All native to Ethereum. | 9 | 9 | - | [P0] [Etherscan weETH](https://etherscan.io/address/0xCd5fE23C85820F7B72D0926FC9b05b43E359b7ee) |

**Collateral Subtotal: 30.0/45 (66.7%)**
- 2 questions at score 9 = 18, 2 questions at score 3 = 6
- Raw: 24/36, Weighted: (24/36) x 45 = 30.0

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum (Tier-0 chain). Chainlink price feeds (Tier-0 oracle) for ETH/USD pricing. CAPO custom oracle layer for weETH/eETH exchange rate validation. EigenLayer protocol dependency for restaking rewards. No bridge dependencies. No CEX custody. | 9 | 9 | - | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P1] [GitHub aave-capo](https://github.com/bgd-labs/aave-capo) |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | **CAPO oracle has NO redundant fallback.** The March 2026 incident (affecting wstETH) demonstrated that the CAPO custom oracle layer has no secondary price source. weETH uses the same CAPO architecture. If weETH CAPO miscalculates, the same type of wrongful liquidations could occur. Underlying Chainlink ETH/USD feed is redundant and battle-tested. | 3 | 9 | **Improvable** | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269), [P1] [GitHub aave-capo](https://github.com/bgd-labs/aave-capo) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | **Unknown.** Chainlink has enterprise certifications. Aave Labs, BGD Labs, Chaos Labs, and ether.fi: no public SOC 2/ISO27001 documentation found. | 3 | 9 | **Source Missing** | [P1] [Aave Security](https://aave.com/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | **CAPO oracle failed for wstETH on March 10, 2026.** While weETH CAPO was not directly affected, the same architecture is used. A near-identical misconfiguration one month earlier went undetected for wstETH. Other infrastructure (Ethereum, Chainlink) performed flawlessly. ether.fi handled Sep 2024 domain takeover attempt without fund loss. | 3 | 3 | **Non-Improvable** | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269), [P1] [ether.fi Sep 2024 Incident](https://etherfi.gitbook.io/etherfi/security/sep-24-incident-attempted-domain-account-takeover) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain-level halts >30 min in 12+ months. Tier-0 reliability. | 9 | 9 | - | Ethereum Tier-0 status, public knowledge |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | **EigenLayer slashing launched April 2025.** No confirmed slashing events affecting ether.fi validators to date. However, the system is relatively new. Certora audited ether.fi's EigenLayer slashing implementation (Apr 2025). If slashing occurs, losses socialized across eETH/weETH holders. Minor ETH consensus slashing events have been absorbed without impact. | 9 | 9 | - | [P1] [Certora EigenLayer Slashing Audit](https://github.com/etherfi-protocol/smart-contracts/tree/master/audits), [P4] [EigenLayer Slashing Launch](https://www.coindesk.com/tech/2025/04/17/eigenlayer-adds-key-slashing-feature-completing-original-vision) |
| ST-IC-07 | Are validators diverse geographically and by operator? | ether.fi uses DVT (Distributed Validator Technology) with multiple operators. Operator set is diversified but smaller and less proven than Lido's 600+ operators. EigenLayer operators are professional infrastructure providers (diversified across AVSs). Ethereum validator set is highly distributed (900K+ validators). No single ether.fi operator >25% of stake based on available information. | 9 | 9 | - | [P1] [ether.fi Technical Docs](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/technical-documentation) |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | **Yes -- the CAPO oracle is a single point of failure for weETH pricing, as demonstrated by the wstETH incident.** A CAPO misconfiguration for weETH could trigger wrongful liquidations. Additionally, EigenLayer itself is a critical dependency -- a systemic EigenLayer failure could affect weETH exchange rate. While Aave withdrawals themselves are permissionless, oracle-driven liquidations can cause user losses. | 3 | 3 | **Non-Improvable** | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |

**Infrastructure Counterparty Subtotal: 30.0/45 (66.7%)**
- 4 questions at score 9 = 36, 4 questions at score 3 = 12
- Raw: 48/72, Weighted: (48/72) x 45 = 30.0

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | None by Aave. User weETH deposits remain in Aave Pool V3 contract. However, weETH itself is backed by ETH restaked on EigenLayer via ether.fi -- this is inherent to the underlying asset. ether.fi is Tier-unrated but among the largest LRT protocols ($2.8B+ TVL). | 9 | 9 | - | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P3] [DeFiLlama ether.fi](https://defillama.com/protocol/ether.fi-stake) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Yes. Protocol fees visible on-chain. Reserve Factor 45% for weETH. DAO treasury managed by Karpatkey with transparent reporting. ether.fi has ETHFI token with governance and points program, but this does not create conflicts for Aave depositors. | 9 | 9 | - | [P0] Reserve Factor: 45%. [P2] [DAO Financial Reports](https://governance.aave.com/t/aave-dao-financial-reports-financial-metrics/5575) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. Supply cap: 2.60M weETH. Borrow cap: 1 (borrowing effectively disabled). E-Mode ETH-correlated parameters provide additional limits. Risk Stewards actively manage parameters. | 9 | 9 | - | [P0] Reserve data: Supply cap 2.60M, Borrow cap 1. |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Instant for Aave withdrawal (near-zero utilization). weETH itself: can be unwrapped to eETH on-chain, swapped on DEXs (Curve, Uniswap), or redeemed via ether.fi (instant if liquidity available, otherwise queue with validator exit ~14 days). Deep secondary market for weETH. | 9 | 9 | - | [P0] Utilization: 0.02%. [P1] [ether.fi Help: Unstaking](https://help.ether.fi/en/articles/269224-how-to-unstake-your-assets) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | For weETH: ether.fi operator set disclosed (DVT operators). EigenLayer operators disclosed. Chainlink oracle operators disclosed. Risk providers Chaos Labs and LlamaRisk publicly identified. Treasury manager Karpatkey disclosed. | 9 | 9 | - | [P1] [ether.fi Technical Docs](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/technical-documentation), [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |

**Protocol Counterparty Subtotal: 45.0/45 (100.0%)**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | All weETH withdrawals permissionless via Pool V3 contract based on available liquidity. Guardians can pause in emergency (5-of-9 required) but cannot block individual addresses. With borrowing disabled, essentially all supplied weETH is available. | 9 | 9 | - | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Yes. With near-zero utilization (0.02%), virtually all $4.95B in supplied weETH is available for immediate withdrawal. Borrowing is disabled (cap = 1), so no utilization risk. This is the most favorable liquidity profile among all Aave reserves. | 9 | 9 | - | [P0] Reserve data: $4.95B supplied, 0.02% utilization, borrow cap 1. |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No withdrawal delays for weETH on Aave. Borrowing disabled means no utilization-based withdrawal constraints. Nov 2023: temporary freeze during vulnerability patch (protocol-wide, not weETH-specific). >95% of withdrawals complete instantly. | 9 | 9 | - | [P0] Reserve data: utilization 0.02%. |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | No. Supply cap (2.60M) does not restrict withdrawals. Borrow cap at 1 means no borrowing, so no utilization constraints on withdrawal. Current utilization is effectively zero. | 9 | 9 | - | [P0] Reserve data: Supply cap 2.60M, Borrow cap 1, Utilization 0.02%. |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | **Favorable due to disabled borrowing.** Since weETH borrowing is disabled, there is no utilization-based constraint on withdrawals even during market stress. Unlike WETH (99.85% utilization in Feb 2026) or wstETH, weETH pool cannot experience a lending-pool liquidity squeeze. During Feb 2025 and Feb 2026 crashes, weETH remained withdrawable. | 9 | 9 | - | [P0] Borrow cap = 1 (borrowing disabled). [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No for Aave withdrawal (instant based on pool liquidity). If user wants to unwrap weETH to ETH, that depends on ether.fi liquidity pool (instant if liquid ETH available) or Ethereum validator exit queue (~14 days). But Aave withdrawal itself is instant. | 9 | 9 | - | [P1] [ether.fi Unstaking](https://help.ether.fi/en/articles/269224-how-to-unstake-your-assets) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary weETH redemption through Pool contract always available (subject to pool liquidity, which is near-100%). weETH can also be swapped on DEXs (Curve, Uniswap, Balancer) but this is optional. | 9 | 9 | - | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | weETH is the largest LRT with $4.95B on Aave and $2.8B+ ether.fi TVL. Deep DEX liquidity across Curve, Uniswap. aEthweETH directly 1:1 redeemable. Can absorb >10% of pool TVL with minimal impact under normal conditions. However, weETH DEX liquidity depth is lower than wstETH's $20B+ market. | 9 | 9 | - | [P3] [DeFiLlama ether.fi](https://defillama.com/protocol/ether.fi-stake), [P0] Reserve data: $4.95B supplied |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | **Very low for weETH specifically due to disabled borrowing.** Since weETH borrowing is disabled (cap = 1), there cannot be a utilization-driven bank-run scenario. All supplied weETH is available for withdrawal. The CAPO oracle risk remains (could trigger forced liquidations independent of utilization), but the bank-run mechanism itself is eliminated. | 9 | 9 | - | [P0] Borrow cap = 1 (borrowing disabled). |

**Liquidity Subtotal: 45.0/45 (100.0%)**

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | aEthweETH maintains 1:1 with underlying weETH by design (claim on pool). weETH/eETH exchange rate increases monotonically by design. weETH has maintained its exchange rate through Feb 2025 and Feb 2026 market crashes without depegging. However, weETH has been trading since 2023 -- less battle-testing history than wstETH. weETH has been through multiple severe market stress events without depeg. | 9 | 9 | - | [P1] [ether.fi Technical Docs](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/technical-documentation), [P3] [DeFiLlama ether.fi](https://defillama.com/protocol/ether.fi-stake) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Low for weETH suppliers. Overcollateralized design protects lenders. Borrowers face liquidation risk. weETH-specific: EigenLayer slashing could reduce weETH exchange rate, but this is a tail risk and audited (Certora). Feb 2026: Aave processed $429M in liquidations with zero bad debt across all pools. | 9 | 9 | - | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | N/A considerations: weETH borrowing is disabled so interest rate model is moot for this reserve. Supply-side only. No rate spikes or utilization stress possible. Model for other Aave reserves (where weETH is collateral for WETH borrows) is well-calibrated with Slope2 Oracle. | 9 | 9 | - | [P0] Borrow cap = 1. [P2] [Chaos Labs Slope2 Oracle](https://chaoslabs.xyz/posts/introducing-the-aave-slope2-risk-oracle) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. Chaos Labs and LlamaRisk provide continuous stress testing. Multiple real-world stress tests: Feb 2025 ($210M liquidations), Feb 2026 ($429M record liquidations), March 2026 CAPO incident. weETH-specific risk parameters explicitly set based on risk analysis (ARFC proposals document rationale). | 9 | 9 | - | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P2] [weETH Risk Parameters](https://governance.aave.com/t/arfc-weeth-risk-parameter-adjustment/20167) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | For weETH borrowers (via WETH): liquidation if collateral drops (protects lenders). For weETH suppliers: overcollateralization protects principal. CAPO oracle risk exists -- could theoretically trigger wrongful liquidations of weETH collateral positions (as demonstrated with wstETH). E-Mode (93% LTV / 95% LT) creates tight buffers. | 9 | 9 | - | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |

**Market Subtotal: 45.0/45 (100.0%)**

---

### **Strategy Total: 236.7/270 (87.7%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 41.7 | 45 | 92.7% |
| Collateral | 30.0 | 45 | 66.7% |
| Infra Counterparty | 30.0 | 45 | 66.7% |
| Protocol Counterparty | 45.0 | 45 | 100.0% |
| Liquidity | 45.0 | 45 | 100.0% |
| Market | 45.0 | 45 | 100.0% |
| **Strategy Total** | **236.7** | **270** | **87.7%** |

---

### OPERATIONS (30% Weight) -- Score: 256.0/270 (94.8%)

**NOTE: All Operations scores are IDENTICAL to the Aave wstETH rating. Same governance, team, docs, treasury, backstop.**

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | On-chain DAO governance via AAVE, stkAAVE, aAAVE token voting. Structured proposal process: Temp Check -> ARFC -> AIP. Risk Stewards handle parameter adjustments. Two 5-of-9 Guardian multisigs. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | Moderate concentration typical of large DAOs. Robust checks: Guardian multisigs, Risk Steward distribution, structured proposals. Note: ACI (61% of governance actions) departing -- may impact governance activity. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. 1-day standard timelock, 7-day for critical changes. Two Guardian multisigs with veto powers. Certora reviews all governance proposals. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A -- Aave has no "strategy manager" in the vault sense. Risk providers can be changed via governance without impacting withdrawals. | N/A | N/A | N/A | - |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 3 questions at score 9 = 27; 1 N/A
- Raw: 27/27, Weighted: (27/27) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Aave: Stani Kulechov (founder, publicly identified since 2017). Aave Labs (Swiss entity). BGD Labs: Ernesto Boado + team. ether.fi: co-founders Mike Silagadze (CEO, ex-Top Hat founder) and team publicly identified. | 9 | 9 | - | [P3] [Crunchbase](https://www.crunchbase.com/organization/ethlend), [P1] [ether.fi docs](https://etherfi.gitbook.io/etherfi/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Aave: multiple independent teams (Aave Labs, BGD Labs). However, BGD Labs departing April 2026 and ACI exit March 2026 create transition risk. ether.fi has a growing development team. | 9 | 9 | - | [P2] [BGD Leaving Aave](https://governance.aave.com/t/bgd-leaving-aave/24122) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Aave SAGL (Swiss entity, Zug). Aave Labs based in London, UK. ether.fi: Ether.fi Inc. (Cayman Islands). Multiple jurisdictional presence. | 9 | 9 | - | [P3] [Tracxn](https://tracxn.com/d/companies/aave/__JiXfiPZKVkx7021dCR937XH3M5d2vj-Cy3z3dnIPJ00) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | **CLEARED.** SEC closed 4-year investigation December 16, 2025 without enforcement action. No ongoing enforcement actions for Aave or ether.fi. | 9 | 9 | - | [P4] [Yahoo Finance](https://finance.yahoo.com/news/sec-closes-4-long-investigation-091715487.html) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Yes. March 2026 CAPO incident: borrow caps reduced within hours, post-mortem within 1 day. Nov 2023: pools secured within hours. Demonstrated rapid, effective incident response. ether.fi Sep 2024 domain incident handled without fund loss. | 9 | 9 | - | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. CAPO incident: post-mortem within 1 day, reimbursement proposal next day. Regular development updates. Active governance forum and Discord. ether.fi has help center. | 9 | 9 | - | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Aave: $29.5M from 41 investors. ether.fi: backed by major investors (publicly disclosed). Service providers all publicly disclosed. | 9 | 9 | - | [P3] [Tracxn](https://tracxn.com/d/companies/aave/__JiXfiPZKVkx7021dCR937XH3M5d2vj-Cy3z3dnIPJ00/funding-and-investors) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | **Significant governance tension and organizational instability.** BGD Labs departure effective April 2026. ACI exit March 2026. "Aave Will Win" proposal debate. Community questions about Chaos Labs' CAPO role. | 3 | 9 | **Improvable** | [P2] [BGD Leaving Aave](https://governance.aave.com/t/bgd-leaving-aave/24122), [P4] [ACI Exit](https://thedefiant.io/news/defi/aave-chan-initiative-announces-exit-from-aave-dao-amid-governance-rift) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | **CAPO incident affected wstETH only.** Chaos Labs operated the oracle that caused $27.78M in wrongful wstETH liquidations. weETH was not affected. However, Chaos Labs manages risk for all Aave reserves including weETH. Single configuration error, full reimbursement committed. 8+ year protocol track record without permanent losses. | 9 | 9 | - | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |

**Team & Legal Subtotal: 62.5/67.5 (92.6%)**
- 8 questions at score 9 = 72, 1 question at score 3 = 3
- Raw: 75/81, Weighted: (75/81) x 67.5 = 62.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive V3 documentation. weETH-specific: E-Mode parameters, CAPO oracle design documented. ether.fi has detailed GitBook with technical documentation, whitepaper. | 9 | 9 | - | [P1] [Aave Docs](https://aave.com/docs/aave-v3/overview), [P1] [ether.fi Docs](https://etherfi.gitbook.io/etherfi/) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Health factor, liquidation, bad debt, E-Mode risk parameters all documented. weETH-specific: E-Mode (93% LTV, 95% LT, 1% penalty), standard mode (77.5% LTV, 80% LT, 7% penalty). EigenLayer slashing risks documented by ether.fi. | 9 | 9 | - | [P1] [Risks](https://aave.com/docs/resources/risks), [P1] [ether.fi Technical Docs](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/technical-documentation) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Pool V3, aEthweETH, PoolConfigurator all documented and verified on Etherscan. BGD Address Book GitHub repo provides canonical registry. weETH contract address documented. | 9 | 9 | - | [P1] [BGD Address Book](https://github.com/bgd-labs/aave-address-book), [P0] [Etherscan weETH](https://etherscan.io/address/0xCd5fE23C85820F7B72D0926FC9b05b43E359b7ee) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Guardian roles, timelocks (1-day/7-day), Risk Steward permissions, CAPO oracle operator roles all documented. All changes on-chain. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full on-chain transparency. All weETH balances verifiable via Pool V3. DeFiLlama tracking. Proof-of-liabilities (borrows) also on-chain -- currently near zero. | 9 | 9 | - | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P3] [DeFiLlama](https://defillama.com/protocol/aave-v3) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. Pool V3, PoolConfigurator, weETH, aEthweETH, ProtocolDataProvider all verified on Etherscan. Full source code readable. | 9 | 9 | - | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2#code), [P0] [Etherscan weETH](https://etherscan.io/address/0xCd5fE23C85820F7B72D0926FC9b05b43E359b7ee#code) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Yes. Umbrella Safety Module (~$263M). CAPO incident reimbursement via separate AIP (~317-358 ETH), demonstrating DAO willingness to compensate. | 9 | 9 | - | [P1] [Umbrella Docs](https://aave.com/docs/aave-v3/umbrella), [P2] [Reimbursement AIP](https://governance.aave.com/t/direct-to-aip-wsteth-capo-oracle-incident-user-reimbursement/24275) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | **Modest relative to scale.** Umbrella ~$263M + DAO Treasury ~$125M = ~$388M vs $44.2B total protocol TVL (~0.88%). Below 1% threshold. | 3 | 9 | **Improvable** | [P2] [DAO Funding Insights](https://governance.aave.com/t/aave-dao-funding-insights/24192) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Treasury ~$125M. $885M fees in 2025. $50M/year buyback approved. Runway >24 months. | 9 | 9 | - | [P2] [DAO Funding Insights](https://governance.aave.com/t/aave-dao-funding-insights/24192) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Highly resilient. Feb 2026: $429M liquidations, zero bad debt. Survived 2022 bear market, FTX, Terra/Luna, SVB. weETH pool: no bad debt ever. | 9 | 9 | - | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Smart contracts permissionless and non-custodial. weETH withdrawals always available. On-chain governance continues. Protocol can operate with frozen parameters. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |

**Financial Resilience Subtotal: 58.5/67.5 (86.7%)**
- 4 questions at score 9 = 36, 1 question at score 3 = 3
- Raw: 39/45, Weighted: (39/45) x 67.5 = 58.5

---

### **Operations Total: 256.0/270 (94.8%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 67.5 | 67.5 | 100.0% |
| Team & Legal | 62.5 | 67.5 | 92.6% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 58.5 | 67.5 | 86.7% |
| **Operations Total** | **256.0** | **270** | **94.8%** |

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 99 | 99 | 180.0 | 180 | 100.0% |
| | Key Management (7 of 8 Q scored) | 57 | 63 | 162.9 | 180 | 90.5% |
| | **Security Subtotal** | | | **342.9** | **360** | **95.2%** |
| **Strategy** | Protocol Mechanics (9 Q) | 75 | 81 | 41.7 | 45 | 92.7% |
| | Collateral (4 Q) | 24 | 36 | 30.0 | 45 | 66.7% |
| | Infra Counterparty (8 Q) | 48 | 72 | 30.0 | 45 | 66.7% |
| | Protocol Counterparty (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity (9 Q) | 81 | 81 | 45.0 | 45 | 100.0% |
| | Market (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | **Strategy Subtotal** | | | **236.7** | **270** | **87.7%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 75 | 81 | 62.5 | 67.5 | 92.6% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 39 | 45 | 58.5 | 67.5 | 86.7% |
| | **Operations Subtotal** | | | **256.0** | **270** | **94.8%** |
| **TOTAL** | | | | **835.6** | **900** | **92.8%** |

---

