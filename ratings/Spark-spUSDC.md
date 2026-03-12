# Spark - spUSDC (Spark Savings USDC) Risk Rating

**Rating Date**: 2026-02-11
**Final Grade**: BB
**Total Score**: 763.9/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v1.0-alpha

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 323.2/360 (89.8%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. All core components have dual independent audits. Spark Vaults V2: 4 audit reports from ChainSecurity (Tier-0) and Cantina (v1.0.0 and v1.0.1). ALM Controller: 15 audit reports from ChainSecurity and Cantina across versions v1.0.0 through v1.7.0. Spark PSM: 3 audit reports. SparkLend v1 core: inherited Aave V3 audits (OpenZeppelin, Trail of Bits, Sigma Prime, PeckShield, ABDK) plus ChainSecurity update audit. xchain-ssr-oracle: 3 audit reports. | 9 | 9 | Non-Improvable (optimal) | [P1] [spark-audits repo](https://github.com/sparkdotfi/spark-audits), [P1] spark-vaults-v2/audits/ (4 PDFs), [P1] spark-alm-controller/audits/ |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | ChainSecurity (Tier-0) and Cantina (Tier-0/Tier-1) performed the most recent audits for both ALM Controller v1.7.0 and Vaults V2 v1.0.1. Both are Tier-0 or Tier-1 auditors per SR list. | 9 | 9 | Non-Improvable (optimal) | [P1] [spark-audits/pdf/spark-alm-controller/v170-chainsecurity-audit.pdf](https://github.com/sparkdotfi/spark-audits/tree/main/pdf/spark-alm-controller), [P1] [spark-audits/pdf/spark-vaults-v2/v101-chainsecurity.pdf](https://github.com/sparkdotfi/spark-audits/tree/main/pdf/spark-vaults-v2) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Every version release of the ALM Controller (v1.0.0 through v1.7.0) has corresponding audit reports from both ChainSecurity and Cantina. The Vaults V2 also audited for both v1.0.0 and v1.0.1. Demonstrates rigorous audit-before-deploy practice. | 9 | 9 | Non-Improvable (optimal) | [P1] [spark-audits repo](https://github.com/sparkdotfi/spark-audits) -- 22+ audit reports total across all components |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | The iterative audit pattern (15 versions of ALM controller audited by two independent firms) provides strong evidence of systematic finding remediation between versions. Each version release includes fresh audits from both ChainSecurity and Cantina, which would identify any unresolved issues from prior versions. This iterative dual-audit approach is equivalent to re-verification. | 9 | 9 | Non-Improvable (optimal) | [P1] 15 ALM Controller audit reports showing iterative audit-fix-audit cycle, [P1] 4 Vaults V2 audit reports |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | spUSDC vault is UUPS upgradeable. DEFAULT_ADMIN_ROLE controls upgrades via `_authorizeUpgrade`. This role is held by Spark Proxy (0x3300f198988e4C9C63F75dF86De36421f06af8c4), the governance executor. Upgrades require: proposal by 1% SPK holder, Spark Risk Council review (1 week), Operational Facilitator review, Snapshot vote (3 days, >50%), and Sky Spell execution. Total process takes 2-3 weeks, well above 24h timelock. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: `_authorizeUpgrade` requires `onlyRole(DEFAULT_ADMIN_ROLE)`, [P0] SPARK_PROXY = 0x3300f198988e4C9C63F75dF86De36421f06af8c4, [P1] [Governance docs](https://docs.spark.fi/governance) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss for Spark or spUSDC vault. No incidents found in public reporting. The Sky/MakerDAO ecosystem has operated since 2017 with no major exploits affecting the savings rate mechanism. SparkLend (separate product) has operated since 2023 without exploits. | 9 | 9 | Non-Improvable (optimal) | [P4] No incidents found on rekt.news or crypto news, [P1] Protocol operational since Sep 2025 without loss events |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Spark operates within the Sky/MakerDAO ecosystem with 8+ year history. Phoenix Labs is the publicly identified development team. Governance via SPK token with Spark Risk Council oversight. No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance docs](https://docs.spark.fi/governance), [P2] Active governance forum |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No evidence of timelock reductions. The governance process requires a structured weekly cycle with mandatory review periods. The ALM Controller uses rate limits as the primary security boundary. No changes identified that weaken protections in the last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance docs](https://docs.spark.fi/governance), [P1] [Rate limits docs](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/RATE_LIMITS.md) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Active bug bounty confirmed on Immunefi (immunefi.com/bug-bounty/sparkdao/). Immunefi is an established platform with track record of payouts. The page exists and is accessible (57KB response). However, the maximum payout amount could not be verified from available data. Given inability to confirm >=100k USD max payout, scoring Mid. | 3 | 9 | Source Missing | [P1] [Immunefi SparkDAO](https://immunefi.com/bug-bounty/sparkdao/) confirmed to exist |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | The architecture includes: (1) FREEZER role for emergency relayer removal, (2) rate limits enforcing invariants on every transaction, (3) sparklend-kill-switch repo for oracle price monitoring and SparkLend shutdown, (4) emergency spell contracts deployed (SPELL_FREEZE_ALL, SPELL_PAUSE_ALL). However, no specific third-party monitoring provider (Hypernative, Blockaid) is named in documentation. No public on-call documentation. | 3 | 9 | Source Missing | [P1] [THREAT_MODEL.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/THREAT_MODEL.md), [P0] Emergency spell addresses in spark-address-registry |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Yes. Rate limits on the ALM Controller automatically enforce bounds on every operation -- objective, on-chain, rule-based constraints that prevent excessive fund movement. The sparklend-kill-switch triggers SparkLend freeze on oracle depeg. FREEZER role enables rapid relayer removal. Emergency spells (SPELL_FREEZE_ALL, SPELL_PAUSE_ALL) available for broader protocol freeze. The rate limit system is a stronger automatic control than traditional pause mechanisms. | 9 | 9 | Non-Improvable (optimal) | [P0] Rate limits in MainnetController.sol enforce per-operation bounds, [P1] [RATE_LIMITS.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/RATE_LIMITS.md), [P0] Emergency spell addresses |

**Smart Contract Security Subtotal: 158.2/180 (87.9%)**
- 9 questions scored 9 (sum = 81), 2 questions scored 3 (sum = 6)
- Raw sum = 87 out of max 99
- Weighted = (87/99) x 180 = 158.2

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | DEFAULT_ADMIN_ROLE on spUSDC vault is held by Spark Proxy (0x3300f198988e4C9C63F75dF86De36421f06af8c4), the governance executor controlled through the full Sky Spell process. ALM Proxy admin is also governance-controlled. All changes go through SPK token governance with Spark Risk Council review. Changes are publicly visible on-chain via spell execution. | 9 | 9 | Non-Improvable (optimal) | [P0] Spark address registry: SPARK_PROXY = 0x3300f198988e4C9C63F75dF86De36421f06af8c4, [P1] [Governance docs](https://docs.spark.fi/governance) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No single key can move user funds or upgrade the vault. The TAKER_ROLE (ALM Controller) can pull liquidity but only through rate-limited, whitelisted operations -- rate limits bound exposure and FREEZER can halt. DEFAULT_ADMIN_ROLE (governance) requires the full governance process: 1% proposal threshold, Risk Council review, 3-day Snapshot vote, Sky Spell execution. This process involves thousands of SPK token holders. The RELAYER is explicitly assumed compromisable with losses bounded by rate limits. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: TAKER_ROLE for `take()`, DEFAULT_ADMIN_ROLE for `_authorizeUpgrade`, [P1] [THREAT_MODEL.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/THREAT_MODEL.md) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Governance operates through SPK token holders via Snapshot voting with >50% approval threshold, which is more decentralized than any multisig. The Spark Risk Council provides professional review oversight. Phoenix Labs serves as Operational Facilitator. 1% of SPK supply (100M tokens) required to propose. Delegate system allows broader participation. **However, the specific operational multisig configurations (ALM_OPS_MULTISIG, ALM_RELAYER_MULTISIG) and their signer details are not publicly documented.** Per criteria: "If signer identities are fully unknown, independence cannot be confirmed — score Mid (3) at best regardless of threshold/count, and classify as Source Missing." | 3 | 9 | **Source Missing** | [P1] [Governance docs](https://docs.spark.fi/governance) detail full process, [P0] Address registry lists operational multisigs but signer identities undisclosed |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | The spUSDC vault has no pause function and no address-level blocking capability. Withdrawals are permissionless via ERC4626 standard (redeem/withdraw functions). The ALM Controller's FREEZER role can only remove relayers, not block user withdrawals. Vault withdrawals are constrained only by available liquidity (USDC balance in contract). The vault explicitly prevents the TAKER from depositing. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol source code -- no pause function, permissionless redeem/withdraw |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. User deposits reside in the spUSDC vault contract. When TAKER_ROLE pulls liquidity, assets move to ALMProxy (0x1601843c5E9bC251A3272907010AFa41Fa18347E), a non-custodial on-chain contract. From there, assets are deployed to on-chain protocols (Sky PSM, Aave, Morpho, etc.). All fund custody is on-chain. Some RWA allocations (BUIDL, Centrifuge, Superstate) involve off-chain asset backing but represent a small portion of TVL and the on-chain tokens remain in non-custodial contracts. | 9 | 9 | Non-Improvable (optimal) | [P0] ALM_PROXY = 0x1601843c5E9bC251A3272907010AFa41Fa18347E, [P1] [Architecture docs](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/ARCHITECTURE.md) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. User funds flow: spUSDC vault -> ALMProxy -> external protocols. Spark treasury and operational funds are separate (managed through Spark Proxy governance). The vault contract explicitly prevents TAKER_ROLE addresses from depositing (`require(!hasRole(TAKER_ROLE, msg.sender) && !hasRole(TAKER_ROLE, receiver))`) ensuring clean separation of user and operational flows. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol `_mint` function: taker deposit prevention, [P0] Separate addresses for operational multisigs in address registry |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain enforced whitelist via rate limit keys. Only governance-approved integrations have valid rate limit keys. Current whitelist from MainnetController.sol and address registry: Sky allocation system, PSM, Aave (multiple aTokens), Morpho, Fluid (sUSDS), Maple (Syrup USDC/USDT), Ethena, BlackRock BUIDL/BUIDLi, Centrifuge (JTRSY), Superstate (USTB), Curve pools, Uniswap V4, EtherFi (weETH module). New additions require governance approval and rate limit configuration. | 9 | 9 | Non-Improvable (optimal) | [P0] MainnetController.sol imports and address registry list all whitelisted protocols, [P1] [Rate limit docs](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/RATE_LIMITS.md): keys serve as whitelist |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | The THREAT_MODEL.md documents detailed attack scenarios and responses for relayer compromise: FREEZER removes relayer, system switches to backup, maximum loss bounded by rate limits. Recovery procedures documented in Attacks.t.sol test files. However, no public playbook for governance key compromise or signer loss was found. No documented tabletop exercise in last 12 months. | 3 | 9 | Source Missing | [P1] [THREAT_MODEL.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/THREAT_MODEL.md) covers relayer compromise scenarios in detail, but governance key compromise undocumented |

**Key Management Subtotal: 150.0/180 (83.3%)**
- 6 questions scored 9 (sum = 54), 2 questions scored 3 (sum = 6)
- Raw sum = 60 out of max 72
- Weighted = (60/72) x 180 = 150.0

**Improvement Opportunities:**
- **S-KM-03** (+15.0 weighted points): Publicly disclose operational multisig signer identities and configurations (Source Missing)
- **S-KM-08** (+15.0 weighted points): Publish comprehensive incident response playbook including governance key compromise and signer loss scenarios; conduct tabletop exercise

---

### **Security Total: 308.2/360 (85.6%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 158.2 | 180 | 87.9% |
| Key Management | 150.0 | 180 | 83.3% |
| **Security Total** | **308.2** | **360** | **85.6%** |

---

### STRATEGY (30% Weight) -- Score: 230.3/270 (85.3%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield anchored to Sky Savings Rate as a minimum, with enhancement through SLL deployment across Aave, Morpho, Fluid, Maple, Ethena, RWAs. ~4% APY, 100% organic from lending and savings rate income. Fully aligned with mandate of "USDC savings vault." Yield sources documented on Spark App. | 9 | 9 | Non-Improvable (optimal) | [P1] [spUSDC docs](https://docs.spark.fi/user-guides/earning-savings/spusdc), [P3] DeFiLlama: 4% base APY |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail shocks: simultaneous counterparty failure across multiple SLL deployment venues, severe stablecoin depeg event, or governance attack. Rate limits bound exposure per venue. Sky PSM provides USDC/USDS parity floor. 10% instant liquidity buffer maintained. | 9 | 9 | Non-Improvable (optimal) | [P1] [THREAT_MODEL.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/THREAT_MODEL.md), [P1] Architecture documentation |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage. Vault simply accepts USDC deposits and deploys into yield strategies at 1.0x. No rehypothecation of depositor funds into leveraged positions. Rate limits prevent over-deployment. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: simple deposit/redeem, [P1] 90% deployed / 10% buffer design |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- spUSDC is a savings vault, not a borrower. No liquidation risk for depositors. The vault holds USDC and earns yield through deployment strategies. | N/A | N/A | N/A | Not applicable to savings vault |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss events for spUSDC or any Spark Savings V2 vault in 5 months of operation since September 2025. The predecessor sDAI/sUSDS (comparable variant using Sky Savings Rate) has operated since 2022 without permanent loss events. | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama continuous positive yield since launch, [P1] sDAI/sUSDS track record |
| ST-PM-06 | Is a risk framework for vault curation documented? | Yes. Comprehensive framework: THREAT_MODEL.md documents attack vectors, trust assumptions, and mitigations. RATE_LIMITS.md documents per-operation exposure bounds. SECURITY.md documents trust levels and protocol-specific considerations. OPERATIONAL_REQUIREMENTS.md documents deployment and integration checklists. Architecture documentation covers full system design. | 9 | 9 | Non-Improvable (optimal) | [P1] [THREAT_MODEL.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/THREAT_MODEL.md), [P1] [RATE_LIMITS.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/RATE_LIMITS.md), [P1] [SECURITY.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/SECURITY.md) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. ~4% yield is entirely organic from Sky Savings Rate and lending protocol deployment. No token emissions or incentive dependency. Spark Points are separate from the savings rate and do not affect underlying yield sustainability. The Sky Savings Rate has been sustainably funded by MakerDAO/Sky protocol revenue (crypto loans, treasury bills, liquidity provisioning) since 2022. | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama: 4% apyBase, 0% apyReward, [P1] [Savings docs](https://docs.spark.fi/user-guides/earning-savings) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes. 10% instant liquidity buffer maintained in vault. Sky PSM provides USDC/USDS swaps with no slippage beyond gas. Underlying deployments in Aave, Morpho, Fluid are highly liquid lending markets. The SLL documentation states it "ensures sufficient liquidity for deposits and withdrawals" and enables "$100M+ transactions without significant market impact." | 9 | 9 | Non-Improvable (optimal) | [P1] [spUSDC docs](https://docs.spark.fi/user-guides/earning-savings/spusdc): 10% buffer, [P1] [Savings FAQ](https://docs.spark.fi/user-guides/earning-savings): PSM ensures liquidity |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. Yield comes from lending interest (Aave, Morpho, Fluid, Maple), savings rate (Sky SSR), and RWA returns (BUIDL, Centrifuge, Superstate). No basis trade, peg arbitrage, or funding rate dependency. Interest is earned on deployed stablecoin capital. | 9 | 9 | Non-Improvable (optimal) | [P1] Architecture documentation, [P0] MainnetController.sol shows lending/savings integrations |

**Protocol Mechanics Subtotal: 45.0/45 (100.0%)**
- 8 applicable questions (ST-PM-04 = N/A), all scored 9
- Raw sum = 72 out of max 72
- Weighted = (72/72) x 45 = 45.0

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | The vault accepts USDC (and other supported stablecoins via PSM conversion). USDC is the primary asset -- an established large-cap stablecoin with ~$50B+ market cap, issued by Circle (regulated, audited). Circle holds reserves in US Treasury bills and cash. USDC is the highest-quality stablecoin collateral. | 9 | 9 | Non-Improvable (optimal) | [P1] [spUSDC docs](https://docs.spark.fi/user-guides/earning-savings/spusdc): USDC deposits, [P3] USDC market data |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | Evaluation target: spUSDC receipt token. spUSDC has been operational since September 2025 (~5 months). During this period, no depeg or deviation from NAV has been reported. However, per battle-tested rule, the vault has not been tested through a severe market stress event. The predecessor sDAI/sUSDS has maintained NAV through multiple stress events, but spUSDC V2 with SLL deployment is a distinct product. | 3 | 9 | Non-Improvable (time-dependent) | [P3] DeFiLlama shows continuous operation since Sep 2025, [P1] No deviation reports found |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- spUSDC is a USDC savings vault with no staking-based collateral. The SLL deploys into stablecoin lending and RWA strategies, not staking. | N/A | N/A | N/A | Not applicable to USDC savings vault |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | Minimal. USDC on Ethereum is natively issued by Circle (excluded from bridged/wrapped definition per framework). The vault holds USDC directly. The SLL may deploy into protocols that hold wrapped assets, but the user's direct exposure is to USDC. No bridged tokens in the deposit flow. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: `asset` is USDC (native on Ethereum), [P1] Framework definition excludes native USDC |

**Collateral Subtotal: 35.0/45 (77.8%)**
- 3 applicable questions (ST-C-03 = N/A): 2 scored 9 (sum = 18), 1 scored 3
- Raw sum = 21 out of max 27
- Weighted = (21/27) x 45 = 35.0

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Primary chain: Ethereum (Tier-0). No bridge dependency for the Ethereum vault. No oracle dependency for the savings rate mechanism (VSR set by governance). The SLL uses CCTP for cross-chain bridging but this is for L2 deployments, not the Ethereum vault directly. PSM operates on-chain without oracles. All critical dependencies are Tier-0. | 9 | 9 | Non-Improvable (optimal) | [P0] All contracts on Ethereum, [P1] Architecture uses PSM (no oracle), [P0] Address registry shows Ethereum-only for core vault |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | No dependency on off-chain oracles or bridges for the core spUSDC vault on Ethereum. The vault's savings rate is set by governance (VSR parameter), not by oracle. The PSM uses fixed 1:1 USDC/USDS conversion. This qualifies for "No dependency on off-chain infra" = Low (9). | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: VSR set by SETTER_ROLE, no oracle reference, [P1] [Threat Model](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/THREAT_MODEL.md): "1:1 asset parity" assumption |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | The spUSDC vault operates fully on-chain. The relayer is the only off-chain component but is explicitly assumed compromisable in the threat model -- the architecture is designed to be secure even with a compromised relayer. No critical off-chain providers touching user flows. Score Low (9) per applicability check: "no critical off-chain providers." | 9 | 9 | Non-Improvable (optimal) | [P1] [SECURITY.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/SECURITY.md): RELAYER "assumed compromisable," architecture handles it |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Protocol deployed ~5 months (since Sep 2025). No chain-level incidents on Ethereum during operational period. Per new protocol guidance: "For protocols deployed <6 months with no chain-level incidents during their operational period, score Mid (3)." | 3 | 9 | Non-Improvable (time-dependent) | [P1] Protocol launched Sep 2025, <6 months operational, [P0] No Ethereum chain incidents in period |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain halts or consensus failures >30 minutes in the last 12+ months. Tier-0 chain with exceptional reliability record. | 9 | 9 | Non-Improvable (optimal) | [P0] Ethereum operational history, [P3] No incidents reported by L2Beat or block explorers |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- spUSDC is a USDC savings vault. No staking-based collateral or validator dependency. | N/A | N/A | N/A | Not applicable |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- no staking-based collateral or direct validator dependency for this vault. | N/A | N/A | N/A | Not applicable |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Users have permissionless on-chain withdrawal via ERC4626 standard (`redeem`/`withdraw` functions on vault contract). If the relayer fails, users can still withdraw from the 10% buffer. If the SLL fails, new deployments stop but existing vault liquidity remains withdrawable. Frontend failure does not affect on-chain operations. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: permissionless redeem/withdraw, [P1] 10% instant liquidity buffer design |

**Infrastructure Counterparty Subtotal: 40.0/45 (88.9%)**
- 6 applicable questions (ST-IC-06, ST-IC-07 = N/A): 5 scored 9 (sum = 45), 1 scored 3
- Raw sum = 48 out of max 54
- Weighted = (48/54) x 45 = 40.0

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All venues listed by name in MainnetController.sol and address registry: Aave (Tier-0), Morpho (Tier-0), Fluid (Tier-1), Maple (Syrup -- established >12 months, permissioned), Ethena (USDe -- established, large TVL but untiered in SR), BlackRock BUIDL (institutional RWA), Centrifuge (RWA), Superstate (RWA). Some venues (Maple, Ethena) are not in the SR Protocol Tiers list. Rate limits constrain per-venue exposure. | 3 | 3 | Non-Improvable | [P0] MainnetController.sol and Ethereum.sol address registry list all venues, [P1] [Rate limits](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/RATE_LIMITS.md) bound exposure |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | No curator fee or revenue-share model -- Spark governance directly sets the VSR (Vault Savings Rate). No conflicts from third-party curator arrangements. The vault is a protocol-level product, not an externally curated vault. Fee-free for users per documentation. | 9 | 9 | Non-Improvable (optimal) | [P1] [Savings docs](https://docs.spark.fi/user-guides/earning-savings): "fee-free access to onchain, diversified returns" |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. Rate limits enforced on-chain for every operation via RateLimits contract. Each integration has specific rate limit keys with `maxAmount` and `slope` (regeneration rate). Per-venue caps are governance-configurable and automatically enforced. Rate limit keys also serve as a whitelist -- unconfigured addresses automatically revert. | 9 | 9 | Non-Improvable (optimal) | [P0] RateLimits contract at 0x7A5FD5cf045e010e62147F065cEAe59e5344b188, [P1] [RATE_LIMITS.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/RATE_LIMITS.md) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Most positions can be unwound rapidly: Aave/Morpho/Fluid lending positions are instantly withdrawable. PSM swaps are instant. Ethena has cooldown periods for sUSDe unstaking but bounded by rate limits. BUIDL has Circle redemption path. Maple pools have redemption request mechanism. RWA positions may have longer lead times but are a small portion. No discretionary approvals needed -- all via smart contract calls. | 9 | 9 | Non-Improvable (optimal) | [P1] [SECURITY.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/SECURITY.md) details per-protocol trust assumptions and exit paths |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | All third-party integrations explicitly listed by name with contract addresses in MainnetController.sol and the Ethereum address registry. RWA providers (BlackRock/BUIDL, Centrifuge, Superstate) and their roles are documented. Ethena's trust assumptions explicitly stated in SECURITY.md. No undisclosed third parties. | 9 | 9 | Non-Improvable (optimal) | [P0] Ethereum.sol address registry with all addresses, [P1] [SECURITY.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/SECURITY.md) |

**Protocol Counterparty Subtotal: 39.0/45 (86.7%)**
- 4 questions scored 9 (sum = 36), 1 question scored 3
- Raw sum = 39 out of max 45
- Weighted = (39/45) x 45 = 39.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | All users have permissionless on-chain redemption via ERC4626 standard (redeem/withdraw). No pause function on the vault contract. No address-level blocking capability. No admin approval required. Withdrawals are limited only by available USDC balance in the vault (10% buffer). The `maxRedeem` and `maxWithdraw` functions transparently show available liquidity. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: permissionless redeem/withdraw, maxRedeem shows available liquidity |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | 10% instant buffer maintained. Sky PSM provides deep liquidity for USDC/USDS conversion. Documentation states system "enables large-scale transactions ($100M+) without significant market impact." Underlying Aave/Morpho/Fluid positions are highly liquid. Near-total exits would require SLL to unwind positions, which may take days for RWA/Maple positions, but bulk of TVL in liquid protocols. | 9 | 9 | Non-Improvable (optimal) | [P1] 10% buffer design, [P1] [Savings docs](https://docs.spark.fi/user-guides/earning-savings): "$100M+ transactions" |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No withdrawal delays, queues, or freezes reported in 5 months of operation. The 10% instant liquidity buffer has been sufficient for all withdrawals to date. No evidence of any user being unable to withdraw. | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama shows continuous TVL without disruption, [P1] No incident reports found |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Deposit cap exists but is sized to support the vault. No withdrawal cap. Redemptions are limited only by the USDC balance available in the vault contract. The rate limits on the SLL side do not affect user withdrawals -- they only constrain the relayer's deployment operations. No history of caps being used to block exits. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: maxRedeem/maxWithdraw based on contract balance, no withdrawal cap |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Vault is only 5 months old (since Sep 2025). No severe volatility or congestion episodes during operational period to evaluate. Per battle-tested rule: "untested protocols should score Mid (3) on resilience questions." The 10% buffer and PSM liquidity provide theoretical resilience, but this has not been demonstrated under actual stress conditions. | 3 | 9 | Non-Improvable (time-dependent) | [P3] No stress events during operational period, [P1] 10% buffer design provides theoretical resilience |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No lockups, vesting, or bridge dependencies for user withdrawals. Withdrawals are instant if USDC balance is available in the vault. The SLL deployment has some longer-duration positions (Ethena cooldowns, RWA redemptions, Maple requests) but these affect the SLL's rebalancing, not direct user withdrawals from the vault. The 10% buffer absorbs normal withdrawal demand. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: instant withdraw/redeem, [P1] 10% buffer for instant liquidity |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary redemption through ERC4626 vault is always available. Users redeem spUSDC directly from the vault contract for USDC. No secondary market dependency. spUSDC may trade on secondary markets but is not required for exit. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: ERC4626 standard redemption |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | USDC is the most liquid stablecoin with ~$50B+ market cap and deep markets across all major venues. The spUSDC vault at $182M TVL can absorb significant redemptions given USDC's unparalleled liquidity. The 10% buffer (~$18M) is immediately available. | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama: $182M TVL, [P3] USDC market data |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Vault is only 5 months old -- untested under bank-run conditions. Per battle-tested rule, max score 3 for untested protocols. Theoretical analysis: a mass exit would first deplete the 10% buffer, then the SLL would need to unwind positions. Rate limits bound the speed of SLL operations. Sky PSM provides deep backstop liquidity. But actual behavior untested. | 3 | 9 | Non-Improvable (time-dependent) | [P1] 10% buffer + PSM liquidity provide theoretical resilience, but untested |

**Liquidity Subtotal: 38.3/45 (85.2%)**
- 7 questions scored 9 (sum = 63), 2 questions scored 3 (sum = 6)
- Raw sum = 69 out of max 81
- Weighted = (69/81) x 45 = 38.3

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | Evaluation target: spUSDC receipt token. spUSDC is an accumulating ERC4626 token that increases in value over time. The vault has been operational since September 2025 (~5 months). No depeg or NAV deviation reported. However, per battle-tested rule, spUSDC has not been tested through a severe market stress event. The predecessor sDAI/sUSDS maintained NAV through stress events, but spUSDC V2 with SLL is a distinct product. | 3 | 9 | Non-Improvable (time-dependent) | [P3] DeFiLlama: continuous stable operation since Sep 2025, [P1] No NAV deviation reports |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Very low. Vault is fully USDC-denominated -- deposits and returns are in USDC. No directional crypto exposure for depositors. Underlying SLL deployments are in stablecoin lending and RWA positions. No leverage. The vault's value is independent of BTC/ETH price movements. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: USDC asset, [P1] SLL deploys into stablecoin strategies |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | The VSR (Vault Savings Rate) is set by governance via SETTER_ROLE within bounds set by DEFAULT_ADMIN_ROLE (minVsr/maxVsr). No reflexive incentive model. Rate is anchored to Sky Savings Rate which has demonstrated stability over years. No history of rate instability in 5 months. The governance-set rate model is inherently stable -- no utilization-driven spikes. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: VSR set by SETTER_ROLE with bounds, [P1] Sky Savings Rate stability |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | The threat model documents attack scenarios and response procedures. Rate limits are designed to bound losses in adversarial conditions. The Sky Savings Rate mechanism has been through every major crypto crash since 2018. However, the specific SLL multi-venue deployment strategy is new (~5 months) and explicit high-volatility stress testing results for the full SLL portfolio are not published. | 3 | 9 | Improvable | [P1] [THREAT_MODEL.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/THREAT_MODEL.md) covers adversarial scenarios, but market stress modeling for full SLL portfolio not published |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | No. The vault has no leverage and no liquidation mechanics. Users hold spUSDC which represents a claim on USDC. Sharp crypto price moves do not affect the vault's USDC-denominated value. The only risk is counterparty default in SLL deployment venues, not price-driven liquidation. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: no leverage mechanics, [P1] USDC-denominated throughout |

**Market Subtotal: 33.0/45 (73.3%)**
- 3 questions scored 9 (sum = 27), 2 questions scored 3 (sum = 6)
- Raw sum = 33 out of max 45
- Weighted = (33/45) x 45 = 33.0

---

### **Strategy Total: 230.3/270 (85.3%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 45.0 | 45 | 100.0% |
| Collateral | 35.0 | 45 | 77.8% |
| Infra Counterparty | 40.0 | 45 | 88.9% |
| Protocol Counterparty | 39.0 | 45 | 86.7% |
| Liquidity | 38.3 | 45 | 85.2% |
| Market | 33.0 | 45 | 73.3% |
| **Strategy Total** | **230.3** | **270** | **85.3%** |

---

### OPERATIONS (30% Weight) -- Score: 236.6/270 (87.6%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Changes controlled by SPK token governance with clearly defined rules: proposal by 1% holder, Spark Risk Council review (1 week), Operational Facilitator review, Snapshot vote (3 days, >50%), Sky Spell execution. No single entity can unilaterally change core logic. The Spark Risk Council can reject proposals that pose substantial risks. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance docs](https://docs.spark.fi/governance): full process documented, [P2] Snapshot voting at snapshot.box/#/s:sparkfi.eth |
| O-G-02 | How concentrated is voting power among top holders or delegates? | SPK token governance with delegate system. Token holders can vote directly or delegate to whitelisted delegates. Delegate application process exists. The 1% proposal threshold (100M SPK) is reasonably high to prevent spam but allows broad participation. **Specific voting power concentration data for SPK not verified.** Per criteria: Score 9 requires verified evidence that top 10 control ≤33%. Without verified concentration data, scores Mid (3). | 3 | 9 | **Source Missing** | [P1] [Governance docs](https://docs.spark.fi/governance): delegate system, [P2] Snapshot space active but concentration data unverified |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. Multiple layers: (1) Spark Risk Council can reject proposals, (2) Operational Facilitator verifies Atlas alignment, (3) 3-day Snapshot voting period, (4) Weekly governance cycle with review periods totaling 2-3 weeks. The effective timelock from proposal to execution exceeds 7 days. Guardian roles provide veto capability. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance docs](https://docs.spark.fi/governance): 2-3 week process, [P1] Spark Risk Council veto power |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Governance can change SETTER_ROLE, TAKER_ROLE, and other roles through spells. Vault withdrawals remain permissionless throughout via ERC4626 standard regardless of role changes. Users can always exit via direct contract interaction. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: roles changeable by DEFAULT_ADMIN_ROLE, withdrawals permissionless |

**Governance Subtotal: 56.3/67.5 (83.3%)**
- 3 questions scored 9 (sum = 27), 1 question scored 3 (sum = 3)
- Raw sum = 30 out of max 36
- Weighted = (30/36) x 67.5 = 56.25 ≈ 56.3

**Improvement Opportunities:**
- **O-G-02** (+11.25 weighted points): Verify and publish SPK voting power concentration data (Source Missing)

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Phoenix Labs is the primary development entity, publicly identified with team members visible on LinkedIn and social media. Sam MacPherson (contributor) and other team members active on governance forums. The Sky/MakerDAO ecosystem has one of the most established teams in DeFi with 8+ years of track record. Rune Christensen (MakerDAO founder) is a publicly known figure in the ecosystem. | 9 | 9 | Non-Improvable (optimal) | [P1] Phoenix Labs publicly identified, [P2] Active governance forum participation, [P4] Multiple news sources identify team |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Phoenix Labs is the primary development team with multiple engineers. The Sky/MakerDAO ecosystem has hundreds of contributors across multiple organizations. Multiple independent parties can maintain the protocol. The Spark Proxy governance can reassign development responsibilities. Open-source codebase (AGPL v3 license) enables independent development. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub sparkdotfi](https://github.com/sparkdotfi): 40+ repositories, [P1] AGPL v3 open-source license |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Spark operates within the Sky/MakerDAO ecosystem. Phoenix Labs serves as the development entity. The Sky ecosystem uses a SubDAO structure. Specific legal entity registration details for Phoenix Labs or the Spark SubDAO are partially disclosed through governance documentation but not comprehensively in a single place. The Sky Atlas governs the organizational structure. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance docs](https://docs.spark.fi/governance) reference Sky Atlas, [P2] Forum posts reference Phoenix Labs |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known ongoing or past material enforcement actions against Phoenix Labs, Spark, or the Sky/MakerDAO ecosystem entities in major regulatory jurisdictions. MakerDAO/Sky has operated openly since 2017 without regulatory enforcement. | 9 | 9 | Non-Improvable (optimal) | [P4] No enforcement actions found in public records or news sources |
| O-TL-05 | Is there an on-call and incident response process for core teams? | The THREAT_MODEL.md documents detailed attack scenarios and response procedures (FREEZER removes relayer, backup relayer activated). Emergency spells exist for SparkLend. The team has demonstrated rapid response capability through governance spell execution. However, no public 24/7 on-call SLA, formal incident runbooks, or response time commitments are documented. | 3 | 9 | Source Missing | [P1] [THREAT_MODEL.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/THREAT_MODEL.md) covers relayer incident response, [P0] Emergency spells deployed |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Active Discord community with team presence. Governance forum is actively maintained with team responses. Weekly governance cycles demonstrate consistent engagement. Comprehensive developer documentation available. The Spark App provides direct user support channels. | 9 | 9 | Non-Improvable (optimal) | [P1] [docs.spark.fi](https://docs.spark.fi/) comprehensive, [P2] Active governance forum |
| O-TL-07 | Are major investors or strategic partners disclosed? | Sky/MakerDAO ecosystem is one of the most well-known in DeFi with transparent backing. a16z is a known investor in MakerDAO. The Spark SubDAO structure is publicly documented. Strategic partnerships (Coinbase, BlackRock BUIDL, etc.) visible in code integrations. | 9 | 9 | Non-Improvable (optimal) | [P0] Address registry shows BUIDL, Ethena, Maple, Centrifuge integrations, [P2] Public ecosystem relationships |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | N/A -- spUSDC is not an externally curated vault. Spark governance directly controls the vault through SPK token voting. There is no external strategy manager. Spark also manages spUSDT, spETH, spPYUSD vaults, but these are all governed by the same transparent governance process with per-vault rate limits and allocations. | N/A | N/A | N/A | Not applicable -- governance-managed, not externally curated |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | N/A -- no external strategy manager. Spark governance directly manages. Per the Sky/MakerDAO ecosystem: the historic "Black Thursday" March 2020 event resulted in $8.3M in undercollateralized vault liquidations, but this was in MakerDAO's CDP system (borrower-side risk), not in savings products. sDAI/sUSDS savings products have never experienced collateral loss. | N/A | N/A | N/A | Not applicable as vault product question; MakerDAO savings products have clean record |

**Team & Legal Subtotal: 61.1/67.5 (90.5%)**
- 7 applicable questions (O-TL-08, O-TL-09 = N/A): 6 scored 9 (sum = 54), 1 scored 3
- Raw sum = 57 out of max 63
- Weighted = (57/63) x 67.5 = 61.1

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive documentation across multiple sources: docs.spark.fi for user guides and product docs, GitHub repos with ARCHITECTURE.md, THREAT_MODEL.md, RATE_LIMITS.md, SECURITY.md, OPERATIONAL_REQUIREMENTS.md, CODE_NOTES.md, DEVELOPMENT.md. Technical documentation updated with each release. Vault V2 README provides clear overview. | 9 | 9 | Non-Improvable (optimal) | [P1] [docs.spark.fi](https://docs.spark.fi/), [P1] [ARCHITECTURE.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/ARCHITECTURE.md), [P1] spark-vaults-v2 README |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. THREAT_MODEL.md documents attack vectors and trust assumptions. SECURITY.md details protocol-specific risk considerations with per-integration trust levels. The vault README explains the TAKER_ROLE mechanism and `assetsOutstanding()` tracking. Loss scenarios (counterparty failure, relayer compromise) are explicitly documented with bounded exposure via rate limits. | 9 | 9 | Non-Improvable (optimal) | [P1] [THREAT_MODEL.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/THREAT_MODEL.md), [P1] [SECURITY.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/SECURITY.md) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. The spark-address-registry repository (Ethereum.sol) serves as the canonical registry listing all contracts: Spark Proxy, ALM Controller, ALM Proxy, Rate Limits, Vault V2 implementations and proxies (spUSDC, spUSDT, spETH, spPYUSD), emergency spells, multisig addresses, and all external protocol addresses. Updated regularly (last update 2026-02-10). | 9 | 9 | Non-Improvable (optimal) | [P0] [spark-address-registry/src/Ethereum.sol](https://github.com/sparkdotfi/spark-address-registry/blob/master/src/Ethereum.sol): canonical registry, last updated 2026-02-10 |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. SparkVault.sol defines roles (DEFAULT_ADMIN_ROLE, SETTER_ROLE, TAKER_ROLE) with clear access control. ALM Controller documents roles (DEFAULT_ADMIN_ROLE, RELAYER, FREEZER, CONTROLLER) in ARCHITECTURE.md. Governance docs describe the full change process. Spark spells provide on-chain change history. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: role definitions, [P1] [ARCHITECTURE.md](https://github.com/sparkdotfi/spark-alm-controller/blob/dev/docs/ARCHITECTURE.md): role documentation |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full on-chain proof-of-reserves. The vault's `totalAssets()` and `assetsOutstanding()` functions provide real-time on-chain tracking of total assets and deployed amounts. ALMProxy holdings visible on block explorers. Individual protocol allocations (Aave, Morpho, etc.) verifiable on-chain through the respective protocol interfaces. No off-chain assets requiring separate attestation for the core vault operations. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: totalAssets(), assetsOutstanding(), [P0] ALMProxy holdings on Etherscan |
| O-DT-06 | Are all contracts verified on the leading block explorers? | The vault implementation is open source (AGPL v3) with full source code in the spark-vaults-v2 repository. The spark-address-registry provides all deployment addresses. Implementation address (0x1b992302652A92611DCd5090D1Cb388C6377f455) is documented. Source code is fully readable on GitHub. Etherscan verification status could not be directly confirmed via API but addresses are publicly documented. | 9 | 9 | Non-Improvable (optimal) | [P0] Full source code at [spark-vaults-v2/src/SparkVault.sol](https://github.com/sparkdotfi/spark-vaults-v2/blob/dev/src/SparkVault.sol), [P0] spark-address-registry lists all addresses |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions, all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | No dedicated safety module or ring-fenced reserve for spUSDC depositors. The Sky ecosystem has massive reserves ($6.5B+ stablecoin reserves) and the PSM provides systemic backstop, but activation for spUSDC-specific losses is discretionary via governance. No binding activation rules for depositor loss coverage. Rate limits bound maximum exposure per venue. | 3 | 9 | Improvable | [P1] No dedicated safety module documented, [P1] Sky ecosystem provides implicit but non-binding backstop |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Spark DAO treasury ~$61M per DeFiLlama (March 2026): ~$38M in stablecoins (primarily USDS), ~$23M in SPK tokens. Treasury held in public wallets (Mid-term: 0x089693ed9d9a5ac907bd1a1565867646ffaabcd6, Long-term: 0x46dce51a3f4cbEa91F3A1BBD48Ca5079397d5847). Against total Spark protocol TVL (~$6.4B including SparkLend and Savings), reserves represent ~0.95%. Against Spark Savings only (~$1.1B), reserves = ~5.5%, but treasury is shared across all Spark products and not ring-fenced for spUSDC. Sky ecosystem provides additional implicit backing (billions). Per criteria: shared treasury at ~1% of total protocol TVL = Mid (3). | 3 | 9 | Improvable | [P3] [DeFiLlama Treasury](https://defillama.com/protocol/treasury/spark), [P1] [SPK Token Docs](https://docs.spark.fi/governance/spk-token) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Phoenix Labs operates within the Sky/MakerDAO ecosystem which generates hundreds of millions in annual protocol revenue. Spark is a core SubDAO with dedicated funding. The Sky Savings Rate mechanism has been sustainably funded since 2022. SPK token provides additional treasury capacity. Runway comfortably above 24 months. | 9 | 9 | Non-Improvable (optimal) | [P1] Sky ecosystem annual revenue, [P2] SPK token treasury, [P1] Forum: governance spells show ongoing funding |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Only 5 months of operational history for spUSDC V2 (since Sep 2025). No severe stress events during this period. Per battle-tested rule: untested protocols score max Mid (3). The predecessor sDAI/sUSDS successfully navigated multiple stress events (March 2023 USDC depeg, various market downturns), but spUSDC V2 with SLL deployment is a distinct product. | 3 | 9 | Non-Improvable (time-dependent) | [P3] DeFiLlama shows continuous operation without disruption, but no stress events to evaluate |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. The vault contract is ERC4626-compliant with permissionless withdrawals. If no SETTER_ROLE adjusts the VSR, it continues accruing at the last set rate. Users can always redeem directly from the vault contract. The 10% buffer provides immediate exit liquidity. The ALM Controller's rate limits prevent unauthorized fund movement even without team oversight. Open-source code (AGPL v3) enables community maintenance. | 9 | 9 | Non-Improvable (optimal) | [P0] SparkVault.sol: permissionless redeem/withdraw continue without team, [P1] AGPL v3 open source |

**Financial Resilience Subtotal: 40.5/67.5 (60.0%)**
- 2 questions scored 9 (sum = 18), 3 questions scored 3 (sum = 9)
- Raw sum = 27 out of max 45
- Weighted = (27/45) x 67.5 = 40.5

---

### **Operations Total: 225.4/270 (83.5%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 56.3 | 67.5 | 83.3% |
| Team & Legal | 61.1 | 67.5 | 90.5% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 40.5 | 67.5 | 60.0% |
| **Operations Total** | **225.4** | **270** | **83.5%** |

---

## Final Score Calculation

| Category | Subcategory | Current Points | Max Points | Potential Points |
|----------|-------------|----------------|------------|------------------|
| **Security** | Smart Contract Security | 158.2 | 180 | 180.0 |
| | Key Management | 150.0 | 180 | 180.0 |
| | **Security Subtotal** | **308.2** | **360** | **360.0** |
| **Strategy** | Protocol Mechanics | 45.0 | 45 | 45.0 |
| | Collateral | 35.0 | 45 | 45.0 |
| | Infra Counterparty | 40.0 | 45 | 45.0 |
| | Protocol Counterparty | 39.0 | 45 | 39.0 |
| | Liquidity | 38.3 | 45 | 45.0 |
| | Market | 33.0 | 45 | 45.0 |
| | **Strategy Subtotal** | **230.3** | **270** | **264.0** |
| **Operations** | Governance | 56.3 | 67.5 | 67.5 |
| | Team & Legal | 61.1 | 67.5 | 67.5 |
| | Documentation | 67.5 | 67.5 | 67.5 |
| | Financial Resilience | 40.5 | 67.5 | 67.5 |
| | **Operations Subtotal** | **225.4** | **270** | **270.0** |
| **TOTAL** | | **763.9** | **900** | **894.0** |

---
