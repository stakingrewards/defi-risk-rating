# Morpho - Steakhouse ETH Vault Risk Rating

**Rating Date**: 2026-03-10
**Final Grade**: BB+
**Total Score**: 800.4/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v1.0-alpha

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 334.1/360 (92.8%)

#### Smart Contract Security (20% weight, 180 max points)

**NOTE: All Smart Contract Security scores are IDENTICAL to the Steakhouse USDC/USDT ratings and all other Morpho vault ratings. The ETH vault uses the same Morpho Blue protocol and MetaMorpho V1 factory contracts.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 25+ audits from Tier-0/1 firms including ChainSecurity, Spearbit/OpenZeppelin, Zellic, Certora, Blackthorn. Both Morpho Blue core and MetaMorpho framework extensively audited. Formal verification by Certora with mathematical proofs. The steakETH vault (0xBEEf050...) is a MetaMorpho V1 vault deployed via the audited MetaMorpho factory. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | December 2025: Certora (Tier-0), Spearbit (Tier-0 via Cantina), Blackthorn for Vaults V2 MarketV1AdapterV2. September 2025: ChainSecurity (Tier-0) for Vaults V2 core. Multiple Tier-0 auditors for most recent work. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable (~600 LOC). Every vault upgrade in last 12 months (Vaults V2 Sep-Dec 2025) was preceded by multiple audits from Tier-0 firms. The steakETH vault is a V1 MetaMorpho vault (non-upgradeable). | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 vulnerability patched immediately with OpenZeppelin. Certora formal verification provides mathematical proof of critical invariants. All V2 audit findings resolved before deployment with multiple re-reviews. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue core is immutable. MetaMorpho vault (0xBEEf050...) is a non-upgradeable ERC4626 contract deployed March 2024. Market changes require Owner 5-of-8 multisig + 7-day timelock (604,800s, confirmed via Morpho API) + Guardian (Aragon DAO) veto. Public upgrade policy documented. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql), [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls), [P0] [Etherscan](https://etherscan.io/address/0xBEEf050ecd6a16c4e7bfFbB52Ebba7846C4b8cD4) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss in Steakhouse vaults. April 2025 frontend vulnerability ($2.6M) was intercepted by white hat c0ffeebabe.eth and all funds returned within minutes. October 2024 oracle exploit ($230K) affected only PAXG/USDC market, not this vault. November 2025 Stream/Elixir contagion affected MEV Capital vault (3.6% bad debt), NOT Steakhouse vaults. February 2025 Bybit hack: Steakhouse proactively responded with risk mitigation but no vault losses occurred. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P2] [Bybit Incident Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho operates as ADDMO, a French nonprofit association. Steakhouse has 2+ year track record managing curated vaults. No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. 7-day timelock (604,800s) confirmed via Morpho GraphQL API as of March 2026, maintained above the 3-day protocol minimum. No changes to timelock duration in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql), [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active public bounty on Cantina with $2.5M max payout for critical vulnerabilities. 236 findings submitted since March 2024. Scope covers both V1 and V2 contracts plus web apps. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. Internal monitoring bots perform continuous invariant checks on each market after each transaction. Chainalysis partnership for transaction monitoring. April 2025 incident: alert received and frontend rolled back within 4 minutes. February 2025 Bybit hack: Steakhouse's automated systems detected price deviations and triggered proactive risk mitigation. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P2] [Bybit Incident Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. Morpho Blue prioritizes immutability over admin controls. Guardian can manually veto pending timelocked actions but cannot pause the protocol. Market-level isolation provides containment. | 3 | 3 | Non-Improvable | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Smart Contract Security Subtotal: 169.1/180 (93.9%)**
- 10 questions scored 9 (sum = 90), 1 question scored 3 (sum = 3)
- Raw sum = 93 out of max 99
- Weighted = (93/99) x 180 = 169.1

---

#### Key Management & Permissions (20% weight, 180 max points)

**NOTE: All Key Management scores are IDENTICAL to the Steakhouse USDC/USDT ratings. Same curator (2-of-5 Safe at 0x827e...), same Owner multisig (5-of-8 Safe at 0x0A0e...), different Guardian per vault (ETH vault: Aragon DAO at 0x4ef0...). Governance data verified via Safe API and Morpho GraphQL API (March 2026).**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Owner: 5-of-8 Safe multisig (0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD, verified via Safe API). Curator: 2-of-5 Safe multisig (0x827e86072B06674a077f592A531dcE4590aDeCdB, verified via Safe API). Guardian: Aragon DAO (0x4ef090B2c36b34974e244f3699DF998e2b9D4FE9, ERC1967 proxy to DAO implementation). All changes visible on-chain. No changes without multi-party approval and 7-day timelock (604,800s confirmed via Morpho GraphQL API). | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API - Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P0] [Safe API - Curator](https://api.safe.global/tx-service/eth/api/v1/safes/0x827e86072B06674a077f592A531dcE4590aDeCdB/), [P0] [Morpho GraphQL API](https://api.morpho.org/graphql), [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Vault contract is non-upgradeable. Moving user funds requires going through Morpho Blue immutable contract logic. Owner actions require 5-of-8 multisig + 7-day timelock (604,800s) + Guardian veto. Curator actions require 2-of-5 multisig + timelock. Permissionless redemption always available. Owner threshold (5) and total signers (8) exceeds minimum of >=3 AND >=5. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API - Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner multisig: 5-of-8 Safe (verified via Safe API, 8 distinct owner addresses on-chain). Steakhouse docs confirm "five persons must coordinate." One signer identified as pitmaster.eth (Steakhouse Financial: Deployer, 0x0D61C8b6CA9669A36F351De3AE335e9689dd9C5b). Guardian is an Aragon DAO (0x4ef090B2c36b34974e244f3699DF998e2b9D4FE9) controlled by depositors proportionally to their vault share. Guardian drill conducted Jan 2024 demonstrated functional veto mechanism. 5-of-8 exceeds 3-of-5 minimum for Low Risk. Note: while 8 distinct addresses are confirmed on-chain, only one signer (pitmaster.eth) is publicly identifiable by name; Steakhouse's statement of "five persons" provides partial independence assurance. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API - Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P0] [Etherscan - pitmaster.eth](https://etherscan.io/address/0x0D61C8b6CA9669A36F351De3AE335e9689dd9C5b), [P1] [Guardian Report](https://kitchen.steakhouse.financial/p/steakusdc-guardian-report), [P2] [Aragon DAO Guardian Upgrade](https://forum.morpho.org/t/steakhouse-metamorpho-vaults-are-upgrading-their-guardian-setups-to-fully-trustless/527) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking capability. No pause function on Morpho Blue (immutable). Guardian can only revoke pending timelocked actions. Withdrawals always permissionless via direct smart contract interaction. Rules publicly documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets held in non-custodial Morpho Blue contracts on Ethereum. Permissionless redemption via ERC4626. No off-chain custody component. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. Morpho is a nonprofit with no profit extraction from protocol operations. Vault funds are held in Morpho Blue markets, separate from any treasury or operational wallets. Performance fee accrued on-chain transparently. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain enforced whitelist of Morpho Blue markets only. Markets accept collateral including WBTC and cbBTC (confirmed via governance forum proposals). New market additions require Curator approval + 7-day timelock + Guardian veto. Supply caps per market enforced on-chain. "Dual engine" strategy may include RWA collateral markets when conditions allow. | 9 | 9 | Non-Improvable (optimal) | [P2] [Vault Whitelisting](https://forum.morpho.org/t/steakhouse-eth-and-steakhouse-btc-vault-whitelisting/514), [P2] [Adding WBTC](https://forum.morpho.org/t/adding-wbtc-as-collateral-on-steakhouse-steaketh/865), [P2] [Adding cbBTC](https://forum.morpho.org/t/adding-cbbtc-as-collateral-on-steakhouse-vaults/763) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Partial. Guardian drill conducted January 2024 successfully demonstrated veto mechanism but revealed low participation (only one depositor voted, though quorum was met). February 2025 Bybit incident demonstrated proactive response capability for ETH-related market stress. No comprehensive public key rotation playbook. No tabletop exercise for key compromise or signer loss documented in last 12 months. | 3 | 9 | **Improvable** | [P1] [Guardian Report](https://kitchen.steakhouse.financial/p/steakusdc-guardian-report), [P2] [Bybit Incident Response](https://forum.morpho.org/t/bybit-incident-response/1544) |

**Key Management Subtotal: 165.0/180 (91.7%)**
- 7 questions scored 9 (sum = 63), 1 question scored 3 (sum = 3)
- Raw sum = 66 out of max 72
- Weighted = (66/72) x 180 = 165.0

**Improvement Opportunities:**
- **S-KM-08** (+15.0 weighted points): Publish comprehensive incident response playbook with key rotation procedures and conduct full tabletop exercise within the last 12 months

---

### **Security Total: 334.1/360 (92.8%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 169.1 | 180 | 93.9% |
| Key Management | 165.0 | 180 | 91.7% |
| **Security Total** | **334.1** | **360** | **92.8%** |

---

### STRATEGY (30% Weight) -- Score: 227.3/270 (84.2%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from overcollateralized ETH lending against blue-chip crypto collateral (WBTC, cbBTC, and potentially other assets through the "dual engine" strategy including RWA collateral when conditions allow). 100% mandate-aligned. The vault's stated strategy is to "optimize yields by lending ETH against blue chip crypto and real-world asset (RWA) collateral markets." Yield sources documented on Morpho App with market-level breakdown. | 9 | 9 | Non-Improvable (optimal) | [P2] [Morpho App - steakETH](https://app.morpho.org/ethereum/vault/0xBEEf050ecd6a16c4e7bfFbB52Ebba7846C4b8cD4/steakhouse-eth), [P2] [Vault Whitelisting](https://forum.morpho.org/t/steakhouse-eth-and-steakhouse-btc-vault-whitelisting/514) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail shocks: (1) simultaneous collateral crash exceeding liquidation buffer (borrowers' WBTC/cbBTC collapses vs ETH); (2) oracle manipulation on immutable oracle; (3) wrapped-asset custodian failure of collateral tokens (cbBTC/WBTC); (4) extreme ETH volatility that outpaces liquidation mechanics. Because both the loan asset (ETH) and collateral (BTC-denominated) are volatile crypto assets, cross-asset price dislocations are possible but mitigated by conservative LLTVs. This represents rare tail-shock territory. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault simply lends ETH. No rehypothecation of depositor funds. Effective leverage: 1.0x. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. Liquidation risk applies to borrowers. Vault benefits from liquidation incentive fees. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss events for Steakhouse ETH vault or any Steakhouse vault since inception. During November 2025 Stream/Elixir contagion, Steakhouse vaults had ZERO bad debt. During February 2025 Bybit hack (400K ETH stolen), Steakhouse proactively responded and no losses occurred. The vault has approximately 23 months of operational history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/products/steakhouse-financial-products/morpho-vaults), [P2] [Bybit Incident Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| ST-PM-06 | Is a risk framework for vault curation documented? | Yes. Steakhouse publishes vault controls documentation with DDQ process (2 internal + 1 external reviewer). Credora A+ rating (best-in-class among Morpho curators, 5 of 6 vaults rated A+). On-chain caps per market. 7-day timelock + Guardian veto. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls), [P2] [Credora Ratings](https://forum.morpho.org/t/credora-network-risk-ratings-on-morpho/1652) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. Yield is primarily organic from ETH lending demand driven by leveraged traders and hedgers who borrow ETH against BTC or other collateral. No emissions or token incentives required for base yield. The steakETH token price reflects consistent yield accrual. Performance fee taken by curator. Coinbase ETH-backed loan program (launched late 2025) may drive additional demand. | 9 | 9 | Non-Improvable (optimal) | [P4] [Coinbase ETH Loans](https://www.theblock.co/post/379680/coinbase-eth-loans-morpho-up-to-1-million), [P3] [CoinGecko steakETH](https://www.coingecko.com/en/coins/steakhouse-eth-morpho-vault) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes. ETH is highly liquid. Slippage limited to rate model dynamics (4x rate at 100% utilization incentivizes rapid repayment). No slippage on ETH itself. The vault is ETH-denominated so exits are in ETH, the most liquid crypto asset after BTC. At $75.9M TVL (March 2026), the vault has grown but remains smaller than steakUSDC (~$152M). | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No reliance on invertible spreads for yield generation. Pure lending interest from overcollateralized borrower demand. Interest rates are set by immutable Adaptive Curve IRM based on utilization. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |

**Protocol Mechanics Subtotal: 45.0/45 (100.0%)**
- 8 applicable questions (ST-PM-04 = N/A), all scored 9
- Raw sum = 72 out of max 72
- Weighted = (72/72) x 45 = 45.0

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Borrowers post collateral to borrow ETH. Confirmed collateral types: WBTC (BitGo/BiT Global), cbBTC (Coinbase custody, NY DFS regulated). Additional collateral may include LSTs/LRTs and RWA tokens depending on the "dual engine" strategy and market conditions. WBTC and cbBTC are established, high-market-cap wrapped BTC assets. cbBTC is Tier-0 custody quality (Coinbase). WBTC carries BiT Global/Justin Sun governance controversy but remains the most liquid wrapped BTC. Credora A+ risk rating applies to the vault. LLTVs are set conservatively per market. | 9 | 9 | Non-Improvable (optimal) | [P2] [Vault Whitelisting](https://forum.morpho.org/t/steakhouse-eth-and-steakhouse-btc-vault-whitelisting/514), [P2] [Adding WBTC](https://forum.morpho.org/t/adding-wbtc-as-collateral-on-steakhouse-steaketh/865), [P2] [Adding cbBTC](https://forum.morpho.org/t/adding-cbbtc-as-collateral-on-steakhouse-vaults/763) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | cbBTC: No depeg >2% since September 2024 launch. WBTC: Briefly depegged during historical events (Alameda Nov 2022, Justin Sun controversy Aug 2024) but recovered within 24 hours each time. No collateral showed >2% depeg lasting >24h in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P3] Market data, [P1] [Coinbase cbBTC](https://www.coinbase.com/cbbtc) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- The vault lends ETH (WETH). The primary collateral types are wrapped BTC (WBTC, cbBTC), which are not staking-based. If LSTs/LRTs are accepted as collateral (e.g., wstETH), they represent a small portion of TVL and Lido uses 30+ diversified operators. However, the vault's loan asset itself is native ETH, not a staking derivative. | N/A | N/A | N/A | Vault mechanics |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | The vault's LOAN ASSET is ETH/WETH (WETH is a thin wrapper, excluded per criteria). However, the COLLATERAL posted by borrowers is predominantly wrapped BTC (WBTC and cbBTC). From the vault lender's perspective, the risk of wrapped collateral matters because if the wrapped collateral depegs, it becomes insufficient to cover the ETH loan, potentially creating bad debt that is socialized among lenders. Wrapped collateral as a share of total collateral backing the vault's loans likely exceeds 60%. | 1 | 9 | **Improvable** | [P2] [Adding WBTC](https://forum.morpho.org/t/adding-wbtc-as-collateral-on-steakhouse-steaketh/865), [P2] [Adding cbBTC](https://forum.morpho.org/t/adding-cbbtc-as-collateral-on-steakhouse-vaults/763) |

**Collateral Subtotal: 31.7/45 (70.4%)**
- ST-C-03 = N/A. 3 applicable questions: 2 scored 9 (sum = 18), 1 scored 1 (sum = 1)
- Raw sum = 19 out of max 27
- Weighted = (19/27) x 45 = 31.7

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | All Tier-0: Ethereum (chain), Chainlink (primary oracle provider). No bridges required. No CEX dependency for operations. Oracle providers documented per market. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | SINGLE ORACLE RISK. Each Morpho Blue market has one immutable oracle -- no fallback mechanism possible post-deployment. Chainlink is Tier-0 and battle-tested, but zero redundancy by design. For the ETH/BTC cross-pair markets, the oracle must correctly price BTC collateral relative to ETH, adding cross-asset oracle complexity. | 3 | 3 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Morpho Labs/ADDMO: No public SOC 2 Type II or ISO27001 certification found. Chainlink: Enterprise certifications in place. Coinbase (cbBTC custodian): NY DFS regulated, SOC 2 certified. No evidence of Morpho or Steakhouse holding such certifications. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Ethereum: No significant halts affecting operations. Morpho: April 2025 frontend vulnerability resolved in 4 minutes. November 2025 stress: protocol operated correctly (market isolation worked, liquidations processed, no system failures). February 2025 Bybit hack: Steakhouse published incident response, automated systems detected price deviations and triggered risk mitigation for ETH-related markets. No blocking of on-chain withdrawals. | 9 | 9 | Non-Improvable (optimal) | [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P2] [Bybit Incident Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain halts >30 minutes in the last 12+ months. Tier-0 chain reliability. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- The vault lends ETH. The primary collateral types are wrapped BTC (not staking-based). If the vault accepts LST collateral, this would become applicable, but currently the dominant collateral is wrapped BTC. Ethereum's validator set is relevant to the base chain but not to the collateral. | N/A | N/A | N/A | Vault mechanics |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- Same reasoning as ST-IC-06. The vault does not depend on validators for its collateral. Ethereum's base-layer validator diversity is captured under ST-IC-05. | N/A | N/A | N/A | Vault mechanics |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Permissionless on-chain redemption is always available via direct smart contract interaction (ERC4626 redeem/withdraw). No off-chain dependency for withdrawals. Frontend failure (as proven April 2025) does not block on-chain operations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Infrastructure Counterparty Subtotal: 35.0/45 (77.8%)**
- ST-IC-06, ST-IC-07 = N/A. 6 applicable questions: 4 scored 9 (sum = 36), 2 scored 3 (sum = 6)
- Raw sum = 42 out of max 54
- Weighted = (42/54) x 45 = 35.0

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All allocation to Morpho Blue markets only (Tier-0 protocol, 25+ audits, formally verified). No CEX exposure. No RWA platforms. Markets clearly listed with on-chain caps. | 9 | 9 | Non-Improvable (optimal) | [P2] [Morpho App - steakETH](https://app.morpho.org/ethereum/vault/0xBEEf050ecd6a16c4e7bfFbB52Ebba7846C4b8cD4/steakhouse-eth) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Yes. Steakhouse charges a performance fee on the vault. Fee documented in governance forum post and on-chain. Fee changes require timelock. No hidden rebates or undisclosed arrangements found. | 9 | 9 | Non-Improvable (optimal) | [P2] [Forum](https://forum.morpho.org/t/key-information-on-steakhouse-branded-vaults/1343) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. On-chain supply caps per market enforced by MetaMorpho contract. Allocator rebalances within caps. New market additions require Curator + 7-day timelock + Guardian veto. Cap changes subject to timelocks for increases. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Lending positions can be unwound as borrowers repay. Rate model (4x at 100% utilization) creates strong incentive for rapid borrower repayment. No discretionary approvals needed. ETH is highly liquid, facilitating repayment. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending -- no external validators, custodians, or asset managers involved in vault operations. Collateral is held in Morpho Blue smart contracts. Steakhouse Financial (curator) is disclosed. Underlying collateral custodians (Coinbase for cbBTC, BitGo for WBTC) are publicly known. | 9 | 9 | Non-Improvable (optimal) | Vault architecture |

**Protocol Counterparty Subtotal: 45.0/45 (100.0%)**
- 5 questions, all scored 9
- Raw sum = 45 out of max 45
- Weighted = (45/45) x 45 = 45.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain redemption via ERC4626 standard. No address-level blocking capability. No admin pause function. Withdrawal availability depends on market liquidity (not all funds may be available if 100% utilized). No admin approval required. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Moderate. Under normal conditions, substantial ETH available for withdrawal. During November 2025 stress, some Morpho markets temporarily reached 100% utilization. Rate spikes (4x at 100%) incentivize repayment within days, but instant 100% exit not guaranteed. The vault's $75.9M TVL (March 2026, Morpho API) has grown significantly but remains smaller than steakUSDC (~$152M). | 3 | 3 | Non-Improvable | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | Steakhouse ETH vault has been operational since March 2024 (~23 months). During the November 2025 stress period, Steakhouse vaults experienced temporary illiquidity but recovered with zero bad debt. During the February 2025 Bybit hack, Steakhouse proactively managed ETH market exposure. Over the full 12-month period, the vast majority (>95%) of withdrawals completed promptly. | 9 | 9 | Non-Improvable (optimal) | [P2] [Bybit Incident Response](https://forum.morpho.org/t/bybit-incident-response/1544), [P1] [Morpho Nov 2025](https://morpho.org/blog/morpho-effect-november-2025/) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Caps appropriately sized. During stress periods, delays were driven by market utilization (all funds lent out), not by cap design preventing exits. Rate model creates strong incentive for borrower repayment. Caps are transparent and on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Stress-tested during November 2025 and February 2025 (Bybit). Some Morpho markets temporarily reached high utilization. Steakhouse vaults experienced temporary illiquidity but access remained available via direct contract interaction. Conditions normalized within days. Rate model incentivized rapid normalization. | 3 | 3 | Non-Improvable | [P2] [Bybit Incident Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure ETH lending with no lockups, vesting, or bridge dependencies. Exit depends on borrower repayment or liquidation timelines, not structural lockups. No time-locks on user assets. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary redemption through ERC4626 vault always available. Secondary market (steakETH trading on DEXs) exists but is not required for exit. Users can always redeem directly from the vault contract. Note: CoinGecko data shows no 24h trading volume for steakETH, confirming the secondary market is thin, but primary redemption is the intended exit mechanism. | 9 | 9 | Non-Improvable (optimal) | [P3] [CoinGecko steakETH](https://www.coingecko.com/en/coins/steakhouse-eth-morpho-vault) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | Moderate. ETH is the most liquid crypto asset, and can absorb large trades with minimal impact. The vault's $75.9M TVL (March 2026) has grown significantly. The steakETH receipt token has minimal secondary market trading. Primary in-protocol redemption can absorb ~10% of TVL under normal conditions but is constrained by utilization during stress. | 3 | 3 | Non-Improvable | [P3] [CoinGecko steakETH](https://www.coingecko.com/en/coins/steakhouse-eth-morpho-vault), [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Moderate. Bank run causes temporary queues and rate spikes (4x at 100% utilization) but is unlikely to cause permanent depositor losses. Market isolation contains risk. November 2025 demonstrated this for Steakhouse vaults -- temporary queues but zero permanent losses. | 3 | 3 | Non-Improvable | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Liquidity Subtotal: 31.7/45 (70.4%)**
- 5 questions scored 9 (sum = 45), 4 questions scored 3 (sum = 12)
- Raw sum = 57 out of max 81
- Weighted = (57/81) x 45 = 31.7

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | steakETH trades at NAV (representing 1:1 ETH claim plus accrued yield). CoinGecko data shows the token tracks ETH value with accrued yield premium. No secondary market depeg history. During November 2025 and February 2025 stress events, vault share value remained stable in ETH terms -- users claiming ETH at full entitlement. However, secondary market trading volume is very thin (no 24h volume reported), limiting the ability to fully assess secondary market behavior under stress. | 3 | 3 | Non-Improvable | [P3] [CoinGecko steakETH](https://www.coingecko.com/en/coins/steakhouse-eth-morpho-vault) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Vault lends ETH -- deposits and returns are ETH-denominated. No directional BTC/ETH exposure for lenders within the vault's terms (deposits ETH, receives ETH back). The cross-asset risk is on the borrower side: if BTC collateral crashes relative to ETH, borrowers face liquidation. For lenders, risk is bad debt from insufficient liquidation, not directional ETH exposure. Scoring Low as the vault itself has no leverage or directional bet. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Immutable Adaptive Curve IRM per market. Rates auto-increase with utilization (4x multiplier at 100% utilization). No governance manipulation possible. Rate curves become steep as utilization approaches critical levels. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. Liquidation mechanism formally verified by Certora. Conservative LLTVs provide buffers before liquidation on all markets. Pre-liquidation mechanism available for additional safety. February 2025 Bybit hack caused significant ETH market stress (400K ETH stolen), providing a real-world stress test for ETH lending markets. | 9 | 9 | Non-Improvable (optimal) | [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/), [P2] [Bybit Incident Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side only. Vault lenders benefit from liquidations (liquidation incentive fee goes to liquidators, not protocol). Risk to lenders: insufficient or slow liquidation creating bad debt that gets socialized. This is mitigated by economic incentives for liquidators and conservative LLTV buffers. For ETH/BTC cross-pair markets, a sharp BTC crash relative to ETH could stress liquidation mechanics, but this is mitigated by the high correlation between BTC and ETH. | 9 | 9 | Non-Improvable (optimal) | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 39.0/45 (86.7%)**
- 4 questions scored 9 (sum = 36), 1 question scored 3 (sum = 3)
- Raw sum = 39 out of max 45
- Weighted = (39/45) x 45 = 39.0

---

### **Strategy Total: 227.3/270 (84.2%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 45.0 | 45 | 100.0% |
| Collateral | 31.7 | 45 | 70.4% |
| Infra Counterparty | 35.0 | 45 | 77.8% |
| Protocol Counterparty | 45.0 | 45 | 100.0% |
| Liquidity | 31.7 | 45 | 70.4% |
| Market | 39.0 | 45 | 86.7% |
| **Strategy Total** | **227.3** | **270** | **84.2%** |

---

### OPERATIONS (30% Weight) -- Score: 239.0/270 (88.5%)

**NOTE: All Operations scores are IDENTICAL to the Steakhouse USDC/USDT ratings. Same curator, same team, same legal entity, same governance model, same documentation, same treasury.**

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid with strong checks. Morpho Blue: immutable. Vault changes: require Owner 5-of-8 Safe multisig (0x0A0e...) + 7-day timelock (604,800s) + Guardian veto (Aragon DAO at 0x4ef0...). All verified on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API](https://api.safe.global/tx-service/eth/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P0] [Morpho GraphQL API](https://api.morpho.org/graphql), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | Guardian voting power is distributed proportionally across depositors. Owner multisig has fixed quorum of 5 signers. No single entity can unilaterally control the vault. | 9 | 9 | Non-Improvable (optimal) | [P2] [Guardian Upgrade](https://forum.morpho.org/t/steakhouse-metamorpho-vaults-are-upgrading-their-guardian-setups-to-fully-trustless/527) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. 7-day timelock (604,800s, confirmed via Morpho API) on all market changes (above 3-day protocol minimum). Aragon DAO Guardian (0x4ef0...) enables depositor veto of pending changes. Guardian drill tested January 2024. Veto powers clearly bounded. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql), [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner can appoint new Curator (subject to 7-day timelock). Withdrawals remain permissionless throughout via ERC4626 standard. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 4 questions, all scored 9
- Raw sum = 36 out of max 36
- Weighted = (36/36) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Steakhouse: adcv (co-founder), Sebastien Derivaux (co-founder, former MakerDAO Head of RWA). Morpho: Paul Frambot (CEO). All publicly identified with verifiable professional backgrounds. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse](https://www.steakhouse.financial/), [P1] [Morpho](https://morpho.org/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Morpho has a full team in Paris (ADDMO + Morpho Labs SAS, ~$73.6M raised). Steakhouse Financial is a separate entity with its own team. Multiple independent parties capable of vault operations. | 9 | 9 | Non-Improvable (optimal) | [P4] [Tracxn](https://tracxn.com/d/companies/morpho/__5iKpzjF_-EXELsu5bJ6cORHuQN7HD3ItPqKPexS2FVw) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Morpho: ADDMO (French nonprofit) + Morpho Labs SAS (France). Steakhouse: Carniciera Tropical Inc. (Panama) + Steakhouse Financial Ltd (Cayman Islands). All entities clearly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/), [P2] [Forum](https://forum.morpho.org/t/key-information-on-steakhouse-branded-vaults/1343) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known ongoing or past material enforcement actions against ADDMO, Morpho Labs, Steakhouse Financial, or Carniciera Tropical in any major jurisdiction. | 9 | 9 | Non-Improvable (optimal) | Public records |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Partial evidence. Monitoring bots + Chainalysis partnership confirmed. April 2025 incident demonstrates rapid response capability (4-minute rollback). February 2025 Bybit hack: Steakhouse published incident response demonstrating active monitoring and response. However, no public 24/7 on-call SLA, formal incident runbook, or response SLA documentation found. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P2] [Bybit Incident Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. April 2025 vulnerability: alert received and frontend rolled back within 4 minutes. February 2025 Bybit hack: Steakhouse published proactive incident response forum post. Active Discord community. Steakhouse publishes regular Kitchen newsletter updates. | 9 | 9 | Non-Improvable (optimal) | [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P2] [Bybit Incident Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. a16z, Variant Fund, Pantera Capital, Coinbase Ventures (29 investors total, $73.6M raised). Partnerships publicly announced. | 9 | 9 | Non-Improvable (optimal) | [P4] [Tracxn](https://tracxn.com/d/companies/morpho/__5iKpzjF_-EXELsu5bJ6cORHuQN7HD3ItPqKPexS2FVw) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Steakhouse manages 48 vaults across multiple chains. Potential for allocation decisions to favor some vaults over others. Limited hard constraints -- DDQ process and Credora rating provide qualitative controls, but no formal conflict-of-interest policy with quantitative rules published. | 3 | 9 | **Improvable** | [P2] [Forum](https://forum.morpho.org/t/key-information-on-steakhouse-branded-vaults/1343) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | No. Zero bad debt across all Steakhouse-curated vaults since inception. November 2025 stress: Steakhouse vaults specifically confirmed zero bad debt while other curators experienced losses. February 2025 Bybit: zero losses. Clean track record. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/products/steakhouse-financial-products/morpho-vaults) |

**Team & Legal Subtotal: 57.5/67.5 (85.2%)**
- 7 questions scored 9 (sum = 63), 2 questions scored 3 (sum = 6)
- Raw sum = 69 out of max 81
- Weighted = (69/81) x 67.5 = 57.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Morpho Docs comprehensive and regularly updated. Steakhouse publishes vault controls, risk management docs, and regular Kitchen newsletter updates. The "dual engine" strategy is described in vault documentation. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Docs](https://docs.morpho.org/), [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Detailed explanation of liquidation mechanics, bad debt scenarios, oracle risks, liquidity risks, and vault-specific loss conditions. Both Morpho and Steakhouse documentation cover these topics. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Morpho docs maintain canonical address registry. Vault address (0xBEEf050...) clearly identified on Morpho App. All Etherscan-verified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Comprehensive documentation of Owner, Curator, Guardian, Allocator roles. Timelock durations, capabilities, and constraints clearly specified. Changes visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves. All vault allocations visible on Morpho App and Etherscan. TVL, market allocations, utilization rates auditable on-chain at any time. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xBEEf050ecd6a16c4e7bfFbB52Ebba7846C4b8cD4), [P2] [Morpho App](https://app.morpho.org/ethereum/vault/0xBEEf050ecd6a16c4e7bfFbB52Ebba7846C4b8cD4/steakhouse-eth) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. All core contracts verified on Etherscan including vault contract, Morpho Blue singleton, factories, and periphery. Full source code readable. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Vault](https://etherscan.io/address/0xBEEf050ecd6a16c4e7bfFbB52Ebba7846C4b8cD4), [P0] [Etherscan Morpho](https://etherscan.io/address/0xbbbbbbbbbb9cc5e90e3b3af64bdaf62c37eeffcb) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions, all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated safety module or ring-fenced reserve for this vault or for Morpho generally. Bad debt is socialized among lenders within each Morpho Blue market. Morpho DAO treasury (~$21.9M) is entirely discretionary with no binding rules. | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/), [P3] [DeFiLlama Treasury](https://defillama.com/protocol/morpho) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Insufficient. Morpho DAO treasury is approximately $21.9M against protocol-wide TVL of ~$10B+ (0.22%). Treasury is not ring-fenced for this vault. Treasury composition likely includes significant MORPHO token holdings (volatile). | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama](https://defillama.com/protocol/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Morpho raised $73.6M total. Nonprofit structure reduces overhead. Steakhouse earns performance fees on vault assets. Runway comfortably above 24 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Resilient. During November 2025 stress, Steakhouse vaults experienced temporary outflows and brief illiquidity but zero bad debt and quick recovery. During February 2025 Bybit hack (which directly impacted ETH markets), Steakhouse proactively managed exposure and reported no losses. Protocol-wide TVL grew from $5B to $13B in 2025 despite stress episodes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/), [P2] [Bybit Incident Response](https://forum.morpho.org/t/bybit-incident-response/1544) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue is immutable and runs perpetually without any team intervention. Permissionless withdrawals always available. Guardian (depositors via Aragon DAO) can veto pending changes. No proprietary off-chain services required. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Financial Resilience Subtotal: 46.5/67.5 (68.9%)**
- 3 questions scored 9 (sum = 27), 1 question scored 3, 1 question scored 1
- Raw sum = 31 out of max 45
- Weighted = (31/45) x 67.5 = 46.5

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
| **Security** | Smart Contract Security | 169.1 | 180 | 169.1 |
| | Key Management | 165.0 | 180 | 180.0 |
| | **Security Subtotal** | **334.1** | **360** | **349.1** |
| **Strategy** | Protocol Mechanics | 45.0 | 45 | 45.0 |
| | Collateral | 31.7 | 45 | 45.0 |
| | Infra Counterparty | 35.0 | 45 | 40.0 |
| | Protocol Counterparty | 45.0 | 45 | 45.0 |
| | Liquidity | 31.7 | 45 | 31.7 |
| | Market | 39.0 | 45 | 39.0 |
| | **Strategy Subtotal** | **227.3** | **270** | **245.7** |
| **Operations** | Governance | 67.5 | 67.5 | 67.5 |
| | Team & Legal | 57.5 | 67.5 | 67.5 |
| | Documentation | 67.5 | 67.5 | 67.5 |
| | Financial Resilience | 46.5 | 67.5 | 67.5 |
| | **Operations Subtotal** | **239.0** | **270** | **270.0** |
| **TOTAL** | | **800.4** | **900** | **864.8** |

---
