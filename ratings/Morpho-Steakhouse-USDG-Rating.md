# Morpho - Steakhouse USDG Vault Risk Rating

**Rating Date**: 2026-07-22
**Analyst**: DeFi Risk Auditor Agent
**Final Grade**: CCC+
**Total Score**: 587.5/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Executive Summary

The Steakhouse USDG vault (`0xBeEff033F34C046626B8D0A041844C5d1A5409dd`) is a Morpho Vault V2 curated by Steakhouse Financial and deployed on **Robinhood Chain** — a brand-new Arbitrum Orbit L2 (chainId 4663) whose mainnet went live on July 1, 2026. It is the on-chain engine behind the retail "Robinhood Earn" product: eligible Robinhood users deposit USDG (Paxos' MAS/MiCA-regulated Global Dollar) and the vault lends that USDG into Morpho Blue markets against three collateral types — **USDe** (Ethena's synthetic dollar, the dominant market at ~$155M chain-wide supply), **syrupUSDG** (Maple institutional-credit receipt), and **spUSDG** (Spark savings) — all at an aggressive 91.5% LLTV. Verified on-chain (Morpho GraphQL API + Robinhood Chain RPC, 2026-07-22): TVL ≈ $169.98M, performance fee 0%, management fee 0%, net APY ≈ 2.72%, immediate liquidity ≈ $25M (~15% of TVL), gates open (permissionless withdrawals), one MarketV1 adapter (`0x44ABc1d6...`).

The vault inherits Morpho's industry-leading smart-contract security — the immutable VaultV2 codebase and Morpho Blue core are the same contracts audited by Tier-0/1 firms (ChainSecurity, Spearbit, Blackthorn, Certora, Zellic, Cantina) and formally verified, with active Cantina/Immunefi bounties. That keeps Smart Contract Security strong (158.2/180). **However, three verified, vault-specific findings pull the rating down sharply relative to the mainnet Steakhouse peers.** First, the **vault Owner is a single externally-owned account** (`0x337feFE4...`, nonce 1, no contract code on Robinhood Chain) — not a multisig or DAO; the emergency Sentinel is a deployed 1-of-7 Safe, but the top admin role is a single key. Second, the **dominant USDe collateral is priced by a hardcoded 1:1 oracle** — the market oracle (`0xE64849bd...`, a 45-byte contract) returns exactly 1e24 (fixed USDe = 1 USDG) and cannot be corrected, so a USDe depeg would not trigger liquidation and would socialize bad debt to lenders. Third, the vault runs on a **3-week-old, single-sequencer L2** with no operating track record, against synthetic/credit collateral that is materially riskier than the BTC/ETH backing the mainnet Steakhouse vaults.

The net effect is a CCC+ grade (587.5/900): excellent code security and credible operators (Morpho, Steakhouse, Robinhood, Paxos) offset by a single-key owner, a fixed-price oracle on the largest collateral market, aggressive LLTVs on synthetic/credit assets, an unproven centralized chain, and zero stress history. No deal breakers trigger — the immutable vault, 7-day timelocks on fund-routing functions, the 1-of-7 Sentinel veto, and permissionless ERC-4626 redemption mean the single-key owner cannot unilaterally move funds or upgrade custody — but the accumulation of elevated risks places this vault well below its mainnet siblings (BB+/BB-). The maximum achievable grade if the owner is moved to a robust multisig, the oracle is upgraded to a correctable feed, circuit breakers/hard caps are added, and the vault, chain, and collateral tokens build a clean operating and stress track record is A- (846.4/900) — still below the mainnet Steakhouse peers' potentials (A/A+).

---

## Rating Overview

| Category | Weight | Current Score | Max Score | Current % | Potential Score | Potential % |
|----------|--------|---------------|-----------|-----------|-----------------|-------------|
| Security | 40% | 238.2 | 360 | 66.2% | 349.1 | 97.0% |
| Strategy | 30% | 148.3 | 270 | 54.9% | 232.3 | 86.0% |
| Operations | 30% | 201.0 | 270 | 74.4% | 265.0 | 98.1% |
| **Total** | **100%** | **587.5** | **900** | **65.3%** | **846.4** | **94.0%** |

**Current Grade**: CCC+ (587.5/900 points)
**Potential Grade**: A- (846.4/900 points) - achievable if all improvements made

---

## Deal Breaker Assessment

| Question Code | Deal Breaker Type | Status | Impact |
|---------------|-------------------|--------|--------|
| [S-SC-01] Audits | Category | PASS | No cap -- immutable VaultV2 + Morpho Blue core audited by Tier-0/1 firms with public reports |
| [S-SC-06] Exploits | Full | PASS | No cap -- no confirmed exploit with user-fund loss in Steakhouse/Morpho V2 vaults or this vault |
| [S-SC-07] Rug Pull | Full | PASS | No cap -- no rug-pull events |
| [S-KM-02] Single Key Control | Category | PASS (Mid) | No cap -- Owner is a single EOA, but immutable vault + 7-day timelocks + 1-of-7 Sentinel veto + permissionless redemption prevent unilateral fund movement or custody upgrade |
| [ST-PM-05] Strategy Losses | Category | PASS | No cap -- no permanent-loss events for comparable Steakhouse stablecoin-lending vaults |
| [ST-PC-05] Third-Party Disclosure | Category | PASS | No cap -- on-chain lending; curator (Steakhouse), USDG issuer (Paxos), and collateral protocols (Ethena/Maple/Spark) all disclosed |
| [O-TL-04] Regulatory Actions | Category | PASS (Mid) | No cap -- past resolved enforcement against Robinhood Crypto (NYDFS 2022) and Paxos (BUSD 2023); no ongoing material action impairing this product |
| [O-DT-05] Proof of Reserves | Category | PASS | No cap -- full on-chain proof-of-reserves; USDG reserves attested monthly by Paxos |

**Deal Breaker Summary**: No deal breakers triggered. The vault passes all critical safety checks. S-KM-02 and O-TL-04 land at Mid (3), which does not cap.

---

## Improvement Summary

| Classification | Count | Notes |
|----------------|-------|-------|
| Improvable | 14 | Single-EOA owner, monitoring, circuit breakers, caps, oracle upgrade, conflict policy, safety module |
| Source Missing | 4 | SOC 2 certs, on-call SLA, treasury disclosure, bridge/native-issuance status of collateral |
| Time-Based (track record) | 12 | Chain maturity/tier listing, stress history, vault-token peg, collateral peg history, unwind/exit liquidity maturation, resilience |
| Non-Improvable (structural) | ~9 | Collateral choice, immutable single-oracle cap, structural near-total-exit liquidity, past regulatory history, no-pause design |
| Already Optimal | remainder | Morpho code security, non-custodial design, documentation |

**Total Improvement Potential:** +258.9 points (587.5 to 846.4)

**Top Improvement Opportunities (ranked by weighted point impact):**

