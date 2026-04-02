# Aave - cbBTC (Ethereum Core Market) Risk Rating

**Rating Date**: 2026-04-01
**Final Grade**: BBB+
**Total Score**: 842.3/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-beta

---

## Detailed Analysis

### SECURITY (40% Weight) - Score: 342.9/360 (95.3%)

**NOTE: All Security scores are IDENTICAL to other Aave Ethereum V3 Core Market ratings per Platform Consistency requirement. Same smart contracts, same key management, same governance infrastructure.**

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 30+ audits from Tier-0/1 firms: OpenZeppelin (2021), Trail of Bits (2022), Sigma Prime (2022, 2023), PeckShield (2022), ABDK (2022), Certora (continuous formal verification through V3.6), MixBytes (V3.1+), Pashov (V3.2+), Sherlock (V3.3), Oxorio (V3.2-V3.3). Latest V3.6 audits include Certora and StErMi. All reports public on GitHub. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [GitHub Audits](https://github.com/aave/aave-v3-core/tree/master/audits) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | V3.4 (June 2025): Certora (Tier-0, formal verification), StErMi. V3.3 (Jan 2025): Certora (Tier-0), Sherlock (Tier-0), Oxorio, StErMi. Multiple Tier-0 auditors on latest versions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [Certora Reports](https://www.certora.com/reports/aave-v3-risk-steward) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Every major version (V3.0 through V3.6) has been audited. Umbrella Safety Module (June 2025), GHO (7 audits), Governance V3 all received dedicated audits. Continuous audit coverage across all upgrades. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [GitHub aave-v3-origin](https://github.com/aave-dao/aave-v3-origin) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. November 2023 critical vulnerability (stable rate bug) patched immediately via emergency governance. All findings tracked with remediation. Certora formal verification provides mathematical proofs. Sherlock contest on V3.3 validated remediation. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P1] [Aave Security](https://aave.com/security) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Upgradeable via transparent proxy pattern. Upgrades require full DAO governance vote followed by 1-day standard timelock or 7-day critical timelock. Two 5-of-9 Guardian multisigs can veto malicious proposals. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No user fund losses in protocol history. Nov 2023: critical stable rate vulnerability patched before exploitation. Aug 2024: periphery contract incident ($56K, not user deposits). March 2026: CAPO oracle misconfiguration caused wstETH liquidations but cbBTC was unaffected (uses BTC/USD oracle, not CAPO). Core protocol has never been exploited for user funds. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Post-Mortem](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Founded by Stani Kulechov in 2017 (ETHLend). 8+ year track record with fully transparent governance and publicly identified team. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. Standard proposals maintain 1-day delay, critical changes require 7-day delay. Guardian system provides additional veto layer. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Immunefi bounty up to $1M for critical smart contract vulnerabilities. 83+ assets in scope. Active since October 2023, last updated September 2025. Bug bounty actively used -- Nov 2023 critical vulnerability reported through program and Aug 2025 bounty payout documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [Immunefi](https://immunefi.com/bug-bounty/aave/), [P2] [BGD Bounty Payout Aug 2025](https://governance.aave.com/t/bgd-request-for-bounty-payout-august-2025/23096) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. DDoS protection, DNSSEC authentication, intrusion detection, CSP/SRI checks documented. Chaos Labs operates Risk Stewards with 1,100+ automated parameter adjustments. Slope2 Risk Oracle provides automated interest rate response. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P2] [Chaos Labs Slope2 Oracle](https://chaoslabs.xyz/posts/introducing-the-aave-slope2-risk-oracle) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Yes. Protocol Emergency Guardian (5-of-9) can pause markets. V3.3 bad debt verification prevents new bad debt post-liquidation. Slope2 Risk Oracle automatically adjusts borrow rates during high utilization. Feb 2026: automated mechanisms processed $429M liquidations without bad debt. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P1] [Aave V3 Features](https://github.com/aave-dao/aave-v3-origin/blob/main/docs/3.3/Aave-v3.3-features.md) |

**Smart Contract Security Subtotal: 180.0/180 (100.0%)**
- 11 questions x 9 = 99
- Raw: 99/99, Weighted: (99/99) x 180 = 180.0

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | DAO governance via AAVE/stkAAVE/aAAVE token voting. All changes require on-chain vote with quorum, then 1-7 day timelock execution. Protocol Emergency Guardian (5-of-9) and Governance Emergency Guardian (5-of-9) provide emergency controls. Risk Stewards (Chaos Labs) adjust parameters within governance-approved bounds. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Requires DAO vote (quorum required) + timelock execution. Guardians can only pause/veto, not move funds or upgrade custody. Protocol is non-custodial with permissionless withdrawals. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2#code) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Protocol Emergency Guardian: 5-of-9 (Chaos Labs, LlamaRisk, Karpatkey, TokenLogic, Certora, BGD Labs, ACI, 2 DAO delegates). Governance Emergency Guardian: 5-of-9 (Zapper, ParaSwap, Standard Crypto, DeFi Saver, Balancer, Chainlink, Lido, security firms). Note: BGD Labs and ACI departing by mid-2026 may require signer replacement. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [Guardian Renewal](https://governance.aave.com/t/arfc-renewal-of-aave-guardian-2024/17523) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause limited to Guardians via 5-of-9 multisig. No address-level blocking capability within Aave. Withdrawals are permissionless via Pool contract. Note: cbBTC token itself has blacklist/pause capability controlled by Coinbase -- this is a token-level risk, not an Aave protocol risk. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [cbBTC FiatTokenV2_1](https://etherscan.io/address/0x7458bfdc30034eb860b265e6068121d18fa5aa72#code) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user cbBTC deposits held in Pool V3 contract (0x87870Bca3F3fD6335C3F4ce8392D69350B4fA4E2). Permissionless supply/withdraw. Note: cbBTC itself depends on Coinbase BTC custody off-chain, but within Aave the cbBTC tokens are held non-custodially. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P0] [aEthcbBTC](https://etherscan.io/address/0x5c647cE0Ae10658ec44FA4E11A51c96e94efd1Dd) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation: Pool V3 contract holds all user funds. DAO treasury managed separately by Karpatkey. No co-mingling. | 9 | 9 | Non-Improvable (optimal) | [P2] [DAO Financial Reports](https://governance.aave.com/t/aave-dao-financial-reports-financial-metrics/5575), [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- Aave is a lending protocol, not a vault. Users deposit cbBTC directly to the pool. No external protocol routing. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | **Partial.** November 2023 incident demonstrated rapid emergency response (pools secured within hours). March 2026 CAPO incident: borrow caps reduced within hours. However, no comprehensive public playbook for key rotation or signer replacement is documented. Critical gap given BGD Labs and ACI departures. | 3 | 9 | **Improvable** | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |

**Key Management Subtotal: 162.9/180 (90.5%)**
- 6 questions at score 9 = 54 points
- 1 question at score 3 = 3 points
- 1 question N/A (S-KM-07)
- Raw: 57/63, Weighted: (57/63) x 180 = 162.857 = 162.9

**Security Total: 180.0 + 162.9 = 342.9/360 (95.3%)**

---

### STRATEGY (30% Weight) - Score: 243.4/270 (90.1%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | cbBTC supply yield comes from overcollateralized borrower interest. Current utilization is extremely low (~1.01%), resulting in near-zero supply APY (~0.00%). cbBTC is primarily held as collateral for borrowing stablecoins or ETH. 100% organic from borrower demand. Reserve factor is 20%. Yield sources are clear and mandate-aligned. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan cbBTC](https://aavescan.com/ethereum-v3/cbbtc), [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss can occur in severe but plausible scenarios: (1) Bad debt from cascading liquidations; (2) Smart contract exploit; (3) **cbBTC-specific: Coinbase custodial failure or BTC reserve shortfall** -- cbBTC token has blacklist/pause capabilities controlled by Coinbase (FiatTokenV2_1 implementation). Coinbase can freeze addresses. Unlike WBTC, the Aave oracle uses BTC/USD (not cbBTC/BTC), meaning a cbBTC depeg from BTC would NOT be reflected in pricing, allowing attackers to borrow at stale prices. Coinbase launched Chainlink PoR (May 2025) but it is NOT integrated into Aave's cbBTC oracle. Single custodian dependency = severe but plausible risk. | 3 | 3 | Non-Improvable | [P0] [cbBTC FiatTokenV2_1](https://etherscan.io/address/0x7458bfdc30034eb860b265e6068121d18fa5aa72), [P2] [cbBTC Listing ARFC](https://governance.aave.com/t/arfc-onboard-cbbtc-to-aave-v3-on-base-and-mainnet/18988), [P1] [Chainlink cbBTC PoR](https://data.chain.link/feeds/ethereum/mainnet/cbbtc-por) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No protocol-level leverage or rehypothecation. User deposits remain in the Pool contract. Users can individually construct leveraged positions but that is user-level risk. cbBTC/WBTC E-Mode allows up to 93% LTV for BTC-to-BTC borrowing. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P2] [cbBTC/WBTC E-Mode](https://governance.aave.com/t/arfc-enable-cbbtc-wbtc-liquid-e-mode-on-aave-v3-mainnet/19705) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | Yes. Two-slope interest rate model with automated rate adjustments. V3.3 bad debt verification prevents new bad debt post-liquidation. 100% close factor below 0.95 health factor. For cbBTC, utilization is so low (~1.01%) that rate model stress is not a practical concern. Liquidation parameters: LTV 73%, liquidation threshold 78%, 7.5% penalty. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Features](https://github.com/aave-dao/aave-v3-origin/blob/main/docs/3.3/Aave-v3.3-features.md), [P2] [cbBTC Listing ARFC](https://governance.aave.com/t/arfc-onboard-cbbtc-to-aave-v3-on-base-and-mainnet/18988) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent losses to cbBTC lenders since listing (Sept 2024). Feb 2026: during severe market crash, Aave processed $429M total liquidations with zero bad debt. cbBTC pool specifically has never experienced bad debt. WBTC pool (comparable variant, same protocol) also has zero lender losses in 8+ year history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P3] [Aavescan cbBTC](https://aavescan.com/ethereum-v3/cbbtc) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Chaos Labs and LlamaRisk provide continuous quantitative risk analysis. cbBTC-specific parameters actively managed. Supply cap increased progressively from 450 to 32,000 based on demand. E-Mode for cbBTC/WBTC enables capital-efficient BTC-to-BTC borrowing. Over 1,100 automated parameter updates since late 2024 across all assets. | 9 | 9 | Non-Improvable (optimal) | [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters), [P2] [cbBTC Supply Cap Increase](https://governance.aave.com/t/arfc-increase-cbbtc-supply-caps-on-aave-v3-ethereum-market-and-base/19304) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | cbBTC supply yield is effectively 0% due to very low utilization (~1.01%). Average 1-year supply APR is 0.01%. 100% organic -- no emissions or incentives. Most cbBTC depositors use the pool for collateral purposes (borrowing against cbBTC), not for yield. Sustainable but economically marginal for yield-seekers. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan cbBTC](https://aavescan.com/ethereum-v3/cbbtc) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes. cbBTC utilization is only ~1.01%, meaning ~99% of supplied cbBTC is immediately available for withdrawal. Far better than WBTC (~2.5%) or WETH (~90%). Withdrawal is direct from Pool contract (1:1 redemption of aEthcbBTC to cbBTC). No slippage on in-protocol withdrawals. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan cbBTC](https://aavescan.com/ethereum-v3/cbbtc), [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Minimal. Core cbBTC lending yield is pure interest from overcollateralized borrower demand. No basis trade or funding rate dependency. cbBTC relies on maintaining 1:1 BTC backing via Coinbase custody. If custody failed, cbBTC would depeg -- but critically, the Aave BTC/USD oracle would NOT reflect this depeg (unlike WBTC's dual-feed oracle). Core yield does not depend on peg maintenance. | 9 | 9 | Non-Improvable (optimal) | [P0] [cbBTC Oracle](https://etherscan.io/address/0xb41E773f507F7a7EA890b1afB7d2b660c30C8B0A), [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | N/A -- Aave is a base-layer lending protocol where users deposit directly, not via a curator/allocator layer. No automated allocation mechanisms. | N/A | N/A | N/A | - |

**Protocol Mechanics Subtotal: 41.7/45 (92.6%)**
- 8 questions at score 9 = 72, 1 question at score 3 = 3, 1 question N/A
- Raw: 75/81, Weighted: (75/81) x 45 = 41.667 = 41.7

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | cbBTC pool: borrowers supply collateral from the full Aave Core Market asset set. For cbBTC suppliers, the key asset IS cbBTC itself -- Coinbase Wrapped BTC, an ERC-20 backed 1:1 by BTC held in Coinbase custody. BTC is a large-cap established asset. However, cbBTC carries custodial/centralization risk (single custodian with freeze capability). Aave governance set cbBTC parameters matching WBTC: LTV 73%, liquidation threshold 78%. Other collateral includes ETH LSTs, stablecoins, all with tiered on-chain LTVs. | 9 | 9 | Non-Improvable (optimal) | [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters), [P2] [cbBTC Listing ARFC](https://governance.aave.com/t/arfc-onboard-cbbtc-to-aave-v3-on-base-and-mainnet/18988) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | cbBTC has maintained a tight peg to BTC since launch (Sept 2024). No depeg >2% lasting >24 hours in the last 12 months. During Feb 2026 crash (BTC fell to ~$60K), cbBTC tracked BTC closely. Chainlink cbBTC PoR (since May 2025) independently verifies 1:1 BTC backing. cbBTC has ~18 months of peg history -- shorter than WBTC (6+ years) but no incidents. | 9 | 9 | Non-Improvable (optimal) | [P1] [Chainlink cbBTC PoR](https://data.chain.link/feeds/ethereum/mainnet/cbbtc-por), [P3] [Aavescan cbBTC](https://aavescan.com/ethereum-v3/cbbtc) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- cbBTC is not a staking-based collateral. It is a wrapped BTC token backed 1:1 by BTC in Coinbase custody. No validator or slashing risk. | N/A | N/A | N/A | - |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | **100% for cbBTC pool specifically.** cbBTC itself IS a wrapped asset (BTC wrapped via Coinbase custody into an ERC-20 token using FiatTokenProxy pattern). The entire $1.78B cbBTC supply in this pool relies on cbBTC's 1:1 BTC backing via Coinbase custody. Unlike WBTC which has Chainlink PoR integrated into its Aave oracle via a dual WBTC/BTC + BTC/USD feed, cbBTC's Aave oracle uses plain BTC/USD, meaning the oracle would NOT detect a cbBTC depeg. Chainlink PoR exists separately but is not oracle-integrated. | 1 | 1 | Non-Improvable | [P0] [cbBTC Oracle (BTC/USD)](https://etherscan.io/address/0xb41E773f507F7a7EA890b1afB7d2b660c30C8B0A), [P1] [Chainlink cbBTC PoR](https://data.chain.link/feeds/ethereum/mainnet/cbbtc-por), [P0] [cbBTC FiatTokenProxy](https://etherscan.io/address/0xcbb7c0000ab88b473b1f5afd9ef808440eed33bf) |

**Collateral Subtotal: 31.7/45 (70.4%)**
- 2 questions at score 9 = 18, 1 question at score 1 = 1, 1 question N/A
- Raw: 19/27, Weighted: (19/27) x 45 = 31.667 = 31.7

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum (Tier-0 chain). Chainlink BTC/USD price feed (Tier-0 oracle) at 0xb41E773f507F7a7EA890b1afB7d2b660c30C8B0A. cbBTC depends on Coinbase custody for BTC backing. Chainlink PoR monitors cbBTC reserves (separate feed, not Aave-integrated). No bridge dependencies for Ethereum deployment. All critical infrastructure Tier-0/1. | 9 | 9 | Non-Improvable (optimal) | [P0] [cbBTC Oracle](https://etherscan.io/address/0xb41E773f507F7a7EA890b1afB7d2b660c30C8B0A), [P1] [Chainlink cbBTC/USD](https://data.chain.link/feeds/ethereum/mainnet/cbbtc-usd) |
| ST-IC-02 | How redundant are oracle and bridge setups, and can oracle values be corrected under abnormal conditions? | **cbBTC uses a plain BTC/USD oracle feed (EACAggregatorProxy), NOT a cbBTC/BTC dual feed.** Per the cbBTC listing ARFC, Chaos Labs recommended "pricing the asset using the BTC/USD market oracle" due to expected close tracking. This effectively assumes a hardcoded 1:1 cbBTC:BTC peg. If cbBTC depegs from BTC (e.g., Coinbase custody failure, regulatory freeze), the Aave oracle would continue pricing cbBTC at BTC/USD, allowing borrowers to extract value at stale prices. Chainlink PoR for cbBTC exists (since May 2025) but is a separate monitoring feed NOT integrated into Aave's pricing. Per framework: hardcoded oracle for deep-liquidity asset where material depeg is historically unprecedented = Mid(3). BTC is deep-liquidity but cbBTC is only ~18 months old with single-custodian risk. | 3 | 9 | **Improvable** | [P0] [cbBTC Oracle (BTC/USD proxy)](https://etherscan.io/address/0xb41E773f507F7a7EA890b1afB7d2b660c30C8B0A), [P2] [cbBTC Listing ARFC](https://governance.aave.com/t/arfc-onboard-cbbtc-to-aave-v3-on-base-and-mainnet/18988), [P1] [Chainlink cbBTC PoR](https://data.chain.link/feeds/ethereum/mainnet/cbbtc-por) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | **Unknown.** Chainlink has enterprise certifications. Coinbase holds SOC 2 Type II certification (publicly traded, regulated). Aave Labs and BGD Labs: no public SOC 2/ISO27001 documentation found. Chaos Labs: no public certification documentation. | 3 | 9 | **Source Missing** | [P1] [Aave Security](https://aave.com/security), [P1] [Coinbase Trust](https://www.coinbase.com/trust) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Highly resilient. Protocol operational through all major Ethereum events. Nov 2023: infrastructure responded within hours. Feb 2026: $429M record liquidations processed with zero bad debt. cbBTC oracle (BTC/USD) functioned correctly throughout all stress events (no cbBTC depeg occurred during these events). | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain-level halts >30 min in 12+ months. Tier-0 reliability. | 9 | 9 | Non-Improvable (optimal) | Ethereum Tier-0 status, public knowledge |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- cbBTC is not staking-based. No validator set backing cbBTC. | N/A | N/A | N/A | - |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- cbBTC has no validator set. | N/A | N/A | N/A | - |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No permanent blocks from single Aave infrastructure failure. Withdrawals are permissionless via Pool contract. cbBTC-specific risk: Coinbase could blacklist the Aave Pool contract address, blocking all cbBTC in the pool -- this is an external token-level risk, not an Aave SPOF. The Chainlink BTC/USD oracle has independent fallback and is battle-tested. | 9 | 9 | Non-Improvable (optimal) | [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P0] [cbBTC FiatTokenV2_1](https://etherscan.io/address/0x7458bfdc30034eb860b265e6068121d18fa5aa72) |

**Infrastructure Counterparty Subtotal: 35.0/45 (77.8%)**
- 4 questions at score 9 = 36, 2 questions at score 3 = 6, 2 questions N/A
- Raw: 42/54, Weighted: (42/54) x 45 = 35.0

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | None externally. User cbBTC deposits remain in Aave Pool V3 contract. No external deployment. Flash loans are atomic (same-block return). | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Yes. Protocol fees publicly visible on-chain. cbBTC reserve factor is 20%. 20% of cbBTC borrow interest goes to DAO treasury. DAO treasury managed by Karpatkey with transparent reporting. No undisclosed arrangements. | 9 | 9 | Non-Improvable (optimal) | [P2] [DAO Financial Reports](https://governance.aave.com/t/aave-dao-financial-reports-financial-metrics/5575), [P2] [cbBTC Listing ARFC](https://governance.aave.com/t/arfc-onboard-cbbtc-to-aave-v3-on-base-and-mainnet/18988) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. cbBTC has specific supply and borrow caps enforced on-chain. Supply cap: 32,000 cbBTC (currently 25.94K / 81% utilized). Caps actively managed by Chaos Labs Risk Stewards, progressively increased from initial 450 based on demand. E-Mode provides additional exposure limits. | 9 | 9 | Non-Improvable (optimal) | [P2] [cbBTC Supply Cap Increase](https://governance.aave.com/t/arfc-increase-cbbtc-supply-caps-on-aave-v3-ethereum-market-and-base/19304), [P3] [Aavescan cbBTC](https://aavescan.com/ethereum-v3/cbbtc) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Instant for available liquidity. cbBTC withdrawal is permissionless from Pool contract. With only ~1.01% utilization, ~99% of supplied cbBTC is immediately available. No withdrawal blocks in cbBTC pool history. cbBTC can then be redeemed for BTC through Coinbase (off-chain, separate from Aave). | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan cbBTC](https://aavescan.com/ethereum-v3/cbbtc), [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Yes. cbBTC custody: Coinbase (NASDAQ-listed, US-regulated, SOC 2 Type II certified). Coinbase is one of the most transparent crypto custodians with SEC reporting obligations. Chainlink oracle operators publicly disclosed. Chaos Labs and LlamaRisk publicly identified as risk providers. All third parties fully named. | 9 | 9 | Non-Improvable (optimal) | [P2] [cbBTC Listing ARFC](https://governance.aave.com/t/arfc-onboard-cbbtc-to-aave-v3-on-base-and-mainnet/18988), [P1] [Coinbase Trust](https://www.coinbase.com/trust) |

**Protocol Counterparty Subtotal: 45.0/45 (100.0%)**
- 5 questions x 9 = 45
- Raw: 45/45, Weighted: (45/45) x 45 = 45.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | All cbBTC withdrawals are permissionless via Pool V3 contract based on available liquidity. Guardians can pause in emergency (5-of-9 multisig) but pause is protocol-wide, not address-specific. No selective blocking capability within Aave. Note: Coinbase can blacklist addresses at the cbBTC token level, which could affect withdrawability of the token post-withdrawal. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Yes. Excellent liquidity. ~25.94K cbBTC supplied, only ~261 borrowed. ~25.68K cbBTC (~99% of TVL) immediately available for withdrawal. At 1.01% utilization, this pool has the highest available liquidity ratio of any Aave BTC pool. Can absorb >10% TVL withdrawals easily. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan cbBTC](https://aavescan.com/ethereum-v3/cbbtc), [P0] [aEthcbBTC](https://etherscan.io/address/0x5c647cE0Ae10658ec44FA4E11A51c96e94efd1Dd) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No cbBTC-specific withdrawal delays since listing (Sept 2024). The November 2023 security incident (pre-cbBTC listing) caused temporary asset freezes across all pools but was resolved within days. cbBTC pool has never experienced high-utilization withdrawal constraints. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan cbBTC](https://aavescan.com/ethereum-v3/cbbtc) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Supply cap (32,000 cbBTC) is above current supply (25.94K). Low borrow demand means caps do not restrict withdrawals. Interest rate model penalizes high utilization with higher borrow rates. No history of caps blocking cbBTC withdrawals. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan cbBTC](https://aavescan.com/ethereum-v3/cbbtc), [P2] [cbBTC Supply Cap Increase](https://governance.aave.com/t/arfc-increase-cbbtc-supply-caps-on-aave-v3-ethereum-market-and-base/19304) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | **Excellent for cbBTC.** At 1.01% utilization (compared to WETH's typical ~90%), cbBTC exits are structurally unconstrained. During Feb 2026 market crash, cbBTC pool maintained ample liquidity. The extremely low borrow demand means utilization spikes are structurally unlikely. Withdrawals remained functional throughout all historical stress events. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan cbBTC](https://aavescan.com/ethereum-v3/cbbtc), [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. cbBTC withdrawals are based on available pool liquidity only. No lockups, vesting, or unstaking delays. Instant withdrawal if liquidity available (which it consistently is at ~1% utilization). The only off-chain process is cbBTC-to-BTC redemption through Coinbase, which is separate from Aave withdrawal. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary cbBTC redemption through Pool contract is always available (subject to pool liquidity). aEthcbBTC tokens can be transferred but primary exit is direct protocol redemption. cbBTC itself has growing secondary market liquidity -- Coinbase exchange provides deep BTC liquidity for redemption. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P0] [aEthcbBTC](https://etherscan.io/address/0x5c647cE0Ae10658ec44FA4E11A51c96e94efd1Dd) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | cbBTC has ~$4.6B+ in total supply across chains (Ethereum: ~$1.1B in this Aave pool alone). cbBTC has growing DEX and Coinbase exchange liquidity. BTC itself is the most liquid crypto asset. aEthcbBTC is directly 1:1 redeemable from Pool. Can absorb >10% of pool TVL with low price impact under normal conditions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Chainlink cbBTC PoR](https://data.chain.link/feeds/ethereum/mainnet/cbbtc-por), [P0] [aEthcbBTC](https://etherscan.io/address/0x5c647cE0Ae10658ec44FA4E11A51c96e94efd1Dd) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | **Negligible for cbBTC.** At ~1.01% utilization, bank-run risk is structurally near-zero. Even if all borrowed cbBTC were not returned, only ~1% of supplied cbBTC would be temporarily inaccessible. Interest rate model would incentivize rapid repayment. Design, buffers, and extremely low utilization indicate mass exit would cause only temporary rate spikes without depositor haircuts. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan cbBTC](https://aavescan.com/ethereum-v3/cbbtc), [P2] [cbBTC Listing ARFC](https://governance.aave.com/t/arfc-onboard-cbbtc-to-aave-v3-on-base-and-mainnet/18988) |

**Liquidity Subtotal: 45.0/45 (100.0%)**
- 9 questions x 9 = 81
- Raw: 81/81, Weighted: (81/81) x 45 = 45.0

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | aEthcbBTC maintains 1:1 with underlying cbBTC by design (interest-bearing token, not a traded peg). No peg deviation possible as aEthcbBTC represents a claim on Pool liquidity plus accrued interest. The cbBTC/BTC peg has remained tight since launch (Sept 2024). During Feb 2026 crash, cbBTC tracked BTC closely. No sustained depeg incidents. However, cbBTC is newer (~18 months) with less stress history than WBTC (6+ years). | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan cbBTC](https://aavescan.com/ethereum-v3/cbbtc), [P1] [Chainlink cbBTC PoR](https://data.chain.link/feeds/ethereum/mainnet/cbbtc-por) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Low for cbBTC lenders. Overcollateralized design protects suppliers. Borrowers face liquidation risk, not lenders. Feb 2026: $429M in total protocol liquidations with zero bad debt. Conservative parameters (73% LTV, 78% liquidation threshold). No leverage for suppliers. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P2] [cbBTC Listing ARFC](https://governance.aave.com/t/arfc-onboard-cbbtc-to-aave-v3-on-base-and-mainnet/18988) |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Two-slope interest rate model with optimal utilization kink at 45% (lower than most assets, reflecting conservative cbBTC risk posture). cbBTC utilization (~1.01%) is far below the kink. Variable Slope2 at 300% would dramatically increase rates above optimal. No history of cbBTC reaching the rate curve kink. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan cbBTC](https://aavescan.com/ethereum-v3/cbbtc), [P2] [cbBTC Listing ARFC](https://governance.aave.com/t/arfc-onboard-cbbtc-to-aave-v3-on-base-and-mainnet/18988) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. Chaos Labs and LlamaRisk provide continuous stress testing. cbBTC parameters modeled from inception with WBTC as precedent. Feb 2026: real-world stress test passed ($429M protocol-wide liquidations). cbBTC/WBTC E-Mode stress analysis performed before activation. Formal verification by Certora validates protocol invariants. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P2] [cbBTC/WBTC E-Mode](https://governance.aave.com/t/arfc-enable-cbbtc-wbtc-liquid-e-mode-on-aave-v3-mainnet/19705) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | For cbBTC borrowers: yes (design intent, protects lenders). For cbBTC lenders/suppliers: no, protected by overcollateralization. Conservative parameters (73% LTV, 78% threshold, 7.5% penalty) provide substantial buffer. Protocol has processed $429M+ liquidations without lender losses. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P2] [cbBTC Listing ARFC](https://governance.aave.com/t/arfc-onboard-cbbtc-to-aave-v3-on-base-and-mainnet/18988) |

**Market Subtotal: 45.0/45 (100.0%)**
- 5 questions x 9 = 45
- Raw: 45/45, Weighted: (45/45) x 45 = 45.0

---

### **Strategy Total: 41.7 + 31.7 + 35.0 + 45.0 + 45.0 + 45.0 = 243.4/270 (90.1%)**

Note: 41.667 + 31.667 + 35.0 + 45.0 + 45.0 + 45.0 = 243.334; rounded subcategory sums = 243.4

---

### OPERATIONS (30% Weight) - Score: 256.0/270 (94.8%)

**NOTE: All Operations scores are IDENTICAL to other Aave Ethereum V3 Core Market ratings per Platform Consistency requirement. Same governance, same team, same documentation, same financial resilience.**

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | On-chain DAO governance via AAVE, stkAAVE, aAAVE token voting. Structured proposal process: Temp Check (Snapshot) -> ARFC (forum) -> AIP (on-chain vote). Cross-chain voting via storage proofs. Risk Stewards (Chaos Labs) handle parameter adjustments within governance-approved bounds. Two 5-of-9 Guardian multisigs provide emergency controls. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [Aave Governance Forum](https://governance.aave.com/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | Moderate concentration typical of large DAOs. "Aave Will Win" Temp Check passed with 52.58% -- narrow margin with self-voting allegations. ACI exit and BGD Labs departure reduce delegate diversity. However: two 5-of-9 Guardian multisigs, Risk Steward system, structured proposal process provide checks. | 9 | 9 | Non-Improvable (optimal) | [P4] [Aave Will Win Vote](https://www.theblock.co/post/391693/aave-proposal-clears-temp-check-vote), [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. 1-day standard timelock, 7-day for critical changes. Two Guardian multisigs (5-of-9 each) with veto powers. Structured proposal process. Certora reviews all governance proposals for security. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A -- Aave has no "strategy manager" in the vault sense. Risk providers can be changed via governance without any impact on user withdrawals. cbBTC withdrawals are always permissionless. | N/A | N/A | N/A | - |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 3 questions at score 9 = 27, 1 question N/A
- Raw: 27/27, Weighted: (27/27) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Aave Labs (London, UK) led by Stani Kulechov. Aave SAGL (Swiss entity, Zug). Chaos Labs (risk management), LlamaRisk (risk analysis), Karpatkey (treasury). All publicly identified with verifiable track records. | 9 | 9 | Non-Improvable (optimal) | [P3] [Tracxn](https://tracxn.com/d/companies/aave/__JiXfiPZKVkx7021dCR937XH3M5d2vj-Cy3z3dnIPJ00) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Multiple independent teams: Aave Labs, BGD Labs, other contributors. However, BGD Labs (V3 codebase maintainer) announced departure effective April 2026, and ACI (61% of governance actions) exited March 3, 2026. While Aave Labs remains and a 2-month security retainer covers incident response through June 2026, the simultaneous loss creates transition risk. Despite this, the protocol has sufficient team depth. | 9 | 9 | Non-Improvable (optimal) | [P2] [BGD Leaving Aave](https://governance.aave.com/t/bgd-leaving-aave/24122), [P4] [ACI Exit](https://thedefiant.io/news/defi/aave-chan-initiative-announces-exit-from-aave-dao-amid-governance-rift) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Aave SAGL (Swiss entity, Zug). Aave Labs based in London, UK. DAO structure with decentralized governance. Multiple jurisdictional presence. Clear legal entity mapping. | 9 | 9 | Non-Improvable (optimal) | [P3] [Tracxn](https://tracxn.com/d/companies/aave/__JiXfiPZKVkx7021dCR937XH3M5d2vj-Cy3z3dnIPJ00) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | **CLEARED.** SEC closed 4-year investigation December 16, 2025 without enforcement action. No charges, fines, or further action. No ongoing enforcement in major jurisdictions. | 9 | 9 | Non-Improvable (optimal) | [P4] [Yahoo Finance](https://finance.yahoo.com/news/sec-closes-4-long-investigation-091715487.html) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Yes. March 2026 CAPO incident: borrow caps reduced within hours, post-mortem within 1 day. Nov 2023: pools secured within hours. Feb 2026: Chaos Labs adjusted parameters in real-time during market crash. Multiple demonstrated instances of rapid response. | 9 | 9 | Non-Improvable (optimal) | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. CAPO incident: post-mortem within 1 day, reimbursement proposal within 2 days. Active governance forum with prompt responses. Regular development updates from Aave Labs. | 9 | 9 | Non-Improvable (optimal) | [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. $29.5M raised from 41 investors including Standard Crypto, Blockchain Coinvestors, ParaFi, Framework Ventures. Service providers all publicly disclosed with governance-approved mandates. | 9 | 9 | Non-Improvable (optimal) | [P3] [Tracxn](https://tracxn.com/d/companies/aave/__JiXfiPZKVkx7021dCR937XH3M5d2vj-Cy3z3dnIPJ00/funding-and-investors) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | **Significant governance tension.** Dec 2025: DAO-Labs conflict over CowSwap fees. Feb 2026: "Aave Will Win" proposal passed Temp Check with narrow 52.58% margin with self-voting allegations. ACI exit March 3, 2026. BGD Labs departure effective April 2026. Both major service providers leaving citing governance tensions. | 3 | 9 | **Improvable** | [P2] [BGD Leaving Aave](https://governance.aave.com/t/bgd-leaving-aave/24122), [P4] [ACI Exit](https://thedefiant.io/news/defi/aave-chan-initiative-announces-exit-from-aave-dao-amid-governance-rift) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | No permanent uncompensated losses to cbBTC lenders. March 2026 CAPO incident caused wstETH liquidations (NOT cbBTC), with 100% reimbursement committed. Feb 2026: $429M record liquidations processed without bad debt. 8+ year track record without permanent depositor principal loss. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |

**Team & Legal Subtotal: 62.5/67.5 (92.6%)**
- 8 questions at score 9 = 72
- 1 question at score 3 = 3
- Raw: 75/81, Weighted: (75/81) x 67.5 = 62.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive documentation covering V3 architecture, smart contracts, risk parameters, governance. Updated through V3.6 (Nov 2025). Risks page covers liquidation, oracle, smart contract risks. cbBTC listing ARFC provides detailed risk analysis specific to cbBTC. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Docs](https://aave.com/docs/aave-v3/overview), [P1] [Risks](https://aave.com/docs/resources/risks) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Detailed documentation: health factor, liquidation process, bad debt scenarios, interest rate models. cbBTC-specific: LTV 73%, liquidation threshold 78%, liquidation penalty 7.5%, reserve factor 20% all documented. Loss conditions clearly explained. | 9 | 9 | Non-Improvable (optimal) | [P1] [Health Factor & Liquidations](https://aave.com/help/borrowing/liquidations), [P1] [Risks](https://aave.com/docs/resources/risks) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Pool V3: 0x87870Bca3F3fD6335C3F4ce8392D69350B4fA4E2. aEthcbBTC: 0x5c647cE0Ae10658ec44FA4E11A51c96e94efd1Dd. cbBTC Oracle: 0xb41E773f507F7a7EA890b1afB7d2b660c30C8B0A. BGD Address Book GitHub repo provides canonical registry. All verified on Etherscan. | 9 | 9 | Non-Improvable (optimal) | [P1] [BGD Address Book](https://github.com/bgd-labs/aave-address-book), [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Guardian roles, timelock durations (1-day standard, 7-day critical), Risk Steward permissions, proposal process all documented. cbBTC parameter changes (supply cap increases) documented in governance forum with full change history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [cbBTC Supply Cap Increase](https://governance.aave.com/t/arfc-increase-cbbtc-supply-caps-on-aave-v3-ethereum-market-and-base/19304) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full on-chain transparency. All cbBTC pool balances verifiable on Etherscan via Pool V3 contract. aEthcbBTC supply (25.94K cbBTC) verifiable on-chain. cbBTC itself has Chainlink Proof of Reserve (since May 2025) monitoring BTC backing across chains. Proof-of-liabilities: outstanding borrows (~261 cbBTC) verifiable via variableDebtcbBTC token. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P0] [aEthcbBTC](https://etherscan.io/address/0x5c647cE0Ae10658ec44FA4E11A51c96e94efd1Dd), [P1] [Chainlink cbBTC PoR](https://data.chain.link/feeds/ethereum/mainnet/cbbtc-por) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. All core contracts verified on Etherscan: Pool V3, PoolConfigurator, aEthcbBTC, variableDebtcbBTC, cbBTC Oracle, cbBTC token (FiatTokenProxy + FiatTokenV2_1 implementation). Full source code readable. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2#code), [P0] [Etherscan aEthcbBTC](https://etherscan.io/address/0x5c647cE0Ae10658ec44FA4E11A51c96e94efd1Dd), [P0] [cbBTC FiatTokenProxy](https://etherscan.io/address/0xcbb7c0000ab88b473b1f5afd9ef808440eed33bf) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions x 9 = 54
- Raw: 54/54, Weighted: (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Yes. Umbrella Safety Module launched June 2025 with ~$263M in staked assets. Automated slashing mechanism for bad debt. DAO Treasury (~$125M) separate. March 2026 CAPO incident: DAO committed to full user reimbursement, demonstrating willingness to compensate. | 9 | 9 | Non-Improvable (optimal) | [P1] [Umbrella Docs](https://aave.com/docs/aave-v3/umbrella), [P2] [BGD Umbrella](https://governance.aave.com/t/bgd-aave-safety-module-umbrella/18366) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | **Modest relative to scale.** Umbrella ~$263M + DAO Treasury ~$125M = ~$388M vs $34.5B Ethereum TVL = ~1.1%. Below the 5% threshold for Low Risk, within 1-5% range = Mid Risk. DAO Treasury requires governance vote to deploy for user losses. Feb 2026: protocol processed $429M liquidations with zero bad debt, suggesting current buffers sufficient for historical stress. | 3 | 9 | **Improvable** | [P2] [DAO Funding Insights](https://governance.aave.com/t/aave-dao-funding-insights/24192), [P2] [LlamaRisk Umbrella Coverage](https://governance.aave.com/t/llamarisk-insights-umbrella-coverage-principles-and-slashing-logic/23527) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. DAO Treasury ~$125M. Protocol generated $885M in fees in 2025. $50M/year AAVE buyback approved. Revenue covers expenses; reserves provide additional buffer. Runway >24 months. | 9 | 9 | Non-Improvable (optimal) | [P2] [DAO Funding Insights](https://governance.aave.com/t/aave-dao-funding-insights/24192), [P3] [DeFiLlama Aave](https://defillama.com/protocol/aave) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Highly resilient. Feb 2026: $429M record liquidations during 30-40% crypto crash, zero bad debt. Survived 2022 bear market (FTX, Terra/Luna, SVB). March 2026 CAPO cost ~$580K-$900K, easily absorbed. cbBTC pool specifically has never experienced bad debt or buffer depletion. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P3] [DeFiLlama Aave](https://defillama.com/protocol/aave) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Smart contracts are permissionless and non-custodial. cbBTC withdrawals always available via direct Pool contract interaction based on available liquidity. Governance via on-chain voting (no off-chain dependency). | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |

**Financial Resilience Subtotal: 58.5/67.5 (86.7%)**
- 4 questions at score 9 = 36, 1 question at score 3 = 3
- Raw: 39/45, Weighted: (39/45) x 67.5 = 58.5

**Operations Total: 67.5 + 62.5 + 67.5 + 58.5 = 256.0/270 (94.8%)**

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 99 | 99 | 180.0 | 180 | 100.0% |
| | Key Management (6 of 8 Q scored) | 57 | 63 | 162.9 | 180 | 90.5% |
| | **Security Subtotal** | | | **342.9** | **360** | **95.3%** |
| **Strategy** | Protocol Mechanics (8 of 10 Q scored) | 75 | 81 | 41.7 | 45 | 92.6% |
| | Collateral (3 of 4 Q scored) | 19 | 27 | 31.7 | 45 | 70.4% |
| | Infra Counterparty (6 of 8 Q scored) | 42 | 54 | 35.0 | 45 | 77.8% |
| | Protocol Counterparty (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity (9 Q) | 81 | 81 | 45.0 | 45 | 100.0% |
| | Market (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | **Strategy Subtotal** | | | **243.4** | **270** | **90.1%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 75 | 81 | 62.5 | 67.5 | 92.6% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 39 | 45 | 58.5 | 67.5 | 86.7% |
| | **Operations Subtotal** | | | **256.0** | **270** | **94.8%** |
| **TOTAL** | | | | **842.3** | **900** | **93.6%** |

---

