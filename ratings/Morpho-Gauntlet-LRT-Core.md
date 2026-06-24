# Morpho - Gauntlet LRT Core Vault Risk Rating

**Rating Date**: 2026-06-23
**Final Grade**: BB-
**Total Score**: 740.6/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 323.2/360 (89.8%)

#### Smart Contract Security (20% weight, 180 max points)

**NOTE: All Smart Contract Security scores are platform-level and IDENTICAL to the unaffected Gauntlet USDC Prime vault under v0.1-gamma. The Morpho Blue core is immutable (~600 LOC); the MetaMorpho V1 vault is a non-upgradeable ERC4626 contract. S-SC-10 and S-SC-11 score 3 per the v0.1-gamma verification principle (monitoring cannot automatically trigger protective actions). S-SC-06 = 9 because THIS vault held no synthetic/wstUSR collateral and was not directly impacted by the March 2026 Resolv exploit — distinct from the directly-hit USDC Core (S-SC-06=1).**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | Yes. 25+ audits from Tier-0/1 firms (ChainSecurity, Spearbit/OpenZeppelin, Zellic, Certora, Blackthorn) plus Cantina competition. Morpho Blue core (~600 LOC, immutable) and MetaMorpho framework extensively audited; Certora formal verification. This vault (0x4881…) is a MetaMorpho V1 vault from the audited factory. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0x4881Ef0BF6d2365D3dd6499ccd7532bcdBCE0658), [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | December 2025: Certora (Tier-0), Spearbit (Tier-0 via Cantina), Blackthorn for Vaults V2 adapter work. September 2025: ChainSecurity (Tier-0). Multiple Tier-0 auditors for most recent work. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable. This vault is a non-upgradeable V1 MetaMorpho contract. Vault-framework upgrades (Vaults V2, Sep-Dec 2025) were preceded by multiple Tier-0 audits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P0] [Etherscan](https://etherscan.io/address/0x4881Ef0BF6d2365D3dd6499ccd7532bcdBCE0658) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 vulnerability patched immediately with OpenZeppelin. Certora formal verification provides mathematical proof of critical invariants. All V2 audit findings resolved before deployment with re-reviews. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue core is immutable. The MetaMorpho V1 vault (0x4881…) is a non-upgradeable ERC4626 contract. Market changes require Curator + 3-day timelock (259,200s) + Guardian veto. Timelock exceeds the 24h minimum. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=259200), [P0] [Etherscan](https://etherscan.io/address/0x4881Ef0BF6d2365D3dd6499ccd7532bcdBCE0658) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss in THIS vault or in the Morpho/MetaMorpho contracts. The March 2026 Resolv USR exploit caused bad debt in Gauntlet's synthetic-collateral vaults (Frontier/Core), but LRT Core holds only LST/LRT collateral (weETH, wstETH) and no wstUSR/synthetic stablecoins. Verified on-chain: LRT Core sharePriceUsd tracked ETH normally across the Resolv window (Mar 16–28 2026, $1,990→$2,193) with no NAV impairment/discontinuity. Distinct from USDC Core (S-SC-06=1). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (historicalState sharePriceUsd Mar 2026, no impairment), [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho operates as ADDMO (French nonprofit). Gauntlet Networks Inc. is a well-funded ($41.8M raised, $1B valuation) US company with public leadership. No credible allegations against either entity. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P2] [Gauntlet About](https://www.gauntlet.xyz/about) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No evidence of timelock reductions. The vault has a 3-day timelock (259,200 seconds), verified via Morpho GraphQL API (June 2026). No reductions observed. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=259200) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Morpho runs dual active public bounties: Cantina ($2.5M max) and Immunefi ($2.5M max for Morpho Blue, $1.5M for MetaMorpho/periphery). Both are Tier-0 platforms. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3), [P1] [Immunefi Bounty](https://immunefi.com/bug-bounty/morpho/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Gauntlet partners with Hypernative (real-time monitoring), ZeroShadow (24/7 vSOC), Chainalysis, and SEAL Intel; Morpho runs internal monitoring bots. Per the v0.1-gamma verification principle, monitoring cannot automatically trigger protective actions — no on-chain circuit breakers, no automated pause; all responses require manual human intervention. The March 2026 Resolv exploit showed (in sister vaults) that the Public Allocator's automated flows are not covered by any automated halt. Platform-level Mid. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. Morpho Blue prioritizes immutability; Guardian can only veto pending timelocked actions, not pause markets. Market-level isolation provides containment but does not cover automated allocation flows. No demonstrated circuit-breaker failure in THIS vault (unlike USDC Core, S-SC-11=1). Mid (3). | 3 | 3 | Non-Improvable | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Smart Contract Security Subtotal: 158.2/180 (87.9%)**
- 9 questions scored 9 (sum = 81), 2 questions scored 3 (sum = 6)
- Raw sum = 87 out of max 99
- Weighted = (87/99) x 180 = 158.2

---

#### Key Management & Permissions (20% weight, 180 max points)

**NOTE: All Key Management scores are IDENTICAL to the other Gauntlet Morpho vaults (USDC Core/Prime). Same Owner 4-of-7 Safe (0xC684…), same Guardian 3-of-7 Safe (0x7084…), same Curator 3-of-7 Safe (0x9E33…), same 3-day timelock. Verified on-chain via the Safe Transaction Service and Morpho GraphQL API (2026-06-23).**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Owner: Gnosis Safe 4-of-7 (0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec), verified (Safe v1.3.0, 7 owners, threshold=4, nonce=508). Guardian: Safe 3-of-7 (0x7084bF4dB6c21e1834dD6482f6056a39A33584cD, v1.4.1, nonce=4). Curator: Safe 3-of-7 (0x9E33faAE38ff641094fa68c65c2cE600b3410585, v1.4.1, nonce=454). Timelock 259,200s (3 days). All changes visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API Guardian](https://api.safe.global/tx-service/eth/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/), [P0] [Safe API Curator](https://api.safe.global/tx-service/eth/api/v1/safes/0x9E33faAE38ff641094fa68c65c2cE600b3410585/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Vault is non-upgradeable. Moving funds requires Morpho Blue immutable logic. Market changes require multisig + 3-day timelock + Guardian. Permissionless ERC4626 redemption always available. Owner is 4-of-7 (threshold >=3, signers >=5), timelock >=24h. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=259200, owner threshold=4), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner 4-of-7 Safe (7 distinct owners, threshold=4) meets the >=4-of-7 Low Risk minimum. Guardian and Curator are each 3-of-7. Gauntlet publicly identified as operator. Several addresses overlap across the three Gauntlet multisigs (all Gauntlet team). | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking. No pause on Morpho Blue (immutable). Guardian can only revoke pending timelocked actions. Withdrawals always permissionless via direct contract interaction. Rules public. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets in non-custodial Morpho Blue contracts on Ethereum. Permissionless ERC4626 redemption. No off-chain custody. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Vault funds held in Morpho Blue markets, segregated from treasury/ops. Performance fee (10%) accrued on-chain transparently. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (fee=0.1), [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain enforced whitelist of Morpho Blue markets only. Current markets (GraphQL, June 2026): weETH/WETH (94.5% LLTV), wstETH/WETH (96.5% and 94.5% LLTV), WBTC/WETH, cbBTC/WETH, LBTC/WETH (91.5% LLTV), plus an idle WETH market. New markets require Curator + 3-day timelock + Guardian veto, with on-chain supply caps. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (allocation data), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Gauntlet's posture includes ZeroShadow (vSOC), Hypernative, SEAL Intel. Morpho docs include emergency procedures. However, no public, vault-specific incident playbook with explicit key-rotation steps or tabletop-exercise results has been published. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Morpho Emergency Procedures](https://docs.morpho.org/curate/emergency/) |

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

### STRATEGY (30% Weight) -- Score: 183.4/270 (67.9%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from overcollateralized WETH lending against LST/LRT collateral (weETH, wstETH). 100% mandate-aligned — the "LRT Core" mandate is ETH lending against (re)staking collateral. Current net APY ~1.46% (gross ~1.63%, 10% fee). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (netApy=0.0146, fee=0.1), [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss can occur in severe but plausible single-shock events: collateral is ~100% LST/LRT at thin 94.5–96.5% LLTV (≈3.5–5.5% buffer). A weETH/wstETH depeg vs ETH (e.g., a restaking-slashing or LST-withdrawal-queue dislocation) within that buffer could socialize bad debt. ETH/LST correlation is high but buffers are thinner than blue-chip BTC markets. Mid (3). | 3 | 9 | **Improvable** | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P0] Morpho GraphQL API (weETH LLTV 0.945, wstETH LLTV 0.965/0.945) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault simply lends WETH. No rehypothecation of depositor funds. Effective leverage 1.0x. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | LRT Core itself has no permanent-loss event. However, per the "comparable variant" guidance ("same codebase with parameter changes only = comparable; same curator"), Gauntlet USDC Frontier/Core ARE comparable variants (same MetaMorpho V1 codebase, same curator, differing only in collateral parameters) and experienced confirmed Resolv bad debt. Root cause (synthetic/wstUSR collateral) is structurally excluded from LRT Core's LST/LRT mandate. Maps to Mid (3) — identical to the unaffected Gauntlet USDC Prime. | 3 | 9 | **Improvable** | [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit), [P4] [OAK Research](https://oakresearch.io/en/analyses/investigations/the-resolv-usr-hack-curators-face-their-responsibilities) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Gauntlet publishes comprehensive curation methodology via VaultBook (risk factors, due diligence, market allocation strategy), quantitative insolvency limits, and a tiering system (Prime/Balanced/Core/Frontier). | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults), [P1] [Curation Methodology](https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. Yield is organic from WETH lending demand against (re)staking collateral (net APY ~1.46% after 10% fee). No emissions required for base yield. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (netApy=0.0146, apy=0.0163, fee=0.1) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | WETH is deeply liquid, but this is a small (~$3M) vault lending into utilized markets, and full immediate exit depends on borrower repayment/market liquidity. Most of the position can be unwound over the stated horizon, but near-total instant exit is not guaranteed and the vault has no demonstrated large-exit track record. Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (allocation/utilization) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | The vault's own yield is lending interest (no carry/basis trade). It lends against peg-dependent LSTs/LRTs, but that risk is captured in collateral/oracle/market questions. The lending mechanic itself is not a carry/peg trade. Low (9). | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Yes. Morpho's Public Allocator / `supplyOnBehalf` can route capital into whitelisted markets. Supply caps limit per-market exposure but no automatic kill-switch exists for abnormal conditions; halting requires manual curator intervention. Same Public Allocator infrastructure as all Morpho vaults. Mid (3). | 3 | 9 | **Improvable** | [P1] [Morpho Public Allocator](https://docs.morpho.org/curate/concepts/public-allocator/), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |

**Protocol Mechanics Subtotal: 31.7/45 (70.4%)**
- 9 applicable questions (ST-PM-04 = N/A): 5 scored 9 (sum = 45), 4 scored 3 (sum = 12)
- Raw sum = 57 out of max 81
- Weighted = (57/81) x 45 = 31.67 ≈ 31.7

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Collateral is ~100% LST/LRT: Ether.fi weETH (restaked-ETH LRT, ~75.7% of TVL, 94.5% LLTV) and Lido wstETH (largest LST, ~24%, 96.5%/94.5% LLTV), plus near-zero BTC dust (WBTC/cbBTC/LBTC <$70 each). wstETH is established/blue-chip (BBB+ SR-tier LST); weETH is newer and carries EigenLayer restaking-slashing risk beyond a plain LST. Each is tiered via on-chain LLTV and supply caps, but weETH is a higher-risk restaking asset and dominates. Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (weETH $2.27M, wstETH $0.70M+$0.02M), [P1] [weETH Collateral Risk (PrismaRisk)](https://hackmd.io/@PrismaRisk/weETH) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | wstETH has a strong track record (tracked stETH/ETH through Lido's July 2025 mass-exit with 235k+ stETH in queues, no >2% sustained depeg). weETH has generally held a tight peg to ETH (deep liquidity across 400+ protocols) with no >2% sustained depeg lasting >24h in the last 12 months; brief ecosystem-wide LRT stress occurred (e.g., April 2026) but weETH itself did not show a >2% sustained depeg. Mid (3) — weETH's shorter, less-tested peg history and restaking layer keep it below the Low bar even though no qualifying depeg occurred. | 3 | 9 | **Improvable** | [P1] [weETH Collateral Risk (PrismaRisk)](https://hackmd.io/@PrismaRisk/weETH), [P3] [Chainlink weETH/ETH Feed](https://data.chain.link/feeds/ethereum/mainnet/weeth-eth) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Applicable: weETH (Ether.fi restaked ETH, EigenLayer slashing live since April 2025) and wstETH (Lido, 30+ operators) are staking-based. Lido slashing is well-mitigated (coverage fund, diversified operators). For weETH, EigenLayer restaking adds an extra slashing layer; major slashing events have been rare but the risk is now live, and dedicated depositor-loss buffers/insurance for restaking are limited. Mid (3). | 3 | 9 | **Improvable** | [P4] [EigenLayer slashing live Apr 2025 (CoinDesk)](https://www.coindesk.com/tech/2025/04/17/eigenlayer-adds-key-slashing-feature-completing-original-vision), [P1] [weETH Collateral Risk (PrismaRisk)](https://hackmd.io/@PrismaRisk/weETH) |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | Low. Per the framework definition, "bridged or wrapped" EXCLUDES protocol receipt tokens / LSTs (stETH, aTokens) and WETH (thin wrapper) — their risk is captured elsewhere. weETH and wstETH are LST/LRT receipt tokens (excluded), and the loan asset WETH is excluded. Only the near-zero BTC dust (WBTC/cbBTC/LBTC, <$70 combined) is wrapped, i.e. far below 20% of TVL. Low (9). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (BTC markets <$70 each; weETH/wstETH = LST/LRT receipts, excluded) |

**Collateral Subtotal: 22.5/45 (50.0%)**
- 1 question scored 9 (sum = 9), 3 questions scored 3 (sum = 9)
- Raw sum = 18 out of max 36
- Weighted = (18/36) x 45 = 22.5

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Chain/oracle dependencies are Tier-0: Ethereum (Tier-0), Chainlink-based Morpho oracle adapters plus LST/LRT exchange-rate feeds. No bridges, no CEX operational dependency. All explicitly identifiable on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | **Hardcoded/immutable oracle check (mandatory):** Each Morpho Blue market uses an immutable oracle that cannot be corrected post-deployment. The markets price ETH/wstETH/weETH via Chainlink (Tier-0) plus LST exchange-rate feeds — battle-tested deep-liquidity assets where material depeg of ETH/wstETH is historically unprecedented (weETH is newer but tightly correlated). No fallback exists; immutability removes any ability to respond to unprecedented events. Per the mandatory check (hardcoded oracle for battle-tested deep-liquidity assets), caps at Mid (3) — consistent with Prime. | 3 | 3 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/), [P3] [Chainlink weETH/ETH Feed](https://data.chain.link/feeds/ethereum/mainnet/weeth-eth) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Gauntlet operates off-chain risk/allocation engines and claims an institutional-grade posture (Hypernative, ZeroShadow, Chainalysis, SEAL Intel) but no SOC 2 Type II or ISO27001 certification for Gauntlet Networks Inc. is publicly disclosed. Chainlink holds enterprise certifications. Mid (3). | 3 | 9 | **Source Missing** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Ethereum: no significant halts. Morpho: April 2025 frontend issue resolved in ~4 minutes; November 2025 stress handled with market isolation; March 2026 Resolv exploit did NOT affect LRT Core (no synthetic collateral). Past incidents caused at most short-lived UX degradation for this vault, not blocked withdrawals or losses. Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum (Tier-0) has had no chain halts >30 minutes in the last 12+ months. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Relevant for weETH (Ether.fi/EigenLayer) and wstETH (Lido), which are ~100% of collateral. No material slashing event impacting these validator sets caused depositor loss in the last 12 months; EigenLayer slashing went live April 2025 with only rare, trivial events. Low (9). | 9 | 9 | Non-Improvable (optimal) | [P4] [EigenLayer slashing live Apr 2025 (CoinDesk)](https://www.coindesk.com/tech/2025/04/17/eigenlayer-adds-key-slashing-feature-completing-original-vision), [P3] Lido / Ether.fi slashing data |
| ST-IC-07 | Are validators diverse geographically and by operator? | wstETH (Lido) uses 30+ diversified operators across jurisdictions (no single operator >25% effective). weETH (Ether.fi) uses diversified node operators; EigenLayer restaking concentration is a noted structural risk but the relevant operator sets are not single-operator dominated. Low (9). | 9 | 9 | Non-Improvable (optimal) | [P3] Lido / Ether.fi operator data, [P1] [weETH Collateral Risk (PrismaRisk)](https://hackmd.io/@PrismaRisk/weETH) |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No single infra component is a single point of failure. Permissionless ERC4626 redemption is always available, so no component can block withdrawals. The immutable-oracle / single-collateral risk is captured in ST-IC-02 and ST-C; consistent with every comparable Morpho vault (Prime/Steakhouse all 9). Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P0] Morpho GraphQL API |
| ST-IC-09 | How robust is the cross-chain messaging or bridge verification setup? | N/A -- The vault operates solely on Ethereum with no cross-chain messaging or bridge dependency. | N/A | N/A | N/A | [P0] Morpho GraphQL API (single-chain Ethereum vault) |
| ST-IC-10 | Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting? | N/A -- No cross-chain escrow, minting, or bridge mechanics; this is pure on-chain Ethereum lending. | N/A | N/A | N/A | [P0] Morpho GraphQL API (single-chain Ethereum vault) |
| ST-IC-11 | Is the off-chain verification infrastructure resilient to data-source manipulation? | N/A -- No off-chain cross-chain verification infrastructure; collateral is priced via on-chain Chainlink oracle adapters (covered in ST-IC-02). | N/A | N/A | N/A | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |

**Infrastructure Counterparty Subtotal: 37.5/45 (83.3%)**
- 8 of 11 questions scored (ST-IC-09/10/11 = N/A): 6 scored 9 (sum = 54), 2 scored 3 (sum = 6)
- Raw sum = 60 out of max 72
- Weighted = (60/72) x 45 = 37.5

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Capital is deployed to Morpho Blue (Tier-0) markets. Collateral dependency chains extend to Ether.fi (weETH / EigenLayer restaking) and Lido (wstETH) — both established (>12 months, >$50M) protocols, with weETH's restaking layer being the newest dependency. No CEX or RWA exposure. All venues disclosed and on-chain. Mid (3) — material reliance on the newer restaking venue (Ether.fi/EigenLayer) keeps this below Low. | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (allocation data), [P1] [weETH Collateral Risk (PrismaRisk)](https://hackmd.io/@PrismaRisk/weETH) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Performance fee (10%) documented and verified on-chain. Any collateral-protocol incentives are publicly visible on the Morpho app. No hidden rebates found. Low (9). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (fee=0.1) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | On-chain supply caps per market exist (e.g., weETH cap ~$13.2M, wstETH caps ~$82M/$165M). Caps are enforced at the vault layer; the same Public Allocator caveat (caps can be reached via supplyOnBehalf in stress) applies platform-wide, but per-market caps are clearly defined. Low (9). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (supplyCapUsd per market) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Lending positions unwind as borrowers repay; the loan asset (WETH) is deeply liquid. Markets run at utilization and the vault is small/untested for large exits, so some positions may require longer lead times under stress. Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (allocation/utilization) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending. No external validators, custodians, or asset managers operate the vault. Gauntlet (curator) disclosed. Underlying collateral issuers (Ether.fi, Lido) are publicly known. Deal Breaker does not trigger. | 9 | 9 | Non-Improvable (optimal) | Vault architecture |

**Protocol Counterparty Subtotal: 33.0/45 (73.3%)**
- 3 questions scored 9 (sum = 27), 2 questions scored 3 (sum = 6)
- Raw sum = 33 out of max 45
- Weighted = (33/45) x 45 = 33.0

---

#### Liquidity (5% weight, 45 max points)

**Withdrawal baseline:** Morpho vault withdrawals are permissionless on-chain (ERC4626) subject to underlying market liquidity (idle WETH plus borrower repayment); design-implied "instant under normal utilization."

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain ERC4626 redemption. No address-level blocking, no admin pause. Withdrawal depends on market liquidity (idle WETH across markets). Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | The vault is small (~$3M) and lends into utilized markets, so only idle WETH is immediately withdrawable; WETH is deeply liquid so staggered exits clear, but near-total instant exit at high utilization is not guaranteed. Mid (3). | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API (allocation data) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No documented withdrawal freezes for this vault. It was not impacted by the March 2026 Resolv exploit. As a small, relatively young WETH vault, it has limited withdrawal time-series, but no qualifying freeze occurred. Low (9). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (historicalState, no impairment) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Caps are sized relative to TVL (per-market caps far exceed current $3M allocations). No history of caps being used to block exits. Low (9). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (supplyCapUsd per market) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | No demonstrated stress-resilience track record for THIS small vault. Per the framework's "favor demonstrated history over uncertainty" rule, an untested vault scores Mid (3) rather than Low — the design supports orderly exits but stress behavior is not proven for this vault. Mid (3). | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure WETH lending with no lockups, vesting, or bridge dependencies. Withdrawal speed limited only by market utilization. Low (9). | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary ERC4626 redemption is always available and the redeemed asset (WETH) is among the most liquid crypto assets. Holders do not depend on a secondary market for the gtLRTcore share. Low (9). | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | The loan/redeem asset (WETH) is deeply liquid, and the collateral tokens (weETH, wstETH) have deep secondary markets (weETH used across 400+ protocols; wstETH is the largest LST). However, at ~$3M the vault is small and the gtLRTcore share is thinly traded; liquidation depth for weETH/wstETH supports well over ~10% of this small TVL. Given the small size and untested depth-under-stress, Mid (3) conservatively. | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API, [P1] [weETH Collateral Risk (PrismaRisk)](https://hackmd.io/@PrismaRisk/weETH) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | A run would cause temporary queues and rate spikes; losses are contained by per-market isolation and caps, with no high leverage. But this small vault has no demonstrated bank-run resilience, so per the framework Mid (3) rather than Low. Mid (3). | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API |

**Liquidity Subtotal: 31.7/45 (70.4%)**
- 5 questions scored 9 (sum = 45), 4 questions scored 3 (sum = 12)
- Raw sum = 57 out of max 81
- Weighted = (57/81) x 45 = 31.67 ≈ 31.7

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | The gtLRTcore share is an ERC4626 NAV claim (≈ WETH-equivalent + accrued yield), not a pegged token. It has no demonstrated stress-test history (small, young vault); on-chain it tracked ETH normally through the March 2026 Resolv window with no impairment, but a deliberate stress test has not occurred. Per the framework's "favor demonstrated history" rule, untested → Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (sharePriceUsd history) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Low. The vault lends WETH and is repaid in WETH; deposits/returns are ETH-denominated with no leverage and no directional bet within the vault's terms. Loss risk is bad debt from borrower default requiring collateral to breach the thin LLTV buffer. Low (9). | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Immutable Adaptive Curve IRM per market; rates steepen as utilization rises. No history of prolonged ≥95% utilization or yield cliffs for this vault. Generally robust. Low (9). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API, [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Gauntlet uses agent-based simulations and targets insolvent-debt limits, but vault-specific stress modeling for the weETH/wstETH LRT collateral set (including EigenLayer restaking-slashing scenarios) is not publicly demonstrated for this vault. Mid (3). | 3 | 9 | **Source Missing** | [P1] [Gauntlet Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side risk. Markets sit at high LLTV (94.5–96.5%, thin 3.5–5.5% buffer), so a sharp weETH/wstETH-vs-ETH dislocation could trigger forced liquidations and potential bad debt; bounded by caps and market isolation but the thin buffer on (re)staking collateral is a real risk. Mid (3). | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (LLTV data), [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 27.0/45 (60.0%)**
- 2 questions scored 9 (sum = 18), 3 questions scored 3 (sum = 9)
- Raw sum = 27 out of max 45
- Weighted = (27/45) x 45 = 27.0

---

### **Strategy Total: 183.4/270 (67.9%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 31.7 | 45 | 70.4% |
| Collateral | 22.5 | 45 | 50.0% |
| Infra Counterparty | 37.5 | 45 | 83.3% |
| Protocol Counterparty | 33.0 | 45 | 73.3% |
| Liquidity | 31.7 | 45 | 70.4% |
| Market | 27.0 | 45 | 60.0% |
| **Strategy Total** | **183.4** | **270** | **67.9%** |

---

### OPERATIONS (30% Weight) -- Score: 234.0/270 (86.7%)

**NOTE: All Operations scores are IDENTICAL to the unaffected Gauntlet USDC Prime vault — same curator (Gauntlet), same team, same legal entity, same governance model (4-of-7 Owner / 3-of-7 Guardian / 3-of-7 Curator, 3-day timelock), same documentation, same treasury. O-FR-04 = 9 because LRT Core was not impacted by Resolv (TVL fluctuated only with ETH price); O-TL-09 = 3 reflects the Gauntlet manager-entity loss history (Resolv at sister vaults), identical to Prime.**

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
| O-TL-05 | Is there an on-call and incident response process for core teams? | Gauntlet has 24/7 on-call (ZeroShadow vSOC, Hypernative, SEAL Intel). However, the framework requires incident response to halt automated allocation within SLA; the March 2026 Resolv exploit showed (in sister vaults) that automated allocation continued supplying broken markets for hours — response did not halt automated flows within SLA, and the same Public Allocator infrastructure applies here. Mid (3). | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P4] [Protos - Resolv](https://protos.com/resolv-hack-shows-defi-learned-nothing-from-last-contagion/) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Gauntlet publishes timely market reports and VaultBook documentation, acknowledged and managed the Resolv incident at sister vaults, and Morpho responded in ~4 minutes to the April 2025 frontend issue. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Gauntlet: $41.8M from Polychain, Paradigm, Ribbit Capital ($1B valuation). Morpho: a16z, Variant, Pantera, Coinbase Ventures ($73.6M). All disclosed. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay - Gauntlet Funding](https://www.clay.com/dossier/gauntlet-funding) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Gauntlet manages 70+ vaults / $1.3B+ AUM across Prime/Balanced/Core/Frontier tiers. Structural mitigations (tiered system, automated allocation, VaultBook) exist, but no formal quantitative conflict-of-interest policy is published. Mid (3). | 3 | 9 | **Improvable** | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | Yes — at the manager-entity level. The March 2026 Resolv USR exploit caused confirmed bad debt in Gauntlet-curated Frontier/Core vaults. LRT Core itself had zero losses (LST/LRT-only mandate, no USR exposure). This is "one historical loss incident" followed by demonstrable risk isolation (the tiered system worked; LRT Core unaffected). Mid (3) — identical to the unaffected Gauntlet USDC Prime. | 3 | 9 | **Improvable** | [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit), [P4] [OAK Research](https://oakresearch.io/en/analyses/investigations/the-resolv-usr-hack-curators-face-their-responsibilities) |

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
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves and proof-of-liabilities (borrows) visible on Morpho App, Etherscan, and the Morpho GraphQL API. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0x4881Ef0BF6d2365D3dd6499ccd7532bcdBCE0658), [P0] Morpho GraphQL API |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. Vault contract (0x4881…) is a MetaMorpho V1 deployment verified on Etherscan; Morpho Blue (0xBBBB…) verified. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0x4881Ef0BF6d2365D3dd6499ccd7532bcdBCE0658) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions, all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated, ring-fenced safety module with binding activation rules. Bad debt is socialized per market. Morpho DAO treasury is discretionary via governance. Mid (3). | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Insufficient. Morpho DAO treasury is ~$23.4M, essentially entirely in MORPHO tokens (DeFiLlama: ~$23.39M OwnTokens + ~$3.7K non-own, June 2026). Against ~$10B+ protocol-wide TVL this is <1% and dominated by a volatile native token. No vault-specific reserve. High (1). | 1 | 9 | **Source Missing** | [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Gauntlet ($41.8M raised, $1B valuation) and Morpho ($73.6M raised) both have sustainable revenue and combined runway >24 months. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay - Gauntlet Funding](https://www.clay.com/dossier/gauntlet-funding) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | Resilient for THIS vault. LRT Core was unaffected by the March 2026 Resolv exploit (no synthetic collateral); across the Resolv window TVL fluctuated only with ETH price (~$19M–$27M) with no impairment, and the vault remains functional with permissionless withdrawals. No depositor haircut or buffer depletion occurred. Low (9) — identical to the unaffected Gauntlet USDC Prime. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (historicalState totalAssetsUsd/sharePriceUsd Mar 2026), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue is immutable; permissionless ERC4626 withdrawals; no proprietary off-chain services required for core operations. If Gauntlet disappeared, existing allocations persist and users can withdraw. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Financial Resilience Subtotal: 46.5/67.5 (68.9%)**
- 3 questions scored 9 (sum = 27), 1 question scored 3 (sum = 3), 1 question scored 1 (sum = 1)
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
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 57 | 81 | 31.7 | 45 | 70.4% |
| | Collateral (4 Q) | 18 | 36 | 22.5 | 45 | 50.0% |
| | Infra Counterparty (8 of 11 Q scored) | 60 | 72 | 37.5 | 45 | 83.3% |
| | Protocol Counterparty (5 Q) | 33 | 45 | 33.0 | 45 | 73.3% |
| | Liquidity (9 Q) | 57 | 81 | 31.7 | 45 | 70.4% |
| | Market (5 Q) | 27 | 45 | 27.0 | 45 | 60.0% |
| | **Strategy Subtotal** | | | **183.4** | **270** | **67.9%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 63 | 81 | 52.5 | 67.5 | 77.8% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 31 | 45 | 46.5 | 67.5 | 68.9% |
| | **Operations Subtotal** | | | **234.0** | **270** | **86.7%** |
| **TOTAL** | | | | **740.6** | **900** | **82.3%** |

---

