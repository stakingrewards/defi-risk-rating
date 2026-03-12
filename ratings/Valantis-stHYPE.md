# Valantis - stHYPE (Staked Hyperliquid) Risk Rating

**Rating Date**: 2026-02-25
**Final Grade**: B
**Total Score**: 690.8/900 points

---

## Detailed Analysis

### SECURITY (40% Weight) - Score: 286.8/360 (79.7%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. All critical contracts (Overseer.sol, HyperCoreUtils.sol, HyperCoreStakingModule.sol) were included in audits by Three Sigma (Feb 2025), Guardian (Oct-Nov 2025), and Pashov (Oct-Nov 2025), plus an additional security review. Three independent audits total. | 9 | 9 | Non-Improvable (optimal) | [P1] [Valantis Audits](https://docs.valantis.xyz/resources/audits#sthype) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent audits by Pashov (Tier-1), Three Sigma (Tier-2), and Guardian (Tier-1). At least one Tier-1 auditor among the most recent. | 9 | 9 | Non-Improvable (optimal) | [P1] [Valantis Audits](https://docs.valantis.xyz/resources/audits#sthype) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. New audits from Guardian and Pashov, as well as an additional security review in Oct-Nov 2025, followed development changes since the initial Three Sigma audit in February 2025. | 9 | 9 | Non-Improvable (optimal) | [P1] [Valantis Audits](https://docs.valantis.xyz/resources/audits#sthype) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. Critical and high-severity issues were remediated and marked as resolved or acknowledged. Pashov and Guardian audits confirmed all major issues were addressed, with fixes verified via commit hashes. Note: pause events still have not been included in the smart contract even though the Three Sigma audit showed it as addressed by the team. | 9 | 9 | Non-Improvable (optimal) | [P1] [Valantis Audits](https://docs.valantis.xyz/resources/audits#sthype), [P0] Audit reports (Google Drive screenshots) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Yes, contracts are upgradeable. Audits confirmed upgradeability and noted role-based access controls (e.g., DEFAULT_ADMIN_ROLE) governing sensitive operations. Events like DefaultAdminTransferScheduled and RoleGranted support upgrade traceability. However, no publicly documented upgrade policy with timelock >=24h exists. | 3 | 9 | **Improvable** | [P0] [HyperEVMScan Events](https://hyperevmscan.io/address/0xffaa4a3d97fe9107cef8a3f48c069f577ff76cc1#events), [P1] Audit reports |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No exploits or malfunctions recorded for stHYPE. | 9 | 9 | Non-Improvable (optimal) | Analytical Research |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events reported. | 9 | 9 | Non-Improvable (optimal) | Analytical Research |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No events recorded for DefaultAdminDelayChangeScheduled or DefaultAdminDelayChangeCanceled on the stHYPE contract. | 9 | 9 | Non-Improvable (optimal) | [P0] [Purrsec Contract](https://purrsec.com/address/0xffaa4a3d97fe9107cef8a3f48c069f577ff76cc1/contract), [P0] Block explorers |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Security contacts provided but no formal bounty program on Immunefi, Code4rena, or other established platforms. Self-hosted security contact only. | 3 | 9 | **Improvable** | [P1] [stakedhype Security](https://docs.stakedhype.fi/technical/security) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Published Monitoring and Incident Response page with invariant-first two-layer model: automatic on-chain safety checks block unsafe actions, off-chain systems provide detection, paging, and incident coordination. Coverage domains include control-plane events, queue/solvency signals, rebase/slashing-accounting signals. SEV-1/2/3 severity classes with timezone-distributed on-call. Comprehensive monitoring infrastructure with documented Safety Control Matrix demonstrates a structured and reputable monitoring setup. | 9 | 9 | Non-Improvable (optimal) | [P1] [Monitoring and Incident Response](https://docs.valantis.xyz/stakedhype/monitoring-and-incident-response) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Published Safety Control Matrix with automatic on-chain protections: pending-slash gating blocks unsafe mint/redeem paths when staking balance changes are detected, rebase bounds revert unsafe supply transitions (SupplyDecreaseTooHigh, AprTooHigh). Operator-confirmed pause controls bounded by on-chain time limits (<=14 days). Automatic protections are embedded in contract logic with clear, deterministic invariant rules. | 9 | 9 | Non-Improvable (optimal) | [P1] [Safety Control Matrix](https://docs.valantis.xyz/stakedhype/monitoring-and-incident-response#safety-control-matrix) |

