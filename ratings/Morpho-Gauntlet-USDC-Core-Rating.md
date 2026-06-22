# Morpho - Gauntlet USDC Core Vault Risk Rating

**Rating Date**: 2026-06-22
**Analyst**: DeFi Risk Auditor Agent
**Final Grade**: B-
**Total Score**: 677.3/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Executive Summary

The Gauntlet USDC Core vault (0x8eB67A509616cd6A7c1B3c8C21D48FF57df3d458) is a MetaMorpho **V1** vault on Ethereum (deployed via the original MetaMorpho factory, Solidity v0.8.21, Etherscan-verified) that lends USDC against a **broad, higher-risk collateral set** through Morpho Blue markets. Curated by Gauntlet — one of the most established DeFi risk firms (founded 2018, $1B valuation, $41.8M raised) — the "Core" mandate explicitly "targets a higher risk level than Gauntlet's Prime Vaults." With approximately $8.42M in TVL and a net APY of ~3.89% (5% performance fee), the vault currently allocates to BTC-wrapped markets (cbBTC, WBTC, tBTC, Lombard LBTC), an ether.fi restaked-ETH market (weETH), and — most significantly — multiple **synthetic / RWA-credit stablecoin markets** at 91.5%/77% LLTV (Cap stcUSD ~24.7%, FalconX/Pareto AA tranche ~25.0%, plus whitelisted InfiniFi siUSD and Maple syrupUSDC).

The decisive differentiator from the other Gauntlet USDC vaults is that **this vault was directly impacted by the March 22, 2026 Resolv USR exploit.** The Core vault held roughly $4.95M in a wstUSR/USDC market priced by a hardcoded $1 oracle; when USR collapsed to ~$0.025 after an attacker minted ~80M unbacked USR (via a compromised AWS signing key) and the Morpho Public Allocator / `supplyOnBehalf` donation-attack continued routing USDC into the broken market, the vault crystallized socialized bad debt. Gauntlet accounts for ~96% of the ~$6.2M of Morpho-wide bad debt from the incident. Unlike the Gauntlet USDC Prime vault (which was completely unaffected due to its blue-chip-only mandate), Core took a real, vault-specific loss. A compensation plan is now live: as of June 4, 2026, a total of 4,379,827 USDC is claimable via Merkl, with **Gauntlet USDC Core (v1, mainnet) explicitly open for claims.** The vault has since had the Resolv markets removed and has recovered to normal operation.

On-chain governance verification (June 2026) confirmed identical Gauntlet multisig infrastructure to the other Gauntlet vaults: Owner is a 4-of-7 Safe (0xC684..., v1.3.0, nonce 508), Guardian is a 3-of-7 Safe (0x7084..., v1.4.1), and Curator is a 3-of-7 Safe (0x9E33..., v1.4.1, nonce 452). The vault timelock is 259,200 seconds (3 days) — shorter than Prime's 7 days. The vault benefits from Morpho's industry-leading smart-contract security (25+ Tier-0/1 audits, immutable Morpho Blue core, Certora formal verification, dual $2.5M Cantina/Immunefi bounties) and Ethereum's Tier-0 chain stability (no sequencer-halt penalty). The B- rating reflects: (1) a direct, demonstrated bad-debt loss from the Resolv exploit equal to ~4.6%–5.3% of the vault's verified ~$76M–$83M pre-exploit TVL (compensation flowing but not verified as 100% complete; historical and non-improvable); (2) high-LLTV synthetic/RWA-credit stablecoin collateral that is materially riskier than Prime's blue-chip mandate; (3) immutable per-market oracles with no fallback (the exact attack vector that failed in this vault); (4) automated allocation (Public Allocator) without on-chain circuit breakers, demonstrably bypassed here; and (5) no dedicated loss reserve. It is offset by full on-chain transparency, permissionless USDC redemption, a strong curator/team, and an active compensation program.

---

## Rating Overview

| Category | Weight | Current Score | Max Score | Current % | Potential Score | Potential % |
|----------|--------|---------------|-----------|-----------|-----------------|-------------|
| Security | 40% | 305.0 | 360 | 84.7% | 330.9 | 91.9% |
| Strategy | 30% | 147.3 | 270 | 54.6% | 244.0 | 90.4% |
| Operations | 30% | 225.0 | 270 | 83.3% | 270.0 | 100.0% |
| **Total** | **100%** | **677.3** | **900** | **75.3%** | **844.9** | **93.9%** |

**Current Grade**: B- (677.3/900 points)
**Potential Grade**: BBB+ (844.9/900 points) - achievable if all improvements made

---

## Deal Breaker Assessment

| Question Code | Deal Breaker Type | Status | Impact |
|---------------|-------------------|--------|--------|
| [S-SC-01] Audits | Category | PASS | No cap -- 25+ audits from Tier-0/1 firms |
| [S-SC-06] Exploits | Full | **NOT CAPPED (High)** | Resolv USR exploit caused confirmed bad debt in this vault's wstUSR market; scored High (1) -- realized Core loss (~$3.8M–$4.05M) is ~4.6%–5.3% of verified pre-exploit TVL (~$76M–$83M), i.e. ≥2%; full compensation of Core depositors is not verifiable (4.38M USDC via Merkl spans five vaults, below the ~$5.7M–$5.95M Gauntlet-wide bad debt, no per-vault split published); and no detailed post-mortem within 30 days. Full Deal Breaker (cap to D) still requires High (1) + permanent uncompensated loss >10% TVL + non-functional protocol; the vault is functional with permissionless withdrawals and compensation is flowing, so the D-cap does NOT trigger. |
| [S-SC-07] Rug Pull | Full | PASS | No cap -- No rug pull events |
| [S-KM-02] Single Key Control | Category | PASS | No cap -- Multisig (4-of-7 Owner) + 3-day timelock required |
| [ST-PM-05] Strategy Losses | Category | **NOT CAPPED (High)** | Scored High (1) -- this vault experienced confirmed permanent loss (socialized bad debt) from Resolv. Category Deal Breaker caps only the Strategy category grade; it does not cap the overall grade. Strategy already scores in its true range. |
| [ST-PC-05] Third Party Disclosure | Category | PASS | No cap -- Pure on-chain lending, no third-party custodians |
| [O-TL-04] Regulatory Actions | Category | PASS | No cap -- No enforcement actions against Gauntlet Networks Inc. |
| [O-DT-05] Proof of Reserves | Category | PASS | No cap -- Full on-chain transparency |

**Deal Breaker Summary**: No full deal breaker caps the grade. S-SC-06 scores High (1) — the wstUSR bad debt is a confirmed vault-specific loss of ~4.6%–5.3% of verified pre-exploit TVL (≥2%), full compensation of Core depositors cannot be verified, and no detailed post-mortem was published within 30 days. However, the Full Deal Breaker D-cap requires High (1) PLUS permanent uncompensated loss >10% of TVL PLUS a non-functional protocol; the vault remains fully functional with permissionless ERC4626 withdrawals and compensation is flowing, so the D-cap does NOT trigger and the grade is set by the calculated score (677.3 = B-). ST-PM-05 triggers at High (1) as a Category deal breaker (this vault did suffer permanent loss), which is reflected in the Strategy score but does not cap the overall grade.

---

## Improvement Summary

| Classification | Count | Current Points Gap | Potential Points Gain |
|----------------|-------|--------------------|-----------------------|
| Improvable | 23 | -145.8 | +145.8 |
| Source Missing | 3 | -21.8 | +21.8 |
| Non-Improvable | 8 | -55.1 | 0 (historical/structural) |
| Already Optimal | 48 | 0 | 0 |
| N/A | 2 | 0 | 0 |

**Top Improvement Opportunities:**

