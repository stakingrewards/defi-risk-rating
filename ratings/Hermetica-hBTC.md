# Hermetica - hBTC Risk Rating

**Rating Date**: 2026-03-23
**Final Grade**: CCC-
**Total Score**: 481.2/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-alpha

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 244.1/360 (67.8%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. hBTC vault contracts audited by two independent firms: Clarity Alliance (Jan 2026, 52 findings covering vault architecture, yield strategies, fee calculations, and token integration) and Greybeard Security (Nov 2025). Audit counting: Clarity Alliance = 1 independent audit, Greybeard Security = 1 independent audit = 2 total. | 9 | 9 | Non-Improvable (optimal) | [P1] Clarity Alliance Vaults audit (Jan 27, 2026): https://clarity-alliance.github.io/audits/Clarity%20Alliance%20-%20Hermetica%20Vaults.pdf; [P3] Greybeard Security hBTC audit (Nov 2025): https://github.com/greybeard-security/audit-reports |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent audit by Clarity Alliance (Jan 2026). Clarity Alliance is a Stacks/Clarity ecosystem specialist with $1B+ TVL secured, 90+ High/Critical vulnerabilities discovered, and clients including Stacks, Bitflow, StackingDAO, and Zest. Classified as **Tier-2** — emerging auditor with real domain expertise and meaningful track record, but niche to the Stacks ecosystem with limited sample outside it. Second auditor StrataLabs (now Greybeard Security) is a two-person team with only 3 public audits (Bitflow, Hermetica hBTC, Zest v2, all late 2025). Classified as **Tier-3** — very new firm with minimal track record. Highest-tier auditor is Tier-2. Score Mid (3): "Most recent audit by only Tier-2 or Tier-3 auditors." | 3 | 9 | **Improvable** | [P1] Clarity Alliance website: https://www.clarityalliance.org/; [P3] Greybeard Security GitHub: https://github.com/greybeard-security (3 audit reports); Framework classification: Clarity Alliance = Tier-2, Greybeard Security = Tier-3 |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | The hBTC vault is a new deployment (2025-2026) audited by both Clarity Alliance (Jan 2026) and Greybeard Security (Nov 2025) before/during deployment. No upgrades to hBTC core contracts have occurred since launch, so there are no unaudited upgrades. Score Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] Clarity Alliance Vaults audit (Jan 27, 2026); [P3] Greybeard Security hBTC audit (Nov 2025); No hBTC upgrades post-deployment |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | The Clarity Alliance hBTC vault audit (Jan 2026) found 4 High, 10 Medium, 17 Low, 21 QA findings (52 total). The full audit report confirms ALL 4 High findings (H-01: fee calculation error, H-02: reward profit handling, H-03: excess loss handling, H-04: covered loss handling) are marked "Resolved." All 10 Medium findings also "Resolved." A "Final Commit After Remediations" (135b453e...) was reviewed, plus 13 subsequent PRs. Only 2 Low/QA findings "Acknowledged" (L-01, QA-01), 1 "Partially Resolved" (L-06). Score Low (9): all critical and high-severity findings fully remediated and re-verified by the auditor. | 9 | 9 | Non-Improvable (optimal) | [P1] Clarity Alliance Vaults audit report pp.13-16: Summary of Findings table shows all H/M resolved; Final commit 135b453e reviewed; 13 subsequent PRs reviewed |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Clarity (Stacks) smart contracts are NOT upgradeable in the traditional proxy pattern sense -- Clarity is decidable and not Turing-complete. However, the Owner role (3-of-6 multisig) can modify critical protocol settings with a documented 24h timelock. Role assignments are also timelocked. Emergency freeze mechanism exists. The governance model documents upgrade constraints clearly. Score Low (9): upgradeable only via governance/multisig with timelock >=24h, narrow upgrade roles, and public upgrade policy. | 9 | 9 | Non-Improvable (optimal) | [P1] Docs governance page: 3-of-6 multisig, 24h timelock; [P1] Clarity language properties: decidable, not Turing-complete; hBTC governance docs |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss for hBTC. The hBTC vault has been operational since 2025. No incidents reported on Rekt.news or other exploit trackers. | 9 | 9 | Non-Improvable (optimal) | [P4] No exploit found on Rekt.news; [P1] No incident disclosures in docs; [P3] DeFiLlama shows no TVL collapse events |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No confirmed rug-pull. Founder Jakob Schillinger publicly identified. $1.7M seed raised from UTXO Management, CMS Holdings, Newman Capital. No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P4] TheBlock seed funding article; [P2] Crunchbase/Tracxn company profile; [P1] LEI registration: Hermetica Labs Inc, Panama |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | Documentation states 24h timelock on critical changes. No evidence of timelock reductions. Protocol is relatively new, so limited history to evaluate. Score Low (9): No reductions identified. | 9 | 9 | Non-Improvable (optimal) | [P1] Governance docs specify 24h timelock; No evidence of changes |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | No active bug bounty found on Immunefi, Code4rena, Sherlock, HackerOne, or any established platform. No self-hosted bounty page identified. | 1 | 9 | **Improvable** | [P3] Searched Immunefi -- no Hermetica listing; [P1] No bounty mentioned in docs |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | No structured monitoring or alerting systems documented. The protocol mentions "automated off-chain service continuously monitors LTV" for risk controls, but this is operational monitoring, not security monitoring (no mention of Hypernative, Blockaid, or similar services). No documented invariant monitoring, anomaly detection, or on-call security response. | 1 | 9 | **Improvable** | [P1] Risk controls docs mention LTV monitoring only; No security monitoring provider disclosed |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | The Guardian role can pause protocol functionality via the 3-of-6 multisig. An emergency mechanism freezes the protocol and allows safe withdrawal of assets. The interest spread control automatically closes/reduces positions after 2 consecutive days of negative spread. These are rules-based but require manual multisig execution for pause. Score Mid (3): manual triggers required but procedures documented. | 3 | 9 | **Improvable** | [P1] Governance docs: Guardian can pause; emergency freeze mechanism; [P1] Risk controls: automated spread-based position management |

**Smart Contract Security Subtotal:**
- Raw: 9+3+9+9+9+9+9+9+1+1+3 = 71/99
- Weighted: (71/99) x 180 = 129.1

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Owner role held by 3-of-6 multisig at SM1QXYXZG78DCWJZJKY0901KTK3350071W9YYRPMT. Role changes and security-sensitive settings subject to 24h timelock. Operator roles (Trader, Manager, Rewarder, Fee Setter) at SP20V8SG811G6CT2QMZQNX6XCN20YAX36DYD1BAE0 have strictly bounded permissions -- cannot move funds arbitrarily. Audit confirms two-step admin procedure for adding admins (L-14). All roles and permissions documented in governance docs. Protocol is new with no role changes to evaluate. Score Low (9): "Admin/upgrade rights held by diversified multisig or governance." 3-of-6 with 24h timelock exceeds the Mid (3) criteria of "small multisig (2-of-N)." | 9 | 9 | Non-Improvable (optimal) | [P1] Governance docs: Owner at SM1QXY..., 3-of-6 multisig, 24h timelock; [P1] Audit L-14: two-step admin procedure confirmed; Bounded operator roles documented |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No single key can move user funds -- 3-of-6 multisig required. Threshold is 3 and total signers is 6. Criteria for Low (9): "threshold >=3 AND total signers >=5 AND timelock >=24h." 3-of-6 with 24h timelock meets all three criteria. However, the timelock is documented but not independently verified on-chain (Stacks explorer did not return contract data). Score Mid (3) due to unverified on-chain timelock. | 3 | 9 | **Source Missing** | [P1] Governance docs: 3-of-6 multisig, 24h timelock claimed; [P0] Stacks explorer: unable to independently verify timelock on-chain |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | 3-of-6 multisig documented. Signer identities are NOT publicly disclosed -- no ENS names, no public signer list, no governance documentation identifying individual signers. Per criteria: "If signer identities are fully unknown, independence cannot be confirmed -- score Mid (3) at best." The structural setup (3-of-6) is adequate, but independence cannot be verified. Score Mid (3): structural multisig exists but unknown signers cap the score at Mid. | 3 | 9 | **Source Missing** | [P1] Governance docs disclose multisig address but not individual signer identities; No public signer disclosure found |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Guardian role can pause protocol, same 3-of-6 multisig as Owner. Emergency freeze available. No documented address-level withdrawal censorship capability. Pause is protocol-wide via multisig. Rules partially documented. Score Mid (3): "Pause/controls exist with broad scope but require multisig and are at least partially documented." | 3 | 9 | **Improvable** | [P1] Governance docs: Guardian can pause; emergency freeze mechanism |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | 100% of hBTC user assets are held in non-custodial on-chain smart contracts. The audit report (Section 4) confirms: "Self-custodial: Assets move only via protocol smart contracts." The hBTC overview states "no centralized custodians." Asset flow: sBTC deposited → vault contract → posted as collateral on Zest (on-chain) → borrow USDh (on-chain) → stake USDh into sUSDh (on-chain). All steps are on-chain Stacks Clarity contracts reviewed by the auditor. Copper/Ceffu custody mentioned in the basis strategy docs applies to the USDh protocol's yield generation layer (backing the basis trade), NOT to hBTC user asset custody. This off-chain dependency is a counterparty risk (captured in ST-PC/ST-IC), not a custody issue. Score Low (9): "100% of user assets held in non-custodial on-chain contracts." | 9 | 9 | Non-Improvable (optimal) | [P1] Audit report Section 4: "Self-custodial: Assets move only via protocol smart contracts"; [P1] hBTC overview: "no centralized custodians"; [P1] Audit scope: all contracts are on-chain Clarity contracts |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | The hBTC architecture enforces on-chain segregation through separate smart contracts: user funds in vault-v1 and reserve-v1, PnL buffer in reserve-fund-v1, fees in fee-collector-v1, and accounting in controller-v1/state-v1 (which don't hold funds). All six contracts were independently reviewed by the Clarity Alliance audit. L-12 (missing auth check on reserve fund transfers) was Resolved, adding extra validation to the already-separate reserve-fund contract. Score Low (9): "Clear on-chain segregation of user funds vs treasury/ops; no co-mingling." Segregation is enforced at the smart contract architecture level. | 9 | 9 | Non-Improvable (optimal) | [P1] Audit scope: separate contracts for vault, reserve, reserve-fund, fee-collector; [P1] L-12 reserve fund auth check Resolved; On-chain contract-level segregation |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | Governance docs specify allowed external integrations: Zest Protocol and Hermetica USDh Protocol. Assets authorized: sBTC, USDh, sUSDh. Changes to externals/assets require Owner multisig (3-of-6) with 24h timelock. Whitelist is on-chain enforced in the contract code (confirmed by Clarity Alliance audit which reviewed all interface contracts). Clarity contracts are readable on-chain providing inherent transparency. Only 2 protocols whitelisted, aligned to mandate. Score Low (9): "On-chain enforced whitelist aligned to mandate; additions/removals require governance/multisig with timelock." All criteria met. | 9 | 9 | Non-Improvable (optimal) | [P1] Governance docs: Externals = Zest Protocol + Hermetica USDh; timelocked changes via Owner multisig; [P1] Clarity Alliance audit confirms on-chain whitelist enforcement in zest-interface-v1.clar and hermetica-interface-v1.clar |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No publicly documented incident playbook. Emergency freeze mechanism exists for owner compromise, allowing safe withdrawal of assets. However, no formal key-rotation procedures, pre-authorized safe addresses, or evidence of tabletop exercises. | 1 | 9 | **Improvable** | [P1] Emergency freeze documented in governance; No formal playbook found |

