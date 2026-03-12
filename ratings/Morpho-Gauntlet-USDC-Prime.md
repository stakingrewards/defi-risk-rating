# Morpho - Gauntlet USDC Prime Vault Risk Rating

**Rating Date**: 2026-03-10
**Final Grade**: BBB-
**Total Score**: 820.6/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v1.0-alpha

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 334.1/360 (92.8%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 25+ audits from Tier-0/1 firms including ChainSecurity, Spearbit/OpenZeppelin, Zellic, Certora, Blackthorn. Both Morpho Blue core and MetaMorpho/Vaults V2 framework extensively audited. Formal verification by Certora with mathematical proofs. The Gauntlet USDC Prime vault (0xdd0f...) is a MetaMorpho V1 vault deployed via the audited MetaMorpho factory. All core contracts holding user funds are covered. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/), [P1] [GitHub metamorpho](https://github.com/morpho-org/metamorpho) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | December 2025: Certora (Tier-0), Spearbit (Tier-0 via Cantina), Blackthorn for Vaults V2 MarketV1AdapterV2. September 2025: ChainSecurity (Tier-0) for Vaults V2 core. Multiple Tier-0 auditors for most recent work. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable (~600 LOC). Every vault upgrade in last 12 months (Vaults V2 Sep-Dec 2025) was preceded by multiple audits from Tier-0 firms. The V2 launch included 8+ separate audit engagements. The Gauntlet USDC Prime vault on Ethereum is a V1 vault (non-upgradeable). | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [Vault V1 Docs](https://docs.morpho.org/learn/concepts/vault/) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 vulnerability patched immediately with OpenZeppelin. Certora formal verification provides mathematical proof of critical invariants. All V2 audit findings resolved before deployment with multiple re-reviews. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue core is immutable. MetaMorpho V1 vault (0xdd0f...) is a non-upgradeable ERC4626 contract deployed March 2024. Market changes require Curator + timelock + Guardian approval. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vault V1 Docs](https://docs.morpho.org/learn/concepts/vault/), [P0] Etherscan contract |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss in Gauntlet vaults. April 2025 frontend vulnerability ($2.6M) was intercepted by white hat c0ffeebabe.eth and all funds returned within minutes -- this was a Morpho App frontend issue, not a vault exploit. October 2024 oracle exploit ($230K) affected only PAXG/USDC market, not this vault. November 2025 Stream/Elixir contagion affected MEV Capital vault (3.6% bad debt), NOT Gauntlet vaults (zero bad debt confirmed). | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P4] [Cointelegraph](https://cointelegraph.com/news/white-hat-intercepts-2-million-morpho-blue-hack), [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho operates as ADDMO, a French nonprofit association. Gauntlet Networks Inc. is a well-funded ($41.8M raised, $1B valuation) US-based company with public leadership. No credible allegations against either entity. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P2] [Gauntlet About](https://www.gauntlet.xyz/about) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No evidence of timelock reductions. The Gauntlet USDC Prime vault has a confirmed 7-day timelock (604,800 seconds), verified via Morpho GraphQL API (March 2026). No reductions have occurred since vault deployment in March 2024. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=604800), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Morpho runs an active public bounty on Cantina with $2.5M max payout for critical vulnerabilities. 236 findings submitted since March 2024. Scope covers both V1 and V2 contracts plus web apps. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. Morpho runs internal monitoring bots with continuous invariant checks. Gauntlet specifically partners with Hypernative (real-time on-chain monitoring, 99.5% hack detection rate), ZeroShadow (24/7 virtual SOC), Chainalysis (blockchain analytics), and SEAL Intel (threat intelligence). April 2025 incident demonstrated 4-minute response time. Gauntlet's 24/7 liquidity monitoring was confirmed during November 2025 stress. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Building Institutional Security](https://www.gauntlet.xyz/resources/building-an-institutional-grade-security-posture-at-gauntlet) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. Morpho Blue prioritizes immutability over admin controls. Guardian can manually veto pending timelocked actions but cannot pause the protocol. Market-level isolation provides containment. Gauntlet's Hypernative partnership provides automated response solutions, but these cannot pause on-chain Morpho contracts. | 3 | 3 | Non-Improvable | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |

**Smart Contract Security Subtotal: 169.1/180 (93.9%)**
- 10 questions scored 9 (sum = 90), 1 question scored 3 (sum = 3)
- Raw sum = 93 out of max 99
- Weighted = (93/99) x 180 = 169.1

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Owner: Gnosis Safe 4-of-7 multisig (0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec), verified on-chain via Safe Transaction Service API (Safe v1.3.0, 7 distinct owner addresses, threshold=4). Guardian: Gnosis Safe 3-of-7 multisig (0x7084bF4dB6c21e1834dD6482f6056a39A33584cD), verified (Safe v1.4.1). Curator: Gnosis Safe 3-of-7 multisig (0x9E33faAE38ff641094fa68c65c2cE600b3410585), verified (Safe v1.4.1). Timelock: 604,800 seconds (7 days), confirmed via Morpho GraphQL API. All changes visible on-chain with 7-day advance notice. No changes in last 12 months without on-chain trail. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API Guardian](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/), [P0] [Safe API Curator](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x9E33faAE38ff641094fa68c65c2cE600b3410585/), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Vault contract is non-upgradeable. Moving user funds requires going through Morpho Blue immutable contract logic. Market changes require multisig + timelock + Guardian. Permissionless redemption always available via ERC4626. The vault architecture inherently prevents single-key fund movement. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Vault V1 Docs](https://docs.morpho.org/learn/concepts/vault/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner multisig is 4-of-7 Safe (verified via Safe API: 7 distinct owner addresses, threshold=4). This exceeds the >=4-of-7 minimum for Low Risk. Guardian is a 3-of-7 Safe multisig. Curator is a 3-of-7 Safe multisig. Gauntlet is publicly identified as the entity operating these multisigs. Five addresses overlap across Owner/Guardian/Curator multisigs, all Gauntlet team members. Depositors have no direct veto power (no Aragon DAO equivalent). | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API Guardian](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking capability. No pause function on Morpho Blue (immutable). Guardian can only revoke pending timelocked actions. Withdrawals always permissionless via direct smart contract interaction. Rules publicly documented. Same architecture as Steakhouse vault. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets held in non-custodial Morpho Blue contracts on Ethereum. Permissionless redemption via ERC4626. No off-chain custody component. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. Vault funds are held in Morpho Blue markets, separate from any treasury or operational wallets. Performance fee accrued on-chain transparently. Morpho is a nonprofit with no profit extraction from protocol operations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain enforced whitelist of Morpho Blue markets only. Current markets: wstETH/USDC, cbBTC/USDC, WBTC/USDC (per the forum whitelisting post and vault description). New market additions require Curator approval + timelock + Guardian veto. Supply caps per market enforced on-chain. The whitelist is well-defined and aligned with the Prime mandate. | 9 | 9 | Non-Improvable (optimal) | [P2] [Gauntlet USDC Prime Whitelisting](https://forum.morpho.org/t/gauntlet-usdc-prime-vault-whitelisting/496), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Gauntlet's institutional security posture includes partnerships with ZeroShadow (24/7 vSOC with incident triage and escalation), Hypernative (automated response), and SEAL Intel (threat intelligence). Morpho docs include emergency procedures documentation for vault curator roles. However, no public, vault-specific incident playbook with explicit key rotation procedures or tabletop exercise results has been published by Gauntlet. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Morpho Emergency Procedures](https://docs.morpho.org/curate/emergency/) |

**Key Management Subtotal: 165.0/180 (91.7%)**
- 7 questions scored 9 (sum = 63), 1 question scored 3 (sum = 3)
- Raw sum = 66 out of max 72
- Weighted = (66/72) x 180 = 165.0

**Improvement Opportunities:**
- **S-KM-08** (+15.0 weighted points): Publish comprehensive incident response playbook with key rotation procedures and conduct full tabletop exercise

---

### **Security Total: 334.1/360 (92.8%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 169.1 | 180 | 93.9% |
| Key Management | 165.0 | 180 | 91.7% |
| **Security Total** | **319.1** | **360** | **88.6%** |

---

### STRATEGY (30% Weight) -- Score: 242.5/270 (89.8%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from overcollateralized USDC lending against blue-chip crypto collateral (wstETH, cbBTC, WBTC). 100% mandate-aligned. The Prime vault mandate explicitly targets "large market cap and high liquidity collateral markets." Yield sources documented on Morpho App and Gauntlet VaultBook. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults), [P2] [Gauntlet USDC Prime Whitelisting](https://forum.morpho.org/t/gauntlet-usdc-prime-vault-whitelisting/496) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail shocks: simultaneous BTC/ETH crash exceeding the liquidation buffer (86% LLTV provides ~14% buffer), oracle manipulation on immutable oracle, or catastrophic wrapped-asset custodian failure. Bad debt per market is isolated and socialized among lenders of that specific market. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault simply lends USDC. No rehypothecation of depositor funds. Effective leverage: 1.0x. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss events for Gauntlet USDC Prime vault since March 2024 launch. During November 2025 liquidity stress, Gauntlet confirmed zero bad debt across all vaults. The vault processed $42.8M (~40% TVL) in withdrawals within 48 hours without impairment. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-PM-06 | Is a risk framework for vault curation documented? | Yes. Gauntlet publishes comprehensive curation methodology via VaultBook, including risk factor overviews, due diligence processes, and market allocation strategy. Quantitative limits for insolvency risk (targeting <10 bps of TVL). Clear tiering system (Prime/Balanced/Frontier). Agent-based simulation models inform allocation decisions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults), [P1] [Curation Methodology](https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. Yield is entirely organic from USDC lending demand. No emissions or token incentives required for base yield. Current net APY approximately 3.22% (March 2026, vault fee 0%). Coinbase crypto-backed loans partnership drives sustainable demand. APY varies with market conditions; was ~9% during higher utilization periods. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet VaultBook Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees), [P0] Morpho GraphQL API (netApy, March 2026) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes. USDC is the most liquid stablecoin. During November 2025 stress, Gauntlet USDC Prime vault maintained average ~53% supply available for immediate withdrawal, and processed 40% of TVL in withdrawals within 48 hours. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. Pure lending interest from overcollateralized borrower demand. No basis trade, peg arbitrage, or funding rate dependency. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |

**Protocol Mechanics Subtotal: 45.0/45 (100.0%)**
- 8 applicable questions (ST-PM-04 = N/A), all scored 9
- Raw sum = 72 out of max 72
- Weighted = (72/72) x 45 = 45.0

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Blue-chip only: wstETH (Lido, largest LST), cbBTC (Coinbase custody, NY DFS regulated), WBTC (BitGo/BiT Global). All established, high-market-cap assets. Gauntlet performs rigorous due diligence on collateral quality. Risk tiering applied per market. | 9 | 9 | Non-Improvable (optimal) | [P2] [Gauntlet USDC Prime Whitelisting](https://forum.morpho.org/t/gauntlet-usdc-prime-vault-whitelisting/496), [P1] [Due Diligence](https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview/due-diligence) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | cbBTC: No depeg >2% since September 2024 launch. WBTC: Brief depegs during historical events, all recovered within 24h. wstETH: Stable tracking. No collateral showed >2% depeg lasting >24h in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P3] Market data |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Only wstETH has staking exposure. Lido uses 30+ diversified operators across multiple jurisdictions. Lido slashing insurance/coverage fund absorbs minor events. | 9 | 9 | Non-Improvable (optimal) | Lido operator data |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | HIGH RISK: Approximately 98% of vault TVL is in wrapped assets (cbBTC and WBTC markets). cbBTC is custodied by Coinbase (NY DFS regulated). WBTC involves BiT Global/Justin Sun governance concerns. Exceeds 60% threshold significantly. | 1 | 9 | **Improvable** | [P2] [Gauntlet USDC Prime Whitelisting](https://forum.morpho.org/t/gauntlet-usdc-prime-vault-whitelisting/496) |

**Collateral Subtotal: 35.0/45 (77.8%)**
- 3 questions scored 9 (sum = 27), 1 question scored 1
- Raw sum = 28 out of max 36
- Weighted = (28/36) x 45 = 35.0

**Improvement Opportunities:**
- **ST-C-04** (+10.0 weighted points): Diversify collateral exposure below 60% wrapped assets

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | All Tier-0/1: Ethereum (Tier-0 chain), Chainlink (Tier-0 oracle). No bridges. No CEX dependency for operations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | SINGLE ORACLE RISK. Each Morpho Blue market has one immutable oracle with no fallback. Chainlink is Tier-0 and battle-tested, but zero redundancy by design. | 3 | 3 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Gauntlet claims "institutional-grade security posture" but no explicit SOC 2 Type II or ISO27001 certification for Gauntlet Networks Inc. has been publicly disclosed. Chainlink and Coinbase hold enterprise certifications. | 3 | 9 | **Source Missing** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Ethereum: No significant halts. Morpho: April 2025 frontend issue resolved in 4 minutes. November 2025: Gauntlet vaults operated correctly with zero bad debt and 53% average withdrawable liquidity. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain halts >30 minutes in the last 12+ months. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Only relevant for wstETH. Lido slashing events trivial and fully absorbed. No depositor impact. | 9 | 9 | Non-Improvable (optimal) | Lido slashing data |
| ST-IC-07 | Are validators diverse geographically and by operator? | Ethereum validator set highly distributed. Lido uses 30+ independent operators. No single operator >33%. | 9 | 9 | Non-Improvable (optimal) | Ethereum validator data |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Permissionless on-chain redemption always available via ERC4626. No off-chain dependency for withdrawals. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Infrastructure Counterparty Subtotal: 37.5/45 (83.3%)**
- 6 questions scored 9 (sum = 54), 2 questions scored 3 (sum = 6)
- Raw sum = 60 out of max 72
- Weighted = (60/72) x 45 = 37.5

**Improvement Opportunities:**
- **ST-IC-03** (+3.75 weighted points): Gauntlet Networks obtain and publish SOC 2 Type II or ISO27001 certification

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All allocation to Morpho Blue markets only (Tier-0 protocol). No CEX or RWA exposure. | 9 | 9 | Non-Improvable (optimal) | [P2] [Gauntlet USDC Prime Whitelisting](https://forum.morpho.org/t/gauntlet-usdc-prime-vault-whitelisting/496) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Yes. Performance fee clearly documented in VaultBook and on-chain. No hidden rebates found. Coinbase partnership is public. | 9 | 9 | Non-Improvable (optimal) | [P1] [Incentives & Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. On-chain supply caps per market. Gauntlet's automated risk models perform daily optimization and continuous rebalancing within caps. | 9 | 9 | Non-Improvable (optimal) | [P1] [Market Allocation Strategy](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/curation-methodology-and-risk-factor-overview/market-allocation-strategy) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Lending positions unwound as borrowers repay. November 2025 demonstrated $42.8M (~40% TVL) processed within 48 hours. No discretionary approvals needed. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending. No external validators, custodians, or asset managers. Gauntlet (curator) clearly identified. Underlying collateral custodians publicly known. | 9 | 9 | Non-Improvable (optimal) | Vault architecture |

**Protocol Counterparty Subtotal: 45.0/45 (100.0%)**
- 5 questions, all scored 9
- Raw sum = 45 out of max 45
- Weighted = (45/45) x 45 = 45.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain redemption via ERC4626. No address-level blocking. No admin pause function. Withdrawal depends on market liquidity. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Moderate. Average ~53% available for immediate withdrawal. $42.8M (~40% TVL) processed within 48 hours during November 2025 stress. Rate spikes incentivize repayment but instant 100% exit not guaranteed. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | Gauntlet USDC Prime demonstrated strong performance during November 2025 stress. Average 53% withdrawable liquidity. $42.8M processed within 48 hours without impairment. No prolonged freezes. >95% of withdrawals completed promptly over 12-month period. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Caps appropriately sized. Gauntlet's risk models actively manage supply-to-market ratios to ensure withdrawal liquidity. During November 2025, delays were driven by utilization, not cap design. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Battle-tested during November 2025. Gauntlet USDC Prime maintained average 53% withdrawable liquidity while other curated vaults fell by >60%. Conditions normalized within days. Demonstrated resilience. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure USDC lending with no lockups, vesting, or bridge dependencies. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary redemption through ERC4626 vault always available. Secondary market not required for exit. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | High. USDC is the most liquid stablecoin. GTUSDC is 1:1 backed by vault assets. ~$137M TVL. | 9 | 9 | Non-Improvable (optimal) | [P3] Market data |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Moderate. Bank run causes temporary queues and rate spikes but unlikely permanent losses. Market isolation contains risk. November 2025 demonstrated zero permanent losses and 53% average withdrawable liquidity. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |

**Liquidity Subtotal: 35.0/45 (77.8%)**
- 6 questions scored 9 (sum = 54), 3 questions scored 3 (sum = 9)
- Raw sum = 63 out of max 81
- Weighted = (63/81) x 45 = 35.0

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | GTUSDC vault shares represent 1:1 USDC claim plus accrued yield. No depeg history. During November 2025 stress, vault share value remained stable. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Very low. Vault lends USDC -- dollar-denominated. No directional BTC/ETH exposure for lenders. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Immutable Adaptive Curve IRM per market. During November 2025, elevated rates attracted additional supply, demonstrating resilience. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. Gauntlet uses agent-based simulations modeling market scenarios. Risk framework targets insolvent debt <10 bps of TVL in extreme scenarios. Certora formally verified liquidation mechanics. Gauntlet monitors cross-protocol leveraged positions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side only. Vault lenders benefit from liquidations. Gauntlet's real-time monitoring of cross-protocol positions helps anticipate cascades. | 9 | 9 | Non-Improvable (optimal) | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 45.0/45 (100.0%)**
- 5 questions, all scored 9
- Raw sum = 45 out of max 45
- Weighted = (45/45) x 45 = 45.0

---

### **Strategy Total: 242.5/270 (89.8%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 45.0 | 45 | 100.0% |
| Collateral | 35.0 | 45 | 77.8% |
| Infra Counterparty | 37.5 | 45 | 83.3% |
| Protocol Counterparty | 45.0 | 45 | 100.0% |
| Liquidity | 35.0 | 45 | 77.8% |
| Market | 45.0 | 45 | 100.0% |
| **Strategy Total** | **242.5** | **270** | **89.8%** |

---

### OPERATIONS (30% Weight) -- Score: 244.0/270 (90.4%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid with strong checks. Morpho Blue immutable. Vault changes require Owner multisig + timelock + Guardian. Multiple layers prevent unilateral changes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- No governance token voting for this vault. Vault controlled by multisig + Guardian, not token-holder governance. Governance concentration captured in S-KM-01 and S-KM-03. | N/A | N/A | N/A | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. The vault has a confirmed 7-day timelock (604,800 seconds), verified via Morpho GraphQL API (March 2026). This matches Steakhouse vaults and far exceeds the 24-hour minimum for Low Risk. The Guardian (3-of-7 Safe multisig) can veto pending changes during the 7-day window. All pending actions visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (timelock=604800), [P0] [Safe API Guardian](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner can appoint new Curator (subject to timelock). Withdrawals remain permissionless throughout via ERC4626. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |

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
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Morpho: ADDMO (French nonprofit, Paris) + Morpho Labs SAS (France). Gauntlet: Gauntlet Networks Inc. (New York, USA). Both clearly identified. Note: SEC action against unrelated "Gauntlet Holdings, LLC" has no connection to Gauntlet Networks Inc. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P1] [Gauntlet](https://www.gauntlet.xyz/) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known actions against Gauntlet Networks Inc. or Morpho entities. The SEC enforcement against "Gauntlet Holdings, LLC" (LR-26266) involves a completely different entity. | 9 | 9 | Non-Improvable (optimal) | [P0] [SEC LR-26266](https://www.sec.gov/enforcement-litigation/litigation-releases/lr-26266), Public records |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Yes. Gauntlet has documented "24/7 liquidity monitoring" confirmed during November 2025 stress. Partnerships with ZeroShadow (24/7 virtual SOC), Hypernative (automated threat detection), and SEAL Intel. Morpho demonstrated 4-minute response April 2025. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Building Institutional Security](https://www.gauntlet.xyz/resources/building-an-institutional-grade-security-posture-at-gauntlet) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Gauntlet published detailed market report within days of November 2025 stress. Active VaultBook documentation. Morpho's 4-minute response in April 2025. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Gauntlet: $41.8M from Polychain, Paradigm, Ribbit Capital ($1B valuation). Morpho: a16z, Variant, Pantera, Coinbase Ventures ($73.6M, 29 investors). All disclosed. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay](https://www.clay.com/dossier/gauntlet-funding), [P4] [Tracxn](https://tracxn.com/d/companies/morpho/__5iKpzjF_-EXELsu5bJ6cORHuQN7HD3ItPqKPexS2FVw) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Gauntlet manages 70+ vaults with $1.4B+ AUM. Structural mitigations exist: tiered risk system (Prime/Balanced/Frontier), automated allocation models, published VaultBook. But formal quantitative conflict-of-interest policy not published. | 3 | 9 | **Improvable** | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | Zero bad debt across all Gauntlet Morpho vaults since March 2024. During prior Aave advisory role (2020-2024), Aave had $1.6M CRV bad debt, but Gauntlet was an advisor, not curator, and the bad debt resulted from governance inaction on Gauntlet's recommendations. As vault curator, zero losses. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |

**Team & Legal Subtotal: 62.5/67.5 (92.6%)**
- 8 questions scored 9 (sum = 72), 1 question scored 3
- Raw sum = 75 out of max 81
- Weighted = (75/81) x 67.5 = 62.5

**Improvement Opportunities:**
- **O-TL-08** (+5.0 weighted points): Publish formal conflict-of-interest policy with quantitative allocation rules

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive documentation from Morpho (docs.morpho.org) and Gauntlet (VaultBook with detailed curation methodology). | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Docs](https://docs.morpho.org/), [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Detailed documentation of liquidation mechanics, bad debt scenarios, oracle risks, and loss conditions across Morpho docs and Gauntlet VaultBook. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Morpho docs canonical address registry. Vault address clearly identified on Morpho App and Gauntlet App. All Etherscan-verified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Comprehensive documentation of vault roles. Changes visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves. All allocations visible on Morpho App and Etherscan. Gauntlet App provides additional dashboard. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xdd0f28e19C1780eb6396170735D45153D261490d), [P3] [Gauntlet App](https://app.gauntlet.xyz/vaults/eth:0xdd0f28e19c1780eb6396170735d45153d261490d) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. All core contracts verified on Etherscan. Full source code readable. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xdd0f28e19C1780eb6396170735D45153D261490d) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions, all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated safety module for this vault. Bad debt socialized per market. Morpho DAO treasury (~$21.9M) discretionary. No Gauntlet-specific backstop. | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Insufficient. Morpho DAO treasury ~$21.9M against ~$10B+ protocol TVL (0.22%). Not ring-fenced. Gauntlet is well-funded ($41.8M raised) but no vault-specific reserve disclosed. | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama](https://defillama.com/protocol/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Gauntlet: $41.8M raised, $1B valuation, profitable since 2021. Morpho: $73.6M raised. Both have sustainable revenue. Combined runway >24 months. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay](https://www.clay.com/dossier/gauntlet-funding) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Resilient. November 2025: Gauntlet USDC Prime maintained TVL >$130M while others fell >60%. Zero bad debt. Gauntlet USDC Balanced gained 35% supply during stress. Revenue model continued. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue is immutable. Permissionless withdrawals via ERC4626. No proprietary off-chain services required. If Gauntlet disappeared, existing allocations continue and users can withdraw. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Financial Resilience Subtotal: 46.5/67.5 (68.9%)**
- 3 questions scored 9 (sum = 27), 1 question scored 3, 1 question scored 1
- Raw sum = 31 out of max 45
- Weighted = (31/45) x 67.5 = 46.5

**Improvement Opportunities:**
- **O-FR-01** (+8.1 weighted points): Create dedicated safety module with binding activation rules
- **O-FR-02** (+10.8 weighted points): Establish liquid reserve >= 5% of vault TVL

---

### **Operations Total: 244.0/270 (90.4%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 67.5 | 67.5 | 100.0% |
| Team & Legal | 62.5 | 67.5 | 92.6% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 46.5 | 67.5 | 68.9% |
| **Operations Total** | **244.0** | **270** | **90.4%** |

---

## Final Score Calculation

| Category | Subcategory | Current Points | Max Points | Potential Points |
|----------|-------------|----------------|------------|------------------|
| **Security** | Smart Contract Security | 169.1 | 180 | 169.1 |
| | Key Management | 165.0 | 180 | 180.0 |
| | **Security Subtotal** | **334.1** | **360** | **349.1** |
| **Strategy** | Protocol Mechanics | 45.0 | 45 | 45.0 |
| | Collateral | 35.0 | 45 | 45.0 |
| | Infra Counterparty | 37.5 | 45 | 41.3 |
| | Protocol Counterparty | 45.0 | 45 | 45.0 |
| | Liquidity | 35.0 | 45 | 35.0 |
| | Market | 45.0 | 45 | 45.0 |
| | **Strategy Subtotal** | **242.5** | **270** | **256.3** |
| **Operations** | Governance | 67.5 | 67.5 | 67.5 |
| | Team & Legal | 62.5 | 67.5 | 67.5 |
| | Documentation | 67.5 | 67.5 | 67.5 |
| | Financial Resilience | 46.5 | 67.5 | 67.5 |
| | **Operations Subtotal** | **244.0** | **270** | **270.0** |
| **TOTAL** | | **820.6** | **900** | **875.4** |

---
