# Aave - USDC (Base V3 Market) Risk Rating

**Rating Date**: 2026-06-12
**Final Grade**: BBB
**Total Score**: 832.65/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 342.9/360 (95.2%)

**NOTE: All Security scores are IDENTICAL to the Aave USDC Ethereum rating per the Platform Consistency rule. Aave V3 Base runs the same Aave V3 Origin codebase, the same DAO governance, the same two 5-of-9 Guardian multisigs, and the same audit coverage. The base chain differs (Base vs Ethereum), but smart-contract and key-management risk is platform-level.**

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | Yes. 30+ audits from Tier-0/1 firms: OpenZeppelin, Trail of Bits, Sigma Prime, PeckShield, ABDK, Certora (continuous formal verification through V3.6), MixBytes, Pashov, Sherlock, Oxorio. Base deployment uses the same audited V3 codebase. All reports public on GitHub. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [GitHub Audits](https://github.com/aave-dao/aave-v3-origin), [P0] [Pool Proxy Base](https://basescan.org/address/0xA238Dd80C259a72e81d7e4664a9801593F98d1c5) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | V3.4 (June 2025): Certora (Tier-0, formal verification), StErMi. V3.3 (Jan 2025): Certora (Tier-0), Sherlock (Tier-0). Multiple Tier-0 auditors on latest versions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [Certora Reports](https://www.certora.com/reports/aave-v3-risk-steward) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Every major version (V3.0-V3.6) audited. Umbrella Safety Module (June 2025), GHO, Governance V3 all received dedicated audits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [GitHub aave-v3-origin](https://github.com/aave-dao/aave-v3-origin) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. November 2023 critical vulnerability patched immediately via emergency governance. All findings tracked with remediation. Certora formal verification validates invariants. Sherlock V3.3 contest validated remediation. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P1] [Aave Security](https://aave.com/security) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Upgradeable via transparent proxy pattern managed through PoolAddressesProvider. Upgrades require full DAO governance vote followed by 1-day standard or 7-day critical timelock. Two 5-of-9 Guardian multisigs can veto. Base Pool is an InitializableImmutableAdminUpgradeabilityProxy verified on Basescan. | 9 | 9 | Non-Improvable (optimal) | [P0] [Pool Proxy Base](https://basescan.org/address/0xA238Dd80C259a72e81d7e4664a9801593F98d1c5), [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No user fund losses in protocol history. Nov 2023 critical stable-rate vulnerability patched before exploitation. Feb 2025: $210M liquidations zero bad debt. Feb 2026: $429M record liquidations zero bad debt. March 2026: CAPO oracle misconfiguration caused $27.78M wstETH liquidations (Ethereum) but USDC suppliers unaffected; DAO committed to 100% reimbursement. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Post-Mortem](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Founded by Stani Kulechov in 2017 (ETHLend). 8+ year track record with transparent governance, audited code, publicly identified team. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P3] [Crunchbase](https://www.crunchbase.com/organization/ethlend) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. Standard proposals maintain 1-day delay, critical changes require 7-day delay. Governance V3 cross-chain voting via storage proofs maintained or strengthened timelock protections. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Immunefi bounty up to $1M for critical vulnerabilities. 83+ assets in scope. Active since October 2023, last updated September 2025. Bug bounty actively used. | 9 | 9 | Non-Improvable (optimal) | [P1] [Immunefi](https://immunefi.com/bug-bounty/aave/), [P2] [BGD Bounty Payout Aug 2025](https://governance.aave.com/t/bgd-request-for-bounty-payout-august-2025/23096) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. DDoS protection, DNSSEC, intrusion detection, CSP/SRI documented. BGD Labs continuous monitoring. Chaos Labs Risk Stewards (1,100+ automated parameter adjustments since late 2024, including active Base supply/borrow cap management). Slope2 Risk Oracle for utilization response. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P2] [Chaos Labs Slope2 Oracle](https://chaoslabs.xyz/posts/introducing-the-aave-slope2-risk-oracle) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Yes. Protocol Emergency Guardian (5-of-9) can pause markets. V3.3 bad-debt verification prevents new bad debt post-liquidation. Slope2 Risk Oracle automatically adjusts borrow rates during high utilization. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Features](https://github.com/aave-dao/aave-v3-origin/blob/main/docs/3.3/Aave-v3.3-features.md), [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |

**Smart Contract Security Subtotal: 180.0/180 (100.0%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | DAO governance via AAVE/stkAAVE/aAAVE token voting. All changes require on-chain vote with quorum, then 1-7 day timelock. Two 5-of-9 Guardian multisigs provide emergency controls. Base ACLManager (0x43955b...) and ACLAdmin (0x9390B1...) controlled via the same governance executor structure. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Base ACLManager](https://basescan.org/address/0x43955b0899Ab7232E3a454cf84AedD22Ad46FD33) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Requires DAO vote (quorum) + timelock execution. Guardians can only pause/veto, not move funds or upgrade custody. Protocol is non-custodial with permissionless withdrawals. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool Proxy Base](https://basescan.org/address/0xA238Dd80C259a72e81d7e4664a9801593F98d1c5) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Protocol Emergency Guardian: 5-of-9 (Chaos Labs, LlamaRisk, Karpatkey, TokenLogic, Certora, BGD Labs, ACI, 2 DAO delegates). Governance Emergency Guardian: 5-of-9 (diverse independent entities). | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [Guardian Renewal](https://governance.aave.com/t/arfc-renewal-of-aave-guardian-2024/17523) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause limited to Guardians via 5-of-9 multisig. No address-level blocking. Withdrawals permissionless via Pool based on available liquidity. Risk Stewards adjust caps within governance bounds. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool Proxy Base](https://basescan.org/address/0xA238Dd80C259a72e81d7e4664a9801593F98d1c5) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user USDC deposits held in the Base Pool contract (0xA238Dd80...). Permissionless supply/withdraw. aBasUSDC tokens (0x4e65fE4D...) represent user positions. | 9 | 9 | Non-Improvable (optimal) | [P0] [Pool Proxy Base](https://basescan.org/address/0xA238Dd80C259a72e81d7e4664a9801593F98d1c5), [P0] [aBasUSDC](https://basescan.org/address/0x4e65fE4DbA92790696d040ac24Aa414708F5c0AB) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Base Pool contract holds all user funds. Base Collector (0xBA9424d6...) is separate. DAO treasury managed separately by Karpatkey. No co-mingling. | 9 | 9 | Non-Improvable (optimal) | [P0] [Base Collector](https://basescan.org/address/0xBA9424d650A4F5c80a0dA641254d1AcCE2A37057), [P0] [Pool Proxy Base](https://basescan.org/address/0xA238Dd80C259a72e81d7e4664a9801593F98d1c5) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- Aave is a lending protocol, not a vault. Users deposit assets directly to pools. No external protocol routing of user funds. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | **Partial.** November 2023 incident demonstrated rapid emergency response. Feb 2026 utilization spike handled via automated Slope2 Oracle + Chaos Labs intervention. However, no comprehensive public playbook for key rotation or signer replacement is documented. | 3 | 9 | **Improvable** | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335) |

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

### STRATEGY (30% Weight) -- Score: 233.75/270 (86.6%)

**NOTE: Strategy is re-assessed for Base specifically. Protocol Mechanics, Protocol Counterparty, Liquidity, and Market scores match Ethereum (same mechanics, same USDC, deeply liquid). Collateral (ST-C-04) and Infrastructure Counterparty (ST-IC-01/04/05/08) score LOWER than Ethereum due to Base's Tier-2 chain status, single Coinbase sequencer (33-min halt Aug 2025), and cbBTC-dominated wrapped collateral.**

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yes. All USDC supply yield from overcollateralized borrower interest. Pool: $174.1M supplied, $147.3M borrowed at 84.59% utilization. Supply APY ~3.22%, organic from borrower demand. No Merit/liquidity-mining incentives identified on the Base USDC supply side. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan Base USDC](https://aavescan.com/base-v3/usdc), [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Principal loss can occur in severe but plausible scenarios: bad debt from cascading liquidations, smart contract exploit, oracle manipulation, or USDC issuer risk -- Circle can freeze user addresses and USDC depegged to $0.87 during March 2023 SVB crisis. S&P rates USDC stability "Strong" (Dec 2025) with BlackRock-managed Treasury reserves, but single-issuer freeze risk remains. Umbrella Safety Module provides aUSDC coverage. | 3 | 3 | Non-Improvable | [P4] [S&P USDC Strong Rating](https://www.disruptionbanking.com/2025/12/19/usdc-stablecoin-stability-assessment-remains-at-2-strong/), [P1] [Umbrella Docs](https://aave.com/docs/aave-v3/umbrella) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No protocol-level leverage or rehypothecation. User deposits remain in the Pool contract. Users can individually construct leveraged positions (user-level risk). Protocol maintains overcollateralized 1:1 backing. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | Yes. Two-slope interest rate model with Slope2 Risk Oracle. V3.3 bad-debt verification prevents new bad debt post-liquidation. 100% close factor below 0.95 health factor. Umbrella auto-slashing for aUSDC coverage. Risk Stewards actively manage Base USDC rate curves. | 9 | 9 | Non-Improvable (optimal) | [P2] [Chaos Labs Slope2 Oracle](https://chaoslabs.xyz/posts/introducing-the-aave-slope2-risk-oracle), [P1] [Aave V3 Features](https://github.com/aave-dao/aave-v3-origin/blob/main/docs/3.3/Aave-v3.3-features.md) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent losses to USDC lenders. Same codebase as Ethereum. Feb 2025: $210M liquidations zero bad debt. Feb 2026: $429M record liquidations zero bad debt. March 2026 CAPO incident affected wstETH collateral only, USDC suppliers unaffected. 8+ year track record without depositor principal loss. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Chaos Labs and LlamaRisk provide continuous quantitative risk analysis. Base USDC parameters actively managed via Risk Stewards (cap changes confirmed June 2026). E-Mode and Isolation Mode documented with clear risk tiering. | 9 | 9 | Non-Improvable (optimal) | [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters), [P2] [Risk Stewards Base Caps June 2026](https://governance.aave.com/t/risk-stewards-supply-cap-increases-on-aave-v3-2026-06-09/25120) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. USDC supply APY (~3.22%) is organic from borrower demand. No emissions required. USDC borrowing demand on Base is structural (leveraged trading, stablecoin arbitrage). Aave protocol generated $885M in fees in 2025. Sustainable without incentive dependency. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan Base USDC](https://aavescan.com/base-v3/usdc), [P3] [DeFiLlama Aave V3](https://defillama.com/protocol/aave-v3) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes under normal conditions. USDC withdrawal is direct from Pool based on available liquidity (~$26.8M = ~15.4% of supplied TVL at 84.59% utilization). USDC is deeply liquid (~$60B market cap). No slippage on in-protocol withdrawal (1:1 aBasUSDC to USDC). Rate model incentivizes repayment during high utilization. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan Base USDC](https://aavescan.com/base-v3/usdc), [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. Core USDC lending yield is pure interest from overcollateralized borrower demand -- no basis trade or funding rate. USDC has S&P "Strong" stability rating with US Treasury reserves. USDC/USD peg dependency exists but is a limited minority of overall risk. No peg inversion analogous to a funding trade. | 9 | 9 | Non-Improvable (optimal) | [P4] [S&P USDC Strong Rating](https://www.disruptionbanking.com/2025/12/19/usdc-stablecoin-stability-assessment-remains-at-2-strong/), [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |

**Protocol Mechanics Subtotal: 41.7/45 (92.6%)**
- 8 questions at score 9 = 72, 1 question at score 3 = 3
- Raw: 75/81, Weighted: (75/81) x 45 = 41.667 = 41.7

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Base USDC borrowers supply collateral from the Base asset set: cbBTC (~$133.87M, Coinbase-wrapped BTC), cbETH (~$29.34M, Coinbase LST), wstETH (~$26.82M, Lido LST), WETH. All are established large-cap or blue-chip-derived assets with on-chain LTVs and Risk-Steward-managed caps. Considered low risk because each maps to a deep underlying (BTC, ETH) with conservative parameters; cbBTC/cbETH carry Coinbase issuer dependency but track BTC/ETH 1:1. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Base Market](https://app.aave.com/markets/?marketName=proto_base_v3), [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | Major Base collateral (cbETH, wstETH, cbBTC) maintained pegs through Feb 2025 and Feb 2026 stress events, tracking ETH/BTC within tight bands. No collateral depeg above 2% lasting >24h on Base in last 12 months. Battle-tested ETH/BTC-correlated assets. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | LST collaterals (cbETH, wstETH) have conservative LTVs accounting for slashing risk. Underlying protocols diversify operators: Lido (600+ operators), Coinbase (institutional staking). Risk is immaterial to USDC lenders -- it only affects borrower collateral value. | 9 | 9 | Non-Improvable (optimal) | [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters), [P1] [Lido Operators](https://lido.fi/ethereum) |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | **Elevated on Base.** The dominant collateral asset is cbBTC (~$133.87M), a Coinbase single-custodian wrapped BTC (custody-dependent 1:1, analogous to WBTC and counted as "wrapped" per methodology). Native USDC, WETH, and protocol receipt tokens (cbETH, wstETH) are excluded from the bridged/wrapped definition. With cbBTC as the largest single collateral, wrapped exposure materially exceeds 20% of collateral TVL -- above the 20% Low threshold. Caps and rebalancing are enforced on-chain via Risk Stewards, placing this in the Mid band (>20% to 60% with documented caps). | 3 | 3 | Non-Improvable | [P1] [Aave V3 Base Market](https://app.aave.com/markets/?marketName=proto_base_v3), [P2] [Risk Stewards Base Caps](https://governance.aave.com/t/risk-stewards-supply-cap-increases-on-aave-v3-2026-06-09/25120) |

**Collateral Subtotal: 37.5/45 (83.3%)**
- 3 questions at score 9 = 27, 1 question at score 3 = 3
- Raw: 30/36, Weighted: (30/36) x 45 = 37.5

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

**NOTE: This is the primary differentiator vs the Ethereum USDC market. Base is a Tier-2 chain (per SR Chain Tiers) operated by a single centralized Coinbase OP-Stack sequencer, which halted block production for 33 minutes on Aug 5, 2025 (within the 12-month lookback). Ethereum is Tier-0 with no comparable single-sequencer SPOF.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Base (**Tier-2 chain** per SR list) -- an Optimism-stack L2 operated by Coinbase via a single centralized sequencer. Chainlink price feeds (Tier-0 oracle) via the Base AaveOracle (0x2Cc0Fc26...). No bridge dependency for native USDC. Most dependencies disclosed but the base chain is Tier-2, not Tier-0. | 3 | 3 | Non-Improvable | [P0] [Base AaveOracle](https://basescan.org/address/0x2Cc0Fc26eD4563A5ce5e8bdcfe1A2878676Ae156), [P4] [Base Sequencer Centralization](https://www.coindesk.com/tech/2025/08/06/base-says-sequencer-failure-caused-block-production-halt-of-33-minutes) |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | Chainlink price feeds (Tier-0) for asset pricing via the Base AaveOracle, which supports updatable asset sources (setAssetSources) and a fallback oracle -- no hardcoded/immutable pricing. USDC/USD feed is widely used and battle-tested. Values can be corrected under abnormal conditions via governance/Risk Stewards. | 9 | 9 | Non-Improvable (optimal) | [P0] [Base AaveOracle](https://basescan.org/address/0x2Cc0Fc26eD4563A5ce5e8bdcfe1A2878676Ae156), [P1] [Aave Oracle Docs](https://aave.com/docs/ecosystem/oracle) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | **Unknown.** Chainlink has enterprise certifications. Aave Labs, BGD Labs, and Chaos Labs: no public SOC 2 Type II / ISO27001 documentation found. | 3 | 9 | **Source Missing** | [P1] [Aave Security](https://aave.com/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Base experienced a 33-minute sequencer halt (Aug 5, 2025) and a 43-minute halt (Sept 5, 2023). During both, block production paused temporarily, degrading access, but the chain recovered with no permanent user losses and no Aave bad debt. Recovered without permanent loss -- consistent with the Mid criterion. | 3 | 3 | Non-Improvable | [P4] [Base 33-min Halt Aug 2025](https://www.theblock.co/post/365732/base-network-sequencer-failure), [P4] [Base Sept 2023 Outage](https://finance.yahoo.com/news/network-suffers-1st-downtime-since-092247914.html) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Yes. Base halted block production for ~33 minutes on Aug 5, 2025 (within the 12-month lookback), caused by a sequencer-handoff bug (Conductor selected an unprovisioned backup during congestion). Above 30 minutes, under 6 hours, full recovery via manual intervention -- Mid criterion. The earlier Sept 2023 43-min halt is outside the 12-month window. | 3 | 3 | Non-Improvable | [P4] [Base 33-min Halt CoinDesk](https://www.coindesk.com/tech/2025/08/06/base-says-sequencer-failure-caused-block-production-halt-of-33-minutes), [P4] [The Block](https://www.theblock.co/post/365732/base-network-sequencer-failure) |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | For LST collaterals (cbETH, wstETH): minor Ethereum validator slashing events, all compensated by underlying LST protocols. No impact on Aave USDC depositors. Conservative LTV parameters account for slashing risk. | 9 | 9 | Non-Improvable (optimal) | [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters) |
| ST-IC-07 | Are validators diverse geographically and by operator? | For LST collaterals backing USDC borrows: Lido (600+ operators, multi-region), Coinbase (institutional). Underlying Ethereum validator set is highly distributed. (Note: Base's single-sequencer chain centralization is captured separately in ST-IC-01/04/05/08; this question evaluates staked-collateral validators.) | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido Operators](https://lido.fi/ethereum) |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | The Base sequencer is a single centralized component whose failure halts the chain and temporarily blocks all on-chain withdrawals (demonstrated Aug 2025, ~33 min; required manual failover). Recovery restored normal operation without permanent loss, but a single-sequencer failure could delay withdrawals up to 24-48h in a worse scenario -- Mid criterion. Users retain a direct on-chain withdrawal path once the sequencer recovers. | 3 | 3 | Non-Improvable | [P4] [Base Sequencer Failover](https://unchainedcrypto.com/base-mainnet-sequencer-lag-triggers-33-minute-outage/), [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |

**Infrastructure Counterparty Subtotal: 26.25/45 (58.3%)**
- 3 questions at score 9 = 27, 5 questions at score 3 = 15
- Raw: 42/72, Weighted: (42/72) x 45 = 26.25

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | None. User USDC deposits remain in the Base Aave Pool contract. No external deployment of user collateral. Flash loans are atomic (same-block return). Liquidators operate permissionlessly but do not route user deposits externally. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P0] [Pool Proxy Base](https://basescan.org/address/0xA238Dd80C259a72e81d7e4664a9801593F98d1c5) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Yes. Protocol fees visible on-chain (Base Collector 0xBA9424d6...). DAO treasury managed by Karpatkey with transparent reporting. Fee dispute over CowSwap interface fees is a governance tension but all arrangements are visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] [Base Collector](https://basescan.org/address/0xBA9424d650A4F5c80a0dA641254d1AcCE2A37057), [P2] [DAO Financial Reports](https://governance.aave.com/t/aave-dao-financial-reports-financial-metrics/5575) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. Supply caps and borrow caps enforced on-chain per asset on Base. Caps actively managed by Chaos Labs Risk Stewards (Base cap changes confirmed June 2026). E-Mode and Isolation Mode provide additional exposure limits. | 9 | 9 | Non-Improvable (optimal) | [P2] [Risk Stewards Base Caps June 2026](https://governance.aave.com/t/risk-stewards-supply-cap-increases-on-aave-v3-2026-06-09/25120) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Instant for available liquidity. USDC withdrawal is permissionless from the Pool contract. ~$26.8M currently available. Rate model incentivizes rapid borrower repayment. No prolonged withdrawal blocks in protocol history (subject to base-chain sequencer availability, captured in ST-IC). | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan Base USDC](https://aavescan.com/base-v3/usdc) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | All disclosed. Circle as native USDC issuer is public. Coinbase as cbBTC/cbETH issuer/custodian is public. Underlying LST operators (Lido, Coinbase) disclosed. Chainlink oracle operators disclosed. Treasury manager Karpatkey disclosed. No undisclosed third parties. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |

**Protocol Counterparty Subtotal: 45.0/45 (100.0%)**

---

#### Liquidity (5% weight, 45 max points)

**Stated withdrawal baseline: Instant (simple lending, subject to available pool liquidity at normal utilization).**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | All USDC withdrawals are permissionless via the Base Pool contract based on available liquidity. Guardians can pause protocol-wide in emergency (5-of-9 multisig) but pause is not address-specific. No selective blocking. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P0] [Pool Proxy Base](https://basescan.org/address/0xA238Dd80C259a72e81d7e4664a9801593F98d1c5) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Under normal conditions, yes. $174.1M supplied, $147.3M borrowed, ~$26.8M available at 84.59% utilization (~15.4% of supplied TVL immediately redeemable, above the ~10% threshold). USDC is deeply liquid in secondary markets. Rate model incentivizes repayment to restore liquidity. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan Base USDC](https://aavescan.com/base-v3/usdc) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No Aave-specific USDC withdrawal freezes on Base. The Aug 2025 sequencer halt (~33 min) temporarily paused all Base on-chain activity but resolved with full recovery; >95% of withdrawals complete within the instant baseline over the 12-month lookback. | 9 | 9 | Non-Improvable (optimal) | [P4] [Base 33-min Halt](https://www.coindesk.com/tech/2025/08/06/base-says-sequencer-failure-caused-block-production-halt-of-33-minutes), [P3] [Aavescan Base USDC](https://aavescan.com/base-v3/usdc) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Supply caps are actively managed by Risk Stewards and have not been used to block USDC exits. Interest rate model penalizes high utilization. No history of Base USDC caps permanently blocking withdrawals. | 9 | 9 | Non-Improvable (optimal) | [P2] [Risk Stewards Base Caps](https://governance.aave.com/t/risk-stewards-supply-cap-increases-on-aave-v3-2026-06-09/25120) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | **Inherent lending risk, plus Base congestion exposure.** At 84.59% utilization, severe stress could temporarily constrain exits. Base's Aug 2025 halt was congestion-driven, adding chain-congestion risk on top of standard lending-pool exit risk. Slope2 Oracle and rate mechanisms restore liquidity, but the combination warrants Mid. | 3 | 3 | Non-Improvable | [P3] [Aavescan Base USDC](https://aavescan.com/base-v3/usdc), [P4] [Base Congestion Halt](https://crypto.news/base-layer-2-blockchain-33-minute-network-outage-2025/) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. USDC withdrawals based on available pool liquidity only. No lockups, vesting, or unstaking delays. Instant withdrawal if liquidity available. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary USDC redemption through the Pool contract is always available (subject to pool liquidity). aBasUSDC redeems 1:1. USDC has the deepest stablecoin secondary market (~$60B). Secondary market is supplementary. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | USDC is the second-most liquid stablecoin (~$60B). aBasUSDC is directly 1:1 redeemable from the Pool. The $174.1M Base pool can absorb >10% of TVL with minimal impact given USDC's global liquidity. | 9 | 9 | Non-Improvable (optimal) | [P0] [aBasUSDC](https://basescan.org/address/0x4e65fE4DbA92790696d040ac24Aa414708F5c0AB), [P3] [DeFiLlama Aave V3](https://defillama.com/protocol/aave-v3) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | **Moderate, inherent to lending design.** At 84.59% utilization, the Base USDC pool is within normal operating range. A mass exit would spike utilization, raise rates (Slope2 Oracle), and incentivize borrower repayment. Umbrella provides aUSDC coverage; V3.3 bad-debt verification prevents cascading. Design mitigations are robust but the fundamental lending-pool bank-run risk exists. | 3 | 3 | Non-Improvable | [P3] [Aavescan Base USDC](https://aavescan.com/base-v3/usdc), [P1] [Umbrella Docs](https://aave.com/docs/aave-v3/umbrella) |

**Liquidity Subtotal: 38.3/45 (85.2%)**
- 7 questions at score 9 = 63, 2 questions at score 3 = 6
- Raw: 69/81, Weighted: (69/81) x 45 = 38.333 = 38.3

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | aBasUSDC maintains 1:1 with underlying USDC by design (interest-bearing token, not a traded peg). No peg deviation possible -- it represents a claim on Pool liquidity plus accrued interest. The "peg" is architectural, not market-dependent. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P0] [aBasUSDC](https://basescan.org/address/0x4e65fE4DbA92790696d040ac24Aa414708F5c0AB) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Low for USDC lenders. Overcollateralized design protects suppliers. Borrowers face liquidation risk, not lenders. USDC has low directional exposure -- a USD stablecoin with S&P "Strong" rating. No leverage for suppliers. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P4] [S&P USDC Strong Rating](https://www.disruptionbanking.com/2025/12/19/usdc-stablecoin-stability-assessment-remains-at-2-strong/) |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Two-slope model with Slope2 Risk Oracle. USDC utilization at 84.59% is below the optimal kink. Rate curves become steep as utilization approaches critical levels, incentivizing borrower repayment. No history of prolonged >=95% utilization for Base USDC. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan Base USDC](https://aavescan.com/base-v3/usdc), [P2] [Chaos Labs Slope2 Oracle](https://chaoslabs.xyz/posts/introducing-the-aave-slope2-risk-oracle) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. Chaos Labs and LlamaRisk provide continuous stress testing across all Aave deployments including Base. Multiple real-world stress tests (Feb 2025, Feb 2026) passed without bad debt. Certora formal verification validates invariants. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P2] [Chaos Labs](https://chaoslabs.xyz/posts/introducing-the-aave-slope2-risk-oracle) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | For USDC borrowers: yes -- collateral value drops trigger liquidations (protecting USDC lenders). For USDC lenders/suppliers: no, protected by overcollateralization. Stablecoin lending advantage: USDC is borrowed against volatile cbBTC/cbETH/wstETH/WETH collateral, so collateral decline triggers protective liquidations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P1] [Aave V3 Features](https://github.com/aave-dao/aave-v3-origin/blob/main/docs/3.3/Aave-v3.3-features.md) |

**Market Subtotal: 45.0/45 (100.0%)**

---

### **Strategy Total: 233.75/270 (86.6%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 41.7 | 45 | 92.6% |
| Collateral | 37.5 | 45 | 83.3% |
| Infra Counterparty | 26.25 | 45 | 58.3% |
| Protocol Counterparty | 45.0 | 45 | 100.0% |
| Liquidity | 38.3 | 45 | 85.2% |
| Market | 45.0 | 45 | 100.0% |
| **Strategy Total** | **233.75** | **270** | **86.6%** |

**Precise Strategy calculation:**
- Protocol Mechanics: (75/81) x 45 = 41.667
- Collateral: (30/36) x 45 = 37.5
- Infra Counterparty: (42/72) x 45 = 26.25
- Protocol Counterparty: (45/45) x 45 = 45.0
- Liquidity: (69/81) x 45 = 38.333
- Market: (45/45) x 45 = 45.0
- **Total: 41.667 + 37.5 + 26.25 + 45.0 + 38.333 + 45.0 = 233.75**

---

### OPERATIONS (30% Weight) -- Score: 256.0/270 (94.8%)

**NOTE: All Operations scores are IDENTICAL to the Aave USDC Ethereum rating. Same DAO governance, same team, same documentation, same treasury/Umbrella backstop.**

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | On-chain DAO governance via AAVE, stkAAVE, aAAVE token voting. Structured proposal process: Temp Check -> ARFC -> AIP. Cross-chain governance executes changes on Base via storage-proof voting. Two 5-of-9 Guardian multisigs provide emergency controls. No single entity can unilaterally change core fund-custody logic. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [Aave Governance Forum](https://governance.aave.com/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | Moderate concentration typical of large DAOs, with robust checks: two 5-of-9 Guardian multisigs with diverse independent membership, Risk Steward system distributing parameter control, structured proposal process requiring community discussion and active participation. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [Governance Forum](https://governance.aave.com/) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. 1-day standard timelock, 7-day for critical changes. Two Guardian multisigs (5-of-9 each) with veto powers. Structured proposal process. Certora reviews governance proposals. No timelock reductions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A -- Aave has no "strategy manager" in the vault sense. Risk providers (Chaos Labs, LlamaRisk) can be changed via governance without impact on user withdrawals. Base USDC withdrawals are always permissionless and independent of service-provider changes. | N/A | N/A | N/A | - |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 3 questions at score 9 = 27 points, 1 question N/A (O-G-04)
- Raw: 27/27, Weighted: (27/27) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Founder: Stani Kulechov (publicly identified since 2017). Aave Labs (Aave SAGL, Swiss entity). BGD Labs: Ernesto Boado (former Aave CTO) + team. Key contributors publicly identified and active in governance. | 9 | 9 | Non-Improvable (optimal) | [P3] [Crunchbase](https://www.crunchbase.com/organization/ethlend), [P1] [BGD Labs GitHub](https://github.com/bgd-labs) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Multiple independent development teams: Aave Labs, BGD Labs, and others. BGD Labs alone has 127 repositories. Certora provides formal verification independently. Chaos Labs handles risk independently. | 9 | 9 | Non-Improvable (optimal) | [P1] [BGD Labs GitHub](https://github.com/bgd-labs), [P2] [BGD Phase 4 Recap](https://governance.aave.com/t/bgd-aave-bgd-labs-phase-4-recap/21667) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Aave SAGL (Swiss entity, Zug). Aave Labs based in London, UK. DAO structure with decentralized governance. Clear legal entity mapping to operational responsibilities. | 9 | 9 | Non-Improvable (optimal) | [P3] [Tracxn](https://tracxn.com/d/companies/aave/__JiXfiPZKVkx7021dCR937XH3M5d2vj-Cy3z3dnIPJ00) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | **CLEARED.** SEC closed 4-year investigation December 16, 2025 without enforcement action. No charges, fines, or further action. No ongoing or past material enforcement in major jurisdictions. | 9 | 9 | Non-Improvable (optimal) | [P4] [Yahoo Finance](https://finance.yahoo.com/news/sec-closes-4-long-investigation-091715487.html), [P4] [Unchained Crypto](https://unchainedcrypto.com/sec-ends-four-year-probe-into-aave/) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Yes. Nov 2023: rapid response (pools secured within hours). Feb 2026: Chaos Labs Risk Stewards adjusted parameters in real-time. March 2026: CAPO incident response with post-mortem and reimbursement within days. BGD Labs continuous monitoring. Guardian multisigs on standby. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Active governance forum with regular updates. Nov 2023 vulnerability resolved within hours. Feb 2026 stress: Chaos Labs published retrospective. Regular development updates from BGD Labs and Aave Labs. Discord and community channels active. | 9 | 9 | Non-Improvable (optimal) | [P2] [AL Development Update](https://governance.aave.com/t/al-development-update-november-2025/23484) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. $29.5M raised from 41 investors including Standard Crypto, Blockchain Coinvestors, ParaFi, Framework Ventures. Transparent cap table. Service providers (Chaos Labs, LlamaRisk, Karpatkey, BGD Labs) all publicly disclosed. | 9 | 9 | Non-Improvable (optimal) | [P3] [Tracxn](https://tracxn.com/d/companies/aave/__JiXfiPZKVkx7021dCR937XH3M5d2vj-Cy3z3dnIPJ00/funding-and-investors) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | **Governance tension exists.** Dec 2025: DAO-Labs conflict over ~$10M/year CowSwap interface fees redirected from DAO treasury. Feb 2026: Aave Labs proposed "Aave Will Win" plan (100% revenue to DAO in exchange for $25M + 75,000 AAVE). Debate ongoing -- a governance health issue but has not impacted user fund safety. | 3 | 9 | **Improvable** | [P4] [CoinDesk Dec 2025](https://www.coindesk.com/tech/2025/12/15/aave-dao-pushes-back-as-interface-fees-shift-away-from-treasury), [P4] [CoinDesk Feb 2026](https://www.coindesk.com/business/2026/02/12/aave-labs-proposes-aave-will-win-plan-to-send-100-of-product-revenue-to-dao) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | No. 8+ year track record without user fund losses. Nov 2023 vulnerability patched before exploitation. Feb 2025/Feb 2026 record liquidations without bad debt. March 2026 CAPO incident -> DAO committed to 100% reimbursement. Clean operational history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |

**Team & Legal Subtotal: 62.5/67.5 (92.6%)**
- 8 questions at score 9 = 72 points, 1 question at score 3 = 3 points
- Raw: 75/81, Weighted: (75/81) x 67.5 = 62.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive documentation covering V3 architecture, smart contracts, risk parameters, governance, interest rate models. Updated through V3.6 (Nov 2025). Risks page covers liquidation mechanics, oracle risks, smart contract risks. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Docs](https://aave.com/docs/aave-v3/overview), [P1] [Risks](https://aave.com/docs/resources/risks) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Detailed documentation: health factor mechanics, liquidation process, bad debt scenarios, interest rate models, E-Mode risk parameters. V3.3 bad-debt features documented. Loss conditions explained with specific scenarios. | 9 | 9 | Non-Improvable (optimal) | [P1] [Health Factor & Liquidations](https://aave.com/help/borrowing/liquidations), [P1] [Risks](https://aave.com/docs/resources/risks) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. The BGD aave-address-book provides a canonical registry including AaveV3Base (POOL 0xA238Dd80..., POOL_ADDRESSES_PROVIDER 0xe20fCBdB..., POOL_CONFIGURATOR 0x5731a04B..., ACL_MANAGER 0x43955b08...). All verified on Basescan. | 9 | 9 | Non-Improvable (optimal) | [P1] [BGD Address Book AaveV3Base](https://github.com/bgd-labs/aave-address-book), [P0] [Pool Proxy Base](https://basescan.org/address/0xA238Dd80C259a72e81d7e4664a9801593F98d1c5) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Guardian roles, timelock durations (1-day standard, 7-day critical), Risk Steward permissions and bounds, proposal process all documented. Changes visible on-chain and in the governance forum. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full on-chain transparency. Base USDC pool balances verifiable via the Pool contract. aBasUSDC supply verifiable on Basescan. AaveProtocolDataProvider (0x0F43731E...) enables programmatic verification of reserve states including borrows (proof-of-liabilities). | 9 | 9 | Non-Improvable (optimal) | [P0] [aBasUSDC](https://basescan.org/address/0x4e65fE4DbA92790696d040ac24Aa414708F5c0AB), [P3] [DeFiLlama Aave V3](https://defillama.com/protocol/aave-v3) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. Core Base contracts verified on Basescan: Pool (0xA238Dd80...), AaveOracle (0x2Cc0Fc26...), aBasUSDC (0x4e65fE4D...), PoolConfigurator, ACLManager. Full source code readable and verified. | 9 | 9 | Non-Improvable (optimal) | [P0] [Pool Proxy Base](https://basescan.org/address/0xA238Dd80C259a72e81d7e4664a9801593F98d1c5), [P0] [Base AaveOracle](https://basescan.org/address/0x2Cc0Fc26eD4563A5ce5e8bdcfe1A2878676Ae156) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Yes. Umbrella Safety Module launched June 2025 with ~$263M in staked assets (93.3M USDC, 120.8M USDT, 35.2K WETH, 14.4M GHO per LlamaRisk Dec 2025). Automated slashing mechanism for aUSDC coverage. Clear published activation rules -- automated, not discretionary. Covers Aave deployments including Base reserves. | 9 | 9 | Non-Improvable (optimal) | [P1] [Umbrella Docs](https://aave.com/docs/aave-v3/umbrella), [P2] [LlamaRisk Umbrella Coverage](https://governance.aave.com/t/llamarisk-insights-umbrella-coverage-principles-and-slashing-logic/23527) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | **Modest relative to scale.** Umbrella (~$263M) + DAO Treasury (~$125M) = ~$388M against Aave's ~$14.5B total V3 TVL = ~2.7%; against Ethereum-anchored TVL the ratio is ~1.1%. Within 1-5% range = Mid Risk. DAO Treasury requires governance to deploy for user losses. For the Base USDC pool ($174.1M), shared dedicated USDC Umbrella coverage (~$93.3M staked USDC) far exceeds the pool size. | 3 | 9 | **Improvable** | [P2] [DAO Funding Insights](https://governance.aave.com/t/aave-dao-funding-insights/24192), [P2] [LlamaRisk Umbrella Coverage](https://governance.aave.com/t/llamarisk-insights-umbrella-coverage-principles-and-slashing-logic/23527) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. DAO Treasury ~$125M. Protocol generated $885M in fees in 2025, est. ~$143M revenue 2026. $50M/year permanent AAVE buyback approved. Revenue broadly covers expenses. Runway >24 months. | 9 | 9 | Non-Improvable (optimal) | [P2] [DAO Funding Insights](https://governance.aave.com/t/aave-dao-funding-insights/24192), [P3] [Coinlaw Statistics](https://coinlaw.io/aave-statistics/) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | Highly resilient across multiple severe stress events. Survived 2022 bear market, SVB crisis. Feb 2025: $210M liquidations zero bad debt. Feb 2026: record $429M liquidations zero bad debt. Demonstrated resilience across every major market stress over 8+ years. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P3] [DeFiLlama Aave V3](https://defillama.com/protocol/aave-v3) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Smart contracts are permissionless and non-custodial. Base USDC withdrawals always available via direct Pool contract interaction based on available liquidity (subject to Base sequencer availability). Governance via on-chain voting. Multiple independent dev teams provide redundancy. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool Proxy Base](https://basescan.org/address/0xA238Dd80C259a72e81d7e4664a9801593F98d1c5) |

**Financial Resilience Subtotal: 58.5/67.5 (86.7%)**
- 4 questions at score 9 = 36, 1 question at score 3 = 3
- Raw: 39/45, Weighted: (39/45) x 67.5 = 58.5

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 99 | 99 | 180.0 | 180 | 100.0% |
| | Key Management (7 of 8 Q scored) | 57 | 63 | 162.9 | 180 | 90.5% |
| | **Security Subtotal** | | | **342.9** | **360** | **95.2%** |
| **Strategy** | Protocol Mechanics (9 Q) | 75 | 81 | 41.7 | 45 | 92.6% |
| | Collateral (4 Q) | 30 | 36 | 37.5 | 45 | 83.3% |
| | Infra Counterparty (8 Q) | 42 | 72 | 26.25 | 45 | 58.3% |
| | Protocol Counterparty (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity (9 Q) | 69 | 81 | 38.3 | 45 | 85.2% |
| | Market (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | **Strategy Subtotal** | | | **233.75** | **270** | **86.6%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 75 | 81 | 62.5 | 67.5 | 92.6% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 39 | 45 | 58.5 | 67.5 | 86.7% |
| | **Operations Subtotal** | | | **256.0** | **270** | **94.8%** |
| **TOTAL** | | | | **832.65** | **900** | **92.5%** |

---