**Key Management Subtotal:**
- Raw: 9+3+3+3+9+9+9+1 = 46/72
- Weighted: (46/72) x 180 = 115.0

---

### **Security Total: 129.1 + 115.0 = 244.1/360 (67.8%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 129.1 | 180 | 71.7% |
| Key Management | 115.0 | 180 | 63.9% |
| **Security Total** | **244.1** | **360** | **67.8%** |

---

### STRATEGY (30% Weight) -- Score: 114.4/270 (42.4%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield comes from: (1) basis trade -- funding rate payments from perpetual futures on Binance, Bybit, OKX, Bitget via delta-neutral BTC/short perp position, (2) BTC-native staking yield via Zest lending. Mandate is "Bitcoin that earns Bitcoin." Yield sources align with BTC-denominated yield generation. Backtest average APY: 10.56% (Jan 2021 - Sep 2025). Percent breakdown between basis and staking yield not explicitly provided. Score Mid (3): "Main yield sources listed but percent breakdown incomplete." | 3 | 9 | **Improvable** | [P1] Basis strategy docs: funding rates from 4 exchanges; [P1] Historical performance: 10.56% avg APY backtest; [P1] hBTC overview: borrow USDh, stake, harvest to BTC |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Negative yield occurs when funding rates are persistently negative (backtest: 5.9% negative days). Additional loss conditions: exchange failure (Copper/Ceffu counterparty risk), liquidation at 70-75% LTV, sBTC bridge failure. Reserve fund covers negative funding periods but is "not a guarantee against loss." These are severe but plausible single-shock events. Score Mid (3). | 3 | 3 | Non-Improvable | [P1] Risk controls: liquidation at 70%/75% LTV; [P1] Historical: 5.9% negative yield days; [P1] Reserve fund disclaimer |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | The strategy uses leverage: LTV target 50% (cap 51%, floor 49%). This implies ~2x effective leverage (borrow 50% of collateral value). LTV is enforced by automated off-chain monitoring. Score Mid (3): "Moderate leverage with enforceable caps above 1.2x and up to 3x." | 3 | 3 | Non-Improvable | [P1] Risk controls: LTV Cap 51%, Target 50%, Floor 49%; Partial liquidation at 70%, full at 75% |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | Automated off-chain service monitors LTV continuously. Thresholds defined: Cap 51%, partial liquidation at 70%, full at 75%. The gap between target (50%) and liquidation (70%) provides 20% buffer. Delta exposure controlled within 0.999-1.001 band. Interest spread control auto-closes positions after 2 days negative. Current LTV target is well below 0.70 of liquidation threshold (50% vs 70% = 0.71). Score Mid (3): "Some automated protections exist but rely on partial manual intervention." | 3 | 9 | **Improvable** | [P1] Risk controls: LTV monitoring, delta control, spread control; Automated but off-chain |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | The basis trade/delta-neutral strategy is used by Ethena (USDe/sUSDe) which is a close comparable variant. Ethena has not experienced permanent loss events, though funding rates have turned negative. Hermetica backtest shows 5.9% negative yield days but reserve fund covers these. No permanent-loss events for hBTC or comparable variant. Score Low (9) with caveat that hBTC is very new. | 9 | 9 | Non-Improvable (optimal) | [P1] Historical backtest: 5.9% negative days covered by reserve; [P4] Ethena comparable -- no permanent losses |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Risk controls documented with quantitative limits: LTV caps (49-51%), delta exposure band (0.999-1.001), interest spread rules (2-day trigger), reserve fund capitalization (5% of daily rewards, 10bp minimum). Change-control procedures via timelocked governance. This is a formal framework with quantitative limits. Score Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] Risk controls page with quantitative thresholds for leverage, delta, spread, and reserve |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yield is primarily from funding rates (organic -- paid by perpetual futures traders). Backtest avg 10.56% APY. No token emissions or incentive programs drive hBTC yield. However, funding rates are cyclical -- 2023 bear: 1.83% APY. Yield is organic but market-dependent. Score Low (9): primarily organic, <30% from incentives. | 9 | 9 | Non-Improvable (optimal) | [P1] Historical: 25% bull, 1.83% bear, 10.56% avg; No incentive programs for hBTC |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | The position involves borrowing USDh on Zest and staking it. Unwinding requires unstaking sUSDh, repaying borrow, and withdrawing sBTC. Cooldown periods apply. Given small TVL, slippage unlikely to be material under normal conditions. Under stress, Zest utilization could constrain exits. Score Mid (3): "Under conservative assumptions only large portion but not all can be unwound within stated horizon." | 3 | 3 | Non-Improvable | [P1] Withdrawal flow: cooldowns + sBTC bridge settlement; Small TVL mitigates slippage concern |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Yes. The strategy is fundamentally a funding rate carry trade. Funding rates can and do invert -- backtest shows 5.9% negative days. Bear market (2023): only 1.83% APY. Reserve fund partially covers negative periods. Majority of yield (~80%+) comes from funding rates. Score High (1): "Strategy is primarily a carry or peg trade with most yield driven by invertible spreads or funding above roughly 70%." | 1 | 1 | Non-Improvable | [P1] Basis strategy: delta-neutral + funding rate capture; [P1] 5.9% negative days; 2023 bear: 1.83% |

