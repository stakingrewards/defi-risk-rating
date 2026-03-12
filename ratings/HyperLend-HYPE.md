# HyperLend - HYPE Core Market Risk Rating

**Rating Date**: 2026-02-19
**Final Grade**: CCC
**Total Score**: 548.9/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v1.0-alpha

---

## Detailed Analysis

### Security (40%) - Current: 264.4/360 | Potential: 360.0/360

#### Smart Contract Security (20%) - Current: 147.3/180 | Potential: 180.0/180

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. Three independent security reviews: (1) Cantina competition (Nov 13 - Dec 4, 2024, 45 findings, 399 submissions), (2) Ackee Blockchain (Jan 10 - Feb 7, 2025, 44 findings, 46 engineering days, with fix reviews Feb 17-24 and Mar 12-18, 2025), (3) Pashov Audit Group (two reports: Jan 11, 2025 and Nov 21, 2025). All three cover core fund-custody/routing contracts. | 9 | 9 | Non-Improvable (optimal) | [P1] Cantina report: https://cdn.cantina.xyz/reports/cantina_competition_hyperlend_november2024.pdf; [P1] Ackee summary: https://ackee.xyz/blog/hyperlend-protocol-audit-summary/; [P1] Pashov reports at https://github.com/pashov/audits; [P1] HyperLend audits repo: https://github.com/hyperlendx/audits |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent audit by Pashov Audit Group (Nov 21, 2025), Tier-1. All auditors (Cantina, Ackee, Pashov) are Tier-1. | 9 | 9 | Non-Improvable (optimal) | [P1] SR Auditor Tiers: Cantina Tier-1, Ackee Tier-1, Pashov Tier-1 |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Protocol launched March 2025 with pre-launch audits. Pashov Nov 2025 audit covers post-launch changes. Ackee conducted fix reviews in Feb and Mar 2025. | 9 | 9 | Non-Improvable (optimal) | [P1] Pashov audit dates: Jan 2025 and Nov 2025; [P1] Ackee fix reviews Feb-Mar 2025 |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Ackee audit: 44 findings including 1 critical (C1: collateral theft risk in isolated pools). Fix reviews conducted Feb 17-24 and Mar 12-18, 2025. Cantina: 45 issues including critical liquidation bug. Protocol deployed after reviews. However, no public per-finding remediation tracker with auditor sign-off exists. | 3 | 9 | **Improvable** | [P1] Ackee fix reviews confirmed; [P1] Cantina report available; deployed post-reviews |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Core Pool (0x00A89d7a5A02160f20150EbEA7a2b5E4879A1A8b) is an InitializableImmutableAdminUpgradeabilityProxy (EIP-1967). Upgrades are constrained by a multi-step governance pipeline: Governance Multisig (GnosisSafeProxy at 0x2110...8E9C) → Timelock A (verified OpenZeppelin TimelockController at 0xaAaa...7879) → Executor (0x1a54...b22) → PoolAddressesProvider. Timelock B (0xbbBB...2432) also verified. Delay durations not publicly documented but timelock infrastructure is on-chain and verified. | 9 | 9 | Non-Improvable (optimal) | [P0] Timelock A verified as TimelockController on hyperevmscan.io; [P0] Timelock B verified; [P0] Governance Multisig is GnosisSafeProxy; [P1] Contract addresses docs: https://docs.hyperlend.finance/developer-documentation/contract-addresses |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit on HyperLend. Hyperdrive (different protocol) was exploited; Hyperliquid JELLY/POPCAT incidents affected HLP, not HyperLend. | 9 | 9 | Non-Improvable (optimal) | [P4] No rekt.news entry for HyperLend; [P1] No incident disclosure in docs |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No. Aave DAO recognized HyperLend as friendly fork, providing credibility signal. | 9 | 9 | Non-Improvable (optimal) | [P2] Aave governance recognition; [P4] No allegations found |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No evidence of timelock reductions. | 9 | 9 | Non-Improvable | [P0] No reduction transactions found on-chain |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Self-hosted GitHub bug bounty (github.com/hyperlendx/bug-bounty). Rewards in USDC and vested HPL. Not on Immunefi or other established platform. Max payout unclear. | 3 | 9 | **Improvable** | [P1] GitHub: https://github.com/hyperlendx/bug-bounty; No Immunefi listing found |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. HyperLend's risks documentation page confirms partnership with Hypernative for "real-time monitoring and incident response, mitigating threats before they happen with automated detection and onchain actions." | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.hyperlend.finance/hyperlend-1/risks — "We are also working with Hypernative to provide real-time monitoring and incident response" |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Aave v3 fork includes per-reserve pause via EmergencyAdmin. No automatic triggers documented. EmergencyAdmin configuration unclear. | 3 | 9 | **Improvable** | [P0] Aave v3 pause functionality inherited; [P1] No circuit breaker documentation |

