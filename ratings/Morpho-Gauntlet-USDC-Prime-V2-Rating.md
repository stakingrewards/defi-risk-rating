# Morpho - Gauntlet USDC Prime V2 Vault (Base) Risk Rating

**Rating Date**: 2026-06-22
**Analyst**: DeFi Risk Auditor Agent
**Final Grade**: BB
**Total Score**: 774.3/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Executive Summary

The Gauntlet USDC Prime vault (0x050cE30b927Da55177A4914EC73480238BAD56f0) is a Morpho Vault V2 deployed on **Base** (chainId 8453) that lends USDC against blue-chip crypto collateral through Morpho Blue markets. Curated by Gauntlet -- one of the most established DeFi risk-management firms (founded 2018, $1B valuation, Tarun Chitra CEO/ex-D.E. Shaw, Gauntlet Networks Inc., New York) -- this vault implements the conservative "Prime" mandate: large-market-cap, high-liquidity collateral only. As of the rating date the vault holds ~$88.1M TVL (totalAssetsUsd $88,113,659) at ~4.38% net APY with 0% performance and 0% management fees (all confirmed via the Morpho V2 GraphQL API). It was deployed on 2025-10-22 (~8 months of operating history). This is a DISTINCT product from the older Gauntlet USDC Prime MetaMorpho V1 vault on Ethereum (0xdd0f28e...); it uses Morpho's newer immutable Vault V2 infrastructure on a Tier-2 chain.

The vault's verified on-chain allocation is genuinely blue-chip and conservative: cbBTC/USDC ~$71.7M (81.4%), WETH/USDC ~$13.7M (15.6%), cbETH/USDC ~$2.5M (2.8%), and wstETH/USDC ~$0.24M (0.3%), all at 86%/77% LLTV (≈14-23% liquidation buffer) and all priced by Chainlink (ChainlinkOracleV2) market oracles. Allocation flows through a MorphoMarketV1 adapter (0x2fEcd40f...) holding the full ~$88.1M; a second MetaMorpho adapter (0xe80b16bA...) is enabled but currently holds $0. Idle assets are $0 and immediately-available liquidity is ~$71.7M (~81% of TVL). The V2 architecture is immutable post-deployment and provides permissionless ERC4626 redemption plus a `forceDeallocate` in-kind exit backstop (configurable penalty up to ~2%).

The V2 codebase benefits from Morpho's industry-leading smart-contract security: dedicated Vault V2 audits by ChainSecurity (Tier-0), Spearbit (Tier-0), Zellic (Tier-0), Blackthorn, and a $200K Cantina competition, plus Certora formal verification, on top of 25+ ecosystem audits and the immutable Morpho Blue core (~600 LOC). Dual bug bounties run on Cantina ($2.5M) and Immunefi ($2.5M Morpho Blue), with V2 in scope. Governance is verified on-chain: Owner is a 4-of-7 Safe (0x5a4E1984...), Curator is a 3-of-7 Safe (0x9E33faAE..., Gauntlet), and there are two Sentinels -- a 3-of-7 Safe (0x7084bF4d...) and an EOA (0x0dF6DaCb...). Most governance functions carry a 7-day (604,800s) timelock; fee and cap changes carry 3 days; force-deallocate-penalty 1 day; only decreaseTimelock and fee-recipient setters are 0s.

