# Morpho - Steakhouse Prime Instant EURCV V2 Vault Risk Rating

**Rating Date**: 2026-04-09
**Final Grade**: BB-
**Total Score**: 745.6/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-beta

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 323.2/360 (89.8%)

**NOTE: Security scores are platform-level and IDENTICAL to all other Steakhouse/Morpho vault ratings. The V2 vault inherits Morpho's security infrastructure (25+ audits, formal verification, $2.5M bug bounty) and uses the same Curator Safe (2-of-5). The V2-specific architecture adds per-function timelocks, an Aragon DAO Owner, and a specialized Sentinel/Revoker contract.**

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 25+ total audits, 11 specifically for Vaults V2 from Tier-0/1 firms: ChainSecurity, Spearbit, Certora, Zellic, Cantina contest, Blackthorn. Both Morpho Blue core and Vaults V2 framework extensively audited. Formal verification by Certora. The MorphoVaultV1Adapter connecting V2 to V1 is covered by the V2 audit scope (Dec 2025). | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | December 2025: Certora (Tier-0), Spearbit (Tier-0 via Cantina), Blackthorn for Vaults V2 MarketV1AdapterV2. September 2025: ChainSecurity (Tier-0) for Vaults V2 core. Multiple Tier-0 auditors for most recent work. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable (~600 LOC). The V2 vault contract is non-upgradeable (deployed ~Nov 2025). Every component of the V2 launch (Jul-Dec 2025) was preceded by multiple audits from Tier-0 firms. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P0] [Etherscan V2 Vault](https://etherscan.io/address/0xbeef0C075Da5D01112AE5cF34d257074fB5DDB2f) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 vulnerability patched immediately with OpenZeppelin. Certora formal verification provides mathematical proof of critical invariants. All V2 audit findings resolved before deployment with multiple re-reviews. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM), [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | V2 vault is non-upgradeable ERC4626 contract. Morpho Blue core is immutable. Critical vault parameter changes require per-function timelocks: 7 days (604800s) for adapter changes, cap increases, gate changes, timelock increases, and abdicate. Sentinel can revoke pending timelocked actions. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P0] [Etherscan V2 Vault](https://etherscan.io/address/0xbeef0C075Da5D01112AE5cF34d257074fB5DDB2f) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss in Steakhouse vaults. April 2025 frontend vulnerability ($2.6M) was intercepted by white hat c0ffeebabe.eth and all funds returned. November 2025 Stream/Elixir contagion affected MEV Capital vault, NOT Steakhouse vaults. March 2026 phishing attack on Steakhouse domain; no contracts affected. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P1] [Binance Square](https://www.binance.com/en/square/post/03-30-2026-steakhouse-financial-warns-users-of-phishing-attack-on-domain-307105025811217) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho operates as ADDMO, a French nonprofit association. Steakhouse has 2+ year track record. No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. V2 vault deployed ~Nov 2025 with 7-day (604800s) timelocks on critical functions, confirmed via Morpho GraphQL API. No decreaseTimelock calls observed. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active public bounty on Cantina with $2.5M max payout for critical vulnerabilities. 552 findings submitted. Scope covers Vaults V2. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Internal monitoring bots perform continuous invariant checks. Chainalysis partnership. April 2025 incident: alert received and frontend rolled back within 4 minutes. However, monitoring exists but cannot automatically trigger protective actions -- all responses require manual human intervention. Automated allocation flows not covered by automated halt mechanism. Platform-level limitation. | 3 | 9 | **Improvable** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. Morpho Blue prioritizes immutability over admin controls. Sentinel can revoke pending timelocked actions but cannot pause or halt allocations. Market-level isolation provides containment. | 3 | 3 | Non-Improvable | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Smart Contract Security Subtotal: 158.2/180 (87.9%)**
- 9 questions scored 9 (sum = 81), 2 questions scored 3 (sum = 6)
- Raw sum = 87 out of max 99
- Weighted = (87/99) x 180 = 158.18 = 158.2

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | V2 Owner: Aragon DAO (0xE67d850dE6E6Fc913fb613573dc00d3Ba863C099). V1 Owner: 5-of-8 Safe (0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD, verified: 8 owners, threshold=5, nonce=108, Safe v1.4.1). Curator: 2-of-5 Safe (0x827e86072B06674a077f592A531dcE4590aDeCdB, verified: 5 owners, threshold=2, nonce=150, Safe v1.4.1). Sentinel: Revoker contract (0xb239fde1ef31641BEB75E3A89C335Ab7aC4b0115). All role changes visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API - V1 Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P0] [Safe API - Curator](https://api.safe.global/tx-service/eth/api/v1/safes/0x827e86072B06674a077f592A531dcE4590aDeCdB/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. V2 vault is non-upgradeable. Moving user funds requires Morpho Blue immutable logic. V1 Owner 5-of-8 Safe (threshold >= 3, signers >= 5) + 7-day timelock. Permissionless ERC4626 redemption always available. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | V2 Owner is Aragon DAO (exceeds 3-of-5 minimum). V1 Owner is 5-of-8 Safe (verified: 8 distinct addresses, threshold=5). Curator is 2-of-5 Safe. One signer identified as pitmaster.eth (0x0D61C8b6CA9669A36F351De3AE335e9689dd9C5b). | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API - V1 Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P0] [Safe API - Curator](https://api.safe.global/tx-service/eth/api/v1/safes/0x827e86072B06674a077f592A531dcE4590aDeCdB/) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking. No pause function on Morpho Blue (immutable) or V2 vault. Sentinel can only revoke pending timelocked actions. Withdrawals always permissionless. V2's forceDeallocate adds permissionless exit even for illiquid adapters. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% in non-custodial smart contracts: V2 vault -> V1 adapter -> V1 MetaMorpho -> Morpho Blue. All on Ethereum. EURCV itself is issued by SG-FORGE (centralized issuer) but vault custody of the token is fully non-custodial. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan V2 Vault](https://etherscan.io/address/0xbeef0C075Da5D01112AE5cF34d257074fB5DDB2f), [P0] [Etherscan V1 Adapter](https://etherscan.io/address/0xE85175298011C788011C49380E0729B04B368aBE) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. Morpho is a nonprofit. V2 vault: 0% fees. V1 vault: 5% performance fee accrued on-chain transparently. Funds fully separate from treasury/ops. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P1] [Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | V2 uses adapter registry. One adapter: MorphoVaultV1Adapter (0xE85175298011C788011C49380E0729B04B368aBE) -> V1 steakEURCV vault (0x75741A). Adding adapters requires Curator + 7-day timelock. V1 vault markets: wstETH/EURCV, WBTC/EURCV, WETH/EURCV, cbBTC/EURCV, steakUSDC/EURCV, EUTBL/EURCV. New V1 market additions require Curator + 7-day timelock + Guardian veto. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P0] [Morpho V1 API](https://api.morpho.org/graphql) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Partial. Guardian drill conducted January 2024 for V1 vaults demonstrated veto mechanism but revealed low participation. V2 has Sentinel/Revoker contract instead. No comprehensive key rotation playbook. No V2-specific tabletop exercise documented. | 3 | 9 | **Improvable** | [P2] [Guardian Report](https://kitchen.steakhouse.financial/p/steakusdc-guardian-report), [P0] [Etherscan Sentinel](https://etherscan.io/address/0xb239fde1ef31641BEB75E3A89C335Ab7aC4b0115) |

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

### STRATEGY (30% Weight) -- Score: 192.4/270 (71.3%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from overcollateralized EURCV lending via V1 vault. Market breakdown: idle EURCV (87.4%), WBTC/EURCV (5.5%), EUTBL/EURCV (2.6%), wstETH/EURCV (2.5%), cbBTC/EURCV (1.5%), steakUSDC/EURCV (0.5%). Net APY ~4.03% is 100% organic from lending demand. High idle share means only ~12.6% of TVL is deployed. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V1 API](https://api.morpho.org/graphql), [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail shocks: (1) simultaneous ETH/BTC crash exceeding 14% liquidation buffer; (2) EUTBL depeg with only 3.5% buffer at 96.5% LLTV; (3) oracle manipulation on immutable oracle; (4) EURCV issuer failure. EURCV is backed by Societe Generale (major bank) and MiCA-compliant, making issuer failure less likely than for unregulated stablecoins. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [SG-FORGE](https://www.sgforge.com/product/coinvertible/) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault simply lends EURCV. No rehypothecation. Effective leverage: 1.0x. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss events for Steakhouse EURCV vault or any Steakhouse vault since inception. During November 2025 stress, Steakhouse vaults had ZERO bad debt. Clean track record across all variants. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Steakhouse publishes vault controls with DDQ process (2 internal + 1 external reviewer). Credora A+ rating. On-chain caps per market in V1, caps per adapter in V2. 7-day timelock + Sentinel veto. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls), [P2] [Credora Ratings](https://forum.morpho.org/t/credora-network-risk-ratings-on-morpho/1652) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. Net APY (~4.03%) is entirely organic from EURCV lending demand. 0% fees at V2 level. No emissions or incentive dependency. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | EURCV has thin DeFi liquidity (~$104M total supply, ~2,700 holders). V2 vault at $33.3M = ~32% of total supply. However, ~87.4% idle in V1 vault means most can withdraw instantly. Active positions ($5.6M) depend on borrower repayment. Under conservative assumptions, most of the position can unwind but the vault's size relative to EURCV supply creates tail risk. Slippage 2-5% range for large exits. | 3 | 3 | Non-Improvable | [P0] [Morpho V1 API](https://api.morpho.org/graphql), [P0] [Etherscan EURCV](https://etherscan.io/token/0x5F7827FDeb7c20b443265Fc2F40845B715385Ff2) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. Pure lending interest from overcollateralized borrower demand. No invertible spread dependency. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | V2 allocators can move funds between adapters within cap boundaries without timelock. V1 also has allocators. Supply caps limit max exposure but no automatic kill-switch for abnormal conditions. Halting requires manual intervention. | 3 | 9 | **Improvable** | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2), [P1] [Morpho Public Allocator](https://docs.morpho.org/curate/concepts/public-allocator/) |

**Protocol Mechanics Subtotal: 38.3/45 (85.2%)**
- 9 applicable questions (ST-PM-04 = N/A): 7 scored 9 (sum = 63), 2 scored 3 (sum = 6)
- Raw sum = 69 out of max 81
- Weighted = (69/81) x 45 = 38.33 = 38.3

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Diversified collateral: wstETH (Lido, 86% LLTV), WBTC (BitGo/BiT Global, 86%), cbBTC (Coinbase, 86%), WETH (native, 86%) -- all established large-cap. Plus novel: steakUSDC (Morpho vault receipt token, 91.5% LLTV) and EUTBL (Spiko EU T-Bills MMF, 96.5% LLTV). The last two are not established large-cap assets: steakUSDC is a vault receipt token introducing recursive risk, EUTBL is a tokenized fund. Mixed collateral quality with some higher risk assets. | 3 | 3 | Non-Improvable | [P0] [Morpho V1 API](https://api.morpho.org/graphql) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | wstETH, WBTC, cbBTC, WETH: No >2% depeg lasting >24h in last 12 months. steakUSDC/EUTBL: Limited stress history but no deviations observed. All collateral tracked well during available history. | 9 | 9 | Non-Improvable (optimal) | [P3] Market data |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | wstETH present as collateral (~$1.1M, ~2.5% of deployed capital). Lido uses 30+ diversified operators. Minimal vault-level exposure. | 9 | 9 | Non-Improvable (optimal) | Lido operator data |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | Wrapped assets: WBTC ($2.43M) + cbBTC ($661K) = ~$3.09M out of $44.3M total TVL = ~7%. wstETH excluded (protocol receipt token per framework). steakUSDC/EUTBL excluded (vault/fund tokens, not bridged/wrapped). 7% is well below 20% threshold. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V1 API](https://api.morpho.org/graphql) |

**Collateral Subtotal: 37.5/45 (83.3%)**
- 3 questions scored 9 (sum = 27), 1 question scored 3 (sum = 3)
- Raw sum = 30 out of max 36
- Weighted = (30/36) x 45 = 37.5

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | All Tier-0/1: Ethereum (Tier-0), Chainlink-based oracle adapters for BTC/ETH markets. No bridges. No CEX dependency. EURCV depends on SG-FORGE as issuer. All dependencies identifiable. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V1 API](https://api.morpho.org/graphql), [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant are oracle and bridge setups, and can oracle values be corrected under abnormal conditions? | Each Morpho Blue market uses an immutable oracle -- no fallback, no correction post-deployment. Per mandatory hardcoded check: oracles price battle-tested assets (ETH, BTC) where material depeg is unprecedented. Chainlink is Tier-0. Caps at Mid (3) per framework. EUTBL oracle adds tokenized fund pricing surface area (96.5% LLTV, 3.5% buffer). | 3 | 3 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Morpho Labs/ADDMO: No public SOC 2 or ISO27001 found. Chainlink: Enterprise certified. SG-FORGE: ACPR licensed (French banking regulation) but not equivalent to SOC 2 for vault operations. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Ethereum: No significant halts. Morpho: April 2025 frontend resolved in 4 minutes. However, the EURCV vault itself is untested under meaningful stress — no significant market event has tested this vault's infrastructure behavior. Per scoring principle: untested protocols score Mid (3) on resilience questions. Consistent with Gauntlet EURC Core correction. | 3 | 9 | **Improvable** | [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain halts >30 minutes in last 12+ months. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Relevant for wstETH (~$1.1M, ~2.5% of deployed capital). Lido slashing trivial and absorbed. No depositor impact. | 9 | 9 | Non-Improvable (optimal) | Lido slashing data |
| ST-IC-07 | Are validators diverse geographically and by operator? | Ethereum validator set highly distributed. Lido uses 30+ independent operators. | 9 | 9 | Non-Improvable (optimal) | Ethereum validator data |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Permissionless on-chain redemption always available. V2 adds forceDeallocate. No off-chain dependency for withdrawals. EURCV issuer failure would impair token value but not block withdrawal mechanism. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |

**Infrastructure Counterparty Subtotal: 33.8/45 (75.0%)**
- 5 questions scored 9 (sum = 45), 3 questions scored 3 (sum = 9)
- Raw sum = 54 out of max 72
- Weighted = (54/72) x 45 = 33.75 = 33.8

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All allocation through Morpho Blue (Tier-0). No CEX exposure. However, the steakUSDC/EURCV market introduces recursive exposure to another Morpho vault (steakUSDC). The EUTBL/EURCV market exposes to Spiko EU T-Bills (tokenized government bond fund -- not a standard Tier-0/1 DeFi protocol). Both are disclosed and capped, but Spiko is not on the SR Protocol Tiers list. | 3 | 3 | Non-Improvable | [P0] [Morpho V1 API](https://api.morpho.org/graphql) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | V2 vault: 0% performance fee, 0% management fee (confirmed via API). V1 vault: 5% performance fee. No hidden rebates. Fee changes in V2 have 0-second timelock but sentinel can revoke. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P0] [Morpho V1 API](https://api.morpho.org/graphql) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. V2 absolute/relative caps per adapter. V1 on-chain supply caps per market. Cap increases require 7-day timelock; decreases immediate. Allocator rebalances within caps. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2), [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Most TVL is idle ($38.7M of $44.3M) -- unwinds instantly. Active positions ($5.6M) depend on borrower repayment. EURCV lending markets are newer and thinner than USDC equivalents. Rate model incentivizes repayment. V2 adds forceDeallocate. EURCV's limited DeFi liquidity means borrower repayment could be slower. | 3 | 3 | Non-Improvable | [P0] [Morpho V1 API](https://api.morpho.org/graphql) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending. Steakhouse (curator) disclosed. Underlying custodians publicly known: BitGo/WBTC, Coinbase/cbBTC, Lido/wstETH, SG-FORGE/EURCV, Spiko/EUTBL. | 9 | 9 | Non-Improvable (optimal) | Vault architecture |

**Protocol Counterparty Subtotal: 33.0/45 (73.3%)**
- 3 questions scored 9 (sum = 27), 2 questions scored 3 (sum = 6)
- Raw sum = 33 out of max 45
- Weighted = (33/45) x 45 = 33.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain ERC4626 redemption. No address-level blocking. No admin pause. V2 forceDeallocate adds permissionless exit. Gates require 7-day timelock to change. Current ~87.4% idle means most capital instantly available. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | V1 vault has ~$38.7M idle EURCV, immediately available. V2 TVL is $33.3M, so the idle buffer exceeds V2 TVL. For in-protocol redemption, sufficient. However, V2 represents ~32% of total EURCV supply (~$104M). Converting redeemed EURCV to other assets depends on thin secondary markets. In-protocol capacity adequate for ~3-10% of TVL. | 3 | 3 | Non-Improvable | [P0] [Morpho V1 API](https://api.morpho.org/graphql), [P0] [Etherscan EURCV](https://etherscan.io/token/0x5F7827FDeb7c20b443265Fc2F40845B715385Ff2) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No documented delays. High idle ratio suggests smooth operations. However, vault is untested under significant withdrawal stress. "No problems because never tested" does not equal proven resilience. Per scoring principle: untested vault scores Mid (3). | 3 | 9 | **Improvable** | Operational history |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Caps appropriately sized. Current high idle ratio means caps are not binding. V2 caps enforced on allocation, not withdrawal. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Untested. EURCV vault has not experienced significant stress. EURCV is a newer stablecoin with limited DeFi liquidity. During volatility, EURCV holders face conversion challenges. High idle ratio is a positive buffer but exit behavior under stress unknown. Per scoring principle: untested scores Mid (3). | 3 | 3 | Non-Improvable | [P0] [Morpho V1 API](https://api.morpho.org/graphql) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure EURCV lending, no lockups, vesting, or bridges. Idle capital (~87.4%) instantly available. Active positions depend on borrower repayment. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Primary ERC4626 redemption always available (users receive EURCV). However, EURCV has extremely thin DeFi secondary market. Unlike USDC/USDT, EURCV cannot be easily swapped on DEXs. Practical exit to USD or fiat EUR requires SG-FORGE institutional redemption or finding EURCV DEX liquidity (very limited). Effective secondary-market dependency for users wanting liquid assets. | 1 | 3 | **Improvable** | [P0] [Etherscan EURCV](https://etherscan.io/token/0x5F7827FDeb7c20b443265Fc2F40845B715385Ff2) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | EURCV DeFi liquidity extremely thin. ~$104M supply, ~2,700 holders. Vault shares (steakEURCV) have ~16 holders. No deep DEX pools. Depth supports <3% of TVL without major impact. Collateral tokens (wstETH, WBTC, WETH) are deeply liquid but EURCV (loan asset) is the bottleneck. | 1 | 3 | **Improvable** | [P0] [Etherscan EURCV](https://etherscan.io/token/0x5F7827FDeb7c20b443265Fc2F40845B715385Ff2) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Currently ~87.4% idle mitigates bank-run risk. If all idle were deployed, bank-run would cause significant queues + rate spikes. EURCV's thin DeFi liquidity amplifies risk. Untested under stress. Per scoring principle: untested scores Mid (3). | 3 | 3 | Non-Improvable | [P0] [Morpho V1 API](https://api.morpho.org/graphql) |

**Liquidity Subtotal: 22.8/45 (50.6%)**
- 3 questions scored 9 (sum = 27), 4 questions scored 3 (sum = 12), 2 questions scored 1 (sum = 2)
- Raw sum = 41 out of max 81
- Weighted = (41/81) x 45 = 22.78 = 22.8

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | V2 vault shares represent 1:1 EURCV claim plus accrued yield (ERC4626 NAV-based). steakEURCV has ~16 holders, very limited trading. Untested under stress. Per scoring principle: untested scores Mid (3). Evaluates vault share, not EURCV itself. | 3 | 9 | **Improvable** | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P0] [Etherscan steakEURCV](https://etherscan.io/token/0x75741A12B36D181f44F389E0c6B1E0210311e3Ff) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Low. Vault lends EURCV -- EUR-denominated. No directional BTC/ETH exposure for lenders. Risk is borrower default creating bad debt, not market direction. EURCV backed by Societe Generale with MiCA compliance -- stronger issuer profile than USDT. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics, [P1] [SG-FORGE](https://www.sgforge.com/product/coinvertible/) |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Immutable Adaptive Curve IRM per market. EURCV markets newer and less battle-tested than USDC equivalents. Very high idle ratio (87.4%) suggests rate models not stress-tested at high utilization. Untested. Per scoring principle: untested scores Mid (3). | 3 | 9 | **Improvable** | [P0] [Morpho V1 API](https://api.morpho.org/graphql) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | 86% LLTV on wstETH/WBTC/cbBTC/WETH provides 14% buffer. 96.5% LLTV on EUTBL provides only 3.5% buffer. Liquidation formally verified by Certora. However, EURCV-specific modeling (EUR/USD volatility, EURCV depeg scenarios, EUTBL behavior) not publicly demonstrated. | 3 | 9 | **Source Missing** | [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side only. Vault lenders benefit from liquidations. Risk: insufficient liquidation creating socialized bad debt. Primary collateral (wstETH/WBTC at 86% LLTV) has ~14% buffer. EUTBL at 96.5% LLTV has thin 3.5% buffer but is a tokenized government bond fund with low volatility. | 9 | 9 | Non-Improvable (optimal) | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 27.0/45 (60.0%)**
- 2 questions scored 9 (sum = 18), 3 questions scored 3 (sum = 9)
- Raw sum = 27 out of max 45
- Weighted = (27/45) x 45 = 27.0

---

### **Strategy Total: 196.1/270 (72.6%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 38.3 | 45 | 85.2% |
| Collateral | 37.5 | 45 | 83.3% |
| Infra Counterparty | 33.8 | 45 | 75.0% |
| Protocol Counterparty | 33.0 | 45 | 73.3% |
| Liquidity | 22.8 | 45 | 50.6% |
| Market | 27.0 | 45 | 60.0% |
| **Strategy Total** | **192.4** | **270** | **71.3%** |

---

### OPERATIONS (30% Weight) -- Score: 230.0/270 (85.2%)

**NOTE: All Operations scores are IDENTICAL to the existing Steakhouse USDT V2 rating EXCEPT O-FR-04 (3 for EURCV vs 9 for USDT V2, because the EURCV vault is untested under stress while the USDT V1 infrastructure demonstrated resilience in November 2025).**

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid with strong checks. Morpho Blue: immutable. V2 changes: Curator (timelocked) + Sentinel revoke + Owner (Aragon DAO). V1 changes: Owner 5-of-8 Safe + 7-day timelock + Guardian veto. Per-function timelocks in V2 provide granular control. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | V2 Owner is Aragon DAO with permission-based governance. V1 Guardian voting distributed proportionally across depositors. No single entity can unilaterally control. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Owner DAO](https://etherscan.io/address/0xE67d850dE6E6Fc913fb613573dc00d3Ba863C099) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. V2 per-function timelocks: 7 days for critical operations. Sentinel can revoke. Abdicate function permanently disables specific curator functions. V1 also has 7-day timelock + Guardian veto. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner (Aragon DAO) can appoint new Curator. Withdrawals remain permissionless via ERC4626. V2 forceDeallocate provides additional exit path. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 4 questions, all scored 9
- Raw sum = 36 out of max 36
- Weighted = (36/36) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Steakhouse: adcv (co-founder), Sebastien Derivaux (co-founder, former MakerDAO Head of RWA). Morpho: Paul Frambot (CEO). All publicly identified with verifiable backgrounds. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse](https://www.steakhouse.financial/), [P1] [Morpho](https://morpho.org/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Morpho has full team in Paris (~$73.6M raised). Steakhouse is a separate entity with its own team. Multiple independent parties capable of operations. | 9 | 9 | Non-Improvable (optimal) | [P4] [Tracxn](https://tracxn.com/d/companies/morpho/__5iKpzjF_-EXELsu5bJ6cORHuQN7HD3ItPqKPexS2FVw) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Morpho: ADDMO (French nonprofit) + Morpho Labs SAS (France). Steakhouse: Carniciera Tropical Inc. (Panama) + Steakhouse Financial Ltd (Cayman Islands). All entities clearly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/), [P2] [Forum](https://forum.morpho.org/t/key-information-on-steakhouse-branded-vaults/1343) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known actions against ADDMO, Morpho Labs, Steakhouse, or Carniciera Tropical in any major jurisdiction. | 9 | 9 | Non-Improvable (optimal) | Public records |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Partial. Monitoring bots + Chainalysis confirmed. April 2025 incident shows rapid 4-minute response. However, no public 24/7 on-call SLA, formal incident runbook, or response SLA documentation. Vault uses automated allocation (V2 allocators) but no documented procedure to halt automated capital flows during incidents. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. April 2025: 4-minute response. Active Discord community. Steakhouse publishes regular Kitchen newsletter. | 9 | 9 | Non-Improvable (optimal) | [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. a16z, Variant Fund, Pantera Capital, Coinbase Ventures (29 investors total, $73.6M raised). | 9 | 9 | Non-Improvable (optimal) | [P4] [Tracxn](https://tracxn.com/d/companies/morpho/__5iKpzjF_-EXELsu5bJ6cORHuQN7HD3ItPqKPexS2FVw) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Steakhouse manages 19+ vaults including both EURC and EURCV variants, V1 and V2, plus USDC and USDT products. The V2 vault wraps V1, creating potential allocation priority conflicts. Limited hard constraints -- DDQ process provides qualitative controls but no formal conflict-of-interest policy with quantitative rules. | 3 | 9 | **Improvable** | [P2] [Forum](https://forum.morpho.org/t/key-information-on-steakhouse-branded-vaults/1343) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | No. Zero bad debt across all Steakhouse vaults since inception. November 2025: zero bad debt confirmed while other curators experienced losses. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |

**Team & Legal Subtotal: 57.5/67.5 (85.2%)**
- 7 questions scored 9 (sum = 63), 2 questions scored 3 (sum = 6)
- Raw sum = 69 out of max 81
- Weighted = (69/81) x 67.5 = 57.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Morpho Docs comprehensive including V2 documentation. Steakhouse publishes vault controls, risk management docs, Kitchen newsletter. V2 source on GitHub. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Docs](https://docs.morpho.org/), [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Detailed explanation of liquidation mechanics, bad debt scenarios, oracle risks, liquidity risks. V2 adds documentation of forceDeallocate penalty, caps system. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Morpho docs maintain canonical address registry covering all chains. V2 vault address clearly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. V2 per-function timelock visible via GraphQL API. Owner, Curator, Sentinel, Allocator roles clearly specified. Source verified on Etherscan. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves. V2 adapter allocations visible via API and Etherscan. V1 market allocations fully transparent. All auditable on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan V2 Vault](https://etherscan.io/address/0xbeef0C075Da5D01112AE5cF34d257074fB5DDB2f) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. All V2 contracts verified on Etherscan: V2 vault, V1 adapter, V1 vault, Morpho Blue, Owner DAO, Sentinel. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xbeef0C075Da5D01112AE5cF34d257074fB5DDB2f) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions, all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated safety module. Bad debt socialized among lenders per market. Morpho DAO treasury (~$34.1M, mostly MORPHO tokens) activation entirely discretionary. | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/), [P3] [DeFiLlama Treasury](https://api.llama.fi/treasury/morpho) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Morpho DAO treasury ~$34.1M: Ethereum $11.4M own tokens + $8K non-own; Base $22.7M own tokens + $2 non-own. ~99.98% MORPHO tokens (volatile native token) with ~$8,143 in liquid non-own assets. Against protocol-wide TVL of ~$6.7B: ~0.51% including own tokens. Not ring-fenced for this vault. Treasury composition almost entirely illiquid native token. | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Morpho raised $73.6M total. Nonprofit structure reduces overhead. Curator fees growing. Steakhouse earns fees on other vaults (V1 EURCV vault charges 5% performance fee). Runway comfortably above 24 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | EURCV vault specifically has NOT been tested under stress conditions. The broader Morpho/Steakhouse ecosystem demonstrated resilience during November 2025 (zero Steakhouse bad debt, protocol-wide TVL grew despite stress). However, this specific EURCV vault with its unique asset has no stress-test history. Per scoring principle: untested protocols score Mid (3). | 3 | 9 | **Improvable** | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue is immutable. Permissionless withdrawals always available via V2 ERC4626 -> V1 adapter -> V1 vault -> Morpho Blue. V2 adds forceDeallocate. No off-chain services required. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Financial Resilience Subtotal: 37.5/67.5 (55.6%)**
- 2 questions scored 9 (sum = 18), 2 questions scored 3 (sum = 6), 1 question scored 1 (sum = 1)
- Raw sum = 25 out of max 45
- Weighted = (25/45) x 67.5 = 37.5

---

### **Operations Total: 239.0/270 (88.5%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 67.5 | 67.5 | 100.0% |
| Team & Legal | 57.5 | 67.5 | 85.2% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 37.5 | 67.5 | 55.6% |
| **Operations Total** | **230.0** | **270** | **85.2%** |

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 87 | 99 | 158.2 | 180 | 87.9% |
| | Key Management (8 Q) | 66 | 72 | 165.0 | 180 | 91.7% |
| | **Security Subtotal** | | | **323.2** | **360** | **89.8%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 69 | 81 | 38.3 | 45 | 85.2% |
| | Collateral (4 Q) | 30 | 36 | 37.5 | 45 | 83.3% |
| | Infra Counterparty (8 Q) | 54 | 72 | 33.8 | 45 | 75.0% |
| | Protocol Counterparty (5 Q) | 33 | 45 | 33.0 | 45 | 73.3% |
| | Liquidity (9 Q) | 41 | 81 | 22.8 | 45 | 50.6% |
| | Market (5 Q) | 27 | 45 | 27.0 | 45 | 60.0% |
| | **Strategy Subtotal** | | | **192.4** | **270** | **71.3%** |
| **Operations** | Governance (4 Q) | 36 | 36 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 69 | 81 | 57.5 | 67.5 | 85.2% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 25 | 45 | 37.5 | 67.5 | 55.6% |
| | **Operations Subtotal** | | | **230.0** | **270** | **85.2%** |
| **TOTAL** | | | | **745.6** | **900** | **82.8%** |

---