**SC Subtotal**: Raw = 9+9+9+3+9+9+9+9+3+9+3 = 81 out of max 99
**SC Weighted**: (81/99) x 180 = 147.3

#### Key Management & Permissions (20%) - Current: 117.1/180 | Potential: 180.0/180

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Admin and upgrade keys are controlled by verified on-chain multisig and timelock infrastructure. Governance Multisig (GnosisSafeProxy at 0x2110...8E9C, 1,378 transactions) controls protocol changes. EmergencyAdmin Multisig (GnosisSafeProxy at 0xC2A0...7cAc, 316 transactions) handles emergency actions. Treasury Multisig (GnosisSafeProxy at 0xCBF4...d7b) manages treasury. Timelocks A and B (verified TimelockControllers) enforce delay periods. Executor contract (0x1a54...b22) executes governance proposals. All admin addresses are documented at docs.hyperlend.finance/developer-documentation/contract-addresses. Signer threshold and identities not publicly disclosed (see S-KM-03). | 9 | 9 | Non-Improvable (optimal) | [P0] Governance Multisig verified as GnosisSafeProxy on hyperevmscan.io; [P0] EmergencyAdmin verified as GnosisSafeProxy; [P0] Timelocks verified as TimelockControllers; [P1] Contract addresses: https://docs.hyperlend.finance/developer-documentation/contract-addresses |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. All admin and upgrade functions are controlled by verified GnosisSafe multisig contracts with timelock enforcement. The Governance Multisig (0x2110...8E9C, GnosisSafeProxy) controls protocol upgrades via Timelock → Executor pipeline. The EmergencyAdmin (0xC2A0...7cAc) is also a verified GnosisSafeProxy, not an EOA — the initial assessment using Hyperscan (Blockscout API) incorrectly reported it as non-contract; hyperevmscan.io confirms it as a GnosisSafeProxy with 316 transactions. No single key can move user funds or upgrade custody contracts. | 9 | 9 | Non-Improvable (optimal) | [P0] EmergencyAdmin verified as GnosisSafeProxy on hyperevmscan.io (316 txns); [P0] Governance Multisig verified as GnosisSafeProxy (1,378 txns); [P0] Timelock A verified as TimelockController; [P1] Contract addresses docs |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Three verified GnosisSafeProxy multisigs (Governance, EmergencyAdmin, Treasury) control all critical actions. However, signer threshold, signer count, and signer identities are not publicly disclosed. Team claims 4/8 threshold with at least 4 independent parties, but this cannot be independently verified without reading the Safe contract state. | 1 | 9 | **Source Missing** | [P0] All three multisigs verified as GnosisSafeProxy on hyperevmscan.io; threshold and signers not publicly readable; [P1] Team claim: 4/8 threshold (unverified) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Aave v3 pause is per-reserve, protocol-wide (not address-selective). No evidence of address-level blocklisting. Pause constraints and time limits undocumented. | 3 | 9 | **Improvable** | [P0] Aave v3 per-reserve pause inherited; [P1] No pause constraint documentation |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. All assets in Pool contract on HyperEVM. Fully non-custodial. | 9 | 9 | Non-Improvable (optimal) | [P0] Pool contract verified on Hyperscan; [P1] Aave v3 non-custodial by design |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Pool contract and Treasury Safe are separate addresses. Aave v3 architecture segregates by design. | 9 | 9 | Non-Improvable (optimal) | [P0] Different contract addresses; [P1] Aave v3 segregation by design |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A - Lending protocol, not a vault/managed strategy. | N/A | N/A | N/A |  |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No documented incident playbook found. | 1 | 9 | **Improvable** | No evidence in docs, blog, or GitHub |

