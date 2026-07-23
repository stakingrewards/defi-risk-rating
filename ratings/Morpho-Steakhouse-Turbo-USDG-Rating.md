# Morpho - Steakhouse Turbo USDG Vault Risk Rating

**Rating Date**: 2026-07-22
**Analyst**: DeFi Risk Auditor Agent
**Final Grade**: CCC
**Total Score**: 557.7/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Executive Summary

The **Steakhouse Turbo USDG** vault (`0xbeEfFF136E3684273e6aA75A1669B784B373A4FD`, symbol `bbqUSDGturbo`) is a Morpho Vault V2 curated by Steakhouse Financial and deployed on **Robinhood Chain** — a brand-new Arbitrum Orbit L2 (chainId 4663) whose mainnet went live on July 1, 2026. Unlike its plain-lending sibling (the "Steakhouse USDG" Robinhood Earn engine, `0xBeEff033...`), Turbo is the highest-risk product line in the Steakhouse catalogue: it deploys deposited USDG (Paxos' MAS/MiCA-regulated Global Dollar) into a **leveraged strategy** via Steakhouse's custom **"Box"** adapter registry. Verified on-chain (Robinhood Chain RPC, 2026-07-22): TVL ≈ $2.73M USDG, performance fee 0%, management fee 0%, ~1.39% (7d) / ~1.76% (30d) net APY, and **~2.4x leverage** (per the Steakhouse app). Funds are split across two adapters: a **BoxAdapter** (`0xec1f17…`, ≈ $2.46M / ~90% of NAV) that feeds the **"Box Turbo USDG"** child vault (`0x3e35b4…`, a 21.3KB leverage engine running Morpho Blue / Aave v3 funding modules against whitelisted collateral), and a **Morpho Market V1 adapter** (`0xda889f…`, ≈ $273.8K / ~10%) that holds the "repo" liquidity buffer.

The vault's **key management is materially stronger than its single-EOA-owned sibling**. On-chain verification shows the vault Owner is a **Supervisor contract** (`0x261a3b7a…`) enforcing a **14-day timelock (0x127500 = 1,209,600s)** on owner actions, and the Supervisor is itself owned by a **5-of-10 Steakhouse Safe** (`0xd062020d…`). The Curator is a **3-of-7 Safe** (`0x9023FBD6…`) and the Sentinel is a **1-of-7 Safe** (`0x5642BCd5…`, the same emergency signer as the sibling). The custom Box leverage code is **not** an unaudited surface: it carries **two independent Tier-0 audits** — ChainSecurity (Dec 2025) and a Cantina competition (Jan 2026), both public in the `Steakhouse-Financial/box` GitHub repo — and Box adds guardian-veto, three-state shutdown/winddown, and oracle-bounded slippage controls, with **permissionless winddown** once a warmup elapses.

Despite these strengths, Turbo lands at **CCC (557.7/900) — ~30 points below its plain-lending sibling (CCC+/587.5)** — because the leverage is a structural, permanent risk multiplier layered on top of an unproven chain. The drivers: (1) **~2.4x leverage** turns collateral depegs, negative carry, borrow-rate spikes, and forced deleveraging into plausible loss events (Strategy 115.3/270, its weakest category — CC grade), with the leveraged carry itself scoring High on spread-inversion risk (ST-PM-09) in line with the Ethena sUSDe and Hermetica hBTC carry-trade precedents; (2) **oracle risk is amplified** — the leverage relies on single-source, non-Tier-0/1 Morpho market oracles with no redundancy, on the same synthetic-stable collateral family (USDe/syrupUSDG/spUSDG) whose sibling market the analyst verified uses a hardcoded 1:1 feed (ST-IC-02 = High); (3) the **live leverage deployment configuration is not in audit scope** and the deployed contracts are **not verified on hoodexplorer** (S-SC-01 = Mid, O-DT-06 = Mid); (4) **adapter addition is instant** on-chain (`setIsAdapter` timelock = 0), weakening governance guardrails on a leverage vault (O-G-03, S-KM-07 = Mid); and (5) **thin liquidity** — only ~10% is an immediate repo buffer, the remaining ~90% is leveraged and exits via Box winddown with escalating slippage, on a 6-week-old single-sequencer chain with zero stress history. No deal breakers trigger: the immutable Morpho V2 core, multisig owner with 14-day/3-day/7-day timelocks, sentinel + guardian vetoes, and permissionless ERC-4626 redemption keep any single key from moving funds. The maximum achievable grade if monitoring/circuit-breakers, a config-inclusive audit, hard caps, signer-independence disclosure, a backstop, and a stress track record are added is **BBB+ (835.7/900)** — a ceiling still below the plain-lending sibling's (A-/846.4) because the ~2.4x leverage permanently caps the Strategy category, though the gap narrows on Security, where the Box architecture's automatable safety controls give Turbo a perfect potential (360.0) the sibling cannot reach.

---

## Rating Overview

| Category | Weight | Current Score | Max Score | Current % | Potential Score | Potential % |
|----------|--------|---------------|-----------|-----------|-----------------|-------------|
| Security | 40% | 271.36 | 360 | 75.4% | 360.00 | 100.0% |
| Strategy | 30% | 115.33 | 270 | 42.7% | 210.67 | 78.0% |
| Operations | 30% | 171.00 | 270 | 63.3% | 265.00 | 98.1% |
| **Total** | **100%** | **557.70** | **900** | **62.0%** | **835.67** | **92.9%** |

**Current Grade**: CCC (557.70/900 points)
**Potential Grade**: BBB+ (835.67/900 points) - achievable if all improvements made

---

## Deal Breaker Assessment

| Question Code | Deal Breaker Type | Status | Impact |
|---------------|-------------------|--------|--------|
| [S-SC-01] Audits | Category | PASS (Mid) | No cap -- Morpho V2 core (immutable) + custom Box code both independently audited by >=2 Tier-0 firms; only the live leverage deployment config is out of scope |
| [S-SC-06] Exploits | Full | PASS | No cap -- no confirmed exploit with user-fund loss on this vault, the Box infrastructure, or Steakhouse/Morpho V2 vaults |
| [S-SC-07] Rug Pull | Full | PASS | No cap -- no rug-pull events; Morpho is a nonprofit, Steakhouse has a clean multi-year curation record |
| [S-KM-02] Single Key Control | Category | PASS (Low) | No cap -- immutable core + 3-of-7 curator Safe + 3-day cap timelock + Supervisor(14-day)/5-of-10 Safe + 1-of-7 Sentinel veto; no single key can move funds or upgrade custody |
| [ST-PM-05] Strategy Losses | Category | PASS (Mid) | No cap -- no confirmed permanent-loss event for Steakhouse Turbo or a comparable Box leverage variant; leverage type carries elevated risk, scored Mid |
| [ST-PC-05] Third-Party Disclosure | Category | PASS | No cap -- on-chain; curator (Steakhouse), USDG issuer (Paxos), funding venues (Aave/Morpho), and collateral protocols (Ethena/Maple/Spark) all disclosed |
| [O-TL-04] Regulatory Actions | Category | PASS (Mid) | No cap -- past resolved enforcement against Robinhood Crypto (NYDFS 2022) and Paxos (BUSD 2023); no ongoing material action impairing this product |
| [O-DT-05] Proof of Reserves | Category | PASS | No cap -- full on-chain proof-of-reserves (positions and leverage legs auditable); USDG reserves attested monthly by Paxos |

**Deal Breaker Summary**: No deal breakers triggered. The vault passes all critical safety checks; S-SC-01, ST-PM-05, and O-TL-04 land at Mid (3), which does not cap.

---

## Improvement Summary

| Classification | Count | Notes |
|----------------|-------|-------|
| Improvable | 17 | Monitoring, automated circuit breakers (incl. S-SC-11 via the Box layer), config-inclusive audit, Box bug-bounty, hard caps, setIsAdapter timelock, backstop, conflict policy, contract verification, governance |
| Source Missing | 5 | Signer identities, SOC 2 certs, on-call SLA, treasury disclosure, native-issuance of collateral |
| Time-Based (track record) | 14 | Chain maturity (incl. ST-IC-01 tier status), stress history, unwind track record (ST-PC-04), vault-token peg, resilience, leverage-strategy track record |
| Non-Improvable (structural) | 13 | Leverage (2.4x) loss/liquidation/liquidity profile, invertible leveraged carry (ST-PM-09 at High), synthetic collateral, chain choice, single-oracle design |
| Already Optimal | 31 | Immutable Morpho V2 core, multisig owner, non-custodial design, documentation, credible operators |

**Total Improvement Potential:** +278.0 points (557.7 to 835.7)

**Top Improvement Opportunities (ranked by weighted point impact):**

1. **Disclose signer independence + document key-compromise playbook, and add a hard on-chain timelock to `setIsAdapter`** [S-KM-03, S-KM-08, S-KM-07]: 3 → 9 (lifts Key Management to 180/180) -- Source Missing / Improvable
2. **Commission a deployment-config-inclusive audit of the live leverage setup + list the Box code in a bug bounty + connect monitoring to automated protections** [S-SC-01, S-SC-09, S-SC-10]: 3 → 9 -- Improvable
3. **Add automated, monitoring-triggered circuit breakers (via the Box shutdown/cap levers) and hard relative concentration caps to the leverage and repo adapters** [S-SC-11, ST-PM-10, ST-PC-03, ST-M-04]: 3 → 9 -- Improvable
4. **Upgrade the leverage-market oracles to correctable, redundant Tier-0/1 feeds** [ST-IC-02]: 1 → 3 (capped by single-oracle-per-market design) -- Improvable
5. **Establish a ring-fenced backstop reserve and disclose treasury detail** [O-FR-01, O-FR-02]: 3/1 → 9 -- Improvable / Source Missing
6. **Verify all deployed contracts on hoodexplorer + publish a canonical Box address registry** [O-DT-06, O-DT-03]: 3 → 9 -- Improvable
7. **Build operating and stress track record; mature chain tier status and demonstrated unwind paths; decentralize the sequencer** [ST-IC-01, ST-IC-04/05/08, ST-PC-04, ST-L-03/05, ST-M-01/03, PM-01/05, O-FR-04/05]: 3 → 9 over time -- Time-Based

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 271.36/360 (75.4%)

#### Smart Contract Security (20% weight, 180 max points)

**NOTE: The base Morpho VaultV2/Blue contracts are the same immutable, audited bytecode used across Morpho V2 deployments. UNLIKE the plain-lending sibling, this vault adds a custom "Box" leverage surface (BoxAdapter + Box Turbo USDG child vault + funding modules). The Box code IS independently audited (ChainSecurity Dec 2025 + Cantina Jan 2026, public on GitHub), so these scores are NOT auto-inherited from the sibling: S-SC-01 drops to Mid because the live leverage deployment configuration is not in audit scope, and S-SC-09 drops to Mid because the Box surface's bug-bounty coverage is not evidenced.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | Yes for code: Morpho VaultV2/Blue (immutable) audited by >=2 Tier-0 firms; the custom Box leverage code independently audited by ChainSecurity (Dec 2025) and Cantina (Jan 2026), both public on GitHub. But the LIVE leverage deployment configuration (funding modules, oracle wiring, collateral whitelist, leverage caps on Robinhood Chain) is not evidenced in audit scope -- Mid per the configuration-scope rule. | 3 | 9 | **Improvable** | [P1] [Box audits (GitHub)](https://github.com/Steakhouse-Financial/box/tree/52ab8b9f20184c5882448df7be31701df1cf6f39/audits), [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/), [P0] RPC (2 adapters, Box child vault verified) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent Box audit is a Cantina competition (Jan 2026, Tier-0), preceded by ChainSecurity (Tier-0, Dec 2025); Morpho V2 base audited by Certora/Spearbit/ChainSecurity (Tier-0). Multiple Tier-0 firms. | 9 | 9 | Non-Improvable (optimal) | [P1] [Box Cantina audit](https://github.com/Steakhouse-Financial/box/blob/52ab8b9f20184c5882448df7be31701df1cf6f39/audits/2026-01-06-cantina.pdf), [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Morpho VaultV2/Blue are immutable (no upgrade path). The Box system is newly deployed with no upgrades since audit; the audited commit (52ab8b9f) predates deployment. No core upgrade has occurred. | 9 | 9 | Non-Improvable (optimal) | [P1] [Box audits](https://github.com/Steakhouse-Financial/box/tree/52ab8b9f20184c5882448df7be31701df1cf6f39/audits), [P0] RPC (immutable base vault) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Box code received two sequential independent Tier-0 reviews (ChainSecurity Dec 2025, then Cantina Jan 2026 covering the updated code), satisfying second-firm re-review; Morpho V2 base is Certora-formally-verified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Box audits](https://github.com/Steakhouse-Financial/box/tree/52ab8b9f20184c5882448df7be31701df1cf6f39/audits), [P1] [Certora Morpho FV](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho VaultV2 and the Box child vault are immutable ERC-4626 contracts (fund-custody logic cannot be upgraded). Config changes are timelocked (caps 3-day, gates 7-day) and guardian/sentinel-vetoable. No upgrade path to custody logic. | 9 | 9 | Non-Improvable (optimal) | [P0] RPC (immutable vault + Box child vault), [P1] [Box Vaults docs](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit with user-fund loss on this vault, the Box infrastructure, or Steakhouse/Morpho V2 vaults. Vault deployed ~June 2026; no incidents. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P0] RPC (no incident) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho is a nonprofit (ADDMO); Steakhouse has a clean multi-year curation track record. No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. The vault was deployed with its current configuration (3-day cap timelocks, 7-day gate/abdicate timelocks, 0s setIsAdapter/fee/allocator). Decreasing a function's timelock is itself subject to that function's current timelock. | 9 | 9 | Non-Improvable (optimal) | [P0] RPC timelock(bytes4) per-function (verified) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Morpho V2 base contracts are covered by Cantina ($2.5M) / Immunefi bounties. But the custom Box leverage code (the dominant risk surface) is not evidenced as in scope of any active bug bounty. | 3 | 9 | **Improvable** | [P1] [Cantina Morpho Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3), [P1] [Immunefi Morpho](https://immunefi.com/bug-bounty/morpho/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Morpho/Steakhouse platform monitoring exists, but responses require manual human intervention and no automated protective action covers this vault's leverage/allocator flows; monitoring configuration for these specific markets on a 6-week-old chain is unverified. | 3 | 9 | **Improvable** | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Mid. No automatic invariant-triggered controls today: Box shutdown/winddown and oracle-bounded slippage caps exist but are guardian/manually triggered, and monitoring is not wired to automatic execution. Unlike the sibling's Sentinel-revoke-only design (structurally capped), the Box layer provides real halting levers (three-state shutdown, permissionless winddown, instant cap decreases) — wiring documented automatic monitoring-triggered protection covering the leverage and allocation flows is an achievable change. Morpho market isolation contains blast radius. | 3 | 9 | **Improvable** | [P1] [Box Vaults docs](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults), [P0] Sentinel 1-of-7 Safe (RPC) |

**Smart Contract Security Subtotal: 136.36/180 (75.8%)**
- 7 questions scored 9 (S-SC-02,03,04,05,06,07,08 = 63), 4 questions scored 3 (S-SC-01,09,10,11 = 12)
- Raw sum = 75 out of max 99
- Weighted = (75/99) x 180 = 136.36

---

#### Key Management & Permissions (20% weight, 180 max points)

**NOTE: This is the KEY MANAGEMENT difference from the plain-lending sibling (which had a bare single-EOA owner). On-chain verification (Robinhood Chain RPC, chainId 4663) shows a robust, layered structure: the vault Owner is a Supervisor contract (`0x261a3b7a…`) with a 14-day timelock (0x127500), whose owner is a 5-of-10 Safe (`0xd062020d…`); the Curator is a 3-of-7 Safe (`0x9023FBD6…`); the Sentinel is a 1-of-7 Safe (`0x5642BCd5…`). This lifts Key Management from the sibling's 80.0 to 135.0/180.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Low. Admin/owner rights are held by a diversified multisig: the vault Owner is a Supervisor contract (14-day timelock) owned by a 5-of-10 Steakhouse Safe -- not a single EOA. This is the single biggest improvement over the sibling. | 9 | 9 | Non-Improvable (optimal) | [P0] RPC: vault.owner()=0x261a3b7a (Supervisor, code + 0x127500=14-day const); Supervisor.owner()=0xd062020d (Safe getThreshold=5, getOwners=10) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | Low. No single key can move funds or upgrade custody: base VaultV2/Box child vault are immutable, permissionless ERC-4626 redemption, adapter caps require a 3-day timelock, the 3-of-7 curator Safe (>=3 threshold, >=5 signers) initiates timelocked actions, and the 1-of-7 Sentinel can revoke. Deal Breaker passes at Low. | 9 | 9 | Non-Improvable (optimal) | [P0] RPC: curator=3-of-7 Safe, cap timelock=259200s, immutable vault, Sentinel 1-of-7 |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Mid. Thresholds/counts are robust (curator 3-of-7 Safe; Supervisor owner 5-of-10 Safe), but (a) the curator is 3-of-7 (below the 4-of-7 Low bar) and (b) signer identities are not publicly disclosed, so independence (distinct individuals) cannot be verified -- capped at Mid per the framework. | 3 | 9 | **Source Missing** | [P0] RPC: curator getThreshold=3/getOwners=7; Supervisor-owner getThreshold=5/getOwners=10 |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Low. Gates are all null (open) today; the immutable vault has no arbitrary pause; a send-assets gate change requires a 7-day timelock + 3-of-7 curator Safe + Sentinel veto, and Box's permissionless winddown provides an exit backstop even if a gate were set. Multisig-controlled, time-bound, rules public. | 9 | 9 | Non-Improvable (optimal) | [P0] RPC gates=0x0 (all open), setSendAssetsGate timelock=604800s; [P1] [Box winddown](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of vault assets are held in non-custodial on-chain Morpho/Box contracts. USDG's fiat reserves at Paxos are the issuer's custody (counterparty risk), not the vault's custody. | 9 | 9 | Non-Improvable (optimal) | [P0] RPC (all funds in on-chain adapters/Box), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. On-chain segregation; performance and management fees are 0% (fee recipient = zero address). No co-mingling with treasury/ops wallets. | 9 | 9 | Non-Improvable (optimal) | [P0] RPC performanceFee=0, managementFee=0, feeRecipient=0x0 |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | Mid. On-chain enforced whitelist (2 adapters -> Box funding modules with whitelisted collateral/debt + one Morpho market), but `setIsAdapter` has a 0-second timelock (adapters can be added instantly by the 3-of-7 curator Safe), and the Box can add tokens (Box-level timelock). Broad and instantly extendable at the vault layer. | 3 | 9 | **Improvable** | [P0] RPC: adaptersLength=2, setIsAdapter timelock=0, increaseAbsoluteCap timelock=259200s |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Mid. Box documents guardian/shutdown/winddown controls, but no published, tested playbook for this vault's Supervisor + curator/sentinel key-compromise or signer-loss scenarios on a new chain. | 3 | 9 | **Improvable** | [P1] [Box Vaults docs](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults) |

**Key Management Subtotal: 135.00/180 (75.0%)**
- S-KM scores: 9, 9, 3, 9, 9, 9, 3, 3
- 5 questions scored 9 (S-KM-01/02/04/05/06 = 45), 3 questions scored 3 (S-KM-03/07/08 = 9)
- Raw sum = 54 out of max 72
- Weighted = (54/72) x 180 = 135.00

---

### **Security Total: 271.36/360 (75.4%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 136.36 | 180 | 75.8% |
| Key Management | 135.00 | 180 | 75.0% |
| **Security Total** | **271.36** | **360** | **75.4%** |

---

### STRATEGY (30% Weight) -- Score: 115.33/270 (42.7%)

**NOTE: Strategy is the weakest category (CC grade) and materially below the plain-lending sibling (148.3/270) because Turbo runs a ~2.4x LEVERAGED carry strategy (verified: ~90% of NAV in the Box Turbo leverage engine) on synthetic/credit stablecoin collateral, priced by single-source oracles, on a 6-week-old single-sequencer L2 with zero stress history. Per the "Favor Demonstrated History Over Uncertainty" principle, resilience questions cannot score Low.**

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Mid. Yield is the organic leveraged carry/lending spread on USDG (mandate-aligned: Turbo = "highest yield via leverage"), 0 vault fees. But the vault is only ~6 weeks old with no 6-12 month history and no published per-source % breakdown; current ~1.4-1.76% APY reflects a compressed carry. | 3 | 9 | Time-Based | [P0] RPC (2 adapters, ~90% Box leverage / ~10% repo), [P1] [Turbo docs](https://www.steakhouse.financial/docs/products/vault-products/current/turbo) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Mid. With ~2.4x leverage, loss can occur in plausible single-shock events: collateral (USDe/syrup) depeg, borrow rate exceeding collateral rate (negative carry), or forced deleveraging with slippage. Box slippage caps and winddown bound the loss, but it is not limited to rare tail shocks. | 3 | 3 | Non-Improvable | [P1] [Turbo docs](https://www.steakhouse.financial/docs/products/vault-products/current/turbo) ("losses when leverage trades executed... if borrow rate exceeds collateral rate") |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | Mid. The vault runs a leveraged loop/carry at ~2.4x effective leverage (per app), between 1.2x and 3x, with enforceable Box LTV caps relative to market LLTV and disclosed drawdown/liquidation risk. | 3 | 3 | Non-Improvable | [P3] Steakhouse app (~2.4x), [P1] [Box repo (Morpho/Aave funding modules, LTV caps)](https://github.com/Steakhouse-Financial/box) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | Mid. Turbo is a borrower (leverage). Box provides slippage-bounded swaps and guardian/winddown controls; at ~2.4x the implied LTV (~58%) sits meaningfully below a ~91.5% LLTV, but automated always-on deleveraging is not confirmed and there is no 30-day no-breach history (6-week-old engine). | 3 | 9 | **Improvable** | [P1] [Box Vaults docs](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults), [P3] app (~2.4x) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | Mid. No confirmed permanent-loss event for Steakhouse Turbo (e.g., AUSD Turbo on mainnet, ~10% organic APY) or a directly comparable Box leverage variant; but leveraged carry is a strategy type with elevated loss potential and this deployment is unproven (<24 months). Deal Breaker passes at Mid. | 3 | 9 | Time-Based | [P4] [Steakhouse markets update](https://kitchen.steakhouse.financial/p/defi-markets-update-2026-07-21), [P1] [Turbo docs](https://www.steakhouse.financial/docs/products/vault-products/current/turbo) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Low. Steakhouse publishes a curation risk framework, and Box adds documented quantitative controls: LTV caps relative to LLTV, oracle-based cumulative slippage limits, guardian veto, three-state shutdown/winddown, timelocked token/oracle additions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Box Vaults docs](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults), [P1] [Steakhouse Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Low. Yield is organic (leveraged lending carry, 0 vault fees, no token emissions in the vault). Sustainability depends on the carry persisting -- already compressed (~1.4-1.76%) -- but it is not incentive-driven. | 9 | 9 | Non-Improvable (optimal) | [P0] RPC (fees=0, organic spread), [P1] [Turbo docs](https://www.steakhouse.financial/docs/products/vault-products/current/turbo) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Mid. The ~10% repo buffer allows small exits; the ~90% leveraged portion unwinds via Box winddown with escalating slippage tolerance. On a thin new L2, unwinding a leveraged position under stress can incur 2-5%+ slippage that compresses/negates returns. | 3 | 3 | Non-Improvable | [P1] [Box winddown](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults), [P0] RPC (~10% repo / ~90% leverage split) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | High. The strategy is primarily a leveraged carry: ~90% of NAV sits in the Box leverage engine, so well above ~70% of expected yield is driven by the invertible collateral-rate-minus-borrow-rate spread (the Turbo docs state losses occur "if borrow rate exceeds collateral rate"), plus dependence on the USDe/syrup pegs. Box stop-rules (slippage caps, winddown) bound but do not prevent negative carry. Scored High (1) for consistency with the Ethena sUSDe and Hermetica hBTC carry-trade ratings (both 1: >70% of yield from invertible spreads). | 1 | 1 | Non-Improvable | [P1] [Turbo docs](https://www.steakhouse.financial/docs/products/vault-products/current/turbo), [P0] RPC (~90% of NAV in leverage adapter) |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Mid. Appointed allocators can allocate within the enabled adapters and their caps, and the Box can lever up within its module config, without real-time approval; caps limit per-market exposure but there is no automatic kill-switch for abnormal conditions -- halting requires manual guardian/sentinel action. | 3 | 9 | **Improvable** | [P0] RPC (allocators, caps, setIsAdapter=0), [P1] [Box Vaults docs](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults) |

**Protocol Mechanics Subtotal: 20.00/45 (44.4%)**
- 10 questions (ST-PM-04 now applicable -- Turbo is a borrower): 2 scored 9 (ST-PM-06,07 = 18), 7 scored 3 (= 21), 1 scored 1 (ST-PM-09 = 1)
- Raw sum = 40 out of max 90
- Weighted = (40/90) x 45 = 20.00

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Mid. The leverage loops within the same higher-risk synthetic/credit stablecoin family the sibling lends against -- USDe (Ethena synthetic dollar), syrupUSDG (Maple institutional credit), spUSDG (Spark) -- tiered with on-chain caps, but at leverage. These are not blue-chip large-caps; leverage amplifies their protocol/credit risk. | 3 | 3 | Non-Improvable | [P0] RPC (Box funding modules; repo Morpho market), [P4] [Robinhood Earn collateral markets](https://cryptoadventure.com/ethenas-usde-joins-robinhood-earn-as-defi-lending-moves-into-the-main-app/) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | Mid. USDe has shown modest (<~2%) historical deviations that recovered; syrupUSDG/spUSDG are new tokens with little peg history. At ~2.4x leverage, deviation behavior is a live concern rather than resolved, and stress history is absent on this chain. | 3 | 9 | Time-Based | Market data (USDe history); [P0] RPC (collateral family) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- the collateral tokens are not staking LSTs; depositors bear no direct slashing risk on the vault collateral. | N/A | N/A | N/A | Vault architecture |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | Mid. USDG/USDe/syrupUSDG/spUSDG are protocol/receipt/regulated-stable tokens -- partly outside the strict "bridged/wrapped" definition -- but on a 6-week-old L2 their native-vs-bridged issuance could not be verified; conservative Mid pending confirmation. | 3 | 9 | **Source Missing** | [P0] RPC (USDG is a proxy token on Robinhood Chain; issuance mechanism unverified) |

**Collateral Subtotal: 15.00/45 (33.3%)**
- 3 questions scored 3 (= 9), 1 question N/A (ST-C-03)
- Raw sum = 9 out of max 27
- Weighted = (9/27) x 45 = 15.00

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Mid. Dependencies disclosed but include non-Tier-0/1 components: Robinhood Chain (new Orbit L2, not on the SR chain list), Box funding modules (Aave v3, Morpho Blue -- both Tier-0), and custom single-source Morpho market oracles (not a named Tier-0/1 provider). USDG (Paxos) disclosed. As with the sibling, Low becomes reachable if Robinhood Chain earns Tier-0/1 status on the SR list as it matures and the leverage markets migrate to Tier-0/1 price feeds. | 3 | 9 | Time-Based | [P0] RPC (chainId 4663, Box modules), [P4] thirdweb/L2Beat (Robinhood Chain) |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | High. The leverage strategy relies on single-source Morpho market oracles (one oracle per market, no redundancy) and Box oracle-based swap pricing -- none from a named Tier-0/1 redundant provider -- on the same synthetic-stable collateral family whose sibling market the analyst verified uses a hardcoded 1:1 feed. At ~2.4x leverage, an oracle error/depeg is amplified into forced losses. No meaningful redundancy -> High. | 1 | 3 | **Improvable** | [P1] [Box Vaults docs](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults) (oracle risk disclosed), [P0] sibling RPC (hardcoded 1:1 USDe oracle on same family) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Mid. No public SOC 2 Type II / ISO 27001 for Steakhouse or Morpho Labs; the Robinhood Chain sequencer operator's IT certifications are not disclosed. Paxos is a regulated issuer. | 3 | 9 | **Source Missing** | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Mid. Robinhood Chain is <6 months old (mainnet July 1, 2026) with no incidents during its short operational period -- a data gap scores Mid per the new-protocol guidance. | 3 | 9 | Time-Based | [P4] [thirdweb: Robinhood Chain](https://blog.thirdweb.com/robinhood-chain-inside-the-ethereum-l2-bringing-tokenized-stocks-to-120-countries/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Mid. Robinhood Chain is ~3 weeks old with a single centralized sequencer; no halt >30 min observed yet, but there is essentially no track record to support a Low score. | 3 | 9 | Time-Based | [P4] [L2Beat Robinhood](https://l2beat.com/scaling/projects/robinhood) |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- no staking-based collateral. | N/A | N/A | N/A | Vault architecture |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- no staking validator set relevant to the vault collateral. | N/A | N/A | N/A | Vault architecture |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | Mid. Users have permissionless on-chain redemption, but the chain relies on a single sequencer, and the ~90% leveraged portion depends on Box winddown to exit. A sequencer/DA failure could delay withdrawals until an unproven L1 force-inclusion path. | 3 | 9 | Time-Based | [P4] [thirdweb: Robinhood Chain](https://blog.thirdweb.com/robinhood-chain-inside-the-ethereum-l2-bringing-tokenized-stocks-to-120-countries/) |
| ST-IC-09 | How robust is the cross-chain messaging or bridge verification setup? | N/A -- the vault operates on a single chain and performs no cross-chain messaging. | N/A | N/A | N/A | Vault architecture |
| ST-IC-10 | Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting? | N/A -- no cross-chain escrow/minting performed by the vault. | N/A | N/A | N/A | Vault architecture |
| ST-IC-11 | Is the off-chain verification infrastructure resilient to data-source manipulation? | N/A -- the vault relies on no off-chain verifiers; oracle data is consumed on-chain. | N/A | N/A | N/A | Vault architecture |

**Infrastructure Counterparty Subtotal: 13.33/45 (29.6%)**
- 6 scored (ST-IC-06/07/09/10/11 = N/A): 5 scored 3 (= 15), 1 scored 1 (ST-IC-02)
- Raw sum = 16 out of max 54
- Weighted = (16/54) x 45 = 13.33

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Mid. Box funding modules use Aave v3 (Tier-0) and Morpho Blue (Tier-0); collateral value depends on Ethena (USDe), Maple (syrupUSDG; predecessor defaulted 2022), and Spark (spUSDG). Mix of Tier-0 venues and untiered/higher-risk synthetic-credit assets, at leverage. | 3 | 3 | Non-Improvable | [P1] [Box repo funding modules](https://github.com/Steakhouse-Financial/box), [P4] [Robinhood Earn collateral](https://cryptoadventure.com/ethenas-usde-joins-robinhood-earn-as-defi-lending-moves-into-the-main-app/) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Low. Vault performance and management fees are 0% (verified); Steakhouse is the publicly disclosed curator. No hidden vault-level rebates. | 9 | 9 | Non-Improvable (optimal) | [P0] RPC (fees=0), [P1] [Morpho: Robinhood](https://morpho.org/blog/robinhood-chooses-morpho-to-power-new-earn-product) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Mid. On-chain caps exist (increases carry a 3-day timelock) and Box enforces per-module LTV caps relative to LLTV, but there is no hard relative concentration limit at the vault layer (~90% is currently in the single Box leverage adapter). | 3 | 9 | **Improvable** | [P0] RPC (caps, increaseAbsoluteCap timelock=259200s; ~90% in one adapter) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Mid. Unwind depends on borrower repayment / Box winddown (escalating slippage) plus the ~10% repo buffer; new-chain secondary liquidity is thin, and stress unwind of the leverage is slow/costly today. But exit paths are documented and permissionless (Aave/Morpho deleverage, Box winddown -- no discretionary approvals), so Low becomes reachable once exits are demonstrated/tested and chain liquidity matures, mirroring the sibling's Time-Based treatment. | 3 | 9 | Time-Based | [P1] [Box winddown](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults), [P0] RPC (utilization/split) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Low. On-chain lending/leverage with no third-party custody of vault assets. Curator (Steakhouse), funding venues (Aave/Morpho), collateral protocols (Ethena/Maple/Spark), and USDG issuer (Paxos) are all disclosed. Deal Breaker passes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho: Robinhood](https://morpho.org/blog/robinhood-chooses-morpho-to-power-new-earn-product), [P1] [USDG/Paxos](https://docs.paxos.com/guides/stablecoin/usdg) |

**Protocol Counterparty Subtotal: 27.00/45 (60.0%)**
- 2 questions scored 9 (ST-PC-02,05 = 18), 3 questions scored 3 (= 9)
- Raw sum = 27 out of max 45
- Weighted = (27/45) x 45 = 27.00

---

#### Liquidity (5% weight, 45 max points)

**Withdrawal baseline: design-implied instant/permissionless (ERC-4626), but only ~10% of NAV is an immediate repo buffer; the ~90% leveraged portion exits via Box winddown (permissionless after warmup, escalating slippage). Verified split: repo adapter ~$273.8K, Box leverage adapter ~$2.46M of ~$2.73M TVL.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Low. Permissionless on-chain ERC-4626 redemption; gates currently open (no address censorship); no admin pause on the immutable vault; Box winddown is permissionless. Gate changes require a 7-day timelock and Sentinel/guardian veto. | 9 | 9 | Non-Improvable (optimal) | [P0] RPC (gates null), [P1] [Box winddown](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Mid. Only ~10% (~$273.8K) is an immediate repo buffer; near-total exit requires deleveraging/winddown of the ~90% Box position with slippage. Adequate for small-medium exits, not near-total instant exits. Untested at scale. | 3 | 3 | Non-Improvable | [P0] RPC (repo ~$273.8K / leverage ~$2.46M of $2.73M) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | Mid. The vault is ~6 weeks old (deployed ~June 2026); no delays observed yet, but there is insufficient (<6-12 month) time-series to support a Low score. | 3 | 9 | Time-Based | [P0] RPC (vault age), [P3] Steakhouse app |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Low. Morpho V2 caps are allocation-side (absolute caps with 3-day timelocked increases) and structurally cannot gate withdrawals; no history of caps restricting exits. Leverage/utilization-driven exit limits are assessed in ST-L-02/ST-PM-08, not here. Platform-consistent with the sibling and mainnet peers (9 on the identical cap architecture). | 9 | 9 | Non-Improvable (optimal) | [P0] RPC (caps, increaseAbsoluteCap timelock=259200s), [P1] [Box docs](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Mid. No stress history on this new chain and a leveraged position whose unwind involves swaps; behavior under volatility/congestion is unknown -- Mid per the untested principle. | 3 | 9 | Time-Based | [P0] RPC (vault age, leverage) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | Low. No structural unstaking/vesting/bridge lockups on the vault position; exit is via ERC-4626 redemption and Box winddown (swap-based), not time-locks. | 9 | 9 | Non-Improvable (optimal) | [P1] [Box winddown](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Mid. Primary redemption is via ERC-4626 against available liquidity; beyond the repo buffer, unwinding the leverage where collateral != loan asset requires swaps that depend on secondary/DEX liquidity, which is thin on a new L2 and may thin further under stress. | 3 | 3 | Non-Improvable | [P1] [Box slippage/swaps](https://github.com/Steakhouse-Financial/box), [P0] RPC |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | Mid. USDG and the collateral tokens have thin on-chain secondary depth on a 6-week-old L2; depth supports staggered rather than near-total exits. | 3 | 3 | Non-Improvable | [P0] RPC, [P4] [Steakhouse on Robinhood Chain](https://cryptobriefing.com/steakhousefi-vaults-robinhood-chain-users/) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Mid. A run would cause queues and force winddown at escalating slippage; the ~10% buffer + moderate (2.4x) leverage + Box winddown contain losses, but significant discounting is possible. Untested. | 3 | 3 | Non-Improvable | [P1] [Box winddown](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults), [P0] RPC |

**Liquidity Subtotal: 25.00/45 (55.6%)**
- 3 questions scored 9 (ST-L-01,04,06 = 27), 6 questions scored 3 (= 18)
- Raw sum = 45 out of max 81
- Weighted = (45/81) x 45 = 25.00

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | Mid. The vault share (bbqUSDGturbo ERC-4626) is ~6 weeks old, leveraged, and untested under redemption stress on this new chain. | 3 | 9 | Time-Based | [P0] RPC (sharePrice, vault age) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Mid. The vault is USD-denominated throughout, but ~2.4x leverage on synthetic-stable collateral means a collateral depeg or sharp move can cause forced deleveraging and permanent losses in severe-but-plausible stress. | 3 | 3 | Non-Improvable | [P3] app (~2.4x), [P0] RPC |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Mid. Immutable Morpho Adaptive Curve IRM per market, but the leveraged carry is exposed to borrow-rate spikes that compress/invert the spread; untested under stress on this chain. | 3 | 9 | Time-Based | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P0] RPC |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Mid. Steakhouse does scenario/secondary-liquidity modeling and Box adds slippage/LTV controls, but the key tails -- collateral depeg at leverage priced by single-source oracles, and a fast deleverage on a thin chain -- are not demonstrably stress-modeled for this deployment. | 3 | 9 | **Improvable** | [P1] [Box docs](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults), [P1] [Steakhouse Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Mid. At ~2.4x leverage with defined but thin buffers on a new engine, fast drawdowns can trigger liquidations in severe stress if markets gap or liquidity thins; risk is bounded by caps and partial auto-deleveraging but not eliminated. | 3 | 3 | Non-Improvable | [P3] app (~2.4x), [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 15.00/45 (33.3%)**
- 5 questions scored 3 (= 15)
- Raw sum = 15 out of max 45
- Weighted = (15/45) x 45 = 15.00

---

### **Strategy Total: 115.33/270 (42.7%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 20.00 | 45 | 44.4% |
| Collateral | 15.00 | 45 | 33.3% |
| Infra Counterparty | 13.33 | 45 | 29.6% |
| Protocol Counterparty | 27.00 | 45 | 60.0% |
| Liquidity | 25.00 | 45 | 55.6% |
| Market | 15.00 | 45 | 33.3% |
| **Strategy Total** | **115.33** | **270** | **42.7%** |

---

### OPERATIONS (30% Weight) -- Score: 171.00/270 (63.3%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Mid. Core contracts (VaultV2, Box child vault) are immutable, so fund-custody logic cannot be upgraded. Control of config rests with a robust multisig structure (Supervisor 14-day timelock + 5-of-10 Safe owner; 3-of-7 curator Safe) -- not on-chain tokenholder governance. | 3 | 9 | **Improvable** | [P0] RPC (owner Supervisor + 5-of-10 Safe; curator 3-of-7 Safe) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- no governance token or on-chain voting for this vault; concentration is captured under S-KM-01/03. | N/A | N/A | N/A | [P0] RPC (multisig governance) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Mid. Fund-safety functions carry >=24h timelocks (caps 3-day, gates/abdicate 7-day) plus a 14-day Supervisor timelock and Sentinel/guardian vetoes -- BUT `setIsAdapter`, `setIsAllocator`, and fee changes have 0-second timelocks, so a new fund-routing destination can be added instantly (funding it still needs the 3-day cap timelock). Not all sensitive changes are timelocked. | 3 | 9 | **Improvable** | [P0] RPC timelocks: setIsAdapter=0, caps=259200s, gates/abdicate/increaseTimelock=604800s; Supervisor const=1209600s |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Low. The Owner/curator process can appoint a new curator/allocators; withdrawals remain permissionless via ERC-4626 + Box winddown throughout. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P1] [Box docs](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults) |

**Governance Subtotal: 37.50/67.5 (55.6%)**
- 2 questions scored 3 (O-G-01,03 = 6), 1 question scored 9 (O-G-04), 1 question N/A (O-G-02)
- Raw sum = 15 out of max 27
- Weighted = (15/27) x 67.5 = 37.50

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Low. Steakhouse (adcv, Sebastien Derivaux -- ex-MakerDAO), Morpho (Paul Frambot et al.), Robinhood (public company), and Paxos (regulated issuer) are all publicly identified and credible. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse](https://www.steakhouse.financial/), [P1] [Morpho](https://morpho.org/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Low. Multiple substantial organizations support the product (Morpho, Steakhouse, Robinhood, Paxos); no single-developer dependency. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Low. Morpho (ADDMO/Morpho Labs, France), Steakhouse (Panama/Cayman), Robinhood (US public company), Paxos Digital Singapore (USDG issuer, MAS-regulated). Entities and jurisdictions clearly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P1] [USDG/Paxos](https://docs.paxos.com/guides/stablecoin/usdg) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | Mid. Curator/infra (Steakhouse/Morpho) are clean, but two integral entities have past resolved enforcement: Robinhood Crypto (NYDFS $30M, 2022; SEC crypto probe opened 2024, closed 2025) and Paxos (NYDFS BUSD wind-down, 2023). No ongoing material action impairing this product. Deal Breaker passes. | 3 | 3 | Non-Improvable | [P4] Public regulatory records (Robinhood Crypto NYDFS 2022; Paxos BUSD 2023) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Mid. Platform monitoring exists, but no public 24/7 on-call SLA or incident runbook covering this vault's leverage/allocator flows on a new chain, including documented steps to halt automated allocation and force Box shutdown/winddown within an SLA. | 3 | 9 | **Source Missing** | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P1] [Box shutdown/winddown](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Low. Morpho/Steakhouse have demonstrated rapid incident response; Steakhouse publishes regular market updates; Robinhood provides retail support channels. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Low. Morpho's investors are public; Robinhood is the disclosed distribution/chain partner; the Morpho-Steakhouse-Robinhood arrangement is publicly announced. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho: Robinhood](https://morpho.org/blog/robinhood-chooses-morpho-to-power-new-earn-product) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Mid. Steakhouse curates many vaults, including the lower-risk "Steakhouse USDG" vault on the same chain and other Turbo vaults across chains, creating allocation/competition conflicts. The DDQ provides qualitative controls but no published hard conflict rules. | 3 | 9 | **Improvable** | [P1] [Steakhouse Products](https://www.steakhouse.financial/docs/products/vault-products/current) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | Low. Steakhouse has no known uncompensated depositor-loss events across its curated vaults since inception (Jan 2024). | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs) |

**Team & Legal Subtotal: 52.50/67.5 (77.8%)**
- 6 questions scored 9 (= 54), 3 questions scored 3 (O-TL-04,05,08 = 9)
- Raw sum = 63 out of max 81
- Weighted = (63/81) x 67.5 = 52.50

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Low. Morpho V2 docs, Steakhouse Turbo/Box docs, and the public Box GitHub repo comprehensively cover architecture, leverage mechanics, funding modules, and risk controls. | 9 | 9 | Non-Improvable (optimal) | [P1] [Turbo docs](https://www.steakhouse.financial/docs/products/vault-products/current/turbo), [P1] [Box Vaults docs](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Low. Box docs explicitly list loss scenarios (slippage, oracle, liquidity, governance) and the winddown lifecycle; Turbo docs describe leverage-trade loss conditions (slippage, borrow > collateral rate). | 9 | 9 | Non-Improvable (optimal) | [P1] [Box Vaults docs](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults), [P1] [Turbo docs](https://www.steakhouse.financial/docs/products/vault-products/current/turbo) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Mid. The Morpho GraphQL API does not index this vault (chainId 4663 not supported), and the custom Box adapter / Box child vault / Supervisor addresses are not consolidated in one canonical public registry (the vault is on the Steakhouse app; Box code is on GitHub without a per-deployment address registry). | 3 | 9 | **Improvable** | [P0] RPC (addresses discovered directly), [P3] [Steakhouse app](https://app.steakhouse.financial/earn/4663/0xbeEfFF136E3684273e6aA75A1669B784B373A4FD/usdg-turbo) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Low. Morpho V2 role/timelock docs + Box guardian/curator role docs are comprehensive, and per-function timelocks/roles are visible on-chain via RPC. | 9 | 9 | Non-Improvable (optimal) | [P1] [Roles & Capabilities](https://docs.morpho.org/curate/concepts/roles/), [P0] RPC (18 timelocks verified) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Low. Full on-chain proof-of-reserves and proof-of-liabilities (positions and leverage legs auditable in real time); USDG's fiat reserves are attested monthly by Paxos. Deal Breaker passes. | 9 | 9 | Non-Improvable (optimal) | [P0] RPC (positions/adapters), [P1] [USDG/Paxos](https://docs.paxos.com/guides/stablecoin/usdg) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Mid. The core logic corresponds to public, audited open-source code (Morpho V2 on GitHub + Box on GitHub with 2 audits), but the deployed vault, both adapters, the Box child vault, and the Supervisor are NOT verified on the Robinhood Chain explorer (hoodexplorer returns "source code not verified"), and the custom Box adapters add unverified on-explorer surface. | 3 | 9 | **Improvable** | [P0] hoodexplorer getsourcecode (all "not verified"); [P1] [Box GitHub](https://github.com/Steakhouse-Financial/box) |

**Documentation Subtotal: 52.50/67.5 (77.8%)**
- 4 questions scored 9 (= 36), 2 questions scored 3 (O-DT-03,06 = 6)
- Raw sum = 42 out of max 54
- Weighted = (42/54) x 67.5 = 52.50

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Mid. No dedicated safety module for this vault; leverage losses/bad debt would be borne by depositors (with Box winddown as loss-mitigation, not a funded backstop). The Morpho DAO treasury exists but activation is discretionary; no Steakhouse/Robinhood vault-specific backstop is disclosed. | 3 | 9 | **Improvable** | [P3] [DeFiLlama Morpho Treasury](https://api.llama.fi/treasury/morpho), [P1] [Box winddown](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | High. No ring-fenced reserve for this vault. The Morpho DAO treasury (~$27.2M per DeFiLlama, predominantly MORPHO own-token) is not vault-specific and is <1% of protocol-wide TVL; Steakhouse's own reserve is not disclosed. | 1 | 9 | **Source Missing** | [P3] [DeFiLlama Morpho Treasury API](https://api.llama.fi/treasury/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Low. Morpho is well-funded; Steakhouse manages >$4.5B TVL earning curation revenue; Robinhood (a large public company) backs the product. Runway comfortably >24 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/), [P4] [Steakhouse markets update](https://kitchen.steakhouse.financial/p/defi-markets-update-2026-07-21) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | Mid. The vault is ~6 weeks old and has not operated through a stress event -- resilience is unproven per the demonstrated-history principle. The vault token is not widely composed externally, limiting contagion surface. | 3 | 9 | Time-Based | [P0] RPC (vault age, TVL ~$2.73M) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Mid. VaultV2/Box child vault are immutable and withdrawals are permissionless (ERC-4626 + Box permissionless winddown, a genuine positive) -- but continued chain operation depends on Robinhood running the single sequencer, and unwinding leverage if abandoned relies on an unproven L1 escape hatch on a 6-week-old chain. | 3 | 9 | Time-Based | [P1] [Box winddown](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults), [P4] [L2Beat Robinhood](https://l2beat.com/scaling/projects/robinhood) |

**Financial Resilience Subtotal: 28.50/67.5 (42.2%)**
- 1 question scored 9 (O-FR-03), 3 questions scored 3 (O-FR-01,04,05 = 9), 1 question scored 1 (O-FR-02)
- Raw sum = 19 out of max 45
- Weighted = (19/45) x 67.5 = 28.50

---

### **Operations Total: 171.00/270 (63.3%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 37.50 | 67.5 | 55.6% |
| Team & Legal | 52.50 | 67.5 | 77.8% |
| Documentation | 52.50 | 67.5 | 77.8% |
| Financial Resilience | 28.50 | 67.5 | 42.2% |
| **Operations Total** | **171.00** | **270** | **63.3%** |

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 75 | 99 | 136.36 | 180 | 75.8% |
| | Key Management (8 Q) | 54 | 72 | 135.00 | 180 | 75.0% |
| | **Security Subtotal** | | | **271.36** | **360** | **75.4%** |
| **Strategy** | Protocol Mechanics (10 Q) | 40 | 90 | 20.00 | 45 | 44.4% |
| | Collateral (3 of 4 Q scored) | 9 | 27 | 15.00 | 45 | 33.3% |
| | Infra Counterparty (6 of 11 Q scored) | 16 | 54 | 13.33 | 45 | 29.6% |
| | Protocol Counterparty (5 Q) | 27 | 45 | 27.00 | 45 | 60.0% |
| | Liquidity (9 Q) | 45 | 81 | 25.00 | 45 | 55.6% |
| | Market (5 Q) | 15 | 45 | 15.00 | 45 | 33.3% |
| | **Strategy Subtotal** | | | **115.33** | **270** | **42.7%** |
| **Operations** | Governance (3 of 4 Q scored) | 15 | 27 | 37.50 | 67.5 | 55.6% |
| | Team & Legal (9 Q) | 63 | 81 | 52.50 | 67.5 | 77.8% |
| | Documentation (6 Q) | 42 | 54 | 52.50 | 67.5 | 77.8% |
| | Financial Resilience (5 Q) | 19 | 45 | 28.50 | 67.5 | 42.2% |
| | **Operations Subtotal** | | | **171.00** | **270** | **63.3%** |
| **TOTAL** | | | | **557.70** | **900** | **62.0%** |

---

## Validation Checklist

- [x] Smart Contract Security: (7x9 + 4x3) = 63+12 = 75/99. 75/99 x 180 = 136.36 (verified)
- [x] Key Management: (5x9 + 3x3) = 45+9 = 54/72. 54/72 x 180 = 135.00 (verified)
- [x] Security subtotal: 136.36 + 135.00 = 271.36 (verified)
- [x] Protocol Mechanics: (2x9 + 7x3 + 1x1) = 18+21+1 = 40/90 (10 Q, none N/A). 40/90 x 45 = 20.00 (verified)
- [x] Collateral: (3x3) = 9/27 (1 N/A: ST-C-03). 9/27 x 45 = 15.00 (verified)
- [x] Infra Counterparty: (5x3 + 1x1) = 15+1 = 16/54 (5 N/A: ST-IC-06/07/09/10/11). 16/54 x 45 = 13.33 (verified)
- [x] Protocol Counterparty: (2x9 + 3x3) = 18+9 = 27/45. 27/45 x 45 = 27.00 (verified)
- [x] Liquidity: (3x9 + 6x3) = 27+18 = 45/81. 45/81 x 45 = 25.00 (verified)
- [x] Market: (5x3) = 15/45. 15/45 x 45 = 15.00 (verified)
- [x] Strategy Total: 20.00 + 15.00 + 13.33 + 27.00 + 25.00 + 15.00 = 115.33 (verified)
- [x] Governance: (1x9 + 2x3) = 9+6 = 15/27 (1 N/A: O-G-02). 15/27 x 67.5 = 37.50 (verified)
- [x] Team & Legal: (6x9 + 3x3) = 54+9 = 63/81. 63/81 x 67.5 = 52.50 (verified)
- [x] Documentation: (4x9 + 2x3) = 36+6 = 42/54. 42/54 x 67.5 = 52.50 (verified)
- [x] Financial Resilience: (1x9 + 3x3 + 1x1) = 9+9+1 = 19/45. 19/45 x 67.5 = 28.50 (verified)
- [x] Operations Total: 37.50 + 52.50 + 52.50 + 28.50 = 171.00 (verified)
- [x] Grand Total: 271.36 + 115.33 + 171.00 = 557.70 (verified)
- [x] All percentages <= 100%: Yes (verified)
- [x] No score exceeds its maximum: Yes (verified)
- [x] Rating Overview table matches Final Score Calculation: Yes (verified)
- [x] Grade check: CCC range is 500-580; 557.70 falls within CCC (verified)
- [x] Potential: 360.00 + 210.67 + 265.00 = 835.67; BBB+ range 834-846 (verified)

---

## Rating Determination

| Grade | Range | This Vault |
|-------|-------|------------|
| CCC+ | 580-660 | - |
| **CCC** | **500-580** | **557.70 points** |
| CCC- | 420-500 | - |

## **FINAL RATING: CCC**

*Very high risk; major loss meaningful if conditions deteriorate. Turbo inherits Morpho's immutable, formally-verified V2 core and adds a custom Box leverage engine that -- unlike a typical unaudited fork -- carries two independent Tier-0 audits (ChainSecurity, Cantina), and it is governed by a genuinely robust on-chain key structure (a 14-day-timelocked Supervisor owned by a 5-of-10 Safe, a 3-of-7 curator Safe, and a 1-of-7 Sentinel), which lifts it above its single-EOA-owned sibling on Key Management. But the product's defining feature -- a ~2.4x leveraged carry on synthetic/credit stablecoin collateral, priced by single-source oracles, on a 6-week-old single-sequencer L2 with a ~10% liquidity buffer and zero stress history -- is a permanent, structural risk multiplier. Leverage drags Strategy to CC (115.3/270) — with the carry spread itself scoring High on inversion risk (ST-PM-09, consistent with the Ethena sUSDe and Hermetica hBTC precedents) — the oracle-at-leverage path scores High (ST-IC-02), the live leverage config sits outside audit scope (S-SC-01) with contracts unverified on-chain (O-DT-06), and adapter addition is instant on-chain (O-G-03). No deal breakers trigger; the maximum achievable grade with monitoring/automated circuit-breakers, a config-inclusive audit, hard caps, signer disclosure, a backstop, and a stress track record is BBB+ (835.7), a ceiling still below the plain-lending sibling's (A-/846.4) because the leverage constraint permanently caps the Strategy ceiling, though the Box architecture's automatable safety controls and multisig key management give Turbo a perfect Security potential (360.0) the sibling cannot reach.*

---

## Key Risks

1. **~2.4x leverage on synthetic/credit stablecoin collateral (ST-PM-09 = 1; ST-PM-02, ST-PM-03, ST-M-02, ST-M-05 = 3)**: ~90% of NAV (~$2.46M verified on-chain) sits in the "Box Turbo USDG" leverage engine looping into Morpho Blue/Aave v3 markets against USDe/syrupUSDG/spUSDG. The strategy is primarily a leveraged carry — well above 70% of expected yield comes from the invertible collateral-rate-minus-borrow-rate spread, scoring High on inversion risk in line with the Ethena sUSDe and Hermetica hBTC carry-trade ratings. Losses are plausible (not tail-only) from collateral depeg, negative carry (borrow rate > collateral rate, per the Turbo docs), slippage, or forced deleveraging. -- [P3] Steakhouse app (~2.4x), [P1] [Turbo docs](https://www.steakhouse.financial/docs/products/vault-products/current/turbo)

2. **Oracle risk amplified by leverage (ST-IC-02 = 1)**: The leverage relies on single-source, non-Tier-0/1 Morpho market oracles (no redundancy) and Box oracle-based swap pricing, on the same synthetic-stable collateral family whose sibling market the analyst verified uses a hardcoded 1:1 feed. At 2.4x, an oracle error or undetected depeg is magnified into forced losses. -- [P1] [Box oracle-risk disclosure](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults)

3. **Live leverage config unaudited + contracts unverified on-chain (S-SC-01 = 3, O-DT-06 = 3)**: The Box code is audited (ChainSecurity Dec 2025, Cantina Jan 2026), but the deployed leverage configuration (funding modules, oracle wiring, collateral whitelist, leverage caps on Robinhood Chain) is not in audit scope, and the vault, both adapters, the Box child vault, and the Supervisor are all "source code not verified" on hoodexplorer. -- [P0] hoodexplorer getsourcecode (all not verified), [P1] [Box audits](https://github.com/Steakhouse-Financial/box/tree/52ab8b9f20184c5882448df7be31701df1cf6f39/audits)

4. **Instant adapter addition weakens leverage guardrails (O-G-03 = 3, S-KM-07 = 3)**: On-chain, `setIsAdapter` has a 0-second timelock, so the 3-of-7 curator Safe can add a new fund-routing destination instantly (funding it still requires the 3-day cap timelock + Sentinel/guardian veto). This is a weaker guardrail than the sibling's uniform 7-day timelocks. -- [P0] RPC (setIsAdapter timelock = 0; caps = 259,200s)

5. **Thin liquidity buffer on a leveraged position (ST-L-02, ST-L-09, ST-PM-08 = 3)**: Only ~10% (~$273.8K verified) is an immediate repo buffer; the ~90% leveraged portion exits via Box winddown with escalating slippage. Near-total or stressed exits on a 6-week-old, thin-liquidity single-sequencer L2 are untested and could crystallize discounts. -- [P0] RPC (repo ~$273.8K / leverage ~$2.46M of $2.73M)

6. **Brand-new centralized L2 with no stress history (ST-IC-05, ST-IC-08, O-FR-04 = 3)**: Robinhood Chain (mainnet July 1, 2026) runs a single centralized sequencer and has ~3 weeks of operating history; a sequencer/DA failure could delay withdrawals until an unproven L1 escape hatch, and the vault has never operated through a stress event. -- [P4] [L2Beat Robinhood](https://l2beat.com/scaling/projects/robinhood)

7. **No dedicated backstop; treasury not ring-fenced (O-FR-01 = 3, O-FR-02 = 1)**: Leverage losses would be borne by depositors; the Morpho DAO treasury (~$27.2M, predominantly volatile MORPHO) is protocol-wide, <1% of TVL, and not ring-fenced for this vault, and no Steakhouse/Robinhood-specific reserve is disclosed. -- [P3] [DeFiLlama Morpho Treasury](https://api.llama.fi/treasury/morpho)

---

## Improvement Roadmap

### Quick Wins (High Impact, Low Effort)

1. **Disclose curator/supervisor signer independence and document a tested key-compromise/signer-loss playbook** [S-KM-03, S-KM-08] -- 3 → 9
2. **Add a hard on-chain timelock to `setIsAdapter` and hard relative concentration caps** [S-KM-07, ST-PC-03, O-G-03] -- 3 → 9
3. **Connect monitoring to automated protective actions and list the Box code in a bug bounty** [S-SC-10, S-SC-09] -- 3 → 9
4. **Verify all deployed contracts on hoodexplorer and publish a canonical Box address registry** [O-DT-06, O-DT-03] -- 3 → 9

### Medium-Term Improvements (High Impact, Moderate Effort)

5. **Commission a deployment-config-inclusive audit of the live leverage setup** [S-SC-01] -- 3 → 9
6. **Add automated, monitoring-triggered circuit breakers for abnormal conditions (wiring the existing Box shutdown/cap levers to automatic execution) and confirm always-on automated deleveraging** [S-SC-11, ST-PM-10, ST-PM-04, ST-M-04] -- 3 → 9
7. **Upgrade the leverage-market oracles to correctable, redundant feeds** [ST-IC-02] -- 1 → 3 (capped by single-oracle-per-market design)
8. **Establish a ring-fenced backstop reserve and disclose treasury detail; publish an on-call SLA and conflict-of-interest policy** [O-FR-01, O-FR-02, O-TL-05, O-TL-08] -- 3/1 → 9

### Long-Term / Time-Based (Track Record & Chain Maturity)

9. **Build operating and stress track record; mature chain tier status and demonstrated unwind paths; decentralize the sequencer** [ST-IC-01, ST-IC-04/05/08, ST-PC-04, ST-L-03/05, ST-M-01/03, ST-PM-01/05, O-FR-04/05] -- 3 → 9 over time

### Evidence Gaps (Source Missing Items)

10. **Obtain SOC 2 / ISO 27001 and confirm native issuance of the collateral tokens on Robinhood Chain** [ST-IC-03, ST-C-04] -- 3 → 9

**Maximum Achievable Grade:** BBB+ (835.67/900 points) if all improvable, source-missing, and time-based items are addressed. The ceiling remains below the plain-lending sibling's (A-/846.4) and well below the mainnet Steakhouse peers because the ~2.4x leverage is a permanent structural constraint on Strategy (ST-PM-02/03/08, ST-C-01, ST-PC-01, ST-L-02/07/08/09, ST-M-02/05 remain capped at Mid; ST-PM-09 remains High) — although on Security the Box architecture supports automated safety controls (S-SC-11 → 9, structurally unreachable for the sibling), giving Turbo a perfect 360.0 Security potential.

**Points to Next Grade Tier (CCC+):** 22.3 points needed to reach CCC+ (580 points).

---

## Smart Contract Addresses

| Role | Address | Explorer Link |
|------|---------|---------------|
| VaultContract | 0xbeEfFF136E3684273e6aA75A1669B784B373A4FD | [hoodexplorer](https://www.hoodexplorer.org/address/0xbeEfFF136E3684273e6aA75A1669B784B373A4FD) |
| Owner (Supervisor, 14-day timelock) | 0x261a3b7a37904b45e57ae14206314ccf4bbcf2b1 | [hoodexplorer](https://www.hoodexplorer.org/address/0x261a3b7a37904b45e57ae14206314ccf4bbcf2b1) |
| Supervisor Owner (5-of-10 Safe) | 0xd062020d07facf39b5a06c34b07d81c43f615ef4 | [hoodexplorer](https://www.hoodexplorer.org/address/0xd062020d07facf39b5a06c34b07d81c43f615ef4) |
| Curator (3-of-7 Safe) | 0x9023FBD6A08C666491A2d1648737E400cF42D2Fb | [hoodexplorer](https://www.hoodexplorer.org/address/0x9023FBD6A08C666491A2d1648737E400cF42D2Fb) |
| Sentinel (1-of-7 Safe) | 0x5642BCd50fC751fF2d04f155423e4D0E25C2a744 | [hoodexplorer](https://www.hoodexplorer.org/address/0x5642BCd50fC751fF2d04f155423e4D0E25C2a744) |
| BoxAdapter (leverage, ~90% of NAV) | 0xec1f17758a4656cc4deae264ead1f6d83c6bea29 | [hoodexplorer](https://www.hoodexplorer.org/address/0xec1f17758a4656cc4deae264ead1f6d83c6bea29) |
| Box Turbo USDG child vault (leverage engine) | 0x3e35b42b20ae940e3b8a1aa40766100aeef13ee7 | [hoodexplorer](https://www.hoodexplorer.org/address/0x3e35b42b20ae940e3b8a1aa40766100aeef13ee7) |
| Morpho Market V1 adapter (repo liquidity, ~10%) | 0xda889f343359ca9766381080f1bf505458bb2513 | [hoodexplorer](https://www.hoodexplorer.org/address/0xda889f343359ca9766381080f1bf505458bb2513) |
| USDG Token (base asset) | 0x5fc5360D0400a0Fd4f2af552ADD042D716F1d168 | [hoodexplorer](https://www.hoodexplorer.org/address/0x5fc5360D0400a0Fd4f2af552ADD042D716F1d168) |

## Additional Info

| Field | Value |
|-------|-------|
| Infrastructure Provider | Morpho / Box |
| Protocol Base | _none_ |
| Stated Withdrawal Time | Instant |
| Treasury | 27200000 |
| Treasury Addresses | 0xcBa28b38103307Ec8dA98377ffF9816C164f9AFa (Ethereum, Base -- Morpho DAO governance multisig), 0xF057afeEc22E220f47AD4220871364e9E828b2e9 (Ethereum -- Morpho rewards multisig), 0x5Eb982bb1E620cC3927E5CF8A5D207e667643297 (Base -- Morpho rewards multisig) |

*Note: Treasury shown is the protocol-level Morpho DAO treasury (~$27.2M, predominantly MORPHO own-token); it is NOT ring-fenced for this vault. Steakhouse's own curator reserve is not publicly disclosed. See O-FR-01/02.*

### Code Audits

| Auditor | Report Link |
|---------|-------------|
| ChainSecurity (Steakhouse Box, Dec 2025) | [2025-12-16-chainsecurity.pdf](https://github.com/Steakhouse-Financial/box/blob/52ab8b9f20184c5882448df7be31701df1cf6f39/audits/2025-12-16-chainsecurity.pdf) |
| Cantina (Steakhouse Box, Jan 2026) | [2026-01-06-cantina.pdf](https://github.com/Steakhouse-Financial/box/blob/52ab8b9f20184c5882448df7be31701df1cf6f39/audits/2026-01-06-cantina.pdf) |
| ChainSecurity (Morpho Vault V2 base) | [Morpho Vault V2 Audit](https://www.chainsecurity.com/security-audit/morpho-vault-v2) |
| Certora (Morpho Blue formal verification) | [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| Spearbit / Cantina (Morpho V2 base) | [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/) |

*Note: The Box audits cover the Box code at commit 52ab8b9f. They do not cover the live Robinhood Chain leverage deployment configuration (funding modules, oracle wiring, collateral whitelist, leverage caps), which is assessed under S-SC-01 and ST-IC-02.*

### Oracles Used

| Oracle | Documentation Link |
|--------|-------------------|
| Custom Morpho market oracles (single-source per market; no named Tier-0/1 redundant provider) -- repo market id 0xf070cd29… | [Morpho Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| Box oracle-based swap/valuation pricing (drives cumulative slippage caps within the leverage engine) | [Box Vaults docs](https://www.steakhouse.financial/docs/products/infrastructure/box-vaults) |

## Sources

1. [P0] Robinhood Chain RPC -- https://rpc.mainnet.chain.robinhood.com (chainId 0x1237=4663; vault name "Steakhouse Turbo USDG"/symbol bbqUSDGturbo; totalAssets ~$2.73M; owner=Supervisor 0x261a3b7a with 0x127500=14-day const; Supervisor owner=5-of-10 Safe 0xd062020d; curator=3-of-7 Safe 0x9023FBD6; Sentinel=1-of-7 Safe 0x5642BCd5; fees=0; gates=null; adaptersLength=2; per-function timelocks; adapter realAssets/box() probes; queried 2026-07-22)
2. [P0] hoodexplorer (Blockscout) getsourcecode API -- https://www.hoodexplorer.org/api?module=contract&action=getsourcecode (vault/adapters/Box child vault/Supervisor all "source code not verified")
3. [P1] Steakhouse Turbo product docs -- https://www.steakhouse.financial/docs/products/vault-products/current/turbo
4. [P1] Steakhouse Box Vaults docs -- https://www.steakhouse.financial/docs/products/infrastructure/box-vaults
5. [P1] Steakhouse Box GitHub repo (code + audits) -- https://github.com/Steakhouse-Financial/box
6. [P1] Box ChainSecurity audit (Dec 2025) -- https://github.com/Steakhouse-Financial/box/blob/52ab8b9f20184c5882448df7be31701df1cf6f39/audits/2025-12-16-chainsecurity.pdf
7. [P1] Box Cantina audit (Jan 2026) -- https://github.com/Steakhouse-Financial/box/blob/52ab8b9f20184c5882448df7be31701df1cf6f39/audits/2026-01-06-cantina.pdf
8. [P1] Morpho Vault V2 Documentation -- https://docs.morpho.org/learn/concepts/vault-v2/
9. [P1] Morpho Roles & Capabilities -- https://docs.morpho.org/curate/concepts/roles/
10. [P1] Morpho Security Reviews / Audits -- https://docs.morpho.org/get-started/resources/audits/
11. [P1] ChainSecurity Morpho Vault V2 Audit -- https://www.chainsecurity.com/security-audit/morpho-vault-v2
12. [P1] Morpho Formal Verification (Certora) -- https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/
13. [P1] Cantina Morpho Bug Bounty -- https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3
14. [P1] Immunefi Bug Bounty (Morpho) -- https://immunefi.com/bug-bounty/morpho/
15. [P1] Morpho Security Framework -- https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/
16. [P1] Morpho: Robinhood Chooses Morpho to Power New Earn Product -- https://morpho.org/blog/robinhood-chooses-morpho-to-power-new-earn-product
17. [P1] Morpho Legal Notice -- https://morpho.org/legal-notice/
18. [P1] USDG Overview -- Paxos Documentation -- https://docs.paxos.com/guides/stablecoin/usdg
19. [P1] Steakhouse Current Vault Products -- https://www.steakhouse.financial/docs/products/vault-products/current
20. [P1] Steakhouse Vault Controls -- https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls
21. [P3] Steakhouse App -- Turbo USDG (Robinhood Chain) -- https://app.steakhouse.financial/earn/4663/0xbeEfFF136E3684273e6aA75A1669B784B373A4FD/usdg-turbo
22. [P3] DeFiLlama Morpho Treasury API -- https://api.llama.fi/treasury/morpho (~$27.2M, predominantly MORPHO)
23. [P2] Steakhouse DeFi Markets Update (2026-07-21) -- https://kitchen.steakhouse.financial/p/defi-markets-update-2026-07-21
24. [P4] thirdweb: Robinhood Chain (single sequencer overview) -- https://blog.thirdweb.com/robinhood-chain-inside-the-ethereum-l2-bringing-tokenized-stocks-to-120-countries/
25. [P4] L2Beat -- Robinhood Chain -- https://l2beat.com/scaling/projects/robinhood
26. [P4] Crypto Briefing: SteakhouseFi vaults on Robinhood Chain -- https://cryptobriefing.com/steakhousefi-vaults-robinhood-chain-users/
27. [P4] Crypto Adventure: Ethena USDe joins Robinhood Earn (collateral markets) -- https://cryptoadventure.com/ethenas-usde-joins-robinhood-earn-as-defi-lending-moves-into-the-main-app/

---

**Rating Analyst:** DeFi Risk Auditor Agent
**Methodology:** Staking Rewards DeFi Protocol Rating Framework v0.1-gamma
**Date:** 2026-07-22