**Protocol Mechanics Subtotal:**
- Raw: 3+3+3+3+9+9+9+3+1 = 43/81
- Weighted: (43/81) x 45 = 23.9

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Only mainnet BTC serves as collateral, accessed via sBTC bridge. BTC is the premier large-cap crypto asset. sBTC is a 1:1 BTC-backed asset with 70% supermajority consensus (10-of-14 signers). Limited to established large-cap asset with bridge dependency. Score Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] Basis docs: "Only mainnet BTC serves as the collateral asset"; [P1] sBTC: 10-of-14 signer supermajority |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | sBTC is relatively new (mainnet deposits from Dec 2024). Limited stress history. No sBTC depeg events have been publicly reported. However, the vault itself is very new (2025-2026) with no documented stress test. Score Mid (3): untested protocol -- cannot score 9 without demonstrated resilience. | 3 | 9 | **Source Missing** | [P1] sBTC launched Dec 2024; [P3] No depeg events reported; Insufficient stress history |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- hBTC is a vault product, not a staking/LST product. The underlying sBTC bridge uses Stacks signers (not validators in the slashing sense). The basis strategy does not involve direct staking/validator operations. | N/A | N/A | N/A | - |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | 100% of TVL relies on sBTC, which is a bridged asset (BTC bridged to Stacks via sBTC bridge with 10-of-14 signer set). sBTC is the canonical bridge token for BTC on Stacks. Score High (1): "Bridged or wrapped assets represent more than 60% of TVL." | 1 | 1 | Non-Improvable | [P1] hBTC deposits require sBTC; sBTC = bridged BTC on Stacks; 100% bridge dependency |