**KM Subtotal** (excl N/A): Raw = 9+9+1+3+9+9+1 = 41 out of max 63
**KM Weighted**: (41/63) x 180 = 117.1

**Security Total**: 147.3 + 117.1 = **264.4**
**Security Potential**: 180.0 + 180.0 = **360.0**

### Strategy (30%) - Current: 171.7/270 | Potential: 243.4/270

#### Protocol Mechanics (5%) - Current: 31.7/45 | Potential: 41.7/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield from borrower interest payments. 100% organic, fully mandate-aligned. | 9 | ? | Non-Improvable (optimal) | [P1] Docs; [P3] DeFiLlama fees data |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Only in tail-risk scenarios (mass defaults, oracle manipulation, smart contract exploit). Aave v3 liquidation mechanics well-tested. | 9 | ? | Non-Improvable (optimal) |  |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No protocol-level leverage for suppliers. HyperLoop is user-optional. | 9 | ? | Non-Improvable (optimal) |  |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | Standard Aave v3 health factor liquidations. No automated deleveraging beyond that. Relies on external liquidators. HyperLend published a liquidator bot (github.com/hyperlendx/liquidator). | 3 | ? | **Improvable** |  |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent loss events on HyperLend or directly comparable Aave v3 forks on HyperEVM. | 9 | ? | Non-Improvable (optimal) |  |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Risks page exists with qualitative descriptions. No formal quantitative risk framework. | 3 | ? | **Improvable** | [P1] https://docs.hyperlend.finance/hyperlend-1/risks |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Core lending yield is organic. HyperTrack points program adds incentive component. HPL token not live yet, making points speculative. | 3 | ? | **Improvable** |  |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions? | High utilization could delay withdrawals. Standard lending protocol risk. No lock-up. | 3 | ? | Non-Improvable |  |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. Yield from borrower interest only. | 9 | ? | Non-Improvable (optimal) |  |

**PM Subtotal**: 9+9+9+3+9+3+3+3+9 = 57 out of max 81
**PM Weighted**: (57/81) x 45 = 31.7

#### Collateral (5%) - Current: 25.0/45 | Potential: 35.0/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | HYPE (~$7B+ market cap, volatile L1 token without SR rating), stablecoins (USDC, USDT). Conservative LTV ~0.5 for HYPE. | 3 | ? | **Improvable** |  |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | HYPE is native (not pegged). Protocol untested under severe stress. | 3 | ? | Non-Improvable |  |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A - No staking-based collaterals. | N/A | ? | - |  |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | HYPE is native to HyperEVM. Minimal bridged exposure for HYPE market. | 9 | ? | Non-Improvable (optimal) |  |

**C Subtotal** (excl N/A): 3+3+9 = 15 out of max 27
**C Weighted**: (15/27) x 45 = 25.0