The BB rating (774.3/900) sits ~18.7 points below the Gauntlet USDC Prime V1 (BB+/793.0) on Ethereum, with the gap driven by three Base-specific / V2-specific factors: (1) **Base is a Tier-2 chain** that experienced a 33-minute sequencer outage on Aug 5, 2025 (ST-IC-05 → Mid 3 vs Ethereum's 9); (2) **untested V2 infrastructure on Base** -- this vault has no demonstrated stress-survival history of its own, so resilience questions (ST-L-05, ST-L-09, ST-M-01, O-FR-04) are capped at Mid per the "Favor Demonstrated History" principle (V1 Prime on Ethereum scored Low on several after surviving Nov 2025); and (3) **Gauntlet manager loss history** from the March 2026 Resolv USR exploit (~$7.5M+ initially-uncompensated bad debt in Gauntlet Core/Frontier vaults) penalizes ST-PM-05, O-TL-05, and O-TL-09. The vault itself was structurally unaffected by Resolv (no USR exposure -- blue-chip-only mandate). It shares the standard Morpho constraints: ~84% wrapped-asset concentration (cbBTC+cbETH), single immutable oracle per market with no fallback, no dedicated loss reserve, no automatic on-chain circuit breakers, and a treasury (~$24.8M, ~100% MORPHO) under 1% of protocol TVL.

---

## Rating Overview

| Category | Weight | Current Score | Potential Score | Current % | Potential % |
|----------|--------|---------------|-----------------|-----------|-------------|
| Security | 40% | 323.2 | 349.1 | 89.8% | 97.0% |
| Strategy | 30% | 226.1 | 252.5 | 83.7% | 93.5% |
| Operations | 30% | 225.0 | 270.0 | 83.3% | 100.0% |
| **Total** | **100%** | **774.3** | **871.6** | **86.0%** | **96.8%** |

**Current Grade**: BB (774.3/900 points)
**Potential Grade**: A+ (871.6/900 points) - achievable if all improvements made

---

## Deal Breaker Assessment

| Question Code | Deal Breaker Type | Status | Impact |
|---------------|-------------------|--------|--------|
| [S-SC-01] Audits | Category | PASS | No cap -- 25+ ecosystem audits; V2 audited by ChainSecurity, Spearbit, Zellic, Blackthorn + Cantina competition; Certora formal verification |
| [S-SC-06] Exploits | Full | PASS | No cap -- No confirmed exploit causing user fund loss in this vault or in Morpho/Vault V2 contracts |
| [S-SC-07] Rug Pull | Full | PASS | No cap -- No rug-pull events (Morpho = ADDMO nonprofit; Gauntlet Networks Inc.) |
| [S-KM-02] Single Key Control | Category | PASS | No cap -- 4-of-7 Safe owner + 7-day timelock + Sentinel; immutable vault; permissionless redemption |
| [ST-PM-05] Strategy Losses | Category | PASS (Mid) | No cap triggered -- scored Mid (3): comparable variant (Gauntlet Frontier/Core) had Resolv losses, but root cause (USR) structurally excluded from Prime's blue-chip mandate. Deal breaker triggers only on High (1). |
| [ST-PC-05] Third Party Disclosure | Category | PASS | No cap -- Pure on-chain lending; no third-party custodians/validators in vault operations |
| [O-TL-04] Regulatory Actions | Category | PASS | No cap -- No enforcement actions against Gauntlet Networks Inc. or Morpho entities |
| [O-DT-05] Proof of Reserves | Category | PASS | No cap -- Full real-time on-chain transparency |

**Deal Breaker Summary**: No deal breakers triggered. ST-PM-05 scores Mid (3) rather than High (1) because, although Gauntlet-curated Frontier/Core vaults experienced uncompensated bad debt during the March 2026 Resolv USR exploit, that loss arose from USR collateral that is structurally excluded from the Prime mandate (this vault holds only cbBTC/WETH/cbETH/wstETH). The vault passes all critical safety checks.

---

## Improvement Summary

| Status | Count | Notes |
|--------|-------|-------|
| Improvable | 11 | S-SC-10, S-KM-08, ST-PM-05, ST-PM-10, ST-C-04, ST-M-01, O-TL-05, O-TL-08, O-TL-09, O-FR-01, O-FR-04 |
| Source Missing | 2 | ST-IC-03, O-FR-02 |
| Non-Improvable (below optimal) | 6 | S-SC-11, ST-IC-02, ST-IC-05, ST-L-02, ST-L-05, ST-L-09 |
| Non-Improvable (optimal) / Already Optimal | 63 | scored 9 |
| N/A | 5 | ST-PM-04, ST-IC-09, ST-IC-10, ST-IC-11, O-G-02 |

**Top Improvement Opportunities:**
1. **Publish Comprehensive Incident Playbook** [S-KM-08]: Current 3 → 9 (+15.0 weighted points) -- Improvable
2. **Connect Monitoring to Automated Protections** [S-SC-10]: Current 3 → 9 (+10.9 weighted points) -- Improvable
3. **Disclose / Build Treasury Reserve** [O-FR-02]: Current 1 → 9 (+12.0 weighted points) -- Source Missing / Improvable
4. **Establish Dedicated Safety Module** [O-FR-01]: Current 3 → 9 (+9.0 weighted points) -- Improvable
5. **Reduce Wrapped-Asset Concentration** [ST-C-04]: Current 1 → 9 -- Improvable
6. **Add Circuit Breakers to Automated Allocation** [ST-PM-10]: Current 3 → 9 -- Improvable

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 323.2/360 (89.8%)

#### Smart Contract Security (20% weight, 180 max points)

**NOTE: All Smart Contract Security scores are platform-level and IDENTICAL to the other Morpho Vault V2 ratings under v0.1-gamma (Steakhouse Prime Instant V2 USDC, Gauntlet USDC Frontier V2) and the Gauntlet USDC Prime V1. The V2 codebase is immutable post-deployment and was independently audited by ChainSecurity/Spearbit/Zellic/Blackthorn + Cantina competition with Certora formal verification. S-SC-10 and S-SC-11 score 3 per the v0.1-gamma verification principle (monitoring cannot automatically trigger protective actions).**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | Yes. Vault V2 infrastructure independently audited by ChainSecurity (Tier-0), Spearbit (Tier-0), Zellic (Tier-0), Blackthorn, and a $200K Cantina competition, with Certora formal verification, on top of 25+ ecosystem audits and the immutable Morpho Blue core (~600 LOC). This vault (0x050cE30b...) deployed via the audited V2 Factory (0x4501125508...). Adapters (MarketV1 0x2fEcd40f..., MetaMorpho 0xe80b16bA...) are V2-audited adapter types. All fund-custody/routing contracts covered by ≥2 independent audits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/), [P1] [ChainSecurity V2 Audit](https://www.chainsecurity.com/security-audit/morpho-vault-v2), [P1] [Cantina V2 Competition](https://cantina.xyz/competitions/523e1540-f8c3-45ae-9c5d-b6d35d3a326c) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent V2 work (Sep-Nov 2025): Spearbit (Tier-0), ChainSecurity (Tier-0), with Certora (Tier-0) formal verification. Multiple Tier-0 auditors. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/), [P1] [ChainSecurity V2 Audit](https://www.chainsecurity.com/security-audit/morpho-vault-v2) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable (~600 LOC). Vault V2 (shipped 2025) was preceded by 5+ Tier-0 audit engagements. The deployed VaultV2 contract is immutable post-deployment (no upgrade risk). MarketV1AdapterV2 was separately audited. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/), [P1] [GitHub vault-v2](https://github.com/morpho-org/vault-v2) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 ecosystem vulnerability patched with OpenZeppelin. ChainSecurity V2 asset-solvency findings fixed before deployment; Certora formal verification of invariants; Cantina competition findings addressed in development. All V2 findings resolved before mainnet. | 9 | 9 | Non-Improvable (optimal) | [P1] [ChainSecurity V2 Audit](https://www.chainsecurity.com/security-audit/morpho-vault-v2), [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue is immutable. The VaultV2 contract (0x050cE30b...) is immutable post-deployment -- non-custodial guarantees cannot be changed. Market/adapter changes require Curator + timelock (7 days for addAdapter/removeAdapter/registry; 3 days for caps), with Sentinel revoke. Verified via V2 API. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P0] Morpho V2 GraphQL API (timelocks) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss in this vault or in Morpho/Vault V2 smart contracts. April 2025 frontend issue ($2.6M) was intercepted by a white hat and fully returned. The March 2026 Resolv USR exploit caused bad debt in OTHER Gauntlet vaults (USR collateral) but NOT this Prime vault (blue-chip-only). Morpho liquidations fired per spec in every incident. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P4] [DeFi Prime - Resolv](https://defiprime.com/resolv-usr-exploit) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No. Morpho operates as ADDMO (French nonprofit). Gauntlet Networks Inc. ($1B valuation, public leadership). No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No. V2 timelock framework requires timelock changes to themselves be timelocked (decreaseTimelock is the only 0s function but any decrease still subject to its own process). Most governance functions at 7 days; no reductions documented since deployment. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (timelocks verified 2026-06-22), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Dual standing bounties: Cantina ($2.5M max) and Immunefi ($2.5M Morpho Blue). V2 contracts in scope. Both Tier-0 platforms with payout history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3), [P1] [Immunefi Bounty](https://immunefi.com/bug-bounty/morpho/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Gauntlet partners with Hypernative (real-time monitoring), ZeroShadow (24/7 vSOC), Chainalysis, SEAL Intel; Morpho runs internal monitoring bots. However, per v0.1-gamma verification principle, monitoring cannot automatically trigger protective actions -- no on-chain circuit breakers, no automated pause. The March 2026 Resolv exploit showed the Public Allocator continued auto-supplying capital to broken markets for ~10 hours, proving alerts are not connected to automated protections. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P4] [DeFi Prime - Resolv](https://defiprime.com/resolv-usr-exploit) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design (Morpho prioritizes immutability). V2 introduces the Sentinel role which can reactively deallocate, decrease caps, and revoke pending proposals -- an improvement over V1's Guardian -- but Sentinel actions are manual/reactive, not auto-triggered by invariant breaches, and do not cover automated allocation flows. | 3 | 3 | Non-Improvable | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Smart Contract Security Subtotal:**
- Raw scores: 9×9 (sum 81) + 2×3 (sum 6) = 87/99
- Adjusted: (87/99) × 180 = **158.2/180 (87.9%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

**NOTE: This vault's roles are Safe multisigs verified on-chain via the Safe Transaction Service (Base) -- Owner 4-of-7, Curator 3-of-7, Sentinel 3-of-7 Safe + one EOA Sentinel. This matches the Gauntlet USDC Prime V1 and Gauntlet Frontier V2 governance posture (NOT the unverified Aragon-DAO owner of the Steakhouse Prime Instant V2 vault). KM scores therefore mirror the Gauntlet vaults.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Owner is a 4-of-7 GnosisSafe (0x5a4E1984..., Safe v1.3.0+L2, nonce 153, 7 distinct signers, verified via Safe API on Base). Curator is a 3-of-7 GnosisSafe (0x9E33faAE..., v1.4.1+L2, nonce 182 -- the Gauntlet multisig, same 7 signers as Owner). Owner is also listed among curators. Changes visible on-chain via Safe Tx Service. V2 per-function timelocks: most 7 days, fees/caps 3 days, penalty 1 day. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://api.safe.global/tx-service/base/api/v1/safes/0x5a4E19842e09000a582c20A4f524C26Fb48Dd4D0/), [P0] [Safe API Curator](https://api.safe.global/tx-service/base/api/v1/safes/0x9E33faAE38ff641094fa68c65c2cE600b3410585/), [P0] Morpho V2 GraphQL API |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. VaultV2 is immutable post-deployment; Morpho Blue logic immutable. Moving funds requires going through immutable contract logic; allocators move only to/from enabled adapters within curator-set caps. Owner is 4-of-7 (threshold ≥3, signers ≥5) with 7-day timelock on critical functions. Permissionless ERC4626 redemption plus forceDeallocate always available. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://api.safe.global/tx-service/base/api/v1/safes/0x5a4E19842e09000a582c20A4f524C26Fb48Dd4D0/), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner multisig is 4-of-7 (meets ≥4-of-7 Low-risk threshold). 7 distinct EOA signers verified via Safe API. Gauntlet is a publicly identified company (Tarun Chitra CEO, 50+ employees), so signers are attributable to a known operator. Curator (3-of-7) and a 3-of-7 Sentinel Safe add further layers. The 7 Owner signers and 7 Curator signers are the same set; one Sentinel is an EOA (single-key) but Sentinel powers are bounded (revoke/deallocate/decrease-cap only, cannot move funds). No multisig changes reducing independence observed. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://api.safe.global/tx-service/base/api/v1/safes/0x5a4E19842e09000a582c20A4f524C26Fb48Dd4D0/), [P0] [Safe API Sentinel](https://api.safe.global/tx-service/base/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking on Morpho Blue (immutable). V2 Gates exist for compliance access control but are timelocked (7 days) and can be permanently disabled via abdication; gates are not currently set to restrict withdrawals. No admin pause. Withdrawals always permissionless. Rules public. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Gates](https://docs.morpho.org/curate/concepts/gates/), [P0] Morpho V2 GraphQL API (gate timelocks = 604800s) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% in non-custodial Morpho Blue contracts on Base. Permissionless ERC4626 redemption + forceDeallocate. No off-chain custody. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P0] Morpho V2 GraphQL API |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation; vault funds in Morpho Blue markets via adapters, separate from treasury/ops. Both fees 0% (V2 API). Morpho is a nonprofit with no profit extraction. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (performanceFee=0, managementFee=0), [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain adapter whitelist: MorphoMarketV1 adapter (0x2fEcd40f...) and a MetaMorpho adapter (0xe80b16bA...). Both access Morpho Blue markets only. Adapter additions require Curator + 7-day timelock; multi-dimensional absolute & relative caps enforce per-market/ID limits on-chain. Aligned to the Prime blue-chip mandate (cbBTC, WETH, cbETH, wstETH markets). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (adapters), [P1] [V2 Adapter Docs](https://docs.morpho.org/curate/tutorials-v2/listing-adapters/) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Gauntlet has ZeroShadow (24/7 SOC), Hypernative, SEAL Intel partnerships; Morpho docs include emergency procedures; V2 Sentinel enables faster de-risking. But no public, vault-specific incident playbook with explicit key-rotation steps or tabletop results published. The Resolv incident response (failure to halt automated allocation for hours) suggests playbook gaps. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Morpho Emergency Procedures](https://docs.morpho.org/curate/emergency/) |

**Key Management Subtotal:**
- Raw scores: 7×9 (sum 63) + 1×3 (sum 3) = 66/72
- Adjusted: (66/72) × 180 = **165.0/180 (91.7%)**

**Security Total: 158.2 + 165.0 = 323.2/360 (89.8%)**

---

### STRATEGY (30% Weight) -- Score: 226.1/270 (83.7%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from overcollateralized USDC lending against blue-chip collateral (cbBTC 81.4%, WETH 15.6%, cbETH 2.8%, wstETH 0.3%) via Morpho Blue. 100% mandate-aligned (Prime = large-cap, high-liquidity collateral). Net APY ~4.38%. May include modest Morpho V2 incentives on Base; core yield is organic lending interest. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (allocations, netApy), [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail shocks: simultaneous BTC/ETH crash exceeding the ~14% liquidation buffer (86% LLTV), oracle manipulation on an immutable market oracle, or catastrophic wrapped-asset custodian failure (cbBTC/cbETH via Coinbase). Bad debt is isolated and socialized per market. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault lends USDC at 1.0x effective leverage. No rehypothecation of depositor funds. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment, [P0] Morpho V2 GraphQL API |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. Liquidation risk applies to borrowers; liquidations protect lenders. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | This V2 Base vault has zero bad debt since 2025-10-22. However, Gauntlet-curated Frontier/Core vaults (comparable variant: same curator, same Morpho protocol, same deposited asset USDC, differing only in collateral parameters) experienced confirmed bad debt (~$7.5M+) in the March 2026 Resolv USR exploit, initially socialized to lenders (partial later compensation via Merkl). The root cause (USR collateral) is structurally excluded from Prime's blue-chip mandate, so the loss-relevant variant is the conservative Prime tier (zero loss). Scored Mid (3): comparable variant had a limited-impact loss, but Prime mandate isolates the cause. | 3 | 9 | **Improvable** | [P4] [DeFi Prime - Resolv](https://defiprime.com/resolv-usr-exploit), [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Gauntlet VaultBook publishes curation methodology, risk-factor overview, due-diligence process, market-allocation strategy, and Prime/Balanced/Frontier tiering with quantitative insolvency targets (<10 bps of TVL). Agent-based simulations inform allocations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Curation Methodology](https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Primarily organic from USDC lending demand against blue-chip collateral. 0% vault fee enhances net yield. Some Base-side Morpho V2 incentives may apply but core yield is organic and remains positive without incentives. No formal incentive breakdown published for this vault. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (netApy, fees=0), [P1] [VaultBook Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes (with caveat). USDC is the most liquid stablecoin; immediately-available liquidity is ~$71.7M (~81% of TVL) and idle is $0. forceDeallocate provides a permissionless in-kind backstop (penalty up to ~2%). However, this specific Base vault has not been stress-tested under direct withdrawal pressure; underlying market utilization is high (~90%). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (liquidityUsd≈$71.7M), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) (forceDeallocate) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. Pure overcollateralized lending interest. No basis trade, peg arbitrage, or funding-rate dependency. Rates set by immutable Adaptive Curve IRM. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment, [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Yes. V2 adapter-based allocation lets appointed allocators move funds to enabled adapters within multi-dimensional caps, without real-time human approval. Caps limit per-market/ID exposure, but no automatic kill-switch exists for abnormal conditions (oracle deviation, depeg, utilization spike). Sentinel can reactively deallocate/decrease caps but this is manual. The March 2026 Resolv exploit demonstrated this exact failure mode on Gauntlet vaults. | 3 | 9 | **Improvable** | [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/), [P4] [DeFi Prime - Resolv](https://defiprime.com/resolv-usr-exploit) |

**Protocol Mechanics Subtotal:**
- 9 applicable (ST-PM-04 = N/A): 7×9 (sum 63) + 2×3 (sum 6) = 69/81
- Adjusted: (69/81) × 45 = **38.3/45 (85.2%)**

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Blue-chip only: cbBTC (Coinbase-custodied wrapped BTC, 81.4%), WETH (native ETH wrapper, 15.6%), cbETH (Coinbase LST, 2.8%), wstETH (Lido LST, 0.3%). All large-cap, high-liquidity, tiered with on-chain LLTVs (86%/77%) and caps. Mandate-aligned. cbBTC/cbETH carry single-custodian (Coinbase) dependency; WETH/wstETH are lower-risk. Low risk per the established large-cap criterion. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (per-market allocations), [P3] [Morpho App](https://app.morpho.org/base/vault/0x050cE30b927Da55177A4914EC73480238BAD56f0/gauntlet-usdc-prime) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | cbBTC: no depeg >2% since Sep 2024 launch. WETH: native, no depeg risk. cbETH/wstETH: tracked stETH/ETH-style ratios with no >2% sustained depeg in 12 months. No collateral here showed >2% depeg lasting >24h. Battle-tested blue-chip assets. | 9 | 9 | Non-Improvable (optimal) | [P3] Market price history, [P0] Morpho V2 GraphQL API |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Only cbETH (~2.8%) and wstETH (~0.3%) carry staking exposure (~3.1% combined). Coinbase (cbETH) and Lido (30+ operators, coverage fund) manage slashing; exposure is immaterial at this allocation. | 9 | 9 | Non-Improvable (optimal) | [P3] Lido/Coinbase operator data |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | HIGH: cbBTC (~81.4%, Coinbase-custodied wrapped BTC) + cbETH (~2.8%, Coinbase LST) ≈ 84% of collateral exposure is wrapped/custodial per the framework definition (WETH excluded as thin wrapper; wstETH is a protocol receipt token). Exceeds the 60% threshold. Concentrated custodial dependency on Coinbase. | 1 | 9 | **Improvable** | [P0] Morpho V2 GraphQL API (cbBTC $71.7M of $88.1M) |

**Collateral Subtotal:**
- 4 questions: 3×9 (sum 27) + 1×1 (sum 1) = 28/36
- Adjusted: (28/36) × 45 = **35.0/45 (77.8%)**

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Base (Tier-2 chain), Chainlink (Tier-0 oracle, ChainlinkOracleV2 per market). No bridges in the strategy; no CEX dependency. All dependencies disclosed and Tier-0/Tier-2. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (oracle types), [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | Mandatory immutable-oracle check: each Morpho Blue market uses one immutable oracle with no fallback and no post-deployment correction. Can the priced collateral depeg? cbBTC/cbETH are wrapped custodial assets that could theoretically depeg if Coinbase fails; WETH/wstETH price deep-liquidity pairs (ETH/USD). Underlying Chainlink feeds price battle-tested deep-liquidity assets where material depeg is historically unprecedented → capped at Mid (3) by the hardcoded/immutable rule. Zero redundancy by design. | 3 | 3 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/), [P0] Morpho V2 GraphQL API (ChainlinkOracleV2) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | No public SOC 2 Type II or ISO27001 for Gauntlet Networks or Morpho Labs/ADDMO disclosed. Chainlink holds enterprise certifications; Coinbase (cbBTC/cbETH custodian) is SOC 2 certified / NY DFS regulated. Gauntlet runs an off-chain risk engine and allocation models. | 3 | 9 | **Source Missing** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Base: Aug 5, 2025 sequencer outage (~33 min) caused short UX degradation, no blocked on-chain withdrawals or losses. Morpho: April 2025 frontend issue (4-min rollback, funds returned). March 2026 Resolv exploit did not affect this Prime vault. No prolonged inability to withdraw. Deployed >6 months. | 9 | 9 | Non-Improvable (optimal) | [P4] [Base Sequencer Outage (CoinDesk)](https://www.coindesk.com/tech/2025/08/06/base-says-sequencer-failure-caused-block-production-halt-of-33-minutes), [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Base experienced a single ~33-minute block-production halt on Aug 5, 2025 (sequencer failover failure), within the last 12 months. One incident above 30 minutes and under 6 hours, fully recovered with no lasting impact → Mid (3). (Ethereum-based Morpho vaults score 9 here; Base is Tier-2.) | 3 | 3 | Non-Improvable | [P4] [TheBlock - Base Sequencer Failure](https://www.theblock.co/post/365732/base-network-sequencer-failure), [P4] [CoinDesk](https://www.coindesk.com/tech/2025/08/06/base-says-sequencer-failure-caused-block-production-halt-of-33-minutes) |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Minimal exposure (cbETH ~2.8% + wstETH ~0.3%). No material slashing events affecting Coinbase/Lido relevant to this vault in 12 months; trivial events absorbed by buffers. | 9 | 9 | Non-Improvable (optimal) | [P3] Lido/Coinbase slashing data |
| ST-IC-07 | Are validators diverse geographically and by operator? | For the small LST exposure: Lido (wstETH) uses 30+ independent operators across regions; Coinbase (cbETH) is a single large operator but the exposure is immaterial (~2.8%). Base sequencing is centralized (Coinbase) but that is a chain property captured in ST-IC-05. LST validator distribution is diverse for the material share. | 9 | 9 | Non-Improvable (optimal) | [P3] Lido operator data |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Permissionless ERC4626 redemption + forceDeallocate always available; no off-chain dependency for withdrawals. A Base sequencer outage delays UX but does not block on-chain withdrawals once the chain resumes; an oracle failure halts new borrows/liquidations on a market but does not block lender withdrawals. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-IC-09 | How robust is the cross-chain messaging or bridge verification setup? | N/A -- The vault operates exclusively on Base with no cross-chain messaging or bridge dependency. | N/A | N/A | N/A | Vault architecture |
| ST-IC-10 | Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting? | N/A -- No cross-chain escrow or minting mechanism for this vault. | N/A | N/A | N/A | Vault architecture |
| ST-IC-11 | Is the off-chain verification infrastructure resilient to data-source manipulation? | N/A -- The vault does not rely on off-chain verifiers or cross-chain attestation; oracle data is consumed on-chain via Morpho oracle adapters. | N/A | N/A | N/A | Vault architecture |

**Infrastructure Counterparty Subtotal:**
- 8 applicable (ST-IC-09/10/11 = N/A): 5×9 (ST-IC-01/04/06/07/08, sum 45) + 3×3 (ST-IC-02/03/05, sum 9) = 54/72
- Adjusted: (54/72) × 45 = **33.75/45 (75.0%)**

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All allocation to Morpho Blue markets (Tier-0 protocol) via adapters. No CEX or RWA exposure. Markets: cbBTC/USDC, WETH/USDC, cbETH/USDC, wstETH/USDC on Base. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (allocations) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Both performance and management fees are 0% (V2 API). Any Base-side Morpho incentives are public via Morpho/Merkl. No hidden rebates identified. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (fees=0), [P1] [VaultBook Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. V2 multi-dimensional absolute & relative caps per market/ID enforced on-chain. Cap increases require 3-day timelock; cap decreases are instant (risk-reducing). Gauntlet runs continuous automated optimization within caps. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (caps, timelocks), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Positions unwind as borrowers repay; ~$71.7M (~81%) immediately available. forceDeallocate provides a permissionless in-kind backstop. No discretionary approvals. This specific Base vault is untested for large-scale unwind, but the underlying blue-chip markets have deep liquidity. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (liquidityUsd), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending; no external validators, custodians, or asset managers in vault operations. Gauntlet (curator) disclosed. Collateral custodians (Coinbase for cbBTC/cbETH, Lido for wstETH) publicly known. | 9 | 9 | Non-Improvable (optimal) | Vault architecture, [P0] Morpho V2 GraphQL API |

**Protocol Counterparty Subtotal:**
- 5 questions: 5×9 = 45/45
- Adjusted: (45/45) × 45 = **45.0/45 (100.0%)**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless ERC4626 redemption via the immutable V2 vault, plus forceDeallocate in-kind backstop. V2 gates (compliance) are not set to restrict and can be permanently disabled via abdication. No admin pause on Morpho Blue. Non-custodial guarantee preserved. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P1] [V2 Gates](https://docs.morpho.org/curate/concepts/gates/) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Moderate. ~$71.7M (~81% of $88.1M TVL) immediately available; idle $0. Markets run at ~90% utilization, so near-total exit during stress would require borrower repayment or face queues. forceDeallocate provides in-kind exit. Can absorb large but not necessarily near-total instant exits under stress. | 3 | 3 | Non-Improvable | [P0] Morpho V2 GraphQL API (liquidityUsd≈$71.7M, utilization≈90%) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | This Base vault (launched Oct 2025) has no reported delays or freezes in its operating history. It has not been independently stress-tested, so a clean record cannot yet evidence Low under stress, but no freeze events have occurred. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API, vault operating history |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | V2 multi-dimensional caps are designed for risk control, not exit restriction; cap decreases are instant and increases timelocked. No evidence of caps used to block exits. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API, [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | UNTESTED for this Base V2 vault. No independent stress event (Nov 2025 predates large TVL here; the vault was not stress-tested under direct withdrawal pressure). Per the "Favor Demonstrated History" principle, an untested vault on a Tier-2 chain caps at Mid (3). Underlying blue-chip markets are deep, supporting recovery, but resilience is not demonstrated. | 3 | 3 | Non-Improvable | Scoring methodology (untested = Mid max for resilience) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure USDC lending with no lockups, vesting, or bridge dependencies on the lender side. forceDeallocate available. <10% longer-dated exposure. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics, [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary ERC4626 redemption always available; no secondary market required. forceDeallocate is an additional in-kind path. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | USDC is the most liquid stablecoin. cbBTC/WETH/cbETH/wstETH are deep-liquidity blue-chip collaterals on Base/Ethereum. In-protocol redemption is the primary exit path; depth comfortably supports staggered exits and most normal-condition sizes. | 9 | 9 | Non-Improvable (optimal) | [P3] Market data, [P0] Morpho V2 GraphQL API |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Moderate / UNTESTED for this vault. ~81% immediate liquidity and 86% LLTV (~14% buffer) plus utilization-based IRM create strong repayment incentives, suggesting temporary queues rather than permanent haircuts in a run. But this Base vault has no demonstrated bank-run survival; capped at Mid (3) per scoring principles. | 3 | 3 | Non-Improvable | [P0] Morpho V2 GraphQL API, Scoring methodology (untested = Mid max) |

**Liquidity Subtotal:**
- 9 questions: 6×9 (sum 54) + 3×3 (sum 9) = 63/81
- Adjusted: (63/81) × 45 = **35.0/45 (77.8%)**

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | The vault share is an ERC4626 NAV-based claim on USDC plus yield. It has NOT yet been tested under direct redemption/withdrawal stress on Base (launched Oct 2025; no major exit event), so per the "Favor Demonstrated History" principle it currently scores Mid (3). Unlike a leveraged or peg token, the NAV-based share holds par by construction: the battle-tested Gauntlet USDC Prime V1 on Ethereum scored Low (9) here after its share stayed stable through Nov 2025 and the March 2026 Resolv crisis (Frontier V2 assigns the same potential 9). This distinct V2 Base vault can therefore reach Low (9) once it survives a comparable direct withdrawal-stress event with NAV intact. | 3 | 9 | **Improvable** | [P0] Morpho V2 GraphQL API, Scoring methodology (untested = Mid now; demonstrated NAV stability = Low 9) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Very low. Vault lends USDC -- dollar-denominated; no directional BTC/ETH exposure for lenders. Risk is borrower bad debt, not market direction. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Immutable Adaptive Curve IRM per market; rates auto-increase with utilization. No governance manipulation possible. No history of prolonged ≥95% utilization on these blue-chip markets beyond brief spikes (current ~90%). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (utilization), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. Gauntlet agent-based simulations and VaultBook risk-exposure modeling; Certora formally verified Morpho Blue liquidation mechanics; 86% LLTV gives ~14% buffer. Blue-chip collateral with deep liquidation markets. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side only. Liquidations protect lenders by restoring market solvency; the LIF goes to liquidators. 86% LLTV (~14% buffer) on deep-liquidity blue-chip collateral makes lender bad debt unlikely outside extreme gaps. | 9 | 9 | Non-Improvable (optimal) | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal:**
- 5 questions: 4×9 (sum 36) + 1×3 (sum 3) = 39/45
- Adjusted: (39/45) × 45 = **39.0/45 (86.7%)**

**Strategy Total: 38.3 + 35.0 + 33.75 + 45.0 + 35.0 + 39.0 = 226.05 ≈ 226.1/270 (83.7%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 38.3 | 45 | 85.2% |
| Collateral | 35.0 | 45 | 77.8% |
| Infra Counterparty | 33.75 | 45 | 75.0% |
| Protocol Counterparty | 45.0 | 45 | 100.0% |
| Liquidity | 35.0 | 45 | 77.8% |
| Market | 39.0 | 45 | 86.7% |
| **Strategy Total** | **226.05** | **270** | **83.7%** |

---

### OPERATIONS (30% Weight) -- Score: 225.0/270 (83.3%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid with strong checks. Morpho Blue immutable; VaultV2 immutable post-deployment. Adapter/cap changes require Curator + timelock (7 days for adapters, 3 for caps) + Sentinel revoke. Role segregation (Owner, Curator, Allocator, Sentinel). No single entity can unilaterally change fund-custody logic. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/), [P0] Morpho V2 GraphQL API |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- No governance-token voting for this vault; controlled by Safe multisigs + Sentinel. Concentration captured in S-KM-01/S-KM-03. | N/A | N/A | N/A | [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. Per-function timelocks verified via V2 API (2026-06-22): setIsAllocator/gates/registry/addAdapter/removeAdapter/increaseTimelock/abdicate = 7 days; setPerformanceFee/setManagementFee/increaseAbsoluteCap/increaseRelativeCap = 3 days; setForceDeallocatePenalty = 1 day; decreaseTimelock & fee-recipient setters = 0s. All material/upgrade functions ≥24h. Sentinel (3-of-7 Safe + EOA) can revoke pending actions and decrease caps. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (timelocks verified), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner (4-of-7) can change Curator/roles subject to timelock; withdrawals remain permissionless via ERC4626 + forceDeallocate throughout. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Governance Subtotal:**
- 3 applicable (O-G-02 = N/A): 3×9 = 27/27
- Adjusted: (27/27) × 67.5 = **67.5/67.5 (100.0%)**

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Gauntlet: Tarun Chitra (CEO/co-founder, ex-D.E. Shaw Research), Rei Chiang (co-founder), 50+ team. Morpho: Paul Frambot (CEO). All publicly identified with verifiable track records. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Team](https://www.gauntlet.xyz/our-team), [P1] [Morpho](https://morpho.org/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Gauntlet has 50+ employees; Morpho is a separate full team ($73.6M raised). Multiple independent parties can operate the vault. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet About](https://www.gauntlet.xyz/about) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Morpho: ADDMO (French nonprofit) + Morpho Labs SAS (France). Gauntlet: Gauntlet Networks Inc. (New York, USA). Both clearly identified. (SEC action vs unrelated "Gauntlet Holdings, LLC" is a different entity.) | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P1] [Gauntlet](https://www.gauntlet.xyz/) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known material enforcement actions against Gauntlet Networks Inc. or Morpho entities in major jurisdictions. | 9 | 9 | Non-Improvable (optimal) | Public records |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Gauntlet has 24/7 on-call (ZeroShadow vSOC, Hypernative, SEAL Intel); Morpho demonstrated 4-min response (April 2025). However, per v0.1-gamma automation override, incident response MUST include documented procedures to halt automated allocation. The March 2026 Resolv exploit showed the Public Allocator kept supplying capital to broken markets for hours -- response did not halt automated allocation within SLA. Same structural gap applies to V2 adapter-driven flows. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P4] [DeFi Prime - Resolv](https://defiprime.com/resolv-usr-exploit) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Gauntlet publishes detailed market reports within days; active VaultBook; rapid incident communication during Nov 2025 and March 2026 events. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Gauntlet: Polychain, Paradigm, Ribbit Capital ($1B valuation). Morpho: a16z, Variant, Pantera, Coinbase Ventures (29 investors, $73.6M). All disclosed. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet $1B Valuation](https://www.gauntlet.xyz/resources/announcing-our-1-billion-valuation-and-next-steps-for-the-gauntlet-platform) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Gauntlet manages many vaults across chains and tiers (Prime/Balanced/Frontier; $1B+ AUM). Tiered risk system, automated allocation, and VaultBook provide structural mitigations, but no formal quantitative conflict-of-interest policy with hard constraints is published. The Resolv incident raised cross-vault risk-management questions. | 3 | 9 | **Improvable** | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | The March 2026 Resolv USR exploit caused confirmed bad debt (~$7.5M+) in Gauntlet-curated Frontier/Core vaults, initially uncompensated (partial later compensation via Merkl). This Prime vault had zero loss (blue-chip-only), but the framework evaluates the manager entity -- Gauntlet is linked to depositor losses in products it curates. Constitutes "one historical loss incident with limited impact" followed by risk isolation (tiered system worked) and partial compensation. Prior Aave advisory CRV bad debt was advisory, not curation. | 3 | 9 | **Improvable** | [P4] [DeFi Prime - Resolv](https://defiprime.com/resolv-usr-exploit), [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |

**Team & Legal Subtotal:**
- 9 questions: 6×9 (sum 54) + 3×3 (sum 9) = 63/81
- Adjusted: (63/81) × 67.5 = **52.5/67.5 (77.8%)**

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive Morpho V2 docs and Gauntlet VaultBook; V2 architecture (adapters, gates, sentinel, timelocks, forceDeallocate) documented; Prime mandate described. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P1] [VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Liquidation mechanics, bad-debt socialization, oracle risks, and V2 adapter/security considerations documented across Morpho docs. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Security Considerations](https://docs.morpho.org/curate/concepts/security-considerations/) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Morpho V2 contract registry (VaultV2Factory, adapter factories, registry) documented; vault address listed on the Morpho app and addresses page. Etherscan/BaseScan verified. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Contracts](https://docs.morpho.org/get-started/resources/contracts/morpho-vaults-v2/), [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Comprehensive V2 role/capability matrix; per-function timelock durations documented; changes visible via on-chain event logs and Safe Tx Service. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/), [P0] Morpho V2 GraphQL API |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves; all adapter/market allocations visible via V2 API, Morpho app, and BaseScan. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API, [P0] [BaseScan](https://basescan.org/address/0x050cE30b927Da55177A4914EC73480238BAD56f0) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. The VaultV2 contract is deployed and listed/recognized by Morpho (V2 API `listed: true`); adapters and factory are deployed contracts on Base; Morpho V2 contracts are verified on BaseScan with public source. | 9 | 9 | Non-Improvable (optimal) | [P0] [BaseScan](https://basescan.org/address/0x050cE30b927Da55177A4914EC73480238BAD56f0), [P0] Morpho V2 GraphQL API (listed=true) |

**Documentation Subtotal:**
- 6 questions: 6×9 = 54/54
- Adjusted: (54/54) × 67.5 = **67.5/67.5 (100.0%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated safety module for this vault or Morpho generally; bad debt is socialized per Morpho Blue market. Morpho DAO treasury exists but activation for loss coverage is discretionary; no Gauntlet-specific backstop with binding rules. | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/), [P3] [DeFiLlama Treasury](https://api.llama.fi/treasury/morpho) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Insufficient. Morpho DAO treasury ≈ $24.8M per DeFiLlama, ~100% MORPHO tokens (volatile native, negligible stables), against ~$14.2B protocol-wide TVL ≈ 0.17%. Not ring-fenced for this $88.1M vault. Below the 1% threshold and dominated by a volatile native token. | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho), [P3] [DeFiLlama Morpho TVL](https://api.llama.fi/protocol/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Gauntlet ($1B valuation, well-funded) and Morpho ($73.6M raised, nonprofit structure) both have multi-year runway. Curator fees and protocol revenue growing. Runway comfortably >24 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet $1B Valuation](https://www.gauntlet.xyz/resources/announcing-our-1-billion-valuation-and-next-steps-for-the-gauntlet-platform), [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | This Base V2 vault has NOT independently survived a major stress event (deployed Oct 2025; not directly impacted by Resolv but also not stress-tested under withdrawal pressure). The broader Morpho protocol grew TVL through 2025 stress with isolated-market containment, but per the "Favor Demonstrated History" principle this untested vault cannot score Low. The vault share is not widely composed into external protocols, limiting contagion surface. | 3 | 9 | **Improvable** | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/), Scoring methodology (untested = Mid max) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue and the VaultV2 contract are immutable; permissionless ERC4626 withdrawals + forceDeallocate always available; no proprietary off-chain service required for exits. Sentinel can veto pending changes. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |

**Financial Resilience Subtotal:**
- 5 questions: 2×9 (sum 18) + 2×3 (sum 6) + 1×1 (sum 1) = 25/45
- Adjusted: (25/45) × 67.5 = **37.5/67.5 (55.6%)**

**Operations Total: 67.5 + 52.5 + 67.5 + 37.5 = 225.0/270 (83.3%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 67.5 | 67.5 | 100.0% |
| Team & Legal | 52.5 | 67.5 | 77.8% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 37.5 | 67.5 | 55.6% |
| **Operations Total** | **225.0** | **270** | **83.3%** |

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 87 | 99 | 158.2 | 180 | 87.9% |
| | Key Management (8 Q) | 66 | 72 | 165.0 | 180 | 91.7% |
| | **Security Subtotal** | | | **323.2** | **360** | **89.8%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 69 | 81 | 38.3 | 45 | 85.2% |
| | Collateral (4 Q) | 28 | 36 | 35.0 | 45 | 77.8% |
| | Infra Counterparty (8 of 11 Q scored) | 54 | 72 | 33.75 | 45 | 75.0% |
| | Protocol Counterparty (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity (9 Q) | 63 | 81 | 35.0 | 45 | 77.8% |
| | Market (5 Q) | 39 | 45 | 39.0 | 45 | 86.7% |
| | **Strategy Subtotal** | | | **226.05** | **270** | **83.7%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 63 | 81 | 52.5 | 67.5 | 77.8% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 25 | 45 | 37.5 | 67.5 | 55.6% |
| | **Operations Subtotal** | | | **225.0** | **270** | **83.3%** |
| **TOTAL** | | | | **774.25** | **900** | **86.0%** |

*Total = 323.2 + 226.05 + 225.0 = 774.25 ≈ 774.3/900.*

---

## Validation Checklist

- [x] Smart Contract Security: (9×9 + 2×3) = 81+6 = 87/99. 87/99 × 180 = 158.18 ≈ 158.2 (verified)
- [x] Key Management: (7×9 + 1×3) = 63+3 = 66/72. 66/72 × 180 = 165.0 (verified)
- [x] Security subtotal: 158.2 + 165.0 = 323.2 (verified)
- [x] Protocol Mechanics: (7×9 + 2×3) = 63+6 = 69/81 (1 N/A: ST-PM-04). 69/81 × 45 = 38.33 ≈ 38.3 (verified)
- [x] Collateral: (3×9 + 1×1) = 27+1 = 28/36. 28/36 × 45 = 35.0 (verified)
- [x] Infra Counterparty: (5×9 + 3×3) = 45+9 = 54/72 (3 N/A: ST-IC-09/10/11; threes = ST-IC-02/03/05). 54/72 × 45 = 33.75 (verified)
- [x] Protocol Counterparty: (5×9) = 45/45. 45/45 × 45 = 45.0 (verified)
- [x] Liquidity: (6×9 + 3×3) = 54+9 = 63/81. 63/81 × 45 = 35.0 (verified)
- [x] Market: (4×9 + 1×3) = 36+3 = 39/45. 39/45 × 45 = 39.0 (verified)
- [x] Strategy subtotal: 38.3 + 35.0 + 33.75 + 45.0 + 35.0 + 39.0 = 226.05 (verified)
- [x] Governance: (3×9) = 27/27 (1 N/A: O-G-02). 27/27 × 67.5 = 67.5 (verified)
- [x] Team & Legal: (6×9 + 3×3) = 54+9 = 63/81. 63/81 × 67.5 = 52.5 (verified)
- [x] Documentation: (6×9) = 54/54. 54/54 × 67.5 = 67.5 (verified)
- [x] Financial Resilience: (2×9 + 2×3 + 1×1) = 18+6+1 = 25/45. 25/45 × 67.5 = 37.5 (verified)
- [x] Operations subtotal: 67.5 + 52.5 + 67.5 + 37.5 = 225.0 (verified)
- [x] Total: 323.2 + 226.05 + 225.0 = 774.25 ≈ 774.3 (verified)
- [x] All percentages ≤ 100%: Yes (verified)
- [x] No score exceeds its maximum: Yes (verified)
- [x] Grade check: 774.25 → BB range is 760-785. 774.25 falls in BB (verified)
- [x] Potential check: 349.1 + 252.5 + 270.0 = 871.6 → A+ range is 870-876. 871.6 falls in A+ (verified; ST-M-01 potential 3→9 lifts Market potential 39.0→45.0 and Strategy potential 246.5→252.5)

---

## Rating Determination

| Grade | Range | This Vault |
|-------|-------|------------|
| BB+ | 785-810 | - |
| **BB** | **760-785** | **774.3 points** |
| BB- | 735-760 | - |

## **FINAL RATING: BB**

*Moderately elevated risk; resilience is more scenario-dependent. The vault pairs Morpho's industry-leading immutable Vault V2 smart-contract security (multiple Tier-0 audits, formal verification, dual $2.5M bug bounties), a verified Safe-multisig governance stack (4-of-7 owner, 7-day timelocks, Sentinel), a genuinely conservative blue-chip allocation (cbBTC/WETH/cbETH/wstETH at 86% LLTV via Chainlink oracles), 0% fees, and ~81% immediate liquidity, with Gauntlet's institutional risk-curation framework. It is held to BB by: (1) deployment on Base, a Tier-2 chain that had a 33-minute sequencer halt in Aug 2025 (ST-IC-05=3); (2) an untested V2 vault on Base with no demonstrated stress survival of its own (ST-L-05, ST-L-09, ST-M-01, O-FR-04 capped at Mid); (3) Gauntlet's manager loss history from the March 2026 Resolv exploit affecting comparable Frontier/Core vaults (ST-PM-05, O-TL-05, O-TL-09=3); plus the standard Morpho constraints (~84% wrapped-asset/Coinbase-custodial concentration, single immutable oracle per market, no loss reserve, no automatic circuit breakers, treasury <1% of TVL).*

---

## Key Risks

- **Base is a Tier-2 chain with a recent sequencer halt**: Base suffered a ~33-minute block-production halt on Aug 5, 2025 (sequencer failover failure), within the 12-month window; centralized Coinbase sequencing adds liveness risk not present on the Ethereum-deployed Gauntlet Prime V1 (ST-IC-05=3). -- [TheBlock](https://www.theblock.co/post/365732/base-network-sequencer-failure)
- **Untested V2 vault on Base under stress**: Deployed 2025-10-22 (~8 months), this distinct V2 vault has no demonstrated survival of a withdrawal-stress or bank-run event of its own; resilience questions (ST-L-05, ST-L-09, ST-M-01, O-FR-04) are capped at Mid (3) per the framework's demonstrated-history principle. -- [Morpho V2 GraphQL API](https://api.morpho.org/graphql)
- **Gauntlet manager loss history (Resolv)**: Gauntlet-curated Frontier/Core vaults incurred ~$7.5M+ initially-uncompensated bad debt in the March 2026 Resolv USR exploit; though this Prime vault was unaffected (blue-chip-only), the manager entity is linked to depositor losses (ST-PM-05, O-TL-09=3). -- [DeFi Prime](https://defiprime.com/resolv-usr-exploit)
- **~84% wrapped/custodial collateral concentration**: cbBTC (~81.4%) plus cbETH (~2.8%) means the bulk of collateral depends on Coinbase custody of wrapped assets; a custodian failure or cbBTC/cbETH depeg is the primary bad-debt path (ST-C-04=1). -- [Morpho V2 GraphQL API](https://api.morpho.org/graphql)
- **Single immutable oracle per market, no fallback (Non-Improvable)**: Each Morpho Blue market uses one immutable Chainlink-based oracle that cannot be corrected post-deployment; a structural Morpho design limitation (ST-IC-02=3). -- [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/)
- **No dedicated loss reserve; thin treasury**: Bad debt is socialized per market with no ring-fenced backstop; Morpho DAO treasury (~$24.8M, ~100% MORPHO) is ~0.17% of protocol TVL with no binding loss-coverage commitment (O-FR-01=3, O-FR-02=1). -- [DeFiLlama Treasury](https://api.llama.fi/treasury/morpho)
- **No automatic circuit breakers for automated allocation**: V2 allocators can increase exposure within caps with no automatic kill-switch; Sentinel response is manual, and monitoring is not connected to automated protections (S-SC-10, S-SC-11, ST-PM-10, O-TL-05). -- [V2 Roles](https://docs.morpho.org/curate/concepts/roles/)

---

## Improvement Roadmap

### Quick Wins (High Impact, Low Effort)
1. **Connect Monitoring to Automated Protections** [S-SC-10] - Current: 3, Potential: 9 (+10.9 weighted points)
2. **Publish Conflict-of-Interest Policy** [O-TL-08] - Current: 3, Potential: 9 (+5.0 weighted points)
3. **Document Procedures to Halt Automated Allocation** [O-TL-05] - Current: 3, Potential: 9 (+5.0 weighted points)

### Medium-Term Improvements (High Impact, Moderate Effort)
1. **Publish Comprehensive Incident Playbook** [S-KM-08] - Current: 3, Potential: 9 (+15.0 weighted points)
2. **Add Circuit Breakers to Automated Allocation** [ST-PM-10] - Current: 3, Potential: 9 (strategy points)
3. **Establish Dedicated Safety Module** [O-FR-01] - Current: 3, Potential: 9 (+9.0 weighted points)
4. **Reduce Wrapped/Custodial Asset Concentration** [ST-C-04] - Current: 1, Potential: 9 (strategy points)

### Long-Term Structural Changes (Variable Impact, High Effort)
1. **Build/Disclose Liquid Reserve ≥5% of TVL** [O-FR-02] - Current: 1, Potential: 9 (+12.0 weighted points)
2. **Demonstrate Stress Survival on Base** [ST-M-01, O-FR-04] - Current: 3 each, Potential: 9 each (ST-M-01: the NAV share demonstrably holds par once tested, as battle-tested V1 Prime showed; O-FR-04: TVL/revenue/buffers behave resiliently through a survived stress event)

### Non-Improvable (Structural Caps)
- **Single Immutable Oracle per Market** [ST-IC-02]: Current 3 - Morpho Blue immutable design; oracle values cannot be corrected post-deployment (blue-chip collateral caps at Mid, not High)
- **No Automatic Circuit Breakers** [S-SC-11]: Current 3 - Morpho immutability philosophy
- **Base Tier-2 Chain / Sequencer Halt** [ST-IC-05]: Current 3 - historical Aug 2025 outage, chain-level (decays to 9 only via passage of time after ~Aug 2026, not protocol action)
- **High-Utilization Lending Liquidity** [ST-L-02, ST-L-05, ST-L-09]: Current 3 - a USDC lending vault run at ~90% utilization is structurally capped at Mid for near-total / stress exits; even the battle-tested V1 Prime (Ethereum) stayed at Mid (3) on ST-L-05/ST-L-09 after surviving Nov 2025, so stress survival does NOT lift these to Low (9)
- **Gauntlet Resolv Loss History** [ST-PM-05, O-TL-09]: Current 3 - historical, improvable only with 24-36 months clean record

### Evidence Gaps (Source Missing Items)
1. **Obtain/Disclose SOC 2 Certification** [ST-IC-03] - Current: 3, Potential: 9 (+3.75 weighted points)
2. **Disclose Ring-Fenced Reserve** [O-FR-02] - Current: 1, Potential: 9

**Maximum Achievable Grade:** A+ (871.6/900 points) if all improvable and source-missing items addressed
**Points to Next Grade Tier (BB+):** 10.7 points needed to reach BB+ (785 points)

---

## Smart Contract Addresses

| Role | Address | Explorer Link |
|------|---------|---------------|
| VaultContract | 0x050cE30b927Da55177A4914EC73480238BAD56f0 | [BaseScan](https://basescan.org/address/0x050cE30b927Da55177A4914EC73480238BAD56f0) |
| OwnerMultisig | 0x5a4E19842e09000a582c20A4f524C26Fb48Dd4D0 | [BaseScan](https://basescan.org/address/0x5a4E19842e09000a582c20A4f524C26Fb48Dd4D0) |
| CuratorMultisig | 0x9E33faAE38ff641094fa68c65c2cE600b3410585 | [BaseScan](https://basescan.org/address/0x9E33faAE38ff641094fa68c65c2cE600b3410585) |
| Sentinel (Safe 3-of-7) | 0x7084bF4dB6c21e1834dD6482f6056a39A33584cD | [BaseScan](https://basescan.org/address/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD) |
| Sentinel (EOA) | 0x0dF6DaCbE6a2ea16EaC22fdbeE4E645c779aCdee | [BaseScan](https://basescan.org/address/0x0dF6DaCbE6a2ea16EaC22fdbeE4E645c779aCdee) |
| MarketV1Adapter | 0x2fEcd40f436CA170D2478a58Da898FcE93988eef | [BaseScan](https://basescan.org/address/0x2fEcd40f436CA170D2478a58Da898FcE93988eef) |
| MetaMorphoAdapter | 0xe80b16bA20d57E72BD8A5C5E01F7AAcadaC674E8 | [BaseScan](https://basescan.org/address/0xe80b16bA20d57E72BD8A5C5E01F7AAcadaC674E8) |
| VaultV2Factory | 0x4501125508079A99ebBebCE205DeC9593C2b5857 | [BaseScan](https://basescan.org/address/0x4501125508079A99ebBebCE205DeC9593C2b5857) |

## Additional Info

| Field | Value |
|-------|-------|
| Infrastructure Provider | Morpho |
| Protocol Base | _none_ |
| Stated Withdrawal Time | Instant |
| Treasury | 24800000 |
| Treasury Addresses | 0xcBa28b38103307Ec8dA98377ffF9816C164f9AFa (Ethereum, Base -- governance multisig 5/9), 0x5Eb982bb1E620cC3927E5CF8A5D207e667643297 (Base -- rewards multisig 3/5), 0xF057afeEc22E220f47AD4220871364e9E828b2e9 (Ethereum -- rewards multisig 3/5) |

### Code Audits

| Auditor | Report Link |
|---------|-------------|
| ChainSecurity | [Morpho Vault V2 Audit](https://www.chainsecurity.com/security-audit/morpho-vault-v2) |
| Spearbit | [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/) |
| Zellic | [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/) |
| Blackthorn | [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/) |
| Cantina (competition) | [V2 Competition](https://cantina.xyz/competitions/523e1540-f8c3-45ae-9c5d-b6d35d3a326c) |
| Certora (formal verification) | [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |

### Oracles Used

| Oracle | Documentation Link |
|--------|-------------------|
| Chainlink (ChainlinkOracleV2 per Morpho Blue market: cbBTC/USDC, WETH/USDC, cbETH/USDC, wstETH/USDC) | [Morpho Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |

## Sources

1. [P0] Morpho V2 GraphQL API -- https://api.morpho.org/graphql (vault data, owner/curators/sentinels, per-function timelocks, fees=0, TVL ≈ $88.1M, avgNetApy ≈ 4.38%, adapters, per-market allocations, liquidity ≈ $71.7M, listed=true, creationTimestamp 2025-10-22; queried 2026-06-22)
2. [P0] Safe Transaction Service (Base) - Owner 4-of-7 -- https://api.safe.global/tx-service/base/api/v1/safes/0x5a4E19842e09000a582c20A4f524C26Fb48Dd4D0/
3. [P0] Safe Transaction Service (Base) - Curator 3-of-7 -- https://api.safe.global/tx-service/base/api/v1/safes/0x9E33faAE38ff641094fa68c65c2cE600b3410585/
4. [P0] Safe Transaction Service (Base) - Sentinel 3-of-7 -- https://api.safe.global/tx-service/base/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/
5. [P0] Base public RPC eth_getCode (Sentinel 0x0dF6DaCb... confirmed EOA; vault/owner/adapters confirmed contracts) -- https://mainnet.base.org
6. [P0] BaseScan - Gauntlet USDC Prime V2 Vault -- https://basescan.org/address/0x050cE30b927Da55177A4914EC73480238BAD56f0
7. [P1] Morpho Vault V2 Documentation -- https://docs.morpho.org/learn/concepts/vault-v2/
8. [P1] Morpho Roles & Capabilities -- https://docs.morpho.org/curate/concepts/roles/
9. [P1] Morpho Timelock Docs -- https://docs.morpho.org/curate/concepts/timelock/
10. [P1] Morpho Gates Docs -- https://docs.morpho.org/curate/concepts/gates/
11. [P1] Morpho Audits Page -- https://docs.morpho.org/get-started/resources/audits/
12. [P1] ChainSecurity Morpho Vault V2 Audit -- https://www.chainsecurity.com/security-audit/morpho-vault-v2
13. [P1] Cantina Morpho Vault V2 Competition -- https://cantina.xyz/competitions/523e1540-f8c3-45ae-9c5d-b6d35d3a326c
14. [P1] Morpho Formal Verification (Certora) -- https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/
15. [P1] Cantina Bug Bounty -- https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3
16. [P1] Immunefi Bug Bounty -- https://immunefi.com/bug-bounty/morpho/
17. [P1] Morpho Security Framework -- https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/
18. [P1] Morpho April 2025 Incident Report -- https://morpho.org/blog/morpho-app-incident-april-10-2025/
19. [P1] Morpho Legal Notice -- https://morpho.org/legal-notice/
20. [P1] Morpho Risk Docs -- https://docs.morpho.org/learn/resources/risks
21. [P1] Morpho Liquidation Concepts -- https://docs.morpho.org/learn/concepts/liquidation/
22. [P1] Morpho Oracle Concepts -- https://docs.morpho.org/learn/concepts/oracle/
23. [P1] Morpho V2 Contracts Page -- https://docs.morpho.org/get-started/resources/contracts/morpho-vaults-v2/
24. [P1] Morpho Governance / Multisigs -- https://docs.morpho.org/learn/governance/organization/
25. [P1] Gauntlet VaultBook (Curation Methodology) -- https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview
26. [P1] Gauntlet Security -- https://www.gauntlet.xyz/vaults/security
27. [P1] Gauntlet $1B Valuation -- https://www.gauntlet.xyz/resources/announcing-our-1-billion-valuation-and-next-steps-for-the-gauntlet-platform
28. [P1] Gauntlet November 2025 Market Report -- https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025
29. [P3] DeFiLlama Treasury API (Morpho ≈ $24.8M, ~100% MORPHO) -- https://api.llama.fi/treasury/morpho
30. [P3] DeFiLlama Morpho Protocol TVL (≈ $14.2B) -- https://api.llama.fi/protocol/morpho
31. [P3] Morpho App - Gauntlet USDC Prime (Base) -- https://app.morpho.org/base/vault/0x050cE30b927Da55177A4914EC73480238BAD56f0/gauntlet-usdc-prime
32. [P4] TheBlock - Base Sequencer Failure (Aug 2025, ~33 min) -- https://www.theblock.co/post/365732/base-network-sequencer-failure
33. [P4] CoinDesk - Base 33-Minute Block Production Halt -- https://www.coindesk.com/tech/2025/08/06/base-says-sequencer-failure-caused-block-production-halt-of-33-minutes
34. [P4] DeFi Prime - Resolv USR Exploit -- https://defiprime.com/resolv-usr-exploit