**Collateral Subtotal:**
- Scored questions: 3 (ST-C-03 is N/A)
- Raw: 9+3+1 = 13/27
- Weighted: (13/27) x 45 = 21.7

---

#### Infra Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Chain: Stacks (not in SR Tier lists, effectively Tier-2/3). Bridge: sBTC (canonical, not in SR bridge tiers). Oracle: DIA (Tier-2). CEXs: Binance, Bybit, OKX, Bitget. Custody: Copper, Ceffu. Protocol: Zest (not in SR tiers). Most dependencies disclosed but Tier-2/3 counterparts used. Score Mid (3). | 3 | 3 | Non-Improvable | [P1] Docs disclose all dependencies; [P1] DIA oracle partnership; Framework tiers: Stacks unlisted, DIA = Tier-2 |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | Oracle: hBTC strategy indirectly depends on DIA Reserve-Backing Ratio feed (used by USDh which hBTC borrows) -- single provider, Tier-2. No documented fallback oracle for the strategy. Bridge: sBTC is the only BTC bridge to Stacks -- single point of entry. Both are single-provider setups. Score High (1): "No meaningful redundancy exists OR only Tier-2/3." | 1 | 3 | **Improvable** | [P1] DIA oracle (Tier-2): single provider, indirect dependency via USDh; [P1] sBTC bridge: only canonical bridge to Stacks |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Copper and Ceffu are the key off-chain providers. Ceffu is ISO 27001 & ISO 27701 certified and SOC 2 Type 1 & Type 2 attested. Copper is a regulated custodian. Both are institutional-grade. Score Low (9): all critical off-chain providers hold current certifications. | 9 | 9 | Non-Improvable (optimal) | [P1] Ceffu: ISO 27001, ISO 27701, SOC 2 Type I & II; [P3] Copper.co: regulated custodian |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Stacks experienced multiple incidents: Jan 2025 5+ hour outage (signer issue), Nov 2024 halt at block 264,670, Mar 2025 GitHub security incident. These caused temporary halts but no user fund losses. hBTC was not yet live during most incidents. Score Mid (3): "Past incidents caused temporary delays or degraded access but recovered without permanent user losses." | 3 | 9 | **Source Missing** | [P4] CryptoSlate: Stacks 5h outage Jan 2025; [P4] Stacks forum: Nov 2024 halt; [P4] Mar 2025 GitHub incident |
| ST-IC-05 | Has the base chain recently halted block production? | Yes. Stacks halted for 5+ hours in January 2025 (signer issue post-Nakamoto upgrade). Additional brief halt in November 2024. This exceeds the 30-minute threshold and occurred within last 12 months. Score High (1): "Any incident above 6 hours or repeated incidents." Multiple incidents occurred. | 1 | 1 | Non-Improvable | [P4] CryptoSlate: 5+ hour Stacks outage Jan 6, 2025; Nov 2024 halt; repeated incidents |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- hBTC is a vault product. sBTC bridge uses signers, not validators in the traditional staking sense. No slashing mechanism applies to the hBTC strategy. | N/A | N/A | N/A | - |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- not a staking/LST product. | N/A | N/A | N/A | - |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | sBTC bridge is a single point of failure for withdrawals to native BTC -- if the sBTC signer set fails (requires 70% consensus), BTC withdrawals are blocked. Users could still exit to sBTC on Stacks but not to native BTC. Stacks chain itself is a dependency. Score Mid (3): "One or two infra components operationally important and single failure could temporarily delay or degrade withdrawals for up to 24-48 hours." | 3 | 3 | Non-Improvable | [P1] sBTC bridge: 10-of-14 signers, 70% consensus required; Stacks chain dependency |

