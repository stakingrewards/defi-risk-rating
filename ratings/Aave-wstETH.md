# Aave - wstETH (Ethereum Core Market) Risk Rating

**Rating Date**: 2026-03-16
**Final Grade**: BBB+
**Total Score**: 843.9/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-beta

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 342.9/360 (95.2%)

**NOTE: All Security scores are IDENTICAL to the Aave WETH and USDT ratings. Same contracts, same governance, same key management.**

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 30+ audits from Tier-0/1 firms: OpenZeppelin (2021), Trail of Bits (2022), Sigma Prime (2022, 2023), PeckShield (2022), ABDK (2022), Certora (continuous formal verification through V3.6), MixBytes (V3.1+), Pashov (V3.2+), Sherlock (V3.3), Oxorio (V3.2-V3.3). All reports public on GitHub. | 9 | 9 | - | [P1] [Aave Security](https://aave.com/security), [P1] [GitHub Audits](https://github.com/aave/aave-v3-core/tree/master/audits) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | V3.4 (June 2025): Certora (Tier-0, formal verification), StErMi. V3.3 (Jan 2025): Certora (Tier-0), Sherlock (Tier-0), Oxorio, StErMi. Multiple Tier-0 auditors on latest versions. | 9 | 9 | - | [P1] [Aave Security](https://aave.com/security), [P1] [Certora Reports](https://www.certora.com/reports/aave-v3-risk-steward) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Every major version (V3.0 through V3.6) has been audited. Umbrella Safety Module, GHO, and Governance V3 all received dedicated audits. Continuous audit coverage across all upgrades. | 9 | 9 | - | [P1] [Aave Security](https://aave.com/security), [P1] [GitHub aave-v3-origin](https://github.com/aave-dao/aave-v3-origin) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. November 2023 critical vulnerability (stable rate bug) patched immediately via emergency governance action; pools secured within hours. Certora formal verification provides mathematical proofs of invariant preservation. | 9 | 9 | - | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P1] [Aave Security](https://aave.com/security) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Upgradeable via transparent proxy pattern. Upgrades require full DAO governance vote followed by 1-day standard timelock or 7-day critical timelock. Two 5-of-9 Guardian multisigs can veto. | 9 | 9 | - | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No user fund losses in protocol history. Nov 2023: vulnerability patched before exploitation. March 2026 CAPO incident: oracle misconfiguration caused wrongful liquidations but no bad debt; DAO reimbursing affected users. Core protocol has never been exploited for user funds. | 9 | 9 | - | [P2] [Nov 2023 Post-Mortem](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Founded by Stani Kulechov in 2017 (ETHLend). 8+ year track record with fully transparent governance. | 9 | 9 | - | [P1] [Aave Security](https://aave.com/security), [P3] [Crunchbase](https://www.crunchbase.com/organization/ethlend) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. Standard proposals maintain 1-day delay, critical changes require 7-day delay. Guardian system provides additional veto layer. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Immunefi bounty up to $1M for critical smart contract vulnerabilities. 83+ assets in scope. Bug bounty has been actively used -- Nov 2023 critical vulnerability reported through program, Aug 2025 bounty payout documented. | 9 | 9 | - | [P1] [Immunefi](https://immunefi.com/bug-bounty/aave/), [P2] [BGD Bounty Payout Aug 2025](https://governance.aave.com/t/bgd-request-for-bounty-payout-august-2025/23096) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. DDoS protection, DNSSEC, intrusion detection documented. Chaos Labs Risk Stewards with 1,100+ automated parameter adjustments. Slope2 Risk Oracle for automated interest rate response. However, CAPO oracle monitoring was insufficient -- a near-identical misconfiguration one month before the March incident went undetected. | 9 | 9 | - | [P1] [Aave Security](https://aave.com/security), [P2] [Chaos Labs Slope2 Oracle](https://chaoslabs.xyz/posts/introducing-the-aave-slope2-risk-oracle) |
| S-SC-11 | Are automatic safety controls (e.g. pause, circuit breakers) triggered by monitoring alerts? | Yes. Protocol Emergency Guardian (5-of-9) can pause markets. V3.3 bad debt verification. Slope2 Risk Oracle auto-adjusts rates. March 2026: borrow caps reduced to 1 post-CAPO incident. However, no automatic circuit breaker prevented the CAPO-triggered liquidations. | 9 | 9 | - | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269), [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |

**Smart Contract Security Subtotal: 180.0/180 (100.0%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | DAO governance via AAVE/stkAAVE/aAAVE token voting. All changes require on-chain vote with quorum, then 1-7 day timelock. Two 5-of-9 Guardian multisigs. Risk Stewards (Chaos Labs) adjust parameters within preset bounds. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Requires DAO vote + timelock. Guardians can only pause/veto, not move funds. Protocol is non-custodial with permissionless withdrawals. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Protocol Emergency Guardian: 5-of-9 (Chaos Labs, LlamaRisk, Karpatkey, TokenLogic, Certora, BGD Labs, ACI, 2 delegates). Governance Emergency Guardian: 5-of-9 (Zapper, ParaSwap, Standard Crypto, DeFi Saver, Balancer, Chainlink, Lido, security firms). Note: BGD Labs and ACI are departing, requiring Guardian signer rotation. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [Guardian Renewal](https://governance.aave.com/t/arfc-renewal-of-aave-guardian-2024/17523) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause limited to Guardians via 5-of-9 multisig. No address-level blocking capability. Withdrawals are permissionless via Pool contract based on available liquidity. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user wstETH deposits held in Pool V3 contract (0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2). aEthwstETH (0x0B925eD163218f6662a35e0f0371Ac234f9E9371) represents user positions. | 9 | 9 | - | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P0] [Etherscan aEthwstETH](https://etherscan.io/address/0x0B925eD163218f6662a35e0f0371Ac234f9E9371) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation: Pool V3 contract holds all user funds. DAO treasury managed separately by Karpatkey. Collector at 0x464C71f6c2F760DdA6093dCB91C24c39e5d6e18c. | 9 | 9 | - | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P0] [Etherscan Collector](https://etherscan.io/address/0x464C71f6c2F760DdA6093dCB91C24c39e5d6e18c) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- Aave is a lending protocol, not a vault. Users deposit assets directly to pools. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | **Partial.** March 2026 CAPO incident demonstrated rapid emergency response (borrow caps reduced within hours, post-mortem within 1 day, reimbursement AIP filed next day). However, no comprehensive public playbook for key rotation or signer replacement. Especially critical given BGD Labs and ACI departures requiring Guardian signer rotation. | 3 | 9 | **Improvable** | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269), [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335) |

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

### STRATEGY (30% Weight) -- Score: 245.0/270 (90.7%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | For wstETH suppliers: yield comes from borrower interest on wstETH borrows. Additionally, wstETH inherently accrues Lido staking rewards. For wstETH as collateral: users borrow WETH/stablecoins and pay interest. All yield is organic lending interest. | 9 | 9 | - | [P0] Pool contract: interest accrual on supplied assets. [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail scenarios: smart contract exploit, severe oracle failure, or massive bad debt. V3.3 bad debt verification prevents cascading. Umbrella provides ~$263M first-loss coverage. The CAPO incident demonstrated oracle failure as a real loss vector, though DAO reimbursed affected users. | 9 | 9 | - | [P1] [Umbrella Docs](https://aave.com/docs/aave-v3/umbrella), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No protocol-level leverage. Users can construct leveraged positions (wstETH/WETH loop via E-Mode at up to 93% LTV, ~14x max leverage). This is user-initiated, not protocol-directed. Protocol itself operates at 1:1. | 9 | 9 | - | [P1] [E-Mode Docs](https://aave.com/help/borrowing/e-mode), [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | Yes. Variable liquidation close factor (50% at HF 0.95-1.0, 100% at HF <0.95). Supply/borrow caps via CapAutomator. E-Mode parameters for correlated assets. However, the CAPO oracle system -- designed as a safety mechanism against oracle manipulation -- itself caused the March 2026 liquidation event. | 9 | 9 | - | [P1] [Aave V3 Features](https://github.com/aave-dao/aave-v3-origin/blob/main/docs/3.3/Aave-v3.3-features.md), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | **Yes -- the March 2026 CAPO incident.** Chaos Labs' CAPO oracle misconfiguration caused ~2.85% wstETH underpricing, triggering $27.78M in wrongful liquidations across 34 accounts. Liquidators captured ~512 ETH in bonuses/profits. DAO committed to 100% reimbursement (~317-358 ETH net cost). While losses were compensated, this is a confirmed loss event for wstETH-collateral positions. A near-identical misconfiguration occurred one month earlier but went undetected. | 3 | 3 | **Non-Improvable** | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269), [P4] [Rekt News](https://rekt.news/aave-rekt) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Chaos Labs and LlamaRisk provide continuous risk analysis. Risk parameters managed through governance spells and Risk Stewards with 1,100+ automated updates since late 2024. E-Mode, Isolation Mode, supply/borrow caps all documented. | 9 | 9 | - | [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters), [P1] [Risks Documentation](https://aave.com/docs/resources/risks) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. wstETH supply APY (<0.01%) is organic from borrower interest. No emissions required. wstETH inherently accrues Lido staking yield (~3-4% APR) regardless of Aave. Low utilization (4.08%) means minimal lending yield, but the primary use case is collateral for leverage, not supply yield. | 9 | 9 | - | [P0] Reserve data: Supply APY <0.01%, Utilization 4.08%. [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-08 | Can the position be fully unwound without slippage turning yield negative? | Yes. wstETH withdrawal depends on available pool liquidity. With low utilization (~4%), most supplied wstETH is available for withdrawal. wstETH is the second-largest LST with $20B+ market cap and deep secondary market liquidity. | 9 | 9 | - | [P0] Pool: available liquidity based on utilization. [P3] wstETH deep secondary markets. |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. Lending yield is from borrower interest, not spread trading. The wstETH/ETH exchange rate is used for oracle pricing (via CAPO) but is not a source of yield. Interest rates set by utilization curves. No invertible spread. | 9 | 9 | - | [P1] Interest rate strategy based on utilization, not spreads. |

**Protocol Mechanics Subtotal: 41.7/45 (92.6%)**
- 8 questions at score 9 = 72, 1 question at score 3 = 3
- Raw: 75/81, Weighted: (75/81) x 45 = 41.667

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | wstETH is used as collateral to borrow WETH, stablecoins. As supply asset: borrowers provide overcollateralized positions. Risk tiering: E-Mode ETH-correlated 93% LTV, standard 78.5% LTV. All major collateral assets are established large-cap. | 9 | 9 | - | [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters), [P0] Reserve data: Max LTV 78.5%, E-Mode 93% |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | wstETH maintained its exchange rate to stETH through all stress events. The March 2026 CAPO issue was NOT a wstETH depeg -- the actual wstETH/ETH rate was correct; the CAPO oracle incorrectly capped the rate below market. wstETH survived Feb 2025 and Feb 2026 market crashes without depegging. Battle-tested through multiple severe events over 3+ years. | 9 | 9 | - | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | wstETH is backed by Lido's stETH with 600+ operators across multiple geographies. No single operator >1%. Conservative LTV parameters account for slashing risk. CAPO implementation for wstETH provides protection against exchange rate manipulation (though it also caused the March incident). Lido has a slashing insurance fund. | 9 | 9 | - | [P1] [Lido Operators](https://lido.fi/ethereum), [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters) |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | wstETH is a wrapped version of stETH (native Ethereum). No bridge risk -- wrapping is a thin on-chain operation via Lido's wstETH contract (0x7f39C581F595B53c5cb19bD0b3f8dA6c935E2Ca0). All assets native to Ethereum. | 9 | 9 | - | [P0] [Etherscan wstETH](https://etherscan.io/address/0x7f39C581F595B53c5cb19bD0b3f8dA6c935E2Ca0), [P1] [Lido wstETH Docs](https://docs.lido.fi/contracts/wsteth/) |

**Collateral Subtotal: 45.0/45 (100.0%)**

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum (Tier-0 chain). Chainlink price feeds (Tier-0 oracle) for ETH/USD pricing. CAPO (Correlated Asset Price Oracle) custom layer for wstETH/stETH exchange rate validation. No bridge dependencies. No CEX custody. | 9 | 9 | - | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P1] [GitHub aave-capo](https://github.com/bgd-labs/aave-capo) |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | **CAPO oracle has NO redundant fallback.** The March 2026 incident demonstrated that the CAPO custom oracle layer -- wrapping Tier-0 Chainlink feeds -- has no secondary price source or sanity check. When CAPO miscalculated the wstETH exchange rate cap, the protocol used the incorrect price directly for liquidation decisions. The underlying Chainlink ETH/USD feed functioned correctly. Chaos Labs has proposed but not yet implemented circuit breakers and boundary checks. | 3 | 9 | **Improvable** | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269), [P4] [Rekt News](https://rekt.news/aave-rekt) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | **Unknown.** Chainlink has enterprise certifications. Aave Labs, BGD Labs, and Chaos Labs: no public SOC 2/ISO27001 documentation found. Particularly important given Chaos Labs' operational role in the CAPO incident. | 3 | 9 | **Source Missing** | [P1] [Aave Security](https://aave.com/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | **CAPO oracle failed on its first live stress test for wstETH.** March 10, 2026: CAPO parameter synchronization failure caused ~2.85% underpricing, triggering $27.78M in wrongful liquidations. A near-identical misconfiguration one month earlier went undetected. Other infrastructure (Ethereum, Chainlink) performed flawlessly through all stress events. | 3 | 3 | **Non-Improvable** | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269), [P4] [Rekt News](https://rekt.news/aave-rekt) |
| ST-IC-05 | Has the base chain recently halted block production? | No. Ethereum has had no chain-level halts >30 min in 12+ months. Tier-0 reliability. | 9 | 9 | - | Ethereum Tier-0 status, public knowledge |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Minor slashing events in Ethereum validator set; all compensated by Lido's insurance fund. wstETH exchange rate has never been adversely affected by slashing. Conservative LTV parameters account for this risk. | 9 | 9 | - | [P1] [Lido Operators](https://lido.fi/ethereum), [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters) |
| ST-IC-07 | Are validators diverse geographically and by operator? | wstETH (Lido): 600+ operators, multi-region, no single operator >1%. Chainlink oracle network: 31+ independent nodes. Ethereum: 900K+ validators globally. Highly diverse. | 9 | 9 | - | [P1] [Lido Operators](https://lido.fi/ethereum) |
| ST-IC-08 | Can any single infra failure block withdrawals or cause losses? | **Yes -- the CAPO oracle proved to be a single point of failure.** The March 2026 CAPO misconfiguration alone caused $27.78M in wrongful liquidations. No secondary oracle source, no automatic sanity check, no circuit breaker prevented the incorrect price from triggering liquidations. While withdrawals themselves were not blocked, the oracle failure directly caused user losses (subsequently reimbursed by DAO). | 3 | 3 | **Non-Improvable** | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269), [P4] [Rekt News](https://rekt.news/aave-rekt) |

**Infrastructure Counterparty Subtotal: 30.0/45 (66.7%)**
- 4 questions at score 9 = 36, 4 questions at score 3 = 12
- Raw: 48/72, Weighted: (48/72) x 45 = 30.0

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | None. User wstETH deposits remain in Aave Pool V3 contract. No external deployment. | 9 | 9 | - | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented? | Yes. Protocol fees visible on-chain. Reserve Factor 35% for wstETH. DAO treasury managed by Karpatkey with transparent reporting. | 9 | 9 | - | [P0] Reserve Factor: 35%. [P2] [DAO Financial Reports](https://governance.aave.com/t/aave-dao-financial-reports-financial-metrics/5575) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. Supply cap: 1.76M wstETH. Borrow cap: temporarily 1 (post-incident, normally 180K+). E-Mode and Isolation Mode provide additional limits. Over 1,100 automated parameter updates since late 2024. | 9 | 9 | - | [P0] Reserve data: Supply cap 1.76M, Borrow cap 1.00 (temporarily reduced). [P2] [Re-enable Borrow Caps](https://governance.aave.com/t/direct-to-aip-re-enable-wsteth-borrow-caps-on-ethereum-core-and-prime-post-capo-incident/24295) |
| ST-PC-04 | How quickly can positions be unwound from each counterparty? | Instant for available liquidity. wstETH has low utilization (~4%), so most supply is available for immediate withdrawal. wstETH itself is highly liquid with $20B+ market cap and deep DEX/CEX markets. | 9 | 9 | - | [P0] Utilization: 4.08%. [P3] wstETH deep secondary markets. |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | For wstETH: Lido operator set fully disclosed (600+ operators). Chainlink oracle operators disclosed. Risk providers Chaos Labs and LlamaRisk publicly identified. Treasury manager Karpatkey disclosed. | 9 | 9 | - | [P1] [Lido Operators](https://lido.fi/ethereum), [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |

**Protocol Counterparty Subtotal: 45.0/45 (100.0%)**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused? | All wstETH withdrawals permissionless via Pool V3 contract based on available liquidity. Guardians can pause in emergency (5-of-9 required) but cannot block individual addresses. March 2026: borrow cap reduced to 1 post-CAPO incident. | 9 | 9 | - | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL? | Yes. With only ~4% utilization, approximately 96% of supplied wstETH is available for immediate withdrawal. $3.73B supplied, $152M borrowed = ~$3.58B available. Much healthier liquidity profile than WETH pool (~90% utilization). | 9 | 9 | - | [P0] Reserve data: $3.73B supplied, $152M borrowed, 4.08% utilization. |
| ST-L-03 | Have there been past withdrawal delays or freezes? | No permanent freezes for wstETH specifically. March 2026 CAPO incident: borrow cap temporarily reduced to 1 (restricting new borrows, not withdrawals). Nov 2023: temporary freeze during vulnerability patch. >95% of withdrawals complete within stated timeframe. | 9 | 9 | - | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| ST-L-04 | Do caps restrict timely redemptions during high utilization? | Supply cap (1.76M) does not restrict withdrawals. Borrow cap temporarily at 1 (restricting new borrows). Interest rate model penalizes high utilization. Current low utilization (4.08%) means caps are not binding for withdrawals. | 9 | 9 | - | [P0] Reserve data: Utilization 4.08%, Supply cap 1.76M. |
| ST-L-05 | How does exit liquidity behave during volatility? | **Potential stress during extreme events.** While wstETH itself has low utilization (~4%), the March 2026 CAPO incident demonstrated that oracle failures can trigger forced liquidations independent of market conditions. If wstETH utilization were higher (like WETH's 90%+), withdrawal liquidity could be constrained during stress. Inherent lending pool risk, though currently well-buffered by low utilization. | 3 | 3 | **Non-Improvable** | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269), [P2] [WETH Utilization Retro](https://governance.aave.com/t/retro-weth-utilization-spike-and-slope2-risk-oracle-performance/24101) |
| ST-L-06 | Do withdrawals rely on unstaking or vesting longer than stated period? | No. wstETH withdrawals from Aave are based on pool liquidity only. No lockups or vesting. Instant withdrawal if liquidity available. If user wants to unwrap wstETH to ETH, that depends on Lido but is outside Aave scope. | 9 | 9 | - | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-L-07 | Does redemption depend on secondary-market liquidity? | No. Primary wstETH redemption through Pool contract is always available (subject to pool liquidity). aEthwstETH can be traded on secondary markets but this is optional. | 9 | 9 | - | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | wstETH is the second-largest LST with $20B+ market cap. Deep DEX liquidity (Curve, Uniswap, Balancer). aEthwstETH directly 1:1 redeemable. $3.73B pool size. Can absorb >10% of pool TVL with minimal impact. | 9 | 9 | - | [P3] [DeFiLlama](https://defillama.com/protocol/aave-v3), [P0] [Etherscan aEthwstETH](https://etherscan.io/address/0x0B925eD163218f6662a35e0f0371Ac234f9E9371) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | **Moderate, inherent to lending design.** While wstETH currently has low utilization (~4%), bank-run risk exists if utilization spikes. The CAPO incident showed that even at low utilization, oracle failures can cause forced sell-offs. During WETH utilization spikes (Feb 2026: 99.85%), leveraged wstETH/WETH borrowers cannot repay WETH to deleverage, creating cascading risk. | 3 | 3 | **Non-Improvable** | [P2] [WETH Utilization Retro](https://governance.aave.com/t/retro-weth-utilization-spike-and-slope2-risk-oracle-performance/24101) |

**Liquidity Subtotal: 38.3/45 (85.2%)**
- 7 questions at score 9 = 63, 2 questions at score 3 = 6
- Raw: 69/81, Weighted: (69/81) x 45 = 38.333

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under stress? | aEthwstETH maintains 1:1 with underlying wstETH by design (interest-bearing claim on pool). No peg deviation possible architecturally. wstETH itself (vs stETH) is not a peg but an exchange rate that increases monotonically. During CAPO incident, actual wstETH rate was correct -- the CAPO oracle was wrong, not wstETH. | 9 | 9 | - | [P0] [Etherscan aEthwstETH](https://etherscan.io/address/0x0B925eD163218f6662a35e0f0371Ac234f9E9371), [P1] [Lido wstETH Docs](https://docs.lido.fi/contracts/wsteth/) |
| ST-M-02 | Can adverse crypto market moves cause permanent losses? | Low for wstETH suppliers. Overcollateralized design protects lenders. Borrowers face liquidation risk. Feb 2026: $429M total Aave liquidations with zero bad debt. wstETH inherent staking yield provides buffer. Only extreme cascading failures could create uncompensated bad debt. | 9 | 9 | - | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |
| ST-M-03 | Are interest rate models robust during TVL shifts? | Yes. Two-slope model with Slope2 Risk Oracle. wstETH-specific: low utilization (~4%) means rate model is in gentle slope region. During extreme events (like WETH utilization spikes), rates auto-adjust. Model calibrated by Chaos Labs with 1,100+ automated updates. | 9 | 9 | - | [P2] [Chaos Labs Slope2 Oracle](https://chaoslabs.xyz/posts/introducing-the-aave-slope2-risk-oracle) |
| ST-M-04 | Have historic scenarios with high volatility been modeled? | Yes. Chaos Labs and LlamaRisk provide continuous stress testing. Multiple real-world stress tests: Feb 2025 ($210M liquidations), Feb 2026 ($429M record liquidations), March 2026 CAPO incident. Certora formal verification validates invariants. The CAPO incident itself provided critical stress testing data for oracle systems. | 9 | 9 | - | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| ST-M-05 | Can sharp price moves trigger forced liquidations? | For wstETH borrowers: liquidation if collateral drops (protects lenders). For wstETH suppliers: overcollateralization protects principal. The CAPO incident showed that even without adverse market moves, oracle errors can trigger forced liquidations of healthy positions. This is the key wstETH-specific market risk. | 9 | 9 | - | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |

**Market Subtotal: 45.0/45 (100.0%)**

---

### **Strategy Total: 245.0/270 (90.7%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 41.7 | 45 | 92.6% |
| Collateral | 45.0 | 45 | 100.0% |
| Infra Counterparty | 30.0 | 45 | 66.7% |
| Protocol Counterparty | 45.0 | 45 | 100.0% |
| Liquidity | 38.3 | 45 | 85.2% |
| Market | 45.0 | 45 | 100.0% |
| **Strategy Total** | **245.0** | **270** | **90.7%** |

---

### OPERATIONS (30% Weight) -- Score: 265.0/270 (98.1%)

**NOTE: All Operations scores are IDENTICAL to the Aave WETH and USDT ratings. Same governance, team, docs, treasury, backstop.**

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes? | On-chain DAO governance via AAVE, stkAAVE, aAAVE token voting. Structured proposal process: Temp Check -> ARFC -> AIP. Risk Stewards handle parameter adjustments. Two 5-of-9 Guardian multisigs. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-G-02 | How concentrated is voting power among top holders? | Moderate concentration typical of large DAOs. Robust checks: Guardian multisigs, Risk Steward distribution, structured proposals. Note: ACI (61% of governance actions) departing -- may impact governance activity levels. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-G-03 | Are mechanisms in place to limit major changes? | Yes. 1-day standard timelock, 7-day for critical changes. Two Guardian multisigs with veto powers. Certora reviews all governance proposals. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-G-04 | Can the protocol replace the strategy manager without blocking withdrawals? | N/A -- Aave has no "strategy manager" in the vault sense. Risk providers can be changed via governance without impacting withdrawals. | N/A | N/A | N/A | - |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 3 questions at score 9 = 27; 1 N/A
- Raw: 27/27, Weighted: (27/27) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified? | Yes. Founder: Stani Kulechov (Finnish, publicly identified since 2017). Aave Labs (Swiss entity). BGD Labs: Ernesto Boado + team. Key contributors publicly identified. | 9 | 9 | - | [P3] [Crunchbase](https://www.crunchbase.com/organization/ethlend), [P1] [BGD Labs GitHub](https://github.com/bgd-labs) |
| O-TL-02 | Is the protocol dependent on a single developer? | No. Multiple independent teams: Aave Labs, BGD Labs, other contributors. However, BGD Labs (127 repos) announced departure effective April 2026, and ACI (61% of governance actions) announced exit March 3, 2026. While Aave Labs remains, the simultaneous loss creates transition risk. | 9 | 9 | - | [P2] [BGD Leaving Aave](https://governance.aave.com/t/bgd-leaving-aave/24122), [P4] [ACI Exit](https://thedefiant.io/news/defi/aave-chan-initiative-announces-exit-from-aave-dao-amid-governance-rift) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol? | Aave SAGL (Swiss entity, Zug). Aave Labs based in London, UK. DAO structure. Multiple jurisdictional presence. | 9 | 9 | - | [P3] [Tracxn](https://tracxn.com/d/companies/aave/__JiXfiPZKVkx7021dCR937XH3M5d2vj-Cy3z3dnIPJ00) |
| O-TL-04 | Are there known investigations or regulatory actions? | **CLEARED.** SEC closed 4-year investigation December 16, 2025 without enforcement action. No ongoing enforcement actions. | 9 | 9 | - | [P4] [Yahoo Finance](https://finance.yahoo.com/news/sec-closes-4-long-investigation-091715487.html) |
| O-TL-05 | Is there an on-call and incident response process? | Yes. March 2026 CAPO incident: borrow caps reduced within hours, post-mortem within 1 day, reimbursement AIP filed next day. Nov 2023: pools secured within hours. Demonstrated rapid, effective incident response. | 9 | 9 | - | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| O-TL-06 | Does the team provide timely support for critical issues? | Yes. CAPO incident: post-mortem within 1 day, reimbursement proposal next day -- exemplary speed. Regular development updates. Active governance forum and Discord. | 9 | 9 | - | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. $29.5M raised from 41 investors. Service providers (Chaos Labs, LlamaRisk, Karpatkey, BGD Labs) all publicly disclosed. | 9 | 9 | - | [P3] [Tracxn](https://tracxn.com/d/companies/aave/__JiXfiPZKVkx7021dCR937XH3M5d2vj-Cy3z3dnIPJ00/funding-and-investors) |
| O-TL-08 | Does the strategy manager manage similar products creating conflict? | **Significant governance tension and organizational instability.** Dec 2025: DAO-Labs conflict over ~$10M/year CowSwap fees. Feb 2026: Aave Labs proposed "Aave Will Win" requesting $25M + 75,000 AAVE. ACI exit March 3. BGD Labs departure effective April 2026. Community raised accountability questions about Chaos Labs' CAPO role. | 3 | 9 | **Improvable** | [P2] [BGD Leaving Aave](https://governance.aave.com/t/bgd-leaving-aave/24122), [P4] [ACI Exit](https://thedefiant.io/news/defi/aave-chan-initiative-announces-exit-from-aave-dao-amid-governance-rift), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| O-TL-09 | Has the strategy manager been involved in products with collateral loss? | **Yes -- CAPO incident.** Chaos Labs operated the oracle that caused $27.78M in wrongful liquidations. They acknowledged operational responsibility. However: single configuration error, not reckless curation; full reimbursement committed; 8+ year protocol track record without permanent losses; Aave is lending protocol not vault -- Chaos Labs is risk provider. | 9 | 9 | - | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |

**Team & Legal Subtotal: 62.5/67.5 (92.6%)**
- 8 questions at score 9 = 72, 1 question at score 3 = 3
- Raw: 75/81, Weighted: (75/81) x 67.5 = 62.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation on architecture and risks? | Yes. Comprehensive V3 documentation. CAPO post-mortem published within 1 day. wstETH-specific: E-Mode parameters, CAPO oracle design documented. | 9 | 9 | - | [P1] [Aave Docs](https://aave.com/docs/aave-v3/overview), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| O-DT-02 | Is it documented how collateral is used and when loss occurs? | Yes. Health factor, liquidation, bad debt, E-Mode risk parameters all documented. wstETH-specific: E-Mode (93% LTV, 95% LT, 1% penalty). CAPO mechanics in GitHub. | 9 | 9 | - | [P1] [Risks](https://aave.com/docs/resources/risks), [P1] [GitHub aave-capo](https://github.com/bgd-labs/aave-capo) |
| O-DT-03 | Are all contract addresses documented in one canonical place? | Yes. Pool V3, aEthwstETH, PoolConfigurator, PoolAddressesProvider all documented and verified on Etherscan. BGD Address Book GitHub repo provides canonical registry. | 9 | 9 | - | [P1] [BGD Address Book](https://github.com/bgd-labs/aave-address-book), [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| O-DT-04 | Are roles, permissions and timelocks documented? | Yes. Guardian roles, timelocks (1-day/7-day), Risk Steward permissions, CAPO oracle operator roles all documented. All changes on-chain. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-DT-05 | Does the protocol publish proof-of-reserves? | Yes. Full on-chain transparency. All wstETH balances verifiable via Pool V3. aEthwstETH supply verifiable. DeFiLlama tracking. Proof-of-liabilities (borrows) also on-chain. | 9 | 9 | - | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P3] [DeFiLlama](https://defillama.com/protocol/aave-v3) |
| O-DT-06 | Are all contracts verified on block explorers? | Yes. Pool V3, PoolConfigurator, aEthwstETH, ProtocolDataProvider all verified on Etherscan. Full source code readable. | 9 | 9 | - | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2#code) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Yes. Umbrella Safety Module (~$263M). CAPO incident reimbursement via separate AIP (~317-358 ETH), demonstrating DAO willingness to compensate for non-Umbrella events. | 9 | 9 | - | [P1] [Umbrella Docs](https://aave.com/docs/aave-v3/umbrella), [P2] [Reimbursement AIP](https://governance.aave.com/t/direct-to-aip-wsteth-capo-oracle-incident-user-reimbursement/24275) |
| O-FR-02 | How large are backstop reserves relative to TVL? | **Modest relative to scale.** Umbrella ~$263M + DAO Treasury ~$125M = ~$388M vs $44.2B total protocol TVL (~0.88%). Below 1% threshold. CAPO net cost (~$580K-$900K) easily absorbed, but reserves modest relative to total exposure. Note: DAO Treasury requires governance vote to deploy for losses (per LlamaRisk). | 3 | 9 | Improvable | [P2] [DAO Funding Insights](https://governance.aave.com/t/aave-dao-funding-insights/24192) |
| O-FR-03 | What is the estimated operational runway? | Strong. Treasury ~$125M. $885M fees in 2025. $50M/year buyback approved. Runway >24 months. | 9 | 9 | - | [P2] [DAO Funding Insights](https://governance.aave.com/t/aave-dao-funding-insights/24192) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress? | Highly resilient. Feb 2026: $429M liquidations, zero bad debt. March 2026 CAPO: net cost ~$580K-$900K, easily absorbed. Survived 2022 bear market, FTX, Terra/Luna, SVB. wstETH pool: no bad debt ever. | 9 | 9 | - | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| O-FR-05 | Can the protocol remain safe if team disappears? | Yes. Smart contracts permissionless and non-custodial. wstETH withdrawals always available. On-chain governance continues. Protocol can operate with frozen parameters. | 9 | 9 | - | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |

**Financial Resilience Subtotal: 39/45 = (39/45) x 67.5 = 58.5/67.5 (86.7%)**

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

| Category | Subcategory | Current Points | Max Points | Potential Points |
|----------|-------------|----------------|------------|------------------|
| **Security** | Smart Contract Security (11 Q) | 180.0 | 180 | 180.0 |
| | Key Management (7 of 8 Q scored) | 162.9 | 180 | 180.0 |
| | **Security Subtotal** | **342.9** | **360** | **360.0** |
| **Strategy** | Protocol Mechanics (9 Q) | 41.7 | 45 | 41.7 |
| | Collateral (4 Q) | 45.0 | 45 | 45.0 |
| | Infra Counterparty (8 Q) | 30.0 | 45 | 37.5 |
| | Protocol Counterparty (5 Q) | 45.0 | 45 | 45.0 |
| | Liquidity (9 Q) | 38.3 | 45 | 38.3 |
| | Market (5 Q) | 45.0 | 45 | 45.0 |
| | **Strategy Subtotal** | **245.0** | **270** | **252.5** |
| **Operations** | Governance (3 of 4 Q scored) | 67.5 | 67.5 | 67.5 |
| | Team & Legal (9 Q) | 62.5 | 67.5 | 67.5 |
| | Documentation (6 Q) | 67.5 | 67.5 | 67.5 |
| | Financial Resilience (5 Q) | 58.5 | 67.5 | 67.5 |
| | **Operations Subtotal** | **256.0** | **270** | **270.0** |
| **TOTAL** | | **843.9** | **900** | **882.5** |

---

