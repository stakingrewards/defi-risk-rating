# Kelp DAO - rsETH Risk Rating

**Rating Date**: 2026-04-20
**Final Grade**: D
**Total Score**: 357.9/900 points (Deal Breaker cap applied)
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 175.0/360 (48.6%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | 10 audit reports from 4 firms (Sigma Prime x6, Code4rena x1, MixBytes x1, Bailsec x2) covering core smart contracts. However, the deployment configuration of the LayerZero OFT bridge adapter -- specifically the 1-of-1 DVN setup -- was NOT in any audit scope. The bridge config was the attack surface that was exploited. Code audits existed but config review was absent. Per updated S-SC-01 criteria: "audits must cover not just contract code but the deployed configuration." | 3 | 9 | **Improvable** | [P1] [Kelp Audits](https://kerneldao.gitbook.io/kernel/getting-started/kelp/audits), [P0] [banteg forensics](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62) showing 1-of-1 DVN config not audited |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Sigma Prime (Tier-0) conducted 6 audits including most recent core contract reviews. Bailsec (Tier-2 equivalent) conducted 2 audits (Sep/Dec 2025). Code4rena is a reputable contest platform. Most recent audit by a Tier-0 firm. | 9 | 9 | Non-Improvable (optimal) | [P1] [Sigma Prime Reports](https://kerneldao.com/kelp/audits/smartcontracts/SigmaPrime.pdf), [P1] [Bailsec Reports](https://kerneldao.com/kelp/audits/smartcontracts/Bailsec_rsETH_december_2025.pdf) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | The April 2025 LRTOracle upgrade introduced the infinite mint bug without prior audit. Post-incident, the team established a robust audit cadence: Sigma Prime June 2025, Bailsec Sep/Dec 2025. However, the LayerZero OFT bridge adapter configuration was never audited as a "deployment configuration upgrade." The bridge config was set up once and never independently reviewed. | 3 | 9 | **Improvable** | [P1] [Sigma Prime June 2025](https://kerneldao.com/kelp/audits/smartcontracts/SigmaPrime_6.pdf), [P1] [Bailsec Dec 2025](https://kerneldao.com/kelp/audits/smartcontracts/Bailsec_rsETH_december_2025.pdf) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Across 10 audits: Bailsec Sep 2025: 3 High found, 1 resolved, 2 acknowledged (no fix applied). Sigma Prime June 2025: 1 High closed as design choice. Pattern of acknowledging but not fixing some High findings persists. Bailsec Dec 2025: 0 High, 0 Medium, showing codebase maturation. | 3 | 9 | **Improvable** | [P1] [Bailsec Sep 2025](https://kerneldao.com/kelp/audits/smartcontracts/Bailsec_rsETH_november.pdf) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | All core contracts use TransparentUpgradeableProxy. Upgrades require 6/8 external admin multisig through TimelockController with 10-day minimum delay. ProxyAdmin owned by TimelockController. Strong upgrade constraints. | 9 | 9 | Non-Improvable (optimal) | [P0] [TimelockController](https://etherscan.io/address/0x49bD9989E31aD35B0A62c20BE86335196A3135B1) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | **TWO MAJOR INCIDENTS**: (1) April 30, 2025: infinite mint bug in LRTOracle (1e36 vs 1e18 scaling). Circuit breakers prevented user fund loss. Tokens burned. Would score Mid (3) on its own. (2) **April 18, 2026: ~$292M bridge exploit**. 116,500 rsETH drained from LayerZero OFT escrow via forged cross-chain message exploiting 1-of-1 DVN. ~$236M borrowed against unbacked collateral on Aave/Compound/Euler. ~18% of supply now unbacked. No compensation. No post-mortem from KelpDAO as of April 20. Scores HIGH (1): permanent user loss, loss >>2% of TVL, no full compensation, no post-mortem. | 1 | 1 | Non-Improvable | [P0] [Exploit tx](https://etherscan.io/tx/0x1ae232da212c45f35c1525f851e4c41d529bf18af862d9ce9fd40bf709db4222), [P0] [banteg forensics](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62), [P4] [DeFiPrime](https://defiprime.com/kelpdao-rseth-exploit), [P4] [LayerZero statement](https://x.com/LayerZero_Core/status/2046081551574983137) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No confirmed rug-pull. Founded by Dheeraj Borra and Amitej Gajjala (Stader Labs co-founders). Funded by SCB Capital, Laser Digital (Nomura), and others ($9M raised). Exploit was an external attack, not team misconduct. | 9 | 9 | Non-Improvable (optimal) | [P4] [Yahoo Finance](https://finance.yahoo.com/news/kelp-dao-raises-9-million-090008172.html) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No evidence of timelock reductions. The 10-day delay has been consistent. | 9 | 9 | Non-Improvable (optimal) | [P0] [TimelockController](https://etherscan.io/address/0x49bD9989E31aD35B0A62c20BE86335196A3135B1) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active Immunefi bug bounty since August 2, 2024. Max payout $250K. Scope covers rsETH, LRTDepositPool, LRTOracle, LRTWithdrawalManager, LRTUnstakingVault, NodeDelegator, FeeReceiver, LRTConverter. KYC required. Last updated March 21, 2025. Note: bridge adapter configuration was likely not in Immunefi scope. | 9 | 9 | Non-Improvable (optimal) | [P1] [Immunefi Kelp DAO](https://immunefi.com/bug-bounty/kelp-dao/scope/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | No evidence of structured monitoring or alerting system. No mention of Hypernative, Blockaid, or similar providers in docs. The April 2025 circuit breaker suggests some automated controls exist, but monitoring configuration is undocumented. The April 2026 exploit was detected by external analysts, not by internal monitoring. Kelp paused contracts ~46 minutes after the initial mint -- adequate but not indicative of proactive detection. | 1 | 9 | **Source Missing** | [P1] No monitoring mentioned in docs, [P4] [DeFiPrime](https://defiprime.com/kelpdao-rseth-exploit) noting 46-min response time |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Circuit breakers exist for exchange rate anomalies (demonstrated April 2025). However, no circuit breaker existed on the bridge adapter or OFT escrow. The entire $116.5K rsETH escrow was drained in a single transaction with no rate limit, no anomaly detection, and no automatic pause. The bridge -- which held more value than many standalone protocols -- had zero automated safety controls. | 1 | 9 | **Improvable** | [P0] [Exploit tx showing single-tx full drain](https://etherscan.io/tx/0x1ae232da212c45f35c1525f851e4c41d529bf18af862d9ce9fd40bf709db4222) |

**Smart Contract Security Subtotal:**
- Raw scores: 3+9+3+3+9+1+9+9+9+1+1 = 57/99
- Adjusted: (57/99) x 180 = **103.6/180 (57.6%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Admin/upgrade rights held by 6/8 External Admin multisig (0xb3696a817D01C8623E66D156B6798291fa10a46d) which is the PROPOSER_ROLE on TimelockController. Signers are publicly identified industry figures. However, the OFT bridge adapter owner (0x9Fc47d6A2F5A1EFd8BaF475E1873c76D9b28dDFD) on Unichain was a separate entity that controlled the DVN configuration -- and this configuration was the attack vector. | 3 | 9 | **Improvable** | [P0] [Safe Address](https://etherscan.io/address/0xb3696a817D01C8623E66D156B6798291fa10a46d), [P0] [banteg forensics](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | Core contracts: No. Upgrading requires 6/8 multisig + 10-day timelock. However, the OFT bridge adapter's DVN configuration was 1-of-1 -- effectively a single key (the DVN's signing key) could authorize release of the entire escrow (~$292M). This single point of failure was the exploit vector. The core protocol meets Low (9) but the bridge infrastructure fails catastrophically. Scores Mid (3) because the bridge escrow held user funds and a single key compromise released them. | 3 | 9 | **Improvable** | [P0] [TimelockController](https://etherscan.io/address/0x49bD9989E31aD35B0A62c20BE86335196A3135B1), [P0] [banteg forensics showing 1-of-1 DVN](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | External Admin is 6/8 with 3+ independently verified signers (named individuals from different organizations). The Manager multisig is 2/5 and the Admin multisig is 3/5. The critical upgrade path (6/8 External Admin) is strong. However, the bridge adapter was controlled by a separate owner without equivalent multisig protections. | 3 | 9 | **Improvable** | [P1] [Kelp Docs](https://kelp.gitbook.io/kelp/rseth-smart-contracts), [P0] [banteg forensics](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause capability demonstrated during both incidents. Contracts currently paused across all chains. The rsETH token has a `transfersBlockedUntil` mapping that was used to freeze the attacker's address (demonstrated in banteg forensics). Pause appears protocol-wide and controlled by multisig. However, current pause is indefinite with no disclosed timeline for resumption. | 3 | 9 | **Improvable** | [P0] [banteg forensics showing TransfersBlocked](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62), [P0] On-chain contract state |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Core staking assets: Yes. 100% held in on-chain non-custodial contracts (LRTDepositPool, NodeDelegator, EigenLayer strategies). However, ~116,500 rsETH (~18% of supply) that was in the bridge escrow is now gone -- drained by the attacker and converted to ETH/WBTC via Aave/Compound. The remaining ~$1.55B TVL on Ethereum is intact in non-custodial contracts. | 3 | 9 | **Improvable** | [P0] [LRTDepositPool](https://etherscan.io/address/0x036676389e48133B63a802f8635AD39E752D375D), [P3] [DeFiLlama TVL $1.55B](https://api.llama.fi/protocols) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | User funds are in distinct smart contracts. The bridge escrow was a separate contract holding tokens for cross-chain bridging. Clear on-chain segregation for core operations. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain contract architecture |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- rsETH is an LST/LRT, not a managed vault strategy. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No documented playbook. The April 2026 response was 46 minutes from exploit to contract pause -- adequate but reactive. The team used a GnosisSafe to freeze the attacker's address, preventing a second tranche (nonce 309), showing some prepared response capability. However, no formal playbook, tabletop exercise, or key rotation procedure is documented. | 1 | 9 | **Improvable** | [P0] [banteg forensics showing Safe freeze at 18:23 UTC](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62) |

**Key Management Subtotal (7 of 8 scored):**
- Raw scores: 3+3+3+3+3+9+1 = 25/63
- Adjusted: (25/63) x 180 = **71.4/180 (39.7%)**
- N/A: S-KM-07

**Validation:** 25/63 = 0.3968; 0.3968 x 180 = 71.4. Confirmed.

**Security Total: 103.6 + 71.4 = 175.0/360 (48.6%)**

---

### STRATEGY (30% Weight) -- Score: 84.3/270 (31.2%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield comes from: (1) ETH staking rewards (consensus + execution layer), (2) EigenLayer restaking rewards from AVSs. Both align with rsETH's stated mandate as a liquid restaking token. Yield sources are organic and mandate-aligned. No breakdown of % contributions publicly available. | 3 | 9 | **Improvable** | [P1] [Kelp Docs](https://kerneldao.gitbook.io/kernel) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | The bridge exploit has already caused permanent loss (~$292M) well beyond any yield consideration. ~18% of rsETH supply is unbacked, meaning holders of bridged rsETH face structural loss. Contracts are paused - no yield is being generated. This is not a tail shock scenario; loss has already materialized in non-tail conditions due to material dependence on a fragile bridge counterparty. | 1 | 9 | **Improvable** | [P0] [Exploit evidence](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62), [P1] Protocol design |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage. rsETH represents 1:1 staked/restaked ETH. Effective leverage is 1.0x. | 9 | 9 | Non-Improvable (optimal) | [P1] Protocol design |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- LST product, no lending/leverage positions to liquidate. | N/A | N/A | N/A | - |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | **YES -- catastrophic loss**. April 18, 2026: ~$292M permanent loss via bridge exploit. This represents ~14% of peak TVL ($2.09B). No compensation as of April 20. Scores HIGH (1): uncompensated permanent-loss event, losses far above 0.5% of peak strategy TVL. The April 2025 infinite mint was resolved without user loss, but the April 2026 bridge exploit is a clear High (1). | 1 | 1 | Non-Improvable | [P0] [Exploit tx](https://etherscan.io/tx/0x1ae232da212c45f35c1525f851e4c41d529bf18af862d9ce9fd40bf709db4222), [P4] [DeFiPrime](https://defiprime.com/kelpdao-rseth-exploit) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | N/A -- LST product, not a vault. | N/A | N/A | N/A | - |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yield is currently zero - contracts are paused, protocol fee is 0, and no staking/restaking rewards are flowing to holders. The protocol is non-functional. While the underlying yield mechanics (ETH staking + EigenLayer restaking) are sustainable in theory, the protocol cannot generate or distribute yield in its current paused state. Sustainability is unknown given the $292M loss overhang and uncertain recovery path. | 1 | 9 | **Improvable** | [P1] Protocol mechanics |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Currently NO -- contracts are paused across all chains. Withdrawals are blocked. Secondary market rsETH is trading at ~$1,921, down ~22% from pre-exploit ~$2,543. Even when/if contracts resume, the ~18% supply unbacking creates structural uncertainty about redemption value. For mainnet rsETH holders (whose backing is intact), slippage is currently severe due to the pause. | 1 | 9 | **Improvable** | [P3] [CoinGecko rsETH price ~$1,921](https://www.coingecko.com/en/coins/kelp-dao-restaked-eth), [P0] Contracts paused on-chain |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | rsETH is designed as non-rebasing and appreciating vs ETH. However, the rsETH/ETH exchange rate has effectively inverted - rsETH is trading at ~$1,921 vs ETH at ~$2,543 (~24% discount). The peg mechanism is broken for the ~18% of unbacked supply, and the depeg persists across all markets. While this isn't a traditional "spread trade," the receipt token's value relationship to its underlying has demonstrably broken down. | 1 | 3 | Non-Improvable | [P1] Protocol design |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | N/A -- LST product. Users deposit directly. No automated allocation layer. | N/A | N/A | N/A | - |

**Protocol Mechanics Subtotal (7 of 10 scored):**
- Raw scores: 3+1+9+1+1+1+1 = 17/63
- Adjusted: (17/63) x 45 = **12.1/45 (26.9%)**
- N/A: ST-PM-04, ST-PM-06, ST-PM-10

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Accepted: ETH (native), stETH (Lido, A-/847.5 SR rating), ETHx (Stader, unrated but smaller LST). All are Ethereum staking derivatives or native ETH -- established large-cap assets. | 9 | 9 | Non-Improvable (optimal) | [P1] [Kelp Docs](https://kerneldao.gitbook.io/kernel), [P0] [LRTDepositPool](https://etherscan.io/address/0x036676389e48133B63a802f8635AD39E752D375D) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | The underlying collateral (ETH, stETH, ETHx) has remained stable. However, rsETH itself is now trading at ~$1,921 vs ETH at ~$2,543 -- a ~24% depeg lasting more than 48 hours (exploit was April 18, still depegged as of April 20). This is a >10% depeg lasting more than 7 days (ongoing). | 1 | 3 | Non-Improvable | [P3] [CoinGecko rsETH](https://www.coingecko.com/en/coins/kelp-dao-restaked-eth), [P0] On-chain price data |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Three operators (Kiln, Allnodes, Luganodes) with RAVER scores >96%. No validators have been slashed. ~5,200+ validators diversified across operators. KERNEL staking planned for insurance. Some diversification but no explicit insurance buffer. | 3 | 9 | **Improvable** | [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth) |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | Prior to exploit: significant rsETH supply existed on 10+ L2 chains via LayerZero OFT bridges. The bridge used 1-of-1 DVN verification on 11 of 12 routes (only Manta had 2 DVNs). A single verifier compromise was sufficient to drain entire escrow. Post-exploit: all L2 chain TVL is $0 (paused), but the structural damage is done -- ~116,500 rsETH (~18% of supply) was drained from bridge escrow. Bridge uses 1-of-1 verification AND bridged share exceeded 10%. Scores HIGH (1). | 1 | 9 | **Improvable** | [P0] [banteg forensics showing 1-of-1 DVN across nearly all routes](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62), [P4] [LayerZero statement](https://x.com/LayerZero_Core/status/2046081551574983137) |

**Collateral Subtotal:**
- Raw scores: 9+1+3+1 = 14/36
- Adjusted: (14/36) x 45 = **17.5/45 (38.9%)**

---

#### Infra Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Core: Ethereum (Tier-0), EigenLayer (Tier-0 protocol), Chainlink oracles (Tier-0), Kiln/Allnodes/Luganodes validators. Bridge: LayerZero (Tier-1 bridge tier per SR list). The LayerZero dependency proved catastrophic. Not all dependencies are Tier-0/1 when considering the bridge configuration (1-of-1 DVN is below any tier). | 3 | 9 | **Improvable** | [P0] Contract addresses, [P0] [banteg forensics](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62) |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | LRTOracle uses internal price calculations with ChainlinkPriceOracle as a component. Post-April 2025, Chainlink PoR Secure Mint adds redundancy for minting. stETH is hardcoded 1:1 (no oracle fallback). ETHx uses internal Stader exchange rate. Single oracle path per asset with hardcoded pricing for stETH. | 3 | 9 | **Improvable** | [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | No SOC 2 or ISO27001 certifications disclosed for Kelp/KernelDAO. LayerZero Labs stated they are "in the final stages of SOC2 audit/verification" in their post-exploit statement. No certification for Kelp's own off-chain infra. | 3 | 9 | **Source Missing** | [P4] [LayerZero statement mentioning SOC2](https://x.com/LayerZero_Core/status/2046081551574983137) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | **Catastrophic failure**. The LayerZero bridge infrastructure -- a critical dependency -- was compromised on April 18, 2026, enabling the $292M exploit. The DVN's RPC infrastructure was poisoned by a state-level attacker, and the 1-of-1 config meant there was no fallback. This is the definition of "past incidents caused prolonged inability to access or withdraw or contributed to losses." Contracts remain paused 48+ hours later. | 1 | 3 | Non-Improvable | [P0] [Exploit tx](https://etherscan.io/tx/0x1ae232da212c45f35c1525f851e4c41d529bf18af862d9ce9fd40bf709db4222), [P4] [LayerZero statement](https://x.com/LayerZero_Core/status/2046081551574983137) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Ethereum (Tier-0) has had no chain halt or consensus failure >30 min in the last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P3] Ethereum network status |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | No slashing events affecting Kelp validators. All three operators maintain RAVER scores >96%. | 9 | 9 | Non-Improvable (optimal) | [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth) |
| ST-IC-07 | Are validators diverse geographically and by operator? | Three independent operators: Kiln (France), Allnodes (Ukraine), Luganodes (Switzerland). No single operator >50%. Geographic diversity across Western Europe, Eastern Europe, and Central Europe. | 9 | 9 | Non-Improvable (optimal) | [P1] [Kelp Docs](https://kelp.gitbook.io/kelp/rseth-smart-contracts) |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | **YES -- demonstrated**. A single DVN compromise blocked ALL withdrawals (contracts paused) AND caused ~$292M in losses. The 1-of-1 DVN was a single point of failure that caused exactly this scenario. Even beyond the DVN, operators must call unlockQueue for withdrawals, and off-chain EigenLayer undelegation services are required. | 1 | 9 | **Improvable** | [P0] [banteg forensics](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62), [P0] Contracts paused on-chain |
| ST-IC-09 | How robust is the cross-chain messaging or bridge verification setup? | **1-of-1 DVN on 11 of 12 routes**. Only Manta (EID 30217) had requiredDVNCount=2. All other routes (Arbitrum, Base, Scroll, Linea, Unichain, etc.) used a single LayerZero Labs DVN as the sole verifier. This directly contradicts LayerZero's own multi-DVN recommendation. LayerZero has stated they previously communicated multi-DVN best practices to KelpDAO, who chose 1-of-1. Scores HIGH (1): messages accepted on attestation of a single verifier. | 1 | 9 | **Improvable** | [P0] [banteg forensics showing all route configs](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62), [P4] [LayerZero statement](https://x.com/LayerZero_Core/status/2046081551574983137) |
| ST-IC-10 | Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting? | **NO**. The entire escrow balance (~116,723 rsETH) was drained in a SINGLE transaction. No per-tx caps, no time-windowed limits, no anomalous release detection, no automatic pause. The adapter held 116,723 rsETH one block before and 223 rsETH after the exploit. A single valid message drained the entire escrow. | 1 | 9 | **Improvable** | [P0] [banteg forensics showing balance drop from 116,723 to 223](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62) |
| ST-IC-11 | Is the off-chain verification infrastructure resilient to data-source manipulation? | **NO -- this was the exact attack vector**. Per LayerZero's statement: the attacker compromised 2 independent RPC nodes used by the DVN, swapped out binaries with malicious versions that delivered fake data only to the DVN while telling truth to monitoring. Then DDoS'd uncompromised RPCs to force failover to poisoned endpoints. The DVN had no cross-validation that detected the manipulation. Self-destructing malware cleaned up evidence. Verification relied on data sources that were simultaneously compromised. | 1 | 9 | **Improvable** | [P4] [LayerZero statement detailing RPC poisoning attack](https://x.com/LayerZero_Core/status/2046081551574983137) |

**Infra Counterparty Subtotal:**
- Raw scores: 3+3+3+1+9+9+9+1+1+1+1 = 41/99
- Adjusted: (41/99) x 45 = **18.6/45 (41.4%)**

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Collateral deployed into EigenLayer (Tier-0 protocol) via NodeDelegator contracts. Staking via Kiln, Allnodes, Luganodes. All Tier-0/1 venues for core operations. | 9 | 9 | Non-Improvable (optimal) | [P0] [NodeDelegator contracts](https://github.com/Kelp-DAO/LRT-rsETH) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | No specific revenue-share arrangements disclosed. Protocol fee set to 0 post-April 2025. No apparent conflict documentation. | 3 | 9 | **Source Missing** | [P1] No disclosure in docs |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | EigenLayer is the sole restaking counterparty. No documented per-counterparty caps or rebalancing rules beyond operator allocation. | 3 | 9 | **Improvable** | [P1] [GitHub README](https://github.com/Kelp-DAO/LRT-rsETH) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Normal operations: 7-10 days via EigenLayer withdrawal queue. Current status: **IMPOSSIBLE** -- contracts are paused. No withdrawals can be processed. Timeline for resumption unknown. | 1 | 9 | **Improvable** | [P0] Contracts paused on-chain, [P1] [Withdrawal docs](https://kelp.gitbook.io/kelp/explore-rseth/rseth-withdrawal) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | All three node operators (Kiln, Allnodes, Luganodes) disclosed by name with performance metrics. EigenLayer operator assignments documented. | 9 | 9 | Non-Improvable (optimal) | [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth) |

**Protocol Counterparty Subtotal:**
- Raw scores: 9+3+3+1+9 = 25/45
- Adjusted: (25/45) x 45 = **25.0/45 (55.6%)**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | On-chain withdrawal via LRTWithdrawalManager exists. However, contracts are CURRENTLY PAUSED across all chains with no timeline for resumption. Withdrawals are completely blocked. This is not a temporary pause -- 18% of supply is unbacked and the resolution path is unclear. | 1 | 9 | **Improvable** | [P0] Contracts paused on-chain, [P1] [Withdrawal docs](https://kelp.gitbook.io/kelp/explore-rseth/rseth-withdrawal) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Core Ethereum TVL (~$1.55B) backing is intact per DeFiLlama. However, ~18% of total rsETH supply is unbacked. In-protocol redemption cannot serve 100% of rsETH holders because there is a structural deficit of ~116,500 rsETH worth of backing. For mainnet rsETH holders, the backing is there, but the question of whether bridged-chain rsETH holders can redeem is unresolved. | 3 | 9 | **Improvable** | [P3] [DeFiLlama Kelp TVL $1.55B](https://api.llama.fi/protocols), [P0] [banteg forensics](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | **YES -- multiple and severe**. (1) April 2025: ~8-day freeze during infinite mint incident. (2) April 2026: **ONGOING freeze** -- contracts paused since April 18. No timeline for resumption. Two major freeze events in 12 months. | 1 | 1 | Non-Improvable | [P0] Contracts paused on-chain |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Moot -- contracts are paused. No redemptions possible regardless of caps. When operational, buffer pool allowed fast withdrawals for small amounts. | 1 | 9 | **Improvable** | [P0] Contracts paused on-chain |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | **Catastrophic failure during exploit stress**. rsETH depegged ~22-24% and remains depegged. Contracts paused across all chains. DEX liquidity largely drained. rsETH frozen on all major lending platforms (Aave, Compound, Spark, Fluid, Euler). No exit path currently exists. | 1 | 3 | Non-Improvable | [P3] [CoinGecko rsETH price](https://www.coingecko.com/en/coins/kelp-dao-restaked-eth), [P4] [DeFiPrime](https://defiprime.com/kelpdao-rseth-exploit) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | EigenLayer imposes 7-day withdrawal queue. Kelp adds processing time for 7-10 days total. Under current conditions, the withdrawal period is effectively infinite (paused). | 1 | 9 | **Improvable** | [P0] Contracts paused on-chain |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Secondary market liquidity has evaporated. rsETH daily volume dropped 97.5% to ~$142K per CoinGecko. DEX pools drained. Lending markets frozen. Users effectively have no exit path. | 1 | 9 | **Improvable** | [P3] [CoinGecko showing $142K volume, -97.5%](https://www.coingecko.com/en/coins/kelp-dao-restaked-eth) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | At current TVL ~$1.55B, the $142K daily DEX volume represents <0.01% of TVL per day. Depth is catastrophically thin. Essentially no liquid market for rsETH. | 1 | 9 | **Improvable** | [P3] CoinGecko volume, [P3] DeFiLlama TVL |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | **Bank run is actively occurring**. L2 holders cannot redeem. Mainnet rsETH holders cannot withdraw (paused). ~$8.45B fled Aave in 48 hours. rsETH lending markets frozen across 12+ protocols. The bank-run scenario has materialized and is ongoing. Permanent losses are occurring for unbacked rsETH holders and Aave WETH suppliers. | 1 | 3 | Non-Improvable | [P4] [0xngmi thread showing $6.2B Aave outflows](https://x.com/0xngmi/status/2045830559683768711), [P4] [CoinDesk $13B DeFi TVL drop](https://www.coindesk.com/markets/2026/04/20/defi-tvl-drops-more-than-usd13-billion-in-two-days-following-kelp-dao-hack) |

**Liquidity Subtotal:**
- Raw scores: 1+3+1+1+1+1+1+1+1 = 11/81
- Adjusted: (11/81) x 45 = **6.1/45 (13.6%)**

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | **>10% depeg, ongoing**. rsETH trading at ~$1,921 vs ETH at ~$2,543. That is a ~24% discount to fair value. Depeg has persisted for 48+ hours with no recovery in sight. One Uniswap pair showed rsETH trading between $1,500-$2,500 per the elfa_ai thread. This is a >10% depeg lasting more than 7 days (ongoing). | 1 | 3 | Non-Improvable | [P3] [CoinGecko rsETH](https://www.coingecko.com/en/coins/kelp-dao-restaked-eth), [P4] [elfa_ai thread](https://x.com/elfa_ai/status/2045728756967575895) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Permanent losses have already been crystallized - ~$292M lost through the bridge exploit. While the loss vector was infrastructure failure rather than market moves, the outcome is identical: permanent depositor principal loss. rsETH holders on L2s face structural loss regardless of market conditions. The protocol's current state (paused, 18% unbacked, 24% depegged) means any market movement compounds existing losses. | 1 | 9 | **Improvable** | [P1] Protocol design |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | The protocol is paused and non-functional. While rsETH has no utilization-based rate curve, the current state demonstrates that the yield model completely ceased during this stress event. The exploit triggered 100% utilization on Aave's WETH markets, trapping suppliers. The composability of rsETH across lending markets amplified the stress beyond what any rate model could absorb. | 1 | 9 | **Improvable** | [P1] Protocol design |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | No published stress testing or scenario analysis. The April 2026 incident was "real-world testing" that the protocol catastrophically failed. No formal modeling exists. | 1 | 9 | **Improvable** | [P1] No published scenarios |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | The exploit directly triggered forced liquidation cascades. rsETH used as collateral on Aave V3/V4 and Compound became worthless, crystallizing ~$236M in bad debt. Leveraged rsETH loopers (borrowing WETH against rsETH) are burning equity at 8-9% borrow rates with no ability to unwind. While the protocol itself has no internal liquidation mechanism, its widespread use as collateral means any rsETH depeg directly triggers forced liquidations that crystallize permanent losses for rsETH holders and WETH suppliers. | 1 | 3 | Non-Improvable | [P1] Protocol design |

**Market Subtotal:**
- Raw scores: 1+1+1+1+1 = 5/45
- Adjusted: (5/45) x 45 = **5.0/45 (11.1%)**

---

**Strategy Total: 12.1 + 17.5 + 18.6 + 25.0 + 6.1 + 5.0 = 84.3/270 (31.2%)**

---

### OPERATIONS (30% Weight) -- Score: 98.6/270 (36.5%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | No on-chain tokenholder governance. KERNEL governance described as "coming soon." Protocol changes controlled by 6/8 External Admin multisig with 10-day timelock. Strong multisig but no binding on-chain governance. The bridge adapter configuration that was the exploit vector was controlled outside governance. | 1 | 9 | **Improvable** | [P2] [KernelDAO Forum](https://forum.kerneldao.com/t/kerneldao-governance-process/27) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- No governance token voting currently active. | N/A | N/A | N/A | - |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | 10-day timelock on all major upgrades via TimelockController. EXECUTOR_ROLE is zero address (anyone can execute after delay). Strong. However, this timelock did not cover the bridge adapter configuration. | 9 | 9 | Non-Improvable (optimal) | [P0] [TimelockController](https://etherscan.io/address/0x49bD9989E31aD35B0A62c20BE86335196A3135B1) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A -- LST product, no strategy manager. | N/A | N/A | N/A | - |

**Governance Subtotal (2 of 4 scored):**
- Raw scores: 1+9 = 10/18
- Adjusted: (10/18) x 67.5 = **37.5/67.5 (55.6%)**
- N/A: O-G-02, O-G-04

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Co-founders Dheeraj Borra and Amitej Gajjala are publicly identified with extensive track records (IIT, Facebook, PayPal, Stader Labs). Credible team, though now facing severe reputational damage from the exploit. | 9 | 9 | Non-Improvable (optimal) | [P4] [IQ.wiki Dheeraj](https://iq.wiki/wiki/dheeraj-borra), [P4] [IQ.wiki Amitej](https://iq.wiki/wiki/amitej-gajjala) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Team size unclear. LlamaRisk noted Discord has "two moderators, eight team members." Small team risk present. During the exploit, response time was 46 minutes which suggests limited operational depth. | 3 | 9 | **Source Missing** | [P2] [LlamaRisk](https://llamarisk.com/research/collateral-risk-rseth) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Operates as KernelDAO with headquarters in Bengaluru, India per Tracxn. No formal registered entity name published. | 3 | 9 | **Improvable** | [P4] [Tracxn](https://tracxn.com/d/companies/kelp-dao) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No confirmed formal enforcement actions yet. However, LayerZero Labs confirmed they are "in direct contact with multiple law enforcement agencies around the globe." Aave community members are actively discussing legal action under MiCA/DORA regulations to pursue KelpDAO for the bad debt. The Lazarus Group attribution brings the exploit into the scope of international sanctions enforcement. While no formal action has been filed as of April 20, the legal exposure is material and developing. | 3 | 9 | **Improvable** | [P4] [Aave Governance Forum](https://governance.aave.com/t/rseth-incident-2026-04-18/24481) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | No documented on-call or incident response process. The April 2026 response: Kelp paused contracts 46 minutes after the exploit (per DeFiPrime). The freeze was done via a GnosisSafe tx that blocked the attacker's address. Effective but informal. No formal playbook. | 1 | 9 | **Improvable** | [P0] [banteg forensics showing Safe freeze timing](https://gist.github.com/banteg/705d0284513b74ad20f61d90f5b5de62), [P4] [DeFiPrime](https://defiprime.com/kelpdao-rseth-exploit) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | During the April 2026 exploit, KelpDAO has NOT published a formal post-mortem as of April 20 (48+ hours after the exploit). LayerZero published their statement but KelpDAO itself has been largely silent. This is a significant failure of communication during a critical event. | 1 | 9 | **Improvable** | [P4] No KelpDAO post-mortem as of April 20, [P4] [LayerZero statement](https://x.com/LayerZero_Core/status/2046081551574983137) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. $9M private sale with disclosed investors: SCB Capital (lead), Laser Digital/Nomura (lead), Bankless Ventures, and 15+ other named investors. | 9 | 9 | Non-Improvable (optimal) | [P4] [Yahoo Finance](https://finance.yahoo.com/news/kelp-dao-raises-9-million-090008172.html) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | N/A -- LST product, not a managed vault. | N/A | N/A | N/A | - |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | N/A -- LST product, not a managed vault. The founders also co-founded Stader Labs (ETHx) which has not had collateral loss events. | N/A | N/A | N/A | - |

**Team & Legal Subtotal (7 of 9 scored):**
- Raw scores: 9+3+3+3+1+1+9 = 29/63
- Adjusted: (29/63) x 67.5 = **31.1/67.5 (46.0%)**
- N/A: O-TL-08, O-TL-09

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Documentation exists across kelp.gitbook.io and kerneldao.gitbook.io but is fragmented. Critically, no documentation existed about the bridge DVN configuration or its risk implications. Bridge risk was never disclosed to users or integrators. | 1 | 9 | **Improvable** | [P1] [Kelp Gitbook](https://kelp.gitbook.io/kelp), [P1] [Kernel Gitbook](https://kerneldao.gitbook.io/kernel) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Core collateral flow documented at high level. However, the bridge escrow risk -- that ~116,500 rsETH in escrow could be drained by a single DVN compromise -- was NEVER documented as a loss scenario. The single biggest loss scenario was completely undocumented. | 1 | 9 | **Improvable** | [P1] [Kelp Gitbook](https://kelp.gitbook.io/kelp) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. The Kelp Gitbook has a dedicated "rsETH Smart Contracts" page listing core contracts, multisig addresses, and roles. GitHub README also lists addresses. However, the OFT adapter addresses and DVN configurations were NOT documented. | 3 | 9 | **Improvable** | [P1] [Kelp Smart Contracts](https://kelp.gitbook.io/kelp/rseth-smart-contracts) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Core roles documented: DEFAULT_ADMIN_ROLE, OPERATOR_ROLE, PROPOSER_ROLE. Signer names listed. However, the OFT adapter owner role and DVN configuration authority were undocumented. Change history not tracked in a changelog. | 3 | 9 | **Improvable** | [P1] [Kelp Smart Contracts](https://kelp.gitbook.io/kelp/rseth-smart-contracts) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Chainlink PoR Secure Mint exists for the minting function but failed to prevent the bridge exploit. The bridge escrow - which was the de facto reserve backing L2 rsETH - was drained entirely. rsETH is now partially unbacked (~18% of supply) with no published accounting of the deficit, no clarity on which tokens are backed vs unbacked, and no plan for how the backing gap will be resolved. Proof-of-reserves is functionally broken when reserves don't exist for a material share of supply. | 1 | 9 | **Improvable** | [P1] [Chainlink PoR Blog](https://blogs.kerneldao.com/blog/kelp-is-integrating-chainlink-proof-of-reserve-to-help-further-secure-rseth-s-minting-function) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. Core contracts verified on Etherscan. OFT adapter contracts also verified (per banteg forensics which reads their ABIs). | 9 | 9 | Non-Improvable (optimal) | [P0] [rsETH on Etherscan](https://etherscan.io/address/0xA1290d69c65A6Fe4DF752f95823fae25cB99e5A7) |

**Documentation Subtotal:**
- Raw scores: 1+1+3+3+1+9 = 18/54
- Adjusted: (18/54) x 67.5 = **22.5/67.5 (33.3%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | KERNEL staking planned for insurance but not operational. No current safety module or backstop. Given the ~$292M exploit loss, any backstop would need to be enormous to be meaningful. | 1 | 9 | **Improvable** | [P1] [KERNEL Tokenomics](https://kerneldao.gitbook.io/kernel/getting-started/usdkernel-tokenomics) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | No treasury data available on DeFiLlama (API returned 400). No treasury wallet addresses disclosed. $9M was raised in May 2024. Protocol fee set to 0. No disclosed reserves. Against a $292M loss, any undisclosed reserves would be dwarfed. | 1 | 9 | **Source Missing** | [P3] DeFiLlama treasury API returned error, [P1] No treasury in docs |
| O-FR-03 | What is the estimated operational runway at current burn? | $9M raised in May 2024. Current burn rate unknown. Fee revenue is zero (protocol fee set to 0). Cannot be estimated. Post-exploit legal costs and potential compensation obligations likely increase burn significantly. | 1 | 9 | **Source Missing** | [P4] [Yahoo Finance fundraise](https://finance.yahoo.com/news/kelp-dao-raises-9-million-090008172.html) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | **Catastrophic composability contagion**: The April 2026 exploit caused ~$236M bad debt across Aave ($196M), Compound ($39.4M), and Euler ($840K). Aave TVL dropped ~$8.45B (24%). Total DeFi TVL dropped ~$13.2B. 12+ protocols froze rsETH markets. AAVE token dropped ~20%. ETH utilization on Aave hit 100%. This is the worst composability contagion event in DeFi history by any measure. Revenue effectively zero. Structural TVL collapse. Buffers non-existent. | 1 | 1 | Non-Improvable | [P4] [CoinDesk $13B DeFi TVL drop](https://www.coindesk.com/markets/2026/04/20/defi-tvl-drops-more-than-usd13-billion-in-two-days-following-kelp-dao-hack), [P4] [0xngmi Aave outflows](https://x.com/0xngmi/status/2045830559683768711), [P4] [elfa_ai breakdown](https://x.com/elfa_ai/status/2045728756967575895) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Partially. Core rsETH contracts on Ethereum are on-chain. However, contracts are currently PAUSED and require team action to resume. The 6/8 External Admin multisig includes external signers. Off-chain services (withdrawal processing, EigenLayer undelegation) would stop. Given the current paused state, team disappearance would permanently lock all user funds. | 1 | 3 | Non-Improvable | [P0] Contracts paused on-chain, [P1] On-chain contract architecture |

**Financial Resilience Subtotal:**
- Raw scores: 1+1+1+1+1 = 5/45
- Adjusted: (5/45) x 67.5 = **7.5/67.5 (11.1%)**

---

**Operations Total: 37.5 + 31.1 + 22.5 + 7.5 = 98.6/270 (36.5%)**

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 57 | 99 | 103.6 | 180 | 57.6% |
| | Key Management (7 of 8 Q scored) | 25 | 63 | 71.4 | 180 | 39.7% |
| | **Security Subtotal** | | | **175.0** | **360** | **48.6%** |
| **Strategy** | Protocol Mechanics (7 of 10 Q scored) | 17 | 63 | 12.1 | 45 | 27.0% |
| | Collateral (4 Q) | 14 | 36 | 17.5 | 45 | 38.9% |
| | Infra Counterparty (11 Q) | 41 | 99 | 18.6 | 45 | 41.4% |
| | Protocol Counterparty (5 Q) | 25 | 45 | 25.0 | 45 | 55.6% |
| | Liquidity (9 Q) | 11 | 81 | 6.1 | 45 | 13.6% |
| | Market (5 Q) | 5 | 45 | 5.0 | 45 | 11.1% |
| | **Strategy Subtotal** | | | **84.3** | **270** | **31.2%** |
| **Operations** | Governance (2 of 4 Q scored) | 10 | 18 | 37.5 | 67.5 | 55.6% |
| | Team & Legal (7 of 9 Q scored) | 29 | 63 | 31.1 | 67.5 | 46.0% |
| | Documentation (6 Q) | 18 | 54 | 22.5 | 67.5 | 33.3% |
| | Financial Resilience (5 Q) | 5 | 45 | 7.5 | 67.5 | 11.1% |
| | **Operations Subtotal** | | | **98.6** | **270** | **36.5%** |
| **TOTAL** | | | | **357.9** | **900** | **39.8%** |

---