**Infra Counterparty Subtotal:**
- Scored questions: 6 (ST-IC-06 and ST-IC-07 are N/A)
- Raw: 3+1+9+3+1+3 = 20/54
- Weighted: (20/54) x 45 = 16.7

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Strategy deploys to: Zest Protocol (lending), Hermetica USDh Protocol (staking). Funding rate exposure via Binance, Bybit, OKX, Bitget (through Copper/Ceffu OES). Venues disclosed with names. Zest and Hermetica USDh are not in SR Protocol Tiers (effectively untiered small Stacks protocols). CEXs are major but accessed via OES. Score Mid (3): "Most venues disclosed with partial tiering and some untiered but established venues." | 3 | 9 | **Improvable** | [P1] Governance docs: Zest Protocol + Hermetica USDh as allowed externals; [P1] Basis docs: Binance, Bybit, OKX, Bitget via Copper/Ceffu |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | No revenue-share or incentive arrangements disclosed. Yield comes from funding rates and lending interest. No evidence of undisclosed arrangements. Score Mid (3): "Arrangements acknowledged but terms only partially disclosed." Given opacity, cannot confirm no arrangements exist. | 3 | 9 | **Source Missing** | [P1] No revenue-share disclosed in docs; Absence of disclosure =/= absence of arrangements |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | LTV caps (49-51%) enforced by automated monitoring. Delta exposure band (0.999-1.001). Interest spread control with 2-day trigger. These are hard limits but per-counterparty caps (e.g., max % on Binance vs Bybit) are not documented. Score Mid (3): "Caps exist and documented but enforcement and rebalancing partly manual." | 3 | 9 | **Improvable** | [P1] Risk controls: quantitative limits for LTV, delta, spread; Per-venue allocation not documented |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | OES settlement (ClearLoop/MirrorX) operates with periodic settlement. Positions on exchanges can generally be closed quickly. sBTC bridge withdrawal: ~80 min (8 Bitcoin confirmations). Cooldown period for hBTC redemption exists but duration unspecified. Score Mid (3): "Positions can usually be unwound but some counterparties require longer lead times." | 3 | 9 | **Source Missing** | [P1] Flows docs: withdrawal ~80 min via sBTC; Cooldown period mentioned but unspecified; OES periodic settlement |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Yes. Custody providers: Copper (ClearLoop, bankruptcy-remote English trust) and Ceffu (MirrorX, ISO 27001/SOC 2). Their roles (custody, OES) clearly described. Exchange venues listed (Binance, Bybit, OKX, Bitget). Score Low (9): all third parties listed by name with roles and responsibilities. | 9 | 9 | Non-Improvable (optimal) | [P1] Basis docs: Copper, Ceffu custodians; ClearLoop, MirrorX settlement; 4 exchanges listed |

**Protocol Counterparty Subtotal:**
- Raw: 3+3+3+3+9 = 21/45
- Weighted: (21/45) x 45 = 21.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused? | Users redeem hBTC for sBTC or native BTC. Cooldown period applies (duration unspecified). Express withdrawal available with fee. Guardian can pause protocol (3-of-6 multisig). No documented address-level blocking. Pause is protocol-wide only. Score Mid (3): "Withdrawals on-chain but multisig can temporarily pause or extend queues under documented conditions." | 3 | 9 | **Improvable** | [P1] Flows docs: redeem hBTC, cooldown applies; [P1] Governance: Guardian can pause |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL? | hBTC TVL is small (not separately tracked on DeFiLlama). sBTC liquidity on Stacks is limited. The strategy borrows USDh on Zest -- unwinding depends on Zest utilization. At current small size, likely adequate. However, untested at scale. Score Mid (3): "Liquidity adequate for small to medium exits." | 3 | 9 | **Source Missing** | [P3] hBTC TVL not separately tracked on DeFiLlama; Small size mitigates concerns |
| ST-L-03 | Have there been past withdrawal delays or freezes? | No documented withdrawal delays, queues, or freezes. However, hBTC is very new with limited operational history. Untested. Score Mid (3): cannot confirm >95% on-time without data. | 3 | 9 | **Source Missing** | [P1] No delays reported; Very limited operational history |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Minting restrictions apply if derivative market capacity is insufficient. Express withdrawal available with fee (fee amount undisclosed). No documented history of caps blocking exits. Score Mid (3): "Caps occasionally created queues during high utilization but cleared within days." Precautionary scoring given design. | 3 | 3 | Non-Improvable | [P1] FAQ: minting restrictions possible; Express withdrawal with fee |
| ST-L-05 | How does exit liquidity behave during volatility? | Stacks experienced 5+ hour outage in Jan 2025, which would have blocked all DeFi operations including withdrawals. hBTC was not yet live during that event but the chain risk persists. sBTC bridge adds settlement time. No documented hBTC-specific stress test. Score High (1): untested protocol on chain with documented outages. | 1 | 3 | Non-Improvable | [P4] Stacks 5h outage Jan 2025; Protocol untested during stress |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | Withdrawal to native BTC requires sBTC bridge (~80 min for 8 confirmations). Plus cooldown period (unspecified). If cooldown + bridge = multiple hours to days, this could exceed stated terms. Unstaking from Zest adds time. Score Mid (3): "Roughly 10-30% of assets have longer duration than withdrawal terms with disclosed queues." | 3 | 3 | Non-Improvable | [P1] Flows: ~80 min BTC settlement + unspecified cooldown; Strategy unwinding adds time |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | hBTC can be redeemed directly through the vault protocol (in-protocol redemption). No need for secondary market. However, subject to cooldowns and strategy unwinding. Score Low (9): "Most users can exit primarily via in-protocol redemption." | 9 | 9 | Non-Improvable (optimal) | [P1] hBTC overview: permissionless redemption via vault |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | sBTC (collateral) liquidity on Stacks is limited -- Stacks DeFi TVL is small (~$100M range). hBTC (receipt token) has no documented secondary market liquidity. BTC itself is deeply liquid but sBTC is not. Score High (1): "Depth below ~3% of TVL without major impact or market data not disclosed." | 1 | 3 | Non-Improvable | [P3] Stacks DeFi TVL limited; sBTC secondary market thin; hBTC no secondary market |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Under bank-run: all hBTC holders try to redeem simultaneously. Strategy must unwind positions on Zest and exchanges. Cooldown period provides buffer. Small TVL means absolute amounts are manageable. Reserve fund covers negative funding. But chain outages could compound the problem. Score Mid (3): "Bank-run would likely cause significant queues and some discounting, but losses expected to be contained." | 3 | 3 | Non-Improvable | [P1] Risk controls: reserve fund, automated position management; Chain risk adds uncertainty |

