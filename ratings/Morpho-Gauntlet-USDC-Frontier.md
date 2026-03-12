# Morpho - Gauntlet USDC Frontier Vault Risk Rating

**Rating Date**: 2026-03-10
**Final Grade**: BB-
**Total Score**: 738.6/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v1.0-alpha

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 334.1/360 (92.8%)

#### Smart Contract Security (20% weight, 180 max points)

**NOTE: All Smart Contract Security scores are IDENTICAL to Gauntlet USDC Prime (BB/775.6). The Frontier vault uses the same Morpho Blue protocol and MetaMorpho V1.1 factory contracts.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 25+ audits from Tier-0/1 firms including ChainSecurity, Spearbit/OpenZeppelin, Zellic, Certora, Blackthorn. Morpho Blue core and MetaMorpho framework extensively audited. Formal verification by Certora. The vault (0xc582...) is a MetaMorpho V1.1 deployed via audited factory. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P0] [Etherscan Vault](https://etherscan.io/address/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | December 2025: Certora (Tier-0), Spearbit (Tier-0), Blackthorn for Vaults V2. September 2025: ChainSecurity (Tier-0). Multiple Tier-0 auditors. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue immutable. V2 upgrades (Sep-Dec 2025) preceded by 8+ audit engagements. Frontier vault is V1.1 (non-upgradeable). | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 vulnerability patched with OpenZeppelin. Certora formal verification of invariants. All findings resolved with re-reviews. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue immutable. MetaMorpho V1.1 (0xc582...) non-upgradeable ERC4626. Market changes require Curator + timelock + Guardian. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan - verified MetaMorphoV1_1](https://etherscan.io/address/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No user fund loss in Gauntlet vaults. April 2025 frontend vulnerability intercepted (4 min response). November 2025 deUSD/Stream contagion: Gauntlet Frontier reported ZERO bad debt despite sdeUSD collateral exposure. Rate-driven deleveraging (72% borrow reduction) was effective. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No. Morpho (French nonprofit ADDMO). Gauntlet Networks Inc. ($41.8M raised, public leadership). No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No evidence of timelock reductions since January 2025 deployment. | 9 | 9 | Non-Improvable (optimal) | [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Cantina bounty with $2.5M max payout. 236 findings submitted. Covers V1 and V2 contracts. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. Morpho monitoring bots + Gauntlet partnerships with Hypernative, ZeroShadow (24/7 SOC), Chainalysis, SEAL Intel. 4-minute response demonstrated. 24/7 liquidity monitoring confirmed in Nov 2025. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. Morpho Blue prioritizes immutability. Guardian can veto pending timelocked actions. Market-level isolation provides containment. | 3 | 3 | Non-Improvable | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Smart Contract Security Subtotal: 169.1/180 (93.9%)**
- 10 questions scored 9 (sum = 90), 1 question scored 3 (sum = 3)
- Raw sum = 93 out of max 99
- Weighted = (93/99) x 180 = 169.1

---

#### Key Management & Permissions (20% weight, 180 max points)

**NOTE: Key Management scores are IDENTICAL to Gauntlet USDC Prime (same curator governance structure). S-KM-01 updated to 9 based on verified Safe API data (March 2026).**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Vault Owner is a Gnosis Safe 4-of-7 multisig (0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec), verified via Safe Transaction Service API (March 2026, nonce 497). Guardian is a 3-of-7 Safe (0x7084bF4dB6c21e1834dD6482f6056a39A33584cD, nonce 3). Curator is a 3-of-7 Safe (0x9E33faAE38ff641094fa68c65c2cE600b3410585, nonce 330). Vault timelock is 259,200s (3 days). All changes visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API Guardian](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/), [P0] [Safe API Curator](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x9E33faAE38ff641094fa68c65c2cE600b3410585/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Non-upgradeable contract. Morpho Blue immutable logic. Multisig + timelock + Guardian required. Permissionless ERC4626 redemption always available. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner is 4-of-7 Safe (exceeds 3-of-5 minimum). Guardian is 3-of-7 Safe. Curator is 3-of-7 Safe. Five signer addresses overlap across all three multisigs. Gauntlet is publicly identified as the entity operating these multisigs. Guardian is Gauntlet-controlled Safe (not depositor-controlled DAO like Steakhouse's Aragon DAO). | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API Guardian](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/), [P0] [Safe API Curator](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x9E33faAE38ff641094fa68c65c2cE600b3410585/) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking. No pause function (immutable Morpho Blue). Guardian can only revoke pending timelocked actions. Withdrawals always permissionless. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% in non-custodial Morpho Blue contracts on Ethereum. Permissionless ERC4626 redemption. No off-chain custody. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. Vault funds in Morpho Blue markets, separate from treasury/ops. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain enforced whitelist of Morpho Blue markets. Current markets include AA_FalconXUSDC/USDC, siUSD/USDC, syrupUSDC/USDC, stcUSD/USDC, wsrUSD/USDC, PT-srUSDe/USDC, PT-cUSD/USDC, RLP/USDC, and smaller residual positions. Supply caps per market enforced on-chain. Changes require Curator + timelock + Guardian. Whitelist aligns with Frontier mandate. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho App](https://app.morpho.org/ethereum/vault/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e/gauntlet-usdc-frontier) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Gauntlet has ZeroShadow (24/7 SOC), Hypernative, SEAL Intel partnerships. Morpho docs include emergency procedures. No public vault-specific incident playbook or tabletop exercise published. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |

**Key Management Subtotal: 165.0/180 (91.7%)**
- 7 questions scored 9 (sum = 63), 1 question scored 3 (sum = 3)
- Raw sum = 66 out of max 72
- Weighted = (66/72) x 180 = 165.0

---

### **Security Total: 334.1/360 (92.8%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 169.1 | 180 | 93.9% |
| Key Management | 165.0 | 180 | 91.7% |
| **Security Total** | **319.1** | **360** | **88.6%** |

---

### STRATEGY (30% Weight) -- Score: 169.5/270 (62.8%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield from USDC lending interest against diversified collateral. The Frontier mandate targets maximum yield across higher-risk markets. The largest allocation (34%, FalconX AA tranche) generates yield from institutional crypto-backed lending at FalconX. siUSD (25.5%) is a yield-bearing staked stablecoin from infiniFi's fractional reserve protocol. syrupUSDC (15.3%) represents Maple's institutional lending. stcUSD (15.1%) is Cap's staked cUSD. MORPHO emissions supplement organic yield. Yield sources listed but percent breakdown between organic lending yield and incentive yield remains incomplete. Incentive component estimated at 30-70% of total realized yield. | 3 | 9 | **Improvable** | [P1] [Gauntlet Frontier Announcement](https://www.gauntlet.xyz/resources/introducing-gauntlet-frontier-vaults-on-the-hunt-for-defi-yields), [P1] [Morpho App](https://app.morpho.org/ethereum/vault/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e/gauntlet-usdc-frontier) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss in severe but plausible single-shock events: (1) FalconX borrower defaults causing AA tranche impairment (mitigated by 77% LLTV providing 23% buffer and institutional structuring); (2) infiniFi siUSD fractional reserve bank run (protocol launched mid-2025, limited stress-test history); (3) syrupUSDC depeg if Maple institutional borrowers default (active Cayman injunction on syrupBTC product); (4) cap USD/stcUSD failure (protocol launched August 2025, ~$500M TVL); (5) Resolv wsrUSD/RLP depeg from delta-neutral strategy failure. The diversity of collateral and the FalconX AA tranche at 77% LLTV provide better loss buffer than the previous uniform 91.5% LLTV profile. However, most non-FalconX markets still use 91.5% LLTV (~8.5% buffer), and the underlying protocols are novel. | 3 | 3 | Non-Improvable | [P1] [Gauntlet FalconX Strategy](https://www.gauntlet.xyz/resources/falconx-levered-rwa-strategy-with-pareto), [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No at the vault level. Vault lends USDC at 1.0x effective leverage. However, the FalconX levered RWA strategy (34% of vault TVL) involves borrowers looping FalconX CV tokens -- this is borrower-side leverage, not vault-level. The vault itself has no rehypothecation. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet FalconX Strategy](https://www.gauntlet.xyz/resources/falconx-levered-rwa-strategy-with-pareto) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss in Gauntlet Frontier vault. The vault survived the November 2025 sdeUSD/deUSD collapse with zero bad debt -- a notable achievement demonstrating effective risk management. However, a close variant (MEV Capital sdeUSD/USDC market on Morpho Blue -- same collateral type, same lending protocol) experienced 3.6% bad debt. Gauntlet's own implementation avoided this through proactive management (72% borrow reduction). One historical loss event on comparable variant above 0.5% of peak TVL but different curator. Scoring Mid as Gauntlet's own vault had zero loss. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025), [P4] [Coinfomania](https://coinfomania.com/morpho-delists-elixir-sdeusd-bad-debt/) |
| ST-PM-06 | Is a risk framework for vault curation documented? | Yes. Gauntlet VaultBook with curation methodology, risk factors, due diligence, and market allocation strategy. Clear Prime/Balanced/Frontier tiering with explicit risk disclosures. Agent-based simulations. FalconX-specific risk parameters documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [Curation Methodology](https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview), [P1] [Gauntlet FalconX Strategy](https://www.gauntlet.xyz/resources/falconx-levered-rwa-strategy-with-pareto) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Partially incentive-driven. Organic yield from lending interest + MORPHO emissions + potential incentives from underlying protocols (Maple, infiniFi points). Estimated 30-70% of yield from incentives/emissions. Would remain positive without incentives but materially lower. Credible taper plan not explicitly published. | 3 | 9 | **Improvable** | [P1] [Gauntlet VaultBook Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Moderate. USDC highly liquid but underlying collateral (syrupUSDC, PT tokens, AA_FalconXUSDC, siUSD, stcUSD) has thin or no secondary markets. Nov 2025: Frontier liquidity dropped below 1% for ~6 hours. Adaptive IRM reduced borrowing 72% within hours. Unwind relies on borrower repayment or collateral liquidation. FalconX CV tokens have limited secondary market. siUSD and stcUSD from newer protocols with limited liquidity track record. Slippage around 2-5% plausible. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Material dependency. Collateral values depend on: siUSD peg (infiniFi fractional reserve health), syrupUSDC peg (Maple institutional borrower health), stcUSD peg (Cap protocol health), wsrUSD peg (Resolv delta-neutral strategy), FalconX AA tranche value (institutional credit quality). These are interconnected with broader stablecoin/credit market health. ~30-70% of collateral depends on peg/spread maintenance, though more diversified than the previous profile. | 3 | 3 | Non-Improvable | [P1] [Morpho App](https://app.morpho.org/ethereum/vault/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e/gauntlet-usdc-frontier) |

**Protocol Mechanics Subtotal: 22.5/45 (50.0%)**
- 8 applicable questions (ST-PM-04 = N/A): 2 scored 9 (sum = 18), 6 scored 3 (sum = 18)
- Raw sum = 36 out of max 72
- Weighted = (36/72) x 45 = 22.5

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Diversified higher-risk collateral, all tokenized/wrapped: (1) AA_FalconXUSDC (34% of TVL) -- Pareto-issued senior tranche of FalconX institutional crypto-backed credit facility, curated by M11 Credit, 77% LLTV. Novel but institutionally structured. (2) siUSD (25.5%) -- infiniFi's staked fractional-reserve stablecoin, launched mid-2025, $174M TVL. No formal audit found. 91.5% LLTV. (3) syrupUSDC (15.3%) -- Maple Finance institutional lending receipt token, $2.6B+ TVL, Sherlock audited. Active Cayman injunction (on syrupBTC). 91.5% LLTV. (4) stcUSD (15.1%) -- Cap protocol staked cUSD, launched August 2025, $500M TVL, Sherlock audit contest (126K USDC). 91.5% LLTV. (5) wsrUSD (3.8%) -- Resolv wrapped savings rUSD, delta-neutral stablecoin, $344M TVL, Halborn + MixBytes audited, Immunefi bounty. 91.5% LLTV. (6) Smaller PT positions. Gauntlet has explicit tiering (Frontier), supply caps, and documented due diligence. Higher-risk per mandate but with clear on-chain limits. The FalconX AA tranche at 77% LLTV is notably more conservative than the other markets. | 3 | 3 | Non-Improvable | [P1] [Morpho App](https://app.morpho.org/ethereum/vault/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e/gauntlet-usdc-frontier), [P1] [Gauntlet FalconX Strategy](https://www.gauntlet.xyz/resources/falconx-levered-rwa-strategy-with-pareto), [P1] [Cap Sherlock Audit](https://audits.sherlock.xyz/contests/990), [P1] [Resolv Halborn Audit](https://www.halborn.com/audits/fortunafi/reservoir-protocol---wsrusd--rebalance-e8e804) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | IMPROVED from previous rating. The sdeUSD/deUSD (which collapsed 98% in Nov 2025) has been completely removed. Current collateral: syrupUSDC has maintained peg (no major depeg). siUSD, stcUSD, and AA_FalconXUSDC are newer tokens with limited stress history -- none have shown depeg >2% lasting >24h, but none have been tested in severe market stress. wsrUSD has maintained peg through Resolv's delta-neutral mechanism. PT tokens have fixed maturity so behave predictably. No current collateral has shown >10% depeg or lasting >7 days. However, several collaterals are too new to have meaningful stress data (siUSD ~9 months old, stcUSD ~7 months old). Scoring Mid: no demonstrated failure but limited stress history for most assets. | 3 | 3 | Non-Improvable | [P3] Market data, [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- No staking-based collateral in the current allocation. | N/A | N/A | N/A | Vault architecture |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | HIGH RISK: 100% of collateral is wrapped/synthetic/tokenized. AA_FalconXUSDC (credit vault receipt token), siUSD (staked fractional-reserve stablecoin), syrupUSDC (yield-bearing Maple wrapper), stcUSD (staked Cap stablecoin), wsrUSD (wrapped savings token), PT tokens (Pendle principal tokens). All involve complex dependency chains. Exceeds 60% threshold maximally. | 1 | 9 | **Improvable** | [P1] [Morpho App](https://app.morpho.org/ethereum/vault/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e/gauntlet-usdc-frontier) |

**Collateral Subtotal: 11.7/45 (25.9%)**
- 3 applicable questions (ST-C-03 = N/A): ST-C-01(3), ST-C-02(3), ST-C-04(1)
- Raw sum = 7 out of max 27
- Weighted = (7/27) x 45 = 11.7

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | All Tier-0/1: Ethereum (Tier-0), Chainlink (Tier-0 oracle). No bridges or CEX dependency. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | SINGLE ORACLE RISK. Each Morpho Blue market has one immutable oracle with no fallback. Frontier collateral types may rely on more complex oracle feeds than simple ETH/BTC. FalconX AA tranche oracle is particularly novel. | 3 | 3 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | No explicit SOC 2 Type II or ISO27001 for Gauntlet Networks disclosed. Chainlink holds enterprise certifications. FalconX (as counterparty for the AA tranche) is a well-funded crypto prime brokerage but certification status not publicly confirmed for this specific facility. | 3 | 9 | **Source Missing** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Ethereum stable. Morpho: April 2025 frontend resolved in 4 min. Nov 2025: Frontier vault operated correctly with zero bad debt despite sdeUSD exposure. Liquidity recovered within hours via adaptive IRM. Infrastructure performed well under real stress. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum: no halts >30 minutes in last 12+ months. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- No staking-based collateral. | N/A | N/A | N/A | Vault architecture |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- No staking-based collateral. | N/A | N/A | N/A | Vault architecture |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Permissionless ERC4626 redemption always available. No off-chain dependency for withdrawals. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Infrastructure Counterparty Subtotal: 35.0/45 (77.8%)**
- 6 applicable questions (ST-IC-06, ST-IC-07 = N/A): 4 scored 9 (sum = 36), 2 scored 3 (sum = 6)
- Raw sum = 42 out of max 54
- Weighted = (42/54) x 45 = 35.0

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All vault capital deployed to Morpho Blue (Tier-0) lending markets only. No CEX or direct RWA exposure. The vault's USDC is deployed into Morpho Blue markets where borrowers post various collateral types -- the collateral quality risk is captured in ST-C-01/02/04, not here. The vault itself interacts only with Morpho Blue. Collateral dependency chains extend to Pareto/FalconX, Maple, infiniFi, Cap, Resolv, and Ethena/Strata, but these are borrower-side exposures. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho App](https://app.morpho.org/ethereum/vault/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e/gauntlet-usdc-frontier), [P1] [Gauntlet FalconX Strategy](https://www.gauntlet.xyz/resources/falconx-levered-rwa-strategy-with-pareto) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Maple provides syrupUSDC incentives to attract borrowers using syrupUSDC as collateral on Morpho. MORPHO emissions flow to vault depositors. infiniFi has a points program leading to TGE. Arrangements partially disclosed but create potential conflicts (Gauntlet benefits from incentive-driven TVL flowing to vault depositors). Terms only partially disclosed across multiple counterparties. | 3 | 9 | **Improvable** | [P1] [Incentives & Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. On-chain supply caps per market. Gauntlet automated models with continuous monitoring. Current allocations show clear differentiation: FalconX at 34%, siUSD at 25.5%, syrupUSDC at 15.3%, stcUSD at 15.1% -- suggesting active cap management. Nov 2025 demonstrated effective management with 72% borrow reduction via IRM. | 9 | 9 | Non-Improvable (optimal) | [P1] [Market Allocation Strategy](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/curation-methodology-and-risk-factor-overview/market-allocation-strategy) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Moderate. Nov 2025: 72% Frontier borrow reduction within hours via adaptive IRM. However, new collateral types (AA_FalconXUSDC, siUSD, stcUSD) have thin or no secondary markets. FalconX CV tokens are particularly illiquid (institutional credit facility tokens). If borrowers default rather than repay, collateral liquidation would face significant friction. The FalconX AA tranche at 77% LLTV provides better buffer than 91.5% markets. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending. No external validators or custodians for the vault itself. Gauntlet (curator) disclosed. Underlying collateral providers disclosed: FalconX/Pareto (M11 Credit as curator), Maple Finance, infiniFi, Cap protocol, Resolv. | 9 | 9 | Non-Improvable (optimal) | Vault architecture, [P1] [Gauntlet FalconX Strategy](https://www.gauntlet.xyz/resources/falconx-levered-rwa-strategy-with-pareto) |

**Protocol Counterparty Subtotal: 33.0/45 (73.3%)**
- 3 scored 9 (sum = 27), 2 scored 3 (sum = 6)
- Raw sum = 33 out of max 45
- Weighted = (33/45) x 45 = 33.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless ERC4626 redemption. No address-level blocking. No admin pause. Withdrawal depends on market liquidity. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | CONSTRAINED. Nov 2025: Frontier liquidity dropped below 1% for ~6 hours. Average recovered to above 30% (vs Prime's 53%). Current collateral types (AA_FalconXUSDC, siUSD, stcUSD) have even thinner secondary markets than previous sdeUSD/syrupUSDC mix. ~3-10% of TVL can be absorbed without major dislocation. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | Yes. Nov 2025: Frontier liquidity dropped below 1% for ~6 hours, effectively constraining withdrawals temporarily. Resolved same day. Between 80-95% of withdrawals completed within stated period over vault lifetime. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Caps appropriately sized. Nov 2025 delays driven by utilization, not cap design. Rate model created 72% Frontier borrow reduction. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | STRESSED during Nov 2025. Frontier liquidity dropped below 1% for ~6 hours. Access remained via direct contract interaction. Conditions normalized within hours. Battle-tested but showed vulnerability. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No lockups on lender positions. PT token maturity dates affect borrower-side risk only. siUSD staking may involve withdrawal delays but this is borrower collateral, not lender funds. Less than ~10% exposure concern. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary ERC4626 redemption always available. Secondary market not required. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | Moderate to thin. USDC highly liquid but collateral types (AA_FalconXUSDC, siUSD, stcUSD, wsrUSD) have limited secondary markets. syrupUSDC has modest Curve/Uniswap liquidity. PT tokens have Pendle market liquidity. Overall depth supports ~3-10% of TVL without major impact, but worse than Prime's blue-chip collateral. | 3 | 3 | Non-Improvable | [P3] Market data |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | ELEVATED. More concerning than Prime: exotic collateral liquidation slower, Nov 2025 showed sub-1% liquidity, most markets at 91.5% LLTV give only ~8.5% buffer, 20% TVL decline showed depositor flight during stress. However, vault survived Nov 2025 with zero bad debt demonstrating effective management. Significant queues and discounting expected, losses expected to be contained but narrow margins. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |

**Liquidity Subtotal: 28.3/45 (62.9%)**
- 4 scored 9 (sum = 36), 5 scored 3 (sum = 15)
- Raw sum = 51 out of max 81
- Weighted = (51/81) x 45 = 28.3

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | Vault shares maintained 1:1 USDC claim (zero bad debt confirmed Nov 2025). TVL declined 20% from depositor exits but no share price impairment. Battle-tested during real stress event. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Low directional risk. Vault lends USDC -- dollar-denominated. Risk is bad debt from collateral failure, not market direction. However, the FalconX AA tranche involves crypto-backed institutional credit that has indirect crypto market exposure. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Immutable Adaptive Curve IRM. Nov 2025: IRM reduced Frontier borrowing 72%, restoring liquidity within hours. Demonstrated resilience. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. Gauntlet agent-based simulations. Nov 2025 served as real-world stress test -- zero bad debt despite sdeUSD collapse. Certora verified core liquidation mechanics. FalconX strategy has its own risk parameters. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side only. Lenders benefit from liquidations. Risk: insufficient/slow liquidation creating socialized bad debt. Most markets at 91.5% LLTV give only ~8.5% buffer. FalconX AA tranche at 77% LLTV provides better ~23% buffer. Exotic collateral liquidation less efficient than BTC/ETH but more diversified than previous profile. | 3 | 3 | Non-Improvable | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 39.0/45 (86.7%)**
- 4 scored 9 (sum = 36), 1 scored 3
- Raw sum = 39 out of max 45
- Weighted = (39/45) x 45 = 39.0

---

### **Strategy Total: 169.5/270 (62.8%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 22.5 | 45 | 50.0% |
| Collateral | 11.7 | 45 | 25.9% |
| Infra Counterparty | 35.0 | 45 | 77.8% |
| Protocol Counterparty | 33.0 | 45 | 73.3% |
| Liquidity | 28.3 | 45 | 62.9% |
| Market | 39.0 | 45 | 86.7% |
| **Strategy Total** | **169.5** | **270** | **62.8%** |

---

### OPERATIONS (30% Weight) -- Score: 235.0/270 (87.0%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid. Morpho Blue immutable. Vault changes require Owner multisig + timelock + Guardian. Multiple layers. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- No governance token voting for this vault. Concentration captured in S-KM-01/S-KM-03. | N/A | N/A | N/A | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Vault timelock verified at 259,200 seconds (3 days) via Morpho GraphQL API (March 2026). Guardian (3-of-7 Safe) can veto pending timelocked actions. 3-day timelock exceeds the 24-hour minimum for Low Risk scoring. Depositors have a reasonable window to react to pending changes. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API vault query (timelock: 259200), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner can appoint new Curator (subject to timelock). Withdrawals remain permissionless via ERC4626. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 3 applicable (O-G-02 = N/A): 3 scored 9 (sum = 27)
- Raw sum = 27 out of max 27
- Weighted = (27/27) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Gauntlet: Tarun Chitra (CEO), Rei Chiang (Co-founder). 50+ team. Morpho: Paul Frambot (CEO). All publicly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Team](https://www.gauntlet.xyz/our-team) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Gauntlet 50+ employees. Morpho separate team ($73.6M raised). | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet About](https://www.gauntlet.xyz/about) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Morpho: ADDMO (France). Gauntlet: Gauntlet Networks Inc. (New York, USA). Both clearly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known actions against Gauntlet Networks Inc. or Morpho entities. | 9 | 9 | Non-Improvable (optimal) | Public records |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Yes. Gauntlet 24/7 liquidity monitoring confirmed Nov 2025. ZeroShadow 24/7 SOC, Hypernative, SEAL Intel partnerships. Morpho 4-minute response April 2025. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Detailed market report published within days of Nov 2025 stress. Active VaultBook. 4-minute frontend response. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Gauntlet: Polychain, Paradigm, Ribbit Capital. Morpho: a16z, Variant, Pantera, Coinbase Ventures. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay](https://www.clay.com/dossier/gauntlet-funding) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Gauntlet manages 70+ vaults with $1.4B+ AUM including Prime, Balanced, Frontier tiers. No formal quantitative conflict-of-interest policy. Risk of routing riskier allocations to Frontier to protect Prime/Balanced vaults is elevated. | 3 | 9 | **Improvable** | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | Zero bad debt across all Gauntlet Morpho vaults since March 2024. Prior Aave advisory role: $1.6M CRV bad debt resulted from governance inaction, not Gauntlet decisions. Clean curator record. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |

**Team & Legal Subtotal: 62.5/67.5 (92.6%)**
- 8 scored 9 (sum = 72), 1 scored 3
- Raw sum = 75 out of max 81
- Weighted = (75/81) x 67.5 = 62.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive Morpho docs and Gauntlet VaultBook. Frontier tier explicitly described with risk warnings. FalconX strategy documented separately. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Docs](https://docs.morpho.org/), [P1] [VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults), [P1] [Gauntlet FalconX Strategy](https://www.gauntlet.xyz/resources/falconx-levered-rwa-strategy-with-pareto) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Liquidation mechanics, bad debt scenarios, oracle risks documented. Frontier risk profile explicitly described. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Canonical address registry. Vault on Morpho App and Gauntlet App. Etherscan-verified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Comprehensive role documentation. Changes visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves. All allocations visible on Morpho App and Etherscan. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. MetaMorphoV1_1 contract verified on Etherscan. Full source code readable. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xc582F04d8a82795aa2Ff9c8bb4c1c889fe7b754e) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated safety module. Bad debt socialized per market. Morpho DAO treasury (~$37.9M own tokens + ~$10K liquid) discretionary. No Gauntlet-specific backstop. | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/), [P3] [DeFiLlama Treasury](https://api.llama.fi/treasury/morpho) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Morpho DAO treasury per DeFiLlama: ~$37.9M own tokens (MORPHO) + ~$10K liquid stables across Ethereum and Base. Against ~$10B+ protocol TVL = ~0.38% (own tokens included). The liquid component is negligible. No vault-specific reserve disclosed. Gauntlet is well-funded ($41.8M raised) but no ring-fenced backstop. | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho), [P3] [DeFiLlama Morpho](https://defillama.com/protocol/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Gauntlet $41.8M raised, $1B valuation. Morpho $73.6M raised. Combined runway >24 months. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay](https://www.clay.com/dossier/gauntlet-funding) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | PARTIALLY RESILIENT. Nov 2025: Frontier TVL declined 20% (worse than Prime which held steady, but better than other curated vaults that fell >60%). Zero bad debt. Revenue continued. Significant but recoverable TVL drop without permanent depositor loss. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue immutable. Permissionless ERC4626 withdrawals. No proprietary off-chain services required. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Financial Resilience Subtotal: 37.5/67.5 (55.6%)**
- 2 scored 9 (sum = 18), 2 scored 3 (sum = 6), 1 scored 1
- Raw sum = 25 out of max 45
- Weighted = (25/45) x 67.5 = 37.5

---

### **Operations Total: 235.0/270 (87.0%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 67.5 | 67.5 | 100.0% |
| Team & Legal | 62.5 | 67.5 | 92.6% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 37.5 | 67.5 | 55.6% |
| **Operations Total** | **235.0** | **270** | **87.0%** |

---

## Final Score Calculation

| Category | Subcategory | Current Points | Max Points | Potential Points |
|----------|-------------|----------------|------------|------------------|
| **Security** | Smart Contract Security | 169.1 | 180 | 169.1 |
| | Key Management | 165.0 | 180 | 180.0 |
| | **Security Subtotal** | **334.1** | **360** | **349.1** |
| **Strategy** | Protocol Mechanics | 22.5 | 45 | 30.0 |
| | Collateral | 11.7 | 45 | 25.0 |
| | Infra Counterparty | 35.0 | 45 | 40.0 |
| | Protocol Counterparty | 33.0 | 45 | 39.0 |
| | Liquidity | 28.3 | 45 | 28.3 |
| | Market | 39.0 | 45 | 39.0 |
| | **Strategy Subtotal** | **169.5** | **270** | **201.3** |
| **Operations** | Governance | 67.5 | 67.5 | 67.5 |
| | Team & Legal | 62.5 | 67.5 | 67.5 |
| | Documentation | 67.5 | 67.5 | 67.5 |
| | Financial Resilience | 37.5 | 67.5 | 58.5 |
| | **Operations Subtotal** | **235.0** | **270** | **261.0** |
| **TOTAL** | | **738.6** | **900** | **811.4** |

---
