# Morpho - Gauntlet EURC Core Vault Risk Rating

**Rating Date**: 2026-04-09
**Final Grade**: BB-
**Total Score**: 740.8/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-beta

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 323.2/360 (89.8%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 25+ audits from Tier-0/1 firms including ChainSecurity, Spearbit/OpenZeppelin, Zellic, Certora, Blackthorn, plus Cantina competition. Both Morpho Blue core and MetaMorpho/Vaults V2 framework extensively audited. Formal verification by Certora. The Gauntlet EURC Core vault (0x2ed1...) is a MetaMorphoV1_1 vault deployed via the audited MetaMorpho factory. Verified on Etherscan (Solidity v0.8.26). | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0x2ed10624315b74a78f11FAbedAa1A228c198aEfB), [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | December 2025: Certora (Tier-0), Spearbit (Tier-0 via Cantina), Blackthorn for Vaults V2 MarketV1AdapterV2. September 2025: ChainSecurity (Tier-0) for Vaults V2 core. Multiple Tier-0 auditors for most recent work. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable (~600 LOC). Every vault upgrade in last 12 months (Vaults V2 Sep-Dec 2025) was preceded by multiple audits from Tier-0 firms. The EURC Core vault is a V1_1 vault (non-upgradeable). | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P0] [Etherscan MetaMorphoV1_1](https://etherscan.io/address/0x2ed10624315b74a78f11FAbedAa1A228c198aEfB) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 vulnerability patched immediately with OpenZeppelin. Certora formal verification provides mathematical proof of critical invariants. All V2 audit findings resolved before deployment with multiple re-reviews. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue core is immutable. MetaMorphoV1_1 vault (0x2ed1...) is a non-upgradeable ERC4626 contract. Market changes require Curator + 3-day timelock (259,200s) + Guardian approval. Timelock exceeds 24h minimum. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=259200), [P0] [Etherscan](https://etherscan.io/address/0x2ed10624315b74a78f11FAbedAa1A228c198aEfB) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No exploit or bug in Morpho Blue or MetaMorpho smart contracts has caused user fund loss. The March 2026 Resolv USR exploit was an external token failure, NOT a Morpho smart contract exploit. EURC Core had zero exposure. April 2025 frontend vulnerability ($2.6M) intercepted by white hat, all funds returned. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho operates as ADDMO, a French nonprofit association. Gauntlet Networks Inc. is a well-funded ($41.8M raised, $1B valuation) US-based company with public leadership. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P2] [Gauntlet About](https://www.gauntlet.xyz/about) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No evidence of timelock reductions. The EURC Core vault has a confirmed 3-day timelock (259,200 seconds), verified via Morpho GraphQL API (April 2026). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=259200) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Morpho runs dual active public bounties: (1) Cantina with $2.5M max payout for critical vulnerabilities; (2) Immunefi with $2.5M max payout for Morpho Blue, $1.5M for MetaMorpho/periphery. Both are Tier-0 platforms. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3), [P1] [Immunefi Bounty](https://immunefi.com/bug-bounty/morpho/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Gauntlet partners with Hypernative (real-time monitoring), ZeroShadow (24/7 vSOC), Chainalysis, and SEAL Intel. However, monitoring exists but cannot automatically trigger protective actions -- no on-chain circuit breakers, no automated pause capability. During March 2026 Resolv exploit, the Public Allocator on Frontier vaults continued auto-supplying capital for hours post-exploit, demonstrating that monitoring alerts are NOT connected to automated protective actions. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Building Institutional Security](https://www.gauntlet.xyz/resources/building-an-institutional-grade-security-posture-at-gauntlet) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. Morpho Blue prioritizes immutability over admin controls. Guardian can manually veto pending timelocked actions but cannot pause the protocol. Market-level isolation provides containment. | 3 | 3 | Non-Improvable | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Smart Contract Security Subtotal: 158.2/180 (87.9%)**
- 9 questions scored 9 (sum = 81), 2 questions scored 3 (sum = 6)
- Raw sum = 87 out of max 99
- Weighted = (87/99) x 180 = 158.2

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Owner: Gnosis Safe 4-of-7 multisig (0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec), verified on-chain (Safe v1.3.0, 7 distinct owner addresses, threshold=4, nonce=506). Guardian: Gnosis Safe 3-of-7 multisig (0x7084bF4dB6c21e1834dD6482f6056a39A33584cD), verified (Safe v1.4.1, nonce=3). Curator: Gnosis Safe 3-of-7 multisig (0x9E33faAE38ff641094fa68c65c2cE600b3410585), verified (Safe v1.4.1, nonce=363). Timelock: 259,200 seconds (3 days). All changes visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API Guardian](https://api.safe.global/tx-service/eth/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/), [P0] [Safe API Curator](https://api.safe.global/tx-service/eth/api/v1/safes/0x9E33faAE38ff641094fa68c65c2cE600b3410585/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Vault contract is non-upgradeable. Moving user funds requires going through Morpho Blue immutable contract logic. Market changes require multisig + 3-day timelock + Guardian. Permissionless redemption always available via ERC4626. Owner multisig is 4-of-7 (threshold >= 3, signers >= 5). Timelock 259,200s (3 days) >= 24h. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=259200, owner threshold=4), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner multisig is 4-of-7 Safe (verified: 7 distinct owner addresses, threshold=4). This meets >=4-of-7 minimum for Low Risk. Guardian is 3-of-7. Curator is 3-of-7. Gauntlet is publicly identified as the entity operating these multisigs. Five addresses overlap across Owner/Guardian/Curator multisigs. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API Guardian](https://api.safe.global/tx-service/eth/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking capability. No pause function on Morpho Blue (immutable). Guardian can only revoke pending timelocked actions. Withdrawals always permissionless via direct smart contract interaction. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets held in non-custodial Morpho Blue contracts on Ethereum. Permissionless redemption via ERC4626. No off-chain custody component. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. Vault funds are held in Morpho Blue markets, separate from any treasury or operational wallets. Performance fee accrued on-chain transparently (10%). Morpho is a nonprofit with no profit extraction from protocol operations. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (fee=0.1), [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain enforced whitelist of Morpho Blue markets only. Current markets verified via GraphQL API: WBTC/EURC (86% LLTV, $10M cap), cbBTC/EURC (86% LLTV, no cap set), wstETH/EURC (86% LLTV, $4M cap), WETH/EURC (86% LLTV, $2.5M cap), plus an idle EURC market. New market additions require Curator approval + 3-day timelock + Guardian veto. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (allocation data), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Gauntlet's institutional security posture includes partnerships with ZeroShadow (24/7 vSOC), Hypernative (automated response), and SEAL Intel. However, no public, vault-specific incident playbook with explicit key rotation procedures or tabletop exercise results has been published. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Morpho Emergency Procedures](https://docs.morpho.org/curate/emergency/) |

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

### STRATEGY (30% Weight) -- Score: 192.6/270 (71.3%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from overcollateralized EURC lending against crypto collateral (WBTC, cbBTC, wstETH, WETH). 100% mandate-aligned. The Core vault targets conservative exposure. Current net APY ~1.59%. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (netApy=0.0159), [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail shocks: simultaneous BTC/ETH crash exceeding the liquidation buffer (86% LLTV provides ~14% buffer), oracle manipulation on immutable oracle, or catastrophic wrapped-asset custodian failure. Bad debt per market is isolated and socialized among lenders of that specific market. EURC depegging from EUR would not directly cause bad debt but would affect dollar-denominated TVL. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault simply lends EURC. No rehypothecation of depositor funds. Effective leverage: 1.0x. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | EURC Core vault itself has zero bad debt. However, per framework "comparable variant" guidance, Gauntlet USDC Frontier IS a comparable variant -- same MetaMorpho codebase, same curator, differing only in collateral parameters and loan asset. Frontier experienced confirmed bad debt (~$7.5M+) during March 2026 Resolv USR exploit. Root cause (USR collateral) is structurally excluded from Core mandate. | 3 | 9 | **Improvable** | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Gauntlet publishes comprehensive curation methodology via VaultBook, including risk factor overviews, due diligence processes, and market allocation strategy. Quantitative limits for insolvency risk. Clear tiering system (Prime/Balanced/Frontier/Core). | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults), [P1] [Curation Methodology](https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. Yield is entirely organic from EURC lending demand. No emissions or token incentives for base yield. Current net APY ~1.59% (10% performance fee applied). Yield is modest but entirely organic. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (netApy=0.0159, fee=0.1) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | EURC is a lower-liquidity stablecoin compared to USDC/USDT. At $5.02M TVL, the position is small enough that unwinding should not cause material slippage. However, EURC DeFi liquidity is limited -- no deep secondary markets comparable to USDC. Under conservative assumptions, most of the position can be unwound within stated horizon with moderate slippage. | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (totalAssetsUsd=$5.02M), [P3] EURC market data |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. Pure lending interest from overcollateralized borrower demand. No basis trade, peg arbitrage, or funding rate dependency. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Yes. Two allocators registered: 0xfd32fA2ca22c76dD6E550706Ad913FC6CE91c75D and 0x8D590845B234C1060751D4Bdc21c8bD24DF03fA0. Supply caps per market limit maximum exposure, but no automatic kill-switch exists for abnormal conditions. During March 2026 Resolv exploit, similar automated allocation infrastructure on Frontier vaults continued auto-supplying capital to broken markets. Halting requires manual curator intervention. | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (allocators data), [P1] [Morpho Public Allocator](https://docs.morpho.org/curate/concepts/public-allocator/) |

**Protocol Mechanics Subtotal: 35.0/45 (77.8%)**
- 9 applicable questions (ST-PM-04 = N/A), 6 scored 9 (sum = 54), 3 scored 3 (sum = 9)
- Raw sum = 63 out of max 81
- Weighted = (63/81) x 45 = 35.0

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | WBTC (BitGo/BiT Global custody, $4.92M, ~98.1% of TVL), wstETH (Lido, $96.8K, ~1.9%), cbBTC (Coinbase custody, $0 allocated), WETH ($711, negligible). WBTC and cbBTC are established wrapped BTC assets. wstETH is BBB+ SR rated. WETH is native Ethereum. All are large-cap established assets. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (allocation data) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | WBTC: Brief historical depegs, all recovered within 24h. wstETH: Stable tracking. cbBTC: No depeg >2% since September 2024 launch. No collateral showed >2% depeg lasting >24h in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P3] Market data, [P0] On-chain price history |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Only wstETH has staking exposure (~$96.8K, <2% of TVL). Lido uses 30+ diversified operators. Minimal vault-level exposure. | 9 | 9 | Non-Improvable (optimal) | [P3] Lido operator data |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | EXTREME RISK: Approximately 98.1% of vault TVL is in wrapped BTC (WBTC $4.92M out of $5.02M total). cbBTC has $0 current allocation but is whitelisted. WBTC involves BiT Global/Justin Sun governance concerns. Exceeds 60% threshold dramatically. | 1 | 9 | **Improvable** | [P0] Morpho GraphQL API (allocation: WBTC $4.92M, wstETH $96.8K, WETH $711) |

