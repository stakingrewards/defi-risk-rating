# Morpho - Gauntlet USDC Prime Vault Risk Rating

**Rating Date**: 2026-03-25
**Analyst**: DeFi Risk Auditor Agent
**Final Grade**: BB+
**Total Score**: 793.0/900 points

---

## Executive Summary

The Gauntlet USDC Prime vault (0xdd0f28e19C1780eb6396170735D45153D261490d) is a MetaMorpho V1 vault on Ethereum that lends USDC against blue-chip crypto collateral through Morpho Blue markets. Curated by Gauntlet -- one of the most established DeFi risk management firms (founded 2018, $1B+ valuation, $41.8M raised) -- the vault targets conservative, risk-adjusted yield from high-liquidity collateral markets including wstETH, cbBTC, and WBTC. With approximately $142.9M in TVL and organic yield from overcollateralized USDC lending (current net APY ~2.99%, 0% vault fee), it represents a significant curated lending vault in DeFi. Gauntlet curates 70+ vaults across multiple chains with $1.3B+ total AUM.

The vault benefits from Morpho's industry-leading smart contract security infrastructure, which includes 25+ audits from Tier-0 firms (ChainSecurity, OpenZeppelin/Spearbit, Zellic, Certora), an immutable Morpho Blue core (~600 lines of code), formal verification by Certora, and dual bug bounty programs on Cantina ($2.5M max, 459 findings) and Immunefi ($2.5M max). Gauntlet further differentiates through its institutional-grade security posture with partnerships with Hypernative (real-time monitoring), ZeroShadow (24/7 virtual SOC), Chainalysis, and SEAL Intel. Since launch in March 2024, the vault has incurred zero bad debt, including through the November 2025 liquidity stress event (where it processed $42.8M in withdrawals within 48 hours without impairment) and the March 2026 Resolv USR exploit (which impacted Gauntlet Frontier/Core vaults but explicitly did NOT affect the USDC Prime vault due to its blue-chip-only collateral mandate).

On-chain governance verification (March 2026) confirmed: the Owner is a 4-of-7 Safe multisig (0xC684..., nonce 499, Safe v1.3.0), the Guardian is a 3-of-7 Safe multisig (0x7084..., Safe v1.4.1), and the Curator is a 3-of-7 Safe multisig (0x9E33..., nonce 353, Safe v1.4.1). The vault timelock is confirmed at 604,800 seconds (7 days) via Morpho GraphQL API. Current market allocation: cbBTC/USDC ($106.2M, 74.3%), WBTC/USDC ($24.5M, 17.2%), wstETH/USDC ($12.2M, 8.5%), with average utilization ~87% across markets.

**March 2026 Re-Rating (beta framework v0.1-beta):** The beta framework introduced stricter criteria for monitoring effectiveness (S-SC-10), automated allocation risk (new ST-PM-10), comparable variant loss history (ST-PM-05), incident response automation coverage (O-TL-05), and manager loss history (O-TL-09). The March 2026 Resolv USR exploit — which caused ~$7.5M+ uncompensated bad debt in Gauntlet Frontier/Core vaults — is the primary driver of five score downgrades despite USDC Prime itself being unaffected. The vault dropped from BBB- (820.6) to BB+ (793.0). The rating remains constrained by: (1) ~91.5% wrapped asset concentration creating custodian dependency; (2) single immutable oracle per market with no fallback; (3) no dedicated loss reserve; (4) no automatic on-chain circuit breakers; and (5) no demonstrated ability to halt automated allocation mechanisms during incidents.

---

## Rating Overview

| Category | Weight | Current Score | Max Score | Current % | Potential Score | Potential % |
|----------|--------|---------------|-----------|-----------|-----------------|-------------|
| Security | 40% | 323.2 | 360 | 89.8% | 349.1 | 97.0% |
| Strategy | 30% | 235.8 | 270 | 87.3% | 256.3 | 94.9% |
| Operations | 30% | 234.0 | 270 | 86.7% | 270.0 | 100.0% |
| **Total** | **100%** | **793.0** | **900** | **88.1%** | **875.4** | **97.3%** |

**Current Grade**: BB+ (793.0/900 points)
**Potential Grade**: A+ (875.4/900 points) - achievable if all improvements made

---

## Deal Breaker Assessment

| Question Code | Deal Breaker Type | Status | Impact |
|---------------|-------------------|--------|--------|
| [S-SC-01] Audits | Category | PASS | No cap -- 25+ audits from Tier-0/1 firms |
| [S-SC-06] Exploits | Full | PASS | No cap -- No confirmed exploits with user fund loss in Gauntlet USDC Prime vault |
| [S-SC-07] Rug Pull | Full | PASS | No cap -- No rug pull events |
| [S-KM-02] Single Key Control | Category | PASS | No cap -- Multisig + timelock required |
| [ST-PM-05] Strategy Losses | Category | PASS (Mid) | No cap triggered -- scored Mid (3) due to comparable variant (Gauntlet Frontier) experiencing uncompensated losses. Root cause (USR collateral) structurally excluded from Prime mandate. Deal breaker only triggers on High (1). |
| [ST-PC-05] Third Party Disclosure | Category | PASS | No cap -- Pure on-chain lending, no third-party custodians |
| [O-TL-04] Regulatory Actions | Category | PASS | No cap -- No enforcement actions against Gauntlet Networks Inc. |
| [O-DT-05] Proof of Reserves | Category | PASS | No cap -- Full on-chain transparency |

**Deal Breaker Summary**: No deal breakers triggered. The vault passes all critical safety checks. Notably, the March 2026 Resolv USR exploit impacted Gauntlet Frontier/Core vaults but the USDC Prime vault was completely unaffected due to its blue-chip-only collateral mandate.

---

## Improvement Summary

| Classification | Count | Current Points Gap | Potential Points Gain |
|----------------|-------|--------------------|-----------------------|
| Improvable | 9 | -56 | +56 |
| Source Missing | 2 | -14 | +14 |
| Non-Improvable | 5 | -30 | 0 |
| Already Optimal | 66 | 0 | 0 |
| N/A | 2 | 0 | 0 |

**Top Improvement Opportunities:**