**Liquidity Subtotal:**
- Raw: 3+3+3+3+1+3+9+1+3 = 29/81
- Weighted: (29/81) x 45 = 16.1

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | hBTC is a vault share token with NAV-based pricing (share price reflects underlying strategy value). It trades at NAV, not a peg. No secondary market trading. Score N/A per applicability check: "Mark N/A for protocols where users hold positions directly represented as non-transferable account balances." hBTC may be transferable but has no meaningful secondary market pricing. N/A. | N/A | N/A | N/A | - |
| ST-M-02 | Can adverse crypto market moves cause permanent losses? | Strategy is delta-neutral (delta exposure band 0.999-1.001). BTC price moves should not directly cause losses. However, extreme moves could trigger liquidation at 70-75% LTV if rebalancing fails. Strategy has moderate leverage (~2x via 50% LTV). Score Mid (3): "Strategy has moderate directional exposure or leverage (roughly >1.2x to <=3x)." | 3 | 3 | Non-Improvable | [P1] Risk controls: delta-neutral, 2x leverage, 70%/75% liquidation thresholds |
| ST-M-03 | Are interest rate models robust during TVL shifts? | Yield depends on perpetual futures funding rates which are highly variable. 2023 bear: 1.83% APY; 2022 bull: 25.03%. Rate inversions cause reserve fund draw-downs. Interest spread control auto-closes after 2 days negative. No documented prolonged >=95% utilization. Score Mid (3): "Models show temporary strain with short spikes." | 3 | 3 | Non-Improvable | [P1] Historical: 1.83% to 25.03% range; Auto-close after 2-day negative spread |
| ST-M-04 | Have historic scenarios with high volatility been modeled? | Backtest covers Jan 2021 - Sep 2025, including 2022 crash and 2023 bear. Shows 5.9% negative yield days. Average 10.56% APY. This provides some stress testing but is a backtest, not forward-looking scenario analysis. Score Mid (3): "Strategy tested against moderate volatility and price shocks but tail assumptions only partially covered." | 3 | 9 | **Improvable** | [P1] Historical performance: 4.5-year backtest including bear and bull markets; 5.9% negative days |
| ST-M-05 | Can sharp price moves trigger forced liquidations? | LTV target 50%, partial liquidation at 70%, full at 75% with 5-10% penalties. 20% buffer between target and liquidation. Sharp BTC price drops could trigger liquidation if rebalancing (off-chain) fails. Moderate leverage (~2x). Score Mid (3): "Strategy uses moderate leverage with defined buffers." | 3 | 3 | Non-Improvable | [P1] Risk controls: 50% target, 70% partial, 75% full liquidation; 5-10% penalties |

**Market Subtotal:**
- Scored questions: 4 (ST-M-01 is N/A)
- Raw: 3+3+3+3 = 12/36
- Weighted: (12/36) x 45 = 15.0

---

### **Strategy Total: 23.9 + 21.7 + 16.7 + 21.0 + 16.1 + 15.0 = 114.4/270 (42.4%)**

---

### OPERATIONS (30% Weight) -- Score: 122.7/270 (45.4%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes? | Role-based governance model with 3-of-6 multisig Owner role. No on-chain token-holder governance. All critical changes require multisig with 24h timelock. This is a "Hybrid model" at best -- multisig can execute upgrades within documented bounds but no binding on-chain governance. Score Mid (3). | 3 | 9 | **Improvable** | [P1] Governance docs: role-based model, 3-of-6 multisig, 24h timelock |
| O-G-02 | How concentrated is voting power among top holders? | N/A -- no governance token exists. Pure multisig governance. Concentration is captured in S-KM-01/03. | N/A | N/A | N/A | - |
| O-G-03 | Are mechanisms in place to limit major changes? | 24h timelock documented on critical changes (role assignments, security-sensitive settings). Guardian can pause as emergency measure. No formal veto mechanism documented. Score Mid (3): "Timelocks exist but shorter than 24 hours or veto safeguards informal." Actually, 24h timelock meets the threshold. Score Low (9): timelock >=24h with narrow guardian powers. | 9 | 9 | Non-Improvable (optimal) | [P1] Governance docs: 24h timelock on critical changes; Guardian pause capability |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | The Owner role can change operator addresses (Trader, Manager, Rewarder) via timelocked governance. Emergency freeze allows safe asset withdrawal. Replacement appears possible without blocking withdrawals. Score Mid (3): "Replacement possible via multisig or governance but may require short pause." | 3 | 9 | **Improvable** | [P1] Governance: Owner can reassign operator roles with timelock; Emergency freeze for asset withdrawal |

