# Puffer Finance - pufETH Risk Rating

**Rating Date**: 2026-03-09
**Final Grade**: B-
**Total Score**: 680.6/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v1.0-alpha

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 283.6/360 (78.8%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. PufferVault (pufETH) contracts audited by 7 independent parties: BlockSec (V1), SlowMist (V1), Quantstamp (V1), Trail of Bits (V2, March 2024), Nethermind (V2), Creed (V2, April 2024), and Immunefi Boost (V1). All audit reports publicly available in GitHub audits/ directory. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub Audits](https://github.com/PufferFinance/pufETH/tree/main/audits) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Trail of Bits (Tier-0) conducted the V2 audit in March 2024. Nethermind (Tier-1) also audited V2. At least one Tier-0 auditor in the most recent cycle. | 9 | 9 | Non-Improvable (optimal) | [P1] Trail of Bits V2 report, [P1] NM0202-FINAL_PUFFER.pdf |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. The V1-to-V2 upgrade was audited by Trail of Bits, Nethermind, and Creed before deployment. Last repo commit was June 2024. No evidence of unaudited core upgrades since V2 launch. | 9 | 9 | Non-Improvable (optimal) | [P1] GitHub commit history, [P1] Deployment docs |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated? | Creed audit fixes merged in PR #77 (April 30, 2024). All published reports are final versions indicating remediation review. No evidence of unresolved critical/high findings. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub PR #77](https://github.com/PufferFinance/pufETH/pull/77) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Yes, UUPS proxy. Upgrades controlled via Timelock with hardcoded MINIMUM_DELAY = 7 days (constant, cannot be reduced). Operations Multisig must queue and wait 7 days. Community Multisig can execute immediately (0 delay) for emergencies -- bypass triggers include: active exploit requiring immediate patch, critical vulnerability needing urgent mitigation, or protocol state requiring emergency pause. The 7-day minimum for standard operations exceeds the 24h threshold. | 9 | 9 | Non-Improvable (optimal) | [P0] Timelock.sol: MINIMUM_DELAY = 7 days constant |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploits in 2+ years of operation (since Feb 2024). TVL decline (~$1.7B to ~$61M) is organic outflows, not exploit-related. | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama TVL data, [P4] No entries in rekt.news |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No. Ethereum Foundation grant recipient. Funded by Lemniscap, Brevan Howard Digital, Binance Labs. 2+ year track record. | 9 | 9 | Non-Improvable (optimal) | [P1] docs.puffer.fi, [P4] Press sources |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No. MINIMUM_DELAY = 7 days is hardcoded as a constant. The _setDelay() function reverts if newDelay <= MINIMUM_DELAY. Cannot be reduced below 7 days. | 9 | 9 | Non-Improvable (optimal) | [P0] Timelock.sol source code |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | No active ongoing bounty. The Immunefi Boost (Feb 22 - Mar 7, 2024) was a substantial one-time competitive audit: $50k rewards pool, 49 security researchers, 109 submitted reports, 14 valid vulnerabilities found (9 Low, 5 Medium), 23 insight reports, $50k distributed to 36 researchers. Top findings: Lido slashing discount impact on totalAssets, Timelock gas exhaustion via EIP-150, stETH 1-2 wei rounding, double-execution risk. However, this was a 2-week event, not a permanent program. immunefi.com/bug-bounty/pufferfinance/ returns 404. No active ongoing bug bounty exists. | 1 | 9 | **Improvable** | [P1] Immunefi Boost Summary Report (GitHub audits/), [P1] immunefi.com/bug-bounty/pufferfinance/ returns 404 |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes, basic monitoring confirmed by two independent auditors. Quantstamp audit (PUFF-10 response): "We are utilizing BlockSec and Hexagate monitors and alerts to monitor the Community multisig and the owners." Trail of Bits executive summary also references "BlockSec and Hexagate monitoring partnership." Two different monitoring services (BlockSec, Hexagate) watching the most security-critical components (Community Multisig that can bypass timelock, and owner addresses). However, scope is focused on admin key activity rather than comprehensive protocol-wide invariant monitoring. No public monitoring dashboard. | 3 | 9 | **Improvable** | [P1] Quantstamp audit PUFF-10 response, [P1] Trail of Bits V2 executive summary |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Manual pause exists via Pauser Multisig (1-of-12, requiring only 1 of 12 signers) calling Timelock.pause() or pauseSelectors() for granular function-level restrictions. PufferVaultV2 uses `restricted` modifier (like whenNotPaused). BlockSec + Hexagate monitoring generates alerts, but no evidence these connect to automated pause triggers. The 1-of-12 Pauser threshold enables rapid manual response when monitoring alerts, but the trigger step remains human-initiated. | 3 | 9 | **Improvable** | [P0] Timelock.sol pause()/pauseSelectors(), [P0] Pauser Multisig 1-of-12, [P1] Quantstamp PUFF-10 |

**Smart Contract Security Subtotal:**
- Raw scores: 9+9+9+9+9+9+9+9+1+3+3 = 79/99
- Adjusted: (79/99) x 180 = **143.6/180 (79.8%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Three documented multisigs via OpenZeppelin AccessManager (0x8c1686069474410E6243425f4a10177a94EBEE11): (1) Community Multisig (0x446d...Cb2a) -- can execute with 0 delay, (2) Operations Multisig (0xC089...580d) -- must queue with 7-day timelock, (3) Pauser Multisig (0x1ba8...0Df4) -- can only pause. Architecture, addresses, role permissions, and scope documented in Deployments-and-ACL repo (mainnet.md). | 9 | 9 | Non-Improvable (optimal) | [P0] Timelock.sol, [P1] mainnet.md deployment docs |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. All three multisigs verified on-chain via Safe Global API: Community Multisig is 3-of-8 (requires 3 of 8 signers), Operations Multisig is 3-of-6, Pauser Multisig is 1-of-12. No single key can unilaterally execute upgrades or move funds. The Community Multisig (emergency path, 0 delay) requires minimum 3 signers. The Operations Multisig (normal path) requires 3 signers plus 7-day timelock. AccessManager enforces role-based access. | 9 | 9 | Non-Improvable (optimal) | [P0] Safe Global API: Community 3-of-8, Operations 3-of-6, Pauser 1-of-12 |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Three separate multisig contracts with on-chain verifiable thresholds: Community 3-of-8, Operations 3-of-6, Pauser 1-of-12 (all Gnosis Safe, verified via Safe Global API). Threshold design is reasonable: 3-of-8 for emergency actions requires 37.5% of signers; 1-of-12 for pause enables rapid emergency response. However, signer identities remain fully unknown -- all 8 Community Multisig addresses are public but no names disclosed. Docs state "trusted partners and respected members of the Ethereum community" but name no individuals. Per the independence verification rule: signer independence cannot be confirmed without identity disclosure. | 3 | 9 | **Source Missing** | [P0] Safe Global API thresholds, [P1] mainnet.md -- signer identities unknown |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause is protocol-wide via AccessManager.setTargetClosed(), not address-level censorship. Requires Pauser Multisig. Daily withdrawal limit and exit fee (currently 1%, max 2% hardcoded in EXIT_FEE_BASIS_POINTS) provide bounded controls. Rules are public in code. No evidence of arbitrary address-level withdrawal blocking. | 9 | 9 | Non-Improvable (optimal) | [P0] Timelock.sol, [P0] PufferVaultV2.sol EXIT_FEE_BASIS_POINTS max 200 |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets held on-chain in PufferVault contract and associated PufferModules (97+ Ethereum validators for EigenLayer restaking). totalAssets() traces all backing on-chain. Withdrawals permissionless via ERC4626 withdraw/redeem. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol totalAssets(), [P1] 97+ PufferModules on mainnet |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. User funds in PufferVault. DAO Multisig and Aera vault are separate addresses. No evidence of co-mingling with operational wallets. | 9 | 9 | Non-Improvable (optimal) | [P1] mainnet.md deployment docs |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- pufETH is a liquid restaking token, not a managed vault strategy. Users freely deploy pufETH across DeFi at their own discretion. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No documented incident response playbook found. No evidence of tabletop exercises, key rotation procedures, or signer replacement protocols in GitHub or documentation. No security partnership for incident response disclosed. | 1 | 9 | **Improvable** | No playbook found in GitHub or docs |

**Key Management Subtotal (7 scored questions, 1 N/A):**
- Raw scores: 9+9+3+9+9+9+1 = 49/63
- Adjusted: (49/63) x 180 = **140.0/180 (77.8%)**

---

**Security Total: 143.6 + 140.0 = 283.6/360 (78.8%)**

---

### STRATEGY (30% Weight) -- Score: 226.0/270 (83.7%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from native Ethereum staking rewards (consensus + execution layer) plus EigenLayer restaking rewards. Validator tickets provide additional yield. No synthetic or leveraged components. Aligned with liquid restaking mandate. | 9 | 9 | Non-Improvable (optimal) | [P1] docs.puffer.fi, [P0] PufferVaultV2.sol |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail scenarios: (1) Mass validator slashing exceeding PufferModule bonds; (2) EigenLayer restaking penalties; (3) Smart contract exploit. pufETH exchange rate has not decreased since launch. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol exchange rate |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage at protocol level. pufETH is backed by staked ETH + restaked positions. EigenLayer restaking adds yield layer but not leverage. Users may leverage externally but protocol maintains full backing. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol totalAssets() |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- LST product, not a lending/borrowing position. No LTV ratio applicable. | N/A | N/A | N/A | - |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent losses to pufETH holders. Exchange rate has been monotonically increasing. TVL decline is organic outflows, not loss events. | 9 | 9 | Non-Improvable (optimal) | [P0] ERC4626 exchange rate history |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | N/A -- pufETH is a liquid restaking token, not a managed vault strategy. | N/A | N/A | N/A | - |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. Base yield from native ETH staking (~3-4% APR) is organic and sustainable. EigenLayer restaking adds supplementary yield. Less than 30% from token incentives. PUFFER emissions may supplement but are not required for core yield. | 9 | 9 | Non-Improvable (optimal) | [P1] docs.puffer.fi, [P3] DeFiLlama |
| ST-PM-08 | Can the position be fully unwound without slippage turning yield negative? | Yes under normal conditions. Two exit paths: instant via liquidity vault (~1-5 min, 1% fee) or standard via Ethereum + EigenLayer unstaking (~14+ days, no fee). No slippage on protocol-level redemption via either path. Daily withdrawal limit may constrain instant exits. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol withdraw/redeem, [P1] [Withdraw docs](https://docs.puffer.fi/yield/stakers/withdraw) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Moderate. pufETH should track ETH fair value via ERC4626 exchange rate. Market price can deviate in secondary markets. No historical stress data for pufETH depegs (TVL decline was gradual, not crisis-driven). Inherent to LST design. Consistent with Lido stETH and Rocket Pool rETH scoring. | 3 | 3 | Non-Improvable | [P0] ERC4626 exchange rate mechanism |

**Protocol Mechanics Subtotal (7 scored questions, 2 N/A):**
- Raw scores: 6x9 + 1x3 = 57/63
- Adjusted: (57/63) x 45 = **40.7/45 (90.5%)**

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Native ETH, stETH, and WETH -- all Tier-0 assets on Ethereum. ETH is the highest quality, most liquid asset on the network. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol deposit functions |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | pufETH has not been tested under significant market stress. TVL declined 96% but this was gradual organic outflow over months, not a crisis-driven depeg event. No data on pufETH secondary market behavior during volatility. Per the battle-tested rule: untested protocols score Mid (3). | 3 | 3 | Non-Improvable | [P3] DeFiLlama TVL history |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | 97+ PufferModules provide validator diversification. Secure Signer anti-slashing technology. EigenLayer delegation to multiple RestakingOperators. Node operators post bonds that absorb slashing before affecting pufETH. | 9 | 9 | Non-Improvable (optimal) | [P1] PufferModules deployment docs |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | 0%. All assets native on Ethereum mainnet. No bridge dependency. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol |

**Collateral Subtotal:**
- Raw scores: 9+3+9+9 = 30/36
- Adjusted: (30/36) x 45 = **37.5/45 (83.3%)**

---

#### Infrastructure Counterparty (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum mainnet (Tier-0 chain). PufferOracle (custom guardian-based oracle for tracking validator-locked ETH). No bridge dependency. No CEX dependency. No external wallet custody. All critical dependencies are Tier-0 or internal to the protocol. | 9 | 9 | Non-Improvable (optimal) | [P0] Etherscan deployment, [P0] PufferOracle.sol |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | PufferOracle is a custom guardian-based oracle for tracking locked ETH in validators -- single oracle with no documented Tier-0/1 fallback. On-chain balances (WETH, ETH, stETH) computed directly in totalAssets() without oracle dependency, but the validator-locked ETH component relies solely on PufferOracle guardian signatures. Not battle-tested under stress. No bridge dependency. | 3 | 9 | **Improvable** | [P0] PufferOracle.sol, [P0] PufferVaultV2.sol totalAssets() |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Node operators/validators running via PufferModules. No SOC 2/ISO27001 certifications disclosed for infrastructure providers. Secure Signer provides TEE-based anti-slashing but certification of operators is unknown. | 3 | 9 | **Source Missing** | [P1] docs.puffer.fi -- no certifications found |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | No oracle or infrastructure downtime events reported for Puffer. PufferOracle has operated without documented failures. Protocol has operated on Ethereum mainnet without disruption through its 2+ year lifetime. Deployed >6 months with no chain-level incidents causing user impact. | 9 | 9 | Non-Improvable (optimal) | No downtime events found |
| ST-IC-05 | Has the base chain recently halted block production? | No. Ethereum mainnet has had no chain-level halts >30 minutes in the last 12+ months. Tier-0 reliability. | 9 | 9 | Non-Improvable (optimal) | Ethereum Tier-0 status |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | No significant slashing events reported for Puffer validators. 97+ PufferModules with Secure Signer anti-slashing technology. Node operator bonds provide first-loss buffer absorbing slashing before pufETH holders are affected. No slashing event has impacted pufETH value. | 9 | 9 | Non-Improvable (optimal) | [P1] Deployment docs, [P1] docs.puffer.fi |
| ST-IC-07 | Are validators diverse geographically and by operator? | Yes. 97+ PufferModules delegating to multiple RestakingOperators. Permissionless validator model allows diverse participants. Secure Signer TEE-based anti-slashing supports client diversity. Geographic distribution not specifically published but permissionless model enables global participation. | 9 | 9 | Non-Improvable (optimal) | [P1] PufferModules deployment docs |
| ST-IC-08 | Can any single infra failure block withdrawals or cause losses? | No single component is a permanent SPOF for withdrawals. ERC4626 vault provides permissionless withdraw/redeem for liquid assets. Validator operations distributed across 97+ PufferModules. PufferOracle is somewhat centralized (guardian-dependent) but does not block withdrawals of liquid assets if it fails. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol, [P1] PufferModules deployment |

**Infrastructure Counterparty Subtotal:**
- Raw scores: 9+3+3+9+9+9+9+9 = 60/72
- Adjusted: (60/72) x 45 = **37.5/45 (83.3%)**

---

#### Protocol Counterparty (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | None externally. Collateral remains exclusively on Ethereum Beacon Chain validators via PufferModules and EigenLayer restaking. No external protocol deployment, no CEX custody, no RWA exposure. Limited, high-quality counterparties: Ethereum (staking), EigenLayer (restaking). | 9 | 9 | Non-Improvable (optimal) | [P1] docs.puffer.fi architecture |
| ST-PC-02 | Are revenue-share or incentive arrangements documented? | Fee structure documented in code: exit fee currently 1% (hardcoded EXIT_FEE_BASIS_POINTS max 200), configurable daily withdrawal limits. Validator ticket mechanics documented. EigenLayer restaking reward flows transparent on-chain. All fee parameters visible in verified smart contracts. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol EXIT_FEE_BASIS_POINTS, [P1] docs.puffer.fi |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | No external counterparties at protocol level. Internal constraints enforced on-chain: daily withdrawal limits via dailyAssetsWithdrawalLimit, exit fee cap at 2% (hardcoded), AccessManager role-based controls. EigenLayer delegation spread across multiple RestakingOperators via 97+ PufferModules. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol, [P1] PufferModules delegation |
| ST-PC-04 | How quickly can positions be unwound from each counterparty? | No external counterparties. Unwinding via standard path requires Ethereum + EigenLayer unstaking (~14+ days). Instant withdrawal available via liquidity vault (~1-5 min, 1% fee) when funded. EigenLayer restaking positions can be exited through module delegation changes. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol withdraw/redeem |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Yes. EigenLayer dependency documented. PufferModules and RestakingOperators listed in deployment docs. All counterparty relationships are public and on-chain verifiable. | 9 | 9 | Non-Improvable (optimal) | [P1] mainnet.md deployment docs |

**Protocol Counterparty Subtotal:**
- Raw scores: 9+9+9+9+9 = 45/45
- Adjusted: 45/45 x 45 = **45.0/45 (100.0%)**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused? | Two withdrawal paths: (1) Instant via liquidity vault (~1-5 minutes, 1% fee), and (2) Standard via Ethereum + EigenLayer unstaking (~14+ days, no fee, requires claim after processing). Daily withdrawal limit (dailyAssetsWithdrawalLimit) may rate-limit instant exits. Protocol can be paused via Pauser Multisig calling Timelock.pause() -- this is protocol-wide, not address-level censorship. No evidence of address-level withdrawal blocking. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol ERC4626, [P0] Timelock.sol pause(), [P1] [Withdraw docs](https://docs.puffer.fi/yield/stakers/withdraw) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | With ~$61M TVL, near-total exit would require extended staggered processing via standard withdrawals (~14+ days due to Ethereum + EigenLayer unstaking). Instant withdrawals via liquidity vault (~1-5 min, 1% fee) are limited by vault funding. Daily withdrawal limit further constrains instant exits. Secondary market (DEX pools) thin relative to TVL. Near-100% redemption within a short window is uncertain. | 3 | 3 | Non-Improvable | [P0] Validator exit mechanics, [P3] DEX liquidity, [P1] [Withdraw docs](https://docs.puffer.fi/yield/stakers/withdraw) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No documented withdrawal delays, queues, or freezes for pufETH. Protocol has operated since early 2024 with ERC4626 withdraw available when liquid assets are present. TVL decline was gradual organic outflow over months, not a crisis-driven delay. No evidence of protocol-initiated withdrawal blocks. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol, [P3] DeFiLlama TVL history |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Yes. Instant withdrawals via liquidity vault charge a 1% fee (hardcoded max 2%) and are subject to dailyAssetsWithdrawalLimit. Standard withdrawals have no fee but take ~14+ days. During high utilization, the liquidity vault may be depleted, forcing users to the standard path. These caps restrict timely redemptions during high demand. | 3 | 9 | **Improvable** | [P0] PufferVaultV2.sol dailyAssetsWithdrawalLimit, [P1] [Withdraw docs](https://docs.puffer.fi/yield/stakers/withdraw) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | No. pufETH has not experienced a stress-driven redemption event. TVL decline was gradual over months. Per the battle-tested rule: untested protocols score Mid (3). | 3 | 3 | Non-Improvable | No stress events documented |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | Two withdrawal paths: (1) Instant via liquidity vault (~1-5 minutes, 1% fee) does not rely on unstaking; (2) Standard path requires Ethereum + EigenLayer unstaking (~14+ days, no fee). Both paths are clearly documented with accurate timeframes. Instant path available for users wanting immediate exit. No bridge dependency, no vesting lock-up. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol, [P1] [Withdraw docs](https://docs.puffer.fi/yield/stakers/withdraw) |
| ST-L-07 | Does redemption depend on secondary-market liquidity? | No. Primary exit is via ERC4626 vault withdraw/redeem functions directly against protocol. Secondary markets provide an additional exit option but are not required. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol withdraw/redeem |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | With ~$61M TVL and significant decline, secondary market depth for pufETH is limited. DEX liquidity pools for pufETH/ETH are thin relative to larger LSTs. Depth likely supports only ~3-10% of TVL without significant slippage. | 3 | 9 | **Improvable** | [P3] DEX liquidity data |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Untested. The daily withdrawal limit provides some bank-run protection by rate-limiting exits. However, no documented stress scenario or simulation exists. Per the battle-tested rule: untested protocols score Mid (3). | 3 | 3 | Non-Improvable | No stress testing documented |

**Liquidity Subtotal:**
- Raw scores: 9+3+9+3+3+9+9+3+3 = 51/81
- Adjusted: (51/81) x 45 = **28.3/45 (62.9%)**

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under stress? | pufETH has been live since February 2024 (2+ years) with no significant depeg events. The ERC4626 exchange rate has been monotonically increasing. During the 96% TVL decline from ~$1.7B to ~$61M (a significant liquidity stress event over months), pufETH maintained its peg without sharp dislocations. Secondary market pricing on CoinGecko confirms stable pufETH/ETH ratio throughout the protocol's lifetime. The gradual TVL decline constitutes a real-world stress scenario (confidence and liquidity drain) that pufETH survived without peg failure. | 9 | 9 | Non-Improvable (optimal) | [P3] CoinGecko pufETH data since Feb 2024, [P0] ERC4626 exchange rate history |
| ST-M-02 | Can adverse crypto market moves cause permanent losses? | Low risk. pufETH is unleveraged at protocol level with full ETH backing via validators. No directional exposure or leverage risk. Node operator bonds provide additional buffer against slashing. ETH-denominated LST tracks ETH directly. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol, ETH-denominated LST |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts? | Staking rate determined by Ethereum protocol, not by Puffer rate models. EigenLayer restaking adds supplementary yield but does not introduce rate model risk. TVL has shifted dramatically (96% decline) without rate model failure -- yield continued from underlying staking. No history of rate model failures. | 9 | 9 | Non-Improvable (optimal) | [P3] StakingRewards data, [P3] DeFiLlama |
| ST-M-04 | Have historic scenarios with high volatility been explicitly modeled? | No documented stress testing or simulation results. No formal high-volatility scenario modeling published. | 1 | 9 | **Improvable** | No stress test documentation found |
| ST-M-05 | Can sharp price moves trigger forced liquidations? | Not at protocol level. pufETH is unleveraged with full ETH backing via validators and EigenLayer restaking. No liquidation mechanism within the Puffer protocol. Users may leverage pufETH externally but the protocol itself has no liquidation triggers. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferVaultV2.sol -- no liquidation logic |

**Market Subtotal:**
- Raw scores: 9+9+9+1+9 = 37/45
- Adjusted: (37/45) x 45 = **37.0/45 (82.2%)**

---

**Strategy Total: 40.7 + 37.5 + 37.5 + 45.0 + 28.3 + 37.0 = 226.0/270 (83.7%)**

---

### OPERATIONS (30% Weight) -- Score: 164.6/270 (61.0%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes? | Active hybrid governance model. PUFFER token with vlPUFFER lock mechanism (30-day to 24-month lock, 1x-24x multiplier). Formal PIP process: 5-day discussion → 2-day Governance Review Committee evaluation → 14-day voting epoch every four Saturdays. vote.puffer.fi (Aragon-based) serves as on-chain voting platform; governance.puffer.fi (Discourse) as discussion forum with 35+ topics. PIP-1 (AVS Whitelisting) and PIP-2 (Gauge Removal Framework, passed with 3.4M vePUFFER votes for vs 202K against) demonstrate active governance. 21 incentive gauge proposals from external protocols. However, Community Multisig retains emergency execution with 0 delay -- hybrid model where governance covers major changes but multisig retains bypass capability. | 3 | 9 | **Improvable** | [P1] [vote.puffer.fi](https://vote.puffer.fi/), [P1] [governance.puffer.fi](https://governance.puffer.fi/), [P1] [Understanding Governance](https://docs.puffer.fi/yield/governance/understanding-governance) |
| O-G-02 | How concentrated is voting power among top holders? | PUFFER token (1B max supply) with documented allocation: 40% Ecosystem/Community, 26% Investors, 20% Early Contributors/Advisors, 7.5% S1 Airdrop, 5.5% S2 Airdrop, 1% Protocol Guild. vlPUFFER voting power is on-chain and publicly queryable. PIP-2 passed with 3.4M for vs 202K against, indicating active participation. However, top-holder concentration of vlPUFFER is not published -- insiders (investors + early contributors) hold 46% of tokens, suggesting potential concentration risk. | 3 | 9 | **Source Missing** | [P1] [PUFFER Token docs](https://docs.puffer.fi/yield/governance/token), [P1] PIP-2 vote results |
| O-G-03 | Are mechanisms in place to limit major changes? | 7-day hardcoded MINIMUM_DELAY for Operations Multisig via Timelock contract. Community Multisig has 0 delay (emergency bypass). The 7-day delay exceeds the 24h threshold for normal operations. | 9 | 9 | Non-Improvable (optimal) | [P0] Timelock.sol MINIMUM_DELAY |
| O-G-04 | Can the protocol replace the strategy manager without blocking withdrawals? | N/A -- pufETH is a liquid restaking token, not a vault with a replaceable strategy manager. | N/A | N/A | N/A | - |

**Governance Subtotal (3 scored questions, 1 N/A):**
- Raw scores: 3+3+9 = 15/27
- Adjusted: (15/27) x 67.5 = **37.5/67.5 (55.6%)**

---

#### Team & Legal (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified? | Yes. Puffer Finance LinkedIn page shows 26 employees with names and roles. Co-founders: Jason Vranek and Amir Forouzani (CEO). Company headquartered in San Francisco, CA, founded 2022. Series A funding (April 2024) with known investors (Binance Labs, Brevan Howard Digital, Lemniscap). Team members identifiable via LinkedIn, GitHub contributions, and public appearances. Tracxn and Crunchbase profiles confirm entity details. | 9 | 9 | Non-Improvable (optimal) | [P2] [LinkedIn - Puffer Finance](https://www.linkedin.com/company/puffer-finance/people/), [P4] Tracxn, Crunchbase profiles |
| O-TL-02 | Is the protocol dependent on a single developer? | No. Puffer Finance has 26 employees per LinkedIn, with multiple active GitHub contributors across the pufETH, Deployments-and-ACL, and related repositories. Co-founders Jason Vranek and Amir Forouzani lead the team. The breadth of protocol components (vault, oracle, modules, staking, governance) is supported by a full engineering team. Not dependent on a single developer. | 9 | 9 | Non-Improvable (optimal) | [P2] [LinkedIn - 26 employees](https://www.linkedin.com/company/puffer-finance/people/), [P1] GitHub contributors |
| O-TL-03 | What legal entity and jurisdiction operate the protocol? | Entity details limited. Puffer Finance website terms of service likely reference an entity but specific legal structure, jurisdiction, and registration details are not prominently disclosed in documentation. | 3 | 9 | **Source Missing** | [P1] docs.puffer.fi |
| O-TL-04 | Are there known investigations or regulatory actions? | No known enforcement actions against Puffer Finance. Ethereum Foundation grant recipient indicates positive regulatory standing. | 9 | 9 | Non-Improvable (optimal) | No enforcement actions found |
| O-TL-05 | Is there an on-call and incident response process? | No documented on-call process, SLA, or escalation path found. Pauser Multisig exists for emergencies but no published response time commitments or staffing details. | 1 | 9 | **Improvable** | No on-call documentation found |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Multiple support channels: Discord with support ticket system (discord.com/invite/pufferfi), Google Forms contact form (forms.gle/obHnypcjsLhVAkXj7), and documentation site. Structured support process demonstrates commitment to user issue resolution. | 9 | 9 | Non-Improvable (optimal) | [P1] puffer.fi, [P28] Discord, [P29] Contact Form |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Known investors: Lemniscap, Brevan Howard Digital, Binance Labs. Ethereum Foundation grant. Investors disclosed through press and documentation. | 9 | 9 | Non-Improvable (optimal) | [P4] Press coverage, [P1] docs.puffer.fi |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict? | N/A -- pufETH is a liquid restaking token, not a vault with a strategy manager. | N/A | N/A | N/A | - |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | N/A -- No strategy manager. | N/A | N/A | N/A | - |

**Team & Legal Subtotal (7 scored questions, 2 N/A):**
- Raw scores: 9+9+3+9+1+9+9 = 49/63
- Adjusted: (49/63) x 67.5 = **52.5/67.5 (77.8%)**

---

#### Documentation (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation on architecture and risks? | Comprehensive documentation at docs.puffer.fi covering: protocol architecture (PufferModules, Guardians, RestakingOperators, AccessManager), strategy mechanics (nLRT, validator tickets, rewards, staking), governance (mission, vlPUFFER token, understanding governance, PIPs), risk disclosures (validator slashing, AVS operator slashing, withdrawal constraints), institutional solutions, node operator requirements, FAQ, and glossary. GitHub provides additional technical docs (PufferVaultV2.md, Timelock.md, PufferOracle.md). Documentation updated to reflect Season 2 and current governance structure. | 9 | 9 | Non-Improvable (optimal) | [P1] [docs.puffer.fi](https://docs.puffer.fi/), [P1] GitHub docs |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Documentation provides end-to-end collateral flow: ETH deposited into PufferVault → allocated to validators via PufferModules → rewards accrue → pufETH conversion rate increases. Loss scenarios explicitly documented: (1) validator slashing exceeding NoOp 2 ETH bond burns pufETH backing, (2) AVS operator slashing reduces pufETH value, (3) withdrawal constraints from daily limits. Conversion rate formula published: (deposits + rewards − penalties) / pufETH supply. Bond mechanics documented as first-loss buffer. | 9 | 9 | Non-Improvable (optimal) | [P1] [nLRT docs](https://docs.puffer.fi/yield/protocol/nlrt), [P1] [Rewards docs](https://docs.puffer.fi/yield/protocol/rewards) |
| O-DT-03 | Are all contract addresses documented in one canonical place? | Yes. Deployments-and-ACL repo (mainnet.md) provides a canonical registry of all deployed contract addresses with roles and implementations. Well-maintained deployment documentation. | 9 | 9 | Non-Improvable (optimal) | [P1] mainnet.md deployment registry |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Central role registry in Deployments-and-ACL GitHub repo (mainnet.md) lists all contract addresses with roles and implementations. AccessManager role-based system documented in code and docs. Timelock roles (COMMUNITY_MULTISIG, OPERATIONS_MULTISIG, pauserMultisig) clearly defined with scope. Change history maintained via Git commits on the public repository. Governance changes tracked through PIP proposals on governance.puffer.fi with public discussion and voting records (PIP-1: AVS Whitelisting, PIP-2: Gauge Removal Framework). | 9 | 9 | Non-Improvable (optimal) | [P1] [Deployments-and-ACL](https://github.com/PufferFinance/Deployments-and-ACL), [P1] [governance.puffer.fi](https://governance.puffer.fi/) |
| O-DT-05 | Does the protocol publish proof-of-reserves? | ERC4626 totalAssets() provides real-time on-chain proof-of-reserves for liquid vault holdings (WETH, ETH, stETH). PufferOracle provides proof-of-reserves for validator-locked ETH via Guardian consensus (7/8 majority required). Guardian roles and consensus requirements documented. Methodology is on-chain and verifiable. Coverage comprehensive across all protocol assets. Guardians are "respected community members" with protocol investment and alignment incentives. Roadmap for further decentralization via EIP-7002/4788/2537. | 9 | 9 | Non-Improvable (optimal) | [P0] PufferOracle.sol, [P0] PufferVaultV2.sol totalAssets(), [P1] [Guardians docs](https://docs.puffer.fi/yield/protocol/guardians) |
| O-DT-06 | Are all contracts verified on block explorers? | Yes. All core contracts verified on Etherscan with full source code available. UUPS proxy pattern with publicly viewable implementation contracts. | 9 | 9 | Non-Improvable (optimal) | [P0] Etherscan verified contracts |

**Documentation Subtotal:**
- Raw scores: 9+9+9+9+9+9 = 54/54
- Adjusted: (54/54) x 67.5 = **67.5/67.5 (100.0%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | No dedicated safety module or backstop reserve found. No insurance fund equivalent. Operator bonds in PufferModules provide some first-loss buffer for slashing but no general-purpose backstop. | 1 | 9 | **Improvable** | No safety module found |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | No meaningful backstop reserves. DeFiLlama treasury API returns no data. PUFFER token market cap is ~$11.7M. DAO treasury (Aera vault listed in deployments) size and composition unknown. No dedicated safety module. Operator bonds in PufferModules provide some first-loss buffer for slashing but not a general-purpose reserve. With ~$61M TVL, verifiable backstop reserves appear to be <1% of TVL. | 1 | 9 | **Improvable** | [P3] DeFiLlama -- no treasury data |
| O-FR-03 | What is the estimated operational runway? | Cannot be estimated from disclosed information. TVL declined 96% (from ~$1.7B to ~$61M), dramatically reducing fee revenue. No published cost structure, revenue model, or runway estimates. VC funding provides some buffer but duration unknown. | 1 | 9 | **Improvable** | [P3] DeFiLlama TVL decline data |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Untested under acute stress. TVL decline was gradual (months), not a crisis event. No evidence of protocol behavior during rapid market volatility. Per the battle-tested rule: untested protocols score Mid (3). | 3 | 3 | Non-Improvable | No stress events documented |
| O-FR-05 | Can the protocol remain safe if team disappears? | Partial. ERC4626 vault provides permissionless withdraw/redeem for liquid assets (WETH, ETH, stETH). However, PufferOracle relies on guardian signatures to track validator-locked ETH -- if guardians are team-adjacent and disappear, oracle stops updating. Community Multisig signer identities are undisclosed, so independent operation cannot be confirmed. No on-chain governance exists (unlike RocketPool's pDAO). Protocol would degrade significantly without team: stale oracle, no upgrades, no validator management. Core withdrawal path remains functional but protocol health would deteriorate. | 3 | 9 | **Improvable** | [P0] PufferOracle.sol guardian dependency, [P0] PufferVaultV2.sol ERC4626 permissionless |

**Financial Resilience Subtotal:**
- Raw scores: 1+1+1+3+3 = 9/45
- Adjusted: (9/45) x 67.5 = **13.5/67.5 (20.0%)**

---

**Operations Total: 37.5 + 52.5 + 67.5 + 13.5 = 171.0/270 (63.3%)**

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 79 | 99 | 143.6 | 180 | 79.8% |
| | Key Management (7 of 8 Q scored) | 49 | 63 | 140.0 | 180 | 77.8% |
| | **Security Subtotal** | | | **283.6** | **360** | **78.8%** |
| **Strategy** | Protocol Mechanics (7 of 9 Q scored) | 57 | 63 | 40.7 | 45 | 90.5% |
| | Collateral (4 Q) | 30 | 36 | 37.5 | 45 | 83.3% |
| | Infra Counterparty (8 Q) | 60 | 72 | 37.5 | 45 | 83.3% |
| | Protocol Counterparty (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity (9 Q) | 51 | 81 | 28.3 | 45 | 63.0% |
| | Market (5 Q) | 37 | 45 | 37.0 | 45 | 82.2% |
| | **Strategy Subtotal** | | | **226.0** | **270** | **83.7%** |
| **Operations** | Governance (3 of 4 Q scored) | 15 | 27 | 37.5 | 67.5 | 55.6% |
| | Team & Legal (7 of 9 Q scored) | 49 | 63 | 52.5 | 67.5 | 77.8% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 9 | 45 | 13.5 | 67.5 | 20.0% |
| | **Operations Subtotal** | | | **171.0** | **270** | **63.3%** |
| **TOTAL** | | | | **680.6** | **900** | **75.6%** |

---