#### Infra Counterparty Exposures (5%) - Current: 25.0/45 | Potential: 45.0/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | HyperEVM (Tier-1), Pyth (Tier-0), RedStone (Tier-1), Hyperliquid native oracle. All disclosed. | 9 | ? | Non-Improvable (optimal) |  |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | Multiple oracle providers but primary is Hyperliquid native with custom adapter. Partial fallback. | 3 | ? | **Improvable** |  |
| ST-IC-03 | Are off-chain infrastructure providers certified? | Oracle keeper is off-chain dependency. No certifications disclosed. Protocol largely on-chain. | 3 | ? | **Source Missing** |  |
| ST-IC-04 | How did these infra components behave in past outages? | Protocol deployed <12 months. July 2025 API outage did not affect HyperEVM block production. HyperLend not directly impacted by chain incidents. | 3 | ? | Non-Improvable |  |
| ST-IC-05 | Has the base chain recently halted block production? | No chain halt or consensus failure >30 minutes in last 12 months. | 9 | ? | Non-Improvable (optimal) |  |
| ST-IC-06 | Has the validator set experienced slashing events? | N/A - Lending protocol, not staking. | N/A | ? | - |  |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A - Lending protocol, not staking. | N/A | ? | - |  |
| ST-IC-08 | Can any single infra component failure alone block withdrawals? | Oracle adapter failure could delay price updates; multi-oracle fallback should prevent extended outage. | 3 | ? | **Improvable** |  |

**IC Subtotal** (excl N/A): 9+3+3+3+9+3 = 30 out of max 54
**IC Weighted**: (30/54) x 45 = 25.0

#### Protocol Counterparty Exposures (5%) - Current: 37.5/45 | Potential: 45.0/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols are collateral deployed? | None. Funds held in HyperLend Pool contract only. | 9 | ? | Non-Improvable (optimal) |  |
| ST-PC-02 | Are revenue-share or incentive arrangements documented? | Aave friendly fork arrangement partially disclosed via governance. Oracle provider investors create potential conflict. | 3 | ? | **Improvable** |  |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Aave v3 supply/borrow caps per asset enforced on-chain. | 9 | ? | Non-Improvable (optimal) |  |
| ST-PC-04 | How quickly can positions be unwound from each counterparty? | No external counterparty positions. Instant unwinding via lending protocol. | 9 | ? | Non-Improvable (optimal) |  |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | N/A - Fully on-chain lending protocol. Deal Breaker does NOT trigger. | N/A | ? | - |  |

**PC Subtotal** (excl N/A): 9+3+9+9 = 30 out of max 36
**PC Weighted**: (30/36) x 45 = 37.5

#### Liquidity (5%) - Current: 25.0/45 | Potential: 31.7/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused? | On-chain permissionless via Pool withdraw(). EmergencyAdmin can pause per-reserve. Admin configuration unclear. | 3 | ? | **Improvable** |  |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL? | Dependent on utilization. Standard lending protocol constraint. | 3 | ? | Non-Improvable |  |
| ST-L-03 | Have there been past withdrawal delays? | No reported delays. Protocol <12 months old, untested under stress. | 3 | ? | Non-Improvable |  |
| ST-L-04 | Do caps restrict timely redemptions? | Caps limit deposits not withdrawals. Interest rate model encourages repayment. | 9 | ? | Non-Improvable (optimal) |  |
| ST-L-05 | How does exit liquidity behave during volatility? | Untested under severe stress. Protocol too new for proven resilience. | 3 | ? | Non-Improvable |  |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits? | No. Instant withdrawal subject to utilization. HYPE is native. | 9 | ? | Non-Improvable (optimal) |  |
| ST-L-07 | Does redemption depend on secondary-market liquidity? | No. In-protocol withdrawal via repayment. Secondary market optional and deep. | 9 | ? | Non-Improvable (optimal) |  |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | HYPE has deep liquidity. hToken receipt tokens have no secondary market. | 3 | ? | Non-Improvable |  |
| ST-L-09 | What is the risk of bank-run scenarios? | At full utilization, no withdrawals until repayment. Standard lending risk. Untested. | 3 | ? | Non-Improvable |  |

**L Subtotal**: 3+3+3+9+3+9+9+3+3 = 45 out of max 81
**L Weighted**: (45/81) x 45 = 25.0