**Governance Subtotal:**
- Scored questions: 3 (O-G-02 is N/A)
- Raw: 3+9+3 = 15/27
- Weighted: (15/27) x 67.5 = 37.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified? | Founder/CEO Jakob Schillinger publicly identified. Hermetica Labs, Inc. registered in Panama (LEI: 875500HJQSF6L5RV7H39, Registration #155736526, active since Apr 2023). Team has "experience from Kraken and State Street." However, only the CEO is publicly named -- other team members not disclosed. Score Mid (3): "Team or entity partially disclosed with limited verifiable background for some critical roles." | 3 | 9 | **Improvable** | [P1] LEI Bloomberg: Hermetica Labs Inc, Panama, LEI 875500HJQSF6L5RV7H39; [P4] TheBlock: Jakob Schillinger, CEO |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Small team -- only CEO publicly identified. $1.7M seed suggests a lean team. Key-person risk is high with Jakob Schillinger as the visible face. No evidence of large engineering team or redundancy. Score High (1): "One person or very small team effectively controls critical code or operations." | 1 | 9 | **Improvable** | [P4] Seed of $1.7M; Only CEO publicly named; Small Stacks ecosystem team |
| O-TL-03 | What legal entity and jurisdiction operate the protocol? | Hermetica Labs, Inc., Republic of Panama, Sociedad Anonima. Registered April 24, 2023. World Trade Center 200-B, Panama. LEI: 875500HJQSF6L5RV7H39. Clear legal entity with named jurisdiction. Score Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] LEI registration; [P1] Terms of Service: Panama jurisdiction, arbitration in Panama |
| O-TL-04 | Are there known investigations or regulatory actions? | No known enforcement actions against Hermetica Labs in any major jurisdiction. Protocol restricts US, EU, and many other jurisdictions via geofencing. Score Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] Terms of Service: restricted jurisdictions listed; No enforcement actions found |
| O-TL-05 | Is there an on-call and incident response process? | No documented on-call or incident response process. Emergency freeze mechanism exists but no formal runbooks, escalation procedures, or response SLAs documented. Score High (1). | 1 | 9 | **Improvable** | [P1] Emergency freeze documented; No formal incident response process published |
| O-TL-06 | Does the team provide timely support for critical issues? | Discord available as support channel. No documented response SLAs or structured escalation. Score Mid (3): "Response inconsistent and often 24-72 hours with limited structured escalation." Giving benefit via Discord presence. | 3 | 9 | **Improvable** | [P1] Discord channel available; No formal support SLA documented |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Seed investors disclosed: UTXO Management (lead), CMS Holdings, Ethos Fund, Trust Machines SPV, Newman Capital. Angel investors named: Tycho Onnasch (Zest), Robin Obermaier (Liquidium), Mithil Thakore (Velar), Matt Maduno (Arch), GM Chung (DeSpread). Roles and rights not fully clear. Score Mid (3). | 3 | 9 | **Improvable** | [P4] TheBlock/Chainwire: investor list; [P2] Crunchbase: funding details |
| O-TL-08 | Does the strategy manager manage similar products creating conflict? | Hermetica manages both hBTC and USDh/sUSDh products. These are related but not directly conflicting -- hBTC uses USDh as a component. Potential conflict: hBTC borrows USDh, benefiting USDh TVL. Partial disclosure, qualitative assessment. Score Mid (3). | 3 | 9 | **Improvable** | [P1] Hermetica manages both hBTC and USDh; hBTC strategy depends on USDh |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | No known collateral loss events linked to Hermetica or Jakob Schillinger. Protocol operational since mid-2024 without incidents. Score Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] No loss events; [P4] No incidents reported |

**Team & Legal Subtotal:**
- Raw: 3+1+9+9+1+3+3+3+9 = 41/81
- Weighted: (41/81) x 67.5 = 34.2

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation on architecture and risks? | hBTC docs cover: overview, deposit/withdrawal flows, yield mechanics (basis strategy), risk controls (LTV, delta, spread), governance (roles, timelock), and accounting (NAV, share price). Documentation is comprehensive and appears current (Hermetica 2.0 launched Apr 2025). Score Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] docs.hermetica.fi/hbtc -- comprehensive coverage of architecture, strategy, risks |
| O-DT-02 | Is it documented how collateral is used and when loss occurs? | Risk controls document LTV thresholds (50% target, 70%/75% liquidation with 5-10% penalties). Delta exposure bands documented. Loss scenarios: negative funding, exchange failure, liquidation. Reserve fund disclaimer: "not a guarantee against loss." Collateral flow documented (sBTC -> borrow USDh -> stake -> harvest). Score Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] Risk controls page: quantitative thresholds; [P1] Reserve fund: loss scenarios described |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Governance docs list Owner multisig (SM1QXY...) and Operator address (SP20V8...). However, the actual hBTC vault contract address is not documented in a single canonical registry. No comprehensive address registry found. Score Mid (3): "Addresses documented but spread across multiple pages or some components missing." | 3 | 9 | **Improvable** | [P1] Governance page lists multisig and operator addresses; No canonical contract registry |
| O-DT-04 | Are roles, permissions and timelocks documented? | Governance docs clearly document: Owner (3-of-6), Guardian, Trader, Manager, Rewarder, Fee Setter roles with addresses. 24h timelock documented. Settings categories documented. However, no visible change history or log of past role changes. Score Mid (3): "Role documentation exists but scattered; occasional role changes documented after the fact." | 3 | 9 | **Improvable** | [P1] Governance docs: comprehensive role documentation; No change history log |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Monthly custodian attestations published per docs. Transparency dashboard provides "near real-time visibility into system backing, venue allocation, reserve fund status." DIA oracle provides reserve-backing ratio feed. For hBTC specifically, proof-of-reserves methodology not explicitly detailed. Score Mid (3): "Proofs not up to date or cover only subset of reserves or liabilities." | 3 | 9 | **Improvable** | [P1] Basis docs: monthly custodian attestations; [P1] DIA oracle: reserve-backing ratio; Transparency dashboard |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Stacks contracts written in Clarity (decidable, readable). Stacks explorer (explorer.hiro.so) provides contract source visibility. However, unable to independently verify hBTC vault contract verification status via web search -- Stacks explorer did not return data. Score Mid (3): "Most core contracts verified but some helper or peripheral contracts not." Precautionary. | 3 | 9 | **Source Missing** | [P0] Stacks explorer: unable to verify; Clarity contracts are inherently readable |

