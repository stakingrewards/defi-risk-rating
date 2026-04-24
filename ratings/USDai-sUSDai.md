# USD.ai - sUSDai Risk Rating

**Rating Date**: 2026-04-16 (updated 2026-04-22 with on-chain verification)
**Final Grade**: CCC-
**Total Score**: 489.9/900 points (Potential: 794.9/900)
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-beta

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 210.0/360 (58.3%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Two independent recognized audits: Cantina (Tier-1, May 2025) covering ERC-7540 vault, redemption queue, blacklisting, oracle, bridging; and Quantstamp (Tier-1, Feb 2026). KTL performed 5 additional audits (May 2025 - Mar 2026) but is not on any SR tier list. Total: 2 independent audits from recognized firms with public reports. | 9 | 9 | Non-Improvable (optimal) | [P1] Cantina audit (cantina.xyz/portfolio/23dbab18), [P1] docs.usd.ai/technical-overview/audits listing 7 reports incl. Quantstamp (Feb 2026) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent recognized audit: Quantstamp (Feb 2026), Tier-1 per SR list. Cantina (May 2025) also Tier-1. KTL (Mar 2026) is unranked/not on any tier list. | 9 | 9 | Non-Improvable (optimal) | [P1] docs.usd.ai/technical-overview/audits |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | sUSDai implementation upgraded Feb 2, 2026 (0x0080... to 0xda8c...). Quantstamp audit dated Feb 3, 2026 and KTL audits in Mar 2026 follow this upgrade. Evidence of post-upgrade audit coverage. | 9 | 9 | Non-Improvable (optimal) | [P0] Arbiscan sUSDai proxy upgrade history, [P1] Audit dates on docs.usd.ai |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Cantina: 0 critical, 0 high, 1 medium (inflation attack -- fixed), 8 low (6 fixed, 2 acknowledged), 10 informational (8 fixed, 2 acknowledged). All critical/high/medium resolved. 80% total remediation. | 9 | 9 | Non-Improvable (optimal) | [P1] Cantina audit report (cantina.xyz/portfolio/23dbab18) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | USDai and sUSDai use ERC-1967 Transparent Proxy with upgradeToAndCall(). Both ProxyAdmins (sUSDai: 0x0b3296b6...; USDai: 0x2ddf39c7...) are owned by a dedicated Upgrade TimelockController at 0x0eEA1ee0... with minimum delay = 86400 seconds (1 day), verified via eth_call. This upgrade timelock is separate from the documented governance Timelock at 0x0EEC... (3-day delay, used by Chip Governor). Upgrade path: proposer schedules -> 1-day delay -> executor calls. Constraint exists but 1-day delay is shorter than 72h+ threshold for Low. | 3 | 9 | **Improvable** | [P0] ERC-1967 admin slot read via RPC, [P0] Upgrade Timelock 0x0eEA1ee08611FF4a4e83bFE3916712751995639b getMinDelay()=86400, [P0] Doc Timelock 0x0EEC...8221 getMinDelay()=259200 |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploits since launch (Aug 2025). No incidents on Rekt.news, DeFiLlama hacks database, or other exploit trackers. ~8 months operational history. | 9 | 9 | Non-Improvable (optimal) | [P1] Cantina audit (no critical/high), [P3] DeFiLlama hacks, [P4] Rekt.news |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No confirmed rug-pull events. Permian Labs is a funded entity ($38M from Framework, Dragonfly, Coinbase Ventures, YZi Labs). Team publicly identified. | 9 | 9 | Non-Improvable (optimal) | [P4] crypto-fundraising.info, [P1] permianlabs.xyz |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | TimelockController parameters now verified on-chain. Governance Timelock (0x0EEC...8221) getMinDelay()=259200s (3 days). Upgrade Timelock (0x0eEA...639b) getMinDelay()=86400s (1 day). Upgrade Timelock has only 1 outbound tx in its history; no on-chain evidence of delay reductions. No DelayChange events observed. | 9 | 9 | Non-Improvable (optimal) | [P0] Upgrade Timelock getMinDelay() verified via eth_call, [P0] Doc Timelock getMinDelay() verified via eth_call, [P0] getTransactionCount = 1 (minimal history) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Active bounty on Cantina (cantina.xyz/bounties/32e64f2e) with $100K total rewards, 139 findings submitted since June 2025. MetaStreet also has separate Immunefi bounty. Cantina is reputable; $100K meets >=100K threshold. | 9 | 9 | Non-Improvable (optimal) | [P1] Cantina bounty page, [P1] Immunefi MetaStreet listing |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | No evidence of monitoring systems in documentation, blog, or protocol announcements. No monitoring provider named. No dashboards, SLAs, or integration details disclosed. | 1 | 9 | **Improvable** | [P1] docs.usd.ai -- no monitoring page, [P4] Web search -- no partnerships found |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | PAUSE_ADMIN_ROLE exists (Cantina confirmed). Pause appears manual only. Cantina recommended splitting pause/unpause roles. No automated circuit breakers documented. No coverage of automated capital flows. | 1 | 9 | **Improvable** | [P1] Cantina audit: pause role finding, [P1] No circuit breaker documentation |

**Smart Contract Security Subtotal:**
- Raw scores: 9+9+9+9+3+9+9+9+9+1+1 = 77/99
- Adjusted: (77/99) x 180 = **140.0/180 (77.8%)**

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Full ownership map verified on-chain. sUSDai DEFAULT_ADMIN_ROLE and PAUSE_ADMIN_ROLE: Gnosis Safe v1.4.1 at 0x5f0bc72f...5841f (3-of-3 threshold). STRATEGY_ADMIN_ROLE: Gnosis Safe v1.4.1 at 0xe7e53f94...3670 (3-of-4 threshold, shares 3 signers with DEFAULT_ADMIN Safe plus one additional signer). sUSDai/USDai proxy upgrades: both ProxyAdmins owned by Upgrade TimelockController at 0x0eEA1ee0...639b (1-day delay). Role grants verified via RoleGranted events (2 grants total, 0 revokes). All admin addresses and thresholds fully verifiable via eth_call. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDai.hasRole(DEFAULT_ADMIN_ROLE, 0x5f0bc72f...5841f)=true, [P0] sUSDai.hasRole(STRATEGY_ADMIN_ROLE, 0xe7e53f94...3670)=true, [P0] Safe getThreshold()=3 and getOwners() both Safes, [P0] ERC-1967 admin slot reads, [P0] RoleGranted event log |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No single key can move user funds or upgrade custody contracts. STRATEGY_ADMIN Safe requires 3-of-4 signatures to deploy/harvest. DEFAULT_ADMIN Safe requires 3-of-3 to grant/revoke roles, pause, or otherwise take admin actions. Proxy upgrades additionally require passing through a 1-day Upgrade Timelock. Meets the >=M-of-N threshold requirement (M>=2), so the Deal Breaker is NOT triggered. However, under the strict framework reading the total distinct signer pool across both Safes is 4 (3 DEFAULT_ADMIN signers + 1 additional STRATEGY_ADMIN signer), below the >=5 total signers threshold typically required for Low. Scored Mid until a 5th signer is added. | 3 | 9 | **Improvable** | [P0] STRATEGY Safe getThreshold()=3, getOwners() returns 4 addresses, [P0] DEFAULT_ADMIN Safe getThreshold()=3, getOwners() returns 3 addresses, [P0] Upgrade Timelock minDelay=86400s |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | STRATEGY Safe is 3-of-4, DEFAULT_ADMIN Safe is 3-of-3, both verified via getThreshold()/getOwners(). 3 of the 4 STRATEGY signers overlap exactly with the 3 DEFAULT_ADMIN signers, so the "core 3" quorum controls both Safes. STEP application states signers represent MetaStreet Foundation, Permian Labs, and third-party observers but signer EOA identities are not publicly linked to these organizations. Thresholds meet the >=3 signer requirement for Mid, but lack of 5+ total signers and lack of public identity linkage prevents Low (9). | 3 | 9 | **Improvable** | [P0] STRATEGY Safe owners: 0xe982B3F6..., 0x986868c9..., 0xD1Affe27..., 0x034d28A3..., [P0] DEFAULT_ADMIN Safe owners: 0xe982B3F6..., 0x986868c9..., 0xD1Affe27..., [P2] STEP application organization claim unlinked to addresses |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Blacklisting functionality exists (Cantina confirmed). Bypass vulnerabilities found: users can bridge to circumvent blacklist. PAUSE_ADMIN_ROLE controls both pause and unpause (same role). Constraints partially documented but broad scope. | 3 | 9 | **Improvable** | [P1] Cantina audit blacklist/pause findings |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | On-chain: USDai/sUSDai held in smart contracts. Backing: M0's $M token (T-bills via regulated custodians -- M0's model, not USD.ai's). When loans deployed: physical GPUs in third-party data centers, GPU Finance Ltd. as Administrative Agent, Wilmington Trust escrow. Currently ~100% in M0 T-bills (on-chain), but architecture designed for 20-30% off-chain GPU loan deployment. Current small-portion custody model with disclosed regulated entities. | 3 | 3 | Non-Improvable | [P0] DeFiLlama: $300M PYUSD in protocol, [P1] Full docs: GPU Finance Ltd., Wilmington Trust |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Loans structured through bankruptcy-remote SPVs with per-loan Wilmington Trust escrow. DSRA (~10% of gross loan) retained per loan. On-chain sUSDai vault holds USDai separately. Segregation well-designed but multi-entity structure creates complexity. | 3 | 9 | **Improvable** | [P1] Full docs: SPV structure, Wilmington Trust, DSRA |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | sUSDai deploys through LoanRouter to MetaStreet lending pools. STRATEGY_ADMIN_ROLE manages pool whitelist. CHIP governance stated to control eligibility. On-chain enforcement mechanism unclear; admin can route without documented timelock. | 3 | 9 | **Improvable** | [P1] Technical overview: LoanRouter, STRATEGY_ADMIN_ROLE |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No documented incident playbook in docs, blog, or STEP application. No evidence of tabletop exercises or key rotation procedures. | 1 | 9 | **Improvable** | [P1] docs.usd.ai -- no playbook, [P2] STEP application -- none |

**Key Management Subtotal:**
- Raw scores: 9+3+3+3+3+3+3+1 = 28/72
- Adjusted: (28/72) x 180 = **70.0/180 (38.9%)**

**Security Total: 140.0 + 70.0 = 210.0/360 (58.3%)**

---

### STRATEGY (30% Weight) -- Score: 140.1/270 (51.9%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield from: (1) GPU-collateralized loan interest 7-15% APR, (2) T-bill yield on idle capital via M0/PYUSD (~4.5%). Both align with "financing AI infrastructure" mandate. Current APR 6.84%, expected 12.18%. Percent breakdown between sources not precisely documented. | 3 | 9 | **Improvable** | [P1] sUSDai page: 6.84% current APR, [P1] Full docs: yield sources |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Principal loss if: GPU borrower defaults AND collateral recovery insufficient (ITAD costs ~30% of gross sale) AND FiLo first-loss buffer insufficient. Also GPU depreciation exceeding insurance. These are severe but plausible single-shock events. Legal enforcement relies on untested UCC Article 7 application. | 3 | 3 | Non-Improvable | [P1] Stablewatch: ITAD costs, legal risks, [P1] Full docs: default mechanics |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage on depositor side. Borrowers get 70-80% LTV loans but this is borrower leverage, not depositor. No rehypothecation of USDai into multiple venues. | 9 | 9 | Non-Improvable (optimal) | [P1] Full docs: 70-80% LTV, no depositor leverage |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- sUSDai is not a lending protocol with depositor LTV. Borrower LTV managed through amortization (3-year schedule). Defaults handled off-chain via ITAD. | N/A | N/A | N/A | - |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No confirmed permanent-loss events for USD.ai or MetaStreet since launch (Aug 2025). MetaStreet v2 NFT lending has operated since 2023 without reported losses. ~8 months operational history. | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama: no loss events, [P1] MetaStreet track record |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Comprehensive framework: CALIBER collateral tokenization, FiLo first-loss model, LTV limits (70-80%), DSRA (~3 months coverage), aggressive 3-year amortization, mandatory insurance, borrower KYC/KYB via iDenfy. Quantitative limits published. | 9 | 9 | Non-Improvable (optimal) | [P1] Full docs: CALIBER, FiLo, risk mitigation table |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Current APR 6.84%, expected 12.18%. T-bill floor (~4.5%) partially from PayPal PYUSD incentive (4.5% up to $1B in 2026 -- time-limited). Loan interest (7-15%) is organic. Allo points program active. PayPal incentive is temporary; organic loan yield alone would be sustainable but lower. 30-70% incentive dependency plausible. | 3 | 3 | Non-Improvable | [P1] sUSDai page APR, [P1] Full docs: PYUSD 4.5% incentive, Allo points |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | sUSDai: 30-day redemption epochs. Loan repayments ~3-4% monthly of deployed principal. Full unwind requires loan maturities (3-year amortization). Under stress, significant portion locked. 2-5% slippage via QEV auction premiums plausible. | 3 | 3 | Non-Improvable | [P1] Full docs: 30-day epochs, 3-year amortization, QEV |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | USDai peg maintained by M0 backing. sUSDai yield depends on loan interest spread. If GPU demand collapses, yield drops to T-bill floor. Spread inversion unlikely to cause permanent losses. <30% from invertible spreads. | 9 | 9 | Non-Improvable (optimal) | [P1] Full docs: yield structure, T-bill floor |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | STRATEGY_ADMIN_ROLE deploys capital -- human-initiated multisig per docs. No permissionless external functions increasing exposure. All allocation requires admin. | 9 | 9 | Non-Improvable (optimal) | [P1] Technical overview: STRATEGY_ADMIN_ROLE |

**Protocol Mechanics Subtotal:**
- Scored questions (9 of 10, ST-PM-04 N/A): 3+3+9+9+9+3+3+9+9 = 57/81
- Adjusted: (57/81) x 45 = **31.7/45 (70.4%)**

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Collateral: NVIDIA enterprise GPUs (B300, B200, H200, RTX Pro 6000). Physical hardware with illiquid secondary markets, rapid technology obsolescence, ~30% ITAD liquidation costs. However: explicitly tiered with conservative LTVs (70-80%), mandatory insurance (Alliant, Barkr), aggressive amortization. Meets Mid criteria: "higher risk assets BUT each explicitly tiered with conservative LTVs and strict exposure caps." | 3 | 3 | Non-Improvable | [P1] Full docs: GPU types, LTV, insurance, ITAD costs |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | GPU hardware depreciates (not "depegs"). Subject to rapid depreciation during NVIDIA product transitions (annual cycles). Protocol uses 3-year amortization vs industry 5-7 years as buffer. No specific stress data during protocol operation. Geopolitical export controls removed China as secondary buyer, creating supply risk. | 3 | 3 | Non-Improvable | [P1] Stablewatch: hardware depreciation, CUDA erosion, export controls |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- not a staking-based protocol. | N/A | N/A | N/A | - |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | USDai backed by M0's $M token (T-bill wrapper). Cross-chain via LayerZero OFT. Primary TVL on Arbitrum uses canonical bridge. PYUSD natively issued. M0's $M is indirect wrapped exposure but not traditional bridge token. <20% direct bridge dependency. | 9 | 9 | Non-Improvable (optimal) | [P0] Arbiscan: USDai on Arbitrum, [P1] LayerZero OFT docs |

**Collateral Subtotal:**
- Scored questions (3 of 4, ST-C-03 N/A): 3+3+9 = 15/27
- Adjusted: (15/27) x 45 = **25.0/45 (55.6%)**

#### Infra Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Chain: Arbitrum (Tier-2 per SR). Bridge: LayerZero OFT (Tier-1). Oracle: Chainlink (Tier-0). Wallet: undisclosed multisig. Dependencies listed but includes Tier-2 chain. | 3 | 3 | Non-Improvable | [P0] Contracts on Arbitrum, [P1] Chainlink oracle 0xd40a, LayerZero OAdapter |
| ST-IC-02 | How redundant are oracle and bridge setups, and can oracle values be corrected under abnormal conditions? | Chainlink Price Oracle (Tier-0) at 0xd40a... for exchange rate. Cantina noted "missing price staleness validation" (informational). Single oracle, no fallback. Chainlink values updatable (not hardcoded). Single primary Tier-0 without fallback. | 3 | 9 | **Improvable** | [P0] Oracle contract 0xd40a, [P1] Cantina: staleness check missing |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Critical off-chain: GPU Finance Ltd. (Administrative Agent), Wilmington Trust (escrow -- major regulated institution, SOC expected), Aravolta (monitoring), iDenfy (KYC). Wilmington Trust is well-established. No SOC 2/ISO27001 status disclosed for GPU Finance Ltd. or Aravolta specifically. | 3 | 9 | **Source Missing** | [P1] Full docs: provider names, [P1] No certification details for custom providers |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Protocol >6 months operational (Aug 2025). No reported infrastructure incidents. Arbitrum stable during this period. Per framework: >=6 months with no incidents = Low. | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama: no outage events |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Arbitrum One: no chain halt or consensus failure >30 minutes in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P3] L2Beat Arbitrum status |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- not a staking/LST protocol. | N/A | N/A | N/A | - |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- not a staking/LST protocol. | N/A | N/A | N/A | - |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | sUSDai redemptions depend on STRATEGY_ADMIN calling serviceRedemptions(). If admin multisig becomes unavailable, FIFO queue processing stops entirely. Users cannot directly redeem sUSDai without admin. Single point of failure for sUSDai exit path. USDai itself may have separate redemption path. | 1 | 3 | **Improvable** | [P1] Technical overview: serviceRedemptions() admin dependency |