#### Market (5%) - Current: 27.5/45 | Potential: 45.0/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed? | N/A - hTokens are non-transferable accounting tokens, not traded on secondary markets. | N/A | ? | - |  |
| ST-M-02 | How likely can adverse market moves cause permanent losses? | Suppliers have no direct directional exposure. Bad debt only in extreme tail scenarios with LTV ~0.5 providing large buffer. | 9 | ? | Non-Improvable (optimal) |  |
| ST-M-03 | Are interest rate models robust during TVL shifts? | Aave v3 utilization model inherited. Untested under extreme conditions on HyperLend. | 3 | ? | Non-Improvable |  |
| ST-M-04 | Have historic scenarios with high volatility been modeled? | No public stress testing documentation for HyperLend HYPE market. | 1 | ? | **Improvable** |  |
| ST-M-05 | Can sharp price moves trigger forced liquidations? | Conservative LTV ~0.5 provides large buffer. No protocol-level leverage for suppliers. | 9 | ? | Non-Improvable (optimal) |  |

**M Subtotal** (excl N/A): 9+3+1+9 = 22 out of max 36
**M Weighted**: (22/36) x 45 = 27.5

**Strategy Total**: 31.7 + 25.0 + 25.0 + 37.5 + 25.0 + 27.5 = **171.7**
**Strategy Potential**: 41.7 + 35.0 + 45.0 + 45.0 + 31.7 + 45.0 = **243.4**

### Operations (30%) - Current: 112.8/270 | Potential: 261.0/270

#### Governance (7.5%) - Current: 22.5/67.5 | Potential: 67.5/67.5

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes? | Structured on-chain governance pipeline: Governance Multisig (GnosisSafeProxy) → Timelock (verified TimelockController) → Executor → Protocol. However, HPL governance token not yet live — decision-making is centralized in team-controlled multisig, not token-based DAO voting. | 3 | ? | **Improvable** |  |
| O-G-02 | How concentrated is voting power? | N/A - No governance token live. | N/A | ? | - |  |
| O-G-03 | Are timelocks and veto mechanisms in place? | Yes. Timelock A (verified OpenZeppelin TimelockController) and Timelock B (verified) enforce delay periods on governance actions. Delay durations not publicly documented. No formal veto mechanism. | 3 | ? | **Improvable** |  |
| O-G-04 | Can the protocol replace the strategy manager without blocking withdrawals? | Technically possible via Aave v3 architecture. Not documented or tested. | 3 | ? | **Improvable** |  |

**G Subtotal** (excl N/A): 3+3+3 = 9 out of max 27
**G Weighted**: (9/27) x 67.5 = 22.5

#### Team & Legal (7.5%) - Current: 26.8/67.5 | Potential: 67.5/67.5

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified? | Partially identified: B.S. (CEO, @0xNessus), F.B. (CTO, @fbsloXBT, 8yr blockchain experience). HyperLabs Inc. Pseudonymous with limited verifiable background. | 3 | ? | **Improvable** |  |
| O-TL-02 | Is the protocol dependent on a single developer? | ~5 FT, <3 active code contributors. CTO key-person risk. | 3 | ? | **Improvable** |  |
| O-TL-03 | What legal entity and jurisdiction operate the protocol? | HyperLabs Inc (per Cantina listing). Jurisdiction not disclosed. | 3 | ? | **Improvable** |  |
| O-TL-04 | Are there known investigations or regulatory actions? | None found. | 9 | ? | Non-Improvable (optimal) |  |
| O-TL-05 | Is there an on-call and incident response process? | No documented on-call or incident response process. | 1 | ? | **Improvable** |  |
| O-TL-06 | Does the team provide timely support? | Discord and Twitter present. Informal support, no SLAs. | 3 | ? | **Improvable** |  |
| O-TL-07 | Are major investors disclosed? | Investors partially disclosed (RockawayX, Dewhales, etc., $1.7M). Rights and influence not clear. | 3 | ? | **Improvable** |  |
| O-TL-08 | Does the strategy manager manage similar vaults? | N/A - Lending protocol. | N/A | ? | - |  |
| O-TL-09 | Has the strategy manager been involved in products with collateral loss? | N/A - Lending protocol. | N/A | ? | - |  |

**TL Subtotal** (excl N/A): 3+3+3+9+1+3+3 = 25 out of max 63
**TL Weighted**: (25/63) x 67.5 = 26.8

