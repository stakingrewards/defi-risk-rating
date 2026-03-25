# Kelp DAO - rsETH Risk Rating

**Rating Date**: 2026-03-18
**Final Grade**: CCC+
**Total Score**: 583.1/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v1.0-alpha

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 261.8/360 (72.7%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 10 independent audits from 3 firms: Sigma Prime (6 reports: core, withdrawal V1/V2, PEPE upgrade Sep 2024, rsETH Adaptor Nov 2024, June 2025 upgrades), Code4rena (Nov 2023), MixBytes (Mar 2024), Bailsec (Sep 2025 full rsETH audit, Dec 2025 core differential). All core fund-custody/routing contracts covered with ongoing audit cadence. | 9 | 9 | Non-Improvable (optimal) | [P1] [Kelp Audits](https://kerneldao.gitbook.io/kernel/getting-started/kelp/audits), [P1] [Code4rena Report](https://code4rena.com/reports/2023-11-kelp) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Sigma Prime (Tier-0) conducted 3 audits including the most recent withdrawal functionality reviews. Code4rena and MixBytes are not on the SR tier list. | 9 | 9 | Non-Improvable (optimal) | [P1] [SigmaPrime Report](https://kerneldao.com/kelp/audits/smartcontracts/SigmaPrime.pdf) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | The April 2025 LRTOracle upgrade introduced the infinite mint bug without a prior audit, which is a historical failure. However, post-incident the team established a robust audit cadence: Sigma Prime audited June 2025 upgrades (1 High, 3 Low, 2 Info -- fixes verified via PR-245), Bailsec conducted a full rsETH audit in Sep 2025 (3 High, 13 Medium -- with resolution commits), and Bailsec performed a differential audit in Dec 2025 (0 High, 0 Medium). Upgrades are now consistently followed by audits, but the April 2025 failure remains a data point. | 3 | 9 | **Improvable** | [P1] [Sigma Prime June 2025](https://kerneldao.com/kelp/audits/smartcontracts/SigmaPrime_6.pdf), [P1] [Bailsec Sep 2025](https://kerneldao.com/kelp/audits/smartcontracts/Bailsec_rsETH_november.pdf), [P1] [Bailsec Dec 2025](https://kerneldao.com/kelp/audits/smartcontracts/Bailsec_rsETH_december_2025.pdf) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Across 10 audits: Code4rena H-01 disputed as intentional design. Sigma Prime June 2025: 1 High (KLP8-01 stale rsETH price -- closed as design choice by team). Bailsec Sep 2025: 3 High found, 1 resolved, 2 acknowledged (no fix applied); 13 Medium, 3 resolved, 10 acknowledged. Bailsec Dec 2025: 0 High, 0 Medium -- showing codebase maturation. Pattern of acknowledging but not fixing some High findings persists across auditors. | 3 | 9 | **Improvable** | [P1] [C4 Report](https://code4rena.com/reports/2023-11-kelp), [P1] [Sigma Prime June 2025](https://kerneldao.com/kelp/audits/smartcontracts/SigmaPrime_6.pdf), [P1] [Bailsec Sep 2025](https://kerneldao.com/kelp/audits/smartcontracts/Bailsec_rsETH_november.pdf), [P1] [Bailsec Dec 2025](https://kerneldao.com/kelp/audits/smartcontracts/Bailsec_rsETH_december_2025.pdf) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | All core contracts use TransparentUpgradeableProxy. Upgrades require 6/8 external admin multisig proposal through TimelockController with 10-day minimum delay. ProxyAdmin owned by TimelockController. Strong upgrade constraints. | 9 | 9 | Non-Improvable (optimal) | [P0] [TimelockController](https://etherscan.io/address/0x49bD9989E31aD35B0A62c20BE86335196A3135B1), [P1] [GitHub README](https://github.com/Kelp-DAO/LRT-rsETH) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | Yes. April 30, 2025: infinite mint bug in LRTOracle fee calculation (1e36 vs 1e18 scaling). ~16.9 quadrillion rsETH minted to fee recipient. Circuit breakers activated, deposits/withdrawals paused. No user fund loss. Excess tokens burned. Fee set to 0. Chainlink PoR integrated post-incident. Scores Mid (3): loss <2%, full compensation (no loss), post-mortem published. Additionally, July 2024 domain hijacking via GoDaddy social engineering redirected users to malicious site -- this was infrastructure, not smart contract exploit. | 3 | 3 | Non-Improvable | [P2] [Aave Freeze](https://governance.aave.com/t/rseth-precautionary-freezing-30-04-2025/21925), [P2] [Morpho Forum](https://forum.morpho.org/t/kelp-incident-response/1727), [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No confirmed rug-pull. Founded by Dheeraj Borra and Amitej Gajjala (also Stader Labs founders). Funded by SCB Capital, Laser Digital (Nomura), Bankless Ventures, and others ($9M raised). | 9 | 9 | Non-Improvable (optimal) | [P4] [Yahoo Finance](https://finance.yahoo.com/news/kelp-dao-raises-9-million-090008172.html) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No evidence of timelock reductions. The 10-day delay has been consistent. | 9 | 9 | Non-Improvable (optimal) | [P0] [TimelockController](https://etherscan.io/address/0x49bD9989E31aD35B0A62c20BE86335196A3135B1) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active Immunefi bug bounty since August 2, 2024. Max payout $250K for critical smart contract vulnerabilities. Scope covers rsETH, LRTDepositPool, LRTOracle, LRTWithdrawalManager, LRTUnstakingVault, NodeDelegator, FeeReceiver, LRTConverter. KYC required. PoC required. Last updated March 21, 2025. | 9 | 9 | Non-Improvable (optimal) | [P1] [Immunefi Kelp DAO](https://immunefi.com/bug-bounty/kelp-dao/scope/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | No evidence of structured monitoring or alerting system. No mention of Hypernative, Blockaid, or similar providers. The circuit breaker that activated during the April 2025 incident suggests some automated controls exist, but no documentation of monitoring providers, dashboards, or on-call procedures. | 1 | 9 | **Source Missing** | [P1] No monitoring mentioned in docs, [P2] Circuit breaker activated in April 2025 incident |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | The April 2025 incident demonstrated that circuit breakers exist and functioned -- exchange rate drop detection paused deposits/withdrawals automatically. However, the monitoring that feeds into these circuit breakers is undocumented. The circuit breaker itself worked as intended, but the trigger mechanism and response procedures are unclear. | 3 | 9 | **Source Missing** | [P2] [Aave Freeze](https://governance.aave.com/t/rseth-precautionary-freezing-30-04-2025/21925), [P2] [Morpho Forum](https://forum.morpho.org/t/kelp-incident-response/1727) |

**Smart Contract Security Subtotal:**
- Raw scores: 9+9+3+3+9+3+9+9+9+1+3 = 67/99
- Adjusted: (67/99) x 180 = **121.8/180 (67.7%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Admin/upgrade rights held by 6/8 External Admin multisig (0xb3696a817D01C8623E66D156B6798291fa10a46d) which is the PROPOSER_ROLE on TimelockController. Signers are publicly identified industry figures from Protokol, Avid VC, AltLayer, Router Protocol, and include co-founder Dheeraj Borra. Well-documented with rationale. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe Address](https://etherscan.io/address/0xb3696a817D01C8623E66D156B6798291fa10a46d), [P1] [Kelp Docs](https://kelp.gitbook.io/kelp/rseth-smart-contracts) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Upgrading custody contracts requires 6/8 multisig + 10-day timelock. EXECUTOR_ROLE set to zero address (anyone can execute after delay). No single key can move user funds or upgrade custody. Threshold 6, signers 8. Exceeds 3-of-5 minimum. | 9 | 9 | Non-Improvable (optimal) | [P0] [TimelockController](https://etherscan.io/address/0x49bD9989E31aD35B0A62c20BE86335196A3135B1), [P1] [GitHub README](https://github.com/Kelp-DAO/LRT-rsETH) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | External Admin is 6/8 with 3+ independently verified signers (named individuals from different organizations: Protokol, Avid VC, AltLayer, Router Protocol). However, the Manager multisig is only 2/5 and the Admin multisig is 3/5, both with less transparency. The critical upgrade path (6/8 External Admin) is strong, but operational roles use weaker thresholds. | 9 | 9 | Non-Improvable (optimal) | [P1] [Kelp Docs](https://kelp.gitbook.io/kelp/rseth-smart-contracts), [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause capability exists and was demonstrated during the April 2025 incident. Circuit breakers automatically pause on exchange rate anomalies. No evidence of address-level withdrawal censorship. Pause appears protocol-wide and controlled by multisig. Rules partially documented. | 3 | 9 | **Source Missing** | [P2] [Aave Freeze](https://governance.aave.com/t/rseth-precautionary-freezing-30-04-2025/21925) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets are held in on-chain non-custodial contracts: LRTDepositPool, NodeDelegator contracts (7 delegators), and EigenLayer strategy contracts. No off-chain custody. | 9 | 9 | Non-Improvable (optimal) | [P0] [LRTDepositPool](https://etherscan.io/address/0x036676389e48133B63a802f8635AD39E752D375D), [P1] GitHub README |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | User funds are in distinct smart contracts (DepositPool, NodeDelegator, EigenLayer strategies). The April 2025 incident minted excess rsETH to a fee recipient controlled by the team, but user deposit contracts were separate. Clear on-chain segregation. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain contract architecture |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- rsETH is an LST/LRT, not a managed vault strategy. Delegation is to EigenLayer only. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No documented playbook found. The April 2025 incident response was effective (pausing, burning, fixing), but no formal playbook, tabletop exercise, or key rotation procedure is publicly documented. | 1 | 9 | **Improvable** | [P1] No playbook in docs or GitHub |

**Key Management Subtotal (7 of 8 scored):**
- Raw scores: 9+9+9+3+9+9+1 = 49/63
- Adjusted: (49/63) x 180 = **140.0/180 (77.8%)**
- N/A: S-KM-07

**Validation:** 49/63 = 0.7778; 0.7778 x 180 = 140.0. Confirmed.

**Security Total: 121.8 + 140.0 = 261.8/360 (72.7%)**

---

### STRATEGY (30% Weight) -- Score: 188.7/270 (69.9%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield comes from: (1) ETH staking rewards (consensus + execution layer), (2) EigenLayer restaking rewards from 9 AVSs. Both align with rsETH's stated mandate as a liquid restaking token. Yield sources are organic and mandate-aligned. No breakdown of % contributions publicly available. | 3 | 9 | **Improvable** | [P1] [Kelp Docs](https://kerneldao.gitbook.io/kernel), [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Negative yield limited to: severe validator slashing (mitigated by operator diversification), extreme ETH market crash, or EigenLayer AVS slashing. These are tail shocks. The rsETH exchange rate gradually increases, and circuit breakers protect against anomalous rate changes. | 9 | 9 | Non-Improvable (optimal) | [P1] Protocol design, [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage. rsETH represents 1:1 staked/restaked ETH. No rehypothecation beyond the restaking to EigenLayer which is the core product function. Effective leverage is 1.0x. | 9 | 9 | Non-Improvable (optimal) | [P1] Protocol design |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- LST product, no lending/leverage positions to liquidate. | N/A | N/A | N/A | - |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent loss to rsETH holders. The April 2025 infinite mint was to a fee recipient, not user funds. The exchange rate was not impacted. No comparable LRT strategy has caused permanent depositor loss. | 9 | 9 | Non-Improvable (optimal) | [P2] [Aave Freeze Discussion](https://governance.aave.com/t/rseth-precautionary-freezing-30-04-2025/21925) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | N/A -- LST product, not a vault. | N/A | N/A | N/A | - |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yield is organic: ETH staking + EigenLayer restaking rewards. No significant token emissions driving yield. KERNEL airdrops exist but are separate from rsETH yield. rsETH's yield is sustainable as long as ETH staking and EigenLayer rewards continue. | 9 | 9 | Non-Improvable (optimal) | [P1] Protocol mechanics |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Withdrawal takes 7-10 days (7-day EigenLayer delay + processing). Under conservative assumptions, most positions can unwind within this horizon. Secondary market (Uniswap) provides faster exit with ~$776K daily volume. Slippage for large exits would be moderate given TVL decline to ~$47M. | 3 | 9 | **Improvable** | [P3] CoinGecko volume data, [P1] [Withdrawal docs](https://kelp.gitbook.io/kelp/explore-rseth/rseth-withdrawal) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | rsETH is non-rebasing and appreciates against ETH. No carry trade or invertible spread. Yield comes from staking/restaking, not from any spread mechanism. | 9 | 9 | Non-Improvable (optimal) | [P1] Protocol design |

**Protocol Mechanics Subtotal (7 of 9 scored):**
- Raw scores: 3+9+9+9+9+3+9 = 51/63
- Adjusted: (51/63) x 45 = **36.4/45 (80.9%)**
- N/A: ST-PM-04, ST-PM-06

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Accepted: ETH (native), stETH (Lido, BBB+/845.4 SR rating), ETHx (Stader, unrated but ETHx is smaller/newer LST). All are Ethereum staking derivatives or native ETH -- established large-cap assets. ETHx is the weakest link but exposure-capped by deposit pool allocation. | 9 | 9 | Non-Improvable (optimal) | [P1] [Kelp Docs](https://kerneldao.gitbook.io/kernel), [P0] [LRTDepositPool](https://etherscan.io/address/0x036676389e48133B63a802f8635AD39E752D375D) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | stETH maintained tight peg to ETH throughout 2024-2025. ETHx has had no significant depeg events. However, the LlamaRisk assessment noted that stETH is hardcoded 1:1 and ETHx uses internal exchange rates, creating potential arbitrage vectors during depeg. The rsETH token itself was frozen on Aave for 8 days during the April 2025 incident, but collateral (ETH/stETH/ETHx) remained stable. | 3 | 9 | **Improvable** | [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth), [P3] CoinGecko price data |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Three operators (Kiln, Allnodes, Luganodes) with RAVER scores >96%. No validators have been slashed per LlamaRisk (as of July 2024). ~5,200 validators diversified across operators. KERNEL staking will provide insurance against slashing (post-TGE). Some diversification but no explicit insurance buffer currently exists. | 3 | 9 | **Improvable** | [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth) |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | On Ethereum mainnet, collateral is native ETH + native stETH + native ETHx. None are bridged or wrapped (stETH is natively issued on Ethereum, not a bridge token). rsETH on L2s is bridged, but the question evaluates the base protocol TVL. <20% bridged/wrapped on Ethereum. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain deposit pool holdings |

**Collateral Subtotal:**
- Raw scores: 9+3+3+9 = 24/36
- Adjusted: (24/36) x 45 = **30.0/45 (66.7%)**

---

#### Infra Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Core dependencies: Ethereum (Tier-0 chain), EigenLayer (Tier-0 protocol), Chainlink oracles (Tier-0), Kiln/Allnodes/Luganodes validators. All critical dependencies use Tier-0/Tier-1 infrastructure. L2 deployments add bridge dependencies but are non-critical for core operations. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub README](https://github.com/Kelp-DAO/LRT-rsETH), [P0] Contract addresses |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | LRTOracle uses internal price calculations with ChainlinkPriceOracle as a component. Post-April 2025, Chainlink PoR Secure Mint adds redundancy for minting. However, stETH is still hardcoded 1:1 (no oracle fallback). ETHx uses internal Stader exchange rate. Single oracle path per asset. | 3 | 9 | **Improvable** | [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth), [P1] [Chainlink PoR Blog](https://blogs.kerneldao.com/blog/kelp-is-integrating-chainlink-proof-of-reserve-to-help-further-secure-rseth-s-minting-function) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | No SOC 2 Type II or ISO27001 certification disclosed for Kelp/KernelDAO's off-chain infrastructure. The withdrawal architecture has been upgraded with on-chain queue unlocking and Aave v3 integration (per Bailsec Dec 2025), reducing off-chain dependency. Operators still need to call unlockQueue but the critical path is more on-chain than the 2024 LlamaRisk assessment suggested. Consistent with peers (Aave, Morpho, Etherfi, Lido) that also lack disclosed certifications. | 3 | 9 | **Source Missing** | [P1] [Bailsec Dec 2025](https://kerneldao.com/kelp/audits/smartcontracts/Bailsec_rsETH_december_2025.pdf), [P1] No certifications in docs |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | The April 2025 incident demonstrated that circuit breakers worked (paused deposits/withdrawals automatically). Protocol was frozen on Aave for 8 days but resumed without user losses. The July 2024 domain hack was resolved. Infrastructure has been tested through actual incidents. | 3 | 3 | Non-Improvable | [P2] [Aave Freeze](https://governance.aave.com/t/rseth-precautionary-freezing-30-04-2025/21925) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Ethereum (Tier-0) has had no chain halt or consensus failure >30 min in the last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P3] Ethereum network status |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | No slashing events affecting Kelp validators per LlamaRisk assessment (as of July 2024). All three operators (Kiln, Allnodes, Luganodes) maintain RAVER scores >96%. No evidence of slashing in the subsequent period. | 9 | 9 | Non-Improvable (optimal) | [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth) |
| ST-IC-07 | Are validators diverse geographically and by operator? | Three independent operators across three jurisdictions: Kiln (France), Allnodes (Ukraine), Luganodes (Switzerland). No single operator controls >50% of Kelp's validators. Geographic diversity spans Western Europe, Eastern Europe, and Central Europe. All three are established professional node operators with high RAVER scores (>96%). This meets the threshold for adequate operator and geographic diversification. | 9 | 9 | Non-Improvable (optimal) | [P1] [Kelp Docs](https://kelp.gitbook.io/kelp/rseth-smart-contracts), [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth) |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | The withdrawal architecture has been significantly upgraded since the 2024 LlamaRisk assessment. Per Bailsec Dec 2025 audit: LRTWithdrawalManager now supports on-chain queue unlocking via both ASSET_TRANSFER_ROLE and OPERATOR_ROLE, and `_processWithdrawalCompletion` automatically handles Aave v3 withdrawals when contract balance is insufficient. However, operators still need to call unlockQueue to process withdrawal requests, and the off-chain component for EigenLayer undelegation likely persists. Single component failure would delay but not permanently block withdrawals. | 3 | 9 | **Improvable** | [P1] [Bailsec Dec 2025](https://kerneldao.com/kelp/audits/smartcontracts/Bailsec_rsETH_december_2025.pdf), [P1] [Bailsec Sep 2025](https://kerneldao.com/kelp/audits/smartcontracts/Bailsec_rsETH_november.pdf) |

**Infra Counterparty Subtotal:**
- Raw scores: 9+3+3+3+9+9+9+3 = 48/72
- Adjusted: (48/72) x 45 = **30.0/45 (66.7%)**

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Collateral deployed into EigenLayer (Tier-0 protocol) via NodeDelegator contracts across 9 AVSs. EigenLayer is the primary external venue. Staking via Kiln, Allnodes, Luganodes. All Tier-0/1 venues. | 9 | 9 | Non-Improvable (optimal) | [P0] [NodeDelegator contracts](https://github.com/Kelp-DAO/LRT-rsETH), [P1] EigenLayer |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | No specific revenue-share arrangements with counterparties disclosed. EigenLayer rewards flow to the protocol. Protocol fee exists but was reduced to 0 post-April 2025 incident. No apparent conflict documentation but also no explicit disclosure. | 3 | 9 | **Source Missing** | [P1] No disclosure in docs |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | EigenLayer is the sole restaking counterparty. NodeDelegator contracts allocate to specific operators. No documented per-counterparty caps or rebalancing rules beyond operator allocation managed by the 2/5 Manager multisig. | 3 | 9 | **Improvable** | [P1] [GitHub README](https://github.com/Kelp-DAO/LRT-rsETH) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | EigenLayer withdrawals take 7 days (protocol-imposed minimum). Kelp adds processing time for a total of 7-10 days. Well-documented and tested. Positions can be unwound without discretionary approvals. | 9 | 9 | Non-Improvable (optimal) | [P1] [Withdrawal docs](https://kelp.gitbook.io/kelp/explore-rseth/rseth-withdrawal) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | All three node operators (Kiln, Allnodes, Luganodes) are disclosed by name with roles and performance metrics (RAVER scores). EigenLayer operator assignments are documented. | 9 | 9 | Non-Improvable (optimal) | [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth), [P1] [Kelp Docs](https://kelp.gitbook.io/kelp/rseth-smart-contracts) |

**Protocol Counterparty Subtotal:**
- Raw scores: 9+3+3+9+9 = 33/45
- Adjusted: (33/45) x 45 = **33.0/45 (73.3%)**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | On-chain withdrawal via LRTWithdrawalManager. Three-step process: (1) request withdrawal (exchange rate locked), (2) off-chain service undelegates within 24h, (3) claim after 7-day hold. Buffer pool allows 2-day fast withdrawal for small amounts. Pause is protocol-wide via multisig. No address-level blocking documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [Withdrawal docs](https://kelp.gitbook.io/kelp/explore-rseth/rseth-withdrawal), [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | With TVL at ~$47M, in-protocol redemption through EigenLayer can process substantial exits. Uniswap V3 WSTETH/RSETH pair has ~$776K daily volume. Given the dramatically reduced TVL, liquidity is adequate for current size. At peak TVL ($6.4B) this would have been a concern. | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama TVL, [P3] CoinGecko volume |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | Yes. During the April 2025 incident, withdrawals were paused for approximately 8 days (April 30 - May 8, 2025). This was a precautionary freeze, not a liquidity issue. Withdrawals resumed without loss. | 3 | 3 | Non-Improvable | [P2] [Aave Freeze](https://governance.aave.com/t/rseth-precautionary-freezing-30-04-2025/21925) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | No evidence of withdrawal caps that restrict exits. The buffer pool allows smaller fast withdrawals. No history of caps being used to block exits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Withdrawal docs](https://kelp.gitbook.io/kelp/explore-rseth/rseth-withdrawal) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | During the April 2025 incident, rsETH was frozen across Aave for 8 days. Secondary market liquidity remained accessible on Uniswap but volumes are modest (~$776K/day). The incident caused stress but access remained via DEX swaps. The protocol has been tested but with notable disruption. | 3 | 3 | Non-Improvable | [P2] [Aave Freeze](https://governance.aave.com/t/rseth-precautionary-freezing-30-04-2025/21925), [P3] CoinGecko |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | Yes. EigenLayer imposes a 7-day withdrawal queue. Kelp adds processing time for total 7-10 days. This is the stated withdrawal period. Less than 10% of assets effectively exceed the stated 7-10 day window under normal conditions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Withdrawal docs](https://kelp.gitbook.io/kelp/explore-rseth/rseth-withdrawal) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Most users can exit via in-protocol redemption (7-10 days). Secondary markets (Uniswap) are optional for faster exit. Uniswap V3 WSTETH/RSETH has $776K daily volume -- sufficient for small exits but thin for large positions. | 3 | 9 | **Improvable** | [P3] CoinGecko, [P1] [DeFi Integration docs](https://kelp.gitbook.io/kelp/explore-rseth/defi-integration) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | At current TVL of ~$47M, the $776K daily DEX volume represents ~1.7% of TVL per day. Depth supports ~3-10% of TVL without major impact -- adequate for staggered exits. However, at historical peak TVL this would have been severely insufficient. | 3 | 9 | **Improvable** | [P3] CoinGecko volume, [P3] DeFiLlama TVL |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | The 99% TVL decline from $6.4B to $47M already represents a near-complete bank run that was handled without permanent losses. The protocol's withdrawal design (7-day EigenLayer queue) creates natural rate-limiting. Rapid mass exit would cause queues but not expected permanent haircuts. | 3 | 3 | Non-Improvable | [P3] DeFiLlama TVL history |

**Liquidity Subtotal:**
- Raw scores: 9+9+3+9+3+9+3+3+3 = 51/81
- Adjusted: (51/81) x 45 = **28.3/45 (62.9%)**

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | rsETH is non-rebasing and appreciates vs ETH. During the April 2025 infinite mint, the rsETH/ETH exchange rate was protected by circuit breakers. However, rsETH was frozen on Aave for 8 days and trading on DEXs may have experienced temporary discount. The incident was an actual stress test with disruption but no permanent impairment. Protocol has been tested under real stress. | 3 | 3 | Non-Improvable | [P2] [Aave Freeze](https://governance.aave.com/t/rseth-precautionary-freezing-30-04-2025/21925), [P3] CoinGecko |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | rsETH is fully backed by ETH and ETH-denominated LSTs. No leverage. Strategy is low-beta (rsETH moves with ETH). Liquidation risk is negligible for the protocol itself (users may face liquidation on Aave/other platforms if using rsETH as collateral). | 9 | 9 | Non-Improvable (optimal) | [P1] Protocol design |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | rsETH yield comes from staking/restaking, not from a rate model. No utilization-based rate curve. TVL shifts don't affect yield mechanics directly. The 99% TVL decline did not cause yield model failure. | 9 | 9 | Non-Improvable (optimal) | [P1] Protocol design |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | No published stress testing or scenario analysis. The April 2025 incident was real-world testing that passed (circuit breakers worked). But no formal high-volatility modeling exists. | 1 | 9 | **Improvable** | [P1] No published scenarios |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | No leverage in the protocol itself. rsETH is a receipt token. Sharp ETH price moves affect USD value but not the rsETH/ETH exchange rate. No forced liquidation mechanism within the protocol. | 9 | 9 | Non-Improvable (optimal) | [P1] Protocol design |

**Market Subtotal:**
- Raw scores: 3+9+9+1+9 = 31/45
- Adjusted: (31/45) x 45 = **31.0/45 (68.9%)**

---

**Strategy Total: 36.4 + 30.0 + 30.0 + 33.0 + 28.3 + 31.0 = 188.7/270 (69.9%)**

---

### OPERATIONS (30% Weight) -- Score: 132.6/270 (49.1%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | No on-chain tokenholder governance. KERNEL governance is described as "coming soon." Currently, protocol changes are controlled by the 6/8 External Admin multisig with 10-day timelock. While the multisig is well-structured, there is no binding on-chain governance process. | 1 | 9 | **Improvable** | [P2] [KernelDAO Forum](https://forum.kerneldao.com/t/kerneldao-governance-process/27), [P1] [Tokenomics](https://kerneldao.gitbook.io/kernel/getting-started/usdkernel-tokenomics) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- No governance token voting currently active. KERNEL token exists but governance voting is "coming soon." Governance concentration is captured by S-KM-01/03 for multisig. | N/A | N/A | N/A | - |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. 10-day timelock on all major upgrades via TimelockController. EXECUTOR_ROLE is set to zero address (anyone can execute after delay). PROPOSER_ROLE is the 6/8 External Admin multisig. This is strong. No veto mechanism beyond cancellation by proposer. | 9 | 9 | Non-Improvable (optimal) | [P0] [TimelockController](https://etherscan.io/address/0x49bD9989E31aD35B0A62c20BE86335196A3135B1) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A -- LST product, no strategy manager to replace. | N/A | N/A | N/A | - |

**Governance Subtotal (2 of 4 scored):**
- Raw scores: 1+9 = 10/18
- Adjusted: (10/18) x 67.5 = **37.5/67.5 (55.6%)**
- N/A: O-G-02, O-G-04

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Co-founders Dheeraj Borra (IIT Kharagpur, UT Austin, Facebook, PayPal, LinkedIn, Stader Labs co-founder) and Amitej Gajjala (IIT Madras, IIM Calcutta, A.T. Kearney, Swiggy, Stader Labs co-founder) are publicly identified with extensive track records. Operating under KernelDAO. Headquartered in Bengaluru, India. | 9 | 9 | Non-Improvable (optimal) | [P4] [Tracxn](https://tracxn.com/d/companies/kelp-dao), [P4] [IQ.wiki Dheeraj](https://iq.wiki/wiki/dheeraj-borra), [P4] [IQ.wiki Amitej](https://iq.wiki/wiki/amitej-gajjala) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Team size is unclear from public sources. LlamaRisk noted Discord has "two moderators, eight team members." The $9M fundraise suggests ability to hire, but team size and redundancy across critical systems is not well documented. Small team risk is present. | 3 | 9 | **Source Missing** | [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth), [P4] [Tracxn](https://tracxn.com/d/companies/kelp-dao) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Operates as KernelDAO -- a DAO structure with publicly identified co-founders (Dheeraj Borra, Amitej Gajjala), named investors ($9M from SCB Capital, Laser Digital/Nomura, etc.), and headquarters in Bengaluru, India per Tracxn. No formal registered entity name published in protocol docs, but DAO structure and jurisdiction are identifiable. Consistent with other DAO protocols (Lombard, Puffer) that have partial entity disclosure. | 3 | 9 | **Improvable** | [P4] [Tracxn](https://tracxn.com/d/companies/kelp-dao), [P1] [KernelDAO](https://kerneldao.gitbook.io/kernel) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known investigations or regulatory actions against Kelp DAO or KernelDAO. | 9 | 9 | Non-Improvable (optimal) | [P4] News search, no findings |
| O-TL-05 | Is there an on-call and incident response process for core teams? | No documented on-call or incident response process. The April 2025 response was effective (4.5 hours from incident to public update), suggesting informal processes exist, but nothing is documented or formalized. | 1 | 9 | **Improvable** | [P1] No documentation found |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Discord community exists. During the April 2025 incident, the team issued a public update within ~4.5 hours. Response to DeFi integrators (Aave, Morpho) was coordinated. However, no structured support channel or SLA is documented. | 3 | 9 | **Improvable** | [P2] [Aave Freeze](https://governance.aave.com/t/rseth-precautionary-freezing-30-04-2025/21925) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. $9M private sale (May 2024) with disclosed investors: SCB Capital (lead), Laser Digital/Nomura (lead), Bankless Ventures, Hypersphere, Draper Dragon, DACM, Cypher Capital, ArkStream, Cluster Capital, GSR, Longhash, Side Door Ventures, NOIA Capital, HTX Ventures, Avid3, ViaBTC Capital, DWF Ventures, Coinseeker. | 9 | 9 | Non-Improvable (optimal) | [P4] [Yahoo Finance](https://finance.yahoo.com/news/kelp-dao-raises-9-million-090008172.html), [P1] [KernelDAO Blog](https://blogs.kerneldao.com/blog/kelp-dao-secures-9-million-in-private-sale-to-propel-restaking-innovation) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | N/A -- LST product, not a managed vault. | N/A | N/A | N/A | - |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | N/A -- LST product, not a managed vault. However, it is worth noting the founders also co-founded Stader Labs (ETHx) which has not had collateral loss events. | N/A | N/A | N/A | - |

**Team & Legal Subtotal (7 of 9 scored):**
- Raw scores: 9+3+3+9+1+3+9 = 37/63
- Adjusted: (37/63) x 67.5 = **39.6/67.5 (58.7%)**
- N/A: O-TL-08, O-TL-09

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Documentation exists across kelp.gitbook.io and kerneldao.gitbook.io but is fragmented. Core architecture is described at high level. The LlamaRisk assessment provides more detail than the protocol's own docs. Risk disclosures are minimal. Docs appear partially outdated (domain migration from kelpdao.xyz to kerneldao.com). | 3 | 9 | **Improvable** | [P1] [Kelp Gitbook](https://kelp.gitbook.io/kelp), [P1] [Kernel Gitbook](https://kerneldao.gitbook.io/kernel) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Collateral flow (ETH -> DepositPool -> NodeDelegator -> EigenLayer) is documented in protocol docs at high level. The publicly available Bailsec audits (Sep & Dec 2025) extensively document core invariants, deposit/withdrawal mechanics, price calculation flow, and access controls for each contract. Loss scenarios (slashing, depeg) are mentioned in third-party assessments but not systematically mapped in protocol's own docs. Partial documentation exists across multiple sources. | 3 | 9 | **Improvable** | [P1] [Kelp Gitbook](https://kelp.gitbook.io/kelp), [P1] [Bailsec Sep 2025](https://kerneldao.com/kelp/audits/smartcontracts/Bailsec_rsETH_november.pdf), [P1] [Bailsec Dec 2025](https://kerneldao.com/kelp/audits/smartcontracts/Bailsec_rsETH_december_2025.pdf) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. The Kelp Gitbook has a dedicated "rsETH Smart Contracts" page listing all core contracts, multisig addresses, and roles. GitHub README also lists mainnet deployment addresses comprehensively. Cross-chain addresses documented per chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [Kelp Smart Contracts](https://kelp.gitbook.io/kelp/rseth-smart-contracts), [P1] [GitHub](https://github.com/Kelp-DAO/LRT-rsETH) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Roles are documented: DEFAULT_ADMIN_ROLE (6/8 External Admin), OPERATOR_ROLE (2/5 Manager), PROPOSER_ROLE/EXECUTOR_ROLE on timelock. Signer names listed. However, change history is not explicitly tracked in a changelog. | 3 | 9 | **Improvable** | [P1] [Kelp Smart Contracts](https://kelp.gitbook.io/kelp/rseth-smart-contracts) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Chainlink Proof of Reserve Secure Mint integration (post-May 2025) provides on-chain verifiable proof of reserves for the minting function. On-chain contracts are transparent -- all assets verifiable in deposit pool and EigenLayer. No liabilities structure (LST, not lending), so proof-of-liabilities N/A. | 9 | 9 | Non-Improvable (optimal) | [P1] [Chainlink PoR Blog](https://blogs.kerneldao.com/blog/kelp-is-integrating-chainlink-proof-of-reserve-to-help-further-secure-rseth-s-minting-function) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. rsETH (0xA1290d69...) verified as TransparentUpgradeableProxy on Etherscan. LRTDepositPool verified. TimelockController verified. LRTOracle verified. All core contracts appear verified on Etherscan. | 9 | 9 | Non-Improvable (optimal) | [P0] [rsETH on Etherscan](https://etherscan.io/address/0xA1290d69c65A6Fe4DF752f95823fae25cB99e5A7), [P0] [DepositPool on Etherscan](https://etherscan.io/address/0x036676389e48133B63a802f8635AD39E752D375D) |

**Documentation Subtotal:**
- Raw scores: 3+3+9+3+9+9 = 36/54
- Adjusted: (36/54) x 67.5 = **45.0/67.5 (66.7%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | KERNEL staking is planned to provide "insurance against potential slashing events" but this is not yet operational (KERNEL TGE was Q2 2025). No current dedicated safety module or backstop exists. | 1 | 9 | **Improvable** | [P1] [KERNEL Tokenomics](https://kerneldao.gitbook.io/kernel/getting-started/usdkernel-tokenomics) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | No treasury data available on DeFiLlama for Kelp or KernelDAO (API returned 400/404). No treasury wallet addresses disclosed in protocol docs. KERNEL token exists but market data suggests modest capitalization. Unable to verify treasury. | 1 | 9 | **Source Missing** | [P3] DeFiLlama treasury API returned error, [P1] No treasury in docs |
| O-FR-03 | What is the estimated operational runway at current burn? | $9M raised in May 2024. Current burn rate unknown. With reduced TVL (~$47M from $6.4B peak), fee revenue is drastically reduced (protocol fee set to 0 post-incident). Runway cannot be estimated without disclosed costs and revenue. | 1 | 9 | **Improvable** | [P4] [Yahoo Finance fundraise](https://finance.yahoo.com/news/kelp-dao-raises-9-million-090008172.html) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | TVL declined ~99% from $6.4B peak (Jan 2025) to ~$47M (Mar 2026). This represents a massive outflow. The April 2025 incident caused a temporary freeze but no permanent losses. Revenue likely declined proportionally with TVL. No buffers were depleted. | 1 | 3 | Non-Improvable | [P3] [DeFiLlama Kelp](https://defillama.com/protocol/kelp) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Partially. rsETH contracts are on-chain and withdrawals are permissionless via LRTWithdrawalManager. However, the off-chain AWS Lambda service is critical for processing withdrawals (undelegation from EigenLayer). If the team disappears, this service would stop, and users would need direct contract interaction. The 6/8 External Admin multisig includes external signers who could potentially manage the protocol. | 3 | 9 | **Improvable** | [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth), [P1] On-chain contract architecture |

**Financial Resilience Subtotal:**
- Raw scores: 1+1+1+1+3 = 7/45
- Adjusted: (7/45) x 67.5 = **10.5/67.5 (15.6%)**

---

**Operations Total: 37.5 + 39.6 + 45.0 + 10.5 = 132.6/270 (49.1%)**

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 67 | 99 | 121.8 | 180 | 67.7% |
| | Key Management (7 of 8 Q scored) | 49 | 63 | 140.0 | 180 | 77.8% |
| | **Security Subtotal** | | | **261.8** | **360** | **72.7%** |
| **Strategy** | Protocol Mechanics (7 of 9 Q scored) | 51 | 63 | 36.4 | 45 | 80.9% |
| | Collateral (4 Q) | 24 | 36 | 30.0 | 45 | 66.7% |
| | Infra Counterparty (8 Q) | 48 | 72 | 30.0 | 45 | 66.7% |
| | Protocol Counterparty (5 Q) | 33 | 45 | 33.0 | 45 | 73.3% |
| | Liquidity (9 Q) | 51 | 81 | 28.3 | 45 | 62.9% |
| | Market (5 Q) | 31 | 45 | 31.0 | 45 | 68.9% |
| | **Strategy Subtotal** | | | **188.7** | **270** | **69.9%** |
| **Operations** | Governance (2 of 4 Q scored) | 10 | 18 | 37.5 | 67.5 | 55.6% |
| | Team & Legal (7 of 9 Q scored) | 37 | 63 | 39.6 | 67.5 | 58.7% |
| | Documentation (6 Q) | 36 | 54 | 45.0 | 67.5 | 66.7% |
| | Financial Resilience (5 Q) | 7 | 45 | 10.5 | 67.5 | 15.6% |
| | **Operations Subtotal** | | | **132.6** | **270** | **49.1%** |
| **TOTAL** | | | | **583.1** | **900** | **64.8%** |

---