**Infra Counterparty Subtotal:**
- Scored questions (6 of 8, ST-IC-06/07 N/A): 3+3+3+9+9+1 = 28/54
- Adjusted: (28/54) x 45 = **23.3/45 (51.9%)**

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | MetaStreet lending pools (not on SR protocol tiers but >12 months, >$50M TVL). M0 Protocol (not on tier list but >12 months, >$150M). GPU Finance Ltd. (custom RWA platform). Most venues disclosed with partial tiering; established but untiered venues used. | 3 | 3 | Non-Improvable | [P1] Full docs: MetaStreet, M0, GPU Finance Ltd. |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | PayPal PYUSD incentive: 4.5% on up to $1B (2026). Creates incentive to hold PYUSD vs deploy into higher-yield loans. Allo points rewards USDai (5x) and sUSDai (2x). Arrangements partially disclosed; conflict analysis limited. | 3 | 9 | **Improvable** | [P1] Full docs: PYUSD incentive terms, Allo points |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | LTV limits (70-80%) per loan. DSRA (~10%). FiLo first-loss per curator. No documented hard caps on total allocation to single borrower, curator, or data center. Stage 2 target 20-30% GPU is guideline, not enforced cap. | 3 | 9 | **Improvable** | [P1] Full docs: LTV limits, DSRA, FiLo |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | GPU loans: 3-year amortization, monthly repayments ~3-4% of principal. No early termination documented. Default triggers off-chain ITAD process with ~30% costs. M0/PYUSD: instant (T+1). GPU positions cannot be unwound quickly -- structural constraint. | 1 | 1 | Non-Improvable | [P1] Full docs: 3-year amortization, ITAD process |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | GPU Finance Ltd., Wilmington Trust, Aravolta, Alliant Insurance, Barkr, iDenfy, ITAD partners all named. Roles described but oversight controls and sub-provider details at aggregate level. | 3 | 9 | **Improvable** | [P1] Full docs: all providers named with roles |

