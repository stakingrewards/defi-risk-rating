# Morpho - Steakhouse Prime Instant V2 USDT Vault Risk Rating

**Rating Date**: 2026-04-09
**Final Grade**: BB-
**Total Score**: 754.75/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-beta

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 293.2/360 (81.4%)

**NOTE: Smart Contract Security scores are platform-level and IDENTICAL to all other Steakhouse/Morpho vault ratings. The V2 vault inherits Morpho's security infrastructure (25+ audits, formal verification, $2.5M bug bounty) and uses the same Curator Safe (2-of-5). Key Management scores differ from V1 because the V2 Owner is an Aragon DAO whose governance parameters (voting power distribution, quorum, proposal thresholds) could not be verified on-chain, unlike V1's 5-of-8 Safe multisig which is directly verifiable.**

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 25+ total audits, 11 specifically for Vaults V2 from Tier-0/1 firms: ChainSecurity, Spearbit, Certora, Zellic, Cantina contest, Blackthorn. Both Morpho Blue core and Vaults V2 framework extensively audited. Formal verification by Certora with mathematical proofs. The MorphoVaultV1Adapter connecting V2 to V1 is covered by the V2 audit scope (Dec 2025 MarketV1AdapterV2 audits by Certora, Spearbit, Blackthorn). | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | December 2025: Certora (Tier-0), Spearbit (Tier-0 via Cantina), Blackthorn for Vaults V2 MarketV1AdapterV2. September 2025: ChainSecurity (Tier-0) for Vaults V2 core. Multiple Tier-0 auditors for most recent work. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable (~600 LOC). The V2 vault contract is non-upgradeable (deployed ~Nov 2025, 125 days ago). Every component of the V2 launch (Jul-Dec 2025) was preceded by multiple audits from Tier-0 firms. The V1 adapter has dedicated audits (Dec 2025). | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P0] [Etherscan V2 Vault](https://etherscan.io/address/0xbeef003C68896c7D2c3c60d363e8d71a49Ab2bf9) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 vulnerability patched immediately with OpenZeppelin. Certora formal verification provides mathematical proof of critical invariants. All V2 audit findings resolved before deployment with multiple re-reviews. V2 includes new security features: virtual shares (inflation attack protection), maxRate cap (prevents runaway share inflation), transient storage optimization. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM), [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | V2 vault is non-upgradeable ERC4626 contract. Morpho Blue core is immutable. The V2 Owner is an Aragon DAO (ERC1967 proxy at 0xFb345Ae -- the DAO itself is upgradeable but its implementation points to Aragon OSx). Critical vault parameter changes require per-function timelocks: 7 days (604800s) for adapter changes, cap increases, gate changes, timelock increases, and abdicate. Sentinel can revoke pending timelocked actions. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P0] [Etherscan V2 Vault](https://etherscan.io/address/0xbeef003C68896c7D2c3c60d363e8d71a49Ab2bf9), [P0] [Etherscan Owner DAO](https://etherscan.io/address/0xFb345Ae28cCe3C55481190771e8c6D18c0f3D279) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss in Steakhouse vaults. April 2025 frontend vulnerability ($2.6M) was intercepted by white hat c0ffeebabe.eth and all funds returned within minutes. October 2024 oracle exploit ($230K) affected only PAXG/USDC market, not this vault. November 2025 Stream/Elixir contagion affected MEV Capital vault (3.6% bad debt), NOT Steakhouse vaults. March 2026 phishing attack on Steakhouse domain served malicious frontend; no contracts affected, no deposits at risk. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P4] [Cointelegraph](https://cointelegraph.com/news/white-hat-intercepts-2-million-morpho-blue-hack), [P1] [Binance Square](https://www.binance.com/en/square/post/03-30-2026-steakhouse-financial-warns-users-of-phishing-attack-on-domain-307105025811217) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho operates as ADDMO, a French nonprofit association. Steakhouse has 2+ year track record managing curated vaults. No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. V2 vault deployed ~Nov 2025 with 7-day (604800s) timelocks on critical functions, confirmed via Morpho GraphQL API. Per-function timelocks add granularity: 7 days for critical operations, 0 for operational adjustments (allocator changes, fee changes, cap decreases). No decreaseTimelock calls observed. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active public bounty on Cantina with $2.5M max payout for critical vulnerabilities. 552 findings submitted. Scope explicitly covers Vaults V2 (VaultV2Factory, adapters, registries) plus V1 contracts and web apps. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Internal monitoring bots perform continuous invariant checks on each market after each transaction. Chainalysis partnership for transaction monitoring. April 2025 incident: alert received and frontend rolled back within 4 minutes. However, per the v0.1-beta framework verification principle, monitoring exists but cannot automatically trigger protective actions -- all responses require manual human intervention. Automated allocation flows (via allocators) are not covered by any automated halt mechanism. Same limitation as all Morpho vaults (platform-level). | 3 | 9 | **Improvable** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. Morpho Blue prioritizes immutability over admin controls. Sentinel can revoke pending timelocked actions but cannot pause the protocol or halt allocations. V2 adds the abdicate function (permanent one-way disable of functions) and forceDeallocate (permissionless withdrawal from illiquid markets with penalty), but these are not automatic circuit breakers triggered by monitoring. Market-level isolation provides containment. | 3 | 3 | Non-Improvable | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |

**Smart Contract Security Subtotal: 158.2/180 (87.9%)**
- 9 questions scored 9 (sum = 81), 2 questions scored 3 (sum = 6)
- Raw sum = 87 out of max 99
- Weighted = (87/99) x 180 = 158.18 = 158.2

---

#### Key Management & Permissions (20% weight, 180 max points)

**NOTE: V2 introduces an Aragon DAO as Owner (replacing the V1 5-of-8 Safe), a specialized Revoker/Sentinel (replacing V1 Guardian), and retains the same 2-of-5 Curator Safe. S-KM-01 and S-KM-03 score Mid (3) because the Aragon DAO's governance parameters (voting power distribution, quorum requirements, proposal thresholds) could not be verified on-chain -- classified as Source Missing. This contrasts with V1's 5-of-8 Safe which is directly verifiable via Safe API.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Owner: Aragon DAO proxy (0xFb345Ae28cCe3C55481190771e8c6D18c0f3D279, ERC1967Proxy to Aragon OSx DAO implementation). This is a DAO contract, not a multisig -- voting power distribution and decision-making process not publicly verified. Curator: Gnosis Safe 2-of-5 multisig (0x827e86072B06674a077f592A531dcE4590aDeCdB, verified via Safe API). Sentinel: Revoker contract (0xc41F4709d0B9D637675aca1bF228732259d1606f) restricting sentinel to only call revoke. All role changes visible on-chain. | 3 | 9 | **Source Missing** | [P0] [Safe API - Curator](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x827e86072B06674a077f592A531dcE4590aDeCdB/), [P0] [Etherscan Owner DAO](https://etherscan.io/address/0xFb345Ae28cCe3C55481190771e8c6D18c0f3D279), [P0] [Etherscan Sentinel](https://etherscan.io/address/0xc41F4709d0B9D637675aca1bF228732259d1606f) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. V2 vault contract is non-upgradeable. Moving user funds requires going through Morpho Blue immutable contract logic. Owner (Aragon DAO) controls curator/sentinel appointment with per-function timelocks (7 days for critical operations). Curator timelocked operations require 7-day delay. Sentinel can only revoke pending actions. Permissionless redemption always available via ERC4626. The V2 forceDeallocate function is permissionless (anyone can call) but includes a penalty mechanism to prevent abuse. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner is an Aragon DAO -- claimed to provide depositor-proportional governance, but DAO voting power distribution, quorum requirements, and proposal thresholds could not be verified on-chain. Per framework: "If signer identities are fully unknown, independence cannot be confirmed -- score Mid (3) at best, classify as Source Missing." Curator is a 2-of-5 Safe (verified via Safe API: 5 distinct owner addresses). One signer identified on Etherscan as "Steakhouse Financial: Deployer" (pitmaster.eth, 0x0D61C8b6CA9669A36F351De3AE335e9689dd9C5b). | 3 | 9 | **Source Missing** | [P0] [Safe API - Curator](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x827e86072B06674a077f592A531dcE4590aDeCdB/), [P0] [Etherscan Owner DAO](https://etherscan.io/address/0xFb345Ae28cCe3C55481190771e8c6D18c0f3D279) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking capability. No pause function on Morpho Blue (immutable) or V2 vault. Sentinel can only revoke pending timelocked actions. V2 adds Gates system for controlling share/asset transfers, but gates are timelocked (7 days) to change. Withdrawals always permissionless via direct smart contract interaction. V2's forceDeallocate adds a permissionless exit path even for illiquid adapter positions. Rules publicly documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets held in non-custodial smart contracts: V2 vault -> V1 adapter -> V1 MetaMorpho -> Morpho Blue markets. All on Ethereum. Permissionless redemption via ERC4626. No off-chain custody component. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan V2 Vault](https://etherscan.io/address/0xbeef003C68896c7D2c3c60d363e8d71a49Ab2bf9), [P0] [Etherscan V1 Adapter](https://etherscan.io/address/0x233a0097F9D931A435Ba92ebb832a34c39135696) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. Morpho is a nonprofit with no profit extraction from protocol operations. Vault funds flow through the adapter to Morpho Blue markets, fully separate from any treasury or operational wallets. Performance fee is 0%, management fee is 0%. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P1] [Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | V2 uses an adapter registry and adapter whitelist. Currently only one adapter registered: MorphoVaultV1Adapter (0x233a0097F9D931A435Ba92ebb832a34c39135696) pointing to the V1 steakUSDT vault (0xBEEF047a). Adding new adapters requires Curator + 7-day timelock. The underlying V1 vault markets are: wstETH/USDT, sUSDS/USDT, WBTC/USDT, cbBTC/USDT, XAUt/USDT. New market additions on V1 also require Curator + 7-day timelock + Guardian veto. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P0] [Etherscan V1 Adapter](https://etherscan.io/address/0x233a0097F9D931A435Ba92ebb832a34c39135696), [P0] [Morpho V1 API](https://api.morpho.org/graphql) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Partial. Guardian drill conducted January 2024 for V1 vaults demonstrated the veto mechanism but revealed low participation (only one depositor voted, though quorum was met). V2 vault has a Sentinel/Revoker contract rather than a depositor-governed Guardian -- the Revoker can only call revoke, narrowing the scope but also meaning no depositor participation in emergency veto for V2. No comprehensive public key rotation playbook. No tabletop exercise for V2-specific scenarios (DAO compromise, curator compromise) documented. | 3 | 9 | **Improvable** | [P2] [Guardian Report](https://kitchen.steakhouse.financial/p/steakusdc-guardian-report), [P0] [Etherscan Sentinel](https://etherscan.io/address/0xc41F4709d0B9D637675aca1bF228732259d1606f) |

**Key Management Subtotal: 135.0/180 (75.0%)**
- 5 questions scored 9 (sum = 45), 3 questions scored 3 (sum = 9)
- Raw sum = 54 out of max 72
- Weighted = (54/72) x 180 = 135.0

---

### **Security Total: 293.2/360 (81.4%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 158.2 | 180 | 87.9% |
| Key Management | 135.0 | 180 | 75.0% |
| **Security Total** | **293.2** | **360** | **81.4%** |

---

### STRATEGY (30% Weight) -- Score: 233.8/270 (86.6%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from overcollateralized USDT lending against diversified crypto collateral via the underlying V1 vault. Current market breakdown: wstETH/USDT (61%), sUSDS/USDT (28%), WBTC/USDT (8%), XAUt/USDT (3%). 100% mandate-aligned. Yield sources documented via Morpho API with market-level breakdown. Small MORPHO rewards component (~0.10% of total 2.83% APY). | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V1 API](https://api.morpho.org/graphql), [P3] [Vaults.fyi](https://app.vaults.fyi/opportunity/mainnet/0xbeef003C68896c7D2c3c60d363e8d71a49Ab2bf9) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail shocks PLUS USDT-specific risk: (1) simultaneous ETH/BTC crash exceeding liquidation buffers (86% LLTV provides ~14% buffer for wstETH/WBTC markets); (2) sUSDS depeg -- this market has 96.5% LLTV with only ~3.5% buffer, making it sensitive to sUSDS/USDT price deviation; (3) oracle manipulation on immutable oracle; (4) USDT depeg -- S&P rated Tether stability "weak" (5/5) in November 2025, with 24% of reserves in riskier assets. A USDT depeg would directly impair depositor purchasing power regardless of lending performance. | 3 | 3 | Non-Improvable | [P4] [S&P Tether Report](https://www.theblock.co/post/380562/tether-usdt-stability-score-weak-sp-reserves-cant-absorb-bitcoin-drop), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault simply lends USDT through the V1 adapter. No rehypothecation of depositor funds. Effective leverage: 1.0x. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. Liquidation risk applies to borrowers in the underlying markets. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss events for Steakhouse USDT vault (V1 or V2) or any Steakhouse vault since inception. During November 2025 Stream/Elixir contagion, Steakhouse vaults had ZERO bad debt. The V2 vault wraps the same V1 vault, so the loss history is identical and clean. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/products/steakhouse-financial-products/morpho-vaults) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Steakhouse publishes vault controls documentation with DDQ process (2 internal + 1 external reviewer). Credora A+ rating (best-in-class among Morpho curators). On-chain caps per market in V1, absolute/relative caps per adapter in V2. 7-day timelock + Sentinel veto in V2. V2 adds the abdicate function for permanently disabling specific curator functions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls), [P2] [Credora Ratings](https://forum.morpho.org/t/credora-network-risk-ratings-on-morpho/1652) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. Base yield (2.63%) is primarily organic from USDT lending demand driven by leveraged borrowers. MORPHO rewards (~0.10%) are a minor component (<4% of total yield). Strategy remains strongly positive after removing incentives. steakUSDT token price indicates consistent yield accrual. | 9 | 9 | Non-Improvable (optimal) | [P3] [Vaults.fyi](https://app.vaults.fyi/opportunity/mainnet/0xbeef003C68896c7D2c3c60d363e8d71a49Ab2bf9), [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes. USDT is highly liquid (>$140B market cap). During November 2025 stress, the V1 Steakhouse vault withdrawals processed within days. V2 adds the forceDeallocate function as a permissionless exit path even when the adapter is illiquid (with a penalty). Slippage limited to rate model dynamics (4x rate at 100% utilization incentivizes rapid repayment). | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2), [P0] [Morpho V1 API](https://api.morpho.org/graphql) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No reliance on invertible spreads for yield generation. Pure lending interest from overcollateralized borrower demand. Interest rates are set by immutable Adaptive Curve IRM based on utilization. The underlying asset (USDT) is a peg -- if USDT depegs, depositor value is impaired, but this is an asset-level risk, not a strategy-level spread dependency. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | V2 architecture: Allocators can move funds between adapters within cap boundaries without timelock. The underlying V1 vault also has allocators and the Public Allocator. Supply caps per market/adapter limit maximum exposure. However, no automatic kill-switch exists for abnormal conditions (oracle deviation, collateral depeg). The March 2026 Resolv exploit demonstrated this risk on other Morpho vaults. Halting requires manual curator/allocator intervention. | 3 | 9 | **Improvable** | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2), [P1] [Morpho Public Allocator](https://docs.morpho.org/curate/concepts/public-allocator/) |

**Protocol Mechanics Subtotal: 38.3/45 (85.2%)**
- 9 applicable questions (ST-PM-04 = N/A): 7 scored 9 (sum = 63), 2 scored 3 (sum = 6)
- Raw sum = 69 out of max 81
- Weighted = (69/81) x 45 = 38.33 = 38.3

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Diversified collateral via underlying V1 vault: wstETH (Lido, 61% of allocation, 86% LLTV), sUSDS (Sky/MakerDAO savings, 28%, 96.5% LLTV), WBTC (BitGo/BiT Global, 8%, 86% LLTV), XAUt (Tether Gold, 3%, 77% LLTV), cbBTC (Coinbase custody, 0% current, 86% LLTV). All are established assets. wstETH is a protocol receipt token (excluded from wrapped definition). sUSDS is a Sky savings product. WBTC/cbBTC are wrapped BTC. XAUt is Tether-issued tokenized gold. Blue-chip quality with conservative LLTVs. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V1 API](https://api.morpho.org/graphql), [P2] [xAUT Collateral Proposal](https://forum.morpho.org/t/steakusdt-adding-xaut-as-collateral-on-steakusdt/1718) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | wstETH: Stable tracking of underlying stETH value, no >2% depeg in last 12 months. sUSDS: Tracks USDS value closely; no significant deviation. WBTC: Briefly depegged during historical events but recovered within 24 hours. XAUt: Tracks gold price closely. cbBTC: No depeg >2% since September 2024 launch. No collateral showed >2% depeg lasting >24h in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P3] Market data |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | wstETH (61% of allocation) has staking exposure. Lido uses 30+ diversified operators across multiple jurisdictions. Lido slashing insurance/coverage fund absorbs minor events. Given wstETH's dominant allocation share, slashing risk is more relevant here than in the V1 rating where BTC collateral dominated. Lido's track record and diversification are strong mitigants. | 9 | 9 | Non-Improvable (optimal) | Lido operator data |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | IMPROVED vs V1 rating. Current allocation: wstETH (61%) is a protocol receipt token per framework definition -- EXCLUDED from wrapped/bridged count. sUSDS (28%) is a Sky savings product -- not a bridged/wrapped asset. WBTC (8%) and cbBTC (0%) are wrapped BTC -- INCLUDED. XAUt (3%) is a Tether-issued wrapped gold token -- INCLUDED. Total wrapped/bridged: ~11% of allocation (8% WBTC + 3% XAUt). This is well below the 20% threshold for Low Risk. The allocation has shifted dramatically from the V1 rating's ~98% wrapped concentration. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V1 API](https://api.morpho.org/graphql) |

**Collateral Subtotal: 45.0/45 (100.0%)**
- 4 questions, all scored 9
- Raw sum = 36 out of max 36
- Weighted = (36/36) x 45 = 45.0

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | All Tier-0: Ethereum (chain), Chainlink (primary oracle provider for BTC and ETH markets). No bridges required. No CEX dependency for operations. Oracle providers documented per market. The sUSDS/USDT market uses a specific oracle (0x0C426d) and the XAUt market uses a gold-price oracle (0xc7d1FE). | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V1 API](https://api.morpho.org/graphql), [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant are oracle and bridge setups, and can oracle values be corrected under abnormal conditions? | SINGLE ORACLE RISK with immutable pricing. Each Morpho Blue market has one immutable oracle -- no fallback mechanism possible post-deployment and oracle values cannot be updated, overridden, or corrected after deployment. Per the v0.1-beta mandatory hardcoded/immutable oracle check: the oracles price battle-tested, deep-liquidity assets (ETH, BTC, sUSDS against USDT) where material depeg is historically unprecedented for the primary assets. Chainlink is Tier-0, but zero redundancy and zero ability to correct under abnormal conditions by design. XAUt adds gold price oracle surface area. Caps at Mid (3) per framework. | 3 | 3 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Morpho Labs/ADDMO: No public SOC 2 Type II or ISO27001 certification found. Chainlink: Enterprise certifications in place. Coinbase (cbBTC custodian): NY DFS regulated, SOC 2 certified. No evidence of Morpho or Steakhouse holding such certifications. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Ethereum: No significant halts affecting operations. Morpho: April 2025 frontend vulnerability resolved in 4 minutes. November 2025 stress: protocol operated correctly (market isolation worked, liquidations processed, no system failures). V1 steakUSDT vault experienced zero bad debt. March 2026: Steakhouse domain phishing attack; smart contracts and vaults unaffected. | 9 | 9 | Non-Improvable (optimal) | [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain halts >30 minutes in the last 12+ months. Tier-0 chain reliability. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Relevant for wstETH (61% of underlying allocation). Lido slashing events have been trivial and fully absorbed by Lido's coverage fund. No depositor impact. Given the significant wstETH allocation, this is more relevant than in a BTC-dominated vault, but Lido's track record is strong. | 9 | 9 | Non-Improvable (optimal) | Lido slashing data |
| ST-IC-07 | Are validators diverse geographically and by operator? | Ethereum validator set is highly distributed across geographies and operators. Lido (for wstETH, 61% of allocation) uses 30+ independent operators. No single operator >33% of relevant stake. | 9 | 9 | Non-Improvable (optimal) | Ethereum validator data |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Permissionless on-chain redemption is always available via direct smart contract interaction (V2 ERC4626 withdraw/redeem -> V1 adapter -> V1 vault -> Morpho Blue). V2 adds forceDeallocate as an additional permissionless exit path. No off-chain dependency for withdrawals. Frontend failure does not block on-chain operations. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Infrastructure Counterparty Subtotal: 37.5/45 (83.3%)**
- 6 questions scored 9 (sum = 54), 2 questions scored 3 (sum = 6)
- Raw sum = 60 out of max 72
- Weighted = (60/72) x 45 = 37.5

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All allocation flows through V2 -> V1 adapter -> V1 MetaMorpho vault -> Morpho Blue markets only (Tier-0 protocol, 25+ audits, formally verified). No CEX exposure. No RWA platforms. Markets clearly listed with on-chain caps. The sUSDS/USDT market introduces exposure to Sky Protocol (Tier-0, formerly MakerDAO). | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V1 API](https://api.morpho.org/graphql), [P0] [Etherscan V1 Adapter](https://etherscan.io/address/0x233a0097F9D931A435Ba92ebb832a34c39135696) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Yes. V2 vault: 0% performance fee, 0% management fee (confirmed via Morpho V2 GraphQL API). V1 vault also has 0% fee. MORPHO rewards are publicly distributed. Fee changes in V2 have 0-second timelock but sentinel can revoke. No hidden rebates or undisclosed arrangements found. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P2] [Forum](https://forum.morpho.org/t/key-information-on-steakhouse-branded-vaults/1343) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. V2 uses absolute and relative caps per adapter (enforced during allocate). V1 uses on-chain supply caps per market. Allocator rebalances within caps. New adapter/market additions require Curator + 7-day timelock. Cap increases subject to 7-day timelock; decreases are immediate (fast-track for de-risking). | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2), [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Lending positions can be unwound as borrowers repay. November 2025 stress demonstrated V1 Steakhouse vaults processed approximately 80% of withdrawals within 3 days. Rate model (4x at 100% utilization) creates strong incentive for rapid borrower repayment. V2 adds forceDeallocate for permissionless exit from illiquid adapter positions (with penalty). No discretionary approvals needed. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending -- no external validators, custodians, or asset managers involved in vault operations. Collateral is held in Morpho Blue smart contracts. Steakhouse Financial (curator) is disclosed. Underlying collateral custodians (Coinbase for cbBTC, BitGo for WBTC, Lido for wstETH, Sky for sUSDS, Tether for XAUt) are publicly known. | 9 | 9 | Non-Improvable (optimal) | Vault architecture |

**Protocol Counterparty Subtotal: 45.0/45 (100.0%)**
- 5 questions, all scored 9
- Raw sum = 45 out of max 45
- Weighted = (45/45) x 45 = 45.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain redemption via ERC4626 standard on both V2 and underlying V1 vaults. No address-level blocking capability. No admin pause function. V2 adds forceDeallocate for permissionless exit from illiquid adapters (with penalty). Gates can restrict share/asset transfers but require 7-day timelock to change. Withdrawal availability depends on market liquidity in underlying V1 vault. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Moderate. V2 vault holds ~$11.4M via the V1 adapter. Under normal conditions, substantial USDT available for withdrawal. However, the underlying V1 vault has ~$138.3M with high utilization across markets (wstETH at 90%, sUSDS at 91%, WBTC at 91%). During November 2025 stress, some markets temporarily reached 100% utilization. Rate spikes incentivize repayment within days, but instant 100% exit not guaranteed. The V2 vault is only ~8% of V1 TVL, so its redemptions are proportionally smaller and more likely to succeed. | 3 | 3 | Non-Improvable | [P0] [Morpho V1 API](https://api.morpho.org/graphql), [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | Minor delays during November 2025 stress period only, affecting the underlying V1 vault. Over the full operational period, the vast majority (>95%) of withdrawals completed promptly. V2 vault is newer (~125 days old) but operates through the same V1 infrastructure that has proven resilient. Steakhouse vaults recovered quickly with zero bad debt. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Nov 2025](https://morpho.org/blog/morpho-effect-november-2025/) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Caps appropriately sized. Delays are driven by market utilization, not by cap design preventing exits. Rate model creates strong incentive for borrower repayment. V2's absolute and relative caps are enforced on allocation, not on withdrawal. Caps are transparent and on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Stressed during November 2025. Some Morpho markets temporarily reached 100% utilization. Steakhouse vaults experienced temporary illiquidity but access remained available via direct contract interaction. Conditions normalized within days. V2 adds forceDeallocate as additional exit mechanism. Rate model incentivized rapid normalization. | 3 | 3 | Non-Improvable | [P1] [Morpho Nov 2025](https://morpho.org/blog/morpho-effect-november-2025/) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure USDT lending with no lockups, vesting, or bridge dependencies. Exit depends on borrower repayment or liquidation timelines, not structural lockups. V2 adds forceDeallocate with penalty for illiquid adapters, providing an additional exit path. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary redemption through V2 ERC4626 vault always available. Users can redeem directly from the vault contract. No secondary market dependency for exit. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | High. USDT is the most liquid stablecoin by market cap (>$140B). Vault shares are 1:1 backed by vault assets. V2 vault's $11.4M TVL means even large proportional exits have low absolute market impact. | 9 | 9 | Non-Improvable (optimal) | [P3] Market data |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Moderate. Bank run causes temporary queues and rate spikes (4x at 100% utilization) but is unlikely to cause permanent depositor losses. Market isolation contains risk. November 2025 demonstrated this -- temporary queues but zero permanent losses for Steakhouse depositors. V2 adds forceDeallocate as additional permissionless exit mechanism (with penalty, protecting non-exiting depositors). | 3 | 3 | Non-Improvable | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Liquidity Subtotal: 35.0/45 (77.8%)**
- 6 questions scored 9 (sum = 54), 3 questions scored 3 (sum = 9)
- Raw sum = 63 out of max 81
- Weighted = (63/81) x 45 = 35.0

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | V2 vault shares trade at NAV (representing 1:1 USDT claim plus accrued yield). Only 39 holders and 161 transactions to date (vault is ~125 days old). No depeg history. The V2 vault token itself has no demonstrated stress resilience -- while the underlying V1 vault maintained stable value through November 2025 stress, the V2 token has not been tested. Per framework scoring principle: untested protocols should score Mid (3) on resilience questions. | 3 | 3 | Non-Improvable | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P3] [Vaults.fyi](https://app.vaults.fyi/opportunity/mainnet/0xbeef003C68896c7D2c3c60d363e8d71a49Ab2bf9) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Mostly low but with USDT-specific caveat. Vault lends USDT -- deposits and returns are USDT-denominated. No directional BTC/ETH exposure for lenders. Risk is borrower default/bad debt, not market direction. However, depositors are inherently exposed to USDT value: if USDT depegs (S&P rated Tether stability "weak"), depositors lose purchasing power even without bad debt. Scoring Mid to reflect this USDT denomination risk. | 3 | 3 | Non-Improvable | [P4] [S&P Tether Report](https://www.theblock.co/post/380562/tether-usdt-stability-score-weak-sp-reserves-cant-absorb-bitcoin-drop) |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Immutable Adaptive Curve IRM per market. Rates auto-increase with utilization (4x multiplier at 100% utilization). No governance manipulation possible. Rate curves become steep as utilization approaches critical levels. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. 86% LLTV on wstETH/WBTC markets provides 14% buffer; 77% LLTV on xAUT provides 23% buffer; 96.5% LLTV on sUSDS provides only 3.5% buffer (designed for low-volatility stablecoin collateral). Liquidation mechanism formally verified by Certora. Pre-liquidation mechanism available for additional safety. | 9 | 9 | Non-Improvable (optimal) | [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side only. Vault lenders benefit from liquidations (5% LIF goes to liquidators). Risk to lenders: insufficient or slow liquidation creating bad debt that gets socialized. Mitigated by economic incentives for liquidators. Primary collateral (wstETH at 86% LLTV) has ~14% buffer. sUSDS at 96.5% LLTV has thin 3.5% buffer but is a stablecoin product with low volatility. | 9 | 9 | Non-Improvable (optimal) | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 33.0/45 (73.3%)**
- 3 questions scored 9 (sum = 27), 2 questions scored 3 (sum = 6)
- Raw sum = 33 out of max 45
- Weighted = (33/45) x 45 = 33.0

---

### **Strategy Total: 233.8/270 (86.6%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 38.3 | 45 | 85.2% |
| Collateral | 45.0 | 45 | 100.0% |
| Infra Counterparty | 37.5 | 45 | 83.3% |
| Protocol Counterparty | 45.0 | 45 | 100.0% |
| Liquidity | 35.0 | 45 | 77.8% |
| Market | 33.0 | 45 | 73.3% |

| **Strategy Total** | **233.8** | **270** | **86.6%** |

---

### OPERATIONS (30% Weight) -- Score: 227.75/270 (84.4%)

**NOTE: Most Operations scores are identical to the existing Steakhouse V1 ratings (same curator, team, legal entity, documentation, treasury). O-G-02 differs because the V2 Owner DAO's voting power distribution could not be verified on-chain, unlike the V1 Guardian DAO which is documented as depositor-proportional.**

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid with strong checks. Morpho Blue: immutable. V2 vault changes: require Curator (timelocked) + Sentinel can revoke + Owner (Aragon DAO) sets curator/sentinel. V1 vault changes: require Owner multisig (5-of-8 Safe) + 7-day timelock + Guardian veto (Aragon DAO). Per-function timelocks in V2 provide granular control. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | The V2 Owner is an Aragon DAO proxy. Steakhouse describes V1 guardian DAOs as "composed of depositors" with proportional voting -- if this applies to the V2 Owner DAO, then voting power is distributed across depositors (currently 39 holders). However, the specific DAO configuration (quorum, proposal threshold, voting power distribution) could not be verified on-chain. The DAO has minimal on-chain activity. Without verifiable voting distribution, scored Mid (3). | 3 | 9 | **Source Missing** | [P0] [Etherscan Owner DAO](https://etherscan.io/address/0xFb345Ae28cCe3C55481190771e8c6D18c0f3D279) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. V2 per-function timelocks: 7 days for critical operations (adapter changes, cap increases, gate changes, timelock increases, abdicate). Sentinel can revoke pending timelocked actions. The abdicate function allows permanently disabling specific curator functions -- an irreversible safety measure. V1 also has 7-day timelock + Guardian veto. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner (Aragon DAO) can appoint new Curator. Withdrawals remain permissionless throughout via ERC4626 standard. V2's forceDeallocate provides additional permissionless exit path. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |

**Governance Subtotal: 56.25/67.5 (83.3%)**
- 3 questions scored 9 (sum = 27), 1 question scored 3 (sum = 3)
- Raw sum = 30 out of max 36
- Weighted = (30/36) x 67.5 = 56.25

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Steakhouse: adcv (co-founder), Sebastien Derivaux (co-founder, former MakerDAO Head of RWA). Morpho: Paul Frambot (CEO). All publicly identified with verifiable professional backgrounds. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse](https://www.steakhouse.financial/), [P1] [Morpho](https://morpho.org/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Morpho has a full team in Paris (ADDMO + Morpho Labs SAS, ~$73.6M raised). Steakhouse Financial is a separate entity with its own team. Multiple independent parties capable of vault operations. | 9 | 9 | Non-Improvable (optimal) | [P4] [Tracxn](https://tracxn.com/d/companies/morpho/__5iKpzjF_-EXELsu5bJ6cORHuQN7HD3ItPqKPexS2FVw) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Morpho: ADDMO (French nonprofit) + Morpho Labs SAS (France). Steakhouse: Carniciera Tropical Inc. (Panama) + Steakhouse Financial Ltd (Cayman Islands). All entities clearly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/), [P2] [Forum](https://forum.morpho.org/t/key-information-on-steakhouse-branded-vaults/1343) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known ongoing or past material enforcement actions against ADDMO, Morpho Labs, Steakhouse Financial, or Carniciera Tropical in any major jurisdiction. | 9 | 9 | Non-Improvable (optimal) | Public records |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Partial evidence. Monitoring bots + Chainalysis partnership confirmed. April 2025 incident demonstrates rapid response capability (4-minute rollback). However, no public 24/7 on-call SLA, formal incident runbook, or response SLA documentation found. Per v0.1-beta automation override requirement: the vault uses automated allocation (V2 allocators), but incident response documentation does not include procedures to halt automated capital flows during incidents. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. April 2025 vulnerability: alert received and frontend rolled back within 4 minutes. Active Discord community. Steakhouse publishes regular Kitchen newsletter updates. | 9 | 9 | Non-Improvable (optimal) | [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. a16z, Variant Fund, Pantera Capital, Coinbase Ventures (29 investors total, $73.6M raised). Partnerships publicly announced. | 9 | 9 | Non-Improvable (optimal) | [P4] [Tracxn](https://tracxn.com/d/companies/morpho/__5iKpzjF_-EXELsu5bJ6cORHuQN7HD3ItPqKPexS2FVw) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Steakhouse manages 19+ vaults across Ethereum and Base including both V1 and V2 variants. The V2 vault wraps V1, creating potential allocation priority conflicts. Limited hard constraints -- DDQ process and Credora rating provide qualitative controls, but no formal conflict-of-interest policy with quantitative rules published. | 3 | 9 | **Improvable** | [P2] [Forum](https://forum.morpho.org/t/key-information-on-steakhouse-branded-vaults/1343) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | No. Zero bad debt across all Steakhouse-curated vaults since inception. November 2025 stress: Steakhouse vaults specifically confirmed zero bad debt while other curators experienced losses. Clean track record. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/products/steakhouse-financial-products/morpho-vaults) |

**Team & Legal Subtotal: 57.5/67.5 (85.2%)**
- 7 questions scored 9 (sum = 63), 2 questions scored 3 (sum = 6)
- Raw sum = 69 out of max 81
- Weighted = (69/81) x 67.5 = 57.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Morpho Docs comprehensive and regularly updated including V2 documentation. Steakhouse publishes vault controls, risk management docs, and regular Kitchen newsletter updates. V2 source code publicly available on GitHub. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Docs](https://docs.morpho.org/), [P1] [GitHub V2](https://github.com/morpho-org/vault-v2), [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Detailed explanation of liquidation mechanics, bad debt scenarios, oracle risks, liquidity risks, and vault-specific loss conditions. V2 adds documentation of forceDeallocate penalty, caps system, and adapter loss realization. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Morpho docs maintain canonical address registry covering Morpho Blue, Vault V1/V2 factories, adapter factories, periphery contracts across all chains. V2 vault address clearly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. V2 introduces comprehensive per-function timelock documentation visible via GraphQL API. Owner, Curator, Sentinel, Allocator roles clearly specified with function-level access control. V2 contract source code verified on Etherscan with full function access matrix. Changes visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql), [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves. V2 vault adapter allocations visible via GraphQL API and Etherscan. V1 vault market allocations fully transparent. TVL, market allocations, utilization rates auditable on-chain at any time. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan V2 Vault](https://etherscan.io/address/0xbeef003C68896c7D2c3c60d363e8d71a49Ab2bf9), [P0] [Morpho V2 GraphQL API](https://api.morpho.org/graphql) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. All core V2 contracts verified on Etherscan: V2 vault (0xbeef003C), V1 adapter (0x233a0097), V1 vault (0xBEEF047a), Morpho Blue singleton (0xBBBB...), Owner DAO (0xFb345A), Sentinel/Revoker (0xc41F47). Full source code readable. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan V2 Vault](https://etherscan.io/address/0xbeef003C68896c7D2c3c60d363e8d71a49Ab2bf9), [P0] [Etherscan V1 Adapter](https://etherscan.io/address/0x233a0097F9D931A435Ba92ebb832a34c39135696), [P0] [Etherscan Sentinel](https://etherscan.io/address/0xc41F4709d0B9D637675aca1bF228732259d1606f) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions, all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated safety module or ring-fenced reserve for this vault or for Morpho generally. Bad debt in underlying V1 vault markets is socialized among lenders. Morpho DAO treasury exists (~$29.4M per DeFiLlama, mostly MORPHO tokens) but activation for loss coverage is entirely discretionary with no binding rules. | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/), [P3] [DeFiLlama Treasury](https://api.llama.fi/treasury/morpho) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Insufficient. Morpho DAO treasury is approximately $29.4M per DeFiLlama (Ethereum: $9.9M own tokens + $7.5K non-own; Base: $19.5M own tokens + $2 non-own). Treasury is ~99.97% MORPHO tokens (volatile native token) with only ~$7,516 in non-own-token liquid assets across both chains. Against protocol-wide TVL of ~$6.7B, the treasury represents ~0.44% including own tokens. Against this vault's ~$11.4M TVL specifically, treasury is not ring-fenced. Treasury composition is almost entirely illiquid native token. | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Morpho raised $73.6M total. Nonprofit structure reduces overhead. Curator fees growing ($13M annualized across ecosystem by end 2025, up 600% YoY). Steakhouse earns fees on other vaults. Runway comfortably above 24 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Resilient. During November 2025 stress, Steakhouse vaults experienced temporary outflows and brief illiquidity but zero bad debt and quick recovery. Protocol-wide TVL grew from $5B to $13B in 2025 despite stress episodes. V2 vault is newer but wraps the same V1 infrastructure. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue is immutable and runs perpetually without any team intervention. Permissionless withdrawals always available via V2 ERC4626 -> V1 adapter -> V1 vault -> Morpho Blue. V2 adds forceDeallocate as additional permissionless exit. Sentinel can revoke pending actions. No proprietary off-chain services required. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P1] [GitHub V2](https://github.com/morpho-org/vault-v2) |

**Financial Resilience Subtotal: 46.5/67.5 (68.9%)**
- 3 questions scored 9 (sum = 27), 1 question scored 3, 1 question scored 1
- Raw sum = 31 out of max 45
- Weighted = (31/45) x 67.5 = 46.5

---

### **Operations Total: 227.75/270 (84.4%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 56.25 | 67.5 | 83.3% |
| Team & Legal | 57.5 | 67.5 | 85.2% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 46.5 | 67.5 | 68.9% |
| **Operations Total** | **227.75** | **270** | **84.4%** |

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 87 | 99 | 158.2 | 180 | 87.9% |
| | Key Management (8 Q) | 54 | 72 | 135.0 | 180 | 75.0% |
| | **Security Subtotal** | | | **293.2** | **360** | **81.4%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 69 | 81 | 38.3 | 45 | 85.2% |
| | Collateral (4 Q) | 36 | 36 | 45.0 | 45 | 100.0% |
| | Infra Counterparty (8 Q) | 60 | 72 | 37.5 | 45 | 83.3% |
| | Protocol Counterparty (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity (9 Q) | 63 | 81 | 35.0 | 45 | 77.8% |
| | Market (5 Q) | 33 | 45 | 33.0 | 45 | 73.3% |
| | **Strategy Subtotal** | | | **233.8** | **270** | **86.6%** |
| **Operations** | Governance (4 Q) | 30 | 36 | 56.25 | 67.5 | 83.3% |
| | Team & Legal (9 Q) | 69 | 81 | 57.5 | 67.5 | 85.2% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 31 | 45 | 46.5 | 67.5 | 68.9% |
| | **Operations Subtotal** | | | **227.75** | **270** | **84.4%** |
| **TOTAL** | | | | **754.75** | **900** | **83.9%** |

---
