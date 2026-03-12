# Morpho - Steakhouse USDT Vault Risk Rating

**Rating Date**: 2026-03-10 (refreshed from 2026-02-15)
**Final Grade**: BB+
**Total Score**: 805.9/900 points

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 334.1/360 (92.8%)

#### Smart Contract Security (20% weight, 180 max points)

**NOTE: All Smart Contract Security scores are IDENTICAL to the Steakhouse USDC rating and all other Morpho vault ratings. The USDT vault uses the same Morpho Blue protocol and MetaMorpho V1 factory contracts.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 25+ audits from Tier-0/1 firms including ChainSecurity, Spearbit/OpenZeppelin, Zellic, Certora, Blackthorn. Both Morpho Blue core and MetaMorpho framework extensively audited. Formal verification by Certora with mathematical proofs. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | December 2025: Certora (Tier-0), Spearbit (Tier-0 via Cantina), Blackthorn for Vaults V2 MarketV1AdapterV2. September 2025: ChainSecurity (Tier-0) for Vaults V2 core. Multiple Tier-0 auditors for most recent work. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable (~600 LOC). Every vault upgrade in last 12 months (Vaults V2 Sep-Dec 2025) was preceded by multiple audits from Tier-0 firms. The steakUSDT vault is a V1 MetaMorpho vault (non-upgradeable). | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 vulnerability patched immediately with OpenZeppelin. Certora formal verification provides mathematical proof of critical invariants. All V2 audit findings resolved before deployment with multiple re-reviews. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue core is immutable. MetaMorpho vault (0xbEef047...) is a non-upgradeable ERC4626 contract. Market changes require 7-day timelock (604,800s confirmed via Morpho GraphQL API) + Guardian (Aragon DAO) veto. Public upgrade policy documented. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql), [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls), [P0] [Etherscan](https://etherscan.io/address/0xbEef047a543E45807105E51A8BBEFCc5950fcfBa) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss in Steakhouse vaults. April 2025 frontend vulnerability ($2.6M) was intercepted by white hat c0ffeebabe.eth and all funds returned within minutes. October 2024 oracle exploit ($230K) affected only PAXG/USDC market, not this vault. November 2025 Stream/Elixir contagion affected MEV Capital vault (3.6% bad debt), NOT Steakhouse vaults. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P4] [Cointelegraph](https://cointelegraph.com/news/white-hat-intercepts-2-million-morpho-blue-hack) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho operates as ADDMO, a French nonprofit association. Steakhouse has 2+ year track record managing curated vaults. No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. 7-day timelock (604,800s confirmed via Morpho GraphQL API on 2026-03-10) maintained on Steakhouse vaults (above the 3-day protocol minimum). No changes to timelock duration in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql), [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active public bounty on Cantina with $2.5M max payout for critical vulnerabilities. 236 findings submitted since March 2024. Scope covers both V1 and V2 contracts plus web apps. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. Internal monitoring bots perform continuous invariant checks on each market after each transaction. Chainalysis partnership for transaction monitoring. April 2025 incident: alert received and frontend rolled back within 4 minutes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. Morpho Blue prioritizes immutability over admin controls. Guardian can manually veto pending timelocked actions but cannot pause the protocol. Market-level isolation provides containment. | 3 | 3 | Non-Improvable | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Smart Contract Security Subtotal: 169.1/180 (93.9%)**
- 10 questions scored 9 (sum = 90), 1 question scored 3 (sum = 3)
- Raw sum = 93 out of max 99
- Weighted = (93/99) x 180 = 169.1

---

#### Key Management & Permissions (20% weight, 180 max points)

**NOTE: All Key Management scores are IDENTICAL to the Steakhouse USDC rating. Same curator (2-of-5 Safe), same Owner (5-of-8 Safe at 0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD), same 7-day timelock (604,800s). Guardian is vault-specific (Aragon DAO at 0xaeC761545Fd135db6d04D27C92BCB3951668c67F for this vault). Governance data confirmed via Morpho GraphQL API and Safe Transaction Service API on 2026-03-10.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Owner: Safe multisig 5-of-8 (0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD), confirmed via Safe Transaction Service API. Curator: Safe multisig 2-of-5 (0x827e86072B06674a077f592A531dcE4590aDeCdB), confirmed via Safe Transaction Service API. Guardian: Aragon DAO (ERC1967Proxy at 0xaeC761545Fd135db6d04D27C92BCB3951668c67F), controlled by depositors proportionally to vault share. 7-day timelock (604,800s) confirmed via Morpho GraphQL API. All changes visible on-chain. No changes without multi-party approval and 7-day timelock. Note: All 5 Curator signers are a subset of the 8 Owner signers, which means the Curator team is fully contained within the Owner team. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API - Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P0] [Safe API - Curator](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x827e86072B06674a077f592A531dcE4590aDeCdB/), [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Vault contract is non-upgradeable. Moving user funds requires going through Morpho Blue immutable contract logic. Owner changes require 5-of-8 Safe multisig + 7-day timelock. Curator market parameter changes require 2-of-5 Safe multisig + 7-day timelock + Guardian veto. Permissionless redemption always available via ERC4626. Owner threshold (5) and signer count (8) exceeds the 3-of-5 minimum for Low Risk. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API - Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner multisig is 5-of-8 Safe (confirmed on-chain). 8 distinct signer addresses, threshold of 5. One signer identified on Etherscan as "Steakhouse Financial: Deployer" (0x0D61C8b6CA9669A36F351De3AE335e9689dd9C5b). The remaining 7 signer identities are not publicly disclosed by name, though they are distinct on-chain addresses. Curator multisig is 2-of-5 Safe; all 5 Curator signers are a subset of the 8 Owner signers. Guardian is an Aragon DAO controlled by depositors proportionally to their vault share. Guardian drill conducted Jan 2024 demonstrated functional veto mechanism. Owner 5-of-8 exceeds 3-of-5 minimum for Low Risk. Signer independence: while individual names are not publicly mapped, the 8 distinct addresses and Steakhouse's public team (adcv, Sebastien Derivaux, and additional team members) provide partial independence evidence. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API - Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P0] [Safe API - Curator](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x827e86072B06674a077f592A531dcE4590aDeCdB/), [P1] [Guardian Report](https://kitchen.steakhouse.financial/p/steakusdc-guardian-report), [P2] [Aragon DAO Guardian Upgrade](https://forum.morpho.org/t/steakhouse-metamorpho-vaults-are-upgrading-their-guardian-setups-to-fully-trustless/527) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking capability. No pause function on Morpho Blue (immutable). Guardian can only revoke pending timelocked actions. Withdrawals always permissionless via direct smart contract interaction. Rules publicly documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets held in non-custodial Morpho Blue contracts on Ethereum. Permissionless redemption via ERC4626. No off-chain custody component. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. Morpho is a nonprofit with no profit extraction from protocol operations. Vault funds are held in Morpho Blue markets, separate from any treasury or operational wallets. Performance fee accrued on-chain transparently. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain enforced whitelist of Morpho Blue markets only. Current markets: cbBTC/USDT, WBTC/USDT, wstETH/USDT, and xAUT/USDT (77% LLTV). New market additions require Curator (2-of-5 Safe multisig) approval + 7-day timelock + Guardian (Aragon DAO) veto. Supply caps per market enforced on-chain. | 9 | 9 | Non-Improvable (optimal) | [P2] [Morpho App - steakUSDT](https://app.morpho.org/ethereum/vault/0xbEef047a543E45807105E51A8BBEFCc5950fcfBa/steakhouse-usdt), [P2] [xAUT Collateral Proposal](https://forum.morpho.org/t/steakusdt-adding-xaut-as-collateral-on-steakusdt/1718) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Partial. Guardian drill conducted January 2024 successfully demonstrated veto mechanism but revealed low participation (only one depositor voted, though quorum was met). No comprehensive public key rotation playbook. No tabletop exercise for key compromise or signer loss documented in last 12 months. | 3 | 9 | **Improvable** | [P1] [Guardian Report](https://kitchen.steakhouse.financial/p/steakusdc-guardian-report) |

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

### STRATEGY (30% Weight) -- Score: 232.8/270 (86.2%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from overcollateralized USDT lending against blue-chip crypto collateral (cbBTC, WBTC, wstETH) and tokenized gold (xAUT). 100% mandate-aligned. Yield sources documented on Morpho App with market-level breakdown. The vault lends USDT rather than USDC but the yield mechanics are identical. | 9 | 9 | Non-Improvable (optimal) | [P2] [Morpho App - steakUSDT](https://app.morpho.org/ethereum/vault/0xbEef047a543E45807105E51A8BBEFCc5950fcfBa/steakhouse-usdt), [P2] [Vault Whitelisting](https://forum.morpho.org/t/steakhouse-financial-wusdm-pyusd-and-usdt-metamorpho-vault-whitelisting/452) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail shocks PLUS USDT-specific risk: (1) simultaneous BTC/ETH crash exceeding liquidation buffer (86% LLTV provides ~14% buffer for BTC markets); (2) oracle manipulation on immutable oracle; (3) wrapped-asset custodian failure (cbBTC/WBTC); (4) xAUT depeg or gold price crash (77% LLTV, ~23% buffer); AND critically (5) USDT depeg -- S&P rated Tether stability "weak" (5/5) in November 2025, with 24% of reserves in riskier assets and Bitcoin exposure exceeding the reserve buffer. A USDT depeg would directly impair depositor value regardless of lending performance. This additional stablecoin issuer risk is a severe but plausible single-shock event. | 3 | 3 | Non-Improvable | [P4] [S&P Tether Downgrade](https://www.theblock.co/post/380562/tether-usdt-stability-score-weak-sp-reserves-cant-absorb-bitcoin-drop), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault simply lends USDT. No rehypothecation of depositor funds. Effective leverage: 1.0x. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. Liquidation risk applies to borrowers. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss events for Steakhouse USDT vault or any Steakhouse vault since inception. During November 2025 Stream/Elixir contagion, Steakhouse vaults had ZERO bad debt. The close variant (steakUSDC) also had zero bad debt. The vault has approximately 10 months of operational history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/products/steakhouse-financial-products/morpho-vaults), [P4] [CryptoRank](https://cryptorank.io/news/feed/275ce-risk-curators-took-off-in-2025-but-led-to-recent-defi-lending-vault-troubles) |
| ST-PM-06 | Is a risk framework for vault curation documented? | Yes. Steakhouse publishes vault controls documentation with DDQ process (2 internal + 1 external reviewer). Credora A+ rating (best-in-class among Morpho curators, 5 of 6 vaults rated A+). On-chain caps per market. 7-day timelock + Guardian veto. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls), [P2] [Credora Ratings](https://forum.morpho.org/t/credora-network-risk-ratings-on-morpho/1652) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. Yield is primarily organic from USDT lending demand driven by BTC/ETH leveraged borrowers. No emissions or token incentives required for base yield. steakUSDT token price of ~$1.10-1.11 indicates consistent yield accrual. Performance fee taken by curator. | 9 | 9 | Non-Improvable (optimal) | [P3] [CoinGecko steakUSDT](https://www.coingecko.com/en/coins/steakhouse-usdt-morpho-vault) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes. USDT is highly liquid (>$180B market cap). During November 2025 stress, Steakhouse vault withdrawals processed within days. Slippage limited to rate model dynamics (4x rate at 100% utilization incentivizes rapid repayment). No slippage on USDT itself under normal conditions. | 9 | 9 | Non-Improvable (optimal) | [P4] [CryptoRank](https://cryptorank.io/news/feed/275ce-risk-curators-took-off-in-2025-but-led-to-recent-defi-lending-vault-troubles) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No reliance on invertible spreads for yield generation. Pure lending interest from overcollateralized borrower demand. Interest rates are set by immutable Adaptive Curve IRM based on utilization. However, the underlying asset (USDT) itself is a peg -- if USDT depegs, depositor value is impaired. This is an asset-level risk, not a strategy-level spread dependency. Scoring Low as the yield mechanism does not depend on spread maintenance. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |

**Protocol Mechanics Subtotal: 41.3/45 (91.7%)**
- 8 applicable questions (ST-PM-04 = N/A): 7 scored 9 (sum = 63), 1 scored 3 (sum = 3)
- Raw sum = 66 out of max 72
- Weighted = (66/72) x 45 = 41.25, rounded to 41.3

**NOTE on calculation precision:** (66/72) x 45 = 41.25. For consistency with the rounding used across the framework, this is reported as 41.3.

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Blue-chip collateral plus tokenized gold: cbBTC (Coinbase custody, NY DFS regulated), WBTC (BitGo/BiT Global), wstETH (Lido), and xAUT (Tether Gold, tokenized physical gold at 77% LLTV). The first three are the same blue-chip assets used in the USDC vault. xAUT adds gold exposure -- a $837M market cap asset backed by LBMA-standard gold in Swiss vaults, issued by Tether. While gold is a traditional safe haven, xAUT carries Tether issuer risk and is a novel DeFi collateral type. Conservative 77% LLTV applied to xAUT. Credora A+ risk rating applies to the vault. | 9 | 9 | Non-Improvable (optimal) | [P2] [xAUT Collateral Proposal](https://forum.morpho.org/t/steakusdt-adding-xaut-as-collateral-on-steakusdt/1718), [P2] [cbBTC Addition](https://forum.morpho.org/t/adding-cbbtc-as-collateral-on-steakhouse-vaults/763) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | cbBTC: No depeg >2% in its history since September 2024 launch. WBTC: Briefly depegged during historical events but recovered within 24 hours each time. wstETH: Stable tracking of underlying stETH value. xAUT: Tracks gold price closely, no significant depeg >2% lasting >24h in last 12 months. No collateral showed >2% depeg lasting >24h in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P3] Market data, [P1] [Coinbase cbBTC](https://www.coinbase.com/cbbtc) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Only wstETH has staking exposure (small portion of vault TVL). Lido uses 30+ diversified operators across multiple jurisdictions. Lido slashing insurance/coverage fund absorbs minor events. Risk is immaterial to vault given allocation size. | 9 | 9 | Non-Improvable (optimal) | Lido operator data, Vault allocation data |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | HIGH RISK: Approximately 98%+ of vault TVL is in wrapped assets (primarily cbBTC and WBTC markets, plus xAUT which is a Tether-issued wrapped gold token). cbBTC is custodied by Coinbase (NY DFS regulated). WBTC involves BiT Global/Justin Sun controversy. xAUT adds Tether custody dependency for gold backing. Exceeds 60% threshold significantly. | 1 | 9 | **Improvable** | [P2] [Morpho App - steakUSDT](https://app.morpho.org/ethereum/vault/0xbEef047a543E45807105E51A8BBEFCc5950fcfBa/steakhouse-usdt) |

**Collateral Subtotal: 35.0/45 (77.8%)**
- 3 questions scored 9 (sum = 27), 1 question scored 1
- Raw sum = 28 out of max 36
- Weighted = (28/36) x 45 = 35.0

**Improvement Opportunities:**
- **ST-C-04** (+10.0 weighted points): Diversify collateral exposure below 60% wrapped assets by adding native ETH or other non-wrapped markets

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | All Tier-0: Ethereum (chain), Chainlink (primary oracle provider). No bridges required. No CEX dependency for operations. Oracle providers documented per market. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | SINGLE ORACLE RISK. Each Morpho Blue market has one immutable oracle -- no fallback mechanism possible post-deployment. Chainlink is Tier-0 and battle-tested, but zero redundancy by design. The xAUT/USDT market requires a gold price oracle feed which adds oracle surface area. | 3 | 3 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Morpho Labs/ADDMO: No public SOC 2 Type II or ISO27001 certification found. Chainlink: Enterprise certifications in place. Coinbase (cbBTC custodian): NY DFS regulated, SOC 2 certified. No evidence of Morpho or Steakhouse holding such certifications. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Ethereum: No significant halts affecting operations. Morpho: April 2025 frontend vulnerability resolved in 4 minutes. November 2025 stress: protocol operated correctly (market isolation worked, liquidations processed, no system failures). steakUSDT vault experienced zero bad debt. | 9 | 9 | Non-Improvable (optimal) | [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain halts >30 minutes in the last 12+ months. Tier-0 chain reliability. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Only relevant for wstETH (small portion of TVL). Lido slashing events have been trivial and fully absorbed by Lido's coverage fund. No depositor impact. | 9 | 9 | Non-Improvable (optimal) | Lido slashing data |
| ST-IC-07 | Are validators diverse geographically and by operator? | Ethereum validator set is highly distributed across geographies and operators. Lido (for wstETH) uses 30+ independent operators. No single operator >33% of relevant stake. | 9 | 9 | Non-Improvable (optimal) | Ethereum validator data |
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
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All allocation to Morpho Blue markets only (Tier-0 protocol, 25+ audits, formally verified). No CEX exposure. No RWA platforms. Markets clearly listed with on-chain caps. | 9 | 9 | Non-Improvable (optimal) | [P2] [Morpho App - steakUSDT](https://app.morpho.org/ethereum/vault/0xbEef047a543E45807105E51A8BBEFCc5950fcfBa/steakhouse-usdt) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Yes. Steakhouse charges a performance fee on the vault. Fee clearly documented in governance forum post and on-chain. Fee changes require timelock. No hidden rebates or undisclosed arrangements found. | 9 | 9 | Non-Improvable (optimal) | [P2] [Forum](https://forum.morpho.org/t/key-information-on-steakhouse-branded-vaults/1343) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. On-chain supply caps per market enforced by MetaMorpho contract. Allocator rebalances within caps. New market additions require Curator + 7-day timelock + Guardian veto. Cap changes subject to timelocks for increases. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Lending positions can be unwound as borrowers repay. November 2025 stress demonstrated Steakhouse vaults processed approximately 80% of withdrawals within 3 days. Rate model (4x at 100% utilization) creates strong incentive for rapid borrower repayment. No discretionary approvals needed. | 9 | 9 | Non-Improvable (optimal) | [P4] [CryptoRank](https://cryptorank.io/news/feed/275ce-risk-curators-took-off-in-2025-but-led-to-recent-defi-lending-vault-troubles) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending -- no external validators, custodians, or asset managers involved in vault operations. Collateral is held in Morpho Blue smart contracts. Steakhouse Financial (curator) is disclosed. Underlying collateral custodians (Coinbase for cbBTC, BitGo for WBTC, Lido for wstETH, Tether for xAUT) are publicly known. | 9 | 9 | Non-Improvable (optimal) | Vault architecture |

**Protocol Counterparty Subtotal: 45.0/45 (100.0%)**
- 5 questions, all scored 9
- Raw sum = 45 out of max 45
- Weighted = (45/45) x 45 = 45.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain redemption via ERC4626 standard. No address-level blocking capability. No admin pause function. Withdrawal availability depends on market liquidity. No admin approval required. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Moderate. Under normal conditions, substantial USDT available for withdrawal. During November 2025 stress, some Morpho markets temporarily reached 100% utilization. Rate spikes (4x at 100%) incentivize repayment within days, but instant 100% exit not guaranteed. Historical evidence from Steakhouse USDC vault suggests ~80% processable within 3 days during severe stress. Same dynamics apply. | 3 | 3 | Non-Improvable | [P4] [CryptoRank](https://cryptorank.io/news/feed/275ce-risk-curators-took-off-in-2025-but-led-to-recent-defi-lending-vault-troubles) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | Minor delays during November 2025 stress period only. Over the full operational period, the vast majority (>95%) of withdrawals completed promptly. Steakhouse vaults recovered quickly with zero bad debt. | 9 | 9 | Non-Improvable (optimal) | [P4] [CryptoRank](https://cryptorank.io/news/feed/275ce-risk-curators-took-off-in-2025-but-led-to-recent-defi-lending-vault-troubles), [P1] [Morpho Nov 2025](https://morpho.org/blog/morpho-effect-november-2025/) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Caps appropriately sized. During November 2025, delays were driven by market utilization, not by cap design preventing exits. Rate model creates strong incentive for borrower repayment. Caps are transparent and on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Stressed during November 2025. Some Morpho markets temporarily reached 100% utilization. Steakhouse vaults experienced temporary illiquidity but access remained available via direct contract interaction. Conditions normalized within days. Rate model incentivized rapid normalization. | 3 | 3 | Non-Improvable | [P4] [CryptoRank](https://cryptorank.io/news/feed/275ce-risk-curators-took-off-in-2025-but-led-to-recent-defi-lending-vault-troubles) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure USDT lending with no lockups, vesting, or bridge dependencies. Exit depends on borrower repayment or liquidation timelines, not structural lockups. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary redemption through ERC4626 vault always available. Secondary market (steakUSDT trading) exists but is not required for exit. Users can always redeem directly from the vault contract. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | High. USDT is the most liquid stablecoin by market cap (>$180B). steakUSDT is 1:1 backed by vault assets. Can absorb >10% of TVL with low impact under normal conditions. | 9 | 9 | Non-Improvable (optimal) | [P3] Market data |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Moderate. Bank run causes temporary queues and rate spikes (4x at 100% utilization) but is unlikely to cause permanent depositor losses. Market isolation contains risk. November 2025 demonstrated this -- temporary queues but zero permanent losses for Steakhouse depositors. | 3 | 3 | Non-Improvable | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Liquidity Subtotal: 35.0/45 (77.8%)**
- 6 questions scored 9 (sum = 54), 3 questions scored 3 (sum = 9)
- Raw sum = 63 out of max 81
- Weighted = (63/81) x 45 = 35.0

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | steakUSDT trades at NAV (representing 1:1 USDT claim plus accrued yield, currently ~$1.10-1.11). No depeg history. During November 2025 stress, vault share value remained stable -- users claiming USDT at full entitlement. No discount/premium dislocation. | 9 | 9 | Non-Improvable (optimal) | [P3] [CoinGecko steakUSDT](https://www.coingecko.com/en/coins/steakhouse-usdt-morpho-vault) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Mostly low but with USDT-specific caveat. Vault lends USDT -- deposits and returns are USDT-denominated. No directional BTC/ETH exposure for lenders. Risk is borrower default/bad debt, not market direction. HOWEVER, depositors are inherently exposed to USDT value: if USDT depegs (S&P rated Tether stability "weak"), depositors lose purchasing power even without bad debt. This is a plausible risk for a USDT-denominated product that does not exist in the USDC variant. Scoring Mid to reflect this additional USDT denomination risk. | 3 | 3 | Non-Improvable | [P4] [S&P Tether Downgrade](https://www.theblock.co/post/380562/tether-usdt-stability-score-weak-sp-reserves-cant-absorb-bitcoin-drop), [P4] [Tether Reserve Analysis](https://dirtroads.substack.com/p/67-tether-in-2025-a-capital-analysis) |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Immutable Adaptive Curve IRM per market. Rates auto-increase with utilization (4x multiplier at 100% utilization). No governance manipulation possible. Rate curves become steep as utilization approaches critical levels. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. 86% LLTV on BTC markets provides 14% buffer; 77% LLTV on xAUT provides 23% buffer. Liquidation mechanism formally verified by Certora. Pre-liquidation mechanism available for additional safety. | 9 | 9 | Non-Improvable (optimal) | [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side only. Vault lenders benefit from liquidations (5% LIF goes to liquidators). Risk to lenders: insufficient or slow liquidation creating bad debt that gets socialized. Mitigated by economic incentives for liquidators, 14% buffer at 86% LLTV for BTC markets, and 23% buffer at 77% LLTV for xAUT. | 9 | 9 | Non-Improvable (optimal) | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 39.0/45 (86.7%)**
- 4 questions scored 9 (sum = 36), 1 question scored 3 (sum = 3)
- Raw sum = 39 out of max 45
- Weighted = (39/45) x 45 = 39.0

---

### **Strategy Total: 232.8/270 (86.2%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 41.3 | 45 | 91.7% |
| Collateral | 35.0 | 45 | 77.8% |
| Infra Counterparty | 37.5 | 45 | 83.3% |
| Protocol Counterparty | 45.0 | 45 | 100.0% |
| Liquidity | 35.0 | 45 | 77.8% |
| Market | 39.0 | 45 | 86.7% |
| **Strategy Total** | **232.8** | **270** | **86.2%** |

**NOTE:** Precise calculation shows Protocol Mechanics at (66/72)*45 = 41.25 and Market at (39/45)*45 = 39.0. Strategy Total = 41.25 + 35.0 + 37.5 + 45.0 + 35.0 + 39.0 = 232.75. Rounded: 232.8.

---

### OPERATIONS (30% Weight) -- Score: 239.0/270 (88.5%)

**NOTE: All Operations scores are IDENTICAL to the Steakhouse USDC rating. Same curator, same team, same legal entity, same governance model, same documentation, same treasury.**

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid with strong checks. Morpho Blue: immutable. Vault changes: require Owner multisig (5-of-8 Safe) + 7-day timelock (604,800s confirmed via Morpho API) + Guardian veto (Aragon DAO). Curator (2-of-5 Safe) manages market parameters within timelocked bounds. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API - Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x0A0e559bc3b0950a7e448F0d4894db195b9cf8DD/), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | Guardian voting power is distributed proportionally across depositors. Owner multisig has fixed quorum of 5 signers. No single entity can unilaterally control the vault. | 9 | 9 | Non-Improvable (optimal) | [P2] [Guardian Upgrade](https://forum.morpho.org/t/steakhouse-metamorpho-vaults-are-upgrading-their-guardian-setups-to-fully-trustless/527) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. 7-day timelock (604,800s, confirmed via Morpho GraphQL API) on all market changes (above 3-day protocol minimum). Aragon DAO Guardian (0xaeC761545Fd135db6d04D27C92BCB3951668c67F) enables depositor veto of pending changes. Guardian drill tested January 2024. Veto powers clearly bounded. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql), [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
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
| O-TL-05 | Is there an on-call and incident response process for core teams? | Partial evidence. Monitoring bots + Chainalysis partnership confirmed. April 2025 incident demonstrates rapid response capability (4-minute rollback). However, no public 24/7 on-call SLA, formal incident runbook, or response SLA documentation found. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. April 2025 vulnerability: alert received and frontend rolled back within 4 minutes. Active Discord community. Steakhouse publishes regular Kitchen newsletter updates. | 9 | 9 | Non-Improvable (optimal) | [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. a16z, Variant Fund, Pantera Capital, Coinbase Ventures (29 investors total, $73.6M raised). Partnerships publicly announced. | 9 | 9 | Non-Improvable (optimal) | [P4] [Tracxn](https://tracxn.com/d/companies/morpho/__5iKpzjF_-EXELsu5bJ6cORHuQN7HD3ItPqKPexS2FVw) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Steakhouse manages 48 vaults across multiple chains. Potential for allocation decisions to favor some vaults over others. Limited hard constraints -- DDQ process and Credora rating provide qualitative controls, but no formal conflict-of-interest policy with quantitative rules published. | 3 | 9 | **Improvable** | [P2] [Forum](https://forum.morpho.org/t/key-information-on-steakhouse-branded-vaults/1343), [P1] [Steakhouse Wrapped 2025](https://kitchen.steakhouse.financial/p/steakhouse-wrapped-2025) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | No. Zero bad debt across all Steakhouse-curated vaults since inception. November 2025 stress: Steakhouse vaults specifically confirmed zero bad debt while other curators experienced losses. Clean track record. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/products/steakhouse-financial-products/morpho-vaults) |

**Team & Legal Subtotal: 57.5/67.5 (85.2%)**
- 7 questions scored 9 (sum = 63), 2 questions scored 3 (sum = 6)
- Raw sum = 69 out of max 81
- Weighted = (69/81) x 67.5 = 57.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Morpho Docs comprehensive and regularly updated. Steakhouse publishes vault controls, risk management docs, and regular Kitchen newsletter updates. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Docs](https://docs.morpho.org/), [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Detailed explanation of liquidation mechanics, bad debt scenarios, oracle risks, liquidity risks, and vault-specific loss conditions. Both Morpho and Steakhouse documentation cover these topics. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Morpho docs maintain canonical address registry covering Morpho Blue, Vault V1/V2 factories, periphery contracts across all chains. Vault address clearly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Comprehensive documentation of Owner, Curator, Guardian, Allocator roles. Timelock durations, capabilities, and constraints clearly specified. Changes visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves. All vault allocations visible on Morpho App and Etherscan. TVL, market allocations, utilization rates auditable on-chain at any time. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xbEef047a543E45807105E51A8BBEFCc5950fcfBa), [P2] [Morpho App](https://app.morpho.org/ethereum/vault/0xbEef047a543E45807105E51A8BBEFCc5950fcfBa/steakhouse-usdt) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. All core contracts verified on Etherscan including vault contract, Morpho Blue singleton, factories, and periphery. Full source code readable. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Vault](https://etherscan.io/address/0xbEef047a543E45807105E51A8BBEFCc5950fcfBa), [P0] [Etherscan Morpho](https://etherscan.io/address/0xbbbbbbbbbb9cc5e90e3b3af64bdaf62c37eeffcb) |

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
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Resilient. During November 2025 stress, Steakhouse vaults experienced temporary outflows and brief illiquidity but zero bad debt and quick recovery. Protocol-wide TVL grew from $5B to $13B in 2025 despite stress episodes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
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
| **Strategy** | Protocol Mechanics | 41.3 | 45 | 41.3 |
| | Collateral | 35.0 | 45 | 45.0 |
| | Infra Counterparty | 37.5 | 45 | 41.3 |
| | Protocol Counterparty | 45.0 | 45 | 45.0 |
| | Liquidity | 35.0 | 45 | 35.0 |
| | Market | 39.0 | 45 | 39.0 |
| | **Strategy Subtotal** | **232.8** | **270** | **246.6** |
| **Operations** | Governance | 67.5 | 67.5 | 67.5 |
| | Team & Legal | 57.5 | 67.5 | 67.5 |
| | Documentation | 67.5 | 67.5 | 67.5 |
| | Financial Resilience | 46.5 | 67.5 | 67.5 |
| | **Operations Subtotal** | **239.0** | **270** | **270.0** |
| **TOTAL** | | **805.9** | **900** | **865.7** |

---


---