**Protocol Counterparty Subtotal:**
- Raw scores: 3+3+3+1+3 = 13/45
- Adjusted: (13/45) x 45 = **13.0/45 (28.9%)**

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | USDai: instant redemption per website. sUSDai: ERC-7540 async via requestRedeem(), processed in 30-day FIFO epochs by admin serviceRedemptions(). Admin can pause via PAUSE_ADMIN_ROLE. Blacklist exists with bypass vulns. Redemptions depend on admin processing. | 3 | 9 | **Improvable** | [P1] Technical overview: ERC-7540, FIFO, [P1] Cantina: blacklist bypass |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Stated: 30-day epochs. Current: ~$300M in PYUSD/T-bills (highly liquid). If loans deployed (target 20-30%), 70-80% liquid. Monthly loan repayments ~3-4%. Currently mostly liquid -- near-total exit within 30 days feasible. | 9 | 9 | Non-Improvable (optimal) | [P0] DeFiLlama: $300M PYUSD in protocol |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | ~8 months operational. No reported delays/freezes in docs, forums, or news. Protocol young, not stress-tested. Per scoring principle: untested = Mid (3). | 3 | 9 | Non-Improvable | [P3] No reported delays, [P4] No news of freezes |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | 30-day epoch batching limits timing. No documented per-epoch caps. Redemptions constrained by vault cash. Currently mostly liquid so caps unlikely to bind. But structural design could restrict if loans deployed. | 3 | 3 | Non-Improvable | [P1] Technical overview: serviceRedemptions(), cash availability |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Not tested under stress. Protocol launched Aug 2025, no significant stress event. 30-day epoch provides buffer against panic. Untested = Mid (3). | 3 | 3 | Non-Improvable | [P1] No stress history |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | Stated: 30-day epochs. Underlying GPU loans: 3-year amortization. Target 20-30% in loans. Monthly repayments ~3-4% of deployed. >10% locked longer than withdrawal terms when loans deployed. | 1 | 1 | Non-Improvable | [P1] Full docs: 3-year amortization, 3-4% monthly |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Primary: in-protocol FIFO queue (30-day). Secondary: sUSDai on Fluid ($528K/day) + Curve ($468K/day) = ~$1M/day. Users can exit via secondary if unwilling to wait. Secondary optional but thin for large exits. | 3 | 3 | Non-Improvable | [P3] CoinGecko: sUSDai 24h volume ~$1.15M |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | sUSDai: ~$1.1M daily volume, $159M market cap = ~0.3% of TVL absorbable. Well below 3% threshold for Mid. USDai: higher transfer volume but concentrated in protocol operations. Thin secondary for both. | 1 | 3 | Non-Improvable | [P3] CoinGecko: sUSDai volume, [P3] RWA.xyz: USDai data |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Currently mostly T-bills (liquid). If all capital deployed and mass redemption, FIFO extends well beyond 30 days. But current state: liquid reserves sufficient. QEV (planned) prices urgency. No forced liquidation. Current buffers adequate; future deployment increases risk. | 3 | 3 | Non-Improvable | [P1] Full docs: no forced liquidation, QEV planned |

