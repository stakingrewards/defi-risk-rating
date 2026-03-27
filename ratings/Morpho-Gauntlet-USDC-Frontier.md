# Morpho - Gauntlet USDC Frontier Vault Risk Rating

**Rating Date**: 2026-03-25
**Final Grade**: CCC+
**Total Score**: 620.8/900 points
**Framework**: v0.1-beta

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 308.6/360 (85.7%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | **Framework criteria unchanged from prior rating.** Yes. 25+ audits from Tier-0/1 firms including ChainSecurity, Spearbit/OpenZeppelin, Zellic, Certora, Blackthorn. Morpho Blue core and MetaMorpho framework extensively audited. Formal verification by Certora. The vault (0xc582...) is a MetaMorpho V1.1 deployed via audited factory. Multiple independent audits covering all core fund-custody/routing contracts with public final reports. Audit counting per framework: each firm engagement = 1 independent audit. Easily exceeds >=2 threshold. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P0] [Etherscan Vault](https://etherscan.io/address/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | **Framework criteria unchanged.** December 2025: Certora (Tier-0), Spearbit (Tier-0), Blackthorn for Vaults V2. September 2025: ChainSecurity (Tier-0). Most recent audits by Tier-0 auditors per SR list. Meets Low (9): at least one most recent audit by Tier-0 auditor. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | **Framework criteria unchanged.** Yes. Morpho Blue immutable. V2 upgrades (Sep-Dec 2025) preceded by 8+ audit engagements. Frontier vault is V1.1 (non-upgradeable). Meets Low (9): every core upgrade had external audit before deployment. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | **Framework criteria unchanged.** Yes. June 2023 vulnerability patched with OpenZeppelin. Certora formal verification of invariants. All findings resolved with auditor re-verification or re-reviews. Meets Low (9): all critical/high findings resolved with auditor re-verification. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | **Framework criteria unchanged.** Morpho Blue immutable. MetaMorpho V1.1 (0xc582...) non-upgradeable ERC4626. Market changes require Curator + timelock + Guardian. Meets Low (9): immutable core contracts with comprehensive audit coverage. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | **Framework criteria include timeframe note (v0.1-beta adds recency weighting guidance).** Criteria verified: Low (9) = no confirmed exploit. Mid (3) = one confirmed exploit with user loss <2% over 24h AND 100% compensation AND post-mortem within 30 days. High (1) = permanent user loss OR loss >=2% over 24h OR no full compensation OR no detailed post-mortem. March 22, 2026: Resolv USR exploit caused confirmed bad debt in wstUSR/USDC, RLP/USDC, and PT-RLP/USDC markets where this vault had supply. Vault exposure ~$1.9M at 100% utilization. This represents <2% of pre-exploit TVL (~$115M). Compensation discussions with Resolv underway but NOT yet completed. No detailed post-mortem published by Gauntlet as of March 25 (3 days post-incident, still within the 30-day window). Strictly, the criteria require both 100% compensation AND post-mortem. Compensation is not yet confirmed. Scoring Mid (3) as loss <2% of pre-exploit TVL; compensation is being discussed; post-mortem window has not expired. If compensation fails or no post-mortem within 30 days, score drops to High (1). | 3 | 3 | Non-Improvable | [P4] [DeFiPrime Resolv Analysis](https://defiprime.com/resolv-usr-exploit), [P4] [The Block](https://www.theblock.co/post/394582/resolvs-usr-stablecoin-depegs-after-attacker-mints-80-million-unbacked-tokens-extracts-roughly-25-million), [P0] Morpho GraphQL API (wstUSR market at 100% utilization) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | **Framework criteria include timeframe note (v0.1-beta adds "no statute of limitations" language).** Criteria verified: Low (9) = no confirmed rug-pull and no unresolved credible allegations. No rug-pull events. Morpho (French nonprofit ADDMO). Gauntlet Networks Inc. ($41.8M raised, public leadership). No credible allegations. Meets Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | **Framework criteria unchanged.** No evidence of timelock reductions. Vault timelock verified at 259,200 seconds (3 days) via Morpho GraphQL API (confirmed March 25, 2026). Meets Low (9): no timelock reductions in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=259200) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | **Framework criteria unchanged.** Yes. Cantina bounty with $2.5M max payout. 236 findings submitted. Covers V1 and V2 contracts. Meets Low (9): active public bounty on established platform with max payout >=100k USD. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | **Framework criteria include expanded "verification principle" in v0.1-beta** requiring demonstration that monitoring is configured for specific risks AND alerts trigger protective actions OR documented SLAs under 15 minutes. Prior rating scored Mid (3) due to monitoring failing to halt automated allocation during Resolv exploit. Re-verified: Gauntlet partners with Hypernative, ZeroShadow (24/7 SOC), Chainalysis, SEAL Intel. The March 2026 Resolv exploit revealed monitoring did NOT prevent automated allocation into compromised markets for hours. The verification principle states: "Claiming to use a monitoring provider is NOT sufficient for Low (9)." Monitoring exists but failed to trigger protective actions during the most recent incident. Meets Mid (3): monitoring provider engaged but cannot automatically trigger protective actions. Score unchanged. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P4] [Protos](https://protos.com/resolv-hack-shows-defi-learned-nothing-from-last-contagion/) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | **Framework criteria include expanded "scope" note in v0.1-beta** explicitly requiring circuit breakers to cover ALL automated capital flows including Public Allocator, auto-rebalancers, keeper-driven supply. Prior rating scored High (1). Re-verified: No automatic on-chain circuit breakers by design. Morpho Blue prioritizes immutability. The March 2026 Resolv exploit demonstrated the consequences: automated allocation services continued providing liquidity to broken markets for hours. Guardian can veto pending timelocked actions but cannot halt automated capital flows. The framework states: "A protocol-level pause that doesn't stop automated capital injection into compromised markets is insufficient." Meets High (1): no effective safeguards covering automated capital flows. Score unchanged. | 1 | 1 | Non-Improvable | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P4] [Protos](https://protos.com/resolv-hack-shows-defi-learned-nothing-from-last-contagion/) |

**Smart Contract Security Subtotal: 143.6/180 (79.8%)**
- 8 questions scored 9 (sum = 72), 2 questions scored 3 (sum = 6), 1 question scored 1 (sum = 1)
- Raw sum = 79 out of max 99
- Weighted = (79/99) x 180 = 143.6

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | **Framework criteria unchanged.** Vault Owner is a Gnosis Safe 4-of-7 multisig (0xC684...), verified via Safe Transaction Service API (March 25, 2026). Guardian is a 3-of-7 Safe (0x7084...). Curator is a 3-of-7 Safe (0x9E33...). Vault timelock is 259,200s (3 days). All changes visible on-chain. Meets Low (9): admin/upgrade rights held by diversified multisig; changes publicly documented with on-chain trail. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | **Framework criteria unchanged.** No. Non-upgradeable contract. Morpho Blue immutable logic. Owner multisig 4-of-7 with 3-day timelock. Permissionless ERC4626 redemption always available. Meets Low (9): moving user funds requires multisig/governance with threshold >=3 AND total signers >=5 (4-of-7) and timelock >=24h (3 days). | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | **Framework criteria include expanded "independence verification" note in v0.1-beta** requiring different individuals to be verified via public disclosures, ENS names, governance docs, or on-chain identity. Prior rating scored 9. Re-verified: Owner is 4-of-7 Safe (exceeds 3-of-5 minimum). Guardian is 3-of-7 Safe. Curator is 3-of-7 Safe. Gauntlet is publicly identified as the entity operating these multisigs. Five signer addresses overlap across all three multisigs. The independence verification note says: "If signer identities are fully unknown, independence cannot be confirmed -- score Mid (3) at best." Gauntlet is publicly identified as the operating entity, but individual signer identities are not individually disclosed. However, Gauntlet has 50+ employees and is a well-known entity with public leadership -- it is reasonable that 7 signers are 7 different individuals within Gauntlet. The framework focuses on whether a single person controls multiple wallets. Gauntlet's institutional context provides reasonable assurance of independence. Meets Low (9): >=4-of-7 with signers controlled by >=3 independent individuals (institutional assurance). | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | **Framework criteria unchanged.** No address-level blocking. No pause function (immutable Morpho Blue). Guardian can only revoke pending timelocked actions. Withdrawals always permissionless. Meets Low (9): pause is time-bound/scope-limited; no address-level withdrawal censorship; rules public. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | **Framework criteria unchanged.** Yes. 100% in non-custodial Morpho Blue contracts on Ethereum. Permissionless ERC4626 redemption. No off-chain custody. Meets Low (9): 100% of user assets held in non-custodial on-chain contracts. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | **Framework criteria unchanged.** Yes. Clear on-chain segregation. Vault funds in Morpho Blue markets, separate from treasury/ops. Meets Low (9): clear on-chain segregation; no co-mingling. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | **Framework criteria unchanged.** On-chain enforced whitelist of Morpho Blue markets. Fresh API data (March 25, 2026) shows 21 markets in the vault's allocation including AA_FalconXUSDC (~79% of supply), plus Resolv-linked stuck positions (wstUSR, RLP, PT-RLP at supply cap 0 = removal pending), sUSDD, various PT tokens, stcUSD, siUSD, USCC, and others. Supply caps per market enforced on-chain. Changes require Curator + timelock + Guardian. Whitelist aligns with Frontier mandate. Meets Low (9): on-chain enforced whitelist; additions/removals require governance/multisig with timelock and public change log. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API vault allocation data |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | **Framework criteria unchanged.** Gauntlet has ZeroShadow (24/7 SOC), Hypernative, SEAL Intel partnerships. No public vault-specific incident playbook or tabletop exercise published. The March 2026 Resolv incident response -- specifically the failure to halt automated allocations for hours -- suggests playbook gaps. Meets Mid (3): a playbook exists but testing is informal or older than 12 months; key-rotation steps only partly automated. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |

**Key Management Subtotal: 165.0/180 (91.7%)**
- 7 questions scored 9 (sum = 63), 1 question scored 3 (sum = 3)
- Raw sum = 66 out of max 72
- Weighted = (66/72) x 180 = 165.0

---

### **Security Total: 308.6/360 (85.7%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 143.6 | 180 | 79.8% |
| Key Management | 165.0 | 180 | 91.7% |
| **Security Total** | **308.6** | **360** | **85.7%** |

---

### STRATEGY (30% Weight) -- Score: 96.9/270 (35.9%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | **Framework criteria include expanded "mandate definition" note in v0.1-beta.** Prior rating scored Mid (3). Re-verified: Yield from USDC lending interest against diversified collateral. The Frontier mandate targets maximum yield. Largest allocation (~79% FalconX AA tranche) generates organic lending yield. MORPHO emissions supplement. Framework states: "If no formal mandate exists, use protocol's stated purpose." Frontier explicitly targets maximum yield across higher-risk markets. Percent breakdown between organic and incentive yield remains incomplete. Estimated 30-70% from incentives. Meets Mid (3): main yield sources listed but percent breakdown incomplete or covers less than 80% of realized yield. Score unchanged. | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API, [P1] [Gauntlet Frontier Announcement](https://www.gauntlet.xyz/resources/introducing-gauntlet-frontier-vaults-on-the-hunt-for-defi-yields) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | **Framework criteria unchanged.** CONFIRMED: Loss has occurred. March 2026 Resolv exploit caused confirmed bad debt (~$1.9M, ~15% of current TVL). Loss can occur from non-tail events given history of two contagion events in 5 months. Meets High (1): negative net yield can occur in non-tail or recurring conditions due to material dependence on fragile counterparties. Score unchanged. | 1 | 1 | Non-Improvable | [P0] Morpho GraphQL API, [P4] [DeFiPrime](https://defiprime.com/resolv-usr-exploit) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | **Framework criteria unchanged.** No leverage at the vault level. Vault lends USDC at 1.0x effective leverage. Meets Low (9): no leverage or rehypothecation. Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet FalconX Strategy](https://www.gauntlet.xyz/resources/falconx-levered-rwa-strategy-with-pareto) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | **Framework criteria unchanged. Applicability: Vault is a lender, not a borrower.** N/A -- Vault is a USDC lender, not a borrower. No LTV position to manage. | N/A | N/A | N/A | Vault architecture |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | **Framework criteria include expanded "comparable variant guidance" in v0.1-beta.** Criteria verified: Low (9) = no permanent-loss events for this strategy or comparable variant over 24 months. High (1) = any uncompensated permanent-loss event or losses >=0.5% of peak TVL. March 2026: Resolv exploit caused confirmed bad debt (~$1.9M) in wstUSR/RLP/PT-RLP markets. $1.9M is ~1.7% of pre-exploit peak TVL (~$115M), which exceeds the 0.5% threshold. Additionally, November 2025: close variant (MEV Capital sdeUSD/USDC market on Morpho) experienced 3.6% bad debt -- comparable per framework ("same codebase with parameter changes = comparable"). Uncompensated permanent loss confirmed. Meets High (1). Score unchanged. | 1 | 1 | Non-Improvable | [P0] Morpho GraphQL API (markets at 100% utilization), [P4] [DeFiPrime](https://defiprime.com/resolv-usr-exploit) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | **Framework criteria unchanged.** Yes. Gauntlet VaultBook with curation methodology, risk factors, due diligence, and market allocation strategy. Clear Prime/Balanced/Frontier tiering. However, the risk framework did not prevent Resolv exposure. Meets Mid (3): partial framework exists with some limits but not consistently enforced. Score unchanged. | 3 | 9 | **Improvable** | [P1] [Curation Methodology](https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | **Framework criteria include expanded "definitions" note in v0.1-beta** explicitly defining organic vs incentive yield. Prior rating scored Mid (3). Re-verified: Organic yield from lending interest. MORPHO emissions supplement. Estimated 30-70% from incentives/emissions. Would remain positive without incentives but materially lower. Framework criteria: Mid (3) = "30-70% of realized yield coming from emissions or temporary programs but credible taper plan published." No formal taper plan published. This could be argued as High (1) since no taper plan is published, but MORPHO emissions are a well-known protocol-level program and strategy would remain positive without them. Scoring Mid (3) as yield is partially incentive-dependent within the 30-70% range. Score unchanged. | 3 | 9 | **Improvable** | [P1] [Gauntlet VaultBook Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | **Framework criteria unchanged.** SEVERELY CONSTRAINED. ~$1.9M in Resolv-linked markets and ~$792K in sUSDD market stuck at 100% utilization. Additional expired PT positions stuck. Only FalconX AA position (~$10.0M) has functioning liquidity. Total frozen/impaired: ~$2.7M or ~21% of TVL. Exits during stress turn yield deeply negative. Meets High (1): meaningful unwind requires long lockups or punitive slippage above 5-10%. Score unchanged. | 1 | 1 | Non-Improvable | [P0] Morpho GraphQL API (allocation data showing 100% utilization) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | **Framework criteria unchanged.** Current active allocation dominated by FalconX AA tranche (~79%), which depends on FalconX institutional credit quality. Residual stuck positions depend on collapsed wstUSR peg (94% down), RLP (18% down), sUSDD peg. These have already inverted causing confirmed losses. Meets High (1): strategy primarily driven by invertible spreads/pegs, regime shifts have already caused permanent losses. Score unchanged. | 1 | 1 | Non-Improvable | [P0] Morpho GraphQL API, [P4] [Resolv Analysis](https://resolv-usr-exploit.vercel.app/) |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | **This question was added in v0.1-beta. Prior rating already included it.** Framework criteria verified: High (1) = "Permissionless functions can increase vault exposure without human approval AND without automatic halt conditions." The March 2026 Resolv exploit demonstrated this exact failure mode. Morpho's supplyOnBehalf function allowed force-allocation of USDC into compromised markets. Gauntlet's automated allocation continued for hours post-exploit. No on-chain circuit breakers. Meets High (1). Score unchanged. | 1 | 1 | Non-Improvable | [P4] [DeFiPrime](https://defiprime.com/resolv-usr-exploit), [P4] [Protos](https://protos.com/resolv-hack-shows-defi-learned-nothing-from-last-contagion/) |

**Protocol Mechanics Subtotal: 12.8/45 (28.4%)**
- 9 applicable questions (ST-PM-04 = N/A): 1 scored 9 (sum = 9), 3 scored 3 (sum = 9), 5 scored 1 (sum = 5)
- Raw sum = 23 out of max 81
- Weighted = (23/81) x 45 = 12.8

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | **Framework criteria include expanded "rationale requirement" note in v0.1-beta** requiring explicit description of which assets and WHY they are rated low/mid/high. Prior rating scored Mid (3). Re-verified with fresh API data: Active allocation dominated by AA_FalconXUSDC (~79% of supply) -- a Pareto credit vault receipt token representing institutional crypto-backed lending (moderate risk: institutional counterparty but novel structure). Additional active markets include stcUSD, siUSD, PT tokens, syrupUSDC, USCC, wsrUSD, cbBTC, ETH+. Stuck positions in wstUSR (Resolv -- collapsed, Tier-3 per SR list), RLP (Resolv -- impaired), sUSDD (100% utilization). Collateral includes some higher-risk assets with explicit tiering via supply caps and LLTVs (ranging from 77% to 94.5%). cbBTC and ETH+ are lower-risk, but majority of exposure is to novel/higher-risk tokenized stablecoin derivatives. Meets Mid (3): collateral includes some higher risk assets but each is explicitly tiered with conservative on-chain LTVs and strict exposure caps. Score unchanged. | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | **Framework criteria unchanged.** CATASTROPHIC FAILURE confirmed. wstUSR collapsed 94% following March 2026 Resolv exploit. RLP declined 18%. These are current collateral types with severe depeg >10% lasting >7 days (still unresolved). Meets High (1): any collateral showed depeg above 10% or lasting more than 7 days. Score unchanged. | 1 | 1 | Non-Improvable | [P4] [Resolv Analysis](https://resolv-usr-exploit.vercel.app/), [P0] Morpho GraphQL API |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | **Framework criteria unchanged. Applicability: No staking-based collateral.** N/A. | N/A | N/A | N/A | Vault architecture |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | **Framework criteria include expanded "definition" note in v0.1-beta** clarifying what counts as bridged/wrapped. Prior rating scored High (1). Re-verified: The framework excludes native chain tokens, WETH, natively issued stablecoins, and protocol receipt tokens from the bridged/wrapped definition. The vault's collateral is all deployed on Ethereum. AA_FalconXUSDC is a credit vault receipt token (protocol receipt token -- arguably excluded). stcUSD, siUSD, wsrUSD, sUSDD are savings/wrapped stablecoin tokens. PT tokens are Pendle principal tokens (protocol receipt tokens). cbBTC is a wrapped BTC (custody-backed by Coinbase). Under the strict framework definition, many of these are "wrapped" or involve wrapping contracts maintaining 1:1 backing. Even excluding protocol receipt tokens, the wrapped/synthetic collateral exposure exceeds 60%. Meets High (1): bridged or wrapped assets >60% of TVL. Score unchanged. | 1 | 9 | **Improvable** | [P0] Morpho GraphQL API |

**Collateral Subtotal: 8.3/45 (18.5%)**
- 3 applicable questions (ST-C-03 = N/A): ST-C-01(3), ST-C-02(1), ST-C-04(1)
- Raw sum = 5 out of max 27
- Weighted = (5/27) x 45 = 8.3

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | **Framework criteria unchanged.** Ethereum (Tier-0), Chainlink (Tier-0 oracle). No bridges or CEX dependency. Some market oracles use Morpho-custom oracle adapters. All critical dependencies listed; only Tier-0/1 counterparts used. Meets Low (9). Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant are oracle and bridge setups, and can oracle values be corrected under abnormal conditions? | **Framework criteria include new "hardcoded/immutable oracle check (MANDATORY)" pre-check in v0.1-beta.** Prior rating scored High (1). Re-verified: The mandatory pre-check asks: (1) Does any oracle use a hardcoded or immutable price? YES -- each Morpho Blue market has one immutable oracle. (2) Can the priced asset depeg or lose value materially? YES -- wstUSR collapsed 94%. Framework states: "If yes to both, score High (1) -- the loss path is unbounded." The March 2026 exploit exploited this directly. Meets High (1): hardcoded/immutable oracle pricing for an asset that can depeg materially. Score unchanged. | 1 | 1 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/), [P4] [Resolv Analysis](https://resolv-usr-exploit.vercel.app/) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | **Framework criteria include new "applicability check (MANDATORY)" in v0.1-beta** requiring first determination of whether strategy relies on ANY off-chain infrastructure. Re-verified: Does the vault rely on off-chain infra? Gauntlet operates automated allocation services (off-chain risk engine, rebalancing logic). These are off-chain components that influence capital allocation. Chainlink oracle infrastructure has enterprise certifications. No explicit SOC 2 Type II or ISO27001 for Gauntlet Networks disclosed. Meets Mid (3): some critical providers certified (Chainlink) while others rely on internal controls. Score unchanged. | 3 | 9 | **Source Missing** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | **Framework criteria include new "new protocol guidance" in v0.1-beta** (not applicable -- vault deployed >6 months). March 2026 Resolv exploit: Gauntlet's automated allocation services continued providing liquidity to broken wstUSR/RLP markets for hours post-exploit, directly aggravating bad debt. The framework High (1) criterion covers incidents where infra components "contributed to losses" -- the automated allocation service is an infra component that contributed to losses by continuing to supply capital to compromised markets. November 2025 sdeUSD: vault operated correctly. April 2025 frontend: resolved in 4 minutes. Meets High (1): past incident directly contributed to permanent user losses. Score changed from 3 to 1. | 1 | 1 | Non-Improvable | [P4] [Protos](https://protos.com/resolv-hack-shows-defi-learned-nothing-from-last-contagion/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | **Framework criteria unchanged.** No. Ethereum: no halts >30 minutes in last 12+ months. Meets Low (9). Score unchanged. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | **Framework criteria unchanged. No staking-based collateral.** N/A. | N/A | N/A | N/A | Vault architecture |
| ST-IC-07 | Are validators diverse geographically and by operator? | **Framework criteria unchanged. No staking-based collateral.** N/A. | N/A | N/A | N/A | Vault architecture |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | **Framework criteria unchanged.** ERC4626 redemption is permissionless. However, the March 2026 exploit demonstrated that oracle failure (stale pricing) combined with supplyOnBehalf bypass CAN cause losses even though withdrawals remain technically possible. Users can withdraw, but ~21% of TVL is stuck at 100% utilization. Single oracle failure cannot block withdrawals but can cause losses. Meets Mid (3): one or two infra components operationally important; single failure could temporarily delay or degrade withdrawals but redundancy expected to restore without permanent user loss. Score unchanged. | 3 | 3 | Non-Improvable | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P0] Morpho GraphQL API |

**Infrastructure Counterparty Subtotal: 21.7/45 (48.1%)**
- 6 applicable questions (ST-IC-06, ST-IC-07 = N/A): ST-IC-01(9), ST-IC-02(1), ST-IC-03(3), ST-IC-04(1), ST-IC-05(9), ST-IC-08(3)
- 2x9=18, 1x3=3, 2x1=2. Raw=23+3=26, Max=54. (26/54)*45 = 21.7

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | **Framework criteria unchanged.** Vault capital deployed to Morpho Blue (Tier-0) lending markets. Collateral dependency chains extend to Resolv (Tier-3, exploited), Pareto/FalconX, stcUSD (Cap), siUSD (InfiniFi), Superstate USCC, syrupUSDC (Maple). The vault had direct exposure to Resolv (Tier-3) which failed catastrophically. Framework criteria: High (1) = "strategy relies materially on Tier-3 venues." The Resolv exposure was ~$1.9M which WAS material (caused permanent loss). However, looking at the overall venue disclosure: most venues are disclosed with partial tiering. Scoring Mid (3): most venues disclosed; strategy relied materially on a Tier-3 venue. Score unchanged. | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | **Framework criteria unchanged.** MORPHO emissions flow to vault depositors. Incentive arrangements with underlying protocols partially disclosed. Terms only partially disclosed. Meets Mid (3): arrangements acknowledged but terms only partially disclosed. Score unchanged. | 3 | 9 | **Improvable** | [P1] [Incentives & Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | **Framework criteria unchanged.** On-chain supply caps per market exist. The March 2026 exploit revealed that supplyOnBehalf can bypass vault-level supply caps. Caps are enforced at the vault layer but not at the Morpho protocol layer. Meets Mid (3): caps exist and documented but enforcement partly manual and timing discretionary. Score unchanged. | 3 | 3 | Non-Improvable | [P4] [DeFiPrime](https://defiprime.com/resolv-usr-exploit) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | **Framework criteria unchanged.** SEVERELY IMPAIRED. ~$2.7M (21% of TVL) stuck at 100% utilization in wstUSR, RLP, PT-RLP, and sUSDD markets. Only FalconX AA position (~$10.0M) has functioning liquidity. Exit feasibility for stuck positions unknown. Meets High (1): positions may be hard to unwind within stated horizons or exit feasibility unknown. Score unchanged. | 1 | 3 | Non-Improvable | [P0] Morpho GraphQL API |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | **Framework criteria include new "applicability check (MANDATORY)" in v0.1-beta.** Re-verified: Does the strategy use ANY third-party validators, custody providers, or asset managers? Pure on-chain lending via Morpho Blue. No external validators or custodians for the vault itself. Gauntlet (curator) disclosed. Per framework: "if so, score Low (9) and the Deal Breaker does NOT trigger." Meets Low (9). Score unchanged. | 9 | 9 | Non-Improvable (optimal) | Vault architecture |

**Protocol Counterparty Subtotal: 19.0/45 (42.2%)**
- ST-PC-01(3), ST-PC-02(3), ST-PC-03(3), ST-PC-04(1), ST-PC-05(9)
- 1x9=9, 3x3=9, 1x1=1. Raw=19, Max=45. (19/45)*45 = 19.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | **Framework criteria include new "withdrawal period baseline" header in v0.1-beta.** Withdrawal baseline for this vault: design-implied instant (ERC4626 AMM-style lending). Permissionless ERC4626 redemption. No address-level blocking. No admin pause. Withdrawal depends on market liquidity -- currently ~21% of TVL is stuck at 100% utilization. Meets Low (9): all users have permissionless on-chain redemption path; any pause is protocol-wide only. Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | **Framework criteria unchanged.** NO. ~$2.7M (21% of TVL) frozen at 100% utilization in broken/stressed markets. Only ~$10.0M in FalconX market accessible. Near-total exit impossible. Meets High (1): liquidity shallow; no credible path for system-wide exits. Score unchanged. | 1 | 1 | Non-Improvable | [P0] Morpho GraphQL API |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | **Framework criteria unchanged.** YES -- REPEATED. November 2025: liquidity dropped below 1% for ~6 hours. March 2026: ~21% of TVL frozen at 100% utilization, ongoing for 3+ days. Less than 80% of withdrawals can currently be completed within stated period. Meets High (1): less than 80% completed within stated period, or prolonged freezes. Score unchanged. | 1 | 1 | Non-Improvable | [P0] Morpho GraphQL API, [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | **Framework criteria unchanged.** The supplyOnBehalf bypass demonstrated that caps can be circumvented. Currently, 100% utilization in broken markets is the binding constraint, not caps. Meets Mid (3): caps occasionally created queues during high utilization but cleared within days. Score unchanged. | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | **Framework criteria unchanged.** REPEATEDLY STRESSED. November 2025: liquidity dropped below 1% for ~6 hours. March 2026: ~21% of TVL frozen with no exit path. Two stress events in 5 months, the most recent causing multi-day dysfunction. Meets High (1): volatility or congestion repeatedly leads to unreliable exits, multi-day dysfunction. Score unchanged. | 1 | 1 | Non-Improvable | [P0] Morpho GraphQL API, [P4] [DeFiPrime](https://defiprime.com/resolv-usr-exploit) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | **Framework criteria unchanged.** ~21% of assets effectively locked for indefinite period (Resolv-linked markets at 100% utilization). Unwind depends on Resolv compensation which is uncertain. More than 10% of assets are longer-dated than stated withdrawal terms. Meets Mid (3): roughly 10-30% of assets have longer duration than withdrawal terms. Score unchanged. | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | **Framework criteria unchanged.** No. Primary ERC4626 redemption always available. Secondary market not required. Meets Low (9): most users can exit via in-protocol redemption. Score unchanged. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | **Framework criteria unchanged.** SEVERELY IMPAIRED. wstUSR liquidity essentially zero (collapsed 94%). RLP impaired. sUSDD at 100% utilization. Only FalconX AA tranche has functioning but thin secondary market. Meets High (1): depth below ~3% of TVL without major impact. Score unchanged. | 1 | 1 | Non-Improvable | [P4] [Resolv Analysis](https://resolv-usr-exploit.vercel.app/) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | **Framework criteria unchanged.** ACTIVELY OCCURRING. The Resolv exploit triggered this scenario -- depositors cannot exit ~21% of positions. The 88%+ TVL decline ($115M to $12.7M) represents a bank run that has already crystallized. Meets High (1): fast bank-run likely to force meaningful permanent losses or prolonged withdrawal blocks. Score unchanged. | 1 | 1 | Non-Improvable | [P0] Morpho GraphQL API |

**Liquidity Subtotal: 16.1/45 (35.8%)**
- 9 questions: ST-L-01(9), ST-L-02(1), ST-L-03(1), ST-L-04(3), ST-L-05(1), ST-L-06(3), ST-L-07(9), ST-L-08(1), ST-L-09(1)
- 2x9=18, 2x3=6, 5x1=5. Raw sum=29, Max=81. (29/81)*45 = 16.1

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | **Framework criteria include new "applicability check (MANDATORY)" in v0.1-beta.** Re-verified applicability: Does this vault issue a transferable receipt token that trades on secondary markets at a price that should track a reference value? Yes -- MetaMorpho vault shares are ERC4626 tokens. However, ERC4626 vault shares do not typically trade on secondary markets with a "peg" -- they represent claims on the underlying NAV. The framework says to mark N/A for "protocols where users hold positions directly" or "non-transferable account balances." ERC4626 shares ARE transferable and tradeable, so the question applies. During stress: vault share price reflects accrued bad debt from wstUSR/RLP markets. The 88% TVL decline and ~21% frozen positions represent severe stress. Share value has declined reflecting embedded losses. Meets Mid (3): during stress, token deviated 2-10% with clear market-wide drivers. Score unchanged. | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | **Framework criteria unchanged.** Low directional risk from crypto market moves for USDC lending. The vault lends USDC -- a stablecoin -- so crypto market direction has limited direct impact. Losses came from collateral protocol failure rather than crypto market direction. The FalconX AA tranche has indirect crypto exposure but at 77% LLTV with institutional counterparty. Meets Low (9): strategy is low-beta with strictly capped leverage. Score unchanged. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | **Framework criteria unchanged.** Immutable Adaptive Curve IRM. November 2025: IRM reduced borrowing 72%. March 2026: IRM cannot resolve 100% utilization when collateral is worthless. Framework criteria: High (1) = "models can remain flat near full utilization or have history of prolonged >=95-100% utilization." Several markets ARE at 100% utilization (wstUSR, RLP, PT-RLP, sUSDD). However, this is due to collateral failure not rate model failure. The IRM itself functions correctly and becomes steep at high utilization. Meets Mid (3): models show temporary strain with short spikes in utilization. Score unchanged. | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | **Framework criteria unchanged.** Yes. Gauntlet agent-based simulations. However, March 2026 Resolv exploit was a novel attack vector not modeled. Partial coverage. Meets Mid (3): strategy tested against moderate volatility but tail assumptions only partially covered. Score unchanged. | 3 | 3 | Non-Improvable | [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | **Framework criteria unchanged.** YES -- CONFIRMED. wstUSR collapsed 94%, RLP declined 18%. Markets at 91.5% LLTV now have bad debt because liquidators cannot profitably liquidate worthless collateral. Meets High (1): common high-volatility moves can trigger rapid liquidations/forced exits that permanently reduce depositor principal. Score unchanged. | 1 | 1 | Non-Improvable | [P0] Morpho GraphQL API, [P4] [Resolv Analysis](https://resolv-usr-exploit.vercel.app/) |

**Market Subtotal: 19.0/45 (42.2%)**
- ST-M-01(3), ST-M-02(9), ST-M-03(3), ST-M-04(3), ST-M-05(1)
- 1x9=9, 3x3=9, 1x1=1. Raw=19, Max=45. (19/45)*45 = 19.0

---

### **Strategy Total: 96.9/270 (35.9%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 12.8 | 45 | 28.4% |
| Collateral | 8.3 | 45 | 18.5% |
| Infra Counterparty | 21.7 | 45 | 48.1% |
| Protocol Counterparty | 19.0 | 45 | 42.2% |
| Liquidity | 16.1 | 45 | 35.8% |
| Market | 19.0 | 45 | 42.2% |
| **Strategy Total** | **96.9** | **270** | **35.9%** |

---

### OPERATIONS (30% Weight) -- Score: 215.3/270 (79.7%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | **Framework criteria unchanged.** Hybrid. Morpho Blue immutable. Vault changes require Owner multisig + timelock + Guardian. Multiple layers. No single entity can unilaterally change core logic. Meets Low (9). Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | **Framework criteria include new "applicability check (MANDATORY)" in v0.1-beta.** Re-verified: Does the protocol have a governance token? This vault does not have governance token voting. Vault controlled by multisig + Guardian. The framework says: "If the protocol has no governance token (pure multisig governance, no on-chain voting), mark N/A." N/A. Score unchanged. | N/A | N/A | N/A | Vault architecture |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | **Framework criteria unchanged.** Vault timelock verified at 259,200 seconds (3 days) via Morpho GraphQL API (March 25, 2026). Guardian (3-of-7 Safe) can veto pending timelocked actions. 3-day timelock exceeds 24-hour minimum. Meets Low (9): all major upgrades subject to visible timelock >=24h. Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock: 259200) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | **Framework criteria unchanged.** Yes. Owner can appoint new Curator (subject to timelock). Withdrawals remain permissionless via ERC4626. Meets Low (9): strategy manager can be replaced while keeping withdrawals functional. Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 3 applicable (O-G-02 = N/A): 3 scored 9 (sum = 27)
- Raw sum = 27 out of max 27
- Weighted = (27/27) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | **Framework criteria unchanged.** Yes. Gauntlet: Tarun Chitra (CEO), Rei Chiang (Co-founder). 50+ team. Morpho: Paul Frambot (CEO). All publicly identified with verifiable track records. Meets Low (9). Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Team](https://www.gauntlet.xyz/our-team) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | **Framework criteria unchanged.** No. Gauntlet 50+ employees. Morpho separate team ($73.6M raised). No key-person dependency. Meets Low (9). Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet About](https://www.gauntlet.xyz/about) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | **Framework criteria unchanged.** Morpho: ADDMO (France). Gauntlet: Gauntlet Networks Inc. (New York, USA). Both clearly identified and mapped to operational responsibilities. Meets Low (9). Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | **Framework criteria unchanged.** No known actions against Gauntlet Networks Inc. or Morpho entities in any major jurisdiction. Meets Low (9). Score unchanged. | 9 | 9 | Non-Improvable (optimal) | Public records |
| O-TL-05 | Is there an on-call and incident response process for core teams? | **Framework criteria include new "automation override requirement" in v0.1-beta** requiring documented procedures to halt automated allocation mechanisms during incidents. Prior rating scored Mid (3). Re-verified: Gauntlet has 24/7 monitoring with ZeroShadow SOC and Hypernative. Framework now requires: "if automated allocation mechanisms exist, runbooks include explicit steps to halt them AND team has demonstrated ability to do so within SLA." The March 2026 Resolv incident revealed: automated allocation continued for hours. Gauntlet did NOT demonstrate ability to halt automated capital flows within SLA. No post-mortem published 3 days later. Framework criteria: Mid (3) = "formal on-call exists but does not cover halting automated allocation mechanisms, OR response time to halt automated systems exceeds 1 hour." Meets Mid (3). Score unchanged. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P4] [Protos](https://protos.com/resolv-hack-shows-defi-learned-nothing-from-last-contagion/) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | **Framework criteria unchanged.** Previous track record: November 2025 market report published within days, April 2025 4-minute frontend response. However, as of March 25, 2026 -- 3 days after the Resolv exploit -- no dedicated post-mortem or market report has been published by Gauntlet. Only brief statements. Framework criteria: Mid (3) = "response inconsistent and often 24-72 hours." 3 days exceeds 72 hours. However, Gauntlet did acknowledge the issue within 24 hours. Scoring Mid (3) for inconsistent response. Score unchanged. | 3 | 9 | **Improvable** | [P4] [WEEX News](https://www.weex.com/news/detail/gauntlet-the-majority-of-treasuries-were-unaffected-by-the-usr-exploit-event-with-a-few-high-yield-treasuries-having-limited-risk-398611) |
| O-TL-07 | Are major investors or strategic partners disclosed? | **Framework criteria include expanded "scoring rationale" note in v0.1-beta** clarifying that this measures investor INFLUENCE risk. Prior rating scored Low (9). Re-verified: Gauntlet investors: Polychain, Paradigm, Ribbit Capital. Morpho: a16z, Variant, Pantera, Coinbase Ventures. All disclosed with roles clear. No opaque control. Meets Low (9): major investors and strategic partners disclosed along with their roles, rights, and governance influence. Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay](https://www.clay.com/dossier/gauntlet-funding) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | **Framework criteria unchanged.** Yes. Gauntlet manages 70+ vaults with $1.4B+ AUM including Prime, Balanced, Frontier, Core tiers. No formal quantitative conflict-of-interest policy. Potential for routing riskier allocations to Frontier. Meets Mid (3): other mandates exist with partial disclosure and qualitative conflict policies but limited hard constraints. Score unchanged. | 3 | 9 | **Improvable** | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | **Framework criteria unchanged.** YES -- March 2026: Gauntlet Frontier (this vault) and Gauntlet Core both have confirmed bad debt from Resolv USR exploit. Total Gauntlet exposure estimated >$7.5M across affected vaults. This is the first confirmed bad debt in a Gauntlet vault. Framework criteria: High (1) = "multiple incidents, any uncompensated depositor losses, or history of materially reckless curation decisions." The Resolv loss is uncompensated so far. Meets High (1). Score unchanged. | 1 | 1 | Non-Improvable | [P4] [DeFiPrime](https://defiprime.com/resolv-usr-exploit), [P4] [The Block](https://www.theblock.co/post/394582/resolvs-usr-stablecoin-depegs-after-attacker-mints-80-million-unbacked-tokens-extracts-roughly-25-million) |

**Team & Legal Subtotal: 45.8/67.5 (67.9%)**
- 5 scored 9 (sum = 45), 3 scored 3 (sum = 9), 1 scored 1 (sum = 1)
- Raw sum = 55 out of max 81
- Weighted = (55/81) x 67.5 = 45.8

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | **Framework criteria unchanged.** Yes. Comprehensive Morpho docs and Gauntlet VaultBook. Frontier tier explicitly described with risk warnings. Updated after V2 upgrade. Meets Low (9). Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Docs](https://docs.morpho.org/), [P1] [VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | **Framework criteria unchanged.** Yes. Liquidation mechanics, bad debt scenarios, oracle risks documented. Frontier risk profile explicitly described. Meets Low (9). Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | **Framework criteria unchanged.** Yes. Canonical address registry. Vault on Morpho App and Gauntlet App. Etherscan-verified. Meets Low (9). Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | **Framework criteria unchanged.** Yes. Comprehensive role documentation. Changes visible on-chain. Meets Low (9). Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | **Framework criteria include expanded "applicability clarification" in v0.1-beta** noting proof-of-reserves is ALWAYS required and proof-of-liabilities is required when protocol has liabilities. This vault is a lending protocol with outstanding borrows -- both apply. Full real-time on-chain proof-of-reserves AND proof-of-liabilities visible on Morpho App and Etherscan. All allocations, borrows, and collateral visible. Meets Low (9): proof-of-reserves published with verifiable methodology AND proof-of-liabilities also published. Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | **Framework criteria unchanged.** Yes. MetaMorphoV1_1 contract verified on Etherscan. Full source code readable. Meets Low (9). Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | **Framework criteria unchanged.** No dedicated safety module. Bad debt socialized per market. Morpho DAO treasury discretionary. No Gauntlet-specific backstop. Gauntlet states "working on compensation plan" for Resolv losses but no commitment yet. Meets Mid (3): backstop stated as intended for loss coverage but activation remains discretionary. Score unchanged. | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | **Framework criteria include expanded "MANDATORY research steps" and "TVL denominator" note in v0.1-beta.** Re-verified with fresh DeFiLlama data (March 25, 2026): Morpho DAO treasury = ~$34.1M in own tokens (MORPHO) + ~$10K in other assets. Liquid non-own-token component is negligible. Against Morpho protocol total TVL (~$6.9B+) = ~0.5%. Against this vault's TVL ($12.7M), Morpho DAO treasury would be large, but the framework says for multi-product protocols: "compare against TOTAL protocol TVL." ~$34.1M / ~$6.9B = ~0.5%. No vault-specific reserve. Framework criteria: High (1) = "liquid reserves and treasury <1% of TVL or dominated by illiquid or highly volatile native tokens." Morpho treasury is dominated by MORPHO tokens (volatile native token). Meets High (1). Score unchanged. | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | **Framework criteria unchanged.** Strong. Gauntlet $41.8M raised, $1B valuation. Morpho $73.6M raised. Combined runway >24 months. Meets Low (9). Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay](https://www.clay.com/dossier/gauntlet-funding) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | **Framework criteria unchanged.** STRUCTURAL COLLAPSE. TVL declined 88%+ from ~$115M to ~$12.7M. Two major contagion events in 5 months. November 2025: 20% TVL decline with zero bad debt. March 2026: 88%+ TVL decline with confirmed bad debt. Framework criteria: High (1) = "stress periods led to structural TVL collapse, persistent revenue impairment, or buffer depletion that increased depositor loss risk." Meets High (1). Score unchanged. | 1 | 1 | Non-Improvable | [P0] Morpho GraphQL API (TVL=$12.7M), [P4] [DeFiPrime](https://defiprime.com/resolv-usr-exploit) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | **Framework criteria unchanged.** Yes. Morpho Blue immutable. Permissionless ERC4626 withdrawals (subject to liquidity). No proprietary off-chain services required. Meets Low (9): contracts allow safe maintenance mode; withdrawals remain permissionless. Score unchanged. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Financial Resilience Subtotal: 34.5/67.5 (51.1%)**
- 2 scored 9 (sum = 18), 1 scored 3 (sum = 3), 2 scored 1 (sum = 2)
- Raw sum = 23 out of max 45
- Weighted = (23/45) x 67.5 = 34.5

---

### **Operations Total: 215.3/270 (79.7%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 67.5 | 67.5 | 100.0% |
| Team & Legal | 45.8 | 67.5 | 67.9% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 34.5 | 67.5 | 51.1% |
| **Operations Total** | **215.3** | **270** | **79.7%** |

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 79 | 99 | 143.6 | 180 | 79.8% |
| | Key Management (8 Q) | 66 | 72 | 165.0 | 180 | 91.7% |
| | **Security Subtotal** | | | **308.6** | **360** | **85.7%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 23 | 81 | 12.8 | 45 | 28.4% |
| | Collateral (3 of 4 Q scored) | 5 | 27 | 8.3 | 45 | 18.5% |
| | Infra Counterparty (6 of 8 Q scored) | 26 | 54 | 21.7 | 45 | 48.1% |
| | Protocol Counterparty (5 Q) | 19 | 45 | 19.0 | 45 | 42.2% |
| | Liquidity (9 Q) | 29 | 81 | 16.1 | 45 | 35.8% |
| | Market (5 Q) | 19 | 45 | 19.0 | 45 | 42.2% |
| | **Strategy Subtotal** | | | **96.9** | **270** | **35.9%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 55 | 81 | 45.8 | 67.5 | 67.9% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 23 | 45 | 34.5 | 67.5 | 51.1% |
| | **Operations Subtotal** | | | **215.3** | **270** | **79.7%** |
| **TOTAL** | | | | **620.8** | **900** | **69.0%** |

---