1. **Publish Comprehensive Incident Playbook** [S-KM-08]: Current 3, Potential 9 (+15.0 weighted points) -- Improvable
2. **Connect Monitoring to Automated Protections** [S-SC-10]: Current 3, Potential 9 (+10.9 weighted points) -- Improvable
3. **Disclose and Build Treasury Reserve** [O-FR-02]: Current 1, Potential 9 (+10.8 weighted points) -- Source Missing / Improvable
4. **Reduce Wrapped Asset Concentration** [ST-C-04]: Current 1, Potential 9 (+10.0 weighted points) -- Improvable
5. **Establish Dedicated Safety Module** [O-FR-01]: Current 3, Potential 9 (+8.1 weighted points) -- Improvable
6. **Add Circuit Breakers to Automated Allocation** [ST-PM-10]: Current 3, Potential 9 (+6.7 weighted points) -- Improvable (new question in beta framework)
7. **Demonstrate Clean Comparable-Variant Track Record** [ST-PM-05]: Current 3, Potential 9 (+6.7 weighted points) -- Improvable (requires 24 months clean + addressing Frontier losses)
8. **Document Procedures to Halt Automated Allocation** [O-TL-05]: Current 3, Potential 9 (+5.0 weighted points) -- Improvable
9. **Demonstrate Clean Manager Track Record** [O-TL-09]: Current 3, Potential 9 (+5.0 weighted points) -- Improvable
10. **Publish Conflict-of-Interest Policy** [O-TL-08]: Current 3, Potential 9 (+5.0 weighted points) -- Improvable

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 323.2/360 (89.8%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 25+ audits from Tier-0/1 firms including ChainSecurity, Spearbit/OpenZeppelin, Zellic, Certora, Blackthorn, plus Cantina competition. Both Morpho Blue core and MetaMorpho/Vaults V2 framework extensively audited. Formal verification by Certora with mathematical proofs. The Gauntlet USDC Prime vault (0xdd0f...) is a MetaMorpho V1 vault deployed via the audited MetaMorpho factory. All core contracts holding user funds are covered. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/), [P1] [GitHub metamorpho](https://github.com/morpho-org/metamorpho) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | December 2025: Certora (Tier-0), Spearbit (Tier-0 via Cantina), Blackthorn for Vaults V2 MarketV1AdapterV2. September 2025: ChainSecurity (Tier-0) for Vaults V2 core. Multiple Tier-0 auditors for most recent work. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable (~600 LOC). Every vault upgrade in last 12 months (Vaults V2 Sep-Dec 2025) was preceded by multiple audits from Tier-0 firms. The V2 launch included 8+ separate audit engagements. The Gauntlet USDC Prime vault on Ethereum is a V1 vault (non-upgradeable). | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [Vault V1 Docs](https://docs.morpho.org/learn/concepts/vault/) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 vulnerability patched immediately with OpenZeppelin. Certora formal verification provides mathematical proof of critical invariants. All V2 audit findings resolved before deployment with multiple re-reviews. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue core is immutable. MetaMorpho V1 vault (0xdd0f...) is a non-upgradeable ERC4626 contract deployed March 2024. Market changes require Curator + timelock + Guardian approval. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vault V1 Docs](https://docs.morpho.org/learn/concepts/vault/), [P0] [Etherscan](https://etherscan.io/address/0xdd0f28e19C1780eb6396170735D45153D261490d) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No exploit or bug in Morpho Blue or MetaMorpho smart contracts has caused user fund loss. This is a smart contract security question — the Morpho protocol contracts worked exactly as designed in every incident. Key distinction: the March 2026 Resolv USR exploit (~$25M across DeFi, ~$7.5M+ in Gauntlet Frontier/Core vaults) was an external token failure (USR depeg), NOT a Morpho smart contract exploit. Morpho liquidations fired correctly, bad debt was socialized per protocol spec. USDC Prime had zero USR exposure (blue-chip-only mandate). The Resolv impact on Gauntlet as a manager entity is captured separately in ST-PM-05 (comparable variant losses), O-TL-09 (manager loss history), and ST-PM-10 (automated allocation risk). Other incidents: April 2025 frontend vulnerability ($2.6M) intercepted by white hat, all funds returned in minutes (frontend issue, not contract exploit). October 2024 oracle exploit ($230K) affected only PAXG/USDC market. November 2025 MEV Capital bad debt (3.6%) — separate curator, separate vault. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P4] [Cointelegraph](https://cointelegraph.com/news/white-hat-intercepts-2-million-morpho-blue-hack), [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho operates as ADDMO, a French nonprofit association. Gauntlet Networks Inc. is a well-funded ($41.8M raised, $1B valuation) US-based company with public leadership. No credible allegations against either entity. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P2] [Gauntlet About](https://www.gauntlet.xyz/about) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No evidence of timelock reductions. The Gauntlet USDC Prime vault has a confirmed 7-day timelock (604,800 seconds), verified via Morpho GraphQL API (March 2026). No reductions have occurred since vault deployment in March 2024. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=604800), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Morpho runs dual active public bounties: (1) Cantina with $2.5M max payout for critical vulnerabilities, 459 findings submitted since March 2024, scope covers V1 and V2 contracts plus web apps; (2) Immunefi with $2.5M max payout for Morpho Blue, $1.5M for MetaMorpho/periphery. Both are Tier-0 platforms. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3), [P1] [Immunefi Bounty](https://immunefi.com/bug-bounty/morpho/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Gauntlet partners with Hypernative (real-time monitoring), ZeroShadow (24/7 vSOC), Chainalysis, and SEAL Intel. Morpho runs internal monitoring bots. However, per beta framework verification principle: monitoring exists but cannot automatically trigger protective actions — no on-chain circuit breakers, no automated pause capability. During March 2026 Resolv exploit, the Public Allocator on Frontier vaults continued auto-supplying capital to broken markets for hours post-exploit, demonstrating that monitoring alerts are NOT connected to automated protective actions. April 2025 Morpho 4-minute response was manual human intervention. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Building Institutional Security](https://www.gauntlet.xyz/resources/building-an-institutional-grade-security-posture-at-gauntlet), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. Morpho Blue prioritizes immutability over admin controls. Guardian can manually veto pending timelocked actions but cannot pause the protocol. Market-level isolation provides containment. Gauntlet's Hypernative partnership provides automated response solutions, but these cannot pause on-chain Morpho contracts. | 3 | 3 | Non-Improvable | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |

**Smart Contract Security Subtotal: 158.2/180 (87.9%)**
- 9 questions scored 9 (sum = 81), 2 questions scored 3 (sum = 6)
- Raw sum = 87 out of max 99
- Weighted = (87/99) x 180 = 158.2

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Owner: Gnosis Safe 4-of-7 multisig (0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec), verified on-chain via Safe Transaction Service API (Safe v1.3.0, 7 distinct owner addresses, threshold=4, nonce=499). Guardian: Gnosis Safe 3-of-7 multisig (0x7084bF4dB6c21e1834dD6482f6056a39A33584cD), verified (Safe v1.4.1, nonce=3). Curator: Gnosis Safe 3-of-7 multisig (0x9E33faAE38ff641094fa68c65c2cE600b3410585), verified (Safe v1.4.1, nonce=353). Timelock: 604,800 seconds (7 days), confirmed via Morpho GraphQL API. All changes visible on-chain with 7-day advance notice. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API Guardian](https://api.safe.global/tx-service/eth/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/), [P0] [Safe API Curator](https://api.safe.global/tx-service/eth/api/v1/safes/0x9E33faAE38ff641094fa68c65c2cE600b3410585/), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Vault contract is non-upgradeable. Moving user funds requires going through Morpho Blue immutable contract logic. Market changes require multisig + timelock + Guardian. Permissionless redemption always available via ERC4626. Owner multisig is 4-of-7 (threshold >= 3, signers >= 5). 7-day timelock confirmed. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=604800, owner threshold=4), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner multisig is 4-of-7 Safe (verified: 7 distinct owner addresses, threshold=4). This meets >=4-of-7 minimum for Low Risk. Guardian is a 3-of-7 Safe multisig. Curator is a 3-of-7 Safe multisig. Gauntlet is publicly identified as the entity operating these multisigs. Five addresses overlap across Owner/Guardian/Curator multisigs, all Gauntlet team members. Depositors have no direct veto power (no Aragon DAO equivalent). | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API Guardian](https://api.safe.global/tx-service/eth/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking capability. No pause function on Morpho Blue (immutable). Guardian can only revoke pending timelocked actions. Withdrawals always permissionless via direct smart contract interaction. Rules publicly documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets held in non-custodial Morpho Blue contracts on Ethereum. Permissionless redemption via ERC4626. No off-chain custody component. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. Vault funds are held in Morpho Blue markets, separate from any treasury or operational wallets. Performance fee accrued on-chain transparently (currently 0%). Morpho is a nonprofit with no profit extraction from protocol operations. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (fee=0), [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain enforced whitelist of Morpho Blue markets only. Current markets verified via GraphQL API: wstETH/USDC (86% LLTV), cbBTC/USDC (86% LLTV), WBTC/USDC (86% LLTV). New market additions require Curator approval + 7-day timelock + Guardian veto. Supply caps per market enforced on-chain ($200M per market). The whitelist is well-defined and aligned with the Prime mandate. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (allocation data), [P2] [Gauntlet USDC Prime Whitelisting](https://forum.morpho.org/t/gauntlet-usdc-prime-vault-whitelisting/496), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Gauntlet's institutional security posture includes partnerships with ZeroShadow (24/7 vSOC with incident triage and escalation), Hypernative (automated response), and SEAL Intel (threat intelligence). Morpho docs include emergency procedures documentation for vault curator roles. However, no public, vault-specific incident playbook with explicit key rotation procedures or tabletop exercise results has been published by Gauntlet. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Morpho Emergency Procedures](https://docs.morpho.org/curate/emergency/) |

**Key Management Subtotal: 165.0/180 (91.7%)**
- 7 questions scored 9 (sum = 63), 1 question scored 3 (sum = 3)
- Raw sum = 66 out of max 72
- Weighted = (66/72) x 180 = 165.0

---

### **Security Total: 323.2/360 (89.8%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 158.2 | 180 | 87.9% |
| Key Management | 165.0 | 180 | 91.7% |
| **Security Total** | **323.2** | **360** | **89.8%** |

---

### STRATEGY (30% Weight) -- Score: 235.8/270 (87.3%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from overcollateralized USDC lending against blue-chip crypto collateral (wstETH, cbBTC, WBTC). 100% mandate-aligned. The Prime vault mandate explicitly targets "large market cap and high liquidity collateral markets." Yield sources documented on Morpho App and Gauntlet VaultBook. Current net APY ~2.99%. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (netApy=0.0299), [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults), [P2] [Gauntlet USDC Prime Whitelisting](https://forum.morpho.org/t/gauntlet-usdc-prime-vault-whitelisting/496) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail shocks: simultaneous BTC/ETH crash exceeding the liquidation buffer (86% LLTV provides ~14% buffer), oracle manipulation on immutable oracle, or catastrophic wrapped-asset custodian failure. Bad debt per market is isolated and socialized among lenders of that specific market. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault simply lends USDC. No rehypothecation of depositor funds. Effective leverage: 1.0x. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | USDC Prime vault itself has zero bad debt since March 2024. However, per beta framework "comparable variant" guidance ("same codebase with parameter changes only = comparable"), Gauntlet USDC Frontier IS a comparable variant — same MetaMorpho V1 codebase, same Morpho Blue protocol, same curator, same deposited asset (USDC), differing only in collateral parameters. Frontier experienced confirmed bad debt (~$7.5M+) during March 2026 Resolv USR exploit, and losses were socialized to lenders (uncompensated). The root cause (USR collateral) is structurally excluded from Prime's blue-chip mandate, but the framework evaluates the strategy type. November 2025: zero bad debt across all Gauntlet vaults. | 3 | 9 | **Improvable** | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Gauntlet publishes comprehensive curation methodology via VaultBook, including risk factor overviews, due diligence processes, and market allocation strategy. Quantitative limits for insolvency risk (targeting <10 bps of TVL). Clear tiering system (Prime/Balanced/Frontier). Agent-based simulation models inform allocation decisions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults), [P1] [Curation Methodology](https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. Yield is entirely organic from USDC lending demand. No emissions or token incentives required for base yield. Current net APY approximately 2.99% (March 2026, vault fee 0%). Coinbase crypto-backed loans partnership drives sustainable demand. APY varies with market conditions; was ~9% during higher utilization periods. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (netApy=0.0299, fee=0), [P1] [Gauntlet VaultBook Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes. USDC is the most liquid stablecoin. During November 2025 stress, Gauntlet USDC Prime vault maintained average ~53% supply available for immediate withdrawal, and processed 40% of TVL in withdrawals within 48 hours. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. Pure lending interest from overcollateralized borrower demand. No basis trade, peg arbitrage, or funding rate dependency. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Yes. Gauntlet uses automated allocation models for continuous rebalancing across whitelisted markets. Supply caps ($200M per market) limit maximum per-market exposure, but no automatic kill-switch exists for abnormal conditions (oracle deviation, collateral depeg, utilization spikes). During March 2026 Resolv exploit, the Public Allocator on Frontier vaults auto-supplied $6.2M in USDC to broken markets for hours post-exploit because anyone could invoke the function and no circuit breaker halted it. While Prime's markets were unaffected, the same automated allocation infrastructure applies. Halting requires manual curator intervention (setting caps to zero). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (allocation data), [P1] [Morpho Public Allocator](https://docs.morpho.org/curate/concepts/public-allocator/), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |

**Protocol Mechanics Subtotal: 38.3/45 (85.2%)**
- 9 applicable questions (ST-PM-04 = N/A), 7 scored 9 (sum = 63), 2 scored 3 (sum = 6)
- Raw sum = 69 out of max 81
- Weighted = (69/81) x 45 = 38.3

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Blue-chip only: wstETH (Lido, largest LST, BBB+ SR rating), cbBTC (Coinbase custody, NY DFS regulated), WBTC (BitGo/BiT Global). All established, high-market-cap assets. Gauntlet performs rigorous due diligence on collateral quality. Risk tiering applied per market. All LLTVs at 86%. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (market allocations), [P2] [Gauntlet USDC Prime Whitelisting](https://forum.morpho.org/t/gauntlet-usdc-prime-vault-whitelisting/496) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | cbBTC: No depeg >2% since September 2024 launch. WBTC: Brief depegs during historical events, all recovered within 24h. wstETH: Stable tracking of stETH/ETH ratio throughout stress events. No collateral showed >2% depeg lasting >24h in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P3] Market data, [P0] On-chain price history |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Only wstETH has staking exposure ($12.2M, ~8.5% of TVL). Lido uses 30+ diversified operators across multiple jurisdictions. Lido slashing insurance/coverage fund absorbs minor events. Minimal vault-level exposure. | 9 | 9 | Non-Improvable (optimal) | [P3] Lido operator data |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | HIGH RISK: Approximately 91.5% of vault TVL is in wrapped BTC assets (cbBTC $106.2M + WBTC $24.5M = $130.7M out of $142.9M total). cbBTC is custodied by Coinbase (NY DFS regulated). WBTC involves BiT Global/Justin Sun governance concerns. Exceeds 60% threshold significantly. | 1 | 9 | **Improvable** | [P0] Morpho GraphQL API (allocation: cbBTC $106.2M, WBTC $24.5M, wstETH $12.2M) |

**Collateral Subtotal: 35.0/45 (77.8%)**
- 3 questions scored 9 (sum = 27), 1 question scored 1
- Raw sum = 28 out of max 36
- Weighted = (28/36) x 45 = 35.0

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | All Tier-0/1: Ethereum (Tier-0 chain), Chainlink (Tier-0 oracle). No bridges. No CEX dependency for operations. All dependencies explicitly identifiable. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant are oracle and bridge setups, and can oracle values be corrected under abnormal conditions? | **Hardcoded oracle check (beta framework mandatory):** Each Morpho Blue market uses an immutable oracle that cannot be updated, overridden, or corrected post-deployment. Can the priced collateral depeg? cbBTC (custodial, Coinbase) and WBTC (custodial, BitGo/BiT Global) are wrapped custodial assets that can theoretically depeg if the custodian fails. Both are deep-liquidity assets with significant market history (WBTC since 2019, cbBTC since September 2024). Scored Mid (3) under "hardcoded oracle used only for battle-tested deep-liquidity assets where material depeg is historically unprecedented" — but this is a borderline call given that cbBTC has only ~18 months of history and WBTC had BiT Global/Justin Sun governance concerns. No fallback oracle exists for any market — a permanent Morpho Blue design limitation. The Resolv exploit demonstrated this exact attack vector (depegged collateral + immutable oracle = unbounded borrowing against stale price), validating the risk — though USR was a novel, untested token unlike the blue-chip collateral in Prime. | 3 | 3 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Gauntlet claims "institutional-grade security posture" and partnerships with Hypernative, ZeroShadow, Chainalysis, and SEAL Intel. However, no explicit SOC 2 Type II or ISO27001 certification for Gauntlet Networks Inc. has been publicly disclosed. Web search found no evidence of such certifications. Chainlink and Coinbase (cbBTC custodian) hold enterprise certifications. | 3 | 9 | **Source Missing** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Ethereum: No significant halts. Morpho: April 2025 frontend issue resolved in 4 minutes. November 2025: Gauntlet vaults operated correctly with zero bad debt and 53% average withdrawable liquidity. March 2026 Resolv exploit: USDC Prime unaffected, demonstrating effective risk isolation. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain halts >30 minutes in the last 12+ months. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Only relevant for wstETH (~8.5% of TVL). Lido slashing events trivial and fully absorbed by coverage fund. No depositor impact. | 9 | 9 | Non-Improvable (optimal) | [P3] Lido slashing data |
| ST-IC-07 | Are validators diverse geographically and by operator? | Ethereum validator set highly distributed. Lido (wstETH collateral) uses 30+ independent operators across multiple jurisdictions. No single operator >33%. | 9 | 9 | Non-Improvable (optimal) | [P3] Ethereum validator data |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Permissionless on-chain redemption always available via ERC4626. No off-chain dependency for withdrawals. Oracle failure would prevent new borrows/liquidations on affected market but would not block existing withdrawals from the vault. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Infrastructure Counterparty Subtotal: 37.5/45 (83.3%)**
- 6 questions scored 9 (sum = 54), 2 questions scored 3 (sum = 6)
- Raw sum = 60 out of max 72
- Weighted = (60/72) x 45 = 37.5

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All allocation to Morpho Blue markets only (Tier-0 protocol). No CEX or RWA exposure. Three active markets: wstETH/USDC, cbBTC/USDC, WBTC/USDC. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (allocation data), [P2] [Gauntlet USDC Prime Whitelisting](https://forum.morpho.org/t/gauntlet-usdc-prime-vault-whitelisting/496) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Yes. Performance fee clearly documented (currently 0%) and verified on-chain via Morpho GraphQL API. No hidden rebates found. Coinbase partnership (cbBTC) is public. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (fee=0), [P1] [Incentives & Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. On-chain supply caps per market ($200M each, verified via GraphQL API). Gauntlet's automated risk models perform daily optimization and continuous rebalancing within caps. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (supplyCap per market), [P1] [Market Allocation Strategy](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/curation-methodology-and-risk-factor-overview/market-allocation-strategy) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Lending positions unwound as borrowers repay. November 2025 demonstrated $42.8M (~40% TVL) processed within 48 hours. No discretionary approvals needed. Rate spikes during high utilization incentivize rapid repayment. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending. No external validators, custodians, or asset managers involved in vault operations. Gauntlet (curator) clearly identified. Underlying collateral custodians (Coinbase for cbBTC, BitGo/BiT Global for WBTC) are publicly known. | 9 | 9 | Non-Improvable (optimal) | Vault architecture |

**Protocol Counterparty Subtotal: 45.0/45 (100.0%)**
- 5 questions, all scored 9
- Raw sum = 45 out of max 45
- Weighted = (45/45) x 45 = 45.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain redemption via ERC4626. No address-level blocking. No admin pause function. Withdrawal depends on market liquidity (idle USDC in markets). | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Moderate. Average ~53% available for immediate withdrawal during November 2025 stress. $42.8M (~40% TVL) processed within 48 hours. Rate spikes incentivize repayment but instant 100% exit not guaranteed during high utilization. Current average utilization ~87% across markets means ~13% immediately available. | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API (utilization ~87%), [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | Gauntlet USDC Prime demonstrated strong performance during November 2025 stress. Average 53% withdrawable liquidity. $42.8M processed within 48 hours without impairment. No prolonged freezes. >95% of withdrawals completed promptly over 12-month period. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Caps appropriately sized ($200M per market). Gauntlet's risk models actively manage supply-to-market ratios to ensure withdrawal liquidity. During November 2025, delays were driven by utilization, not cap design. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (supplyCap=$200M per market), [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Battle-tested during November 2025 stress. Gauntlet USDC Prime maintained average 53% withdrawable liquidity while other curated vaults fell by >60%. Conditions normalized within days. Also unaffected during March 2026 Resolv USR crisis. Demonstrated resilience across two significant stress events. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure USDC lending with no lockups, vesting, or bridge dependencies. Withdrawal speed limited only by market utilization. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary redemption through ERC4626 vault always available. Secondary market not required for exit. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | High. USDC is the most liquid stablecoin. gtUSDC vault shares are 1:1 backed by vault assets ($142.9M TVL). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (totalAssetsUsd=$142.9M) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Moderate. Bank run causes temporary queues and rate spikes but unlikely permanent losses. Market isolation contains risk. November 2025 demonstrated zero permanent losses and 53% average withdrawable liquidity during actual stress. Utilization-based interest rate curves create strong repayment incentives. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |

**Liquidity Subtotal: 35.0/45 (77.8%)**
- 6 questions scored 9 (sum = 54), 3 questions scored 3 (sum = 9)
- Raw sum = 63 out of max 81
- Weighted = (63/81) x 45 = 35.0

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | gtUSDC vault shares represent 1:1 USDC claim plus accrued yield. No depeg history. During November 2025 stress and March 2026 Resolv crisis, vault share value remained stable. ERC4626 standard ensures NAV-based redemption. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Very low. Vault lends USDC -- dollar-denominated. No directional BTC/ETH exposure for lenders. Risk is limited to bad debt from borrower defaults, which requires collateral values to drop beyond the 14% liquidation buffer (~86% LLTV). | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Immutable Adaptive Curve IRM per market. During November 2025, elevated rates attracted additional supply, demonstrating resilience. No history of prolonged >=95% utilization on Prime vault markets. Current utilization ~87% with healthy rate dynamics. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (utilization data), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. Gauntlet uses agent-based simulations modeling market scenarios. Risk framework targets insolvent debt <10 bps of TVL in extreme scenarios. Certora formally verified liquidation mechanics. Gauntlet monitors cross-protocol leveraged positions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side only. Vault lenders benefit from liquidations (no loss to lenders unless bad debt occurs). Gauntlet's real-time monitoring of cross-protocol positions helps anticipate cascades. 14% buffer (86% LLTV) provides substantial margin. | 9 | 9 | Non-Improvable (optimal) | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 45.0/45 (100.0%)**
- 5 questions, all scored 9
- Raw sum = 45 out of max 45
- Weighted = (45/45) x 45 = 45.0

---

### **Strategy Total: 235.8/270 (87.3%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 38.3 | 45 | 85.2% |
| Collateral | 35.0 | 45 | 77.8% |
| Infra Counterparty | 37.5 | 45 | 83.3% |
| Protocol Counterparty | 45.0 | 45 | 100.0% |
| Liquidity | 35.0 | 45 | 77.8% |
| Market | 45.0 | 45 | 100.0% |
| **Strategy Total** | **235.8** | **270** | **87.3%** |

---

### OPERATIONS (30% Weight) -- Score: 234.0/270 (86.7%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid with strong checks. Morpho Blue immutable. Vault changes require Owner multisig (4-of-7) + 7-day timelock + Guardian (3-of-7) veto. Multiple layers prevent unilateral changes. No single entity can unilaterally change core logic. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock, owner, guardian), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- No governance token voting for this vault. Vault controlled by multisig + Guardian, not token-holder governance. Governance concentration captured in S-KM-01 and S-KM-03. | N/A | N/A | N/A | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. The vault has a confirmed 7-day timelock (604,800 seconds), verified via Morpho GraphQL API (March 2026). This far exceeds the 24-hour minimum for Low Risk. The Guardian (3-of-7 Safe multisig) can veto pending changes during the 7-day window. All pending actions visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=604800), [P0] [Safe API Guardian](https://api.safe.global/tx-service/eth/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner can appoint new Curator (subject to 7-day timelock). Withdrawals remain permissionless throughout via ERC4626. Transition fully transparent on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 3 questions scored 9 (sum = 27); O-G-02 = N/A
- Raw sum = 27 out of max 27
- Weighted = (27/27) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Gauntlet: Tarun Chitra (CEO/Co-founder, former D.E. Shaw Research, HFT background), Rei Chiang (Co-founder). 50+ team. Morpho: Paul Frambot (CEO). All publicly identified with verifiable track records. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Team](https://www.gauntlet.xyz/our-team), [P1] [Morpho](https://morpho.org/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Gauntlet has 50+ employees across 3 continents. Morpho has a separate full team ($73.6M raised). Multiple independent parties capable of vault operations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet About](https://www.gauntlet.xyz/about) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Morpho: ADDMO (French nonprofit, Paris) + Morpho Labs SAS (France). Gauntlet: Gauntlet Networks Inc. (New York, USA). Both clearly identified with appropriate legal structures. Note: SEC action against unrelated "Gauntlet Holdings, LLC" has no connection to Gauntlet Networks Inc. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P1] [Gauntlet](https://www.gauntlet.xyz/) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known actions against Gauntlet Networks Inc. or Morpho entities. The SEC enforcement against "Gauntlet Holdings, LLC" (LR-26266) involves a completely different entity -- confirmed by different jurisdiction and business type. | 9 | 9 | Non-Improvable (optimal) | [P0] [SEC LR-26266](https://www.sec.gov/enforcement-litigation/litigation-releases/lr-26266), Public records |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Gauntlet has 24/7 on-call with ZeroShadow (vSOC), Hypernative, and SEAL Intel partnerships. Morpho demonstrated 4-minute response April 2025. However, per beta framework: incident response MUST include documented procedures to halt automated allocation mechanisms. During March 2026 Resolv exploit, the Public Allocator on Frontier vaults continued auto-supplying capital to broken markets for hours post-exploit — demonstrating that incident response procedures did NOT cover halting automated allocation within SLA. Same automated infrastructure applies to Prime vault. Formal on-call exists but does not cover halting automated allocation mechanisms within 1 hour. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Building Institutional Security](https://www.gauntlet.xyz/resources/building-an-institutional-grade-security-posture-at-gauntlet), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Gauntlet published detailed market report within days of November 2025 stress. Active VaultBook documentation. Morpho's 4-minute response in April 2025. Gauntlet communicated quickly during March 2026 Resolv crisis ("majority of vaults unaffected"). | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Gauntlet: $41.8M from Polychain, Paradigm, Ribbit Capital ($1B valuation). Morpho: a16z, Variant, Pantera, Coinbase Ventures ($73.6M, 29 investors). All disclosed with roles and influence clear. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay](https://www.clay.com/dossier/gauntlet-funding), [P4] [Tracxn](https://tracxn.com/d/companies/morpho/__5iKpzjF_-EXELsu5bJ6cORHuQN7HD3ItPqKPexS2FVw) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Gauntlet manages 70+ vaults with $1.3B+ AUM across multiple chains and risk tiers (Prime/Balanced/Frontier). Structural mitigations exist: tiered risk system, automated allocation models, published VaultBook. However, the March 2026 Resolv incident raised questions about cross-vault risk management. Formal quantitative conflict-of-interest policy not published. | 3 | 9 | **Improvable** | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults), [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | March 2026 Resolv USR exploit caused confirmed bad debt in Gauntlet-curated Frontier and Core vaults (~$7.5M+ exposure). While USDC Prime specifically had zero losses (blue-chip-only mandate, no USR exposure), the framework evaluates the **manager entity** -- Gauntlet is linked to uncompensated depositor losses in products they curate. This constitutes "one historical loss incident with limited impact" followed by demonstrable risk isolation (tiered system worked). Prior Aave advisory role (2020-2024) saw $1.6M CRV bad debt but Gauntlet was advisor, not curator. | 3 | 9 | **Improvable** | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |

**Team & Legal Subtotal: 52.5/67.5 (77.8%)**
- 6 questions scored 9 (sum = 54), 3 questions scored 3 (sum = 9)
- Raw sum = 63 out of max 81
- Weighted = (63/81) x 67.5 = 52.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive documentation from Morpho (docs.morpho.org) and Gauntlet (VaultBook with detailed curation methodology, risk factors, market allocation strategy). Updated regularly -- Gauntlet published $775M supply event report Feb 2026. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Docs](https://docs.morpho.org/), [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Detailed documentation of liquidation mechanics, bad debt scenarios, oracle risks, and loss conditions across Morpho docs and Gauntlet VaultBook. Bad debt socialization mechanics clearly explained. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Morpho docs maintain canonical address registry. Vault address clearly identified on Morpho App and Gauntlet App. All contracts Etherscan-verified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Comprehensive documentation of vault roles (Owner, Curator, Guardian, Allocator) with detailed permission descriptions. Timelock mechanics documented. Changes visible on-chain via Safe transaction history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves. All allocations visible on Morpho App, Gauntlet App, and Etherscan. Morpho GraphQL API provides programmatic access to all vault state including allocations, utilization, and TVL. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xdd0f28e19C1780eb6396170735D45153D261490d), [P0] Morpho GraphQL API |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. All core contracts verified on Etherscan. Full source code readable. Morpho Blue (0xBBBB...) and vault contract (0xdd0f...) both fully verified. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xdd0f28e19C1780eb6396170735D45153D261490d) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions, all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated safety module for this vault. Bad debt socialized per market among lenders. Morpho DAO treasury (~$33.8M, mostly MORPHO tokens) is discretionary via governance. No Gauntlet-specific backstop fund. No binding activation rules for loss coverage. | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Insufficient. Morpho DAO treasury ~$33.8M across Ethereum ($11.4M) and Base ($22.4M), consisting entirely of MORPHO tokens (no stablecoins). Against ~$10B+ protocol-wide TVL this represents ~0.34%. Against vault TVL ($142.9M) it represents ~23.7%, but it is NOT ring-fenced for this vault and is entirely in volatile native tokens. Gauntlet is well-funded ($41.8M raised, $1B valuation) but no vault-specific reserve disclosed. | 1 | 9 | **Source Missing** | [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho), [P0] [DeFiLlama Treasury Adapter](https://raw.githubusercontent.com/DefiLlama/DefiLlama-Adapters/refs/heads/main/projects/treasury/morpho.js) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Gauntlet: $41.8M raised, $1B valuation, profitable since 2021 per public claims. Morpho: $73.6M raised. Both have sustainable revenue streams. Combined runway >24 months. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay](https://www.clay.com/dossier/gauntlet-funding), [P1] [Gauntlet $1B Valuation](https://www.gauntlet.xyz/resources/announcing-our-1-billion-valuation-and-next-steps-for-the-gauntlet-platform) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Resilient. November 2025: Gauntlet USDC Prime maintained TVL >$130M while others fell >60%. Zero bad debt. Revenue model continued. March 2026: Prime vault unaffected by Resolv crisis. Current TVL $142.9M shows continued growth. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (totalAssetsUsd=$142.9M), [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue is immutable. Permissionless withdrawals via ERC4626. No proprietary off-chain services required for core operations. If Gauntlet disappeared, existing allocations continue and users can withdraw freely. No curation would occur but funds remain safe. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Financial Resilience Subtotal: 46.5/67.5 (68.9%)**
- 3 questions scored 9 (sum = 27), 1 question scored 3, 1 question scored 1
- Raw sum = 31 out of max 45
- Weighted = (31/45) x 67.5 = 46.5

---

### **Operations Total: 234.0/270 (86.7%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 67.5 | 67.5 | 100.0% |
| Team & Legal | 52.5 | 67.5 | 77.8% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 46.5 | 67.5 | 68.9% |
| **Operations Total** | **234.0** | **270** | **86.7%** |

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 87 | 99 | 158.2 | 180 | 87.9% |
| | Key Management (8 Q) | 66 | 72 | 165.0 | 180 | 91.7% |
| | **Security Subtotal** | | | **323.2** | **360** | **89.8%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 69 | 81 | 38.3 | 45 | 85.2% |
| | Collateral (4 Q) | 28 | 36 | 35.0 | 45 | 77.8% |
| | Infra Counterparty (8 Q) | 60 | 72 | 37.5 | 45 | 83.3% |
| | Protocol Counterparty (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity (9 Q) | 63 | 81 | 35.0 | 45 | 77.8% |
| | Market (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | **Strategy Subtotal** | | | **235.8** | **270** | **87.3%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 63 | 81 | 52.5 | 67.5 | 77.8% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 31 | 45 | 46.5 | 67.5 | 68.9% |
| | **Operations Subtotal** | | | **234.0** | **270** | **86.7%** |
| **TOTAL** | | | | **793.0** | **900** | **88.1%** |

---

## Validation Checklist

- [x] Smart Contract Security: (9x9 + 2x3) = 81+6 = 87/99; (87/99)*180 = 158.18 ~ 158.2 (verified)
- [x] Key Management: (7x9 + 1x3) = 63+3 = 66/72; (66/72)*180 = 165.0 (verified)
- [x] Security Total: 158.2 + 165.0 = 323.2 (verified)
- [x] Protocol Mechanics: (7x9 + 2x3) = 63+6 = 69/81; (69/81)*45 = 38.33 ~ 38.3 (1 N/A, ST-PM-10 new) (verified)
- [x] Collateral: (3x9 + 1x1) = 27+1 = 28/36; (28/36)*45 = 35.0 (verified)
- [x] Infra Counterparty: (6x9 + 2x3) = 54+6 = 60/72; (60/72)*45 = 37.5 (verified)
- [x] Protocol Counterparty: (5x9) = 45/45; (45/45)*45 = 45.0 (verified)
- [x] Liquidity: (6x9 + 3x3) = 54+9 = 63/81; (63/81)*45 = 35.0 (verified)
- [x] Market: (5x9) = 45/45; (45/45)*45 = 45.0 (verified)
- [x] Strategy Total: 38.3 + 35.0 + 37.5 + 45.0 + 35.0 + 45.0 = 235.8 (verified)
- [x] Governance: (3x9) = 27/27; (27/27)*67.5 = 67.5 (1 N/A) (verified)
- [x] Team & Legal: (6x9 + 3x3) = 54+9 = 63/81; (63/81)*67.5 = 52.5 (verified)
- [x] Documentation: (6x9) = 54/54; (54/54)*67.5 = 67.5 (verified)
- [x] Financial Resilience: (3x9 + 1x3 + 1x1) = 27+3+1 = 31/45; (31/45)*67.5 = 46.5 (verified)
- [x] Operations Total: 67.5 + 52.5 + 67.5 + 46.5 = 234.0 (verified)
- [x] Grand Total: 323.2 + 235.8 + 234.0 = 793.0 (verified)
- [x] All percentages <= 100% (verified)
- [x] Rating Overview table matches Final Score Calculation (verified)
- [x] BB+ range: 785-810; 793.0 falls within BB+ (verified)
- [x] Potential: 349.1 + 256.3 + 270.0 = 875.4; A+ range: 870-876 (verified)

---

## Rating Determination

| Grade | Range | This Vault |
|-------|-------|------------|
| BBB- | 810-822 | - |
| **BB+** | **785-810** | **793.0 points** |
| BB | 760-785 | - |

## **FINAL RATING: BB+**

*Speculative -- Outcomes depend on favourable conditions and active management. Lowest risk within speculative grade.*

---

## Key Risks

1. **Wrapped Asset Concentration (~91.5%)**: cbBTC ($106.2M) and WBTC ($24.5M) together represent ~91.5% of vault TVL, creating significant custodian dependency on Coinbase (NY DFS regulated) and BitGo/BiT Global -- [P0] Morpho GraphQL API allocation data

2. **Single Oracle Per Market (Non-Improvable)**: Each Morpho Blue market has one immutable oracle with no fallback mechanism. Oracle failure or manipulation requires deploying an entirely new market -- a permanent design choice in Morpho Blue's architecture -- [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/)

3. **No Dedicated Loss Reserve**: Bad debt is socialized among lenders per market with no ring-fenced backstop. Morpho DAO treasury (~$33.8M) consists entirely of volatile MORPHO tokens and represents <0.34% of protocol-wide TVL -- [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho)

4. **Cross-Vault Curator Risk**: While USDC Prime was unaffected by the March 2026 Resolv exploit, the incident demonstrated that Gauntlet's monitoring and automated allocation systems can fail in higher-risk vaults (~$7.5M+ exposure across Frontier/Core vaults). No formal quantitative conflict-of-interest policy is published despite managing 70+ vaults -- [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit)

5. **No Automatic Circuit Breakers (Non-Improvable)**: Protocol prioritizes immutability over admin intervention capabilities. No on-chain pause or circuit breaker exists -- [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/)

---

## Improvement Roadmap

### Quick Wins (High Impact, Low Effort)

1. **Publish Conflict-of-Interest Policy** [O-TL-08] -- Current: 3, Potential: 9 (+5.0 weighted points)
   - Formalize quantitative allocation rules and independent oversight across Gauntlet's 70+ vaults

2. **Document Procedures to Halt Automated Allocation** [O-TL-05] -- Current: 3, Potential: 9 (+5.0 weighted points)
   - Publish incident runbooks with explicit steps to halt Public Allocator and automated rebalancing within 15-minute SLA

3. **Connect Monitoring to Automated Protections** [S-SC-10] -- Current: 3, Potential: 9 (+10.9 weighted points)
   - Integrate Hypernative alerts with automated halt mechanisms for capital flows during anomalous conditions

### Medium-Term Improvements (High Impact, Moderate Effort)

4. **Publish Comprehensive Incident Playbook** [S-KM-08] -- Current: 3, Potential: 9 (+15.0 weighted points)
   - Document key rotation procedures, conduct full tabletop exercise, publish results

5. **Diversify Collateral Exposure** [ST-C-04] -- Current: 1, Potential: 9 (+10.0 weighted points)
   - Reduce wrapped asset concentration below 60% by adding more native ETH collateral markets

6. **Establish Dedicated Safety Module** [O-FR-01] -- Current: 3, Potential: 9 (+8.1 weighted points)
   - Create ring-fenced backstop with binding activation rules for bad debt coverage

7. **Build/Disclose Reserve** [O-FR-02] -- Current: 1, Potential: 9 (+10.8 weighted points)
   - Establish liquid reserve >= 5% of vault TVL with diversified holdings including stablecoins

8. **Add Circuit Breakers to Automated Allocation** [ST-PM-10] -- Current: 3, Potential: 9 (+6.7 weighted points)
   - Implement on-chain circuit breakers that halt automated allocation when anomalous conditions detected (oracle deviation, collateral depeg)

### Time-Dependent Improvements

9. **Demonstrate Clean Comparable-Variant Track Record** [ST-PM-05] -- Current: 3, Potential: 9 (+6.7 weighted points)
   - Requires 24 months without further losses in comparable Gauntlet-curated USDC vaults + addressing Frontier losses

10. **Demonstrate Clean Manager Track Record** [O-TL-09] -- Current: 3, Potential: 9 (+5.0 weighted points)
   - Requires 24-36 months without further incidents across all Gauntlet-curated products

### Long-Term Structural Changes (Non-Improvable)

- **Oracle Redundancy** [ST-IC-02]: Current 3, Potential 3 -- Requires Morpho protocol redesign (immutable architecture)
- **Liquidity During Stress** [ST-L-02, ST-L-05, ST-L-09]: Current 3 each -- Inherent to lending design
- **Automatic Circuit Breakers** [S-SC-11]: Current 3 -- Morpho's design philosophy prioritizes immutability

### Evidence Gaps (Source Missing Items)

11. **Obtain/Disclose SOC 2 Certification** [ST-IC-03] -- Current: 3, Potential: 9 (+3.75 weighted points)
   - Gauntlet Networks obtain and publish SOC 2 Type II or ISO27001 certification

**Maximum Achievable Grade:** A+ (875.4/900 points) if all improvable and source-missing items addressed

**Points to Next Grade Tier (BBB-):** 17.0 points needed to reach BBB- (810 points)

**Points to Qualified Grade Mid-Range (A-):** 53.0 points needed to reach A- (846 points)

---

## Platform Consistency Notes

This rating shares the following platform-level scores with all Morpho vault ratings, as they operate on the same Morpho Blue protocol:

**Identical Scores (Platform-Level):**
- S-SC-01 through S-SC-11: All identical (same Morpho Blue smart contract infrastructure)
- S-KM-04, S-KM-05, S-KM-06: Identical (same protocol architecture)
- All Strategy questions: Identical where same underlying mechanics apply
- O-DT-01 through O-DT-06: Identical base documentation quality
- O-FR-01, O-FR-02, O-FR-03, O-FR-05: Identical (same Morpho treasury/protocol structure)

**Gauntlet Platform Consistency (shared across Prime, Frontier V2, VaultBridge WBTC):**
- All Gauntlet vaults share the same Owner multisig (0xC684..., 4-of-7) and Curator multisig (0x9E33..., 3-of-7)
- Security score: 323.2/360 for Prime (beta framework S-SC-10 downgrade applies to all Gauntlet vaults)
- Frontier V1 Security dropped further to 308.6/360 after March 2026 Resolv exploit

**Different Scores (Vault-Specific):**
- O-G-02: Gauntlet N/A (no governance token for vault)
- O-TL-05: Gauntlet Prime 3 (beta framework requires incident response to cover automated allocation — Resolv exploit proved this was inadequate) vs previous 9
- O-TL-09: Gauntlet Prime 3 (Gauntlet as manager entity linked to Frontier/Core bad debt from Resolv exploit) vs Steakhouse 9
- S-SC-10: Gauntlet Prime 3 (beta framework verification principle — monitoring not connected to automated protections) vs previous 9
- ST-PM-05: Gauntlet Prime 3 (Frontier as comparable variant experienced uncompensated losses) vs Steakhouse 9
- ST-PM-10: Gauntlet Prime 3 (new beta framework question — automated allocation without circuit breakers)

**Score Differential vs Steakhouse USDC:**
- Gauntlet Prime: 793.0 vs Steakhouse USDC: 815.6 (-22.6 points)
- Security: 323.2 vs 334.1 (-10.9) from S-SC-10 downgrade
- Strategy: 235.8 vs 242.5 (-6.7) from ST-PM-05 and ST-PM-10
- Operations: 234.0 vs 239.0 (-5.0) from O-TL-05 and O-TL-09

**Note:** Steakhouse USDC has NOT yet been re-rated under the beta framework. When re-rated, S-SC-10, ST-PM-10, and O-TL-05 changes may also apply to Steakhouse depending on its automated allocation configuration, narrowing the gap.

---

## Smart Contract Addresses

| Role | Address | Explorer Link |
|------|---------|---------------|
| VaultContract | 0xdd0f28e19C1780eb6396170735D45153D261490d | [Etherscan](https://etherscan.io/address/0xdd0f28e19C1780eb6396170735D45153D261490d) |
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
| Treasury | 33800000 |
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
8. [Morpho Vault V1 Documentation](https://docs.morpho.org/learn/concepts/vault/)
9. [Morpho Contract Addresses](https://docs.morpho.org/get-started/resources/addresses/)
10. [Morpho Timelock Documentation](https://docs.morpho.org/curate/concepts/timelock/)
11. [Morpho Emergency Procedures](https://docs.morpho.org/curate/emergency/)

### Gauntlet Documentation
12. [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults)
13. [Gauntlet Curation Methodology](https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview)
14. [Gauntlet Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure)
15. [Gauntlet Due Diligence](https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview/due-diligence)
16. [Gauntlet Market Allocation Strategy](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/curation-methodology-and-risk-factor-overview/market-allocation-strategy)
17. [Gauntlet Incentives & Performance Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees)
18. [Gauntlet Security](https://www.gauntlet.xyz/vaults/security)
19. [Building Institutional-Grade Security at Gauntlet](https://www.gauntlet.xyz/resources/building-an-institutional-grade-security-posture-at-gauntlet)
20. [Sustainable APYs at Scale](https://www.gauntlet.xyz/resources/sustainable-apys-at-scale-how-gauntlets-active-curation-on-morpho-handled-a-775-million-supply-event)
21. [Gauntlet November 2025 Market Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025)

### Security & Verification
22. [Cantina Bug Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3)
23. [Immunefi Bug Bounty](https://immunefi.com/bug-bounty/morpho/)
24. [Morpho Formal Verification (Certora)](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/)
25. [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/)
26. [Morpho April 2025 Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/)
27. [Morpho Vulnerability Report (June 2023)](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM)
28. [Etherscan - Gauntlet USDC Prime Vault](https://etherscan.io/address/0xdd0f28e19C1780eb6396170735D45153D261490d)
29. [Etherscan - Morpho Blue](https://etherscan.io/address/0xbbbbbbbbbb9cc5e90e3b3af64bdaf62c37eeffcb)

### On-Chain Data
30. [Morpho GraphQL API](https://blue-api.morpho.org/graphql) -- Vault state, allocations, APY, timelock, roles (queried March 2026)
31. [Safe Transaction Service API - Owner Multisig](https://api.safe.global/tx-service/eth/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/)
32. [Safe Transaction Service API - Guardian](https://api.safe.global/tx-service/eth/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/)
33. [Safe Transaction Service API - Curator](https://api.safe.global/tx-service/eth/api/v1/safes/0x9E33faAE38ff641094fa68c65c2cE600b3410585/)
34. [DeFiLlama Treasury API - Morpho](https://api.llama.fi/treasury/morpho)
35. [DeFiLlama Treasury Adapter Source](https://raw.githubusercontent.com/DefiLlama/DefiLlama-Adapters/refs/heads/main/projects/treasury/morpho.js)
36. [Morpho App - Gauntlet USDC Prime](https://app.morpho.org/ethereum/vault/0xdd0f28e19C1780eb6396170735D45153D261490d/gauntlet-usdc-prime)
37. [Gauntlet App - USDC Prime](https://app.gauntlet.xyz/vaults/eth:0xdd0f28e19c1780eb6396170735d45153d261490d)

### Governance
38. [Gauntlet USDC Prime Vault Whitelisting](https://forum.morpho.org/t/gauntlet-usdc-prime-vault-whitelisting/496)

### News & Analysis
39. [CoinDesk - Gauntlet Moves to Morpho](https://www.coindesk.com/tech/2024/02/27/days-after-ditching-aave-risk-manager-gauntlet-moves-to-rival-lender-morpho/)
40. [CoinDesk - Gauntlet $380M Exit](https://www.coindesk.com/tech/2026/03/19/defi-risk-management-giant-gauntlet-sees-usd380-million-exit-as-okx-crypto-campaign-ends)
41. [Cointelegraph - White Hat Intercepts Morpho Vulnerability](https://cointelegraph.com/news/white-hat-intercepts-2-million-morpho-blue-hack)
42. [DeFi Prime - Resolv USR Exploit](https://defiprime.com/resolv-usr-exploit)
43. [Protos - Resolv Hack Analysis](https://protos.com/resolv-hack-shows-defi-learned-nothing-from-last-contagion/)
44. [Gauntlet $1B Valuation](https://www.gauntlet.xyz/resources/announcing-our-1-billion-valuation-and-next-steps-for-the-gauntlet-platform)