**Liquidity Subtotal:**
- Raw scores: 3+9+3+3+3+1+3+1+3 = 29/81
- Adjusted: (29/81) x 45 = **16.1/45 (35.8%)**

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | sUSDai is yield-bearing vault token. ATH $1.19 (Aug 2025), ATL $0.7961 (Sep 2025) per CoinGecko -- >20% deviation from expected ~$1.0x NAV. This was during first month of trading on thin liquidity. Since stabilized at ~$1.08. Early deviation severe (>10%) but likely thin-market artifact. Real stress history too short. | 1 | 3 | Non-Improvable | [P3] CoinGecko: ATL $0.7961, current $1.08 |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | sUSDai yield from GPU loans -- no direct crypto market exposure. Collateral is physical hardware. USDai peg by M0/T-bill backing. Strategy low-beta/non-directional to crypto. | 9 | 9 | Non-Improvable (optimal) | [P1] Full docs: GPU loans, T-bill backing |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | GPU loan rates (7-15%) contractually fixed. No utilization-based rate curve. T-bill yield varies with macro rates. No reflexive incentive mechanisms. No history of rate distortion. | 9 | 9 | Non-Improvable (optimal) | [P1] Full docs: fixed loan rates |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | CALIBER framework with aggressive amortization. Stablewatch covers GPU depreciation, CUDA erosion, export controls. No formal published stress test with quantified max-loss. Partial coverage. | 3 | 9 | **Improvable** | [P1] Full docs: risk framework, [P4] Stablewatch deep dive |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | No leverage on depositor side. No on-chain liquidation mechanism. Defaults handled off-chain via ITAD. No cascading liquidation risk. | 9 | 9 | Non-Improvable (optimal) | [P1] Full docs: no leverage, ITAD |

