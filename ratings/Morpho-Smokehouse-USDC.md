# Morpho - Smokehouse USDC Vault Risk Rating

**Rating Date**: 2026-03-26
**Final Grade**: BB-
**Total Score**: 751.5/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-beta

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 323.2/360 (89.8%)

#### Smart Contract Security (20% weight, 180 max points)

**NOTE: Smart Contract Security scores are based on the same Morpho Blue protocol infrastructure as the Steakhouse USDC rating. S-SC-10 is scored 3 (monitoring exists but cannot automatically trigger protective actions), consistent with Gauntlet vaults under the beta framework verification principle. Steakhouse USDC has not yet been re-rated under the beta framework.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 25+ audits from Tier-0/1 firms including ChainSecurity, Spearbit/OpenZeppelin, Zellic, Certora, Blackthorn. Both Morpho Blue core and MetaMorpho/Vaults V2 framework extensively audited. Formal verification by Certora. The Smokehouse USDC vault (0xBEeFFF...) is a MetaMorpho V1 vault deployed via the audited MetaMorpho factory. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | December 2025: Certora (Tier-0), Spearbit (Tier-0 via Cantina), Blackthorn for Vaults V2 MarketV1AdapterV2. September 2025: ChainSecurity (Tier-0) for Vaults V2 core. Multiple Tier-0 auditors for most recent work. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable (~600 LOC). Every vault upgrade in last 12 months (Vaults V2 Sep-Dec 2025) was preceded by multiple audits from Tier-0 firms. Smokehouse USDC is a V1 vault (non-upgradeable). | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 vulnerability patched immediately with OpenZeppelin. Certora formal verification provides mathematical proof of critical invariants. All V2 audit findings resolved before deployment. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue core is immutable. MetaMorpho V1 vault (0xBEeFFF...) is a non-upgradeable ERC4626 contract deployed ~December 2024. Market changes require Curator + 3-day timelock + Guardian veto. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vault V1 Docs](https://docs.morpho.org/learn/concepts/vault/), [P0] Etherscan verified contract |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss in Steakhouse/Smokehouse vaults. April 2025 frontend vulnerability ($2.6M) was intercepted by white hat c0ffeebabe.eth and all funds returned within minutes. October 2024 oracle exploit ($230K) affected only PAXG/USDC market, not this vault. November 2025 Stream/Elixir contagion affected MEV Capital vault (3.6% bad debt), NOT Steakhouse/Smokehouse vaults. Steakhouse confirmed zero bad debt across all mandates. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P4] [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1985620465650381093) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho operates as ADDMO, a French nonprofit association. Steakhouse Financial has a 2+ year track record. No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. 3-day timelock maintained on Smokehouse vault (the protocol minimum). No changes to timelock duration in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active public bounty on Cantina with $2.5M max payout for critical vulnerabilities. 236 findings submitted since March 2024. Scope covers both V1 and V2 contracts plus web apps. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Internal monitoring bots perform continuous invariant checks on each market after each transaction. Chainalysis partnership for transaction monitoring. April 2025 incident: alert received and frontend rolled back within 4 minutes. February 2025 Bybit hack: bbqUSDC reallocation within ~90 minutes. However, per the framework verification principle, monitoring exists but cannot automatically trigger protective actions — all responses require manual human intervention. The Public Allocator and automated allocation flows are not covered by any automated halt mechanism. Same limitation as all Morpho vaults (platform-level). | 3 | 9 | **Improvable** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P2] [Bybit Incident Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. Morpho Blue prioritizes immutability over admin controls. Guardian can manually veto pending timelocked actions but cannot pause the protocol. Market-level isolation provides containment. | 3 | 3 | Non-Improvable | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Smart Contract Security Subtotal: 158.2/180 (87.9%)**
- 9 questions scored 9 (sum = 81), 2 questions scored 3 (sum = 6)
- Raw sum = 87 out of max 99
- Weighted = (87/99) x 180 = 158.2

---

#### Key Management & Permissions (20% weight, 180 max points)

**NOTE: Key Management scores are IDENTICAL to the Steakhouse USDC rating. Smokehouse vaults are curated by the same entity (Carniciera Tropical Inc.) with the same Owner multisig (0x0A0e...8DD, 5-of-8 Safe), same Curator multisig (0x827e...CdB, 2-of-5 Safe), and the same non-custodial Morpho Blue architecture. The Guardian is a separate Aragon DAO per vault (Smokehouse: 0x94aa...A27D3). The only difference is the timelock duration (3 days vs 7 days), which is captured under O-G-03 in Governance, not in this section. All multisig configurations verified on-chain via Safe Transaction Service API on 2026-03-10.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Owner: Safe multisig 5-of-8 (0x0A0e...8DD, threshold=5, 8 signers, confirmed via Safe Transaction Service API). Same multisig as Steakhouse Prime vaults. Curator: Safe multisig 2-of-5 (0x827e...CdB, threshold=2, 5 signers -- all 5 are a subset of the 8 Owner signers). Guardian: Aragon DAO (0x94aa...A27D3, ERC1967Proxy). All changes visible on-chain. No changes without multi-party approval and 3-day timelock. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe Transaction Service API](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Vault contract is non-upgradeable. Moving user funds requires going through Morpho Blue immutable contract logic. Owner multisig requires 5-of-8 signatures (threshold >=3, total signers >=5) plus 3-day timelock (>=24h) for any market changes. Guardian (Aragon DAO) can veto pending timelocked actions. Permissionless redemption always available via ERC4626. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe Transaction Service API](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner multisig is 5-of-8 Safe (0x0A0e...8DD), confirmed on-chain via Safe Transaction Service API. 8 distinct EOA signers with threshold of 5 -- exceeds the >=3-of-5 minimum for Low Risk. Steakhouse docs state "five persons must coordinate" (P1 independence claim). All 5 Curator signers (0x827e...CdB, 2-of-5 Safe) are a subset of the 8 Owner signers. Guardian is an Aragon DAO (0x94aa...A27D3) controlled by depositors proportionally to their vault share. Guardian drill conducted Jan 2024 demonstrated functional veto mechanism (for steakUSDC; same architecture applies to bbqUSDC). No multisig changes in last 12 months that reduced independence. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe Transaction Service API - Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P0] [Safe Transaction Service API - Curator](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x827e86072B06674a077f592A531dcE4590aDeCdB/), [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls), [P2] [Guardian Report](https://kitchen.steakhouse.financial/p/steakusdc-guardian-report) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking capability. No pause function on Morpho Blue (immutable). Guardian can only revoke pending timelocked actions. Withdrawals always permissionless via direct smart contract interaction. Rules publicly documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets held in non-custodial Morpho Blue contracts on Ethereum. Permissionless redemption via ERC4626. No off-chain custody component. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. Morpho is a nonprofit with no profit extraction from protocol operations. Vault funds are held in Morpho Blue markets, separate from any treasury or operational wallets. Performance fee is 0% (confirmed via Morpho GraphQL API, March 2026). | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://blue-api.morpho.org/graphql), [P1] [Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain enforced whitelist of Morpho Blue markets only. The Smokehouse vault accesses a wider range of markets than Steakhouse Prime (exotic collateral: sUSDe, PT tokens, mF-ONE, syrupUSDC, plus blue-chip wstETH, cbBTC, WBTC). New market additions require Curator approval + 3-day timelock + Guardian veto. Supply caps per market enforced on-chain. Collateral additions announced in advance on governance forum. | 9 | 9 | Non-Improvable (optimal) | [P2] [Introducing Smokehouse](https://forum.morpho.org/t/introducing-the-smokehouse-product-line-bbqusdc-and-bbqdai/1182), [P2] [Adding mF-ONE](https://forum.morpho.org/t/bbqusdc-adding-mf-one-as-collateral/1846), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Partial. Guardian drill conducted January 2024 for steakUSDC demonstrated functional veto mechanism (same Aragon DAO architecture applies). However, low participation (one depositor voted). No comprehensive public key rotation playbook. No tabletop exercise for key compromise or signer loss documented in last 12 months. February 2025 Bybit hack response demonstrated rapid operational capability but no formal playbook published. | 3 | 9 | **Improvable** | [P2] [Guardian Report](https://kitchen.steakhouse.financial/p/steakusdc-guardian-report), [P2] [Bybit Response](https://forum.morpho.org/t/bybit-incident-response/1544) |

**Key Management Subtotal: 165.0/180 (91.7%)**
- 7 questions scored 9 (sum = 63), 1 question scored 3 (sum = 3)
- Raw sum = 66 out of max 72
- Weighted = (66/72) x 180 = 165.0

**Improvement Opportunities:**
- **S-KM-08** (+15.0 weighted points): Publish comprehensive incident response playbook with key rotation procedures and conduct full tabletop exercise within the last 12 months

---

### **Security Total: 323.2/360 (89.8%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 158.2 | 180 | 87.9% |
| Key Management | 165.0 | 180 | 91.7% |
| **Security Total** | **323.2** | **360** | **89.8%** |

---

### STRATEGY (30% Weight) -- Score: 189.3/270 (70.1%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield from overcollateralized USDC lending against diverse collateral (sUSDe, PT tokens, mF-ONE, syrupUSDC, wstETH, cbBTC, WBTC). Main sources: organic lending interest + MORPHO token rewards (~0.3-0.5% APR per Merkl campaign #172904, ~1.277K MORPHO daily). Mandate is "High Yield" with explicit risk disclosure for exotic collateral. Yield breakdown per Exponential: 5.5% base + 0.3% rewards = 5.85% 30d APY. Incentive portion is a minority (<10%) but present. | 9 | 9 | Non-Improvable (optimal) | [P3] [Exponential DeFi](https://exponential.fi/pools/morpho-usd-lending-smokehouse-ethereum/f17e1f50-4752-4741-a103-ecf8ad5dcc7b), [P3] [Merkl](https://app.merkl.xyz/opportunities/ethereum/MORPHOVAULT/0xBEeFFF209270748ddd194831b3fa287a5386f5bC) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss in severe but plausible single-shock events: (1) sUSDe depeg if Ethena encounters issues (Ethena's USDe has depegged multiple times historically); (2) mF-ONE credit default (Midas/Fasanara private credit, though Steakhouse claims safeguards); (3) PT token maturity risk at expiry; (4) syrupUSDC depeg if Maple borrowers default (Cayman injunction history); (5) rapid collateral price crash exceeding liquidation buffer. Exotic collateral makes these events more plausible than for Prime vault. | 3 | 3 | Non-Improvable | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P2] [Introducing Smokehouse](https://forum.morpho.org/t/introducing-the-smokehouse-product-line-bbqusdc-and-bbqdai/1182) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault simply lends USDC. No rehypothecation of depositor funds. Effective leverage: 1.0x. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. Liquidation risk applies to borrowers. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss events for Smokehouse/Steakhouse vaults. Steakhouse confirmed zero bad debt across ALL mandates (including Smokehouse/High Yield) during November 2025 Stream/Elixir contagion. Steakhouse explicitly stated "no exposure to xUSD/yUSD/deUSD/mHYPER/mMEV." The close-variant bad debt event (MEV Capital sdeUSD/USDC 3.6% on Morpho Blue) affected a different curator, not Steakhouse. | 9 | 9 | Non-Improvable (optimal) | [P4] [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1985620465650381093), [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/products/steakhouse-financial-products/morpho-vaults) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Steakhouse publishes comprehensive risk management framework with collateral rating system (AA through C), vault DDQ process (2 internal + 1 external reviewer), platform rating methodology, and final market rating criteria. Smokehouse/High Yield vaults explicitly positioned within this framework: "BB and B assets are considered High Yield." Credora A+ rating for 5 of 6 Steakhouse vaults. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Framework](https://www.steakhouse.financial/docs/risk-management), [P1] [Collateral Criteria](https://www.steakhouse.financial/docs/risk-management/collateral/layers-pillars-and-criteria), [P2] [Credora Ratings](https://forum.morpho.org/t/credora-network-risk-ratings-on-morpho/1652) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Primarily organic. Exponential data shows 5.5% base rate + 0.3% rewards = 5.85% total. MORPHO rewards comprise ~5% of total yield, well below 30% threshold. Base organic yield remains positive without incentives. Yield driven by borrower demand for leverage against exotic collateral. | 9 | 9 | Non-Improvable (optimal) | [P3] [Exponential DeFi](https://exponential.fi/pools/morpho-usd-lending-smokehouse-ethereum/f17e1f50-4752-4741-a103-ecf8ad5dcc7b) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | USDC itself is highly liquid. However, during November 2025, Steakhouse warned that "High Yield vault users are advised these may experience periods of illiquidity as market conditions resolve." Exotic collateral types mean borrowers may be slower to repay or harder to liquidate. Under conservative assumptions, slippage/penalties around 2-5% could materially compress returns during stress. | 3 | 3 | Non-Improvable | [P4] [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1985620465650381093), [P2] [Introducing Smokehouse](https://forum.morpho.org/t/introducing-the-smokehouse-product-line-bbqusdc-and-bbqdai/1182) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Partial dependency. Some collateral values depend on pegs: sUSDe/USDe peg (Ethena), syrupUSDC peg (Maple), mF-ONE NAV (private credit). However, vault is a USDC lender -- these peg risks affect borrower collateral quality, not the lender's direct position. Lending interest itself does not depend on spreads/pegs. Peg risk contributes indirectly to bad debt risk if collateral depegs and liquidations fail. Minority of yield at risk. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Yes. The vault uses automated allocation via the Public Allocator and Curator-appointed allocators. Supply caps per market limit maximum per-market exposure. However, no automatic kill-switch exists for abnormal conditions (oracle deviation, collateral depeg, utilization spikes). During the March 2026 Resolv exploit, the Public Allocator on other Morpho vaults auto-supplied $6.2M in USDC to broken markets for hours because anyone could invoke the function and no circuit breaker halted it. While Smokehouse markets were not directly affected, the same Public Allocator infrastructure applies. Halting requires manual curator intervention (setting caps to zero). | 3 | 9 | **Improvable** | [P1] [Morpho Public Allocator](https://docs.morpho.org/curate/concepts/public-allocator/), [P4] [Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |

**Protocol Mechanics Subtotal: 35.0/45 (77.8%)**
- 9 applicable questions (ST-PM-04 = N/A): 6 scored 9 (sum = 54), 3 scored 3 (sum = 9)
- Raw sum = 63 out of max 81
- Weighted = (63/81) x 45 = 35.0

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Mixed risk profile. Blue-chip: wstETH (Lido), cbBTC (Coinbase custody), WBTC (BitGo/BiT Global). Higher-risk/exotic: sUSDe (Ethena staked USDe, CCC SR tier), syrupUSDC (Maple, Cayman injunction history), mF-ONE (Midas/Fasanara tokenized private credit), various PT tokens (Pendle). Steakhouse rates these BB/B in their framework. Per Steakhouse: "BB and B assets are considered High Yield in higher risk products." Each market has explicit on-chain LTVs and supply caps. | 3 | 3 | Non-Improvable | [P1] [Collateral Criteria](https://www.steakhouse.financial/docs/risk-management/collateral/layers-pillars-and-criteria), [P2] [Introducing Smokehouse](https://forum.morpho.org/t/introducing-the-smokehouse-product-line-bbqusdc-and-bbqdai/1182) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | Mixed. Blue-chip (wstETH, cbBTC, WBTC): No >2% depeg lasting >24h in last 12 months. Ethena USDe/sUSDe: Has depegged multiple times historically, though recovered. Steakhouse confirmed no exposure to deUSD (which collapsed 98%). Bybit hack (Feb 2025): bbqUSDC automatically reallocated reducing Ethena exposure within 90 minutes. One or more exotic collaterals showed 2-10% deviation with recovery, scoring Mid. | 3 | 3 | Non-Improvable | [P2] [Bybit Response](https://forum.morpho.org/t/bybit-incident-response/1544), [P4] [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1985620465650381093) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Only wstETH has staking exposure. Lido uses 30+ diversified operators. Minor allocation relative to vault TVL. sUSDe is staked USDe (not validator-staked), so no slashing risk from sUSDe. | 9 | 9 | Non-Improvable (optimal) | Lido operator data |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | Moderate. Per the framework definition, "bridged or wrapped" means assets whose value depends on a bridge or wrapping contract maintaining a 1:1 backing relationship. Protocol receipt tokens (stETH, aTokens) are EXCLUDED. Applying strictly: cbBTC (Coinbase custody) and WBTC (BitGo/BiT Global) are bridged/wrapped BTC. sUSDe, syrupUSDC, mF-ONE, and PT tokens are protocol receipt tokens (excluded). wstETH is a receipt token (excluded). The wrapped BTC markets (cbBTC/WBTC) represent an estimated 20-60% of vault collateral exposure, as the vault's focus is exotic collateral. Caps and monitoring in place per market. | 3 | 9 | **Improvable** | [P3] [Morpho App](https://app.morpho.org/ethereum/vault/0xBEeFFF209270748ddd194831b3fa287a5386f5bC/smokehouse-usdc), [P2] [Introducing Smokehouse](https://forum.morpho.org/t/introducing-the-smokehouse-product-line-bbqusdc-and-bbqdai/1182) |

**Collateral Subtotal: 22.5/45 (50.0%)**
- 1 question scored 9 (sum = 9), 3 questions scored 3 (sum = 9)
- Raw sum = 18 out of max 36
- Weighted = (18/36) x 45 = 22.5

**Improvement Opportunities:**
- **ST-C-04** (+7.5 weighted points): Reduce bridged/wrapped BTC (cbBTC, WBTC) exposure below 20% of vault collateral

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | All Tier-0: Ethereum (chain), Chainlink (primary oracle provider). No bridges required. No CEX dependency for operations. Oracle providers clearly documented per market. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant are oracle and bridge setups, and can oracle values be corrected under abnormal conditions? | SINGLE ORACLE RISK. Each Morpho Blue market has one immutable oracle -- no fallback mechanism possible post-deployment. Chainlink is Tier-0 and battle-tested, but zero redundancy by design. Oracle failure would require deploying an entirely new market. | 3 | 3 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Morpho Labs/ADDMO: No public SOC 2 Type II or ISO27001 certification found. Chainlink: Enterprise certifications in place. Coinbase (cbBTC custodian): NY DFS regulated, SOC 2 certified. No evidence of Morpho or Steakhouse holding such certifications. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Ethereum: No significant halts affecting operations. Morpho: April 2025 frontend vulnerability resolved in 4 minutes. November 2025 stress: protocol operated correctly (market isolation worked, liquidations processed, no system failures). February 2025 Bybit hack: bbqUSDC automatically reallocated within 90 minutes. No blocking of on-chain withdrawals. | 9 | 9 | Non-Improvable (optimal) | [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P2] [Bybit Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain halts >30 minutes in the last 12+ months. Tier-0 chain reliability. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Only relevant for wstETH (minority allocation). Lido slashing events have been trivial and fully absorbed by Lido's coverage fund. No depositor impact. | 9 | 9 | Non-Improvable (optimal) | Lido slashing data |
| ST-IC-07 | Are validators diverse geographically and by operator? | Ethereum validator set is highly distributed. Lido (for wstETH) uses 30+ independent operators. No single operator >33% of relevant stake. | 9 | 9 | Non-Improvable (optimal) | Ethereum validator data |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Permissionless on-chain redemption is always available via direct smart contract interaction (ERC4626 redeem/withdraw). No off-chain dependency for withdrawals. Frontend failure (as proven April 2025) does not block on-chain operations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Infrastructure Counterparty Subtotal: 37.5/45 (83.3%)**
- 6 questions scored 9 (sum = 54), 2 questions scored 3 (sum = 6)
- Raw sum = 60 out of max 72
- Weighted = (60/72) x 45 = 37.5

**Improvement Opportunities:**
- **ST-IC-03** (+3.75 weighted points): Morpho Labs obtain and publish SOC 2 Type II or ISO27001 certification

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All allocation to Morpho Blue markets only (Tier-0 protocol, 25+ audits, formally verified). No CEX exposure. No RWA platforms directly. Markets clearly listed with on-chain caps. Collateral dependency chain extends to Ethena (sUSDe), Maple (syrupUSDC), Midas/Fasanara (mF-ONE), Pendle (PT tokens) -- but vault only interacts with Morpho Blue directly. | 9 | 9 | Non-Improvable (optimal) | [P3] [Morpho App](https://app.morpho.org/ethereum/vault/0xBEeFFF209270748ddd194831b3fa287a5386f5bC/smokehouse-usdc) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | MORPHO token rewards distributed via Merkl (campaign #172904, ~1.277K MORPHO daily). Vault performance fee is 0% (confirmed via Morpho GraphQL API). Fee changes require timelock. Merkl incentive arrangement is transparent. No undisclosed rebates found. However, the incentive from underlying collateral protocols (e.g., Maple incentivizing syrupUSDC adoption) creates potential conflict -- Steakhouse may be incentivized to allocate to markets where collateral issuers provide incentives, potentially not aligned with depositor safety. Terms only partially disclosed. | 3 | 9 | **Improvable** | [P0] [Morpho GraphQL API](https://blue-api.morpho.org/graphql), [P3] [Merkl](https://app.merkl.xyz/opportunities/ethereum/MORPHOVAULT/0xBEeFFF209270748ddd194831b3fa287a5386f5bC), [P2] [Forum](https://forum.morpho.org/t/key-information-on-steakhouse-branded-vaults/1343) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. On-chain supply caps per market enforced by MetaMorpho contract. Allocator rebalances within caps. New market additions require Curator + timelock + Guardian. Cap changes subject to timelocks for increases. mF-ONE initial borrow cap was $20M, "scaled conservatively in line with borrow demand." | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P2] [Adding mF-ONE](https://forum.morpho.org/t/bbqusdc-adding-mf-one-as-collateral/1846) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Lending positions can be unwound as borrowers repay. Rate model (4x at 100% utilization) creates incentive for rapid repayment. However, exotic collateral types mean borrowers may be slower to repay or harder to liquidate. November 2025 demonstrated temporary illiquidity in High Yield vaults. Steakhouse warned of "periods of illiquidity." mF-ONE positions depend on private credit maturity. | 3 | 3 | Non-Improvable | [P4] [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1985620465650381093) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending -- no external validators, custodians, or asset managers involved in vault operations. Steakhouse Financial (curator) is disclosed. Underlying collateral providers (Coinbase for cbBTC, Lido for wstETH, Ethena for sUSDe, Maple for syrupUSDC, Midas/Fasanara for mF-ONE) are publicly known and documented in governance forum posts. | 9 | 9 | Non-Improvable (optimal) | [P2] [Forum Posts](https://forum.morpho.org/t/introducing-the-smokehouse-product-line-bbqusdc-and-bbqdai/1182) |

**Protocol Counterparty Subtotal: 33.0/45 (73.3%)**
- 3 questions scored 9 (sum = 27), 2 questions scored 3 (sum = 6)
- Raw sum = 33 out of max 45
- Weighted = (33/45) x 45 = 33.0

**Improvement Opportunities:**
- **ST-PC-02** (+6.0 weighted points): Fully disclose all incentive arrangements with collateral issuers and publish conflict-of-interest analysis

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain redemption via ERC4626 standard. No address-level blocking capability. No admin pause function. Withdrawal availability depends on market liquidity (not all funds may be available if 100% utilized). No admin approval required. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Moderate. Under normal conditions, substantial USDC available for withdrawal. During November 2025 stress, Steakhouse explicitly warned High Yield vault users about "periods of illiquidity." Exotic collateral types mean borrower repayment may be slower. Rate spikes incentivize repayment but instant 100% exit not guaranteed. | 3 | 3 | Non-Improvable | [P4] [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1985620465650381093) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | November 2025: Steakhouse warned High Yield vaults "may experience periods of illiquidity as market conditions resolve." This is weaker than the Prime vault experience (where ~80% processed within 3 days). The explicit warning suggests meaningful delays occurred or were expected. Over the broader 12-month period, most withdrawals likely completed on time, but the November warning indicates between 80-95% completion within stated period. | 3 | 3 | Non-Improvable | [P4] [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1985620465650381093) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Caps appropriately sized and managed. Delays driven by market utilization (all funds lent out), not cap design. Rate model creates strong incentive for borrower repayment. No history of caps being manipulated to block exits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Stressed during November 2025. Steakhouse explicitly warned High Yield vault users about illiquidity. Exotic collateral markets have thinner secondary markets than blue-chip. During Bybit hack (Feb 2025), bbqUSDC reallocated but the stress was brief. Conditions normalized within days in both events. Scoring Mid given documented stress periods. | 3 | 3 | Non-Improvable | [P4] [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1985620465650381093), [P2] [Bybit Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure USDC lending with no lockups, vesting, or bridge dependencies. Exit depends on borrower repayment or liquidation timelines. mF-ONE positions have private credit maturity but initial borrow cap was limited to $20M with conservative scaling. Less than ~10% of assets at longer duration. | 9 | 9 | Non-Improvable (optimal) | [P2] [Adding mF-ONE](https://forum.morpho.org/t/bbqusdc-adding-mf-one-as-collateral/1846) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary redemption through ERC4626 vault always available. Secondary market (bbqUSDC trading on DEXs) exists but is not required for exit. Users can always redeem directly from the vault contract. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | USDC is the most liquid stablecoin. bbqUSDC is 1:1 backed by vault assets. With ~$59.7M TVL (per Morpho API, March 2026), depth supports ~3-10% of TVL without major impact. Smaller than steakUSDC but still adequate for normal exits. Exotic collateral markets have thinner secondary markets which affects unwind speed. | 3 | 3 | Non-Improvable | [P0] [Morpho GraphQL API](https://blue-api.morpho.org/graphql) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Moderate to elevated. Bank run causes temporary queues and rate spikes (4x at 100% utilization). Exotic collateral means liquidation mechanics may be less efficient. November 2025 demonstrated illiquidity warnings for High Yield vaults specifically. However, zero permanent losses confirmed. Market isolation contains risk. | 3 | 3 | Non-Improvable | [P4] [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1985620465650381093), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Liquidity Subtotal: 28.3/45 (62.9%)**
- 4 questions scored 9 (sum = 36), 5 questions scored 3 (sum = 15)
- Raw sum = 51 out of max 81
- Weighted = (51/81) x 45 = 28.3

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | bbqUSDC vault shares represent 1:1 USDC claim plus accrued yield. During November 2025 stress, Steakhouse confirmed zero bad debt across all vaults. The vault share value remained stable (no permanent loss). However, the warning about "periods of illiquidity" suggests temporary inability to redeem at NAV, even though NAV itself was maintained. During Bybit hack (Feb 2025), vault operated normally. Battle-tested through two stress events with maintained NAV. | 9 | 9 | Non-Improvable (optimal) | [P4] [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1985620465650381093), [P2] [Bybit Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Very low. Vault lends USDC -- deposits and returns are denominated in USDC. No directional BTC/ETH exposure for lenders. Risk is borrower default/bad debt from exotic collateral, not market direction. Dollar-denominated throughout. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Immutable Adaptive Curve IRM per market. Rates auto-increase with utilization (4x multiplier at 100% utilization). No governance manipulation possible. Rate curves become steep as utilization approaches critical levels. November 2025 stress demonstrated the IRM functioning as designed -- elevated rates incentivizing repayment. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. Steakhouse publishes risk framework with collateral rating system covering asset quality, platform risk, and market risk. Certora formally verified liquidation mechanics. Morpho Blue market parameters (LLTV, oracle) set per market based on collateral risk profile. However, stress modeling for exotic collateral (mF-ONE private credit default, correlated collateral failure) is less established than for blue-chip assets. | 3 | 9 | **Improvable** | [P1] [Risk Framework](https://www.steakhouse.financial/docs/risk-management), [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side only. Vault lenders benefit from liquidations. Risk to lenders: insufficient or slow liquidation creating bad debt that gets socialized. For exotic collateral, liquidation efficiency may be lower due to thinner secondary markets. mF-ONE liquidation depends on private credit market depth. | 3 | 3 | Non-Improvable | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 33.0/45 (73.3%)**
- 3 questions scored 9 (sum = 27), 2 questions scored 3 (sum = 6)
- Raw sum = 33 out of max 45
- Weighted = (33/45) x 45 = 33.0

---

### **Strategy Total: 189.3/270 (70.1%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 35.0 | 45 | 77.8% |
| Collateral | 22.5 | 45 | 50.0% |
| Infra Counterparty | 37.5 | 45 | 83.3% |
| Protocol Counterparty | 33.0 | 45 | 73.3% |
| Liquidity | 28.3 | 45 | 62.9% |
| Market | 33.0 | 45 | 73.3% |
| **Strategy Total** | **189.3** | **270** | **70.1%** |

---

### OPERATIONS (30% Weight) -- Score: 239.0/270 (88.5%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid with strong checks. Morpho Blue: immutable (no upgrades possible). Vault changes: require Owner multisig (5-of-8 Safe, 0x0A0e...8DD) + 3-day timelock (259200s) + Guardian veto (Aragon DAO, 0x94aa...A27D3). Curator (2-of-5 Safe, 0x827e...CdB) submits market changes subject to Owner timelock. Multiple independent layers prevent unilateral changes. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe Transaction Service API](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | Guardian voting power is distributed proportionally across depositors (Aragon DAO, 0x94aa...A27D3). Owner multisig is 5-of-8 Safe (0x0A0e...8DD, verified on-chain). No single entity can unilaterally control the vault. Same Owner multisig as Steakhouse Prime vaults. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe Transaction Service API](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | 3-day timelock (259200s, confirmed via Morpho GraphQL API) on vault changes (protocol minimum). Aragon DAO Guardian (0x94aa...A27D3) enables depositor veto. Timelock is SHORTER than Steakhouse Prime's 7-day timelock (604800s). The 3-day timelock meets the minimum 24-hour threshold for Low Risk scoring but is at the protocol floor. Veto powers clearly bounded. Steakhouse states this shorter timelock reflects the "more dynamic" nature of High Yield vault management where collateral changes occur more frequently. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://blue-api.morpho.org/graphql), [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner can appoint new Curator (subject to 3-day timelock). Withdrawals remain permissionless throughout via ERC4626 standard. Users can always exit regardless of curator changes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 4 questions, all scored 9
- Raw sum = 36 out of max 36
- Weighted = (36/36) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

**NOTE: Team & Legal scores are IDENTICAL to the Steakhouse USDC rating. Same curator entity, same Morpho protocol operator.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Steakhouse: adcv (co-founder, former M&A/investment banking), Sebastien Derivaux (co-founder, former MakerDAO Head of RWA). Morpho: Paul Frambot (CEO), Merlin Egalite, Mathis Gontier Delaunay. All publicly identified with verifiable professional backgrounds. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse](https://www.steakhouse.financial/), [P1] [Morpho](https://morpho.org/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Morpho has a full team in Paris (ADDMO + Morpho Labs SAS, ~$73.6M raised, 29 investors). Steakhouse Financial is a separate entity with its own team. Multiple independent parties capable of vault operations. | 9 | 9 | Non-Improvable (optimal) | [P4] [Tracxn](https://tracxn.com/d/companies/morpho/__5iKpzjF_-EXELsu5bJ6cORHuQN7HD3ItPqKPexS2FVw) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Morpho: ADDMO (French nonprofit, W751263773, 24 rue de Clichy, 75009 Paris) + Morpho Labs SAS (France, RCS 902 498 492). Steakhouse: Carniciera Tropical Inc. (Panama) + Steakhouse Financial Ltd (Cayman Islands). All entities clearly identified with registration numbers. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/), [P2] [Forum](https://forum.morpho.org/t/key-information-on-steakhouse-branded-vaults/1343) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known ongoing or past material enforcement actions against ADDMO, Morpho Labs, Steakhouse Financial, or Carniciera Tropical in any major jurisdiction. Morpho nonprofit structure reduces regulatory risk. | 9 | 9 | Non-Improvable (optimal) | Public records |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Partial evidence. Monitoring bots + Chainalysis partnership confirmed. April 2025 incident demonstrates rapid response capability (4-minute rollback). February 2025 Bybit hack: bbqUSDC automatic reallocation within 90 minutes. However, no public 24/7 on-call SLA, formal incident runbook, or response SLA documentation found for either Morpho or Steakhouse. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P2] [Bybit Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. April 2025 vulnerability: 4-minute rollback. November 2025 stress: Steakhouse publicly addressed concerns on Twitter within hours, providing clear guidance differentiating Prime (liquidity available) from High Yield (may experience illiquidity). February 2025 Bybit: governance forum post with detailed response. Active Substack updates (Kitchen newsletter). | 9 | 9 | Non-Improvable (optimal) | [P4] [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1985620465650381093), [P2] [Bybit Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Morpho: a16z, Variant Fund, Pantera Capital, Coinbase Ventures, Ribbit Capital (29 investors total, $73.6M raised). Roles and influence clearly described. Steakhouse: venture-backed entity with disclosed partnerships. | 9 | 9 | Non-Improvable (optimal) | [P4] [Tracxn](https://tracxn.com/d/companies/morpho/__5iKpzjF_-EXELsu5bJ6cORHuQN7HD3ItPqKPexS2FVw) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Steakhouse manages 48 vaults across Ethereum, Base, and other chains including both Prime and High Yield product lines. Potential for allocation decisions to favor some vaults over others. The Smokehouse vault specifically receives collateral that may be incentivized by issuers (e.g., Maple for syrupUSDC), creating potential conflict. Limited hard constraints -- DDQ process and Credora rating provide qualitative controls, but no formal conflict-of-interest policy with quantitative rules published. | 3 | 9 | **Improvable** | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/products/steakhouse-financial-products/morpho-vaults), [P2] [Forum](https://forum.morpho.org/t/key-information-on-steakhouse-branded-vaults/1343) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | No. Zero bad debt across all Steakhouse-curated vaults (including Smokehouse/High Yield) since inception. November 2025: Steakhouse vaults specifically confirmed zero bad debt while other curators (MEV Capital) experienced losses. Steakhouse is "the only major curator with no bad debt events." Clean 2+ year track record. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/products/steakhouse-financial-products/morpho-vaults), [P4] [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1985620465650381093) |

**Team & Legal Subtotal: 57.5/67.5 (85.2%)**
- 7 questions scored 9 (sum = 63), 2 questions scored 3 (sum = 6)
- Raw sum = 69 out of max 81
- Weighted = (69/81) x 67.5 = 57.5

**Improvement Opportunities:**
- **O-TL-05** (+5.0 weighted points): Publish documented 24/7 on-call procedures with defined escalation and response SLAs
- **O-TL-08** (+5.0 weighted points): Implement and publish formal conflict-of-interest policy with quantitative allocation rules

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Morpho Docs comprehensive and regularly updated. Steakhouse publishes vault controls documentation, risk management framework, collateral rating criteria, and regular Substack updates (Kitchen newsletter). Smokehouse/High Yield product line explicitly described with risk warnings. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Docs](https://docs.morpho.org/), [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls), [P1] [Steakhouse Products](https://www.steakhouse.financial/docs/products/steakhouse-financial-products/morpho-vaults) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Detailed explanation of liquidation mechanics, bad debt scenarios (socialized per market), oracle risks, liquidity risks. Steakhouse's collateral rating framework (AA through C) explicitly maps risk tiers. High Yield risk profile clearly documented: "use a wide range of collateral to allow vaults exposure to diverse types of borrowing activity." | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Collateral Criteria](https://www.steakhouse.financial/docs/risk-management/collateral/layers-pillars-and-criteria) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Morpho docs maintain canonical address registry. Vault address (0xBEeFFF...) clearly identified on Morpho App. All addresses Etherscan-verified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Comprehensive documentation of Owner, Curator, Guardian, Allocator roles. Timelock durations, capabilities, and constraints clearly specified. Steakhouse vault controls documentation covers all role configurations. Changes visible on-chain via Etherscan event logs. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves. All vault allocations visible on Morpho App and Etherscan. TVL, market allocations, utilization rates, and user positions all auditable on-chain at any time. No off-chain assets to track. | 9 | 9 | Non-Improvable (optimal) | [P3] [Morpho App](https://app.morpho.org/ethereum/vault/0xBEeFFF209270748ddd194831b3fa287a5386f5bC/smokehouse-usdc), [P0] Etherscan |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. All core contracts verified on Etherscan: vault (0xBEeFFF...), Morpho Blue singleton (0xBBBB...), factories, periphery, and bundler contracts. Full source code readable. | 9 | 9 | Non-Improvable (optimal) | [P0] Etherscan |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions, all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated safety module or ring-fenced reserve for this vault or for Morpho generally. Bad debt is socialized among lenders within each Morpho Blue market. Morpho DAO treasury exists (~$21.9M) but activation for loss coverage is entirely discretionary with no binding rules or criteria. | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/), [P3] [DeFiLlama Treasury](https://defillama.com/protocol/morpho) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Insufficient. Morpho DAO treasury is approximately $21.9M against protocol-wide TVL of ~$10B+ (0.22%). Even against this vault's ~$59.7M TVL (per Morpho API, March 2026), the treasury is not ring-fenced for this vault. Treasury composition likely includes significant MORPHO token holdings (volatile native token). No disclosed liquid reserve allocation strategy. | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama](https://defillama.com/protocol/morpho), [P0] [Morpho GraphQL API](https://blue-api.morpho.org/graphql) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Morpho raised $73.6M total (most recent: $50M Series C, Aug 2024 led by Ribbit Capital). Nonprofit structure reduces overhead. Steakhouse earns performance fees across its vault portfolio (note: this specific Smokehouse USDC vault has 0% fee, confirmed via Morpho GraphQL API), plus revenue from other 47 vaults ($1.45B total AUM, $0.5M+ annual recurring revenue). Runway comfortably above 24 months for both entities. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://blue-api.morpho.org/graphql), [P1] [Morpho Story](https://morpho.org/stories/steakhouse/), [P1] [Steakhouse Wrapped 2025](https://kitchen.steakhouse.financial/p/steakhouse-wrapped-2025) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Resilient. During November 2025 stress, Steakhouse vaults experienced temporary illiquidity warnings for High Yield vaults but zero bad debt. TVL has declined significantly from peak (currently ~$59.7M per Morpho API, March 2026), reflecting post-crisis outflows rather than losses. Protocol-wide Steakhouse TVL grew from ~$250M to $1.45B in 2025 despite stress episodes. Revenue model (curator fees) continued functioning. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://blue-api.morpho.org/graphql), [P1] [Steakhouse Wrapped 2025](https://kitchen.steakhouse.financial/p/steakhouse-wrapped-2025) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue is immutable and runs perpetually without any team intervention. Permissionless withdrawals always available via on-chain contract calls. Guardian (depositors via Aragon DAO) can veto pending changes. No proprietary off-chain services required for core operations. Vault contract is non-upgradeable. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Financial Resilience Subtotal: 46.5/67.5 (68.9%)**
- 3 questions scored 9 (sum = 27), 1 question scored 3, 1 question scored 1
- Raw sum = 31 out of max 45
- Weighted = (31/45) x 67.5 = 46.5

**Improvement Opportunities:**
- **O-FR-01** (+9.0 weighted points): Create dedicated safety module with clear, binding activation rules
- **O-FR-02** (+12.0 weighted points): Disclose detailed treasury composition, establish ring-fenced reserve target >= 5% of TVL in liquid assets

---

### **Operations Total: 239.0/270 (88.5%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 67.5 | 67.5 | 100.0% |
| Team & Legal | 57.5 | 67.5 | 85.2% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 46.5 | 67.5 | 68.9% |
| **Operations Total** | **239.0** | **270** | **88.5%** |

---

## Final Score Calculation

| Category | Subcategory | Current Points | Max Points | Potential Points |
|----------|-------------|----------------|------------|------------------|
| **Security** | Smart Contract Security | 158.2 | 180 | 169.1 |
| | Key Management | 165.0 | 180 | 180.0 |
| | **Security Subtotal** | **323.2** | **360** | **349.1** |
| **Strategy** | Protocol Mechanics | 35.0 | 45 | 38.3 |
| | Collateral | 22.5 | 45 | 30.0 |
| | Infra Counterparty | 37.5 | 45 | 41.3 |
| | Protocol Counterparty | 33.0 | 45 | 39.0 |
| | Liquidity | 28.3 | 45 | 28.3 |
| | Market | 33.0 | 45 | 39.0 |
| | **Strategy Subtotal** | **189.3** | **270** | **215.9** |
| **Operations** | Governance | 67.5 | 67.5 | 67.5 |
| | Team & Legal | 57.5 | 67.5 | 67.5 |
| | Documentation | 67.5 | 67.5 | 67.5 |
| | Financial Resilience | 46.5 | 67.5 | 67.5 |
| | **Operations Subtotal** | **239.0** | **270** | **270.0** |
| **TOTAL** | | **751.5** | **900** | **835.0** |

---