1. **Reduce Synthetic/Wrapped Collateral Concentration** [ST-C-04, ST-C-01]: Current 3/3, Potential 9 -- Improvable
2. **Connect Monitoring to Automated Protections** [S-SC-10]: Current 3, Potential 9 -- Improvable
3. **Publish Comprehensive Incident Playbook** [S-KM-08]: Current 3, Potential 9 -- Improvable
4. **Disclose and Build Treasury / Loss Reserve** [O-FR-01, O-FR-02]: Current 3/1, Potential 9 -- Improvable / Source Missing
5. **Document Procedures to Halt Automated Allocation** [O-TL-05, ST-PM-10]: Current 3, Potential 9 -- Improvable
6. **Demonstrate Clean Post-Resolv Track Record** [O-TL-09, O-FR-04, ST-PM-02]: Current 1-3, Potential 9 -- Time-Dependent Improvable

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 305.0/360 (84.7%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | Yes. 25+ audits from Tier-0/1 firms (ChainSecurity, Spearbit/OpenZeppelin, Zellic, Certora, Blackthorn) plus Cantina competition. Morpho Blue core (~600 LOC, immutable) and MetaMorpho framework extensively audited; Certora formal verification. This vault (0x8eB6...) is a MetaMorpho V1 vault from the audited factory, Etherscan-verified (Solidity v0.8.21). | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0x8eB67A509616cd6A7c1B3c8C21D48FF57df3d458), [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | December 2025: Certora (Tier-0), Spearbit (Tier-0 via Cantina), Blackthorn for Vaults V2 adapter work. September 2025: ChainSecurity (Tier-0). Multiple Tier-0 auditors for most recent work. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable. This vault is a non-upgradeable V1 MetaMorpho contract. Vault-framework upgrades (Vaults V2, Sep-Dec 2025) were preceded by multiple Tier-0 audits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P0] [Etherscan](https://etherscan.io/address/0x8eB67A509616cd6A7c1B3c8C21D48FF57df3d458) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 vulnerability patched immediately with OpenZeppelin. Certora formal verification provides mathematical proof of critical invariants. All V2 audit findings resolved before deployment with re-reviews. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue core is immutable. The MetaMorpho V1 vault (0x8eB6...) is a non-upgradeable ERC4626 contract. Market changes require Curator + 3-day timelock (259,200s) + Guardian veto. Timelock exceeds the 24h minimum. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=259200), [P0] [Etherscan](https://etherscan.io/address/0x8eB67A509616cd6A7c1B3c8C21D48FF57df3d458) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | YES — confirmed vault-specific loss ≥2% of pre-exploit TVL, not fully verified as 100% compensated, no detailed post-mortem within 30 days. The March 2026 Resolv USR exploit caused confirmed socialized bad debt in this vault's wstUSR/USDC market (~$4.95M allocation, ~$2.91M liquidity; USR collapsed to ~$0.025). **Verified pre-exploit TVL ≈ $76M–$83M** (Morpho API historicalState: $82.6M on Mar 20, $75.5M on Mar 21, $76.4M on the Mar 22 exploit day; mid-March peak ~$115.5M). **Realized Core bad debt ≈ $3.8M–$4.05M** (Gauntlet = 96% of the ~$5.95M–$6.2M Morpho-wide bad debt, net of Frontier's ~$1.9M portion; the wstUSR/USDC structural deficit is the dominant driver), i.e. **~4.6%–5.3% of pre-exploit TVL — above the 2% Mid threshold.** Independently corroborated on-chain: live vault sharePriceUsd ≈ 0.818 vs un-impaired baseline ≈ 1.085 (~24.6% crystallized NAV impairment). Compensation now live (4,379,827 USDC via Merkl, June 4 2026, Core open) but that total covers FIVE vaults and is **less than** Gauntlet-wide bad debt (~$5.7M–$5.95M) with **no per-vault split published**, so 100% coverage of Core depositors is unverifiable; no detailed Resolv/Gauntlet post-mortem published within 30 days. Per the NO-ASSUMPTIONS / conservative rule, score High (1): loss ≥2% AND full compensation unverifiable AND no post-mortem. | 1 | 1 | Non-Improvable | [P0] Morpho GraphQL API (historicalState totalAssetsUsd Mar 2026; live sharePriceUsd=0.818), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit), [P4] [OAK Research - Curators Face Responsibilities](https://oakresearch.io/en/analyses/investigations/the-resolv-usr-hack-curators-face-their-responsibilities), [P4] [Gauntlet/Resolv Compensation (Bitget)](https://www.bitget.com/asia/amp/news/detail/12560605443387) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho operates as ADDMO (French nonprofit). Gauntlet Networks Inc. is a well-funded ($41.8M raised, $1B valuation) US company with public leadership. No credible allegations against either entity. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P2] [Gauntlet About](https://www.gauntlet.xyz/about) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No evidence of timelock reductions. The vault has a 3-day timelock (259,200 seconds), verified via Morpho GraphQL API (June 2026). No reductions observed. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=259200) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Morpho runs dual active public bounties: Cantina ($2.5M max) and Immunefi ($2.5M max for Morpho Blue, $1.5M for MetaMorpho/periphery). Both are Tier-0 platforms. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3), [P1] [Immunefi Bounty](https://immunefi.com/bug-bounty/morpho/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Gauntlet partners with Hypernative (real-time monitoring), ZeroShadow (24/7 vSOC), Chainalysis, and SEAL Intel. However, monitoring cannot automatically trigger protective actions — no on-chain circuit breakers, no automated pause. During the March 2026 Resolv exploit, the Public Allocator continued auto-supplying USDC into this vault's broken wstUSR market post-exploit, demonstrating that alerts were not connected to automated protective actions. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers. The Resolv exploit confirmed this failure in THIS vault: automated allocation (Public Allocator / supplyOnBehalf) injected USDC into the compromised wstUSR market and no circuit breaker halted it. Morpho Blue prioritizes immutability; Guardian can only veto pending timelocked actions, not pause markets. Scored High (1) per framework scope requiring circuit breakers to cover automated allocation flows. | 1 | 1 | Non-Improvable | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P4] [Resolv Analysis](https://resolv-usr-exploit.vercel.app/) |

**Smart Contract Security Subtotal: 140.0/180 (77.8%)**
- 8 questions scored 9 (sum = 72), 1 question scored 3 (sum = 3), 2 questions scored 1 (sum = 2)
- Raw sum = 77 out of max 99
- Weighted = (77/99) x 180 = 140.0

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Owner: Gnosis Safe 4-of-7 (0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec), verified (Safe v1.3.0, 7 owners, threshold=4, nonce=508). Guardian: Safe 3-of-7 (0x7084bF4dB6c21e1834dD6482f6056a39A33584cD, v1.4.1, nonce=4). Curator: Safe 3-of-7 (0x9E33faAE38ff641094fa68c65c2cE600b3410585, v1.4.1, nonce=452). Timelock 259,200s (3 days). All changes visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API Guardian](https://api.safe.global/tx-service/eth/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/), [P0] [Safe API Curator](https://api.safe.global/tx-service/eth/api/v1/safes/0x9E33faAE38ff641094fa68c65c2cE600b3410585/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Vault is non-upgradeable. Moving funds requires Morpho Blue immutable logic. Market changes require multisig + 3-day timelock + Guardian. Permissionless ERC4626 redemption always available. Owner is 4-of-7 (threshold >=3, signers >=5), timelock >=24h. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=259200, owner threshold=4), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner 4-of-7 Safe (7 distinct owners, threshold=4) meets the >=4-of-7 Low Risk minimum. Guardian and Curator are each 3-of-7. Gauntlet publicly identified as operator. Several addresses overlap across the three Gauntlet multisigs (all Gauntlet team). | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking. No pause on Morpho Blue (immutable). Guardian can only revoke pending timelocked actions. Withdrawals always permissionless via direct contract interaction. Rules public. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets in non-custodial Morpho Blue contracts on Ethereum. Permissionless ERC4626 redemption. No off-chain custody. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Vault funds held in Morpho Blue markets, segregated from treasury/ops. Performance fee (5%) accrued on-chain transparently. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (fee=0.05), [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain enforced whitelist of Morpho Blue markets only. Current markets (GraphQL, June 2026): cbBTC/USDC, WBTC/USDC, tBTC/USDC, LBTC/USDC, weETH/USDC (all 86%/77% LLTV), stcUSD/USDC, siUSD/USDC, syrupUSDC/USDC, AA_FalconXUSDC/USDC (91.5%/77% LLTV). New markets require Curator + 3-day timelock + Guardian veto, with on-chain supply caps. The whitelist is broad ("Core" higher-risk mandate). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (allocation data), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Gauntlet's posture includes ZeroShadow (vSOC), Hypernative, SEAL Intel. Morpho docs include emergency procedures. However, no public, vault-specific incident playbook with explicit key-rotation steps or tabletop-exercise results has been published. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Morpho Emergency Procedures](https://docs.morpho.org/curate/emergency/) |

**Key Management Subtotal: 165.0/180 (91.7%)**
- 7 questions scored 9 (sum = 63), 1 question scored 3 (sum = 3)
- Raw sum = 66 out of max 72
- Weighted = (66/72) x 180 = 165.0

---

### **Security Total: 305.0/360 (84.7%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 140.0 | 180 | 77.8% |
| Key Management | 165.0 | 180 | 91.7% |
| **Security Total** | **305.0** | **360** | **84.7%** |

---

### STRATEGY (30% Weight) -- Score: 147.3/270 (54.6%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from overcollateralized USDC lending against crypto and synthetic-stablecoin collateral. 100% mandate-aligned — the "Core" mandate explicitly targets a higher risk/yield level than Prime. Current net APY ~3.89% (5% fee). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (netApy=0.0389), [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss can occur in severe but plausible single-shock events: the vault holds synthetic/RWA-credit stablecoin collateral (stcUSD, FalconX AA, siUSD) at 91.5%/77% LLTV, and the March 2026 Resolv loss demonstrated that a depegging synthetic collateral plus immutable oracle can socialize bad debt. Mid (3) per "principal loss can occur in severe but plausible single-shock events." | 3 | 9 | **Improvable** | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P4] [Resolv Analysis](https://resolv-usr-exploit.vercel.app/) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault simply lends USDC. No rehypothecation of depositor funds. Effective leverage 1.0x. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | YES -- this vault itself experienced permanent loss. The March 2026 Resolv USR exploit caused confirmed socialized bad debt in this vault's wstUSR/USDC market (loss >=0.5% of peak strategy TVL). Although compensation is now live (4.38M USDC via Merkl across affected Gauntlet vaults), the loss was crystallized for depositors at the time. Meets High (1): permanent-loss event at or above 0.5% of peak strategy TVL. **Time-dependent:** Low (9) requires "no permanent-loss events for this strategy or comparable variant over last 24 months" -- unlike S-SC-06 there is no "never mitigated by age" clause, so once the Resolv event rolls out of the 24-month window (~March 2028) with no recurrence and a published post-mortem, this returns toward 9 (same basis on which O-TL-09/ST-PM-02 are treated as improvable). | 1 | 9 | **Improvable (Time-Dependent)** | [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit), [P4] [OAK Research](https://oakresearch.io/en/analyses/investigations/the-resolv-usr-hack-curators-face-their-responsibilities) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Gauntlet publishes comprehensive curation methodology via VaultBook (risk factors, due diligence, market allocation strategy), quantitative insolvency limits, and a tiering system (Prime/Balanced/Core/Frontier). | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults), [P1] [Curation Methodology](https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. Yield is organic from USDC lending demand (net APY ~3.89% after 5% fee). No emissions required for base yield, though some collateral markets carry external incentives (e.g., syrupUSDC rewards). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (netApy=0.0389, fee=0.05) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | USDC is deeply liquid, so redeemed assets are immediately usable. However, current utilization is ~85-92% across markets and the vault demonstrated that some markets (wstUSR, Resolv) can become stuck/illiquid. Most of the position can be unwound over the stated horizon, but full immediate exit is not guaranteed. Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (utilization ~85-92%) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | The vault's own yield is lending interest (no carry/basis trade). However it lends against peg-dependent synthetic stablecoins; that risk is captured in collateral/oracle questions. The lending mechanic itself is not a carry/peg trade. Low (9). | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Yes. Morpho's Public Allocator / `supplyOnBehalf` can route capital into whitelisted markets. Supply caps limit per-market exposure but no automatic kill-switch exists for abnormal conditions — and during the March 2026 Resolv exploit, the donation-attack/Public Allocator bypassed zero-caps and supplied USDC into this vault's broken market for hours. Halting requires manual curator intervention. Mid (3). | 3 | 9 | **Improvable** | [P1] [Morpho Public Allocator](https://docs.morpho.org/curate/concepts/public-allocator/), [P4] [Resolv Analysis](https://resolv-usr-exploit.vercel.app/) |

**Protocol Mechanics Subtotal: 30.6/45 (67.9%)**
- 9 applicable questions (ST-PM-04 = N/A): 5 scored 9 (sum = 45), 3 scored 3 (sum = 9), 1 scored 1 (sum = 1)
- Raw sum = 55 out of max 81
- Weighted = (55/81) x 45 = 30.6

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Higher-risk mixed set: wrapped BTC (cbBTC, WBTC, tBTC, Lombard LBTC), ether.fi restaked weETH (86% LLTV), and synthetic/RWA-credit stablecoins — Cap stcUSD (~24.7%), Pareto/FalconX AA tranche (~25.0%), InfiniFi siUSD, Maple syrupUSDC (91.5%/77% LLTV). cbBTC/WBTC are established but custodial; tBTC/LBTC/weETH are newer; the synthetic stablecoins are novel, lower-liquidity, higher-risk. Each is tiered via on-chain LLTV and supply caps, but the set includes materially riskier assets than Prime's blue-chip mandate. Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (allocation data) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | High risk. Within the 12-month lookback, this vault's wstUSR collateral collapsed >97% (to ~$0.025) during the March 2026 Resolv exploit — a depeg far above 10%. The market has since been removed, but the demonstrated history within the window meets High (1): any collateral showed depeg above 10%. **Time-dependent:** the >10% depeg falls out of the 12-month lookback after ~March 2027; with the market removed and no new collateral depeg, this rises toward Low (9) — consistent with roadmap item 9 and ST-L-03 (which already carries potential 9). | 1 | 9 | **Improvable (Time-Dependent)** | [P4] [Resolv Analysis](https://resolv-usr-exploit.vercel.app/), [P0] Morpho GraphQL API |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Applicable: weETH (ether.fi restaked ETH, EigenLayer slashing) and LBTC (Lombard, Babylon BTC staking) are staking-based collaterals (~$1.04M + $1.75M). EigenLayer/Babylon slashing is monitored with diversified operators, but mitigation buffers/insurance for these newer restaking assets are limited. Mid (3). | 3 | 9 | **Improvable** | [P3] ether.fi / Lombard operator data |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | Moderate. Per the framework definition, "bridged or wrapped" excludes protocol receipt tokens and synthetic/credit stablecoins (their risk is captured in ST-C-01/ST-C-02/ST-PC-01/ST-IC-02/ST-M-05). Applying strictly — consistent with how Smokehouse USDC scored this (sUSDe/syrupUSDC/PT excluded → Mid 3) — only bridged/wrapped BTC counts: cbBTC+WBTC+tBTC+LBTC ~$3.19M ≈ 38% of TVL. weETH (~$1.04M, ether.fi LST receipt) and the synthetic stablecoins (stcUSD, siUSD, FalconX AA, syrupUSDC ~$4.18M+) are excluded. ~38% falls in the 20–60% band with on-chain caps → Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (allocation: stcUSD $2.08M, FalconX AA $2.10M, LBTC $1.75M, weETH $1.04M, cbBTC $0.95M, tBTC $0.49M) |

**Collateral Subtotal: 12.5/45 (27.8%)**
- 3 questions scored 3 (sum = 9), 1 question scored 1 (sum = 1)
- Raw sum = 10 out of max 36
- Weighted = (10/36) x 45 = 12.5

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Chain/oracle dependencies are Tier-0: Ethereum (Tier-0), Chainlink-based Morpho oracle adapters. No bridges, no CEX operational dependency. All explicitly identifiable on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | **Hardcoded/immutable oracle check (mandatory):** Each Morpho Blue market uses an immutable oracle that cannot be corrected post-deployment. This vault holds depeg-capable synthetic stablecoin collateral, and the March 2026 Resolv loss directly exploited a hardcoded $1 wstUSR oracle in THIS vault. Per the mandatory check (immutable oracle + asset can depeg = High), score High (1). No fallback oracle exists for any market. | 1 | 1 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/), [P4] [Resolv Analysis](https://resolv-usr-exploit.vercel.app/) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Gauntlet operates off-chain risk/allocation engines. It claims an institutional-grade security posture (Hypernative, ZeroShadow, Chainalysis, SEAL Intel) but no SOC 2 Type II or ISO27001 certification for Gauntlet Networks Inc. is publicly disclosed. Chainlink holds enterprise certifications. Mid (3). | 3 | 9 | **Source Missing** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | High risk. During the March 2026 Resolv exploit, Gauntlet's automated allocation continued supplying USDC to this vault's broken wstUSR market post-exploit, directly contributing to the bad debt. The framework High (1) covers incidents where infra components "contributed to losses." | 1 | 1 | Non-Improvable | [P4] [Protos - Resolv](https://protos.com/resolv-hack-shows-defi-learned-nothing-from-last-contagion/), [P4] [Resolv Analysis](https://resolv-usr-exploit.vercel.app/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum (Tier-0) has had no chain halts >30 minutes in the last 12+ months. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Relevant for weETH and LBTC (staking-based collateral, ~$2.8M combined). No material slashing events affecting these validator sets caused depositor loss in the last 12 months. Low (9). | 9 | 9 | Non-Improvable (optimal) | [P3] ether.fi / Lombard slashing data |
| ST-IC-07 | Are validators diverse geographically and by operator? | weETH (ether.fi) uses diversified node operators; LBTC (Lombard) uses multiple Babylon finality providers (Galaxy, Kiln, P2P, Figment). No single operator >25% for the relevant sets. Low (9). | 9 | 9 | Non-Improvable (optimal) | [P3] ether.fi / Lombard operator data |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No single infra component is a single point of failure. Permissionless ERC4626 redemption is always available, so no component can block withdrawals. The Resolv loss did NOT result from a single component — it required a multi-factor failure (USR collateral collapse + a hardcoded $1 oracle + the donation-attack/supplyOnBehalf flow); the single-oracle/collateral risk is already captured in ST-IC-02=1 and ST-C-02=1. Consistent with every comparable Morpho USDC vault (Prime, Steakhouse, Smokehouse, and Frontier V2 — which references the same Resolv loss path — all score 9). Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P0] Morpho GraphQL API |

**Infrastructure Counterparty Subtotal: 31.3/45 (69.4%)**
- 5 questions scored 9 (sum = 45), 1 question scored 3 (sum = 3), 2 questions scored 1 (sum = 2)
- Raw sum = 50 out of max 72
- Weighted = (50/72) x 45 = 31.25 ≈ 31.3

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Capital is deployed to Morpho Blue (Tier-0) markets, but collateral dependency chains extend to multiple newer/Tier-3 venues: Resolv (Tier-3, exploited and caused this vault's loss), Cap (stcUSD), InfiniFi (siUSD), Pareto/FalconX (AA tranche), Maple (syrupUSDC), Lombard (LBTC). Most venues are disclosed, but the strategy relied materially on a Tier-3 venue (Resolv) that failed. Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (allocation data) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Performance fee (5%) documented and verified on-chain. Collateral-protocol incentives (e.g., syrupUSDC rewards) are publicly visible on the Morpho app. No hidden rebates found. Low (9). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (fee=0.05) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | On-chain supply caps per market exist (e.g., tBTC $6M, LBTC $20M, stcUSD/FalconX/weETH $10M each). However, the March 2026 exploit demonstrated that `supplyOnBehalf` can bypass vault-level caps (including zero-caps). Caps are enforced at the vault layer but not fully at the protocol layer. Mid (3). | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API (supplyCap per market), [P4] [DeFi Prime - Resolv](https://defiprime.com/resolv-usr-exploit) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Lending positions unwind as borrowers repay. This vault demonstrated the downside: the Resolv markets became stuck/illiquid and had to be removed. Current markets run at high utilization. Some counterparties require longer lead times under stress. Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (utilization data) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending. No external validators, custodians, or asset managers operate the vault. Gauntlet (curator) disclosed. Underlying collateral issuers (Coinbase, BitGo, Cap, InfiniFi, Pareto, Maple, Lombard) are publicly known. Deal Breaker does not trigger. | 9 | 9 | Non-Improvable (optimal) | Vault architecture |

**Protocol Counterparty Subtotal: 27.0/45 (60.0%)**
- 2 questions scored 9 (sum = 18), 3 questions scored 3 (sum = 9)
- Raw sum = 27 out of max 45
- Weighted = (27/45) x 45 = 27.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain ERC4626 redemption. No address-level blocking, no admin pause. Withdrawal depends on market liquidity (idle USDC across markets). Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Current utilization is ~85-92% across markets, so only ~10-15% is immediately withdrawable; USDC is deeply liquid so staggered exits clear, but near-total instant exit is not guaranteed at high utilization. Mid (3). | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API (utilization ~85-92%) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | This vault experienced a real withdrawal-impairment event: during the March 2026 Resolv exploit, the affected markets were removed and a claim snapshot was taken, impairing exit from those positions. The broader vault recovered and processes normal withdrawals. Short, resolved overruns with clear cause. Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API, [P4] [Resolv Analysis](https://resolv-usr-exploit.vercel.app/) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Caps are sized relative to TVL, but the Resolv stress and supplyOnBehalf bypass demonstrated cap-related friction. Queues during the incident were resolved. Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (supplyCap data) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | During the March 2026 Resolv stress, the affected markets became illiquid (multi-day dysfunction for those positions), but the broader USDC vault remained functional and normalized after the markets were removed. Noticeable delays/discounts but access remained. Mid (3). | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API, [P4] [Resolv Analysis](https://resolv-usr-exploit.vercel.app/) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure USDC lending with no lockups, vesting, or bridge dependencies. Withdrawal speed limited only by market utilization. Low (9). | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary ERC4626 redemption is always available and the redeemed asset (USDC) is the most liquid stablecoin — unlike a EURC vault, holders face no meaningful secondary-market friction. Low (9). | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | USDC and the gtUSDCcore receipt are deep, but several collateral tokens (stcUSD, FalconX AA tranche, siUSD) have thin secondary markets, limiting liquidation depth in those markets. Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API, [P3] synthetic-stablecoin market data |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | The Resolv event was effectively a partial bank-run on the affected markets, and bad debt was socialized (then compensated). For the current healthy USDC portfolio, a run would cause queues and some discounting with losses contained by caps/market isolation. Mid (3). | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API |

**Liquidity Subtotal: 25.0/45 (55.6%)**
- 3 questions scored 9 (sum = 27), 6 questions scored 3 (sum = 18)
- Raw sum = 45 out of max 81
- Weighted = (45/81) x 45 = 25.0

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | gtUSDCcore shares are ERC4626 NAV claims. During the March 2026 Resolv stress the share value reflected accrued bad debt (a real, if bounded, dislocation) before compensation. Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Low. The vault lends USDC (dollar-denominated); no directional BTC/ETH exposure for lenders. Loss risk is bad debt from borrower defaults requiring collateral to breach the LLTV buffer. Low (9). | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Immutable Adaptive Curve IRM per market. Generally robust, but several Core markets reach high utilization and the Resolv markets hit 100% (collateral failure, not rate-model failure). Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (utilization data) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Gauntlet uses agent-based simulations and targets insolvent debt limits, but the March 2026 Resolv attack vector (mint exploit + hardcoded oracle + donation attack) was not modeled, and Core-specific synthetic-collateral stress modeling is not publicly demonstrated. Mid (3). | 3 | 9 | **Source Missing** | [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side risk. Current synthetic markets sit at 91.5% LLTV (thin ~8.5% buffer); the Resolv collapse already demonstrated forced-liquidation-into-bad-debt in this vault, though that market is removed and current BTC markets carry an ~14% buffer (86% LLTV). Bounded by caps and market isolation. Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API, [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 21.0/45 (46.7%)**
- 1 question scored 9 (sum = 9), 4 questions scored 3 (sum = 12)
- Raw sum = 21 out of max 45
- Weighted = (21/45) x 45 = 21.0

---

### **Strategy Total: 147.3/270 (54.6%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 30.6 | 45 | 67.9% |
| Collateral | 12.5 | 45 | 27.8% |
| Infra Counterparty | 31.3 | 45 | 69.4% |
| Protocol Counterparty | 27.0 | 45 | 60.0% |
| Liquidity | 25.0 | 45 | 55.6% |
| Market | 21.0 | 45 | 46.7% |
| **Strategy Total** | **147.3** | **270** | **54.6%** |

---

### OPERATIONS (30% Weight) -- Score: 225.0/270 (83.3%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid with strong checks. Morpho Blue immutable. Vault changes require Owner multisig (4-of-7) + 3-day timelock + Guardian (3-of-7) veto. No single entity can unilaterally change core logic. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock, owner, guardian), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- No governance-token voting for this vault. Controlled by multisig + Guardian; concentration captured in S-KM-01/03. | N/A | N/A | N/A | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. 3-day timelock (259,200s) verified via Morpho GraphQL API, exceeding the 24h minimum. Guardian (3-of-7 Safe) can veto pending changes; all pending actions visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=259200), [P0] [Safe API Guardian](https://api.safe.global/tx-service/eth/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner can appoint a new Curator (subject to 3-day timelock). Withdrawals remain permissionless via ERC4626 throughout. Transparent on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 3 questions scored 9 (sum = 27); O-G-02 = N/A
- Raw sum = 27 out of max 27
- Weighted = (27/27) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Gauntlet: Tarun Chitra (CEO/Co-founder, ex-D.E. Shaw Research), Rei Chiang (Co-founder), 50+ team. Morpho: Paul Frambot (CEO). All publicly identified with verifiable track records. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Team](https://www.gauntlet.xyz/our-team), [P1] [Morpho](https://morpho.org/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Gauntlet has 50+ employees across 3 continents; Morpho has a separate full team ($73.6M raised). No key-person dependency. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet About](https://www.gauntlet.xyz/about) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Morpho: ADDMO (French nonprofit, Paris) + Morpho Labs SAS. Gauntlet: Gauntlet Networks Inc. (New York, USA). Both clearly identified. The SEC action against unrelated "Gauntlet Holdings, LLC" is a different entity. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P1] [Gauntlet](https://www.gauntlet.xyz/) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known actions against Gauntlet Networks Inc. or Morpho entities. SEC LR-26266 concerns a different "Gauntlet Holdings, LLC." | 9 | 9 | Non-Improvable (optimal) | [P0] [SEC LR-26266](https://www.sec.gov/enforcement-litigation/litigation-releases/lr-26266) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Gauntlet has 24/7 on-call (ZeroShadow vSOC, Hypernative, SEAL Intel). However, the framework requires incident response to halt automated allocation within SLA. During the March 2026 Resolv exploit, automated allocation continued supplying this vault's broken market for hours — response did not halt automated flows within SLA. Mid (3). | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P4] [Protos - Resolv](https://protos.com/resolv-hack-shows-defi-learned-nothing-from-last-contagion/) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Gauntlet acknowledged the Resolv incident, published updates, and ultimately negotiated and launched a compensation program (4.38M USDC via Merkl, June 2026). Active VaultBook documentation; Morpho's 4-minute response in April 2025. | 9 | 9 | Non-Improvable (optimal) | [P4] [Gauntlet/Resolv Compensation (Bitget)](https://www.bitget.com/asia/amp/news/detail/12560605443387) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Gauntlet: $41.8M from Polychain, Paradigm, Ribbit Capital ($1B valuation). Morpho: a16z, Variant, Pantera, Coinbase Ventures ($73.6M). All disclosed. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay - Gauntlet Funding](https://www.clay.com/dossier/gauntlet-funding) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Gauntlet manages 70+ vaults / $1.3B+ AUM across Prime/Balanced/Core/Frontier tiers. Structural mitigations (tiered system, automated allocation, VaultBook) exist, but no formal quantitative conflict-of-interest policy is published, and the Resolv incident raised cross-vault risk-routing questions. Mid (3). | 3 | 9 | **Improvable** | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | Yes — directly. The March 2026 Resolv USR exploit caused confirmed bad debt in this Gauntlet-curated Core vault (and Frontier). This is the first confirmed bad debt in a Gauntlet vault. It is now being compensated (4.38M USDC via Merkl, opened June 4 2026, Core included) and Gauntlet implemented process changes (markets removed, caps to zero). Scored Mid (3): one historical loss incident, now compensated with demonstrable process improvements. Borderline with High given the direct hit and the curation decision to hold a hardcoded-oracle synthetic. | 3 | 9 | **Improvable** | [P4] [Gauntlet/Resolv Compensation (Bitget)](https://www.bitget.com/asia/amp/news/detail/12560605443387), [P4] [OAK Research](https://oakresearch.io/en/analyses/investigations/the-resolv-usr-hack-curators-face-their-responsibilities) |

**Team & Legal Subtotal: 52.5/67.5 (77.8%)**
- 6 questions scored 9 (sum = 54), 3 questions scored 3 (sum = 9)
- Raw sum = 63 out of max 81
- Weighted = (63/81) x 67.5 = 52.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive Morpho docs and Gauntlet VaultBook (curation methodology, risk factors, allocation strategy), updated regularly. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Docs](https://docs.morpho.org/), [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Liquidation mechanics, bad-debt socialization, oracle risks, and loss conditions documented across Morpho docs and Gauntlet VaultBook. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Morpho docs maintain a canonical address registry; vault address shown on Morpho App and Gauntlet App; all contracts Etherscan-verified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Vault roles (Owner, Curator, Guardian, Allocator) documented with permission descriptions; timelock documented; changes visible on-chain via Safe history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves and proof-of-liabilities (borrows) visible on Morpho App, Etherscan, and the Morpho GraphQL API. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0x8eB67A509616cd6A7c1B3c8C21D48FF57df3d458), [P0] Morpho GraphQL API |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. Vault contract (0x8eB6...) verified on Etherscan as MetaMorpho (Solidity v0.8.21). Morpho Blue (0xBBBB...) verified. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0x8eB67A509616cd6A7c1B3c8C21D48FF57df3d458) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions, all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated, ring-fenced safety module with binding activation rules. Bad debt is socialized per market; the Resolv compensation was a discretionary, negotiated program (Gauntlet/Resolv), not a pre-committed reserve. Morpho DAO treasury is discretionary via governance. Mid (3). | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Insufficient. Morpho DAO treasury is ~$24.8M, essentially entirely in MORPHO tokens (~$24.84M own-tokens + ~$5.7K non-own per DeFiLlama, June 2026; lower than prior ~$33.8M as MORPHO price declined). Against ~$10B+ protocol-wide TVL this is <1% and dominated by a volatile native token. No vault-specific reserve. High (1). | 1 | 9 | **Source Missing** | [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Gauntlet ($41.8M raised, $1B valuation) and Morpho ($73.6M raised) both have sustainable revenue and combined runway >24 months. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay - Gauntlet Funding](https://www.clay.com/dossier/gauntlet-funding) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | Mixed. This vault took a direct Resolv hit (socialized bad debt; TVL is now ~$8.4M, below historical peak), but recovered: affected markets removed, vault functional, and compensation arranged (no permanent uncompensated depositor loss as of June 2026). Significant but recoverable stress, buffers/compensation used. Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (totalAssetsUsd=$8.42M), [P4] [Gauntlet/Resolv Compensation (Bitget)](https://www.bitget.com/asia/amp/news/detail/12560605443387) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue is immutable; permissionless ERC4626 withdrawals; no proprietary off-chain services required for core operations. If Gauntlet disappeared, existing allocations persist and users can withdraw. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Financial Resilience Subtotal: 37.5/67.5 (55.6%)**
- 2 questions scored 9 (sum = 18), 2 questions scored 3 (sum = 6), 1 question scored 1 (sum = 1)
- Raw sum = 25 out of max 45
- Weighted = (25/45) x 67.5 = 37.5

---

### **Operations Total: 225.0/270 (83.3%)**

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
| **Security** | Smart Contract Security (11 Q) | 77 | 99 | 140.0 | 180 | 77.8% |
| | Key Management (8 Q) | 66 | 72 | 165.0 | 180 | 91.7% |
| | **Security Subtotal** | | | **305.0** | **360** | **84.7%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 55 | 81 | 30.6 | 45 | 67.9% |
| | Collateral (4 Q) | 10 | 36 | 12.5 | 45 | 27.8% |
| | Infra Counterparty (8 Q) | 50 | 72 | 31.3 | 45 | 69.4% |
| | Protocol Counterparty (5 Q) | 27 | 45 | 27.0 | 45 | 60.0% |
| | Liquidity (9 Q) | 45 | 81 | 25.0 | 45 | 55.6% |
| | Market (5 Q) | 21 | 45 | 21.0 | 45 | 46.7% |
| | **Strategy Subtotal** | | | **147.3** | **270** | **54.6%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 63 | 81 | 52.5 | 67.5 | 77.8% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 25 | 45 | 37.5 | 67.5 | 55.6% |
| | **Operations Subtotal** | | | **225.0** | **270** | **83.3%** |
| **TOTAL** | | | | **677.3** | **900** | **75.3%** |

---

## Validation Checklist

- [x] Smart Contract Security: (8x9 + 1x3 + 2x1) = 72+3+2 = 77/99; (77/99)*180 = 140.0 (verified)
- [x] Key Management: (7x9 + 1x3) = 63+3 = 66/72; (66/72)*180 = 165.0 (verified)
- [x] Security Total: 140.0 + 165.0 = 305.0 (verified)
- [x] Protocol Mechanics: (5x9 + 3x3 + 1x1) = 45+9+1 = 55/81; (55/81)*45 = 30.56 ~ 30.6 (1 N/A) (verified)
- [x] Collateral: (3x3 + 1x1) = 9+1 = 10/36; (10/36)*45 = 12.5 (verified)
- [x] Infra Counterparty: (5x9 + 1x3 + 2x1) = 45+3+2 = 50/72; (50/72)*45 = 31.25 ≈ 31.3 (verified)
- [x] Protocol Counterparty: (2x9 + 3x3) = 18+9 = 27/45; (27/45)*45 = 27.0 (verified)
- [x] Liquidity: (3x9 + 6x3) = 27+18 = 45/81; (45/81)*45 = 25.0 (verified)
- [x] Market: (1x9 + 4x3) = 9+12 = 21/45; (21/45)*45 = 21.0 (verified)
- [x] Strategy Total: 30.56 + 12.5 + 31.25 + 27.0 + 25.0 + 21.0 = 147.31 ≈ 147.3 (verified)
- [x] Governance: (3x9) = 27/27; (27/27)*67.5 = 67.5 (1 N/A) (verified)
- [x] Team & Legal: (6x9 + 3x3) = 54+9 = 63/81; (63/81)*67.5 = 52.5 (verified)
- [x] Documentation: (6x9) = 54/54; (54/54)*67.5 = 67.5 (verified)
- [x] Financial Resilience: (2x9 + 2x3 + 1x1) = 18+6+1 = 25/45; (25/45)*67.5 = 37.5 (verified)
- [x] Operations Total: 67.5 + 52.5 + 67.5 + 37.5 = 225.0 (verified)
- [x] Grand Total: 305.0 + 147.3 + 225.0 = 677.3 (verified)
- [x] All percentages <= 100% (verified)
- [x] No score exceeds its maximum (verified)
- [x] Rating Overview table matches Final Score Calculation (verified)
- [x] Grade check: B- range is 660-685; 677.3 falls within B- (verified)
- [x] Potential: 330.9 + 244.0 + 270.0 = 844.9; BBB+ range 834-846 (verified; ST-PM-05 & ST-C-02 potential 1→9 time-dependent, ST-IC-08 potential 3→9, ST-C-04 current 1→3)

---

## Rating Determination

| Grade | Range | This Vault |
|-------|-------|------------|
| B | 685-710 | - |
| **B-** | **660-685** | **677.3 points** |
| CCC+ | 580-660 | - |

## **FINAL RATING: B-**

*High risk -- pronounced capital-at-risk in stress with thin buffers. This vault took a direct, demonstrated bad-debt loss in the March 2026 Resolv exploit (now compensated) and continues to hold high-LLTV synthetic/RWA-credit stablecoin collateral, placing it well below the blue-chip Gauntlet USDC Prime vault.*

---

## Key Risks

1. **Direct, Demonstrated Resolv Bad Debt (March 22, 2026) — ≥2% Loss, Incomplete Compensation**: This vault held ~$4.95M in a wstUSR/USDC market priced by a hardcoded $1 oracle; when USR collapsed to ~$0.025 after an ~80M unbacked-mint exploit, socialized bad debt was crystallized. Verified pre-exploit TVL was ~$76M–$83M (Morpho API historicalState, Mar 20–22, 2026), and the realized Core loss (~$3.8M–$4.05M; Gauntlet = ~96% of the ~$5.95M–$6.2M Morpho-wide bad debt, net of Frontier's ~$1.9M) is **~4.6%–5.3% of pre-exploit TVL — above the 2% threshold** (live sharePriceUsd ≈ 0.818 vs ≈ 1.085 baseline confirms a ~24.6% crystallized NAV impairment). Compensation (4,379,827 USDC via Merkl) opened June 4, 2026 with Core included, but it spans five vaults and is below the Gauntlet-wide bad debt with no per-vault split, so 100% Core coverage is unverifiable, and no detailed post-mortem was published within 30 days (ST-PM-05=1, S-SC-06=1) -- [OAK Research](https://oakresearch.io/en/analyses/investigations/the-resolv-usr-hack-curators-face-their-responsibilities), [Gauntlet/Resolv Compensation (Bitget)](https://www.bitget.com/asia/amp/news/detail/12560605443387)

2. **High-LLTV Synthetic / RWA-Credit Stablecoin Collateral**: ~50% of current TVL is in synthetic/credit stablecoins — Cap stcUSD (~$2.08M), Pareto/FalconX AA tranche (~$2.10M) — plus whitelisted InfiniFi siUSD and Maple syrupUSDC, several at 91.5% LLTV (thin ~8.5% buffer). These are novel, lower-liquidity, higher-risk assets versus Prime's blue-chip mandate (ST-C-01=3, ST-C-04=3, ST-M-05=3) -- [P0] Morpho GraphQL API allocation data

3. **Immutable Per-Market Oracle With No Fallback (Non-Improvable)**: Each Morpho Blue market uses one immutable oracle that cannot be corrected under abnormal conditions. This is the exact attack vector that failed in this vault (hardcoded $1 wstUSR price), and the vault still holds depeg-capable synthetic collateral (ST-IC-02=1) -- [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/)

4. **Automated Allocation Without Circuit Breakers (Demonstrated Failure)**: The Public Allocator / `supplyOnBehalf` donation attack supplied USDC into this vault's broken market post-exploit with no on-chain kill-switch, and monitoring was not connected to automated protective actions (S-SC-10=3, S-SC-11=1, ST-PM-10=3) -- [Resolv Analysis](https://resolv-usr-exploit.vercel.app/)

5. **No Dedicated Loss Reserve; Volatile-Token Treasury**: Bad debt is socialized per market; the Resolv compensation was a discretionary negotiated program, not a pre-committed reserve. Morpho DAO treasury (~$24.8M) is essentially 100% MORPHO tokens, <1% of protocol-wide TVL (O-FR-01=3, O-FR-02=1) -- [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho)

---

## Improvement Roadmap

### Quick Wins (High Impact, Low Effort)

1. **Connect Monitoring to Automated Protections** [S-SC-10] -- Current: 3, Potential: 9
   - Integrate Hypernative alerts with automated halt mechanisms for capital flows during anomalous conditions (oracle deviation, depeg, utilization spike)
2. **Publish Conflict-of-Interest Policy** [O-TL-08] -- Current: 3, Potential: 9
   - Formalize quantitative allocation rules and independent oversight across Gauntlet's 70+ vaults
3. **Document Procedures to Halt Automated Allocation** [O-TL-05, ST-PM-10] -- Current: 3, Potential: 9
   - Publish runbooks with explicit steps to halt the Public Allocator / set caps to zero within a 15-minute SLA

### Medium-Term Improvements (High Impact, Moderate Effort)

4. **Reduce Synthetic/Wrapped Collateral Concentration** [ST-C-01, ST-C-04] -- Current: 3/3, Potential: 9
   - Cap synthetic/RWA-credit stablecoin and wrapped exposure and shift toward blue-chip collateral (note: ST-C-04 already Mid at ~38% bridged/wrapped BTC; ST-C-01 reflects the broad synthetic-collateral set)
5. **Publish Comprehensive Incident Playbook** [S-KM-08] -- Current: 3, Potential: 9
   - Document key-rotation procedures and publish tabletop-exercise results
6. **Establish Dedicated Safety Module** [O-FR-01] -- Current: 3, Potential: 9
   - Create a ring-fenced backstop with binding activation rules (the Resolv compensation showed willingness; formalize it)
7. **Build/Disclose Reserve** [O-FR-02] -- Current: 1, Potential: 9
   - Establish a liquid reserve >=5% of vault TVL including stablecoins

### Time-Dependent Improvements

8. **Demonstrate Clean Post-Resolv Track Record** [O-TL-09, O-FR-04, ST-PM-02, ST-PM-05, ST-PC-04] -- Current: 1-3, Potential: 9
   - 24-36 months without further losses across Gauntlet-curated USDC vaults, plus full closure of the Resolv compensation (ST-PM-05 returns to 9 once the loss rolls out of the 24-month window ~March 2028 with no recurrence and a published post-mortem)
9. **Roll Off the wstUSR Depeg from the Lookback** [ST-C-02, ST-L-03] -- Current: 1/3, Potential: 9/9
   - The >10% depeg falls out of the 12-month window after ~March 2027, raising these once no new collateral depegs occur

### Long-Term Structural Changes (Non-Improvable)

- **Oracle Redundancy** [ST-IC-02]: Current 1 -- Requires Morpho protocol redesign (immutable oracle architecture); ST-IC-08 is now 9 (no single component blocks withdrawals; the Resolv loss was multi-factor)
- **Automatic Circuit Breakers** [S-SC-11]: Current 1 -- Morpho's design prioritizes immutability
- **Historical Resolv Loss** [S-SC-06]: Current 1 -- Permanent-loss exploit ≥2% of TVL; per the S-SC-06 timeframe rule, High-severity losses are never mitigated by age (unlike ST-PM-05, which carries a 24-month rolling window and is therefore time-dependent improvable)

### Evidence Gaps (Source Missing Items)

10. **Obtain/Disclose SOC 2 Certification** [ST-IC-03] -- Current: 3, Potential: 9
11. **Publish Core-Specific Synthetic-Collateral Stress Modeling** [ST-M-04] -- Current: 3, Potential: 9

**Maximum Achievable Grade:** BBB+ (844.9/900 points) if all improvable and source-missing items are addressed
**Points to Next Grade Tier (B):** 7.7 points needed to reach B (685 points)

---

## Platform Consistency Notes

This rating shares Morpho-platform-level scores with all Morpho vault ratings and Gauntlet-curator-level scores with the other Gauntlet vaults, except where this vault's **direct Resolv exposure** and **higher-risk collateral** create documented differences.

**Identical Scores (Platform/Curator-Level):**
- S-SC-01 through S-SC-05, S-SC-07, S-SC-08, S-SC-09: identical (Morpho Blue / MetaMorpho V1 infrastructure)
- S-KM-01 through S-KM-08: identical (same Gauntlet 4-of-7 Owner / 3-of-7 Guardian / 3-of-7 Curator multisigs, 3-day timelock)
- O-G-01 through O-G-04: identical governance model
- O-DT-01 through O-DT-06: identical documentation quality
- O-TL-01 through O-TL-08: identical team/legal (O-TL-05/08 = 3 as for all Gauntlet vaults)
- O-FR-01, O-FR-02, O-FR-03, O-FR-05: identical protocol-level financial resilience

**Different Scores vs Gauntlet USDC Prime (BB+/793.0) — driven by direct Resolv hit + higher-risk collateral:**
- S-SC-06: Core 1 (direct wstUSR bad debt, ≥2% loss, compensation unverified) vs Prime 9 (unaffected)
- S-SC-11: Core 1 (circuit-breaker failure demonstrated in this vault) vs Prime 3
- ST-PM-02: Core 3 vs Prime 9; ST-PM-05: Core 1 (direct loss) vs Prime 3 (comparable variant); ST-PM-08: Core 3 vs Prime 9
- ST-C-01: Core 3 vs Prime 9; ST-C-02: Core 1 (wstUSR depeg) vs Prime 9; ST-C-03: Core 3 vs Prime 9
- ST-C-04: Core 3 (only ~38% bridged/wrapped BTC; synthetic-credit stablecoins and weETH excluded per framework, as in Smokehouse USDC) vs Prime 1 (91.5% wrapped BTC) — Core scores *higher* here because Prime is far more wrapped-BTC-concentrated; Core's synthetic-collateral risk is captured in ST-C-01/ST-C-02/ST-PC-01/ST-IC-02/ST-M-05 instead
- ST-IC-02: Core 1 (immutable oracle exploited here) vs Prime 3; ST-IC-04: Core 1 vs Prime 9; ST-IC-08: Core 9 = Prime 9 (identical — no single component blocks withdrawals; consistent with all Morpho USDC vaults incl. Frontier V2)
- ST-PC-01: Core 3 vs Prime 9; ST-PC-03: Core 3 vs Prime 9; ST-PC-04: Core 3 vs Prime 9
- ST-L-03/04/08: Core 3 vs Prime 9; ST-M-01/03/05: Core 3 vs Prime 9
- O-TL-09: Core 3 (direct hit, now compensated) vs Prime 3 (same — comparable manager event)
- O-FR-04: Core 3 (affected-but-recovered) vs Prime 9 (unaffected)

**Relation to Gauntlet USDC Frontier V1 (CCC+/620.8):** Core (B-/677.3) and Frontier (CCC+/620.8) were both directly hit by Resolv. Core's Security is now 305.0/360 (S-SC-06=1 on the verified ≥2% loss) versus Frontier's 308.6/360 — the 3.6-point gap is because Frontier's larger pre-exploit TVL (~$115M) put its ~$1.9M loss at ~1.7% (<2%), letting Frontier hold S-SC-06 at Mid (3), whereas Core's ~4.6%–5.3% loss is High (1). Core still scores 56.5 points higher overall because it recovered (Resolv markets removed, vault functional, compensation live, current healthy USDC portfolio) whereas Frontier suffered an 88% TVL collapse with ~21% of positions stuck at 100% utilization and active distress at the time of its April 2026 rating.

---

## Smart Contract Addresses

| Role | Address | Explorer Link |
|------|---------|---------------|
| VaultContract | 0x8eB67A509616cd6A7c1B3c8C21D48FF57df3d458 | [Etherscan](https://etherscan.io/address/0x8eB67A509616cd6A7c1B3c8C21D48FF57df3d458) |
| MorphoBlue | 0xBBBBBBBBbb9cc5e90e3b3Af64bdAF62C37EEFFCb | [Etherscan](https://etherscan.io/address/0xBBBBBBBBbb9cc5e90e3b3Af64bdAF62C37EEFFCb) |
| OwnerMultisig | 0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec | [Etherscan](https://etherscan.io/address/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec) |
| Guardian | 0x7084bF4dB6c21e1834dD6482f6056a39A33584cD | [Etherscan](https://etherscan.io/address/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD) |
| CuratorMultisig | 0x9E33faAE38ff641094fa68c65c2cE600b3410585 | [Etherscan](https://etherscan.io/address/0x9E33faAE38ff641094fa68c65c2cE600b3410585) |

## Additional Info

| Field | Value |
|-------|-------|
| Infrastructure Provider | Morpho |
| Protocol Base | _none_ |
| Stated Withdrawal Time | Instant |
| Treasury | 24800000 |
| Treasury Addresses | 0xcBa28b38103307Ec8dA98377ffF9816C164f9AFa (Ethereum, Base -- governance multisig 5/9) |

### Code Audits

| Auditor | Report Link |
|---------|-------------|
| ChainSecurity | [Security Reviews](https://docs.morpho.org/security-reviews/) |
| Spearbit | [Security Reviews](https://docs.morpho.org/security-reviews/) |
| OpenZeppelin | [Security Reviews](https://docs.morpho.org/security-reviews/) |
| Zellic | [Security Reviews](https://docs.morpho.org/security-reviews/) |
| Certora | [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| Blackthorn | [Security Reviews](https://docs.morpho.org/security-reviews/) |

### Oracles Used

| Oracle | Documentation Link |
|--------|-------------------|
| Chainlink | [Chainlink Data Feeds](https://data.chain.link/) |
| Morpho Chainlink Oracle Adapters (per-market, immutable) | [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |

---

## Sources

### Protocol Documentation
1. [Morpho Documentation](https://docs.morpho.org/)
2. [Morpho Security Reviews](https://docs.morpho.org/security-reviews/)
3. [Morpho Risk & Security](https://docs.morpho.org/learn/resources/risks)
4. [Morpho Roles & Capabilities](https://docs.morpho.org/curate/concepts/roles/)
5. [Morpho Oracle Concepts](https://docs.morpho.org/learn/concepts/oracle/)
6. [Morpho Liquidation](https://docs.morpho.org/learn/concepts/liquidation/)
7. [Morpho Bad Debt Handling](https://docs.morpho.org/curate/tutorials-v1/bad-debt/)
8. [Morpho Contract Addresses](https://docs.morpho.org/get-started/resources/addresses/)
9. [Morpho Timelock Documentation](https://docs.morpho.org/curate/concepts/timelock/)
10. [Morpho Emergency Procedures](https://docs.morpho.org/curate/emergency/)
11. [Morpho Public Allocator](https://docs.morpho.org/curate/concepts/public-allocator/)

### Gauntlet Documentation
12. [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults)
13. [Gauntlet Curation Methodology](https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview)
14. [Gauntlet Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure)
15. [Gauntlet Security](https://www.gauntlet.xyz/vaults/security)
16. [Building Institutional-Grade Security at Gauntlet](https://www.gauntlet.xyz/resources/building-an-institutional-grade-security-posture-at-gauntlet)
17. [Gauntlet November 2025 Market Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025)

### Security & Verification
18. [Cantina Bug Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3)
19. [Immunefi Bug Bounty](https://immunefi.com/bug-bounty/morpho/)
20. [Morpho Formal Verification (Certora)](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/)
21. [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/)
22. [Morpho April 2025 Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/)
23. [Morpho Vulnerability Report (June 2023)](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM)
24. [Etherscan - Gauntlet USDC Core Vault](https://etherscan.io/address/0x8eB67A509616cd6A7c1B3c8C21D48FF57df3d458)
25. [Etherscan - Morpho Blue](https://etherscan.io/address/0xbbbbbbbbbb9cc5e90e3b3af64bdaf62c37eeffcb)

### On-Chain Data
26. [Morpho GraphQL API](https://api.morpho.org/graphql) -- Vault state, allocations, APY, timelock, roles, fee (queried June 2026)
27. [Safe Transaction Service API - Owner Multisig](https://api.safe.global/tx-service/eth/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/)
28. [Safe Transaction Service API - Guardian](https://api.safe.global/tx-service/eth/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/)
29. [Safe Transaction Service API - Curator](https://api.safe.global/tx-service/eth/api/v1/safes/0x9E33faAE38ff641094fa68c65c2cE600b3410585/)
30. [DeFiLlama Treasury API - Morpho](https://api.llama.fi/treasury/morpho)
31. [Morpho App - Gauntlet USDC Core](https://app.morpho.org/ethereum/vault/0x8eB67A509616cd6A7c1B3c8C21D48FF57df3d458/gauntlet-usdc-core)

### Resolv USR Exploit & Compensation
32. [DeFi Prime - Resolv USR Exploit](https://defiprime.com/resolv-usr-exploit)
33. [OAK Research - The Resolv (USR) Hack: Curators Face Their Responsibilities](https://oakresearch.io/en/analyses/investigations/the-resolv-usr-hack-curators-face-their-responsibilities)
34. [Resolv USR Exploit: Full Analysis](https://resolv-usr-exploit.vercel.app/)
35. [Protos - Resolv Hack Analysis](https://protos.com/resolv-hack-shows-defi-learned-nothing-from-last-contagion/)
36. [The Block - Resolv USR Depeg](https://www.theblock.co/post/394582/resolvs-usr-stablecoin-depegs-after-attacker-mints-80-million-unbacked-tokens-extracts-roughly-25-million)
37. [Gauntlet & Resolv USR Compensation Agreement (Bitget)](https://www.bitget.com/asia/amp/news/detail/12560605443387)
38. [Resolv Foundation Recovery Plan (Bitget)](https://www.bitget.com/amp/news/detail/12560605429902)

### Collateral Assets
39. [Maple - syrupUSDC on Morpho (curated by Gauntlet)](https://maple.finance/insights/syrupusdc-is-now-live-on-morpho-curated-by-gauntlet-and-mev-capital)
40. [Falcon Finance](https://falcon.finance/)

### Team, Legal & Funding
41. [Gauntlet Funding Info (Clay)](https://www.clay.com/dossier/gauntlet-funding)
42. [Morpho Legal Notice](https://morpho.org/legal-notice/)
43. [SEC LR-26266 (unrelated "Gauntlet Holdings, LLC")](https://www.sec.gov/enforcement-litigation/litigation-releases/lr-26266)