1. **Migrate Owner from a single EOA to a robust multisig** [S-KM-01, S-KM-03, S-KM-04, S-KM-07, S-KM-02, O-G-01]: multiple questions 1/3 → 9 (+~110 weighted KM points + governance) -- Improvable
2. **Replace the hardcoded USDe oracle with a correctable price feed** [ST-IC-02]: 1 → 3 (capped by immutable single-oracle design), plus improves ST-M-04 -- Improvable
3. **Add on-chain circuit breakers and hard relative caps** [ST-PM-10, ST-PC-03]: 3 → 9 where achievable -- Improvable (S-SC-11 itself is structural: the immutable no-pause design caps it at Mid, matching the mainnet peers)
4. **Disclose/establish a backstop reserve and treasury detail** [O-FR-01, O-FR-02]: 3/1 → 9 -- Improvable / Source Missing
5. **Connect monitoring to automated protections** [S-SC-10]: 3 → 9 -- Improvable
6. **Publish incident playbook, on-call SLA, conflict-of-interest policy, SOC 2** [S-KM-08, O-TL-05, O-TL-08, ST-IC-03]: 3 → 9 -- Improvable / Source Missing
7. **Build operating and stress track record; mature chain, liquidity and collateral history; decentralize the sequencer** [ST-IC-01, ST-IC-04/05/08, ST-PM-08, ST-C-02, ST-PC-04, ST-L-03, ST-L-05, ST-M-01, O-FR-04/05]: 3 → 9 over time -- Time-Based

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 238.2/360 (66.2%)

#### Smart Contract Security (20% weight, 180 max points)