**Market Subtotal:**
- Raw scores: 1+9+9+3+9 = 31/45
- Adjusted: (31/45) x 45 = **31.0/45 (68.9%)**

**Strategy Total: 31.7 + 25.0 + 23.3 + 13.0 + 16.1 + 31.0 = 140.1/270 (51.9%)**

---

### OPERATIONS (30% Weight) -- Score: 139.8/270 (51.8%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | CHIP Governor (0x0DDC...) and TimelockController (0x0EEC...) deployed on Arbitrum. Token TGE March 30, 2026 (~3.5 weeks ago). No governance proposals executed yet. Currently multisig controls operations with stated intent to transition to on-chain governance. Hybrid model. | 3 | 9 | **Improvable** | [P0] Chip Governor, TimelockController on Arbiscan, [P1] CHIP governance scope |
| O-G-02 | How concentrated is voting power among top holders or delegates? | CHIP token ~3.5 weeks old (TGE March 30, 2026). No governance voting history. Distribution partially disclosed (27.5% ecosystem, 19.5% reserve). Core contributors and investors locked 12 months. Actual voting power concentration cannot be determined. | 1 | 9 | **Improvable** | [P1] Tokenomics: distribution percentages, [P0] No on-chain voting data |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Two independent TimelockControllers fully verified on-chain. Governance Timelock (0x0EEC...8221): minDelay = 3 days. Chip Governor (0x0DDC...) holds both PROPOSER_ROLE and EXECUTOR_ROLE on it (hasRole()=true). Upgrade Timelock (0x0eEA...639b): minDelay = 1 day, owns both ProxyAdmins. All major admin/upgrade actions go through a timelock. Parameters fully specified and verifiable. | 9 | 9 | Non-Improvable (optimal) | [P0] Governance Timelock getMinDelay()=259200 verified, [P0] Chip Governor hasRole(PROPOSER)=true and hasRole(EXECUTOR)=true on Doc Timelock, [P0] Upgrade Timelock getMinDelay()=86400 |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Applicable (vault product). STRATEGY_ADMIN can theoretically be replaced via governance/multisig. But sUSDai redemptions depend on admin calling serviceRedemptions(). Replacement during transition may pause queue processing briefly. Process not documented. | 3 | 9 | **Improvable** | [P1] Technical overview: STRATEGY_ADMIN dependency |

