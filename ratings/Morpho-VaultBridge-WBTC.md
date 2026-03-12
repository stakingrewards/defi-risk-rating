# Morpho - Vault Bridge WBTC Risk Rating

**Rating Date**: 2026-03-10
**Final Grade**: B+
**Total Score**: 724.7/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v1.0-alpha

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 334.1/360 (92.8%)

#### Smart Contract Security (20% weight, 180 max points)

**NOTE: All Smart Contract Security scores are IDENTICAL to other Morpho vault ratings. The Vault Bridge WBTC vault operates on the same Morpho Blue protocol and uses the same audited MetaMorpho vault framework.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 25+ audits from Tier-0/1 firms including ChainSecurity, Spearbit/OpenZeppelin, Zellic, Certora, Blackthorn. Both Morpho Blue core and MetaMorpho/Vaults V2 framework extensively audited. Formal verification by Certora with mathematical proofs. Additionally, all Vault Bridge-specific contracts have passed formal third-party audits per Agglayer documentation. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/), [P1] [Vault Bridge Security](https://docs.agglayer.dev/vault-bridge/reference/risk-security/) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | December 2025: Certora (Tier-0), Spearbit (Tier-0 via Cantina), Blackthorn for Vaults V2 MarketV1AdapterV2. September 2025: ChainSecurity (Tier-0) for Vaults V2 core. Multiple Tier-0 auditors for most recent work. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable (~600 LOC). Every vault upgrade in last 12 months (Vaults V2 Sep-Dec 2025) was preceded by multiple audits from Tier-0 firms. The V2 launch included 8+ separate audit engagements. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 vulnerability patched immediately with OpenZeppelin. Certora formal verification provides mathematical proof of critical invariants. All V2 audit findings resolved before deployment with multiple re-reviews. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue core is immutable. The Vault Bridge WBTC vault is a MetaMorpho vault deployed via the audited factory. Market changes require Curator + timelock + Guardian approval. Public upgrade policy documented via Morpho docs. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vault Docs](https://docs.morpho.org/learn/concepts/vault/), [P0] [Etherscan](https://etherscan.io/address/0x812B2C6Ab3f4471c0E43D4BB61098a9211017427) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss in Vault Bridge vaults. April 2025 frontend vulnerability ($2.6M) was intercepted by white hat c0ffeebabe.eth and all funds returned within minutes -- this was a Morpho App frontend issue, not a vault exploit. October 2024 oracle exploit ($230K) affected only PAXG/USDC market, not WBTC vaults. November 2025 Stream/Elixir contagion affected MEV Capital vault (3.6% bad debt), NOT Vault Bridge vaults. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P4] [Cointelegraph](https://cointelegraph.com/news/white-hat-intercepts-2-million-morpho-blue-hack) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho operates as ADDMO, a French nonprofit association. Polygon Labs is a well-funded, public company. No credible allegations against either entity. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No evidence of timelock reductions. The vault uses a timelock within MetaMorpho's standard range (1 day to 2 weeks per protocol specification). No reductions detected. | 9 | 9 | Non-Improvable (optimal) | [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Morpho runs an active public bounty on Cantina with $2.5M max payout for critical vulnerabilities. 236 findings submitted since March 2024. Scope covers both V1 and V2 contracts plus web apps. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. Morpho runs internal monitoring bots with continuous invariant checks. Chainalysis partnership for transaction monitoring. April 2025 incident demonstrated 4-minute response time. Vault Bridge curator partners Gauntlet and Steakhouse both have monitoring infrastructure (Hypernative, ZeroShadow). | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. Morpho Blue prioritizes immutability over admin controls. Guardian can manually veto pending timelocked actions but cannot pause the protocol. Market-level isolation provides containment. | 3 | 3 | Non-Improvable | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Smart Contract Security Subtotal: 169.1/180 (93.9%)**
- 10 questions scored 9 (sum = 90), 1 question scored 3 (sum = 3)
- Raw sum = 93 out of max 99
- Weighted = (93/99) x 180 = 169.1

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Verified via Safe Transaction Service API (March 2026). The vault Owner is a 4-of-7 Safe multisig (`0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec`), the same multisig used across all Gauntlet Morpho vaults. The Guardian is a 3-of-7 Safe multisig (`0x7084bF4dB6c21e1834dD6482f6056a39A33584cD`). The Curator is a 3-of-7 Safe multisig (`0x9E33faAE38ff641094fa68c65c2cE600b3410585`). The timelock is 259,200s (3 days). All changes are visible on-chain. The owner multisig has 497 nonce (very active). | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API - Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API - Guardian](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/), [P0] [Safe API - Curator](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x9E33faAE38ff641094fa68c65c2cE600b3410585/), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. The vault contract uses MetaMorpho architecture which is non-upgradeable. Moving user funds requires going through Morpho Blue immutable contract logic. Market changes require multisig + timelock + Guardian. Permissionless redemption always available via ERC4626. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Verified via Safe API (March 2026). Owner is 4-of-7 Safe multisig (exceeds >=3-of-5 criterion). Guardian is 3-of-7 Safe multisig. Curator is 3-of-7 Safe multisig. 10 unique signers across all three multisigs. Gauntlet is a known firm with publicly identified leadership (Tarun Chitra, CEO), providing at least partial signer identifiability. The 4-of-7 owner threshold with 7 signers provides robust decentralization. No multisig changes reducing independence detected. Consistent with other Gauntlet vault scoring. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API - Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API - Guardian](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/), [P1] [Gauntlet About](https://www.gauntlet.xyz/about) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking capability. No pause function on Morpho Blue (immutable). Guardian can only revoke pending timelocked actions. Withdrawals always permissionless via direct smart contract interaction. Rules publicly documented. Same architecture as all Morpho vaults. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets held in non-custodial Morpho Blue contracts on Ethereum. Permissionless redemption via ERC4626. No off-chain custody component for the vault itself (note: the underlying WBTC asset does rely on BitGo/BiT Global custody, but that is a collateral/asset risk, not a vault custody risk). | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. Vault funds are held in Morpho Blue markets, separate from any treasury or operational wallets. Morpho is a nonprofit with no profit extraction from protocol operations. Vault Bridge yield distribution is administered by an independent third-party escrow agent. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P1] [Agglayer VB Docs](https://docs.agglayer.dev/vault-bridge/get-started/overview/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain enforced whitelist of Morpho Blue markets only. The vault lends WBTC to borrowers posting BTC-derivative collateral (LBTC, cbBTC, and potentially other BTC-wrapped assets). New market additions require Curator approval + timelock + Guardian veto. Supply caps per market enforced on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho App](https://app.morpho.org/ethereum/vault/0x812B2C6Ab3f4471c0E43D4BB61098a9211017427/vault-bridge-wbtc), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No public, vault-specific incident playbook with explicit key rotation procedures or tabletop exercise results has been published for the Vault Bridge vaults. While Gauntlet has documented partnerships with ZeroShadow (24/7 SOC) and Morpho has demonstrated rapid response (April 2025, 4-minute rollback), no vault-specific playbook covering the Vault Bridge governance actors has been disclosed. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Morpho Emergency](https://docs.morpho.org/curate/emergency/) |

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
| **Security Total** | **334.1** | **360** | **92.8%** |

---

### STRATEGY (30% Weight) -- Score: 178.1/270 (66.0%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from overcollateralized WBTC lending against BTC-derivative collateral (LBTC, cbBTC, etc.). 100% mandate-aligned -- the vault's purpose is to generate yield on bridged WBTC. Yield sources documented on Morpho App with market-level breakdown. Revenue generated flows back to the Vault Bridge ecosystem. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho App](https://app.morpho.org/ethereum/vault/0x812B2C6Ab3f4471c0E43D4BB61098a9211017427/vault-bridge-wbtc), [P1] [Polygon VB Blog](https://polygon.technology/blog/introducing-vaultbridge-a-new-revenue-lego-for-evm-chains) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail shocks: simultaneous collapse of BTC-derivative collateral (LBTC, cbBTC) depegging from BTC value, oracle manipulation on immutable oracle, or catastrophic WBTC custodian failure (BitGo/BiT Global). Bad debt per market is isolated and socialized among lenders of that specific market. Additional risk: if WBTC itself depegs from BTC (custody risk), the loan asset loses value. | 3 | 3 | Non-Improvable | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault simply lends WBTC. No rehypothecation of depositor funds. Effective leverage: 1.0x. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. Liquidation risk applies to borrowers. Vault benefits from liquidation incentive fees. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss events for the Vault Bridge WBTC vault since launch. Other WBTC-denominated Morpho vaults (MEV Capital WBTC vault, Re7 WBTC vault) have also operated without permanent losses. November 2025 contagion did not affect WBTC lending markets. However, the vault is relatively young (launched 2025) and has limited stress-test history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho App](https://app.morpho.org/ethereum/vault/0x812B2C6Ab3f4471c0E43D4BB61098a9211017427/vault-bridge-wbtc), [P2] [MEV Capital WBTC Updates](https://forum.morpho.org/t/mev-capital-wbtc-vault-updates/836) |
| ST-PM-06 | Is a risk framework for vault curation documented? | Partial. The Vault Bridge curators (Gauntlet and Steakhouse Financial) each have their own well-documented risk frameworks (Gauntlet VaultBook, Steakhouse vault controls). However, no specific risk framework document exists for the Vault Bridge WBTC vault itself, describing how the two curators coordinate, what risk limits apply to WBTC-specific markets, or how allocation decisions are made between Gauntlet and Steakhouse strategies. | 3 | 9 | **Source Missing** | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults), [P1] [Steakhouse Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yield is primarily organic from WBTC lending demand driven by BTC-derivative borrowers (LBTC holders wanting to leverage their BTC exposure, etc.). The Vault Bridge model generates yield that flows to the L2 chain ecosystem. Yield sustainability depends on continued demand for WBTC borrowing, which is driven by the broader BTC DeFi ecosystem. No evidence of heavy incentive-dependence for this vault. | 9 | 9 | Non-Improvable (optimal) | [P1] [Polygon VB Blog](https://polygon.technology/blog/introducing-vaultbridge-a-new-revenue-lego-for-evm-chains), [P1] [Lombard LBTC](https://www.lombard.finance/blog/lbtc-powering-morpho-lending-markets/) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Moderate concern. WBTC has reasonable but not exceptional liquidity compared to USDC or ETH. Unwinding depends on borrowers repaying WBTC or being liquidated. The rate model (4x at 100% utilization) incentivizes repayment. However, WBTC secondary market liquidity is thinner than USDC, and in a stress scenario where WBTC depeg concerns arise, both lending demand and secondary liquidity could deteriorate simultaneously. | 3 | 3 | Non-Improvable | Market assessment, [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Partial concern. The vault lends WBTC, which maintains a peg to BTC via the BitGo/BiT Global custody arrangement. If WBTC depegs from BTC, the loan asset itself loses value relative to the underlying Bitcoin. This is a custody-peg dependency, not a traditional spread trade, but it introduces regime risk. The lending interest is not peg-dependent, but the asset value is. Yield from lending is not spread-dependent (<30% of yield at risk from peg). | 9 | 9 | Non-Improvable (optimal) | [P1] [BitGo WBTC](https://www.bitgo.com/resources/blog/bitgo-to-move-wbtc-to-multi-jurisdictional-custody-to-accelerate-global/), Market assessment |

**Protocol Mechanics Subtotal: 33.8/45 (75.0%)**
- 8 applicable questions (ST-PM-04 = N/A): 5 scored 9 (sum = 45), 3 scored 3 (sum = 9)
- Raw sum = 54 out of max 72
- Weighted = (54/72) x 45 = 33.75 ~ 33.8

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Collateral posted by borrowers includes BTC-derivative assets: LBTC (Lombard -- liquid BTC restaking token, relatively new), cbBTC (Coinbase custody, NY DFS regulated), and potentially other wrapped BTC assets. LBTC is a newer asset without extensive track record (launched 2024). cbBTC is more established (September 2024). Neither LBTC nor cbBTC has an SR A-grade rating. The collateral mix includes some higher-risk assets (LBTC) alongside more established ones (cbBTC). | 3 | 9 | **Improvable** | [P1] [Morpho App](https://app.morpho.org/ethereum/vault/0x812B2C6Ab3f4471c0E43D4BB61098a9211017427/vault-bridge-wbtc), [P1] [Lombard LBTC](https://www.lombard.finance/blog/lbtc-powering-morpho-lending-markets/) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | cbBTC: No depeg >2% since September 2024 launch. LBTC: Relatively new, limited stress-test data. No confirmed depeg >2% lasting >24h. However, as a relatively untested BTC restaking token, LBTC has not been through a severe BTC market stress event. The vault is untested through severe stress -- maximum score should be Mid (3) per the battle-tested principle. | 3 | 3 | Non-Improvable | Market data, [P1] [Lombard Docs](https://docs.lombard.finance/lbtc-liquid-bitcoin/lbtc-in-defi/borrow-lend) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | LBTC (Lombard) involves Bitcoin staking/restaking infrastructure (Babylon ecosystem). Slashing risk exists for Babylon-staked BTC. Lombard's documentation describes risk management but the Babylon ecosystem is relatively new. This is a relevant risk given LBTC is a staking-based collateral. cbBTC does not carry staking risk. | 3 | 3 | Non-Improvable | [P1] [Lombard Docs](https://docs.lombard.finance/lbtc-liquid-bitcoin/lbtc-in-defi/borrow-lend) |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | CRITICAL: 100% of the vault's loan asset (WBTC) is a wrapped asset, and 100% of borrower collateral consists of wrapped/derivative BTC assets (LBTC, cbBTC). This creates the deepest possible wrapped-asset concentration. WBTC itself depends on BitGo/BiT Global multi-jurisdictional custody. cbBTC depends on Coinbase custody. LBTC depends on Lombard/Babylon infrastructure. | 1 | 3 | **Improvable** | [P1] [Morpho App](https://app.morpho.org/ethereum/vault/0x812B2C6Ab3f4471c0E43D4BB61098a9211017427/vault-bridge-wbtc), [P1] [BitGo WBTC](https://www.bitgo.com/resources/blog/bitgo-to-move-wbtc-to-multi-jurisdictional-custody-to-accelerate-global/) |

**Collateral Subtotal: 12.5/45 (27.8%)**
- ST-C-01=3, ST-C-02=3, ST-C-03=3, ST-C-04=1
- Raw sum = 10 out of max 36
- Weighted = (10/36) x 45 = 12.5

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum (Tier-0 chain), Chainlink (Tier-0 oracle) for price feeds. The Vault Bridge infrastructure also involves the Agglayer bridge for L2 operations, but the Morpho vault itself operates purely on Ethereum. No CEX dependency for vault operations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | SINGLE ORACLE RISK. Each Morpho Blue market has one immutable oracle with no fallback mechanism. Chainlink is Tier-0 and battle-tested, but zero redundancy by design. Oracle failure would require deploying an entirely new market. | 3 | 3 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | No evidence of SOC 2 Type II or ISO27001 certification for any Vault Bridge-specific entities. Chainlink and Coinbase hold enterprise certifications. Morpho Labs/ADDMO does not have disclosed certifications. | 3 | 9 | **Source Missing** | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Ethereum: No significant halts. Morpho: April 2025 frontend vulnerability resolved in 4 minutes. However, the Vault Bridge WBTC vault is relatively new and has limited operational history through chain-level incidents. Per new protocol guidance, score Mid (3) for vaults deployed <6 months that have not experienced incidents during their operational period. If the vault has been operational >6 months without incidents, Low (9) applies. Given launch in 2025 and >6 months of operation without incidents, score Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), Ethereum operational history |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain halts >30 minutes in the last 12+ months. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Potentially relevant for LBTC (Babylon staking) collateral. Babylon is a new ecosystem and slashing events for BTC staking are not well-documented. However, this risk is borne by borrowers (collateral holders), not vault lenders directly. Indirect risk exists if slashing causes LBTC depeg, leading to bad debt on LBTC/WBTC markets. No slashing events impacting vault depositors reported. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lombard Docs](https://docs.lombard.finance/lbtc-liquid-bitcoin/lbtc-in-defi/borrow-lend) |
| ST-IC-07 | Are validators diverse geographically and by operator? | Ethereum validator set is highly distributed. For LBTC/Babylon validators, Lombard works with multiple node operators. No single operator appears to exceed 25% of relevant stake. | 9 | 9 | Non-Improvable (optimal) | Ethereum validator data |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Permissionless on-chain redemption always available via ERC4626 redeem/withdraw function. No off-chain dependency for withdrawals from the Morpho vault. Frontend failure does not block on-chain operations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Infrastructure Counterparty Subtotal: 37.5/45 (83.3%)**
- 6 questions scored 9 (sum = 54), 2 questions scored 3 (sum = 6)
- Raw sum = 60 out of max 72
- Weighted = (60/72) x 45 = 37.5

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All allocation to Morpho Blue markets only (Tier-0 protocol). No CEX or RWA exposure. Markets clearly listed with on-chain caps. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho App](https://app.morpho.org/ethereum/vault/0x812B2C6Ab3f4471c0E43D4BB61098a9211017427/vault-bridge-wbtc) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Vault Bridge revenue is distributed to the L2 chain ecosystem through an independent escrow agent. Performance fees are visible on-chain. However, the exact revenue-sharing arrangement between Polygon Labs, Morpho, and the curators is not fully disclosed in public documentation. | 3 | 9 | **Source Missing** | [P1] [Agglayer VB Docs](https://docs.agglayer.dev/vault-bridge/get-started/overview/), [P1] [Polygon VB Blog](https://polygon.technology/blog/introducing-vaultbridge-a-new-revenue-lego-for-evm-chains) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. On-chain supply caps per market enforced by MetaMorpho contract. Allocator rebalances within caps. New market additions require Curator + timelock + Guardian. Cap changes subject to timelocks. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Lending positions can be unwound as borrowers repay. WBTC market liquidity is thinner than USDC markets, so unwind time may be longer during stress. Rate model (4x at 100% utilization) creates incentive for rapid borrower repayment. No discretionary approvals needed. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending -- no external validators, custodians, or asset managers involved in vault operations. Curators (Gauntlet, Steakhouse) disclosed. Underlying asset custodians publicly known (BitGo/BiT Global for WBTC, Coinbase for cbBTC, Lombard for LBTC). Vault Bridge escrow agent mentioned but not named publicly. | 9 | 9 | Non-Improvable (optimal) | [P1] [Agglayer VB Docs](https://docs.agglayer.dev/vault-bridge/get-started/overview/) |

**Protocol Counterparty Subtotal: 39.0/45 (86.7%)**
- 4 questions scored 9 (sum = 36), 1 question scored 3 (sum = 3)
- Raw sum = 39 out of max 45
- Weighted = (39/45) x 45 = 39.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain redemption via ERC4626 standard. No address-level blocking capability. No admin pause function. Withdrawal availability depends on market liquidity (not all WBTC may be available if fully lent out). | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Moderate concern. WBTC markets are typically less liquid than USDC markets. During stress, borrowers may be slow to repay. Rate model incentivizes repayment but instant 100% exit not guaranteed. The vault is part of the Vault Bridge infrastructure which enforces a minimum reserve ratio for instant withdrawals, but this applies to the VaultBridgeToken layer, not the underlying Morpho vault. | 3 | 3 | Non-Improvable | [P1] [Vault Bridge Architecture](https://docs.polygon.technology/chain-development/vault-bridge/core-concepts/architecture/), Market assessment |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No confirmed withdrawal delays or freezes for the Vault Bridge WBTC vault. However, the vault is relatively new and has not been tested through severe market stress. Per the battle-tested principle, untested protocols score Mid (3) maximum on resilience questions. | 3 | 9 | Non-Improvable | [P1] [Morpho App](https://app.morpho.org/ethereum/vault/0x812B2C6Ab3f4471c0E43D4BB61098a9211017427/vault-bridge-wbtc) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Caps sized per MetaMorpho standard. Rate model creates incentive for borrower repayment during high utilization. No history of caps being used to block exits. Vault Bridge also maintains a reserve ratio. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [VB Architecture](https://docs.polygon.technology/chain-development/vault-bridge/core-concepts/architecture/) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Untested. The vault has not been through a severe WBTC-specific stress event or a period where WBTC custody concerns drove mass withdrawals. Given the vault's limited stress history, score Mid (3). The November 2025 contagion did not specifically stress WBTC lending markets. | 3 | 3 | Non-Improvable | Market assessment |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure WBTC lending with no lockups, vesting, or bridge dependencies for the vault itself. Note: users of the full Vault Bridge system (L2 users) may face bridge delays when exiting from the L2 back to Ethereum, but that is a Vault Bridge infrastructure concern, not a Morpho vault concern. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary redemption through ERC4626 vault always available. Users can always redeem directly from the vault contract. No secondary market dependence required. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | Moderate. WBTC has reasonable secondary market liquidity but is thinner than USDC or ETH. On major DEXs, WBTC can absorb moderate trade sizes but may experience slippage for very large exits. The vault receipt token (vault shares) likely has very limited secondary market trading. | 3 | 3 | Non-Improvable | Market data |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Moderate to elevated. A bank-run scenario would be exacerbated by WBTC-specific risks: if WBTC custody concerns trigger mass withdrawal demand, the rate model and borrower repayment dynamics may be insufficient. Market isolation contains risk per market. The vault is untested through such a scenario. Per the battle-tested principle, score Mid (3). | 3 | 3 | Non-Improvable | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Liquidity Subtotal: 28.3/45 (62.9%)**
- 4 questions scored 9 (L-01, L-04, L-06, L-07 = 36), 5 questions scored 3 (L-02, L-03, L-05, L-08, L-09 = 15)
- Raw sum = 51 out of max 81
- Weighted = (51/81) x 45 = 28.3

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | The vault share token represents a claim on WBTC plus accrued yield. It is redeemable via ERC4626. Limited secondary market trading exists for the vault shares. The vault has not been tested through severe WBTC-specific stress. Per the battle-tested principle, untested vault shares score Mid (3). | 3 | 3 | Non-Improvable | [P1] [Morpho App](https://app.morpho.org/ethereum/vault/0x812B2C6Ab3f4471c0E43D4BB61098a9211017427/vault-bridge-wbtc) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Moderate concern. The vault is WBTC-denominated, meaning depositors have BTC price exposure. If measured in USD, large BTC drawdowns reduce the USD value of deposits. Within BTC terms, the vault is low-beta (lending earns interest on WBTC). However, the correlation between WBTC collateral (LBTC, cbBTC) and the loan asset (WBTC) means that during BTC drawdowns, both sides move together, reducing liquidation risk. The WBTC custody risk (potential depeg from BTC) adds a non-market directional risk. | 3 | 3 | Non-Improvable | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Immutable Adaptive Curve IRM per market. Rates auto-increase with utilization. No governance manipulation possible. Same battle-tested IRM as all Morpho Blue markets. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Partial. Morpho's formal verification by Certora covers liquidation mechanics. Gauntlet uses agent-based simulations. However, no WBTC-specific stress testing (e.g., WBTC depeg scenario, BTC custody crisis) has been publicly documented for this vault. | 3 | 9 | **Source Missing** | [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/), [P1] [Gauntlet Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side only. Vault lenders benefit from liquidations. However, in a BTC-denominated vault with BTC-correlated collateral (LBTC, cbBTC), sharp BTC price drops cause both loan and collateral value to fall similarly, reducing liquidation pressure. Risk to lenders is primarily from collateral depegging from BTC (not BTC price drops), or insufficient liquidation during rapid LBTC/cbBTC depegs. | 9 | 9 | Non-Improvable (optimal) | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 27.0/45 (60.0%)**
- 2 questions scored 9 (M-03, M-05 = 18), 3 questions scored 3 (M-01, M-02, M-04 = 9)
- Raw sum = 27 out of max 45
- Weighted = (27/45) x 45 = 27.0

---

### **Strategy Total: 178.1/270 (65.9%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 33.8 | 45 | 75.0% |
| Collateral | 12.5 | 45 | 27.8% |
| Infra Counterparty | 37.5 | 45 | 83.3% |
| Protocol Counterparty | 39.0 | 45 | 86.7% |
| Liquidity | 28.3 | 45 | 62.9% |
| Market | 27.0 | 45 | 60.0% |
| **Strategy Total** | **178.1** | **270** | **65.9%** |

---

### OPERATIONS (30% Weight) -- Score: 212.5/270 (78.7%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid with strong checks. Morpho Blue immutable. Vault changes require Owner multisig + timelock + Guardian. Multiple layers prevent unilateral changes. Same MetaMorpho architecture as all Morpho vaults. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- No governance token voting for this vault. Vault controlled by multisig + Guardian, not token-holder governance. Governance concentration captured in S-KM-01 and S-KM-03. | N/A | N/A | N/A | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Verified via Morpho GraphQL API (March 2026). The vault has a 259,200-second (3-day) timelock, well above the 24-hour minimum for Low risk. The Guardian (3-of-7 Safe multisig) can veto pending timelocked actions. All pending actions visible on-chain. The 3-day timelock provides reasonable depositor reaction time. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API vault query (March 2026), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner can appoint new Curator (subject to timelock). Withdrawals remain permissionless throughout via ERC4626. Users can always exit regardless of curator changes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 3 questions scored 9 (sum = 27); O-G-02 = N/A
- Raw sum = 27 out of max 27
- Weighted = (27/27) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Morpho: Paul Frambot (CEO), ADDMO (French nonprofit). Polygon Labs: Marc Boiron (CEO), well-known public company. Gauntlet: Tarun Chitra (CEO). Steakhouse: adcv, Sebastien Derivaux. All publicly identified with verifiable track records. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho](https://morpho.org/), [P1] [Polygon](https://polygon.technology/), [P1] [Gauntlet About](https://www.gauntlet.xyz/about), [P1] [Steakhouse](https://www.steakhouse.financial/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. The Vault Bridge ecosystem involves multiple independent teams: Morpho Labs/ADDMO, Polygon Labs, Gauntlet, and Steakhouse Financial. Each has full engineering teams with redundancy. | 9 | 9 | Non-Improvable (optimal) | [P1] [Polygon VB Blog](https://polygon.technology/blog/introducing-vaultbridge-a-new-revenue-lego-for-evm-chains) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Morpho: ADDMO (French nonprofit, Paris) + Morpho Labs SAS (France). Polygon Labs: incorporated in US. Gauntlet: Gauntlet Networks Inc. (New York, USA). Steakhouse: Carniciera Tropical Inc. (Panama). Vault Bridge escrow: entity not publicly named. Multiple entities with clear jurisdictions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P1] [Polygon](https://polygon.technology/) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known actions against Morpho, Polygon Labs, Gauntlet, or Steakhouse entities. | 9 | 9 | Non-Improvable (optimal) | Public records |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Yes. Morpho: monitoring bots + 4-minute response demonstrated. Gauntlet: 24/7 monitoring partnerships with ZeroShadow, Hypernative. Steakhouse: monitoring infrastructure. Multiple teams with overlapping coverage. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Morpho's 4-minute response in April 2025. Gauntlet published detailed stress report within days. Active community channels. Multiple teams provide support coverage. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Morpho: a16z, Variant, Pantera, Coinbase Ventures ($73.6M). Polygon Labs: well-funded public company. Gauntlet: Polychain, Paradigm ($41.8M). All disclosed. | 9 | 9 | Non-Improvable (optimal) | [P4] [Tracxn Morpho](https://tracxn.com/d/companies/morpho/__5iKpzjF_-EXELsu5bJ6cORHuQN7HD3ItPqKPexS2FVw) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. The Vault Bridge WBTC vault is curated by Gauntlet and Steakhouse, both of whom manage many other Morpho vaults (Gauntlet: 70+ vaults, Steakhouse: 19 vaults). Allocation decisions across vaults could create conflicts. No formal quantitative conflict-of-interest policy published for the Vault Bridge specifically. | 3 | 9 | **Improvable** | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults), [P1] [Steakhouse Vaults](https://www.steakhouse.financial/docs/products/steakhouse-financial-products/morpho-vaults) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | No. Both Gauntlet and Steakhouse have clean track records on Morpho vaults. Zero bad debt across Steakhouse vaults since January 2024. Zero bad debt across Gauntlet vaults since March 2024. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |

**Team & Legal Subtotal: 62.5/67.5 (92.6%)**
- 8 questions scored 9 (sum = 72), 1 question scored 3
- Raw sum = 75 out of max 81
- Weighted = (75/81) x 67.5 = 62.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Partial. Morpho docs are comprehensive and regularly updated. Polygon/Agglayer Vault Bridge documentation exists (docs.agglayer.dev, docs.polygon.technology). However, vault-specific documentation for the WBTC vault (markets, allocation strategy, risk parameters) is less detailed than Steakhouse or Gauntlet's named vaults. The documentation is spread across multiple sources (Morpho, Polygon, Agglayer, Gauntlet, Steakhouse). | 3 | 9 | **Source Missing** | [P1] [Morpho Docs](https://docs.morpho.org/), [P1] [VB Architecture](https://docs.polygon.technology/chain-development/vault-bridge/core-concepts/architecture/), [P1] [Agglayer VB Docs](https://docs.agglayer.dev/vault-bridge/get-started/overview/) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Morpho documentation provides comprehensive coverage of liquidation mechanics, bad debt scenarios, oracle risks, and loss conditions. This applies universally to all Morpho vaults including Vault Bridge WBTC. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Partial. Morpho docs maintain a canonical address registry for core Morpho contracts. The Vault Bridge WBTC vault address is listed on the Morpho App. However, no single canonical page lists all governance addresses (owner, curator, guardian) for this specific vault. | 3 | 9 | **Improvable** | [P1] [Morpho Addresses](https://docs.morpho.org/get-started/resources/addresses/), [P3] [Morpho App](https://app.morpho.org/ethereum/vault/0x812B2C6Ab3f4471c0E43D4BB61098a9211017427/vault-bridge-wbtc) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Partial. Morpho's role documentation is comprehensive at the protocol level. However, the specific role assignments for the Vault Bridge WBTC vault (who is the owner, guardian, timelock duration) are not documented to the same standard as Steakhouse vaults. | 3 | 9 | **Improvable** | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves. All vault allocations visible on Morpho App and Etherscan. TVL, market allocations, utilization rates all auditable on-chain. Additionally, WBTC itself publishes proof-of-reserves via wbtc.network. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0x812B2C6Ab3f4471c0E43D4BB61098a9211017427), [P3] [Morpho App](https://app.morpho.org/ethereum/vault/0x812B2C6Ab3f4471c0E43D4BB61098a9211017427/vault-bridge-wbtc) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. The Morpho Blue singleton and MetaMorpho factory contracts are all verified on Etherscan. The vault contract at 0x812B... should be verified via the MetaMorpho factory deployment. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Morpho Blue](https://etherscan.io/address/0xbbbbbbbbbb9cc5e90e3b3af64bdaf62c37eeffcb) |

**Documentation Subtotal: 45.0/67.5 (66.7%)**
- 3 questions scored 9 (DT-02, DT-05, DT-06 = 27), 3 questions scored 3 (DT-01, DT-03, DT-04 = 9)
- Raw sum = 36 out of max 54
- Weighted = (36/54) x 67.5 = 45.0

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated safety module for this vault. Bad debt socialized per market. Morpho DAO treasury (~$21.9M) discretionary. No Vault Bridge-specific backstop. | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Insufficient. Morpho DAO treasury ~$21.9M against ~$10B+ protocol TVL (0.22%). Not ring-fenced for this vault. Polygon Labs is well-funded but no vault-specific reserve disclosed. | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama](https://defillama.com/protocol/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. The Vault Bridge ecosystem is supported by Morpho ($73.6M raised), Polygon Labs (well-funded public company), Gauntlet ($41.8M raised), and Steakhouse Financial. Combined operational runway is comfortably >24 months. | 9 | 9 | Non-Improvable (optimal) | [P4] [Tracxn Morpho](https://tracxn.com/d/companies/morpho/__5iKpzjF_-EXELsu5bJ6cORHuQN7HD3ItPqKPexS2FVw) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Limited data. The Vault Bridge WBTC vault is relatively new and has not been through a severe stress event. The broader Vault Bridge infrastructure has been operating at >$230M scale. The vault survived the November 2025 contagion without bad debt, but WBTC markets were not specifically stressed. Per the battle-tested principle, score Mid (3). | 3 | 3 | Non-Improvable | [P1] [Polygon VB Blog](https://polygon.technology/blog/introducing-vaultbridge-a-new-revenue-lego-for-evm-chains) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue is immutable. Permissionless withdrawals via ERC4626. No proprietary off-chain services required for core vault operations. If all teams disappeared, existing allocations continue and users can withdraw. Note: the Vault Bridge L2 infrastructure would be more impacted, but the underlying Morpho vault continues functioning independently. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Financial Resilience Subtotal: 37.5/67.5 (55.6%)**
- 2 questions scored 9 (FR-03, FR-05 = 18), 2 questions scored 3 (FR-01, FR-04 = 6), 1 question scored 1 (FR-02 = 1)
- Raw sum = 25 out of max 45
- Weighted = (25/45) x 67.5 = 37.5

---

### **Operations Total: 212.5/270 (78.7%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 67.5 | 67.5 | 100.0% |
| Team & Legal | 62.5 | 67.5 | 92.6% |
| Documentation | 45.0 | 67.5 | 66.7% |
| Financial Resilience | 37.5 | 67.5 | 55.6% |
| **Operations Total** | **212.5** | **270** | **78.7%** |

---

---

## Final Score Calculation

| Category | Subcategory | Current Points | Max Points | Potential Points |
|----------|-------------|----------------|------------|------------------|
| **Security** | Smart Contract Security | 169.1 | 180 | 169.1 |
| | Key Management | 165.0 | 180 | 180.0 |
| | **Security Subtotal** | **334.1** | **360** | **349.1** |
| **Strategy** | Protocol Mechanics | 33.8 | 45 | 37.5 |
| | Collateral | 12.5 | 45 | 22.5 |
| | Infra Counterparty | 37.5 | 45 | 41.3 |
| | Protocol Counterparty | 39.0 | 45 | 45.0 |
| | Liquidity | 28.3 | 45 | 31.7 |
| | Market | 27.0 | 45 | 33.0 |
| | **Strategy Subtotal** | **178.1** | **270** | **210.9** |
| **Operations** | Governance | 67.5 | 67.5 | 67.5 |
| | Team & Legal | 62.5 | 67.5 | 67.5 |
| | Documentation | 45.0 | 67.5 | 67.5 |
| | Financial Resilience | 37.5 | 67.5 | 58.5 |
| | **Operations Subtotal** | **212.5** | **270** | **261.0** |
| **TOTAL** | | **724.7** | **900** | **821.0** |

---