**Collateral Subtotal: 35.0/45 (77.8%)**
- 3 questions scored 9 (sum = 27), 1 question scored 1
- Raw sum = 28 out of max 36
- Weighted = (28/36) x 45 = 35.0

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | All Tier-0/1: Ethereum (Tier-0 chain), Chainlink (Tier-0 oracle) for price feeds. No bridges. No CEX dependency for operations. All dependencies explicitly identifiable. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant are oracle and bridge setups, and can oracle values be corrected under abnormal conditions? | **Hardcoded oracle check (mandatory):** Each Morpho Blue market uses an immutable oracle that cannot be updated or corrected post-deployment. The WBTC/EURC market uses oracle 0x9CB3...b89. Can the priced collateral depeg? WBTC is a custodial wrapped asset that can theoretically depeg. WBTC is a battle-tested deep-liquidity asset (since 2019). Scored Mid (3) per "hardcoded oracle used only for battle-tested deep-liquidity assets." No fallback oracle exists -- permanent Morpho Blue design limitation. | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API (oracle addresses per market), [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Gauntlet claims "institutional-grade security posture" with Hypernative, ZeroShadow, Chainalysis, SEAL Intel partnerships. No explicit SOC 2 Type II or ISO27001 certification publicly disclosed for Gauntlet Networks Inc. | 3 | 9 | **Source Missing** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Ethereum: No significant halts. Morpho: April 2025 frontend issue resolved in 4 minutes. However, the EURC Core vault itself is too small ($5.02M TVL) and new to have been tested under meaningful stress. No documented stress-test data exists for this vault specifically. Per scoring principle: untested protocols score Mid (3) on resilience questions. | 3 | 9 | **Improvable** | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain halts >30 minutes in the last 12+ months. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Only relevant for wstETH (<2% of TVL). Lido slashing events trivial and fully absorbed. No depositor impact. | 9 | 9 | Non-Improvable (optimal) | [P3] Lido slashing data |
| ST-IC-07 | Are validators diverse geographically and by operator? | Ethereum validator set highly distributed. Lido (wstETH collateral) uses 30+ independent operators across multiple jurisdictions. | 9 | 9 | Non-Improvable (optimal) | [P3] Ethereum validator data |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Permissionless on-chain redemption always available via ERC4626. No off-chain dependency for withdrawals. Oracle failure would prevent new borrows/liquidations on affected market but would not block existing withdrawals. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Infrastructure Counterparty Subtotal: 33.8/45 (75.0%)**
- 5 questions scored 9 (sum = 45), 3 questions scored 3 (sum = 9)
- Raw sum = 54 out of max 72
- Weighted = (54/72) x 45 = 33.75 ~ 33.8

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All allocation to Morpho Blue markets only (Tier-0 protocol). No CEX or RWA exposure. Active markets: WBTC/EURC, wstETH/EURC, WETH/EURC, cbBTC/EURC. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (allocation data) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Performance fee clearly documented (10%) and verified on-chain via Morpho GraphQL API. No hidden rebates found. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (fee=0.1) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. On-chain supply caps per market verified: WBTC/EURC $10M cap, wstETH/EURC $4M cap, WETH/EURC $2.5M cap. Gauntlet's automated risk models manage allocation within caps. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (supplyCap per market) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Lending positions unwound as borrowers repay. EURC lending markets are newer and thinner than USDC equivalents. At $5.02M TVL, unwind feasibility is adequate under normal conditions but untested under stress. Rate spikes during high utilization incentivize repayment. | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (totalAssetsUsd=$5.02M) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending. No external validators, custodians, or asset managers involved in vault operations. Gauntlet (curator) clearly identified. Underlying collateral custodians (BitGo/BiT Global for WBTC) are publicly known. | 9 | 9 | Non-Improvable (optimal) | Vault architecture |

**Protocol Counterparty Subtotal: 39.0/45 (86.7%)**
- 4 questions scored 9 (sum = 36), 1 question scored 3 (sum = 3)
- Raw sum = 39 out of max 45
- Weighted = (39/45) x 45 = 39.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain redemption via ERC4626. No address-level blocking. No admin pause function. Withdrawal depends on market liquidity (idle EURC in markets). | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Uncertain. At $5.02M TVL, the vault is small but EURC is a thin-liquidity stablecoin in DeFi. Idle EURC in markets depends on utilization. No stress test data available for this vault. EURC secondary market depth is significantly thinner than USDC. Markets can absorb small exits but near-total exit capacity is uncertain. | 1 | 3 | **Improvable** | [P0] Morpho GraphQL API (totalAssetsUsd=$5.02M), [P3] EURC market data |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No documented withdrawal delays, but this is because no significant withdrawal stress events have occurred given the small TVL ($5.02M). "No problems because never tested" is not equivalent to "survived actual stress." Compare to USDC Prime which demonstrated $42.8M processed in 48h during November 2025 stress. Per scoring principle: untested protocols score Mid (3) on resilience questions. | 3 | 9 | **Improvable** | Operational history |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Caps appropriately sized relative to TVL ($10M WBTC cap, $4M wstETH cap, $2.5M WETH cap). At $5.02M TVL, caps are not binding. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (supplyCap data) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Untested. The EURC Core vault has not experienced significant stress events. At $5.02M TVL, it has not been tested during high volatility. EURC itself is a newer, thinner stablecoin. Per scoring principle: "untested protocols should score Mid (3) on resilience questions." | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API (totalAssetsUsd=$5.02M) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure EURC lending with no lockups, vesting, or bridge dependencies. Withdrawal speed limited only by market utilization. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Primary redemption through ERC4626 vault always available. However, practical exit requires converting EURC to USD-denominated stablecoins, and EURC on-chain liquidity pools are thin. Unlike USDC/USDT vaults where redeemed assets are immediately usable, EURC holders face meaningful secondary-market friction. EURC DeFi liquidity is a fraction of major stablecoins, creating practical exit dependency on thin secondary markets. | 3 | 3 | Non-Improvable | [P3] EURC market data |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | EURC DeFi liquidity is thin compared to USDC/USDT. At $5.02M TVL, the vault is small. No deep gteurcc secondary market exists. EURC on-chain liquidity pools are limited. Depth likely supports <3% of TVL without major impact. | 1 | 3 | **Improvable** | [P3] EURC market data |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Untested. The vault is small ($5.02M) and has not experienced stress. EURC lending markets are thin -- a bank run would likely cause significant queues and rate spikes. EURC's thinner DeFi liquidity amplifies bank-run risk compared to USDC vaults. No stress test data available. Per scoring principle: untested protocols score Mid (3) on resilience questions. | 3 | 3 | Non-Improvable | [P0] Morpho GraphQL API (totalAssetsUsd=$5.02M) |

**Liquidity Subtotal: 22.8/45 (50.6%)**
- 3 questions scored 9 (sum = 27), 4 questions scored 3 (sum = 12), 2 questions scored 1 (sum = 2)
- Raw sum = 41 out of max 81
- Weighted = (41/81) x 45 = 22.78 ~ 22.8

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | gteurcc vault shares represent 1:1 EURC claim plus accrued yield. ERC4626 standard ensures NAV-based redemption. However, the vault is untested under stress. Per scoring principle: "untested protocols should score Mid (3) on resilience questions." | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Very low. Vault lends EURC -- EUR-denominated. No directional BTC/ETH exposure for lenders. Risk limited to bad debt from borrower defaults, requiring collateral to drop beyond the 14% liquidation buffer (~86% LLTV). | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Immutable Adaptive Curve IRM per market. EURC markets are newer and less battle-tested than USDC equivalents. At $5.02M TVL, rate model behavior under stress is untested. No history of prolonged >=95% utilization. | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (allocation data) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. Gauntlet uses agent-based simulations modeling market scenarios. Risk framework targets insolvent debt <10 bps of TVL. Certora formally verified liquidation mechanics. However, EURC-specific scenario modeling has not been publicly demonstrated. | 3 | 9 | **Source Missing** | [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side only. Vault lenders benefit from liquidations (no loss to lenders unless bad debt occurs). 14% buffer (86% LLTV) provides substantial margin. | 9 | 9 | Non-Improvable (optimal) | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 27.0/45 (60.0%)**
- 2 questions scored 9 (sum = 18), 3 questions scored 3 (sum = 9)
- Raw sum = 27 out of max 45
- Weighted = (27/45) x 45 = 27.0

---

### **Strategy Total: 192.6/270 (71.3%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 35.0 | 45 | 77.8% |
| Collateral | 35.0 | 45 | 77.8% |
| Infra Counterparty | 33.8 | 45 | 75.0% |
| Protocol Counterparty | 39.0 | 45 | 86.7% |
| Liquidity | 22.8 | 45 | 50.6% |
| Market | 27.0 | 45 | 60.0% |
| **Strategy Total** | **192.6** | **270** | **71.3%** |

---

### OPERATIONS (30% Weight) -- Score: 225.0/270 (83.3%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid with strong checks. Morpho Blue immutable. Vault changes require Owner multisig (4-of-7) + 3-day timelock + Guardian (3-of-7) veto. Multiple layers prevent unilateral changes. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock, owner, guardian), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- No governance token voting for this vault. Vault controlled by multisig + Guardian, not token-holder governance. | N/A | N/A | N/A | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. The vault has a confirmed 3-day timelock (259,200 seconds), verified via Morpho GraphQL API. This exceeds the 24-hour minimum for Low Risk. The Guardian (3-of-7 Safe multisig) can veto pending changes. All pending actions visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=259200), [P0] [Safe API Guardian](https://api.safe.global/tx-service/eth/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner can appoint new Curator (subject to 3-day timelock). Withdrawals remain permissionless throughout via ERC4626. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 3 questions scored 9 (sum = 27); O-G-02 = N/A
- Raw sum = 27 out of max 27
- Weighted = (27/27) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Gauntlet: Tarun Chitra (CEO/Co-founder, former D.E. Shaw Research), Rei Chiang (Co-founder). 50+ team. Morpho: Paul Frambot (CEO). All publicly identified with verifiable track records. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Team](https://www.gauntlet.xyz/our-team), [P1] [Morpho](https://morpho.org/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Gauntlet has 50+ employees across 3 continents. Morpho has a separate full team ($73.6M raised). Multiple independent parties capable of vault operations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet About](https://www.gauntlet.xyz/about) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Morpho: ADDMO (French nonprofit, Paris) + Morpho Labs SAS (France). Gauntlet: Gauntlet Networks Inc. (New York, USA). Both clearly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P1] [Gauntlet](https://www.gauntlet.xyz/) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known actions against Gauntlet Networks Inc. or Morpho entities. | 9 | 9 | Non-Improvable (optimal) | [P0] [SEC LR-26266](https://www.sec.gov/enforcement-litigation/litigation-releases/lr-26266), Public records |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Gauntlet has 24/7 on-call with ZeroShadow (vSOC), Hypernative, and SEAL Intel partnerships. However, per framework: incident response MUST include documented procedures to halt automated allocation mechanisms. During March 2026 Resolv exploit, Frontier vaults demonstrated that incident response procedures did NOT cover halting automated allocation within SLA. Same automated infrastructure applies. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Building Institutional Security](https://www.gauntlet.xyz/resources/building-an-institutional-grade-security-posture-at-gauntlet) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Gauntlet published detailed market reports, active VaultBook documentation. Morpho's 4-minute response in April 2025. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Gauntlet: $41.8M from Polychain, Paradigm, Ribbit Capital. Morpho: a16z, Variant, Pantera, Coinbase Ventures ($73.6M). All disclosed. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay](https://www.clay.com/dossier/gauntlet-funding) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Gauntlet manages 70+ vaults with $1.3B+ AUM across multiple chains and risk tiers. Structural mitigations exist: tiered risk system, automated allocation models, published VaultBook. However, formal quantitative conflict-of-interest policy not published. | 3 | 9 | **Improvable** | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | March 2026 Resolv USR exploit caused confirmed bad debt in Gauntlet-curated Frontier and Core vaults (~$7.5M+). While EURC Core specifically had zero losses, the framework evaluates the manager entity. This constitutes "one historical loss incident with limited impact." | 3 | 9 | **Improvable** | [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |

**Team & Legal Subtotal: 52.5/67.5 (77.8%)**
- 6 questions scored 9 (sum = 54), 3 questions scored 3 (sum = 9)
- Raw sum = 63 out of max 81
- Weighted = (63/81) x 67.5 = 52.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive documentation from Morpho (docs.morpho.org) and Gauntlet (VaultBook). Updated regularly. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Docs](https://docs.morpho.org/), [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Detailed documentation of liquidation mechanics, bad debt scenarios, oracle risks, and loss conditions across Morpho docs and Gauntlet VaultBook. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Morpho docs maintain canonical address registry. Vault address clearly identified on Morpho App. All contracts Etherscan-verified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Comprehensive documentation of vault roles (Owner, Curator, Guardian, Allocator) with detailed permission descriptions. Changes visible on-chain via Safe transaction history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves. All allocations visible on Morpho App and Etherscan. Morpho GraphQL API provides programmatic access to all vault state. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0x2ed10624315b74a78f11FAbedAa1A228c198aEfB), [P0] Morpho GraphQL API |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. All core contracts verified on Etherscan. Vault contract (0x2ed1...) verified as MetaMorphoV1_1 (Solidity v0.8.26). Morpho Blue (0xBBBB...) verified. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0x2ed10624315b74a78f11FAbedAa1A228c198aEfB) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions, all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated safety module for this vault. Bad debt socialized per market among lenders. Morpho DAO treasury (~$34.1M, mostly MORPHO tokens) is discretionary via governance. No Gauntlet-specific backstop fund. | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Insufficient. Morpho DAO treasury ~$34.1M (Ethereum $11.4M + Base $22.7M OwnTokens, plus $8.1K non-own-token), consisting almost entirely of MORPHO tokens (no stablecoins). Against ~$10B+ protocol-wide TVL this represents ~0.34%. Against vault TVL ($5.02M) it represents ~680%, but it is NOT ring-fenced for this vault and is entirely in volatile native tokens. Gauntlet is well-funded but no vault-specific reserve disclosed. | 1 | 9 | **Source Missing** | [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Gauntlet: $41.8M raised, $1B valuation. Morpho: $73.6M raised. Both have sustainable revenue streams. Combined runway >24 months. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay](https://www.clay.com/dossier/gauntlet-funding) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Untested for this specific vault. The EURC Core vault at $5.02M TVL has not experienced any significant stress events. Per scoring principle: untested protocols score Mid (3) on resilience questions. | 3 | 9 | **Improvable** | [P0] Morpho GraphQL API (totalAssetsUsd=$5.02M) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue is immutable. Permissionless withdrawals via ERC4626. No proprietary off-chain services required. If Gauntlet disappeared, existing allocations continue and users can withdraw freely. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Financial Resilience Subtotal: 37.5/67.5 (55.6%)**
- 2 questions scored 9 (sum = 18), 2 questions scored 3 (sum = 6), 1 question scored 1
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
| **Security** | Smart Contract Security (11 Q) | 87 | 99 | 158.2 | 180 | 87.9% |
| | Key Management (8 Q) | 66 | 72 | 165.0 | 180 | 91.7% |
| | **Security Subtotal** | | | **323.2** | **360** | **89.8%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 63 | 81 | 35.0 | 45 | 77.8% |
| | Collateral (4 Q) | 28 | 36 | 35.0 | 45 | 77.8% |
| | Infra Counterparty (8 Q) | 54 | 72 | 33.8 | 45 | 75.0% |
| | Protocol Counterparty (5 Q) | 39 | 45 | 39.0 | 45 | 86.7% |
| | Liquidity (9 Q) | 41 | 81 | 22.8 | 45 | 50.6% |
| | Market (5 Q) | 27 | 45 | 27.0 | 45 | 60.0% |
| | **Strategy Subtotal** | | | **192.6** | **270** | **71.3%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 63 | 81 | 52.5 | 67.5 | 77.8% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 25 | 45 | 37.5 | 67.5 | 55.6% |
| | **Operations Subtotal** | | | **225.0** | **270** | **83.3%** |
| **TOTAL** | | | | **740.8** | **900** | **82.3%** |

---