**Governance Subtotal:**
- Raw scores: 3+1+9+3 = 16/36
- Adjusted: (16/36) x 67.5 = **30.0/67.5 (44.4%)**

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Co-founders: David Choi (CEO, Deutsche Bank, Taureon), Conor Moore (COO, Rockpoint, Eastdil), Ivan Sergeev (CTO, MIT, DRW, 21.co). All publicly identified with verifiable backgrounds. No credibility red flags. | 9 | 9 | Non-Improvable (optimal) | [P2] STEP application: team bios, [P4] crypto-fundraising.info, [P1] LinkedIn |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Permian Labs: 3 co-founders + team (raised $38M). Builds both MetaStreet and USD.ai. Multiple engineers. But exact team size undisclosed. Small but not single-person. | 3 | 9 | **Improvable** | [P4] crypto-fundraising.info: $38M raised, [P2] STEP application |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | USD.AI Foundation (Cayman Islands Foundation Company). GPU Finance Ltd. (subsidiary, Administrative Agent). Permian Labs (Delaware corp, technical services). Clara Formations (Cayman) as formation agent. Entities clearly named and mapped to responsibilities. | 9 | 9 | Non-Improvable (optimal) | [P2] STEP application: entity details, [P1] Full docs: entity structure |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known enforcement actions in any major jurisdiction. Stablewatch notes "high likelihood" sUSDai classified as security but no actual regulatory action. | 9 | 9 | Non-Improvable (optimal) | [P4] No enforcement actions found, [P4] Stablewatch analysis |
| O-TL-05 | Is there an on-call and incident response process for core teams? | No documented on-call or incident response process. No runbooks. STRATEGY_ADMIN manages off-chain operations. No documented procedures to halt loan deployment during incidents. | 1 | 9 | **Improvable** | [P1] docs.usd.ai -- no incident response page |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Support via Telegram (t.me/usdaiofficial), Twitter (@USDai_Official). STEP application mentions quarterly reporting. No structured ticket system or SLA documented. Response times inconsistent based on public channels. | 3 | 9 | **Improvable** | [P1] docs.usd.ai: social links, [P2] STEP application |
| O-TL-07 | Are major investors or strategic partners disclosed? | Investors fully disclosed: Framework Ventures (lead), Dragonfly, YZi Labs, DCG, Coinbase Ventures, Arbitrum Foundation, Bullish, Flowdesk, CMT Digital, Big Brain Holdings. Roles/governance influence not fully detailed. | 3 | 9 | **Improvable** | [P4] crypto-fundraising.info: investor list |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Permian Labs operates MetaStreet (NFT lending) and USD.ai (GPU lending). Different markets/collateral types. No obvious competing vault strategies. Other mandates partially disclosed. | 3 | 9 | **Improvable** | [P1] MetaStreet docs, permianlabs.xyz |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | No known collateral loss events for Permian Labs or MetaStreet in last 24-36 months. MetaStreet v2 (NFT lending) since 2023 without reported losses. | 9 | 9 | Non-Improvable (optimal) | [P1] MetaStreet track record, [P3] DeFiLlama |