**Smart Contract Security Subtotal: 87/99 = (87/99) x 180 = 158.2/180 (87.9%)**
**Potential: (99/99) x 180 = 180.0/180**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Admin rights held by multisig via DEFAULT_ADMIN_ROLE and ProxyAdmin ownership. Published Roles and Controls Registry with dated changelog documenting all historical admin/upgrade events including the 2025-08-22 ownership transition, with on-chain transaction links. All changes in last 12 months publicly documented with rationale. | 9 | 9 | Non-Improvable (optimal) | [P1] [Roles and Controls Registry](https://docs.valantis.xyz/stakedhype/roles-and-controls-registry) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | Single key cannot directly drain funds; changes require multisig/governance. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Overview](https://docs.stakedhype.fi/technical/security#governance-overview-2) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Admin multisig address published (0x97dEe0eA4Ca10560f260A0f6f45bdC128A1D51f9). Signers spread across timezones with isolated devices, cold wallets, and verified signing software. Security practices inherited from team securing >$5B in DeFi multisigs. However, threshold configuration, total number of signers, and signer identities remain undisclosed. | 3 | 9 | **Improvable** | [P1] [Roles and Controls Registry](https://docs.valantis.xyz/stakedhype/roles-and-controls-registry), [P1] [Contract Addresses](https://docs.valantis.xyz/stakedhype/contract-addresses) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause/controls exist with broad scope but require multisig and are at least partially documented. Full constraint details not public. | 3 | 9 | **Improvable** | [P1] [Valantis Audits](https://docs.valantis.xyz/resources/audits#sthype) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. Smart contracts hold all assets; no custodian access. All staked HYPE is held on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [Institutional Primer](https://www.stakedhype.fi/institutional.pdf), [P0] On-chain verification |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Segregated; staking pool is separate from treasury/operational wallets. | 9 | 9 | Non-Improvable (optimal) | [P1] [Transparency and Risks](https://docs.stakedhype.fi/info/transparency-and-risks) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A - stHYPE is a liquid staking token, not a vault strategy. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Published Monitoring and Incident Response page documenting incident classes including privileged-key/control-plane incidents, severity-based escalation, and role-bounded emergency controls. Key-compromise and signer-loss response procedures rehearsed internally through STEX operations and stHYPE acquisition. However, no public evidence of formal tabletop exercises. | 3 | 9 | **Improvable** | [P1] [Monitoring and Incident Response](https://docs.valantis.xyz/stakedhype/monitoring-and-incident-response) |

**Key Management Subtotal (7 scored questions, 1 N/A):**
- Raw scores: 9+9+3+3+9+9+3 = 45/63
- Adjusted to weight: (45/63) x 180 = **128.6/180 (71.4%)**
- Potential: (63/63) x 180 = 180.0/180

Note: S-KM-07 marked N/A reduces both numerator and denominator proportionally.

---

**Security Total: 158.2 + 128.6 = 286.8/360 (79.7%)**
**Security Grade: B+** (falls in 284.0-294.0 range)

**Potential Security: 180.0 + 180.0 = 360.0/360 (AAA)**

---

### STRATEGY (30% Weight) - Score: 233.9/270 (86.6%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Validator revenue from HYPE staking, minus validator and protocol fees. Rewards auto-compounded into the stHYPE exchange rate. A portion of deposits (~19%) is allocated into two special HyperCore Stake Accounts (HyENA HIP-3 + USDe Quote Deployer) that earn above-baseline HYPE yield. Distribution: ~81% standard staking, ~13.6% HyENA, ~5.4% USDe Deployer. Note: protocol fee discrepancy -- public FAQs show 3% but smart contract shows 10%. | 9 | 9 | Non-Improvable (optimal) | [P1] [stakedhype FAQ](https://www.stakedhype.fi/faq), [P0] [Purrsec Contract](https://purrsec.com/address/0xb96f07367e69e86d6e9c3f29215885104813eeae/contract), [P1] [Stake Accounts](https://docs.valantis.xyz/stakedhype/stake-accounts), [P1] [Institutional Primer](https://www.stakedhype.fi/institutional.pdf) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Yield can go negative in extreme cases where validators are slashed. Part of the yield comes from two non-standard stake accounts (HyENA HIP-3 and USDe Quote Asset Deployer) which earn elevated HYPE-denominated rewards in exchange for stricter withdrawal conditions and higher slashing exposure. | 9 | 9 | Non-Improvable (optimal) | [P1] [Terms of Service](https://docs.stakedhype.fi/info/terms-of-service#id-7.7.3-risks-of-smart-contracts-validators-and-sovereign-vaults), [P1] [Institutional Primer](https://www.stakedhype.fi/institutional.pdf), [P1] [Stake Accounts](https://docs.valantis.xyz/stakedhype/stake-accounts) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | stHYPE itself does not use leverage; underlying HYPE staking is unlevered. No rehypothecation. | 9 | 9 | Non-Improvable (optimal) | Analytical Research |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A - stHYPE is a liquid staking token, not a lending protocol. No LTV ratio applicable. | N/A | N/A | N/A | - |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | N/A - Lending/Vault only question per product type modifiers. | N/A | N/A | N/A | - |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | N/A - Lending/Vault only question per product type modifiers. | N/A | N/A | N/A | - |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. stHYPE's yield is derived entirely from Hyperliquid's native staking emissions and the HIP-3/USDe stake-account mechanisms, grounded in the network's real economic activity. No token emissions or incentive subsidies required for yield. | 9 | 9 | Non-Improvable (optimal) | [P1] [Stake Accounts](https://docs.valantis.xyz/stakedhype/stake-accounts) |
| ST-PM-08 | Can the position be fully unwound without slippage turning yield negative? | Under the stated withdrawal times, the entire position can be unstaked, and users will receive their assets plus accrued rewards minus fees. Standard accounts unwind in ~7.2 days. Non-standard accounts may take up to 90 days. | 9 | 9 | Non-Improvable (optimal) | [P1] [Stake Accounts](https://docs.valantis.xyz/stakedhype/stake-accounts) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | N/A - Lending/Vault only question per product type modifiers. | N/A | N/A | N/A | - |

**Protocol Mechanics Subtotal (5 scored questions, 4 N/A):**
- Raw scores: 9+9+9+9+9 = 45/45
- Adjusted: (45/45) x 45 = **45.0/45 (100.0%)**

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | HYPE is Hyperliquid's native token with strong liquidity and market presence. As the base asset of a Tier-1 chain, it is a reasonable collateral for liquid staking. | 9 | 9 | Non-Improvable (optimal) | [P3] Market data |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | No major depeg recorded. Small depeg on Sep 25th. Minor deviations during sharp market moves; generally tracks underlying with exchange-rate drift. | 9 | 9 | Non-Improvable (optimal) | [P3] [StakingRewards Analytics](https://www.stakingrewards.com/asset/staked-hyperliquid/analytics), [P3] [DexScreener](https://dexscreener.com/hyperevm/0xa0a3ad6ed38354c02b892ddfc79c4a93729ee9b3) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Slashing risk disclosed; operators monitored; no major slashing events recorded. Mix of large professional operators distributed across Europe and Asia. Validators are selected based on audited track record and reputation, must meet minimum staking requirements (10k HYPE bond), and get accepted and voted by stHYPE holders. No automated validator replacement mechanism, but underperforming validators can be removed from the set. | 9 | 9 | Non-Improvable (optimal) | [P1] [Operators](https://docs.stakedhype.fi/governance/operators), [P1] [Validators](https://www.stakedhype.fi/validators), [P3] [ASXN Dashboard](https://hyperscreener.asxn.xyz/validators) |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | stHYPE relies on Hyperliquid's internal bridging (CoreWriter), and essentially 100% of its TVL is in assets that have been moved to the HyperCore layer via that mechanism. However, CoreWriter is not an external bridge -- Hyperliquid's architecture has HyperCore and HyperEVM sharing a single unified state under the same consensus. It is a series of state updates within a single Core block, not a cross-chain bridge. Scored Mid due to the technical bridging mechanism despite it being internal. | 3 | 3 | **Non-Improvable** | [P1] [HyperEVM Docs](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/interacting-with-hypercore), [P4] [Oak Research](https://oakresearch.io/en/analyses/fundamentals/hyperliquid-vision-aws-of-liquidity-builder-codes-core-writer-hip-3), [P4] [Ambit Labs](https://medium.com/@ambitlabs/demystifying-the-hyperliquid-precompiles-and-corewriter-ef4507eb17ef) |

**Collateral Subtotal: 30/36 = (30/36) x 45 = 37.5/45 (83.3%)**
**Potential: (30/36) x 45 = 37.5/45** (ST-C-04 non-improvable at 3)

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Chain: Hyperliquid/HyperEVM (Tier-1). Bridge: CoreWriter (internal, not external). Oracles: HyperCore validator-provided price feeds (inherent to chain). Wallets: Rabby, Keplr, Safe, Coinbase Wallet. CEXs: Not utilized directly. All dependencies listed and Tier-0/1. | 9 | 9 | Non-Improvable (optimal) | [P1] [HyperEVM Docs](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/interacting-with-hypercore), [P1] [Oracle Docs](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/oracle) |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | Bridging is entirely within Hyperliquid's unified network. No external bridge risk. Oracle feeds provided natively by validators as part of consensus. No dependency on external oracle providers. | 9 | 9 | Non-Improvable (optimal) | [P1] [HyperEVM Docs](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/interacting-with-hypercore) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | stHYPE is not using any critical off-chain infrastructure providers. All operations are on-chain. Score Low (9) per applicability check. | 9 | 9 | Non-Improvable (optimal) | Analytical Research |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | No reported blockchain failures. The chain does not experience persistent congestion. Some spikes occur during market events. Fees sometimes increase due to market conditions. Hyperliquid validators have not experienced any slashing events to date. | 9 | 9 | Non-Improvable (optimal) | Analytical Research |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No reported blockchain failures or halts. The chain has been operational without consensus failures in the evaluation period. | 9 | 9 | Non-Improvable (optimal) | Analytical Research |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | No. Hyperliquid validators have not experienced any slashing events to date. The slashing mechanism primarily targets deployers under HIP-3 rather than validators directly for consensus faults. | 9 | 9 | Non-Improvable (optimal) | Analytical Research |
| ST-IC-07 | Are validators diverse geographically and by operator? | Mix of large professional operators; some centralization but multiple entities. Validator node locations (per ASXN dashboard) are distributed in Europe and Asia. Validator companies have coverage across both regions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Operators](https://docs.stakedhype.fi/governance/operators), [P1] [Validators](https://www.stakedhype.fi/validators), [P3] [ASXN Dashboard](https://hyperscreener.asxn.xyz/validators) |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | If CoreWriter fails, withdrawals would not be possible to execute. This is a single point of failure for exits, though CoreWriter is integral to Hyperliquid's unified architecture rather than an external dependency. | 3 | 3 | **Non-Improvable** | Analytical Research |

**Infra Counterparty Subtotal: 66/72 = (66/72) x 45 = 41.25/45 (91.7%)**
**Potential: (66/72) x 45 = 41.25/45** (ST-IC-08 non-improvable at 3)

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Apart from staking users' funds on HyperCore, HYPE has been deployed into stake accounts: HIP-3 Staking Module (Ethena HyENA, 500k HYPE) and Quote Asset Deployer Staking Module (USDe, 200k HYPE). Issues include: increased withdrawal time (90 days) for these accounts, and additional slashing risks for HIP-3 based options. Distribution: ~61.1% standard staking, ~27.8% HyENA, ~11.1% USDe Deployer. | 3 | 9 | **Improvable** | [P1] [Stake Accounts](https://docs.valantis.xyz/stakedhype/stake-accounts), [P1] [Valantis App](https://app.valantis.xyz/staking) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Valantis is running a points campaign. There is no conflict of interest identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Valantis Docs](https://docs.valantis.xyz/) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. stHYPE has hard limits per counterparty (500k HYPE in Ethena HyENA HIP-3 module and 200k in USDe Quote Deployer, totaling 700k HYPE) with rebalancing rules triggered when exceeded or when TVL hits the 1M HYPE early-exit threshold, initiating managed liquidity buffers. High-frequency withdrawals from standard HyperCore accounts first, with up to 90-day timed exits from non-standard accounts. | 9 | 9 | Non-Improvable (optimal) | [P1] [Stake Accounts](https://docs.valantis.xyz/stakedhype/stake-accounts) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Standard Stake Accounts offer fast and secure unwinding (~7.2 days). Non-standard Stake Accounts introduce higher yield and slashing risk, with up to a 90-day withdrawal lag. | 3 | 9 | **Improvable** | [P1] [Stake Accounts](https://docs.valantis.xyz/stakedhype/stake-accounts) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | stHYPE does not utilize any custody providers (all assets on-chain). No asset managers used. All validators/operators are disclosed on the website with names and details. | 9 | 9 | Non-Improvable (optimal) | [P1] [Validators](https://www.stakedhype.fi/validators) |

**Protocol Counterparty Subtotal: 33/45 = (33/45) x 45 = 33.0/45 (73.3%)**
**Potential: (45/45) x 45 = 45.0/45**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Unstake via HyperCore queue or sell stHYPE on secondary markets. New HYPE staked via stHYPE minting must first settle queued user withdrawals before being staked to any Staking Module. However, withdrawals and token burning can be paused by admin. | 3 | 9 | **Improvable** | [P1] [Stake Accounts](https://docs.valantis.xyz/stakedhype/stake-accounts), [P1] [GitHub Audits](https://github.com/thunderhead-labs/audits/tree/main/stHYPE) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | You can withdraw, but you have to wait. In-protocol redemption is available via standard unstaking. Near-total exits would require extended processing through the queue. | 9 | 9 | Non-Improvable (optimal) | Analytical Research |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | The average withdrawal time over the checked period (May 2025 to mid-May 2026) oscillated around 7.2 days, matching the protocol's guarantees. The median was even lower thanks to mostly instant unstaking in recent weeks. | 9 | 9 | Non-Improvable (optimal) | Analytical Research (on-chain data) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | N/A - Lending/Vault only question per product type modifiers. | N/A | N/A | N/A | - |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Historical high-volatility periods show slightly increased volume and modestly wider spreads but no freezes, extreme slippage, or broken redemption mechanics. | 9 | 9 | Non-Improvable (optimal) | [P3] [DexScreener](https://dexscreener.com/hyperevm/0xa0a3ad6ed38354c02b892ddfc79c4a93729ee9b3) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | Around 19% of the collateral is staked with HyENA and USDe Stake Accounts, and their withdrawal times range up to 90 days. This exceeds the stated ~7.2 day withdrawal period for approximately 10-30% of assets. | 3 | 3 | **Non-Improvable** | [P1] [Transparency and Risks](https://docs.stakedhype.fi/info/transparency-and-risks), [P1] [Stake Accounts](https://docs.valantis.xyz/stakedhype/stake-accounts) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Redemptions do not solely rely on secondary markets; standard unstaking is available as the primary path. Secondary markets are an additional option. | 9 | 9 | Non-Improvable (optimal) | [P1] [Unstake Guide](https://docs.stakedhype.fi/guides/unstake), [P1] [Stake Accounts](https://docs.valantis.xyz/stakedhype/stake-accounts) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | HYPE has hundreds of millions in daily volume. stHYPE secondary-market liquidity has improved: STEX TVL is ~570k HYPE split between stHYPE AMM (313k HYPE) and kHYPE AMM (257k HYPE), with stHYPE AMM turnover of 1.31x and kHYPE AMM turnover of 2.66x. stHYPE depeg is median 2.99 bps. However, absolute liquidity remains insufficient to absorb ~10% of TVL without significant impact. | 3 | 9 | **Improvable** | [P3] [CoinGecko stHYPE](https://www.coingecko.com/en/coins/staked-hype), [P1] [stHYPE Health Report Feb 2026](stHYPE Health Report - March 1 2026.pdf) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | N/A - Lending/Vault only question per product type modifiers. | N/A | N/A | N/A | - |

**Liquidity Subtotal (7 scored questions, 2 N/A):**
- Raw scores: 3+9+9+9+3+9+3 = 45/63
- Adjusted: (45/63) x 45 = **32.1/45 (71.4%)**
- Potential: (57/63) x 45 = 40.7/45 (ST-L-06 non-improvable at 3)

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | No major depeg recorded. Small depeg on Sep 25th. Minor deviations during sharp market moves; generally tracks underlying with exchange-rate drift. | 9 | 9 | Non-Improvable (optimal) | [P3] [StakingRewards Analytics](https://www.stakingrewards.com/asset/staked-hyperliquid/analytics), [P3] [DexScreener](https://dexscreener.com/hyperevm/0xa0a3ad6ed38354c02b892ddfc79c4a93729ee9b3) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses? | N/A - Lending/Vault only question per product type modifiers. | N/A | N/A | N/A | - |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | N/A - Lending/Vault only question per product type modifiers. | N/A | N/A | N/A | - |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | N/A - Lending/Vault only question per product type modifiers. | N/A | N/A | N/A | - |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | N/A - Lending/Vault only question per product type modifiers. | N/A | N/A | N/A | - |

**Market Subtotal (1 scored question, 4 N/A):**
- Raw scores: 9/9
- Adjusted: (9/9) x 45 = **45.0/45 (100.0%)**

---

**Strategy Total: 45.0 + 37.5 + 41.25 + 33.0 + 32.1 + 45.0 = 233.9/270 (86.6%)**
**Strategy Grade: BB** (falls in 228.0-235.5 range)

**Potential Strategy: 45.0 + 37.5 + 41.25 + 45.0 + 40.7 + 45.0 = 254.5/270 (A-)**

---

### OPERATIONS (30% Weight) - Score: 170.1/270 (63.0%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid governance model: team multisig with community veto. Not fully on-chain tokenholder governance; multisig can execute some changes within documented bounds. | 3 | 9 | **Improvable** | [P1] [Institutional Primer](https://www.stakedhype.fi/institutional.pdf) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | Top 10 voting addresses control >33% and <=66% of voting power, implying moderate capture risk. No public governance dashboard or interface found. | 3 | 9 | **Improvable** | [P0] [HyperEVMScan Token Holders](https://hyperevmscan.io/token/0xffaa4a3d97fe9107cef8a3f48c069f577ff76cc1#balances) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Community veto exists. ABIs for stHYPE and Overseer show timelocks and delay parameters. Documentation is not explicit enough on the delay duration. | 3 | 9 | **Improvable** | [P1] [Institutional Primer](https://www.stakedhype.fi/institutional.pdf) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A - Vault only question per product type modifiers. | N/A | N/A | N/A | - |

**Governance Subtotal (3 scored questions, 1 N/A):**
- Raw scores: 3+3+3 = 9/27
- Adjusted: (9/27) x 67.5 = **22.5/67.5 (33.3%)**
- Potential: (27/27) x 67.5 = 67.5/67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Core team publicly identified with verifiable track records. Deven Matthews identified as key figure. | 9 | 9 | Non-Improvable (optimal) | [P2] [Crunchbase](https://www.crunchbase.com/person/deven-matthews-9f30), [P3] [RootData](https://www.rootdata.com/Projects/detail/Valantis%20Protocol?k=MTA0NDM%3D) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Small team maintains most critical systems. LinkedIn shows fewer than 5 engineers. Partial redundancy but some key-person risk. | 3 | 3 | **Non-Improvable** | [P2] [LinkedIn](https://www.linkedin.com/company/valantis-labs/people/) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Valantis Panama Inc. named as the entity operating the website and serving as liaison of the protocol multisig involved in proxy upgrades. Panama jurisdiction with governing law in Terms of Service. However, entity deliberately distances itself from protocol operations, emphasizing the protocol is "a set of smart contracts which do not involve a sole operator." | 3 | 9 | **Improvable** | [P1] [Terms of Service](https://docs.valantis.xyz/terms-of-service), [P1] [Transparency and Risks](https://docs.valantis.xyz/stakedhype/transparency-and-risks) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known ongoing or past material enforcement actions. ComplyAdvantage KYB check clean. | 9 | 9 | Non-Improvable (optimal) | ComplyAdvantage KYB check |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Published Monitoring and Incident Response page documenting formal incident response process with SEV-1/2/3 severity classification, timezone-distributed operational coverage with primary/backup ownership, escalation expectations, and response SLAs. | 9 | 9 | Non-Improvable (optimal) | [P1] [Monitoring and Incident Response](https://docs.valantis.xyz/stakedhype/monitoring-and-incident-response) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Dedicated Discord with ticketing system available. | 9 | 9 | Non-Improvable (optimal) | [P2] [Discord](https://discord.com/invite/9cUzQ7EgJQ) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Investors publicly disclosed for Valantis Labs. | 9 | 9 | Non-Improvable (optimal) | [P3] [Crypto Fundraising](https://crypto-fundraising.info/projects/valantis-labs/) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | N/A - Vault only question per product type modifiers. | N/A | N/A | N/A | - |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | N/A - Vault only question per product type modifiers. | N/A | N/A | N/A | - |

**Team & Legal Subtotal (7 scored questions, 2 N/A):**
- Raw scores: 9+3+3+9+9+9+9 = 51/63
- Adjusted: (51/63) x 67.5 = **54.6/67.5 (80.9%)**
- Potential: (57/63) x 67.5 = 61.1/67.5 (O-TL-02 non-improvable at 3)

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Documentation consolidated to docs.valantis.xyz/stakedhype as canonical source. Comprehensive coverage including multiple new pages: Monitoring and Incident Response, Roles and Controls Registry, Upgrade and Risk Governance, Transparency and Risks. docs.stakedhype.fi being redirected to canonical source. | 9 | 9 | Non-Improvable (optimal) | [P1] [Valantis stakedhype Docs](https://docs.valantis.xyz/stakedhype) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. The stHYPE whitepaper and official documentation provide information on how collateral is used and the risks that could lead to losses. | 9 | 9 | Non-Improvable (optimal) | [P1] [Institutional Primer](https://www.stakedhype.fi/institutional.pdf) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Smart contract addresses are documented. Proxies are accessible through explorers. Admin roles are not documented centrally, apart from visible roles in the smart contract. | 9 | 9 | Non-Improvable (optimal) | [P1] [Contract Addresses](https://docs.valantis.xyz/stakedhype/contract-addresses), [P0] [Purrsec stHYPE](https://purrsec.com/address/0xffaa4a3d97fe9107cef8a3f48c069f577ff76cc1/contract), [P0] [Purrsec Overseer](https://purrsec.com/address/0xb96f07367e69e86d6e9c3f29215885104813eeae/contract) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Published Roles and Controls Registry as canonical public registry with comprehensive role documentation across all contracts (stHYPE, Overseer, wstHYPE, ProxyAdmin) and dated changelog entries from August 2025 through February 2026 with on-chain transaction links. | 9 | 9 | Non-Improvable (optimal) | [P1] [Roles and Controls Registry](https://docs.valantis.xyz/stakedhype/roles-and-controls-registry) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Users' assets are verifiable through the stHYPE smart contract. All assets are on-chain and fully transparent. | 9 | 9 | Non-Improvable (optimal) | [P0] [Purrsec stHYPE](https://purrsec.com/address/0xffaa4a3d97fe9107cef8a3f48c069f577ff76cc1/contract) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | stHYPE and Overseer V1 verified on leading block explorers (HyperEVMScan, Purrsec, Hyperscan). stHYPE proxy verified on purrsec. | 9 | 9 | Non-Improvable (optimal) | [P0] [Purrsec stHYPE](https://purrsec.com/address/0xffaa4a3d97fe9107cef8a3f48c069f577ff76cc1/contract), [P0] [HyperEVMScan stHYPE](https://hyperevmscan.io/token/0xffaa4a3d97fe9107cef8a3f48c069f577ff76cc1#code), [P0] [Hyperscan stHYPE](https://www.hyperscan.com/token/0xfFaa4a3D97fE9107Cef8a3F48c069F577Ff76cC1?tab=contract) |

**Documentation Subtotal: 54/54 = (54/54) x 67.5 = 67.5/67.5 (100.0%)**
**Potential: (54/54) x 67.5 = 67.5/67.5**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Team explicitly confirmed: "there is no guaranteed insolvency backstop and no binding activation commitment for loss recovery today." No dedicated insurance fund, safety module, or backstop reserve exists. Users bear full exposure to losses. | 1 | 9 | **Improvable** | [P1] [Transparency and Risks](https://docs.valantis.xyz/stakedhype/transparency-and-risks) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Team confirmed treasury/backstop size and liquidity are not yet published. Committed to introducing a "resilience-disclosure format" in the future, but no disclosure has been made. | 1 | 9 | **Improvable** | [P1] [Transparency and Risks](https://docs.valantis.xyz/stakedhype/transparency-and-risks) |
| O-FR-03 | What is the estimated operational runway at current burn? | Team disclosed operational runway of ~12-18 months at current growth-phase run rate. Protocol is self-sustaining based on current revenue and maintenance-only operational costs. Covers emergency contingencies and expected future audit costs. | 9 | 9 | Non-Improvable (optimal) | Team disclosure |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | TVL diminishing while rewards and revenue remain stable from native HYPE staking. A portion of deposits allocated to non-standard stake accounts earning above-baseline yields. Team acknowledged no recurring stress-history report has been published and committed to publishing periodic resilience reports. | 3 | 9 | **Improvable** | [P1] [stakedhype Analytics](https://www.stakedhype.fi/analytics), [P3] [ASXN Staking](https://hyperscreener.asxn.xyz/staking) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Standard modules and base burn/redeem flows are on-chain and user-triggered. For non-standard modules, legal documentation includes automatic triggers obligating HyENA team to return HYPE when stHYPE circulation drops below 1M TVL. External management multisig operated by BasedApp Team, Ethena Foundation, and Valantis Labs. Full autonomy in a no-team scenario not yet guaranteed for non-standard accounts. | 3 | 9 | **Improvable** | [P1] [Stake Accounts](https://docs.valantis.xyz/stakedhype/stake-accounts), [P1] [Transparency and Risks](https://docs.valantis.xyz/stakedhype/transparency-and-risks) |

**Financial Resilience Subtotal: 17/45 = (17/45) x 67.5 = 25.5/67.5 (37.8%)**
**Potential: (45/45) x 67.5 = 67.5/67.5**

---

**Operations Total: 22.5 + 54.6 + 67.5 + 25.5 = 170.1/270 (63.0%)**
**Operations Grade: CCC** (falls in 150.0-174.0 range)

**Potential Operations: 67.5 + 61.1 + 67.5 + 67.5 = 263.6/270 (AA-)**

---

## Final Score Calculation

| Category | Subcategory | Weight | Current Score | Max Score | Current % | Potential Score |
|----------|-------------|--------|---------------|-----------|-----------|-----------------|
| Security | Smart Contract Security | 20% | 158.2 | 180 | 87.9% | 180.0 |
| Security | Key Management | 20% | 128.6 | 180 | 71.4% | 180.0 |
| **Security Total** | | **40%** | **286.8** | **360** | **79.7%** | **360.0** |
| Strategy | Protocol Mechanics | 5% | 45.0 | 45 | 100.0% | 45.0 |
| Strategy | Collateral | 5% | 37.5 | 45 | 83.3% | 37.5 |
| Strategy | Infra Counterparty | 5% | 41.25 | 45 | 91.7% | 41.25 |
| Strategy | Protocol Counterparty | 5% | 33.0 | 45 | 73.3% | 45.0 |
| Strategy | Liquidity | 5% | 32.1 | 45 | 71.4% | 40.7 |
| Strategy | Market | 5% | 45.0 | 45 | 100.0% | 45.0 |
| **Strategy Total** | | **30%** | **233.9** | **270** | **86.6%** | **254.5** |
| Operations | Governance | 7.5% | 22.5 | 67.5 | 33.3% | 67.5 |
| Operations | Team & Legal | 7.5% | 54.6 | 67.5 | 80.9% | 61.1 |
| Operations | Documentation | 7.5% | 67.5 | 67.5 | 100.0% | 67.5 |
| Operations | Financial Resilience | 7.5% | 25.5 | 67.5 | 37.8% | 67.5 |
| **Operations Total** | | **30%** | **170.1** | **270** | **63.0%** | **263.6** |
| **GRAND TOTAL** | | **100%** | **690.8** | **900** | **76.8%** | **878.0** |

**Current Grade: B** (690.8 falls in 685-710 range)
**Potential Grade: AA-** (878.0 falls in 876-882 range)

---


---
