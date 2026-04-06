# Aave - EURe (Gnosis V3 Market) Risk Rating

**Rating Date**: 2026-04-03
**Final Grade**: BB+
**Total Score**: 794.0/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-beta

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 342.9/360 (95.2%)

**NOTE: All Security scores are IDENTICAL to other Aave V3 ratings for platform-level questions. The Aave V3 codebase deployed on Gnosis is the same audited code. However, EURe token-specific and Gnosis chain-specific factors are reflected in Strategy and Operations.**

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 30+ Aave V3 audits from Tier-0/1 firms: OpenZeppelin, Trail of Bits, Sigma Prime, Certora, PeckShield, MixBytes, Pashov, Sherlock, Oxorio, StErMi. EURe V2 token audited by Ackee Blockchain Security (18 findings, none critical/high, all remediated). All reports public. Gnosis Pool V3 (0xb502...) deployed Oct 2023, verified on GnosisScan. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P0] [GnosisScan Pool V3](https://gnosisscan.io/address/0xb50201558B00496A145fE76f7424749556E326D8), [P1] [Ackee Audit](https://github.com/monerium/smart-contracts/blob/main/audits/v2.0.0-ackee-blockchain-monerium-smart-contracts-report-1.2.pdf) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | V3.4 (June 2025): Certora (Tier-0), StErMi. V3.3 (Jan 2025): Certora (Tier-0), Sherlock (Tier-0), Oxorio, StErMi. EURe V2: Ackee Blockchain Security (Tier-1). Multiple Tier-0 auditors on latest Aave versions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [Ackee Audit Summary](https://ackee.xyz/blog/monerium-audit-summary/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Every major Aave V3 version (V3.0 through V3.6) audited. EURe V1->V2 migration audited by Ackee. Gnosis deployment uses same audited codebase as Ethereum. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [Monerium V2 Docs](https://monerium.dev/docs/contracts-v2) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. Ackee EURe V2 audit: 18 findings (info to medium), all remediated. Multi-sig upgraded from 2/6 to 3/6 per audit recommendation. Aave findings tracked with remediation across all versions. Certora formal verification validates invariants. | 9 | 9 | Non-Improvable (optimal) | [P1] [Ackee Audit Summary](https://ackee.xyz/blog/monerium-audit-summary/), [P1] [Aave Security](https://aave.com/security) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Aave Pool V3 upgradeable via transparent proxy pattern managed through PoolAddressesProvider (0x3661...). Upgrades require DAO governance vote + timelock execution. EURe V2 token is ERC-1967 proxy (0x420C...) upgradeable by Monerium admin (Gnosis Safe multisig 3/6). Two separate upgrade authorities: Aave governance for protocol, Monerium for token. Aave upgrades well-constrained; EURe token upgrades are issuer-controlled. | 9 | 9 | Non-Improvable (optimal) | [P0] [GnosisScan Pool V3](https://gnosisscan.io/address/0xb50201558B00496A145fE76f7424749556E326D8), [P0] [GnosisScan EURe V2](https://gnosisscan.io/address/0x420CA0f9B9b604cE0fd9C18EF134C705e5Fa3430) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No user fund losses in Aave protocol history or EURe Gnosis pool. Nov 2023: Aave stable rate vulnerability patched before exploitation. Aug 2024: Periphery contract tip jar ($56K, not user deposits). March 2026: CAPO incident affected wstETH on Ethereum only -- EURe Gnosis unaffected. Nov 2025: Balancer exploit on Gnosis required EURe freeze by Monerium but Aave pools were not impacted. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Post-Mortem](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P4] [Gnosis Balancer Response](https://x.com/gnosisdotio/status/1985321081255891396) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Aave founded by Stani Kulechov in 2017 (ETHLend). 8+ year track record. Monerium founded 2016 by team with central banking and fintech backgrounds. Both entities publicly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [Monerium Team](https://monerium.com/team/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. Standard proposals maintain 1-day delay, critical changes require 7-day delay. Governance V3 introduced cross-chain voting via storage proofs. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Immunefi bounty up to $1M for critical vulnerabilities. Aave V3 Gnosis explicitly in scope with all severity levels (Critical, High, Medium). 83+ assets in scope including AaveV3Gnosis.sol and GovernanceV3Gnosis.sol. | 9 | 9 | Non-Improvable (optimal) | [P1] [Immunefi Aave Scope](https://immunefi.com/bug-bounty/aave/scope/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. BGD Labs provides continuous monitoring. Chaos Labs operates Risk Stewards with 1,100+ automated risk parameter adjustments. Slope2 Risk Oracle provides automated interest rate response. DDoS protection, DNSSEC, intrusion detection documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P2] [Chaos Labs Slope2 Oracle](https://chaoslabs.xyz/posts/introducing-the-aave-slope2-risk-oracle) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Yes. Protocol Emergency Guardian (5-of-9) can pause markets including Gnosis. V3.3 bad debt verification prevents new bad debt post-liquidation. Slope2 Risk Oracle automatically adjusts borrow rates during high utilization. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Features](https://github.com/aave-dao/aave-v3-origin/blob/main/docs/3.3/Aave-v3.3-features.md) |

**Smart Contract Security Subtotal: 180.0/180 (100.0%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | DAO governance via AAVE/stkAAVE/aAAVE token voting. All changes require on-chain vote with quorum, then timelock execution. Cross-chain governance executes on Gnosis via bridge executor. Protocol Emergency Guardian (5-of-9) and Governance Emergency Guardian (5-of-9) provide emergency controls. Risk Stewards (Chaos Labs) adjust parameters within governance-approved bounds. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [GnosisScan ACLManager](https://gnosisscan.io/address/0xEc710f59005f48703908bC519D552Df5B8472614) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Aave requires DAO vote + timelock execution. Guardians can only pause/veto, not move funds or upgrade custody. EURe token issuer (Monerium) has freeze/blacklist capability via 3/6 multisig but cannot move user funds from Aave Pool. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [GnosisScan Pool V3](https://gnosisscan.io/address/0xb50201558B00496A145fE76f7424749556E326D8) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Protocol Emergency Guardian: 5-of-9 (Chaos Labs, LlamaRisk, Karpatkey, TokenLogic, Certora, BGD Labs, ACI, 2 DAO delegates). Governance Emergency Guardian: 5-of-9 (Zapper, ParaSwap, Standard Crypto, DeFi Saver, Balancer, Chainlink, Lido, security firms). Diverse set of independent entities across both multisigs. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [Guardian Renewal](https://governance.aave.com/t/arfc-renewal-of-aave-guardian-2024/17523) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Aave: Pause limited to Guardians via 5-of-9 multisig. No address-level blocking by Aave. Withdrawals permissionless via Pool contract. However, EURe token itself has address-level freeze/blacklist controlled by Monerium (3/6 multisig). Nov 2025: Monerium froze ~EUR 1.3M in EURe during Balancer exploit response. This freeze power exists at the token level, not at the Aave protocol level. Aave cannot selectively block. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P1] [Monerium Token Design](https://github.com/monerium/smart-contracts/blob/main/docs/tokendesign.md) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user EURe deposits held in Aave Pool V3 contract (0xb502...) on Gnosis. Permissionless supply/withdraw via smart contract. aGnoEURe tokens (0xEdBC...) represent user positions. | 9 | 9 | Non-Improvable (optimal) | [P0] [GnosisScan Pool V3](https://gnosisscan.io/address/0xb50201558B00496A145fE76f7424749556E326D8), [P0] [GnosisScan aEURe](https://gnosisscan.io/address/0xEdBC7449a9b594CA4E053D9737EC5Dc4CbCcBfb2) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation: Pool V3 contract holds all user funds. DAO treasury managed separately by Karpatkey. No co-mingling of user deposits with treasury operations. | 9 | 9 | Non-Improvable (optimal) | [P0] [GnosisScan Pool V3](https://gnosisscan.io/address/0xb50201558B00496A145fE76f7424749556E326D8) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- Aave is a lending protocol, not a vault. Users deposit assets directly to pools. No external protocol routing of user funds. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | **Partial.** November 2023 incident demonstrated rapid emergency response (pools secured within hours). Feb 2026: Risk Stewards adjusted parameters in real-time. Nov 2025: Gnosis Balancer response demonstrated cross-ecosystem coordination (Monerium freeze + Gnosis soft fork). However, no comprehensive public playbook for key rotation or signer replacement procedures is documented. | 3 | 9 | **Improvable** | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335) |

**Key Management Subtotal: 162.9/180 (90.5%)**
- 6 questions at score 9 = 54 points
- 1 question at score 3 = 3 points
- 1 question N/A (S-KM-07)
- Raw: 57/63, Weighted: (57/63) x 180 = 162.857 = 162.9

---

### **Security Total: 342.9/360 (95.2%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 180.0 | 180 | 100.0% |
| Key Management | 162.9 | 180 | 90.5% |
| **Security Total** | **342.9** | **360** | **95.2%** |

---

### STRATEGY (30% Weight) -- Score: 195.1/270 (72.3%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yes. All EURe supply yield comes from overcollateralized borrower interest. EURe borrowers post collateral from the Gnosis market asset set (WETH, wstETH, GNO, USDC, sDAI). Supply APY ~3.50% at ~82.9% utilization, 100% organic from borrower demand. No emissions dependency. EURe reserve factor reduced from 20% to 10% in Dec 2024 governance proposal to incentivize supply. | 9 | 9 | Non-Improvable (optimal) | [P3] [Vaults.fyi](https://app.vaults.fyi/opportunity/gnosis/0xEdBC7449a9b594CA4E053D9737EC5Dc4CbCcBfb2), [P2] [Gnosis Instance Updates](https://governance.aave.com/t/arfc-aave-v3-gnosis-instance-updates/20334) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Negative yield or principal loss can occur in severe but plausible scenarios: (1) Bad debt from cascading liquidations; (2) Smart contract exploit; (3) Oracle manipulation; (4) EURe issuer risk -- Monerium can freeze/blacklist addresses (demonstrated Nov 2025 during Balancer exploit); (5) EUR/USD FX risk for non-EUR allocators; (6) Gnosis chain risk (hard fork precedent Dec 2025); (7) Monerium is a smaller issuer than Circle (~$28-32M total market cap vs EURC's ~$450M), with a 7-person core team. EURe is backed 100% (102% overcollateralized) by euro reserves per Monerium. | 3 | 3 | Non-Improvable | [P1] [Monerium EURe](https://monerium.com/eure/), [P4] [Gnosis Hard Fork](https://unchainedcrypto.com/gnosis-completes-hard-fork-to-recover-balancer-exploit-funds/) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No protocol-level leverage or rehypothecation. User deposits remain in the Pool contract. Protocol maintains overcollateralized 1:1 backing. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | Yes. Interest rate model with steep slope2 (50% at Gnosis, per governance proposals). V3.3 bad debt verification prevents new bad debt post-liquidation. 100% close factor below 0.95 health factor. Current utilization at ~82.9% is below optimal utilization. Risk Stewards actively manage EURe parameters. | 9 | 9 | Non-Improvable (optimal) | [P2] [Gnosis Instance Updates](https://governance.aave.com/t/arfc-aave-v3-gnosis-instance-updates/20334), [P1] [Aave V3 Features](https://github.com/aave-dao/aave-v3-origin/blob/main/docs/3.3/Aave-v3.3-features.md) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent losses to EURe lenders on Gnosis. Aave V3 stablecoin lending (directly comparable variant -- same codebase, same risk mechanics) has 8+ year track record without depositor principal loss across all chains. Feb 2025: $210M liquidations, zero bad debt. Feb 2026: $429M record liquidations, zero bad debt. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Chaos Labs and LlamaRisk provide continuous risk analysis. EURe-specific parameters on Gnosis: reserve factor 10% (reduced from 20%), LTV/LT parameters set at activation. Cap increases tracked via Risk Stewards governance. LlamaRisk and Chaos Labs both provided risk assessments for Gnosis instance updates. | 9 | 9 | Non-Improvable (optimal) | [P2] [Gnosis Instance Updates](https://governance.aave.com/t/arfc-aave-v3-gnosis-instance-updates/20334), [P2] [Gnosis Enhancements](https://governance.aave.com/t/arfc-enhancements-in-aave-v3-gnosis-chain-instance/21214) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. EURe supply APY (~3.50%) is 100% organic from borrower demand. No emissions required. Borrowing demand driven by EUR-denominated leverage on Gnosis (Gnosis Pay integration driving real-world EUR payment use cases). Revenue sustainable without incentive dependency. Higher yield than Ethereum EURC (~1.70%) reflects higher Gnosis utilization (~82.9% vs ~55.66%). | 9 | 9 | Non-Improvable (optimal) | [P3] [Vaults.fyi](https://app.vaults.fyi/opportunity/gnosis/0xEdBC7449a9b594CA4E053D9737EC5Dc4CbCcBfb2) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Under normal conditions, withdrawal is direct from Pool contract. Available liquidity ~2.7M EURe at ~82.9% utilization ($3.13M) -- only ~17% of supplied TVL is immediately available. For in-protocol exit, rate model incentivizes repayment. However, EURe secondary market liquidity on Gnosis is extremely thin post-Balancer exploit. Converting EURe to other assets or bridging to Ethereum adds friction. For positions >$1M, material slippage risk exists. | 3 | 3 | Non-Improvable | [P3] [Vaults.fyi](https://app.vaults.fyi/opportunity/gnosis/0xEdBC7449a9b594CA4E053D9737EC5Dc4CbCcBfb2) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | EURe lending yield is pure interest from overcollateralized borrower demand. No basis trade or funding rate dependency. EURe borrowing demand partially depends on EUR/USD carry trade dynamics and Gnosis Pay adoption. EUR/USD FX peg dependency exists but EURe maintains robust 1:1 EUR peg. | 9 | 9 | Non-Improvable (optimal) | [P1] [Monerium EURe](https://monerium.com/eure/) |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | N/A -- Aave is a base-layer lending protocol where users deposit directly. No curator/allocator layer. All deposits are user-initiated. | N/A | N/A | N/A | - |

**Protocol Mechanics Subtotal: 38.3/45 (85.2%)**
- 7 questions at score 9 = 63 points
- 2 questions at score 3 = 6 points
- 1 question N/A (ST-PM-10)
- Raw: 69/81, Weighted: (69/81) x 45 = 38.333 = 38.3

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Gnosis Aave V3 collateral set: WETH, wstETH, GNO, USDC (deprecated, caps reduced), USDC.e, wXDAI, sDAI, EURe, osGNO. Assets are established but Gnosis-specific (GNO, osGNO are Gnosis native tokens with moderate liquidity). USDC deprecated with LTV reduced to 65%. E-Mode categories provide risk tiering. sDAI/EURe E-Mode proposed (85% LTV). Overall collateral is reasonable but includes some mid-tier assets (GNO: 80% 30-day volatility per governance). | 3 | 3 | Non-Improvable | [P2] [Gnosis Enhancements](https://governance.aave.com/t/arfc-enhancements-in-aave-v3-gnosis-chain-instance/21214), [P2] [Gnosis Instance Updates](https://governance.aave.com/t/arfc-aave-v3-gnosis-instance-updates/20334) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | Major collaterals (WETH, wstETH) maintained pegs through stress events. sDAI maintained 1:1 with DAI. GNO experienced moderate volatility (80.46% 30-day annualized per governance data) but maintained exchange rate. EURe itself maintained EUR peg. Nov 2025 Balancer exploit caused temporary EURe pool freezes but not depegs. No documented depeg >2% lasting >24h for any collateral in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P2] [Gnosis Instance Updates](https://governance.aave.com/t/arfc-aave-v3-gnosis-instance-updates/20334) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | wstETH collateral backed by Lido (600+ operators). osGNO backed by StakeWise V3 on Gnosis validators. Gnosis chain has 300,000+ validators distributed across 70 countries. Conservative LTVs account for slashing risk. Risk is immaterial to EURe lenders as it only affects borrower collateral value. | 9 | 9 | Non-Improvable (optimal) | [P2] [osGNO Onboarding](https://governance.aave.com/t/arfc-onboard-osgno-to-aave-v3-gnosis-instance/22033) |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | EURe on Gnosis is natively issued by Monerium on Gnosis chain (V1: 0xcB44..., V2: 0x420C...) -- not bridged. However, WETH on Gnosis is bridged from Ethereum via Gnosis bridge. wstETH on Gnosis is also bridged. USDC.e is bridged. sDAI requires the bridge-mediated sDAI vault. Significant portion of the broader Gnosis Aave collateral relies on bridged assets (>60% likely when including WETH, wstETH, USDC.e). For the EURe deposit itself: EURe is native. Collateral backing borrows is partially bridged. | 3 | 3 | Non-Improvable | [P0] [GnosisScan EURe V1](https://gnosisscan.io/address/0xcb444e90d8198415266c6a2724b7900fb12fc56e), [P1] [Gnosis Bridges](https://docs.gnosischain.com/bridges/) |

**Collateral Subtotal: 30.0/45 (66.7%)**
- 2 questions at score 9 = 18 points
- 2 questions at score 3 = 6 points
- Raw: 24/36, Weighted: (24/36) x 45 = 30.0

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Gnosis Chain (Tier-2 per SR list, not Tier-0 like Ethereum). Chainlink EUR/USD price feed on Gnosis (0xab70..., Tier-0 oracle) with 10 oracle nodes, 24h heartbeat, 0.1% deviation threshold. Gnosis bridge infrastructure for cross-chain governance execution. No CEX custody. Tier-2 chain dependency prevents Low (9) score. | 3 | 3 | Non-Improvable | [P0] [Chainlink EUR/USD Gnosis](https://data.chain.link/feeds/xdai/mainnet/eur-usd), [P0] [GnosisScan Oracle](https://gnosisscan.io/address/0xab70BCB260073d036d1660201e9d5405F5829b7a) |
| ST-IC-02 | How redundant are oracle and bridge setups, and can oracle values be corrected under abnormal conditions? | Chainlink EUR/USD feed on Gnosis: 10 oracle nodes (SNZPool, Inotel, Pier Two, Chainlayer, LinkPool, Fiews, Simply VC, DexTrac, Blockdaemon, 01Node). "Low Market Risk" classification by Chainlink. 24-hour heartbeat (same as Ethereum EUR/USD feed). Can be updated/corrected under abnormal conditions. Single primary provider (Chainlink) with partial fallback capability. Tier-0 oracle. | 9 | 9 | Non-Improvable (optimal) | [P0] [Chainlink EUR/USD Gnosis](https://data.chain.link/feeds/xdai/mainnet/eur-usd) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | **Unknown.** Chainlink has enterprise certifications. Aave Labs and BGD Labs: no public SOC 2/ISO27001 documentation found. Chaos Labs: no public certification documentation. Same gap as Ethereum Aave. | 3 | 9 | **Source Missing** | [P1] [Aave Security](https://aave.com/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Gnosis Chain had no major chain-level halts in last 12 months. Nov 2025: Balancer exploit required emergency response -- Gnosis team coordinated soft fork to freeze stolen funds, then Dec 2025 hard fork to recover $9.4M. Aave Gnosis pools were not directly impacted but the chain-level intervention (soft fork + hard fork) constitutes a significant chain incident even though it protected users. Infrastructure response was coordinated and effective but precedent-setting. | 3 | 3 | Non-Improvable | [P4] [Gnosis Hard Fork](https://unchainedcrypto.com/gnosis-completes-hard-fork-to-recover-balancer-exploit-funds/), [P4] [Balancer Exploit](https://www.theblock.co/post/377863/balancer-identifies-rounding-error-as-root-cause-of-multi-chain-defi-exploit) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Gnosis Chain had no chain halt >30 minutes in last 12 months. However, the Nov 2025 soft fork and Dec 2025 hard fork, while not "halts," represent significant consensus-layer interventions. The soft fork restricted bridge movements, and the hard fork changed state. Validators who didn't upgrade within 10 days faced penalties. This is not a halt but is a consensus intervention -- Mid (3) reflects the elevated chain-level risk from these interventions. Safe's Meissner confirmed "no bigger outages" on Gnosis Chain as of May 2025 (pre-fork). | 3 | 3 | Non-Improvable | [P4] [Gnosis Hard Fork Penalties](https://finance.yahoo.com/news/gnosis-chain-warns-validator-penalty-133203404.html), [P4] [Pectra on Gnosis](https://www.theblock.co/post/353018/pectra-gnosis-chain-bodes-well-major-ethereum-hardfork-safe-meissner-says) |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- This question applies to staking-based products. This is a lending protocol for EURe. While LST collaterals (wstETH, osGNO) are used by borrowers, slashing risk is borne by borrowers not EURe lenders. | N/A | N/A | N/A | - |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- Same rationale as ST-IC-06. For context: Gnosis Chain has 300,000+ validators across 70 countries. Chainlink EUR/USD oracle network includes 10 geographically diverse operators. | N/A | N/A | N/A | - |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | Gnosis Chain as single chain dependency: if Gnosis Chain halts, all withdrawals blocked (unlike Ethereum where this risk is near-zero). Gnosis bridge dependency for cross-chain governance. Oracle failure may trigger Guardian pause. However, withdrawals are permissionless via Pool contract as long as chain is live. Single chain failure could block withdrawals temporarily but chain has 300,000+ validators and no history of prolonged halts. | 3 | 3 | Non-Improvable | [P1] [Gnosis Chain](https://www.gnosis.io/chain) |

**Infrastructure Counterparty Subtotal: 20.0/45 (44.4%)**
- 1 question at score 9 = 9 points
- 5 questions at score 3 = 15 points
- 2 questions N/A (ST-IC-06, ST-IC-07)
- Raw: 24/54, Weighted: (24/54) x 45 = 20.0

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | None. User EURe deposits remain in Aave Pool V3 contract on Gnosis. No external deployment. Flash loans are atomic. Liquidators operate permissionlessly. | 9 | 9 | Non-Improvable (optimal) | [P0] [GnosisScan Pool V3](https://gnosisscan.io/address/0xb50201558B00496A145fE76f7424749556E326D8) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Yes. Protocol fees publicly visible on-chain. DAO treasury managed by Karpatkey. Fee dispute regarding ~$10M/year CowSwap interface fees acknowledged. Feb 2026: Aave Labs proposed directing 100% revenue to DAO. On-chain transparency of all fee flows. | 9 | 9 | Non-Improvable (optimal) | [P2] [DAO Financial Reports](https://governance.aave.com/t/aave-dao-financial-reports-financial-metrics/5575) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. Supply and borrow caps enforced on-chain for EURe on Gnosis. Caps actively managed by Chaos Labs Risk Stewards. Per-counterparty exposure limits via isolation mode and E-Mode categories. EURe reserve factor set to 10%. | 9 | 9 | Non-Improvable (optimal) | [P2] [Gnosis Instance Updates](https://governance.aave.com/t/arfc-aave-v3-gnosis-instance-updates/20334) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | In-protocol withdrawal is instant for available liquidity (~$3.13M at ~82.9% utilization). Rate model incentivizes rapid repayment at high utilization. However, bridging EURe from Gnosis to Ethereum adds delay (Gnosis bridge typically takes hours). Converting EURe to other assets on Gnosis faces extremely thin DEX liquidity post-Balancer exploit. | 3 | 3 | Non-Improvable | [P3] [Vaults.fyi](https://app.vaults.fyi/opportunity/gnosis/0xEdBC7449a9b594CA4E053D9737EC5Dc4CbCcBfb2) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | N/A for core EURe lending (no external custody by Aave). Monerium as EURe issuer is publicly known (Monerium EMI ehf., Iceland). For collateral: underlying operators disclosed (Lido for wstETH, StakeWise for osGNO). Chainlink oracle operators disclosed. | 9 | 9 | Non-Improvable (optimal) | [P1] [Monerium](https://monerium.com/) |

**Protocol Counterparty Subtotal: 39.0/45 (86.7%)**
- 4 questions at score 9 = 36 points
- 1 question at score 3 = 3 points
- Raw: 39/45, Weighted: (39/45) x 45 = 39.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | All EURe withdrawals are permissionless via Pool V3 contract based on available liquidity. Guardians can pause in emergency (5-of-9 multisig required) but pause is protocol-wide, not address-specific. No selective blocking by Aave. Note: Monerium can freeze addresses at the token level (demonstrated Nov 2025). | 9 | 9 | Non-Improvable (optimal) | [P0] [GnosisScan Pool V3](https://gnosisscan.io/address/0xb50201558B00496A145fE76f7424749556E326D8) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | At ~82.9% utilization, only ~$3.13M (~17.1% of TVL) is immediately available. This is significantly tighter than the EURC Ethereum pool (44.3% available at 55.66% utilization). Rate model incentivizes repayment but high utilization constrains immediate exits. For ~10% TVL (~$1.83M): yes, available. For near-total exit: would require borrower repayment driven by rate increases, potentially taking days. Total EURe market cap on Gnosis is only ~$18-22M, limiting repayment sources. | 3 | 9 | Non-Improvable | [P3] [Vaults.fyi](https://app.vaults.fyi/opportunity/gnosis/0xEdBC7449a9b594CA4E053D9737EC5Dc4CbCcBfb2) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No withdrawal delays, queues, or freezes reported for EURe specifically on Gnosis Aave. The broader Aave protocol: Nov 2023 temporary asset freezes during vulnerability patch (other pools, not EURe). Nov 2025 Balancer exploit caused Monerium to freeze ~EUR 1.3M but this was at the token level by issuer, not Aave protocol level. >95% of withdrawals complete within reasonable timeframe. | 9 | 9 | Non-Improvable (optimal) | [P3] [Vaults.fyi](https://app.vaults.fyi/opportunity/gnosis/0xEdBC7449a9b594CA4E053D9737EC5Dc4CbCcBfb2) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Current utilization ~82.9% is approaching the optimal utilization point (likely 90% based on standard Aave configuration). Supply cap is above current supply. Rate model penalizes high utilization. Risk Stewards have historically increased caps when needed (e.g., EURC Ethereum cap increases). Currently no cap-related withdrawal restrictions but high utilization is a concern. | 3 | 9 | Non-Improvable | [P2] [Gnosis Instance Updates](https://governance.aave.com/t/arfc-aave-v3-gnosis-instance-updates/20334) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | **Very limited stress data for EURe Gnosis specifically.** The pool has not been through a major stress event while operational. Nov 2025 Balancer exploit was a Gnosis ecosystem event but EURe Gnosis Aave pool was not directly stressed. Gnosis chain itself handled the exploit response well but required soft fork + hard fork. Per framework, untested protocols should score Mid (3). EURe's thin secondary market on Gnosis (Balancer pools frozen, CowSwap via UniV3 as fallback) exacerbates exit challenges. | 3 | 3 | Non-Improvable | [P4] [Gnosis Balancer Response](https://x.com/gnosisdotio/status/1985321081255891396) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No lockups, vesting, or unstaking delays for EURe withdrawal from Aave. Instant withdrawal if liquidity available. However, if the user needs to bridge EURe from Gnosis to Ethereum, the Gnosis bridge exit takes hours. This is a post-withdrawal step, not an in-protocol restriction. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Primary EURe redemption through Pool contract is always available (subject to pool liquidity). However, if users need to convert EURe to other assets after withdrawal, Gnosis DEX liquidity is extremely thin for EURe post-Balancer exploit. Balancer EURe/sDAI pools were frozen. Uniswap V3 pools on Gnosis are primary remaining venue. CowSwap routes through remaining liquidity. | 3 | 3 | Non-Improvable | [P4] [Gnosis Balancer Response](https://x.com/gnosisdotio/status/1985321081255891396) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | **Very thin secondary market.** EURe total market cap across all chains is only ~$28-32M. On Gnosis specifically, primary DEX liquidity disrupted after Balancer exploit (Nov 2025). Balancer EURe/sDAI pool frozen. Remaining liquidity via UniV3 and CowSwap is minimal. For the ~$18.31M pool, secondary market cannot absorb even ~3% of TVL without major impact. Below the ~3% threshold = High (1). | 1 | 1 | Non-Improvable | [P3] [CoinGecko](https://www.coingecko.com/en/coins/monerium-eur-money) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | **Elevated.** At ~82.9% utilization, only ~$3.13M available. EURe total market cap (~$28-32M across all chains) is barely larger than the Gnosis Aave pool itself (~$18.31M). A bank-run would spike rates but borrowers may face extreme difficulty sourcing EURe to repay given the tiny total supply. Circular liquidity problem is severe: if all lenders want to exit, there is insufficient EURe in existence outside the pool to facilitate repayment. Rate model provides protection but the systemic constraint is binding. | 1 | 1 | Non-Improvable | [P3] [CoinGecko](https://www.coingecko.com/en/coins/monerium-eur-money) |

**Liquidity Subtotal:**
- ST-L-01=9, ST-L-02=3, ST-L-03=9, ST-L-04=3, ST-L-05=3, ST-L-06=9, ST-L-07=3, ST-L-08=1, ST-L-09=1
- 3x9 + 4x3 + 2x1 = 27+12+2 = 41. Max = 9x9 = 81.
- (41/81) x 45 = 22.778 = 22.8

**Liquidity Subtotal: 22.8/45 (50.6%)**

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | aGnoEURe maintains 1:1 with underlying EURe by design (interest-bearing aToken). No peg deviation possible as aToken represents a claim on Pool liquidity plus accrued interest. Architectural peg, not market-dependent. | 9 | 9 | Non-Improvable (optimal) | [P0] [GnosisScan aEURe](https://gnosisscan.io/address/0xEdBC7449a9b594CA4E053D9737EC5Dc4CbCcBfb2) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Low for EURe lenders from crypto market moves. Overcollateralized design protects suppliers. Borrowers face liquidation risk, not lenders. EUR/USD FX exposure exists for non-EUR allocators but EURe principal is protected in EUR terms. Score reflects stablecoin lending's inherent low directional exposure. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Interest rate model with steep slope2. Current utilization at ~82.9% is approaching optimal but rate model forces repayment at high utilization. Reserve factor reduced to 10% to incentivize supply. No history of prolonged >=95% utilization for EURe on Gnosis. However, the small pool size means TVL shifts are more impactful -- a single large withdrawal/deposit can significantly move utilization. | 9 | 9 | Non-Improvable (optimal) | [P2] [Gnosis Instance Updates](https://governance.aave.com/t/arfc-aave-v3-gnosis-instance-updates/20334) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Chaos Labs and LlamaRisk provided risk assessments for Gnosis instance, including analysis of on-chain liquidity and parameter recommendations. GNO volatility (80.46%) explicitly modeled. sDAI/EURe E-Mode analyzed. Aave platform stress-tested multiple times (Feb 2025, Feb 2026). EURe Gnosis-specific stress testing is limited by pool's shorter history. | 9 | 9 | Non-Improvable (optimal) | [P2] [Gnosis Instance Updates](https://governance.aave.com/t/arfc-aave-v3-gnosis-instance-updates/20334) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | For EURe borrowers: yes, if collateral value drops. For EURe lenders/suppliers: no, protected by overcollateralization. Stablecoin lending advantage: EURe is borrowed against volatile collateral (GNO, WETH, wstETH), so collateral decline triggers protective liquidations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Features](https://github.com/aave-dao/aave-v3-origin/blob/main/docs/3.3/Aave-v3.3-features.md) |

**Market Subtotal: 45.0/45 (100.0%)**

---

### **Strategy Total: 195.1/270 (72.3%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 38.3 | 45 | 85.2% |
| Collateral | 30.0 | 45 | 66.7% |
| Infra Counterparty | 20.0 | 45 | 44.4% |
| Protocol Counterparty | 39.0 | 45 | 86.7% |
| Liquidity | 22.8 | 45 | 50.6% |
| Market | 45.0 | 45 | 100.0% |
| **Strategy Total** | **195.1** | **270** | **72.3%** |

**Precise Strategy calculation:**
- Protocol Mechanics: (69/81) x 45 = 38.333 = 38.3
- Collateral: (24/36) x 45 = 30.0
- Infra Counterparty: (24/54) x 45 = 20.0
- Protocol Counterparty: (39/45) x 45 = 39.0
- Liquidity: (41/81) x 45 = 22.778 = 22.8
- Market: (45/45) x 45 = 45.0
- **Total: 38.3 + 30.0 + 20.0 + 39.0 + 22.8 + 45.0 = 195.1**

---

### OPERATIONS (30% Weight) -- Score: 256.0/270 (94.8%)

**NOTE: All Operations scores are IDENTICAL to other Aave V3 Core Market ratings per Platform Consistency. Same governance, same team, same docs, same treasury, same backstop.**

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | On-chain DAO governance via AAVE, stkAAVE, aAAVE token voting. Cross-chain governance executes on Gnosis via bridge executor. Structured proposal process: Temp Check -> ARFC -> AIP. Risk Stewards handle parameter adjustments. Two 5-of-9 Guardian multisigs. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [Gnosis Enhancements](https://governance.aave.com/t/arfc-enhancements-in-aave-v3-gnosis-chain-instance/21214) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | Moderate concentration typical of large DAOs. Robust checks: two 5-of-9 Guardian multisigs, Risk Steward system, structured proposal process. Active governance participation demonstrated by Gnosis-specific proposals. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. 1-day standard timelock, 7-day for critical changes. Two Guardian multisigs (5-of-9 each) with veto powers. Cross-chain governance execution preserves timelock protections on Gnosis. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A -- Aave has no "strategy manager." Risk providers can be changed via governance without impact on withdrawals. EURe pool withdrawals are always permissionless. | N/A | N/A | N/A | - |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 3 questions at score 9 = 27, 1 N/A
- Raw: 27/27, Weighted: (27/27) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Aave: Stani Kulechov (founder), Aave Labs, BGD Labs. Monerium: CEO Gisli Kristjansson, Chair Sveinn Valfells (PhD), COO Hjortur Hjartarson, CTO Margus Kerma, Head of Strategic Partnerships Jon Helgi Egilsson (PhD, ex-Central Bank of Iceland supervisory board). All publicly identified with verifiable backgrounds. | 9 | 9 | Non-Improvable (optimal) | [P1] [Monerium Team](https://monerium.com/team/), [P3] [Crunchbase Aave](https://www.crunchbase.com/organization/ethlend) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Aave: Multiple independent development teams (Aave Labs, BGD Labs, Certora, Chaos Labs). Monerium: Smaller team (7 core), but EURe issuance is operationally simpler than smart contract development. The Aave protocol itself is not dependent on Monerium. | 9 | 9 | Non-Improvable (optimal) | [P1] [BGD Labs GitHub](https://github.com/bgd-labs), [P1] [Monerium Team](https://monerium.com/team/) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Aave: Aave SAGL (Swiss, Zug), Aave Labs (London). Monerium: Monerium hf. (Iceland, No. 550512-1060) and Monerium EMI ehf. (licensed EMI, regulated by Central Bank of Iceland). Clear entity mapping for both protocol and asset issuer. | 9 | 9 | Non-Improvable (optimal) | [P1] [Monerium](https://monerium.com/), [P3] [Monerium EMI Registration](https://thebanks.eu/emis/monerium-emi-354914) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | **CLEARED for Aave.** SEC closed 4-year investigation December 16, 2025 without enforcement action. No ongoing actions. Monerium: Licensed EMI, no known investigations or enforcement actions. MiCA-compliant. | 9 | 9 | Non-Improvable (optimal) | [P4] [SEC Investigation Closure](https://finance.yahoo.com/news/sec-closes-4-long-investigation-091715487.html) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Yes. Demonstrated rapid response: Nov 2023 vulnerability patched within hours. Feb 2026: Real-time parameter adjustments during market crash. Nov 2025: Cross-ecosystem coordination between Gnosis, Monerium, and Balancer during exploit. Monerium froze EURe within hours of Balancer exploit discovery. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P4] [Gnosis Balancer Response](https://x.com/gnosisdotio/status/1985321081255891396) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Active governance forum with regular updates. Gnosis-specific proposals receive dedicated analysis from Chaos Labs and LlamaRisk. Discord and community channels active for both Aave and Monerium. | 9 | 9 | Non-Improvable (optimal) | [P2] [Gnosis Instance Updates](https://governance.aave.com/t/arfc-aave-v3-gnosis-instance-updates/20334) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Aave: $29.5M raised from 41 investors. Monerium: Seed from ConsenSys, Crowberry Capital; $4M from Teleport/Wise founders (Sten Tamkivi, Taavet Hinrikus). Notable investors include David Helgason (Unity), Hjalmar Winbladh (EQT Ventures), Balaji Srinivasan. All disclosed. | 9 | 9 | Non-Improvable (optimal) | [P1] [Monerium Funding](https://monerium.com/press/20210922-monerium-funding-first-billion-euro/), [P3] [Crunchbase Aave](https://www.crunchbase.com/organization/ethlend) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | **Governance tension exists.** Dec 2025: DAO-Labs conflict over CowSwap interface fees. Feb 2026: Aave Labs proposed "Aave Will Win" plan. Debate ongoing. Conflict represents governance health issue but has not impacted user fund safety. Same as all Aave pools. | 3 | 9 | **Improvable** | [P4] [CoinDesk Dec 2025](https://www.coindesk.com/tech/2025/12/15/aave-dao-pushes-back-as-interface-fees-shift-away-from-treasury) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | No. 8+ year Aave track record without user fund losses. March 2026 CAPO incident: DAO committed to 100% reimbursement. Monerium: no known collateral loss events. Clean operational history for both entities. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |

**Team & Legal Subtotal: 62.5/67.5 (92.6%)**
- 8 questions at score 9 = 72 points
- 1 question at score 3 = 3 points
- Raw: 75/81, Weighted: (75/81) x 67.5 = 62.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive Aave V3 documentation. Gnosis-specific governance proposals document parameters. Monerium docs cover V2 token architecture, migration details. Risks page covers liquidation, oracle, smart contract risks. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Docs](https://aave.com/docs/aave-v3/overview), [P1] [Monerium V2 Docs](https://monerium.dev/docs/contracts-v2) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Aave documentation covers health factor, liquidation process, bad debt scenarios, interest rate models. EURe-specific parameters documented in governance proposals. Loss conditions clearly explained. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Risks](https://aave.com/docs/resources/risks) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. BGD Address Book (AaveV3Gnosis.sol) provides canonical registry of all Gnosis contracts: Pool (0xb502...), ACLManager (0xEc71...), Oracle (0xeb0a...), aEURe (0xEdBC...), etc. All verified on GnosisScan. | 9 | 9 | Non-Improvable (optimal) | [P1] [BGD Address Book](https://github.com/bgd-labs/aave-address-book/blob/main/src/AaveV3Gnosis.sol) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Guardian roles, timelock durations, Risk Steward permissions documented. All governance changes visible on-chain and in governance forum. Gnosis-specific parameter changes tracked via ARFC proposals. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full on-chain transparency. All EURe pool balances verifiable via Pool V3 contract on GnosisScan. Protocol Data Provider enables programmatic verification. DeFiLlama tracking. Monerium publishes reserve attestations (102% overcollateralization). | 9 | 9 | Non-Improvable (optimal) | [P0] [GnosisScan Pool V3](https://gnosisscan.io/address/0xb50201558B00496A145fE76f7424749556E326D8), [P1] [Monerium EURe](https://monerium.com/eure/) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. All core contracts verified on GnosisScan: Pool V3 (0xb502...), PoolConfigurator (0x7304...), aEURe (0xEdBC...), variableDebtEURe (0xb964...), ACLManager (0xEc71...), Oracle (0xeb0a...), EURe V1 (0xcB44...), EURe V2 (0x420C...). Full source code readable. | 9 | 9 | Non-Improvable (optimal) | [P0] [GnosisScan Pool V3](https://gnosisscan.io/address/0xb50201558B00496A145fE76f7424749556E326D8) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Yes. Aave Umbrella Safety Module (~$263M in staked assets, automated slashing). DAO Treasury ~$119.5M (per DeFiLlama 2026). Combined ~$382M. Note: Umbrella is shared across all Aave markets including Gnosis. EURC is not currently a staked asset in Umbrella but cross-asset coverage applies. | 9 | 9 | Non-Improvable (optimal) | [P1] [Umbrella Docs](https://aave.com/docs/aave-v3/umbrella), [P3] [DeFiLlama Aave](https://defillama.com/protocol/aave) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | **Modest relative to overall scale.** Combined ~$382M vs ~$28.5B total Aave V3 TVL = ~1.3%. Below 5% threshold for Low Risk; within 1-5% range = Mid Risk. For Gnosis EURe specifically: $382M vs $18.31M EURe TVL = huge ratio, but backstop is shared across ALL Aave markets globally. | 3 | 9 | **Improvable** | [P3] [DeFiLlama Aave V3](https://defillama.com/protocol/aave-v3) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. DAO Treasury ~$119.5M. Protocol generated $885M in fees in 2025. Revenue broadly covers expenses. Runway >24 months. Monerium also has disclosed funding (ConsenSys, Crowberry, Wise/Teleport founders). | 9 | 9 | Non-Improvable (optimal) | [P3] [DeFiLlama Aave](https://defillama.com/protocol/aave) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Aave: Highly resilient. Survived multiple severe stress events. Feb 2025: $210M liquidations, zero bad debt. Feb 2026: $429M record liquidations, zero bad debt. Gnosis-specific: Pool has operated without issues since activation (~Oct 2023). Gnosis chain-level Balancer exploit (Nov 2025) was handled without Aave losses. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Smart contracts are permissionless and non-custodial. EURe withdrawals always available via direct Pool contract interaction based on available liquidity. Cross-chain governance via on-chain voting. Multiple independent development teams. Monerium as EURe issuer would need to continue operations for new EURe issuance/redemption, but existing on-chain EURe in Aave Pool remains accessible. | 9 | 9 | Non-Improvable (optimal) | [P0] [GnosisScan Pool V3](https://gnosisscan.io/address/0xb50201558B00496A145fE76f7424749556E326D8) |

**Financial Resilience Subtotal: 58.5/67.5 (86.7%)**
- 4 questions at score 9 = 36, 1 question at score 3 = 3
- Raw: 39/45, Weighted: (39/45) x 67.5 = 58.5

---

### **Operations Total: 256.0/270 (94.8%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 67.5 | 67.5 | 100.0% |
| Team & Legal | 62.5 | 67.5 | 92.6% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 58.5 | 67.5 | 86.7% |
| **Operations Total** | **256.0** | **270** | **94.8%** |

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 99 | 99 | 180.0 | 180 | 100.0% |
| | Key Management (7 of 8 Q scored) | 57 | 63 | 162.9 | 180 | 90.5% |
| | **Security Subtotal** | | | **342.9** | **360** | **95.2%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 69 | 81 | 38.3 | 45 | 85.2% |
| | Collateral (4 Q) | 24 | 36 | 30.0 | 45 | 66.7% |
| | Infra Counterparty (6 of 8 Q scored) | 24 | 54 | 20.0 | 45 | 44.4% |
| | Protocol Counterparty (5 Q) | 39 | 45 | 39.0 | 45 | 86.7% |
| | Liquidity (9 Q) | 41 | 81 | 22.8 | 45 | 50.6% |
| | Market (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | **Strategy Subtotal** | | | **195.1** | **270** | **72.3%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 75 | 81 | 62.5 | 67.5 | 92.6% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 39 | 45 | 58.5 | 67.5 | 86.7% |
| | **Operations Subtotal** | | | **256.0** | **270** | **94.8%** |
| **TOTAL** | | | | **794.0** | **900** | **88.2%** |

---