**Team & Legal Subtotal:**
- Raw scores: 9+3+9+9+1+3+3+3+9 = 49/81
- Adjusted: (49/81) x 67.5 = **40.8/67.5 (60.5%)**

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Comprehensive docs at docs.usd.ai: technical overview, CALIBER framework, FiLo model, loan structure, legal documentation, risk framework. Updated through Mar 2026 (audits). Whitepaper-equivalent content published. | 9 | 9 | Non-Improvable (optimal) | [P1] docs.usd.ai comprehensive structure |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | End-to-end collateral flow documented: USDai -> LoanRouter -> MetaStreet pools -> GPU loans. Loss scenarios: borrower default, GPU depreciation, ITAD recovery costs, FiLo first-loss absorption. Clear triggers tied to strategy. | 9 | 9 | Non-Improvable (optimal) | [P1] Full docs: collateral flow, default mechanics |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Single canonical page at docs.usd.ai/technical-overview/contract-addresses. Lists all core contracts for Arbitrum (hub), Ethereum, Base, Plasma. Includes token, oracle, router, escrow, timelock, governor addresses. Updated on each deployment. | 9 | 9 | Non-Improvable (optimal) | [P1] docs.usd.ai/technical-overview/contract-addresses |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | STRATEGY_ADMIN_ROLE, BRIDGE_ADMIN_ROLE, PAUSE_ADMIN_ROLE documented in technical overview. Role holders (addresses) NOT disclosed. No change history. Roles defined but not fully transparent. | 3 | 9 | **Improvable** | [P1] Technical overview: role definitions, [P1] No role addresses |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Website states "on-chain proof of reserves ensures transparency at all times." app.usd.ai/reserves referenced. Monthly audit cadence stated. DeFiLlama shows $300M PYUSD. But detailed PoR methodology not published. Liabilities (outstanding loans) partially visible via on-chain records. PoR exists but coverage incomplete. | 3 | 9 | **Improvable** | [P1] Website: PoR claim, [P3] DeFiLlama: TVL composition |
| O-DT-06 | Are all contracts verified on the leading block explorers? | USDai and sUSDai verified on Arbiscan (source code verified, exact match). ERC-1967 proxy + implementation both verified. Solidity v0.8.29, Cancun EVM. Other contracts (Oracle, LoanRouter, etc.) listed but individual verification not checked. Core contracts verified. | 9 | 9 | Non-Improvable (optimal) | [P0] Arbiscan: USDai, sUSDai verified |