**NOTE: Smart Contract Security is platform-level. The VaultV2 and Morpho Blue contracts deployed on Robinhood Chain are the same immutable, audited bytecode used across all Morpho V2 deployments. These scores match the Morpho Steakhouse Prime Instant V2 peers. The Robinhood Chain *deployment configuration* (hardcoded oracle, single-EOA owner) is a separate concern scored under ST-IC-02 and Key Management, not here.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | Yes. The VaultV2 codebase and Morpho Blue core (immutable) are audited by >=2 Tier-0/1 firms with public reports (ChainSecurity Sep 2025, Spearbit, Blackthorn, Certora, Zellic, Cantina competition) and formally verified. Same audited bytecode is deployed on Robinhood Chain. Caveat: the Robinhood Chain oracle/market configuration is not covered by these mainnet audits (assessed in ST-IC-02). | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/), [P1] [ChainSecurity V2](https://www.chainsecurity.com/security-audit/morpho-vault-v2), [P0] Vault verified via RPC (Morpho V2 bytecode) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent V2 audits by Certora (Tier-0), Spearbit (Tier-0 via Cantina), ChainSecurity (Tier-0), Blackthorn. Multiple Tier-0 firms. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. VaultV2 and Morpho Blue are immutable (non-upgradeable). No upgrade path exists on this vault; every V2 component was preceded by Tier-0 audits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/), [P0] Morpho V2 API |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. V2 audit findings resolved and re-verified before deployment; Certora formal verification provides mathematical proof of critical invariants. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | VaultV2 is immutable (ERC-4626). Morpho Blue is immutable. Adapter/gate/cap changes require 7-day timelocks; the Sentinel can revoke pending actions. No upgrade of fund-custody logic possible. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (timelocks), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit with user-fund loss in Steakhouse/Morpho V2 vaults. This vault (launched ~July 1, 2026) has had no incidents. The March 2026 Resolv and April 2026 Kelp/rsETH incidents did not affect Steakhouse vaults. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P2] [Steakhouse DeFi Update](https://kitchen.steakhouse.financial/p/defi-markets-update-2026-04-22) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho is a nonprofit (ADDMO); Steakhouse has a multi-year clean curation track record. No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. Deployed with 7-day timelocks on fund-routing/gate/cap/abdicate functions; 0-second base on fee/allocator/penalty functions is the original configuration (not a reduction). Per Morpho V2 design, decreasing a function's timelock is itself subject to that function's current timelock, preventing instant reduction of the 7-day fund-safety timelocks. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (18 per-function timelocks verified), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Cantina ($2.5M max, covers Morpho V2 contracts) and Immunefi ($2.5M Morpho Blue). Both Tier-0 platforms; V2 contracts in scope. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3), [P1] [Immunefi](https://immunefi.com/bug-bounty/morpho/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Morpho monitoring bots + Chainalysis exist at the platform level, but responses require manual human intervention and no automated protective action covers this vault's allocator flows. On a 3-week-old chain, monitoring maturity for these specific markets is unverified. | 3 | 9 | **Improvable** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. The Sentinel can only revoke pending timelocked actions; it cannot pause the protocol or halt allocation. Morpho Blue market isolation provides containment. | 3 | 3 | Non-Improvable | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P0] Sentinel = 1-of-7 Safe (RPC) |

**Smart Contract Security Subtotal: 158.2/180 (87.9%)**
- 9 questions scored 9 (sum = 81), 2 questions scored 3 (sum = 6)
- Raw sum = 87 out of max 99
- Weighted = (87/99) x 180 = 158.2

---

#### Key Management & Permissions (20% weight, 180 max points)

**NOTE: This is the primary driver of the low Security score and the biggest difference from the mainnet Steakhouse V2 peers. On-chain verification (Robinhood Chain RPC, chainId 4663 confirmed) shows the vault Owner (`0x337feFE4...`) has NO contract code and nonce 1 -- it is a single EOA, not a multisig or DAO. The Sentinel (`0x5642BCd5...`) IS a deployed 1-of-7 Safe. The recurring "curator" addresses from the Morpho API (0x0A0e..., 0x827e...) also have no code on Robinhood Chain (they are the mainnet Steakhouse multisig addresses, mirrored as EOAs here).**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | High risk. The vault Owner is a single EOA (`0x337feFE4...`, verified: eth_getCode = 0 bytes, nonce 1) -- the top admin role of a ~$170M vault is held by one key, not a diversified multisig or governance. | 1 | 9 | **Improvable** | [P0] RPC eth_getCode/getTransactionCount on 0x337feFE4...; vault.owner() = 0x337feFE4... |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | Mid. Despite the single-EOA owner, no single key can move user funds or upgrade custody: VaultV2/Morpho Blue are immutable, users have permissionless ERC-4626 redemption, adapter/gate/cap changes carry 7-day timelocks, the forceDeallocate penalty is capped, and the 1-of-7 Sentinel can revoke pending actions. The owner can instantly change only fee/allocator/penalty parameters (yield, not principal). Not High -- Deal Breaker does not trigger. | 3 | 9 | **Improvable** | [P0] Morpho V2 API (timelocks), RPC (immutable vault, Sentinel 1-of-7), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | High risk. Critical actions are initiated by the single-EOA Owner (1-of-1 effective control). The Sentinel is a 1-of-7 Safe but can only veto/reduce, not initiate. No multisig controls the critical-action path. | 1 | 9 | **Improvable** | [P0] RPC: owner is EOA; Sentinel getThreshold()=1, getOwners()=7 |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Mid. Gates are currently all null (open) -- withdrawals are permissionless with no address censorship today. The immutable vault has no pause. But the single-EOA Owner could set restrictive gates (address-level control is a V2 feature) subject to a 7-day timelock and Sentinel revoke. Control rests with a single key rather than a multisig. | 3 | 9 | **Improvable** | [P0] Morpho V2 API gatesConfig (all null), timelocks=604800s on gate functions |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of vault assets are held in non-custodial on-chain Morpho contracts. USDG's fiat reserves at Paxos are the issuer's custody (assessed as counterparty risk), not the vault's custody. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P0] Morpho V2 API |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. On-chain segregation; performance and management fees are 0% (fee recipients = zero address). No co-mingling with treasury/ops wallets. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (performanceFee=0, managementFee=0, recipients=0x0) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | Mid. On-chain enforced adapter/cap whitelist (one MarketV1 adapter routing to whitelisted USDe/syrupUSDG/spUSDG markets); adapter additions and cap increases require 7-day timelocks. But changes are controlled by the single-EOA Owner (not a multisig), and relative caps are set to 100% (no hard concentration limit). | 3 | 9 | **Improvable** | [P0] Morpho V2 API (1 adapter, caps: relativeCap=1e18=100%), RPC |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No published, tested playbook for this vault's novel single-EOA-owner + 1-of-7-Sentinel structure on a new chain. Key-rotation/signer-loss procedures for the EOA owner are undocumented. | 3 | 9 | **Improvable** | [P2] [Supervisor V2 Blog](https://kitchen.steakhouse.financial/p/launching-supervisor-v2-and-migration) |

**Key Management Subtotal: 80.0/180 (44.4%)**
- S-KM scores: 1, 3, 1, 3, 9, 9, 3, 3
- 2 questions scored 9 (S-KM-05, S-KM-06 = 18), 4 questions scored 3 (S-KM-02/04/07/08 = 12), 2 questions scored 1 (S-KM-01/03 = 2)
- Raw sum = 18 + 12 + 2 = 32 out of max 72
- Weighted = (32/72) x 180 = 80.0

---

### **Security Total: 238.2/360 (66.2%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 158.2 | 180 | 87.9% |
| Key Management | 80.0 | 180 | 44.4% |
| **Security Total** | **238.2** | **360** | **66.2%** |

---

### STRATEGY (30% Weight) -- Score: 148.3/270 (54.9%)

**NOTE: Strategy is materially weaker than the mainnet Steakhouse USDC vaults because the collateral is synthetic/credit stablecoins at 91.5% LLTV (not blue-chip BTC/ETH), the dominant USDe market is priced by a hardcoded 1:1 oracle, and the vault runs on a 3-week-old centralized L2 with no stress history.**

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield is borrower interest from lending USDG against USDe/syrupUSDG/spUSDG. Mandate-aligned (USDG lending); on-chain markets show ~90% utilization = organic borrower demand. Net APY ~2.72% (the headline ~7% Robinhood Earn figure includes app-level incentives outside the vault). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (markets, utilization), [P2] [Steakhouse: Robinhood](https://kitchen.steakhouse.financial/p/robinhood-charts-a-new-course-onchain) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Mid. With 91.5% LLTV (~8.5% buffer) and a hardcoded 1:1 oracle on USDe, a plausible single-shock event -- USDe depeg, a Maple credit event impairing syrupUSDG -- can cause bad debt socialized to lenders. Loss is not limited to rare tail shocks. | 3 | 3 | Non-Improvable | [P0] Morpho V2 API (LLTV 91.5%), [P0] USDe oracle hardcoded 1:1 (RPC) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. The vault is a 1.0x lender; no leverage or rehypothecation of depositor funds. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment; [P0] Morpho V2 API |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- the vault is a lender, not a borrower. Liquidation risk applies to borrowers. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss events for comparable Steakhouse stablecoin-lending vaults (USDC/USDT) since Jan 2024. No confirmed permanent loss in USDe/syrup/spUSDG-collateralized USDG lending. Deal Breaker passes. (Forward risk from the collateral/oracle is captured in ST-PM-02, ST-C, ST-IC-02.) | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Steakhouse publishes a curation risk framework (DDQ, quantitative and secondary-liquidity modeling, deliberate exposure sizing). The framework document is the same used across Steakhouse vaults. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls), [P2] [Steakhouse: Robinhood](https://kitchen.steakhouse.financial/p/robinhood-charts-a-new-course-onchain) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Organic. Realized net APY (~2.72%) reflects on-chain borrower interest (markets at ~90% utilization). The vault charges 0 fees. The ~7% Robinhood Earn headline reflects app-level incentives, separate from the vault's organic yield. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (utilization, APY), [P2] [Robinhood Earn](https://robinhood.com/us/en/support/articles/crypto-earn/) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Mid. Markets run at ~90% utilization; only ~15% of TVL is immediately liquid, so large exits depend on borrower repayment (rate-incentivized) or forceDeallocate in-kind exit (capped penalty). USDG itself is stable, but secondary USDG/collateral liquidity on a new L2 is thin. Identical mechanics score Low on the mainnet peers with deep, stress-tested liquidity — achievable here as Robinhood Chain liquidity matures. | 3 | 9 | Time-Based | [P0] Morpho V2 API (idle $10M, liquidity $25M of $170M, utilization ~90%) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Mid. Lending interest itself does not invert, but the value of the dominant collateral (USDe) depends on Ethena's funding-rate/basis regime, and syrupUSDG depends on Maple credit spreads -- inversions in severe markets can impair collateral and produce losses. | 3 | 3 | Non-Improvable | [P2] [Steakhouse: Robinhood](https://kitchen.steakhouse.financial/p/robinhood-charts-a-new-course-onchain) |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Mid. Appointed allocators can allocate within the enabled adapter and its caps without real-time approval; caps limit per-market exposure but no automatic kill-switch exists for abnormal conditions -- halting requires manual curator/Sentinel action. | 3 | 9 | **Improvable** | [P0] Morpho V2 API (allocators, caps), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |

**Protocol Mechanics Subtotal: 31.7/45 (70.4%)**
- 9 applicable questions (ST-PM-04 = N/A): 5 scored 9 (sum = 45), 4 scored 3 (sum = 12)
- Raw sum = 57 out of max 81
- Weighted = (57/81) x 45 = 31.7

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Mid. Collateral = USDe (Ethena synthetic dollar; largest market), syrupUSDG (Maple institutional-credit receipt), spUSDG (Spark savings). These are higher-risk yield-bearing/synthetic assets, not blue-chip large-caps. They are tiered with on-chain caps, but the 91.5% LLTV is aggressive (not conservative), and USDe/Maple carry protocol/credit risk. spUSDG (Spark, Tier-0) is the safest of the three. | 3 | 3 | Non-Improvable | [P0] Morpho V2 API markets (USDe/syrup/spUSDG at 91.5% LLTV) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | Mid. USDe has shown modest (<~2%) historical deviations that recovered; syrupUSDG and spUSDG are new tokens with little peg history. Combined with a hardcoded 1:1 USDe oracle that cannot detect a depeg, deviation behavior is a real concern rather than a resolved one. The Low criterion is a 12-month clean-peg-history test — reachable once syrupUSDG/spUSDG accrue a clean track record and USDe deviations stay within bounds. | 3 | 9 | Time-Based | Market data (USDe history); [P0] USDe oracle hardcoded 1:1 (RPC) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- the collateral tokens are not staking LSTs. USDe's backing includes staked ETH within Ethena, but depositors do not bear direct slashing risk on the vault collateral. | N/A | N/A | N/A | Vault architecture |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | Mid. The collateral and loan tokens are protocol/receipt tokens (USDe, syrupUSDG, spUSDG) and a regulated stablecoin (USDG) -- categories partly excluded from the strict "bridged/wrapped" definition. However, on a 3-week-old L2 their native-vs-bridged representation could not be verified; conservative Mid pending confirmation of native issuance. | 3 | 9 | **Source Missing** | [P0] RPC (USDG is a proxy on Robinhood Chain; issuance mechanism unverified) |

**Collateral Subtotal: 15.0/45 (33.3%)**
- 3 questions scored 3 (sum = 9), 1 question N/A (ST-C-03)
- Raw sum = 9 out of max 27
- Weighted = (9/27) x 45 = 15.0

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Mid. Critical dependencies are disclosed but include non-Tier-0/1 components: Robinhood Chain (a new Arbitrum Orbit L2 not on the SR chain list) and custom fixed-price/exchange-rate Morpho oracles (not a named Tier-0/1 oracle provider). USDG (Paxos) is disclosed. Low becomes reachable if Robinhood Chain earns Tier-0/1 status on the SR list as it matures and markets migrate to Tier-0/1 price feeds (the mainnet peer scores 9 with Ethereum + Chainlink-sourced feeds). | 3 | 9 | Time-Based | [P0] Morpho V2 API, RPC (chainId 4663), [P4] [L2Beat Robinhood](https://l2beat.com/scaling/projects/robinhood) |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | High risk. The dominant USDe/USDG market uses a HARDCODED 1:1 oracle (`0xE64849bd...`, a 45-byte contract returning exactly 1e24 = fixed USDe = 1 USDG), verified on-chain -- it cannot be updated or corrected, and USDe CAN depeg materially. Per the mandatory hardcoded-oracle check, this is High (1). syrupUSDG/spUSDG use exchange-rate oracles that track protocol NAV (not market/credit markdowns). No redundancy; single immutable oracle per market. | 1 | 3 | **Improvable** | [P0] USDe oracle price()=1e24, 45-byte code (RPC); syrup/spUSDG oracles read exchange rate |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Mid. No public SOC 2 Type II / ISO 27001 for Morpho Labs or Steakhouse. The Robinhood Chain sequencer operator's IT certifications for this chain are not disclosed. Paxos is a regulated issuer. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Mid. Robinhood Chain is <6 months old (mainnet July 1, 2026) with no incidents during its short operational period -- per the new-protocol guidance, a data gap scores Mid rather than High. | 3 | 9 | Time-Based | [P4] [thirdweb: Robinhood Chain](https://blog.thirdweb.com/robinhood-chain-inside-the-ethereum-l2-bringing-tokenized-stocks-to-120-countries/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Mid. Robinhood Chain is ~3 weeks old with a single centralized sequencer; no halt >30 min has occurred yet, but there is essentially no track record to support a Low score. | 3 | 9 | Time-Based | [P4] [thirdweb: Robinhood Chain](https://blog.thirdweb.com/robinhood-chain-inside-the-ethereum-l2-bringing-tokenized-stocks-to-120-countries/), [P4] [L2Beat](https://l2beat.com/scaling/projects/robinhood) |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- no staking-based collateral in this vault. | N/A | N/A | N/A | Vault architecture |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- no staking validator set relevant to the vault collateral. Chain sequencer centralization is assessed under ST-IC-01/05/08. | N/A | N/A | N/A | Vault architecture |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | Mid. Users have permissionless on-chain redemption, but the chain relies on a single sequencer -- a sequencer/DA failure could delay withdrawals until L1 force-inclusion. The design has an escape hatch but it is unproven on a 3-week-old chain. | 3 | 9 | Time-Based | [P4] [thirdweb: Robinhood Chain](https://blog.thirdweb.com/robinhood-chain-inside-the-ethereum-l2-bringing-tokenized-stocks-to-120-countries/) |
| ST-IC-09 | How robust is the cross-chain messaging or bridge verification setup? | N/A -- the vault operates on a single chain and performs no cross-chain messaging itself. | N/A | N/A | N/A | Vault architecture |
| ST-IC-10 | Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting? | N/A -- no cross-chain escrow/minting performed by the vault. | N/A | N/A | N/A | Vault architecture |
| ST-IC-11 | Is the off-chain verification infrastructure resilient to data-source manipulation? | N/A -- the vault relies on no off-chain verifiers; oracle data is consumed on-chain. | N/A | N/A | N/A | Vault architecture |

**Infrastructure Counterparty Subtotal: 13.3/45 (29.6%)**
- 6 scored (ST-IC-06/07/09/10/11 = N/A): 5 scored 3 (sum = 15), 1 scored 1
- Raw sum = 16 out of max 54
- Weighted = (16/54) x 45 = 13.3

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Mid. Collateral value depends on external protocols: Spark (Tier-0, spUSDG), Ethena (untiered but major, >$5B, USDe -- dominant exposure), and Maple (untiered, syrupUSDG; predecessor product had a 2022 credit default). Mix of Tier-0 and untiered/higher-risk venues; the largest exposure is a synthetic dollar. | 3 | 3 | Non-Improvable | [P0] Morpho V2 API markets, [P2] [Steakhouse: Robinhood](https://kitchen.steakhouse.financial/p/robinhood-charts-a-new-course-onchain) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Low risk. Vault performance and management fees are 0% (verified). Steakhouse is the publicly disclosed curator and the Robinhood partnership is publicly announced. No hidden vault-level rebates. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (fees=0), [P1] [Morpho: Robinhood](https://morpho.org/blog/robinhood-chooses-morpho-to-power-new-earn-product) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Mid. On-chain caps exist (absolute caps ~$200-500M; increases require 7-day timelock), but relative caps are set to 100%, so the vault can allocate up to 100% to a single market -- no hard concentration limit. | 3 | 9 | **Improvable** | [P0] Morpho V2 API caps (relativeCap = 1e18 = 100%) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Mid. Unwind depends on borrower repayment at ~90% utilization; forceDeallocate provides an in-kind backstop (capped penalty). New-chain secondary liquidity is thin; no discretionary approvals needed. The mainnet peer scores Low on identical unwind mechanics with mature liquidity and stress-tested exit paths — achievable here as liquidity deepens and exits are demonstrated. | 3 | 9 | Time-Based | [P0] Morpho V2 API (utilization, forceDeallocatableLiquidity ~$5.1M), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Low risk. On-chain lending with no third-party custody of vault assets. Curator (Steakhouse), collateral protocols (Ethena/Maple/Spark), and USDG issuer/custodian (Paxos/DBS/Standard Chartered) are all disclosed. Deal Breaker passes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho: Robinhood](https://morpho.org/blog/robinhood-chooses-morpho-to-power-new-earn-product), [P1] [USDG/Paxos](https://docs.paxos.com/guides/stablecoin/usdg) |

**Protocol Counterparty Subtotal: 27.0/45 (60.0%)**
- 2 questions scored 9 (sum = 18), 3 questions scored 3 (sum = 9)
- Raw sum = 27 out of max 45
- Weighted = (27/45) x 45 = 27.0

---

#### Liquidity (5% weight, 45 max points)

**Withdrawal baseline: design-implied instant/permissionless (ERC-4626), subject to underlying market liquidity. Immediate liquidity ~$25M (~15% of TVL); markets at ~90% utilization.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain ERC-4626 redemption; gates are currently open (no address censorship); no admin pause on the immutable vault; forceDeallocate provides an in-kind backstop. Gate changes require 7-day timelock and can be revoked by the Sentinel. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (gates null), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Mid. Immediate liquidity ~$25M (~15% of $170M TVL); near-total exit depends on borrower repayment at ~90% utilization. Untested at scale. | 3 | 3 | Non-Improvable | [P0] Morpho V2 API (liquidity $25M, idle $10M of $170M) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | Mid. The vault is ~3 weeks old; no delays observed yet, but there is insufficient (<6-12 month) time-series to support a Low score. | 3 | 9 | Time-Based | [P0] Morpho V2 API (creationTimestamp ~late May 2026, mainnet July 1 2026) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Low. Morpho V2 caps are allocation-side (supply caps, absolute caps ~$200-500M above current TVL) and structurally cannot gate withdrawals; cap increases require a 7-day timelock (transparent governance) and there is no history of caps restricting exits. Utilization-driven exit limits are assessed in ST-L-02/ST-PM-08, not here. Platform-consistent with the mainnet Steakhouse peers (both score 9 on the identical cap architecture). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (caps, timelocks 604800s on cap increases) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Mid. No stress history on this new chain; behavior under volatility/congestion is unknown -- scored Mid per the untested principle. Low becomes reachable once the vault demonstrates functional exits with only modest delays through actual volatility/congestion episodes (same time-based logic as ST-L-03/O-FR-04). | 3 | 9 | Time-Based | [P0] Morpho V2 API (vault age) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No structural lockups, vesting, or bridge exits on the vault position; exit depends on borrower repayment, not time-locks. forceDeallocate provides an in-kind backstop. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Primary redemption is via ERC-4626 (always available); no secondary-market dependency for exit. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | Mid. USDG and the collateral tokens (USDe/syrup/spUSDG) have thin on-chain secondary depth on a 3-week-old L2; immediate vault liquidity is ~$25M of $170M. Depth supports staggered rather than near-total exits. | 3 | 3 | Non-Improvable | [P0] Morpho V2 API, [P4] [SteakhouseFi on Robinhood Chain](https://cryptobriefing.com/steakhousefi-vaults-robinhood-chain-users/) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Mid. A run would cause queues and rate spikes; thin ~15% buffer and the hardcoded-oracle USDe risk mean some discounting is possible, but the rate model and market isolation constrain permanent loss. Untested. | 3 | 3 | Non-Improvable | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Liquidity Subtotal: 28.3/45 (62.9%)**
- 4 questions scored 9 (sum = 36), 5 questions scored 3 (sum = 15)
- Raw sum = 51 out of max 81
- Weighted = (51/81) x 45 = 28.3

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | Mid. The vault share (USDG-denominated ERC-4626) is ~3 weeks old and has not been tested under redemption stress on this new chain. | 3 | 9 | Time-Based | [P0] Morpho V2 API (sharePrice, vault age) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Low. The vault lends USDG against stablecoin collateral -- dollar-denominated throughout, no directional BTC/ETH beta for lenders. The risk is collateral depeg/credit (captured in ST-C/ST-IC-02), not market direction. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Low. Immutable Adaptive Curve IRM per market; rates rise with utilization; no governance manipulation. Current ~90% utilization is below the >=95% prolonged-stress threshold. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Mid. Morpho liquidation is formally verified and Steakhouse does scenario/secondary-liquidity modeling, but the key tail -- a USDe depeg priced by a hardcoded 1:1 oracle -- is not liquidation-protected, leaving an effectively unbounded loss path unmitigated. | 3 | 9 | **Improvable** | [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/), [P0] USDe oracle (RPC) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Low (borrower-side). The vault has no leverage and is not itself liquidated; lenders benefit from liquidations. The collateral-depeg/bad-debt path is captured in ST-IC-02/ST-PM-02. | 9 | 9 | Non-Improvable (optimal) | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 33.0/45 (73.3%)**
- 3 questions scored 9 (sum = 27), 2 questions scored 3 (sum = 6)
- Raw sum = 33 out of max 45
- Weighted = (33/45) x 45 = 33.0

---

### **Strategy Total: 148.3/270 (54.9%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 31.7 | 45 | 70.4% |
| Collateral | 15.0 | 45 | 33.3% |
| Infra Counterparty | 13.3 | 45 | 29.6% |
| Protocol Counterparty | 27.0 | 45 | 60.0% |
| Liquidity | 28.3 | 45 | 62.9% |
| Market | 33.0 | 45 | 73.3% |
| **Strategy Total** | **148.3** | **270** | **54.9%** |

---

### OPERATIONS (30% Weight) -- Score: 201.0/270 (74.4%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Mid. Core contracts (VaultV2, Morpho Blue) are immutable, so fund-custody logic cannot be upgraded. But the top admin (Owner) is a single EOA controlling vault parameters (via 7-day timelocks + Sentinel veto) -- not on-chain tokenholder governance and not even a multisig. | 3 | 9 | **Improvable** | [P0] RPC (owner EOA), Morpho V2 API |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- no governance token or on-chain voting for this vault; the Owner is an EOA (concentration captured under S-KM-01/03). | N/A | N/A | N/A | [P0] RPC (owner EOA) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Low. Critical functions (adapters, gates, caps, abdicate) carry 7-day timelocks (>=24h); the 1-of-7 Sentinel can veto any pending action. Fee/allocator functions have 0-second base timelocks (yield, not principal). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (18 timelocks verified) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Low. The Owner can appoint a new curator/allocators; withdrawals remain permissionless via ERC-4626 + forceDeallocate throughout. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |

**Governance Subtotal: 52.5/67.5 (77.8%)**
- 2 questions scored 9 (sum = 18), 1 question scored 3, 1 question N/A (O-G-02)
- Raw sum = 21 out of max 27
- Weighted = (21/27) x 67.5 = 52.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Low. Steakhouse (adcv, Sebastien Derivaux -- ex-MakerDAO), Morpho (Paul Frambot et al.), Robinhood (public company), and Paxos (regulated issuer) are all publicly identified and credible. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse](https://www.steakhouse.financial/), [P1] [Morpho](https://morpho.org/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Low. Multiple substantial organizations (Morpho, Steakhouse, Robinhood, Paxos) support the product; no single-developer dependency. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Low. Morpho (ADDMO/Morpho Labs, France), Steakhouse (Panama/Cayman), Robinhood (US public company), Paxos Digital Singapore (USDG issuer, MAS-regulated). Entities and jurisdictions clearly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P1] [USDG/Paxos](https://docs.paxos.com/guides/stablecoin/usdg) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | Mid. Curator/infra (Steakhouse/Morpho) are clean, but two entities integral to this product have past resolved enforcement: Robinhood Crypto (NYDFS $30M, 2022; SEC crypto investigation opened 2024 and closed 2025) and Paxos (NYDFS BUSD wind-down, 2023). No ongoing material action impairing this product. Deal Breaker passes. | 3 | 3 | Non-Improvable | [P4] Public regulatory records (Robinhood Crypto NYDFS 2022; Paxos BUSD 2023) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Mid. Platform monitoring exists, but no public 24/7 on-call SLA or incident runbook covering this vault's allocator flows on a new chain, including steps to halt automated allocation. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Low. Morpho/Steakhouse have demonstrated rapid incident response; Steakhouse publishes regular updates; Robinhood provides retail support channels. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Low. Morpho's investors are public; Robinhood is the disclosed distribution/chain partner; the Morpho-Steakhouse-Robinhood arrangement is publicly announced. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho: Robinhood](https://morpho.org/blog/robinhood-chooses-morpho-to-power-new-earn-product) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Mid. Steakhouse curates many vaults, including a separate "Steakhouse Turbo USDG" vault on the same chain (a higher-risk variant), creating allocation/competition conflicts. DDQ provides qualitative controls but no published hard conflict rules. | 3 | 9 | **Improvable** | [P1] [Steakhouse Products](https://www.steakhouse.financial/docs) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | Low. Steakhouse has no uncompensated depositor-loss events across its curated vaults since inception (Jan 2024). | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs) |

**Team & Legal Subtotal: 52.5/67.5 (77.8%)**
- 6 questions scored 9 (sum = 54), 3 questions scored 3 (sum = 9)
- Raw sum = 63 out of max 81
- Weighted = (63/81) x 67.5 = 52.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Low. Morpho V2 docs, Steakhouse docs, and Robinhood Earn disclosures comprehensively cover architecture, mechanics, and risks (including explicit loss-risk disclosure). | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P2] [Steakhouse: Robinhood](https://kitchen.steakhouse.financial/p/robinhood-charts-a-new-course-onchain) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Low. Morpho docs cover liquidation/bad-debt mechanics; Steakhouse and Robinhood disclosures state collateral, protocol, and liquidity loss scenarios. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P2] [Robinhood Earn](https://robinhood.com/us/en/support/articles/crypto-earn/) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Low. Morpho maintains a canonical addresses registry; the vault is listed on the Morpho app (Robinhood Chain deployment). | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Addresses](https://docs.morpho.org/get-started/resources/addresses/), [P3] [Morpho App](https://app.morpho.org/robinhood-chain/vault/0xBeEff033F34C046626B8D0A041844C5d1A5409dd/steakhouse-usdg) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Low. Morpho V2 role/timelock documentation is comprehensive; per-function timelocks and roles are visible on-chain and via the Morpho API. | 9 | 9 | Non-Improvable (optimal) | [P1] [Roles & Capabilities](https://docs.morpho.org/curate/concepts/roles/), [P0] Morpho V2 API |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Low. Full on-chain proof-of-reserves (vault positions/allocations auditable in real time); USDG's fiat reserves are attested monthly by Paxos. Deal Breaker passes. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API, [P1] [USDG/Paxos](https://docs.paxos.com/guides/stablecoin/usdg) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Low. The deployed contracts are the standard Morpho V2/Blue bytecode; Morpho verifies its deployments and the vault responds to standard calls. (Robinhood Chain uses Blockscout-based explorers.) | 9 | 9 | Non-Improvable (optimal) | [P0] Vault/oracle contracts respond via RPC; [P3] [hoodexplorer](https://www.hoodexplorer.org/) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions, all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Mid. No dedicated safety module for this vault; bad debt is socialized among Morpho Blue market lenders. The Morpho DAO treasury exists but activation for loss coverage is discretionary. No Robinhood/Steakhouse-specific backstop disclosed. | 3 | 9 | **Improvable** | [P3] [DeFiLlama Treasury](https://api.llama.fi/treasury/morpho), [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | High risk. The Morpho DAO treasury is ~$27.2M (per DeFiLlama, predominantly MORPHO own-token, negligible stablecoins). Both ratios per the framework's TVL-denominator rule: vs Morpho's multi-billion protocol-wide TVL it is <1%; vs this vault's TVL (~$170M) it is ~16% nominal -- but the holdings are dominated by the volatile MORPHO native token, which independently meets the High criterion regardless of denominator, and the treasury is not ring-fenced for this vault. No dedicated liquid reserve or disclosed Robinhood/Steakhouse backstop. | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho) (Base+Ethereum OwnTokens ~$27.2M) |
| O-FR-03 | What is the estimated operational runway at current burn? | Low. Morpho is well-funded; Steakhouse earns curation revenue from other vaults; Robinhood (a large public company) backs the product. Runway comfortably >24 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | Mid. The vault is ~3 weeks old and has not operated through a stress event -- resilience is unproven per the demonstrated-history principle. The vault token is not widely composed externally, limiting contagion surface. | 3 | 9 | Time-Based | [P0] Morpho V2 API (vault age, TVL) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Mid. VaultV2/Morpho Blue are immutable and withdrawals are permissionless, but continued chain operation depends on Robinhood running the single sequencer; if abandoned, exit relies on an unproven L1 force-inclusion/escape hatch on a 3-week-old chain. | 3 | 9 | Time-Based | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P4] [L2Beat Robinhood](https://l2beat.com/scaling/projects/robinhood) |

**Financial Resilience Subtotal: 28.5/67.5 (42.2%)**
- 1 question scored 9, 3 questions scored 3 (sum = 9), 1 question scored 1
- Raw sum = 9 + 9 + 1 = 19 out of max 45
- Weighted = (19/45) x 67.5 = 28.5

---

### **Operations Total: 201.0/270 (74.4%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 52.5 | 67.5 | 77.8% |
| Team & Legal | 52.5 | 67.5 | 77.8% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 28.5 | 67.5 | 42.2% |
| **Operations Total** | **201.0** | **270** | **74.4%** |

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 87 | 99 | 158.2 | 180 | 87.9% |
| | Key Management (8 Q) | 32 | 72 | 80.0 | 180 | 44.4% |
| | **Security Subtotal** | | | **238.2** | **360** | **66.2%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 57 | 81 | 31.7 | 45 | 70.4% |
| | Collateral (3 of 4 Q scored) | 9 | 27 | 15.0 | 45 | 33.3% |
| | Infra Counterparty (6 of 11 Q scored) | 16 | 54 | 13.3 | 45 | 29.6% |
| | Protocol Counterparty (5 Q) | 27 | 45 | 27.0 | 45 | 60.0% |
| | Liquidity (9 Q) | 51 | 81 | 28.3 | 45 | 62.9% |
| | Market (5 Q) | 33 | 45 | 33.0 | 45 | 73.3% |
| | **Strategy Subtotal** | | | **148.3** | **270** | **54.9%** |
| **Operations** | Governance (3 of 4 Q scored) | 21 | 27 | 52.5 | 67.5 | 77.8% |
| | Team & Legal (9 Q) | 63 | 81 | 52.5 | 67.5 | 77.8% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 19 | 45 | 28.5 | 67.5 | 42.2% |
| | **Operations Subtotal** | | | **201.0** | **270** | **74.4%** |
| **TOTAL** | | | | **587.5** | **900** | **65.3%** |

---

## Validation Checklist

- [x] Smart Contract Security: (9x9 + 2x3) = 81+6 = 87/99. 87/99 x 180 = 158.18 = 158.2 (verified)
- [x] Key Management: (2x9 + 4x3 + 2x1) = 18+12+2 = 32/72. 32/72 x 180 = 80.0 (verified)
- [x] Security subtotal: 158.2 + 80.0 = 238.2 (verified)
- [x] Protocol Mechanics: (5x9 + 4x3) = 45+12 = 57/81 (1 N/A: ST-PM-04). 57/81 x 45 = 31.67 = 31.7 (verified)
- [x] Collateral: (3x3) = 9/27 (1 N/A: ST-C-03). 9/27 x 45 = 15.0 (verified)
- [x] Infra Counterparty: (5x3 + 1x1) = 15+1 = 16/54 (5 N/A: ST-IC-06/07/09/10/11). 16/54 x 45 = 13.33 = 13.3 (verified)
- [x] Protocol Counterparty: (2x9 + 3x3) = 18+9 = 27/45. 27/45 x 45 = 27.0 (verified)
- [x] Liquidity: (4x9 + 5x3) = 36+15 = 51/81. 51/81 x 45 = 28.33 = 28.3 (verified)
- [x] Market: (3x9 + 2x3) = 27+6 = 33/45. 33/45 x 45 = 33.0 (verified)
- [x] Strategy Total: 31.7 + 15.0 + 13.3 + 27.0 + 28.3 + 33.0 = 148.3 (verified)
- [x] Governance: (2x9 + 1x3) = 18+3 = 21/27 (1 N/A: O-G-02). 21/27 x 67.5 = 52.5 (verified)
- [x] Team & Legal: (6x9 + 3x3) = 54+9 = 63/81. 63/81 x 67.5 = 52.5 (verified)
- [x] Documentation: (6x9) = 54/54. 54/54 x 67.5 = 67.5 (verified)
- [x] Financial Resilience: (1x9 + 3x3 + 1x1) = 9+9+1 = 19/45. 19/45 x 67.5 = 28.5 (verified)
- [x] Operations Total: 52.5 + 52.5 + 67.5 + 28.5 = 201.0 (verified)
- [x] Grand Total: 238.2 + 148.3 + 201.0 = 587.5 (verified)
- [x] All percentages <= 100%: Yes (verified)
- [x] No score exceeds its maximum: Yes (verified)
- [x] Rating Overview table matches Final Score Calculation: Yes (verified)
- [x] Grade check: CCC+ range is 580-660; 587.5 falls within CCC+ (verified)
- [x] Potential: 349.1 + 232.3 + 265.0 = 846.4; A- range 846-858 (verified)

---

## Rating Determination

| Grade | Range | This Vault |
|-------|-------|------------|
| B- | 660-685 | - |
| **CCC+** | **580-660** | **587.5 points** |
| CCC | 500-580 | - |

## **FINAL RATING: CCC+**

*Very high risk; major loss likely without favorable conditions. The vault inherits Morpho's excellent, immutable, formally-verified smart-contract stack and is operated by credible parties (Morpho, Steakhouse, Robinhood, Paxos) with strong documentation and a regulated underlying stablecoin (USDG). But three verified findings drive the grade well below the mainnet Steakhouse peers: (1) the vault Owner is a single EOA (not a multisig/DAO); (2) the dominant USDe collateral is priced by a hardcoded 1:1 oracle that cannot detect a depeg; and (3) the vault runs on a 3-week-old, single-sequencer L2 (Robinhood Chain) against synthetic/credit collateral (USDe/syrupUSDG/spUSDG) at an aggressive 91.5% LLTV with no stress history. No deal breakers trigger — immutability, 7-day timelocks, the 1-of-7 Sentinel veto, and permissionless redemption keep the single-key owner from unilaterally moving funds — but the accumulation of key-management, oracle, collateral, and chain-immaturity risks places this vault in the very-high-risk band.*

---

## Key Risks

1. **Single-EOA vault Owner**: The top admin role of a ~$170M vault is held by a single externally-owned account (`0x337feFE4...`, verified on-chain: no contract code, nonce 1), not a multisig or DAO. If this key is compromised, an attacker can instantly change fees/allocators and queue 7-day-timelocked adapter/gate/cap changes (the 1-of-7 Sentinel can revoke, and the vault is immutable, so principal is protected — but this is a severe governance/key-management weakness). -- [P0] Robinhood Chain RPC (eth_getCode = 0 bytes)

2. **Hardcoded 1:1 oracle on the dominant USDe collateral**: The USDe/USDG market oracle (`0xE64849bd...`) is a 45-byte contract returning exactly 1e24 (fixed USDe = 1 USDG) and cannot be corrected. USDe is a synthetic dollar that can depeg; a depeg would not trigger liquidation and would socialize bad debt to lenders. USDe is the largest collateral market on the chain (~$155M supply). -- [P0] RPC price() = 1e24

3. **Aggressive LLTV on synthetic/credit collateral**: The vault lends USDG at 91.5% LLTV (~8.5% buffer) against USDe (Ethena synthetic dollar), syrupUSDG (Maple institutional credit; Maple's predecessor defaulted in 2022), and spUSDG (Spark). This is materially riskier than the BTC/ETH collateral of the mainnet Steakhouse vaults. -- [P0] Morpho V2 API markets

4. **Brand-new centralized L2**: Robinhood Chain is an Arbitrum Orbit L2 whose mainnet launched July 1, 2026 (~3 weeks before this rating), runs a single centralized sequencer, and has no operating or stress track record. A sequencer/DA failure could delay withdrawals until an unproven L1 escape hatch. -- [P4] [L2Beat Robinhood](https://l2beat.com/scaling/projects/robinhood)

5. **Permissive concentration limits**: On-chain relative caps are set to 100%, so the vault can allocate up to 100% to a single market (currently USDe-heavy). There is no hard on-chain concentration limit; concentration relies on curator discretion. -- [P0] Morpho V2 API caps (relativeCap = 1e18)

6. **No dedicated backstop; thin treasury**: Bad debt is socialized among Morpho Blue market lenders. The Morpho DAO treasury (~$27.2M, predominantly volatile MORPHO tokens) is <1% of protocol TVL and not ring-fenced for this vault; no Robinhood/Steakhouse-specific reserve is disclosed. -- [P3] [DeFiLlama Treasury](https://api.llama.fi/treasury/morpho)

---

## Improvement Roadmap

### Quick Wins (High Impact, Low Effort)

1. **Migrate the Owner to a robust multisig** [S-KM-01/02/03/04/07, O-G-01] -- multiple 1/3 → 9 (largest single lever, ~+110 KM points plus governance)
   - Deploy a >=3-of-5 (or 4-of-7) Safe as Owner with disclosed, independent signers

2. **Connect monitoring to automated protective actions** [S-SC-10] -- 3 → 9
   - Configure alerts covering the allocator flows and collateral-depeg conditions with documented response SLAs

3. **Publish incident playbook, on-call SLA, and conflict-of-interest policy** [S-KM-08, O-TL-05, O-TL-08] -- 3 → 9
   - Document EOA/multisig key-rotation, allocator-halt procedures, and quantitative allocation rules across Steakhouse's USDG vaults

### Medium-Term Improvements (High Impact, Moderate Effort)

4. **Replace the hardcoded USDe oracle with a correctable price feed** [ST-IC-02, ST-M-04] -- 1 → 3 (capped by immutable single-oracle design)
   - Use a Tier-0/1 USDe/USD feed so a depeg triggers liquidation

5. **Set hard relative caps and add circuit breakers** [ST-PC-03, ST-PM-10] -- 3 → 9
   - Enforce per-market concentration limits below 100% and automatic halt conditions

6. **Establish a dedicated backstop and disclose treasury detail** [O-FR-01, O-FR-02] -- 3/1 → 9
   - Ring-fence a liquid reserve (>=5% of vault TVL) with binding activation rules

### Long-Term / Time-Based (Track Record & Chain Maturity)

7. **Build operating and stress track record; mature chain, liquidity and collateral history; decentralize the sequencer** [ST-IC-01, ST-IC-04/05/08, ST-PM-08, ST-C-02, ST-PC-04, ST-L-03, ST-L-05, ST-M-01, O-FR-04/05] -- 3 → 9 over time
   - These mature only with clean operation, demonstrated stress resilience, deepening on-chain liquidity, clean collateral peg history, Robinhood Chain earning an SR tier listing, and sequencer decentralization

### Evidence Gaps (Source Missing Items)

8. **Obtain SOC 2 / ISO 27001 and verify native issuance of collateral** [ST-IC-03, ST-C-04] -- 3 → 9
   - Publish infrastructure certifications and confirm whether USDG/USDe/syrupUSDG/spUSDG are natively issued (vs bridged) on Robinhood Chain

**Maximum Achievable Grade:** A- (846.4/900 points) if all improvable, source-missing, and time-based items are addressed. The ceiling remains below the mainnet Steakhouse peers' potentials (A / A+) because the collateral choice, the immutable single-oracle design, structural near-total-exit liquidity, and past regulatory history are permanent constraints.

**Points to Next Grade Tier (B-):** 72.5 points needed to reach B- (660 points).

---

## Smart Contract Addresses

| Role | Address | Explorer Link |
|------|---------|---------------|
| VaultContract | 0xBeEff033F34C046626B8D0A041844C5d1A5409dd | [hoodexplorer](https://www.hoodexplorer.org/address/0xBeEff033F34C046626B8D0A041844C5d1A5409dd) |
| Owner (single EOA) | 0x337feFE49514fb901eB455A501b8Be76CDeF7660 | [hoodexplorer](https://www.hoodexplorer.org/address/0x337feFE49514fb901eB455A501b8Be76CDeF7660) |
| Sentinel (1-of-7 Safe) | 0x5642BCd50fC751fF2d04f155423e4D0E25C2a744 | [hoodexplorer](https://www.hoodexplorer.org/address/0x5642BCd50fC751fF2d04f155423e4D0E25C2a744) |
| LiquidityAdapter (MarketV1) | 0x44ABc1d6cCFF2696d98890B92E2157AF242179c2 | [hoodexplorer](https://www.hoodexplorer.org/address/0x44ABc1d6cCFF2696d98890B92E2157AF242179c2) |
| USDG Token (loan asset) | 0x5fc5360D0400a0Fd4f2af552ADD042D716F1d168 | [hoodexplorer](https://www.hoodexplorer.org/address/0x5fc5360D0400a0Fd4f2af552ADD042D716F1d168) |
| Oracle: USDe/USDG (hardcoded 1:1) | 0xE64849bd4AD03DfaBbe02bb521de19997a19055f | [hoodexplorer](https://www.hoodexplorer.org/address/0xE64849bd4AD03DfaBbe02bb521de19997a19055f) |
| Oracle: syrupUSDG/USDG (exchange-rate) | 0x152c638fad68913739Ee19Ba8eF47fAEB09DCa91 | [hoodexplorer](https://www.hoodexplorer.org/address/0x152c638fad68913739Ee19Ba8eF47fAEB09DCa91) |
| Oracle: spUSDG/USDG (exchange-rate) | 0xe694c531F65c4BaBc88A52d7178476e095e51574 | [hoodexplorer](https://www.hoodexplorer.org/address/0xe694c531F65c4BaBc88A52d7178476e095e51574) |

## Additional Info

| Field | Value |
|-------|-------|
| Infrastructure Provider | Morpho |
| Protocol Base | _none_ |
| Stated Withdrawal Time | Instant |
| Treasury | 27200000 |
| Treasury Addresses | 0xcBa28b38103307Ec8dA98377ffF9816C164f9AFa (Ethereum, Base -- Morpho DAO governance multisig), 0xF057afeEc22E220f47AD4220871364e9E828b2e9 (Ethereum -- Morpho rewards multisig), 0x5Eb982bb1E620cC3927E5CF8A5D207e667643297 (Base -- Morpho rewards multisig) |

### Code Audits

| Auditor | Report Link |
|---------|-------------|
| ChainSecurity | [Morpho Vault V2 Audit](https://www.chainsecurity.com/security-audit/morpho-vault-v2) |
| Spearbit | [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/) |
| Blackthorn | [Sherlock Case Study](https://sherlock.xyz/case-studies/morpho) |
| Certora | [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| Zellic | [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/) |
| Cantina | [Competition](https://cantina.xyz/competitions/523e1540-f8c3-45ae-9c5d-b6d35d3a326c) |

*Note: These audits cover the Morpho Vault V2 / Morpho Blue codebase. They do not cover the Robinhood Chain deployment configuration (hardcoded oracle, single-EOA owner), which is assessed under ST-IC-02 and Key Management.*

### Oracles Used

| Oracle | Documentation Link |
|--------|-------------------|
| USDe/USDG market oracle -- hardcoded 1:1 fixed price (0xE64849bd...) | [Etherscan/RPC verified; Morpho Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| syrupUSDG/USDG market oracle -- exchange-rate (0x152c638f...) | [Morpho Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| spUSDG/USDG market oracle -- exchange-rate (0xe694c531...) | [Morpho Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |

## Sources

1. [P0] Morpho V2 GraphQL API -- https://api.morpho.org/graphql (vaultV2ByAddress on chainId 4663: name, owner, sentinels, curators, timelocks, fees, TVL, APY, gates, caps, adapters; markets on Robinhood Chain; queried 2026-07-22)
2. [P0] Robinhood Chain RPC -- https://rpc.mainnet.chain.robinhood.com (chainId 0x1237=4663 confirmed; owner EOA eth_getCode=0/nonce=1; Sentinel getThreshold=1/getOwners=7; USDe oracle price()=1e24 with 45-byte code)
3. [P1] Morpho Vault V2 Documentation -- https://docs.morpho.org/learn/concepts/vault-v2/
4. [P1] Morpho Roles & Capabilities -- https://docs.morpho.org/curate/concepts/roles/
5. [P1] Morpho Security Reviews / Audits -- https://docs.morpho.org/get-started/resources/audits/
6. [P1] ChainSecurity Morpho Vault V2 Audit -- https://www.chainsecurity.com/security-audit/morpho-vault-v2
7. [P1] Morpho Formal Verification (Certora) -- https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/
8. [P1] Cantina Bug Bounty / Competition -- https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3
9. [P1] Immunefi Bug Bounty (Morpho) -- https://immunefi.com/bug-bounty/morpho/
10. [P1] Morpho Security Framework -- https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/
11. [P1] Morpho Incident Report (April 2025) -- https://morpho.org/blog/morpho-app-incident-april-10-2025/
12. [P1] Morpho: Robinhood Chooses Morpho to Power New Earn Product -- https://morpho.org/blog/robinhood-chooses-morpho-to-power-new-earn-product
13. [P1] Morpho Legal Notice -- https://morpho.org/legal-notice/
14. [P1] Morpho Contract Addresses -- https://docs.morpho.org/get-started/resources/addresses/
15. [P1] USDG Overview -- Paxos Documentation -- https://docs.paxos.com/guides/stablecoin/usdg
16. [P1] Paxos Introduces Global Dollar (USDG) -- https://www.paxos.com/newsroom/paxos-introduces-global-dollar-usdg
17. [P2] Steakhouse: Robinhood Charts a New Course Onchain -- https://kitchen.steakhouse.financial/p/robinhood-charts-a-new-course-onchain
18. [P2] Steakhouse DeFi Markets Update (2026-04-22) -- https://kitchen.steakhouse.financial/p/defi-markets-update-2026-04-22
19. [P1] Steakhouse Vault Controls -- https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls
20. [P2] Robinhood Earn Support -- https://robinhood.com/us/en/support/articles/crypto-earn/
21. [P3] Morpho App -- Steakhouse USDG (Robinhood Chain) -- https://app.morpho.org/robinhood-chain/vault/0xBeEff033F34C046626B8D0A041844C5d1A5409dd/steakhouse-usdg
22. [P3] DeFiLlama Morpho Treasury API -- https://api.llama.fi/treasury/morpho (~$27.2M, predominantly MORPHO)
23. [P4] L2Beat -- Robinhood Chain -- https://l2beat.com/scaling/projects/robinhood
24. [P4] thirdweb: Robinhood Chain (L2 technical overview, single sequencer) -- https://blog.thirdweb.com/robinhood-chain-inside-the-ethereum-l2-bringing-tokenized-stocks-to-120-countries/
25. [P4] Crypto Briefing: SteakhouseFi vaults on Robinhood Chain adoption -- https://cryptobriefing.com/steakhousefi-vaults-robinhood-chain-users/
26. [P3] Robinhood Chain Explorer (hoodexplorer / Blockscout) -- https://www.hoodexplorer.org/
27. [P4] MyEtherWallet: What is USDG by Global Dollar -- https://www.myetherwallet.com/blog/stablecoins-what-is-usdg-by-global-dollar/

---

**Rating Analyst:** DeFi Risk Auditor Agent
**Methodology:** Staking Rewards DeFi Protocol Rating Framework v0.1-gamma
**Date:** 2026-07-22