#### Documentation & Transparency (7.5%) - Current: 35.0/67.5 | Potential: 67.5/67.5

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation? | Comprehensive docs at docs.hyperlend.finance covering architecture, risks, oracle, liquidation, developer docs. | 9 | ? | Non-Improvable (optimal) | [P1] https://docs.hyperlend.finance |
| O-DT-02 | Is collateral use and loss conditions documented? | High-level descriptions. No systematic loss scenario mapping. | 3 | ? | **Improvable** |  |
| O-DT-03 | Are all contract addresses documented in one place? | Yes, at docs.hyperlend.finance/developer-documentation/contract-addresses. | 9 | ? | Non-Improvable (optimal) |  |
| O-DT-04 | Are roles, permissions and timelocks documented? | ACLManager listed but role assignments, timelock durations, and change history not documented. | 1 | ? | **Improvable** |  |
| O-DT-05 | Does the protocol publish proof-of-reserves? | On-chain transparency inherent to lending protocol. No formal PoR publication. DeFiLlama tracks TVL. Proof-of-liabilities also on-chain visible. | 3 | ? | **Improvable** |  |
| O-DT-06 | Are all contracts verified on block explorers? | Most core contracts verified (Pool, PoolAddressesProvider, Treasury Safe, Timelock B). ACLManager not verified. Some gaps. | 3 | ? | **Improvable** |  |

**DT Subtotal**: 9+3+9+1+3+3 = 28 out of max 54
**DT Weighted**: (28/54) x 67.5 = 35.0

#### Financial Resilience (7.5%) - Current: 28.5/67.5 | Potential: 58.5/67.5

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module? | Insurance fund receives portion of interest/liquidation bonuses. No published activation rules or size. | 3 | ? | **Improvable** |  |
| O-FR-02 | How large and liquid are backstop reserves? | Treasury balance and composition not disclosed. $1.7M raised. Cannot assess adequacy. | 1 | ? | **Source Missing** |  |
| O-FR-03 | What is the estimated operational runway? | $1.7M raised, ~5 FT team, protocol revenue undisclosed. Runway uncertain. | 3 | ? | **Source Missing** |  |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress? | Untested under stress. Steady growth since March 2025. | 3 | ? | Non-Improvable |  |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Aave v3 architecture self-sustaining. Permissionless withdrawals. Oracle updates from Pyth/RedStone would continue. | 9 | ? | Non-Improvable (optimal) |  |

**FR Subtotal**: 3+1+3+3+9 = 19 out of max 45
**FR Weighted**: (19/45) x 67.5 = 28.5

**Operations Total**: 22.5 + 26.8 + 35.0 + 28.5 = **112.8**
**Operations Potential**: 67.5 + 67.5 + 67.5 + 58.5 = **261.0**

## Final Score Calculation

| Category | Subcategory | Current Points | Max Points | Potential Points |
|----------|-------------|----------------|------------|------------------|
| **Security** | Smart Contract Security | 147.3 | 180 | 180.0 |
| | Key Management | 117.1 | 180 | 180.0 |
| | **Security Subtotal** | **264.4** | **360** | **360.0** |
| **Strategy** | Protocol Mechanics | 31.7 | 45 | 41.7 |
| | Collateral | 25.0 | 45 | 35.0 |
| | Infra Counterparty | 25.0 | 45 | 45.0 |
| | Protocol Counterparty | 37.5 | 45 | 45.0 |
| | Liquidity | 25.0 | 45 | 31.7 |
| | Market | 27.5 | 45 | 45.0 |
| | **Strategy Subtotal** | **171.7** | **270** | **243.4** |
| **Operations** | Governance | 22.5 | 67.5 | 67.5 |
| | Team & Legal | 26.8 | 67.5 | 67.5 |
| | Documentation | 35.0 | 67.5 | 67.5 |
| | Financial Resilience | 28.5 | 67.5 | 58.5 |
| | **Operations Subtotal** | **112.8** | **270** | **261.0** |
| **TOTAL** | | **548.9** | **900** | **864.4** |

---