**Documentation Subtotal:**
- Raw scores: 9+9+9+3+3+9 = 42/54
- Adjusted: (42/54) x 67.5 = **52.5/67.5 (77.8%)**

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | CHIP staking as "first loss module" per docs. DSRA (~10% per loan) provides per-loan backstop. FiLo curators absorb first-loss. Insurance (Alliant, Barkr) covers collateral. Multiple layers but CHIP module nascent (token ~3.5 weeks old). Activation rules discretionary. | 3 | 9 | **Improvable** | [P1] CHIP page: first loss module, [P1] Full docs: DSRA, FiLo, insurance |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | DeFiLlama treasury API returned 400 (no data). No disclosed DAO treasury wallet addresses. CHIP token ~3.5 weeks old -- no treasury accumulation yet. Protocol revenue ~$21.5M annualized (DeFiLlama). Treasury composition and size unknown. <1% of TVL. | 1 | 9 | **Improvable** | [P3] DeFiLlama: no treasury data, [P1] No treasury disclosure |
| O-FR-03 | What is the estimated operational runway at current burn? | $38M+ raised (Aug 2025 Series A + other rounds). $19.4M from CHIP public sale (Mar 2026). $21.5M annualized revenue. Burn rate undisclosed but with $57M+ in funding and growing revenue, runway likely >24 months. Cannot fully confirm from disclosed information. | 3 | 9 | **Improvable** | [P4] crypto-fundraising.info: funding rounds, [P3] DeFiLlama: revenue |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | No major stress event. TVL grew 0 -> $687M peak (Sep 2025) then settled ~$300M. Decline was orderly. Revenue growing ($21.5M annualized). No depositor haircuts or emergency actions. Young protocol, untested. | 3 | 3 | Non-Improvable | [P3] DeFiLlama: TVL history |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | serviceRedemptions() requires admin. Off-chain loans managed by GPU Finance Ltd. Without team: redemption queue stops, loan servicing uncertain, contract upgrades frozen. Users cannot exit sUSDai permissionlessly. Critical off-chain dependencies. | 1 | 9 | **Improvable** | [P1] Technical overview: admin dependencies |

**Financial Resilience Subtotal:**
- Raw scores: 3+1+3+3+1 = 11/45
- Adjusted: (11/45) x 67.5 = **16.5/67.5 (24.4%)**

**Operations Total: 30.0 + 40.8 + 52.5 + 16.5 = 139.8/270 (51.8%)**

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 77 | 99 | 140.0 | 180 | 77.8% |
| | Key Management (8 Q) | 28 | 72 | 70.0 | 180 | 38.9% |
| | **Security Subtotal** | | | **210.0** | **360** | **58.3%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 57 | 81 | 31.7 | 45 | 70.4% |
| | Collateral (3 of 4 Q scored) | 15 | 27 | 25.0 | 45 | 55.6% |
| | Infra Counterparty (6 of 8 Q scored) | 28 | 54 | 23.3 | 45 | 51.9% |
| | Protocol Counterparty (5 Q) | 13 | 45 | 13.0 | 45 | 28.9% |
| | Liquidity (9 Q) | 29 | 81 | 16.1 | 45 | 35.8% |
| | Market (5 Q) | 31 | 45 | 31.0 | 45 | 68.9% |
| | **Strategy Subtotal** | | | **140.1** | **270** | **51.9%** |
| **Operations** | Governance (4 Q) | 16 | 36 | 30.0 | 67.5 | 44.4% |
| | Team & Legal (9 Q) | 49 | 81 | 40.8 | 67.5 | 60.5% |
| | Documentation (6 Q) | 42 | 54 | 52.5 | 67.5 | 77.8% |
| | Financial Resilience (5 Q) | 11 | 45 | 16.5 | 67.5 | 24.4% |
| | **Operations Subtotal** | | | **139.8** | **270** | **51.8%** |
| **TOTAL** | | | | **489.9** | **900** | **54.4%** |

---

