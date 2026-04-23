# Puffer Finance - pufETH Risk Rating

**Rating Date**: 2026-04-22
**Final Grade**: BB-
**Total Score**: 735.8/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 311.2/360 (86.4%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | Yes. 23 independent audit reports from 8 firms covering V1 through V5: BlockSec (8 reports), SlowMist (6), Cantina/Spearbit (3), Trail of Bits (1, V2 March 2024), Nethermind (1), Creed (2), Quantstamp (1), Immunefi Boost (1). All reports public in GitHub audits/ directory. Every major upgrade (V1->V2->V5) audited before deployment. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub Audits](https://github.com/PufferFinance/puffer-contracts/tree/master/audits) -- 23 reports |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Cantina/Spearbit (Tier-1) performed the most recent audit covering PufferVaultV5. Trail of Bits (Tier-0) audited V2 (March 2024). Nethermind (Tier-1) also audited V2. Multiple Tier-0/1 auditors in the audit history. | 9 | 9 | Non-Improvable (optimal) | [P1] Cantina-VaultV5.pdf, [P1] ToB-2024-03-pufferfinance.pdf |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. V5 upgrade audited by Cantina/Spearbit before deployment. V2 upgrade audited by Trail of Bits, Nethermind, and Creed. 1-Step Withdrawal Fee Rework audited by BlockSec. Every significant upgrade from V1 through V5 has been audited. | 9 | 9 | Non-Improvable (optimal) | [P1] GitHub audits/ commit history |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | All published reports are final versions indicating remediation review. Creed audit fixes merged in PR #77 (April 30, 2024). No evidence of unresolved critical/high findings across any of the 23 audit reports. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub PR #77](https://github.com/PufferFinance/pufETH/pull/77) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Yes, UUPS proxy. Upgrades controlled via Timelock with hardcoded MINIMUM_DELAY = 7 days (constant, cannot be reduced). Operations Multisig (3-of-6) must queue and wait 7 days. Community Multisig (3-of-6) can execute immediately (0 delay) for emergencies. The 7-day minimum for standard operations exceeds the 24h threshold. | 9 | 9 | Non-Improvable (optimal) | [P0] Timelock.sol: MINIMUM_DELAY = 7 days constant |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploits in 2+ years of operation (since Feb 2024). TVL decline (~$1.84B to ~$71.5M) is organic outflows, not exploit-related. pufETH exchange rate has been monotonically increasing. | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama TVL data, [P4] No entries in rekt.news |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No. Ethereum Foundation grant recipient. Funded by Lemniscap, Brevan Howard Digital, Binance Labs. 2+ year track record. | 9 | 9 | Non-Improvable (optimal) | [P1] docs.puffer.fi, [P4] Press sources |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No. MINIMUM_DELAY = 7 days is hardcoded as a constant. The _setDelay() function reverts if newDelay < MINIMUM_DELAY. Cannot be reduced below 7 days. | 9 | 9 | Non-Improvable (optimal) | [P0] Timelock.sol source code |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | No active ongoing bounty. The Immunefi Boost (Feb 22 - Mar 7, 2024) was a substantial one-time competitive audit: $50k rewards pool, 49 security researchers, 109 submitted reports, 14 valid vulnerabilities found. However, this was a 2-week event. immunefi.com/bug-bounty/pufferfinance/ returns 404. No active ongoing bug bounty exists. | 1 | 9 | **Improvable** | [P1] Immunefi Boost Summary Report (GitHub audits/), [P1] immunefi.com/bug-bounty/pufferfinance/ returns 404 |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. BlockSec Phalcon provides comprehensive protocol-wide 24/7 monitoring. Phalcon operates as a Safe module (address: 0x1b46e5d889aC1b0D411Ea45eca9C2f655a3E9Ef7) on the 1-of-9 Pauser Multisig, enabling autonomous pause execution without human intervention. Monitoring covers: contract upgrades, pause/unpause events, role changes, vault balance anomalies, deposit/withdrawal deviations, oracle updates, validator exit flows. On-chain proof: pause tx 0xa9f5c1...440e7f (April 9, 2026) was executed via the BlockSec module with ExecutionFromModuleSuccess event emitted by the Pauser Multisig. This demonstrates monitoring connected to automated protective action. No public monitoring dashboard. (Hexagate previously used but discontinued.) | 9 | 9 | Non-Improvable (optimal) | [P0] Safe API: BlockSec module on Pauser Multisig, [P0] Pause tx 0xa9f5c1...440e7f, [P0] Timelock TargetClosed event |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Yes. BlockSec Phalcon detection pipeline autonomously triggers on-chain pause via Safe module on Pauser Multisig. Architecture: (1) Phalcon detects anomaly, (2) auto-crafts and submits pause tx from module address, (3) module executes directly without requiring any owner signature, (4) Timelock.pause() or pauseSelectors() executed. On-chain proof: tx 0xa9f5c1...440e7f shows ExecutionFromModuleSuccess event. The Pauser Multisig can ONLY pause (never unpause, upgrade, or move funds). pufETH is an LST with no automated allocation mechanisms, so pause covers all capital flows. | 9 | 9 | Non-Improvable (optimal) | [P0] Pause tx 0xa9f5c1...440e7f with ExecutionFromModuleSuccess, [P0] Timelock.sol pause()/pauseSelectors() |

**Smart Contract Security Subtotal:**
- Raw scores: 10x9 + 1x1 = 91/99
- Adjusted: (91/99) x 180 = **165.5/180 (91.9%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Three documented multisigs via OpenZeppelin AccessManager (0x8c1686069474410E6243425f4a10177a94EBEE11): (1) Community Multisig (0x446d...Cb2a, 3-of-6) -- can execute with 0 delay, (2) Operations Multisig (0xC089...580d, 3-of-6) -- must queue with 7-day timelock, (3) Pauser Multisig (0x1ba8...0Df4, 1-of-9 with BlockSec module) -- can only pause. Architecture, addresses, role permissions, and scope documented in Deployments-and-ACL repo (mainnet.md). | 9 | 9 | Non-Improvable (optimal) | [P0] Timelock.sol, [P1] mainnet.md deployment docs, [P0] Safe API verified |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. All multisigs verified on-chain via Safe Global API: Community Multisig is 3-of-6 (requires 3 of 6 signers), Operations Multisig is 3-of-6. No single key can unilaterally execute upgrades or move funds. The Community Multisig (emergency path, 0 delay) requires minimum 3 signers. The Operations Multisig (normal path) requires 3 signers plus 7-day timelock. Pauser Multisig (1-of-9) can only pause, not move funds. AccessManager enforces role-based access. | 9 | 9 | Non-Improvable (optimal) | [P0] Safe API: Community 3-of-6, Operations 3-of-6, Pauser 1-of-9 |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Three separate multisig contracts with on-chain verifiable thresholds: Community 3-of-6 (50% threshold), Operations 3-of-6, Pauser 1-of-9 with BlockSec module (all Gnosis Safe, verified via Safe API). Threshold design is reasonable: 3-of-6 for emergency actions requires 50% of signers. Team states signers are drawn from multiple independent Ethereum-ecosystem categories (research, media, staking advocates, security firms) and offers private verification. However, signer identities remain publicly unknown. Per the framework independence verification rule: "If signer identities are fully unknown, independence cannot be confirmed -- score Mid (3) at best." | 3 | 9 | **Source Missing** | [P0] Safe API thresholds verified, [P1] Signer identities unknown publicly |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause is protocol-wide via AccessManager.setTargetClosed(), not address-level censorship. Requires Pauser Multisig. Exit fee currently 1% (max 2.5% hardcoded as _MAX_EXIT_FEE_BASIS_POINTS = 250 in PufferVaultV5.sol line 43). dailyAssetsWithdrawalLimit is deprecated in PufferVaultV5 -- no daily caps. Rules are public in code. No evidence of arbitrary address-level withdrawal blocking. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol _MAX_EXIT_FEE_BASIS_POINTS = 250, [P0] PufferVaultStorage.sol deprecated_dailyAssetsWithdrawalLimit |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets held on-chain in PufferVault contract and associated PufferModules (97+ Ethereum validators for EigenLayer restaking). totalAssets() traces all backing on-chain. Withdrawals permissionless via ERC4626 withdraw/redeem. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol totalAssets(), [P1] 97+ PufferModules on mainnet |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. User funds in PufferVault. DAO Multisig and Aera vault are separate addresses. No evidence of co-mingling with operational wallets. | 9 | 9 | Non-Improvable (optimal) | [P1] mainnet.md deployment docs |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- pufETH is a liquid restaking token, not a managed vault strategy. Users freely deploy pufETH across DeFi at their own discretion. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No formal documented playbook. However, an operational de-facto incident response process exists and has been demonstrated: (1) Detection via BlockSec Phalcon 24/7 monitoring, (2) Automated containment via Phalcon module on Pauser Multisig, (3) Assessment via Operations Multisig (3-of-6), (4) Remediation via Community Multisig (3-of-6, 0-delay for emergencies) or Operations Multisig (7-day timelock). On-chain proof of process: pause tx 0xa9f5c1...440e7f functioned as an unplanned test of the detection -> automated containment -> assessment -> remediation flow. Deployments-and-ACL repo serves as operational reference during triage. Lacks formal documentation, key rotation procedures, and scheduled tabletop exercises. | 3 | 9 | **Improvable** | [P0] Pause tx 0xa9f5c1...440e7f, [P1] Deployments-and-ACL repo, [P0] Timelock.sol |

**Key Management Subtotal (7 scored questions, 1 N/A):**
- Raw scores: 5x9 + 2x3 = 51/63
- Adjusted: (51/63) x 180 = **145.7/180 (81.0%)**

---

**Security Total: 165.5 + 145.7 = 311.2/360 (86.4%)**

---

### STRATEGY (30% Weight) -- Score: 245.5/270 (90.9%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from native Ethereum staking rewards (consensus + execution layer) plus EigenLayer restaking rewards. Validator tickets provide additional yield. No synthetic or leveraged components. Aligned with liquid restaking mandate. | 9 | 9 | Non-Improvable (optimal) | [P1] docs.puffer.fi, [P0] PufferVaultV5.sol |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail scenarios: (1) Mass validator slashing exceeding 2 ETH operator bonds per validator; (2) EigenLayer restaking penalties; (3) Smart contract exploit. pufETH exchange rate has not decreased since launch. Validator bonds absorb slashing losses before pufETH holders affected. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol exchange rate, [P0] PufferProtocol.sol bond cascade |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage at protocol level. pufETH is backed by staked ETH + restaked positions. EigenLayer restaking adds yield layer but not leverage. Users may leverage externally but protocol maintains full backing. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol totalAssets() |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- LST product, not a lending/borrowing position. No LTV ratio applicable. | N/A | N/A | N/A | - |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent losses to pufETH holders. Exchange rate has been monotonically increasing. TVL decline is organic outflows, not loss events. | 9 | 9 | Non-Improvable (optimal) | [P0] ERC4626 exchange rate history |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | N/A -- pufETH is a liquid restaking token, not a managed vault strategy. | N/A | N/A | N/A | - |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. Base yield from native ETH staking (~3-4% APR) is organic and sustainable. EigenLayer restaking adds supplementary yield. Less than 30% from token incentives. PUFFER emissions may supplement but are not required for core yield. | 9 | 9 | Non-Improvable (optimal) | [P1] docs.puffer.fi, [P3] DeFiLlama |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes under normal conditions. Two exit paths: instant via 1-step withdrawal (no fee cap, 1% exit fee, no daily limits in V5) or standard via 2-step Ethereum unstaking (~14 days, no fee). No slippage on protocol-level redemption via either path. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol withdraw/redeem, [P1] [Withdraw docs](https://docs.puffer.fi/yield/stakers/withdraw) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Moderate. pufETH should track ETH fair value via ERC4626 exchange rate. Market price can deviate in secondary markets. pufETH maintained peg through 96% TVL drawdown. Inherent to LST design. | 3 | 3 | Non-Improvable | [P0] ERC4626 exchange rate, [P3] CoinGecko pufETH/ETH data |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | N/A -- pufETH is a base-layer LST where users deposit directly. All allocation changes (validator provisioning, EigenLayer delegation) require explicit governance/multisig transactions. No automated allocation mechanisms, no Public Allocator, no auto-rebalancer. | N/A | N/A | N/A | [P0] PufferVaultV5.sol, [P0] PufferProtocol.sol |

**Protocol Mechanics Subtotal (7 scored questions, 3 N/A):**
- Raw scores: 6x9 + 1x3 = 57/63
- Adjusted: (57/63) x 45 = **40.7/45 (90.5%)**

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Native ETH, stETH, and WETH -- all Tier-0 assets on Ethereum. ETH is the highest quality, most liquid asset on the network. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol deposit functions |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | pufETH has been battle-tested: protocol processed ~$1.5B in withdrawals during 96% TVL drawdown ($1.84B to ~$59M over ~2.5 months, June-September 2024). pufETH/ETH exchange rate remained monotonically increasing throughout. Currently trading at ~1.0679 ETH, confirming no depeg above 2%. Additionally, 2 ETH validator bonds provide structural insulation from slashing before affecting pufETH holders. | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama TVL history, [P3] CoinGecko pufETH/ETH data, [P0] ERC4626 exchange rate |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | 97+ PufferModules provide validator diversification. Secure Signer anti-slashing technology. EigenLayer delegation to multiple RestakingOperators. Node operators post 2 ETH bonds (1 ETH with enclave) that absorb slashing before affecting pufETH. Bond burn cascade: slashing = full bond burned, inactivity = partial burn, normal exit = bond returned. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferProtocol.sol _getBondBurnAmount(), [P1] PufferModules deployment docs |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | 0%. All assets native on Ethereum mainnet. No bridge dependency. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol |

**Collateral Subtotal:**
- Raw scores: 4x9 = 36/36
- Adjusted: (36/36) x 45 = **45.0/45 (100.0%)**

---

#### Infrastructure Counterparty (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum mainnet (Tier-0 chain). PufferOracle (custom guardian-based oracle for tracking validator-locked ETH). No bridge dependency. No CEX dependency. No external wallet custody. All critical dependencies are Tier-0 or internal to the protocol. | 9 | 9 | Non-Improvable (optimal) | [P0] Etherscan deployment, [P0] PufferOracle.sol |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | PufferOracle is a custom guardian-based oracle for tracking locked ETH in validators. totalAssets() computes on-chain balances (WETH, ETH, stETH) directly without oracle dependency; only validator-locked ETH relies on PufferOracle guardian consensus. setTotalNumberOfValidators() exists as a governance-controlled override but has never been used. This provides partial redundancy (on-chain for liquid assets, oracle for staked). Single custom oracle with no Tier-0/1 fallback for the validator component. | 3 | 9 | **Improvable** | [P0] PufferOracle.sol, [P0] PufferVaultV5.sol totalAssets() lines 123-132 |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Node operators/validators running via PufferModules. No SOC 2/ISO27001 certifications disclosed for infrastructure providers. Secure Signer provides TEE-based anti-slashing but certification of operators is unknown. | 3 | 9 | **Source Missing** | [P1] docs.puffer.fi -- no certifications found |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | No oracle or infrastructure downtime events reported for Puffer. PufferOracle has operated without documented failures. Protocol has operated on Ethereum mainnet without disruption through its 2+ year lifetime. Deployed >6 months with no chain-level incidents causing user impact. | 9 | 9 | Non-Improvable (optimal) | No downtime events found |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum mainnet has had no chain-level halts >30 minutes in the last 12+ months. Tier-0 reliability. | 9 | 9 | Non-Improvable (optimal) | Ethereum Tier-0 status |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | No significant slashing events reported for Puffer validators. 97+ PufferModules with Secure Signer anti-slashing technology. Node operator bonds provide first-loss buffer absorbing slashing before pufETH holders are affected. No slashing event has impacted pufETH value. | 9 | 9 | Non-Improvable (optimal) | [P1] Deployment docs, [P1] docs.puffer.fi |
| ST-IC-07 | Are validators diverse geographically and by operator? | Yes. 97+ PufferModules delegating to multiple RestakingOperators. Permissionless validator model allows diverse participants. Secure Signer TEE-based anti-slashing supports client diversity. Geographic distribution not specifically published but permissionless model enables global participation. | 9 | 9 | Non-Improvable (optimal) | [P1] PufferModules deployment docs |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No single component is a permanent SPOF for withdrawals. ERC4626 vault provides permissionless withdraw/redeem for liquid assets. Validator operations distributed across 97+ PufferModules. PufferOracle is somewhat centralized (guardian-dependent) but does not block withdrawals of liquid assets if it fails. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol, [P1] PufferModules deployment |
| ST-IC-09 | How robust is the cross-chain messaging or bridge verification setup? | N/A -- pufETH operates exclusively on Ethereum mainnet with no cross-chain messaging or bridge dependency. | N/A | N/A | N/A | - |
| ST-IC-10 | Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting? | N/A -- No bridge or cross-chain minting exists for pufETH. | N/A | N/A | N/A | - |
| ST-IC-11 | Is the off-chain verification infrastructure resilient to data-source manipulation? | N/A -- No off-chain verification component for cross-chain messages. PufferOracle uses guardian consensus for validator tracking but this is covered under ST-IC-02. | N/A | N/A | N/A | - |

**Infrastructure Counterparty Subtotal (8 scored questions, 3 N/A):**
- Raw scores: 6x9 + 2x3 = 60/72
- Adjusted: (60/72) x 45 = **37.5/45 (83.3%)**

---

#### Protocol Counterparty (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | None externally. Collateral remains exclusively on Ethereum Beacon Chain validators via PufferModules and EigenLayer restaking. No external protocol deployment, no CEX custody, no RWA exposure. Limited, high-quality counterparties: Ethereum (staking), EigenLayer (restaking). | 9 | 9 | Non-Improvable (optimal) | [P1] docs.puffer.fi architecture |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Fee structure documented in code: exit fee currently 1% (hardcoded _MAX_EXIT_FEE_BASIS_POINTS = 250, max 2.5%), configurable via governance. Validator ticket mechanics documented. EigenLayer restaking reward flows transparent on-chain. All fee parameters visible in verified smart contracts. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol _MAX_EXIT_FEE_BASIS_POINTS = 250, [P1] docs.puffer.fi |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | No external counterparties at protocol level. Internal constraints enforced on-chain: exit fee cap at 2.5% (hardcoded), AccessManager role-based controls. EigenLayer delegation spread across multiple RestakingOperators via 97+ PufferModules. Daily withdrawal limits deprecated in V5. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol, [P1] PufferModules delegation |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | No external counterparties. Unwinding via standard path requires Ethereum + EigenLayer unstaking (~14 days). Instant withdrawal available via 1-step path (1% fee, no daily caps in V5) when vault has liquid assets. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol withdraw/redeem |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Yes. EigenLayer dependency documented. PufferModules and RestakingOperators listed in deployment docs. All counterparty relationships are public and on-chain verifiable. | 9 | 9 | Non-Improvable (optimal) | [P1] mainnet.md deployment docs |

**Protocol Counterparty Subtotal:**
- Raw scores: 5x9 = 45/45
- Adjusted: 45/45 x 45 = **45.0/45 (100.0%)**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Two withdrawal paths: (1) 1-step instant withdrawal (1% fee, no daily caps in V5), and (2) 2-step standard withdrawal via Ethereum unstaking (~14 days, no fee). Protocol can be paused via Pauser Multisig calling Timelock.pause() -- this is protocol-wide, not address-level censorship. No evidence of address-level withdrawal blocking. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol ERC4626, [P0] Timelock.sol pause(), [P1] [Withdraw docs](https://docs.puffer.fi/yield/stakers/withdraw) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | With ~$71.5M TVL, near-total exit would require extended staggered processing via standard withdrawals (~14 days due to Ethereum + EigenLayer unstaking). Instant 1-step withdrawals limited by vault liquid asset availability. Secondary market (DEX pools) thin relative to TVL. Near-100% redemption within a short window is uncertain. However, the protocol previously processed ~$1.5B in exits over 2.5 months. | 3 | 3 | Non-Improvable | [P0] Validator exit mechanics, [P3] DeFiLlama TVL data |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No documented withdrawal delays, queues, or freezes for pufETH. Protocol has operated since early 2024 with ERC4626 withdraw available. The $1.5B drawdown was processed without delays. No evidence of protocol-initiated withdrawal blocks. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol, [P3] DeFiLlama TVL history |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | No. The dailyAssetsWithdrawalLimit is deprecated in PufferVaultV5 (confirmed in PufferVaultStorage.sol: "uint96 deprecated_dailyAssetsWithdrawalLimit; // Not in use anymore"). PufferVaultV5 withdraw/redeem functions contain no daily limit checks. The only constraint is the exit fee (currently 1%, max 2.5% hardcoded). Users can withdraw without daily caps. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultStorage.sol line 30: deprecated_dailyAssetsWithdrawalLimit, [P0] PufferVaultV5.sol -- no daily limit enforcement |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Battle-tested. Protocol processed ~$1.5B in withdrawals over ~2.5 months during 96% TVL drawdown ($1.84B to ~$59M, June-September 2024). pufETH/ETH exchange rate remained monotonically increasing throughout. No withdrawal delays, queues, or freezes during the drawdown. ERC4626 withdraw/redeem operated correctly throughout. Per the battle-tested rule, proven resilience under real stress scores higher than untested. | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama TVL history, [P3] CoinGecko pufETH/ETH, [P0] ERC4626 exchange rate |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | Two withdrawal paths: (1) 1-step instant (~1 transaction, 1% fee, no daily limits) does not rely on unstaking; (2) 2-step standard path requires Ethereum + EigenLayer unstaking (~14 days, no fee). Both paths are clearly documented. No bridge dependency, no vesting lock-up. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol, [P1] [Withdraw docs](https://docs.puffer.fi/yield/stakers/withdraw) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary exit is via ERC4626 vault withdraw/redeem functions directly against protocol. Secondary markets provide an additional exit option but are not required. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol withdraw/redeem |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | With ~$71.5M TVL, secondary market depth for pufETH is limited. Primary trading on Curve pufETH/wstETH pair. Depth likely supports only ~3-10% of TVL without significant slippage. | 3 | 9 | **Improvable** | [P3] DEX liquidity data |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Battle-tested. The 96% TVL drawdown ($1.84B to ~$59M) is a near-total exit scenario. Protocol processed this without haircuts, delays, or withdrawal blocks. With deprecated daily withdrawal limits (V5), no rate-limiting caps exist. Exit fee (1%) discourages panic exits but does not block them. Validator bonds returned cleanly during drawdown (no slashing), demonstrating orderly unwind. Framework: "Design, buffers, and unwind rules indicate rapid mass exit would primarily cause temporary queues or rate spikes without expected permanent depositor haircuts." | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama TVL drawdown, [P0] PufferVaultV5.sol -- no daily caps |

**Liquidity Subtotal:**
- Raw scores: 7x9 + 2x3 = 69/81
- Adjusted: (69/81) x 45 = **38.3/45 (85.2%)**

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | pufETH has been live since February 2024 (2+ years) with no significant depeg events. The ERC4626 exchange rate has been monotonically increasing. During the 96% TVL decline from ~$1.84B to ~$59M, pufETH maintained its peg without sharp dislocations. Currently trading at ~1.0679 ETH. CoinGecko confirms stable pufETH/ETH ratio throughout. The 96% TVL drawdown constitutes a real-world stress scenario that pufETH survived without peg failure. | 9 | 9 | Non-Improvable (optimal) | [P3] CoinGecko pufETH data, [P0] ERC4626 exchange rate history |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Low risk. pufETH is unleveraged at protocol level with full ETH backing via validators. No directional exposure or leverage risk. Node operator bonds (2 ETH per validator) provide additional buffer against slashing. ETH-denominated LST tracks ETH directly. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol, [P0] PufferProtocol.sol bonds |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Staking rate determined by Ethereum protocol, not by Puffer rate models. EigenLayer restaking adds supplementary yield but does not introduce rate model risk. TVL has shifted dramatically (96% decline) without rate model failure -- yield continued from underlying staking. No history of rate model failures. | 9 | 9 | Non-Improvable (optimal) | [P3] StakingRewards data, [P3] DeFiLlama |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | No formal Monte Carlo simulation or forward-looking stress test published. However, the protocol has undergone a real-world stress scenario: ~$1.5B in withdrawals processed over ~2.5 months during 96% TVL drawdown with peg maintained and operational continuity preserved. This constitutes empirical stress validation but is not explicit modeling. Framework Mid (3): "Strategy tested against moderate volatility and price shocks but tail assumptions or cross-factor interactions only partially covered." | 3 | 9 | **Improvable** | [P3] DeFiLlama TVL history, [P0] On-chain exchange rate |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Not at protocol level. pufETH is unleveraged with full ETH backing via validators and EigenLayer restaking. No liquidation mechanism within the Puffer protocol. Users may leverage pufETH externally but the protocol itself has no liquidation triggers. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV5.sol -- no liquidation logic |

**Market Subtotal:**
- Raw scores: 4x9 + 1x3 = 39/45
- Adjusted: (39/45) x 45 = **39.0/45 (86.7%)**

---

**Strategy Total: 40.7 + 45.0 + 37.5 + 45.0 + 38.3 + 39.0 = 245.5/270 (90.9%)**

---

### OPERATIONS (30% Weight) -- Score: 179.1/270 (66.3%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Active hybrid governance model. PUFFER token with vlPUFFER lock mechanism (30-day to 24-month lock, 1x-24x multiplier). Formal PIP process: 5-day discussion, 2-day Governance Review Committee evaluation, 14-day voting epoch. vote.puffer.fi (Aragon-based) for on-chain voting; governance.puffer.fi (Discourse) for discussion. PIP-1 (AVS Whitelisting) and PIP-2 (Gauge Removal Framework, passed 3.4M vs 202K) demonstrate active governance. However, Community Multisig (3-of-6) retains emergency execution with 0 delay -- hybrid model where governance covers major changes but multisig retains bypass capability. This is industry-standard (Lido, Aave, Rocket Pool) but remains a Mid characteristic per framework. | 3 | 9 | **Improvable** | [P1] vote.puffer.fi, [P1] governance.puffer.fi, [P1] docs.puffer.fi governance |
| O-G-02 | How concentrated is voting power among top holders or delegates? | PUFFER token (1B max supply) with documented allocation: 40% Ecosystem/Community, 26% Investors, 20% Early Contributors/Advisors, 7.5% S1 Airdrop, 5.5% S2 Airdrop, 1% Protocol Guild. vlPUFFER voting power is on-chain. PIP-2 passed with 3.4M for vs 202K against. However, top-holder concentration of vlPUFFER is not published -- insiders (investors + early contributors) hold 46% of tokens, suggesting potential concentration risk. | 3 | 9 | **Source Missing** | [P1] PUFFER Token docs, [P1] PIP-2 vote results |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | 7-day hardcoded MINIMUM_DELAY for Operations Multisig via Timelock contract. Community Multisig has 0 delay (emergency bypass). The 7-day delay exceeds the 24h threshold for normal operations. | 9 | 9 | Non-Improvable (optimal) | [P0] Timelock.sol MINIMUM_DELAY |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A -- pufETH is a liquid restaking token, not a vault with a replaceable strategy manager. | N/A | N/A | N/A | - |

**Governance Subtotal (3 scored questions, 1 N/A):**
- Raw scores: 1x9 + 2x3 = 15/27
- Adjusted: (15/27) x 67.5 = **37.5/67.5 (55.6%)**

---

#### Team & Legal (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Puffer Finance LinkedIn page shows 26 employees with names and roles. Co-founders: Jason Vranek and Amir Forouzani (CEO). Company headquartered in San Francisco, CA, founded 2022. Series A funding (April 2024) with known investors (Binance Labs, Brevan Howard Digital, Lemniscap). Team members identifiable via LinkedIn, GitHub contributions, and public appearances. | 9 | 9 | Non-Improvable (optimal) | [P2] LinkedIn - Puffer Finance, [P4] Tracxn, Crunchbase profiles |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Puffer Finance has 26 employees per LinkedIn, with multiple active GitHub contributors across the puffer-contracts, Deployments-and-ACL, and related repositories. Co-founders Jason Vranek and Amir Forouzani lead the team. Breadth of protocol components supported by full engineering team. | 9 | 9 | Non-Improvable (optimal) | [P2] LinkedIn - 26 employees, [P1] GitHub contributors |
| O-TL-03 | What legal entity and jurisdiction operate the protocol? | Entity details limited. Puffer Finance website terms of service likely reference an entity but specific legal structure, jurisdiction, and registration details are not prominently disclosed in documentation. San Francisco headquarters identified via LinkedIn. | 3 | 9 | **Source Missing** | [P1] docs.puffer.fi |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known enforcement actions against Puffer Finance. Ethereum Foundation grant recipient indicates positive regulatory standing. | 9 | 9 | Non-Improvable (optimal) | No enforcement actions found |
| O-TL-05 | Is there an on-call and incident response process for core teams? | BlockSec Phalcon provides 24/7 automated monitoring and response capability. BlockSec is retained as a security partner and operates as a Safe module on the Pauser Multisig, providing professional security incident response. Clear escalation path: Pauser Multisig (automated containment) -> Operations Multisig (investigation) -> Community Multisig (emergency remediation). On-chain proof of automated response: pause tx 0xa9f5c1...440e7f. Multiple support channels (Discord, contact forms). However, no published response-time SLAs, formal on-call rotation, or documented escalation procedures. Framework Mid (3): "Informal on-call exists with partial playbooks." | 3 | 9 | **Improvable** | [P0] Pause tx 0xa9f5c1...440e7f, [P0] BlockSec module on Pauser Multisig, [P1] Discord support |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Multiple support channels: Discord with support ticket system (discord.com/invite/pufferfi), Google Forms contact form, and documentation site. Structured support process demonstrates commitment to user issue resolution. | 9 | 9 | Non-Improvable (optimal) | [P1] puffer.fi, Discord, Contact Form |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Known investors: Lemniscap, Brevan Howard Digital, Binance Labs. Ethereum Foundation grant. Investors disclosed through press and documentation. | 9 | 9 | Non-Improvable (optimal) | [P4] Press coverage, [P1] docs.puffer.fi |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | N/A -- pufETH is a liquid restaking token, not a vault with a strategy manager. | N/A | N/A | N/A | - |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | N/A -- No strategy manager. | N/A | N/A | N/A | - |

**Team & Legal Subtotal (7 scored questions, 2 N/A):**
- Raw scores: 5x9 + 2x3 = 51/63
- Adjusted: (51/63) x 67.5 = **54.6/67.5 (80.9%)**

---

#### Documentation (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Comprehensive documentation at docs.puffer.fi covering: protocol architecture (PufferModules, Guardians, RestakingOperators, AccessManager), strategy mechanics (nLRT, validator tickets, rewards, staking), governance (vlPUFFER token, understanding governance, PIPs), risk disclosures (validator slashing, AVS operator slashing, withdrawal constraints), institutional solutions, node operator requirements, FAQ, and glossary. GitHub provides additional technical docs. | 9 | 9 | Non-Improvable (optimal) | [P1] docs.puffer.fi, [P1] GitHub docs |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Documentation provides end-to-end collateral flow: ETH deposited into PufferVault -> allocated to validators via PufferModules -> rewards accrue -> pufETH conversion rate increases. Loss scenarios explicitly documented: (1) validator slashing exceeding operator 2 ETH bond, (2) AVS operator slashing reduces pufETH value, (3) withdrawal constraints. Bond mechanics documented as first-loss buffer. | 9 | 9 | Non-Improvable (optimal) | [P1] nLRT docs, [P1] Rewards docs |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Deployments-and-ACL repo (mainnet.md) provides a canonical registry of all deployed contract addresses with roles and implementations. Well-maintained deployment documentation. | 9 | 9 | Non-Improvable (optimal) | [P1] mainnet.md deployment registry |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Central role registry in Deployments-and-ACL GitHub repo (mainnet.md) lists all contract addresses with roles and implementations. AccessManager role-based system documented in code and docs. Timelock roles clearly defined with scope. Change history maintained via Git commits. Governance changes tracked through PIP proposals. | 9 | 9 | Non-Improvable (optimal) | [P1] Deployments-and-ACL, [P1] governance.puffer.fi |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | ERC4626 totalAssets() provides real-time on-chain proof-of-reserves for liquid vault holdings (WETH, ETH, stETH). PufferOracle provides proof-of-reserves for validator-locked ETH via Guardian consensus (7/8 majority required). Guardian roles and consensus requirements documented. Methodology is on-chain and verifiable. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferOracle.sol, [P0] PufferVaultV5.sol totalAssets() |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. All core contracts verified on Etherscan with full source code available. UUPS proxy pattern with publicly viewable implementation contracts. | 9 | 9 | Non-Improvable (optimal) | [P0] Etherscan verified contracts |

**Documentation Subtotal:**
- Raw scores: 6x9 = 54/54
- Adjusted: (54/54) x 67.5 = **67.5/67.5 (100.0%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | The validator bond system functions as an on-chain, automatically enforced first-loss capital layer. Each node operator posts a 2 ETH bond (1 ETH with enclave) when registering a validator, held as pufETH. Bond burn cascade: slashing = full bond burned, inactivity = partial bond burned proportional to shortfall, normal exit = bond returned. This is automatic (no governance action required) and proportional to risk. However, this covers only validator slashing/inactivity -- not general-purpose losses (smart contract exploit, oracle failure). Framework Mid (3): "Backstop or treasury stated as intended for loss coverage but activation remains discretionary." The bond activation is actually automatic (better than discretionary) but scope is narrow (only validator risk). Score: Mid (3) for narrow-scope backstop. | 3 | 9 | **Improvable** | [P0] PufferProtocol.sol VALIDATOR_BOND = 2 ether, [P0] _getBondBurnAmount() bond burn cascade |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | No dedicated treasury wallet disclosed. Puffer docs mention VT fee revenue allocated to "treasury" but no address is identified. DeFiLlama treasury API returns no data (no adapter). The Aera Vault (0x6c25...0b8) listed in Deployments-and-ACL is labeled "AVS Rewards Management," not general treasury. PUFFER token market cap ~$11M (FDV ~$25.3M) but these are volatile native tokens. However, the validator bond mechanism (2 ETH per validator, denominated in pufETH, burned automatically on slashing/inactivity via _getBondBurnAmount()) functions as a protocol-level first-loss reserve that is on-chain verifiable, liquid, and scales proportionally with active validator count. While not a pooled treasury, the bonds provide a workable, concentrated low-risk buffer targeting the primary loss vector (validator slashing/inactivity). Framework Mid (3): "holdings somewhat concentrated but still include workable low-risk liquid buffer." Score reflects bond mechanism as the operative reserve. | 3 | 9 | **Improvable** | [P0] PufferProtocol.sol VALIDATOR_BOND, [P0] Bond burn cascade on-chain, [P1] Deployments-and-ACL -- no treasury wallet found, [P3] CoinGecko PUFFER mcap ~$11M |
| O-FR-03 | What is the estimated operational runway at current burn? | Cannot be estimated from disclosed information. TVL declined 96% (from ~$1.84B to ~$71.5M), dramatically reducing fee revenue. No published cost structure, revenue model, or runway estimates. VC funding provides some buffer but duration unknown. | 1 | 9 | **Improvable** | [P3] DeFiLlama TVL decline data |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | The 96% TVL decline ($1.84B to ~$59M over ~2.5 months) is a structural decline, not a temporary stress event. Protocol maintained full operational continuity: no peg deviation, no withdrawal delays, no oracle failures, no slashing events. Validator bonds were returned cleanly. However, the decline was not temporary -- TVL has recovered only marginally to ~$71.5M. Revenue was dramatically impaired. Framework Mid (3): "Stress periods caused significant but recoverable TVL or revenue drops." The decline was significant; partial recovery has occurred. pufETH composability surface is limited (not widely integrated into external lending markets like rsETH). | 3 | 9 | **Improvable** | [P3] DeFiLlama TVL history, [P0] ERC4626 exchange rate |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Partial. ERC4626 vault provides permissionless withdraw/redeem for liquid assets (WETH, ETH, stETH). However, PufferOracle relies on guardian signatures to track validator-locked ETH -- if guardians are team-adjacent and disappear, oracle stops updating. Community Multisig signer identities are undisclosed, so independent operation cannot be confirmed. No on-chain governance exists (unlike RocketPool's pDAO). Protocol would degrade significantly without team: stale oracle, no upgrades, no validator management. Core withdrawal path remains functional but protocol health would deteriorate. | 3 | 9 | **Improvable** | [P0] PufferOracle.sol guardian dependency, [P0] PufferVaultV5.sol ERC4626 permissionless |

**Financial Resilience Subtotal:**
- Raw scores: 3+3+1+3+3 = 13/45
- Adjusted: (13/45) x 67.5 = **19.5/67.5 (28.9%)**

---

**Operations Total: 37.5 + 54.6 + 67.5 + 19.5 = 179.1/270 (66.3%)**

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 91 | 99 | 165.5 | 180 | 91.9% |
| | Key Management (7 of 8 Q scored) | 51 | 63 | 145.7 | 180 | 81.0% |
| | **Security Subtotal** | | | **311.2** | **360** | **86.4%** |
| **Strategy** | Protocol Mechanics (7 of 10 Q scored) | 57 | 63 | 40.7 | 45 | 90.5% |
| | Collateral (4 Q) | 36 | 36 | 45.0 | 45 | 100.0% |
| | Infra Counterparty (8 of 11 Q scored) | 60 | 72 | 37.5 | 45 | 83.3% |
| | Protocol Counterparty (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity (9 Q) | 69 | 81 | 38.3 | 45 | 85.2% |
| | Market (5 Q) | 39 | 45 | 39.0 | 45 | 86.7% |
| | **Strategy Subtotal** | | | **245.5** | **270** | **90.9%** |
| **Operations** | Governance (3 of 4 Q scored) | 15 | 27 | 37.5 | 67.5 | 55.6% |
| | Team & Legal (7 of 9 Q scored) | 51 | 63 | 54.6 | 67.5 | 80.9% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 13 | 45 | 19.5 | 67.5 | 28.9% |
| | **Operations Subtotal** | | | **179.1** | **270** | **66.3%** |
| **TOTAL** | | | | **735.8** | **900** | **81.8%** |

---