**Documentation Subtotal:**
- Raw: 9+9+3+3+3+3 = 30/54
- Weighted: (30/54) x 67.5 = 37.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Reserve Fund exists: 5% of daily rewards allocated, minimum 10bp capitalization. Covers negative funding periods and exchange failure losses. Held in multisig wallets. However, activation "designed as a risk mitigation mechanism, not as a guarantee against loss" -- discretionary, not binding. Score Mid (3): "Backstop or treasury stated as intended for loss coverage but activation remains discretionary." | 3 | 9 | **Improvable** | [P1] Reserve fund docs: 5% of daily rewards, 10bp minimum; Discretionary activation |
| O-FR-02 | How large are backstop reserves relative to TVL? | Reserve fund size not disclosed. $1.7M seed raised, but treasury holdings not publicly documented. DeFiLlama does not track Hermetica treasury. No treasury wallet addresses disclosed. Score High (1): "Liquid reserves and treasury <1% of TVL or balances and composition not disclosed." | 1 | 9 | **Source Missing** | [P3] DeFiLlama: no treasury data; [P1] $1.7M seed raised; Reserve fund size undisclosed |
| O-FR-03 | What is the estimated operational runway? | $1.7M seed funding raised Oct 2024. No revenue disclosures. Small team suggests moderate burn rate. Cannot estimate runway from disclosed information. Score High (1): "Runway cannot be estimated from disclosed information." | 1 | 3 | **Source Missing** | [P4] $1.7M seed (Oct 2024); No burn rate or revenue disclosures |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress? | hBTC is newly launched (2025-2026) with no documented stress events. The vault has not been tested through a significant market downturn. Score Mid (3): untested. | 3 | 9 | **Source Missing** | [P1] No stress events; hBTC too new for meaningful stress history |
| O-FR-05 | Can the protocol remain safe if team disappears? | On-chain vault contracts on Stacks would continue to hold assets. Emergency freeze mechanism allows safe withdrawal. However, the basis strategy requires active management (off-chain keepers, exchange position management, Copper/Ceffu operations). If team disappears, strategy positions may not be managed, risking liquidation. Score High (1): "Loss of core team would likely impair or block withdrawals due to centralized keys, critical off-chain dependencies." | 1 | 3 | Non-Improvable | [P1] Strategy requires active management: off-chain keepers, custody operations, exchange positions |

**Financial Resilience Subtotal:**
- Raw: 3+1+1+3+1 = 9/45
- Weighted: (9/45) x 67.5 = 13.5

---

### **Operations Total: 37.5 + 34.2 + 37.5 + 13.5 = 122.7/270 (45.4%)**

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 71 | 99 | 129.1 | 180 | 71.7% |
| | Key Management (8 Q) | 46 | 72 | 115.0 | 180 | 63.9% |
| | **Security Subtotal** | | | **244.1** | **360** | **67.8%** |
| **Strategy** | Protocol Mechanics (9 Q) | 43 | 81 | 23.9 | 45 | 53.1% |
| | Collateral (3 of 4 Q scored) | 13 | 27 | 21.7 | 45 | 48.1% |
| | Infra Counterparty (6 of 8 Q scored) | 20 | 54 | 16.7 | 45 | 37.0% |
| | Protocol Counterparty (5 Q) | 21 | 45 | 21.0 | 45 | 46.7% |
| | Liquidity (9 Q) | 29 | 81 | 16.1 | 45 | 35.8% |
| | Market (4 of 5 Q scored) | 12 | 36 | 15.0 | 45 | 33.3% |
| | **Strategy Subtotal** | | | **114.4** | **270** | **42.4%** |
| **Operations** | Governance (3 of 4 Q scored) | 15 | 27 | 37.5 | 67.5 | 55.6% |
| | Team & Legal (9 Q) | 41 | 81 | 34.2 | 67.5 | 50.6% |
| | Documentation (6 Q) | 30 | 54 | 37.5 | 67.5 | 55.6% |
| | Financial Resilience (5 Q) | 9 | 45 | 13.5 | 67.5 | 20.0% |
| | **Operations Subtotal** | | | **122.7** | **270** | **45.4%** |
| **TOTAL** | | | | **481.2** | **900** | **53.5%** |

**Current Grade**: CCC- (481.2/900 points -- within 420-500 range)
**Potential Grade**: BB+ (793.4/900 points) -- achievable if all improvements made

---

