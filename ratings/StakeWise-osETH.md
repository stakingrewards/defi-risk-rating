# StakeWise - osETH Risk Rating

**Rating Date**: 2026-03-31
**Final Grade**: BB+
**Total Score**: 788.4/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-beta

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 332.0/360 (92.2%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 7 independent audits: Halborn (May 2023, Aug 2023), Sigma Prime (Aug 2023, Jun 2024, Sep 2024), ConsenSys Diligence (Mar 2024), ABDK (Sep 2025). All core fund-custody/routing contracts covered with public reports. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub Audits](https://github.com/stakewise/v3-core/tree/main/audits) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent: ABDK (Sep 2025) -- not on SR tier list. Prior: Sigma Prime (Tier-0, Sep 2024), ConsenSys Diligence (Tier-0, Mar 2024). Multiple Tier-0 auditors on recent codebase. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub Audits](https://github.com/stakewise/v3-core/tree/main/audits), [P1] [ConsenSys Audit](https://diligence.security/audits/2024/03/stakewise-v3-vaults-/-ethfoxvault/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. SWIP-25 Vault Factory v3 upgrade (Nov 2024) was audited by Sigma Prime and Hexens (Sep 2024) before deployment. Core contracts (OsToken, Keeper, VaultController) are non-upgradeable, eliminating upgrade risk. | 9 | 9 | Non-Improvable (optimal) | [P2] [SWIP-25](https://forum.stakewise.io/t/swip-25-upgrade-vault-factory-to-v3-and-introduce-the-stakewise-boost-feature/1725) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | ConsenSys Diligence Mar 2024: 0 critical, 0 major, 5 medium (4 acknowledged, 1 fixed), 11 minor. Sigma Prime Aug 2023: 2 critical, 5 high -- all resolved. Acknowledged items are documented design decisions. | 9 | 9 | Non-Improvable (optimal) | [P1] [ConsenSys Audit](https://diligence.security/audits/2024/03/stakewise-v3-vaults-/-ethfoxvault/) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Core contracts (OsToken, OsTokenVaultController, Keeper, PriceFeed) are non-upgradeable. Vault contracts use UUPSUpgradeable requiring dual approval (vault admin + DAO). SafeSnap provides 48h delay. No emergency bypass documented. | 9 | 9 | Non-Improvable (optimal) | [P0] [OsToken Etherscan](https://etherscan.io/address/0xf1C9acDc66974dFB6dEcB12aA385b9cD01190E38) -- not a proxy |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No exploit of StakeWise's own contracts. The Nov 2025 Balancer hack drained 6,851 osETH from Balancer V2 pools (external Balancer vulnerability). StakeWise DAO recovered 73.5% ($19M) via emergency token burn/mint. Remaining 26.5% (~$7M) unrecovered but this was a Balancer vulnerability, not StakeWise. | 9 | 9 | Non-Improvable (optimal) | [P4] [Crypto.news recovery](https://crypto.news/balancer-hack-update-stakewise-recovers-oseth-2025/), [P0] On-chain recovery txs |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No. Protocol operational since 2021. Founded by Dmitri Tsumak and Kirill Kutakov, publicly identified. ~$2M fundraise disclosed. No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P4] [Crunchbase](https://www.crunchbase.com/person/dmitri-tsumak), [P1] [StakeWise](https://stakewise.io) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | SafeSnap module has 24h question timeout + 24h cooldown (48h effective). No reductions documented in last 12 months. SWIP-25 added features without reducing timelocks. | 9 | 9 | Non-Improvable (optimal) | [P2] [Governance Forum](https://forum.stakewise.io), [P1] SafeSnap parameters |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active Immunefi bounty: max $200,000 for critical smart contract bugs, $50,000 for high. 14 smart contracts + 1 web app in scope. Payouts in SWISE or USDC. $200K max >= $100K threshold. | 9 | 9 | Non-Improvable (optimal) | [P1] [Immunefi StakeWise](https://immunefi.com/bug-bounty/stakewise/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Internal monitoring and alerting systems are in place for core components: DAO governance, oracle votes, osETH APY changes, deposits/withdrawals, with some exposed publicly (status.stakewise.io for oracles, Discord for DAO governance). However, monitoring lacks demonstrated connection to automated protective actions or documented response SLAs under 15 minutes. Monitoring exists but cannot automatically trigger protective actions beyond the KeeperRewards APY cap. | 3 | 9 | **Improvable** | [P0] [Oracle status](https://status.stakewise.io/), [P1] [DAO governance Discord](https://discord.com/channels/613394789882134529/851471420781494342) |
| S-SC-11 | Are automatic safety controls (e.g. pause, circuit breakers) triggered by monitoring alerts? | KeeperRewards.sol contract automatically caps osETH APY to protect holders from inflation attacks -- a genuine on-chain circuit breaker with clear trigger conditions. For an LST with no automated allocation mechanisms, this covers the main risk vector (oracle/inflation attack). No broader pause function in core contracts, but core contracts are immutable, limiting attack surface. | 9 | 9 | Non-Improvable (optimal) | [P1] KeeperRewards.sol [automatically caps osETH APY](https://github.com/stakewise/v3-core/blob/main/contracts/keeper/KeeperRewards.sol) |

**Smart Contract Security Subtotal:**
- Raw scores: 9+9+9+9+9+9+9+9+9+3+9 = 93/99
- Adjusted: (93/99) x 180 = **169.1/180 (93.9%)**

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | OsTokenVaultController owner is the DAO multisig (4-of-7 Gnosis Safe at 0x144a98cb1CdBb23610501fE6108858D9B7D24934). SafeSnap module enables SWISE governance execution. 7 signers confirmed via Safe API (March 2026). Changes documented via SWIPs. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Multisig](https://etherscan.io/address/0x144a98cb1CdBb23610501fE6108858D9B7D24934), [P0] Safe API: 4-of-7 threshold, 7 owners confirmed |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. OsToken minting/burning requires registered vault controllers. Vault upgrades require dual approval (vault admin + DAO). DAO operations require 4-of-7 multisig (threshold >=3, signers >=5). SafeSnap adds 48h delay (>=24h). 4-of-7 explicitly meets Low (9) criteria. Emergency Balancer recovery required full 4-of-7 consensus. | 9 | 9 | Non-Improvable (optimal) | [P0] OsToken contract: setController() is owner-only (4-of-7 multisig), [P1] SafeSnap 48h delay |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | 4-of-7 Gnosis Safe with 7 signers confirmed via Safe API (March 2026). Previously publicly identified: Ali Nuraldin, Andreas Dittrich, Auryn Macmillan, Dmitri Tsumak, Gleb Dudka, Mikko Ohtamaa, Otto de Voogd. Meets >=3-of-5 threshold with >=3 independent individuals. No multisig changes in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P0] Safe API: 7 owners confirmed, [P0] [Etherscan](https://etherscan.io/address/0x144a98cb1CdBb23610501fE6108858D9B7D24934) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No pause function in core contracts. No address-level censorship. Vault admins can set blocklists only on opt-in BlocklistVault variants. Withdrawals are permissionless on-chain. No arbitrary blocking possible. | 9 | 9 | Non-Improvable (optimal) | [P0] No pause in OsToken/Keeper/VaultController code |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of staked ETH held in non-custodial on-chain vault contracts. Validators registered on-chain through Keeper/DepositDataRegistry. No off-chain custody. | 9 | 9 | Non-Improvable (optimal) | [P0] Vault contracts hold ETH on-chain |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. User funds in individual vault contracts, separate from DAO treasury (0x144a...4934). Treasury holds only ~$323K. No co-mingling. | 9 | 9 | Non-Improvable (optimal) | [P0] [Treasury](https://etherscan.io/address/0x144a98cb1CdBb23610501fE6108858D9B7D24934): ~$323K |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- osETH is an LST product, not a managed vault strategy. Vaults stake ETH to Ethereum validators only. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No formally documented and recently tested playbook with tabletop exercises. However, replacement of multisig signers (SWIP-13) and oracle operators (SWIP-20) has been executed following industry best practices (announce ahead of time, execute, keep records), demonstrating informal capability. Balancer hack recovery (Nov 2025) showed rapid ad-hoc response. Meets Mid (3): informal playbook with demonstrated precedent but no formal tabletop/simulation in last 12 months. | 3 | 9 | **Improvable** | [P1] [Multisig rotation](https://forum.stakewise.io/t/swip-13-rotate-stakewise-dao-multisig-signers/809), [P1] [Oracle rotation](https://forum.stakewise.io/t/swip-20-change-the-oracle-config-on-gnosis-chain-to-replace-an-oracle/1624) |

**Key Management Subtotal (7 of 8 scored):**
- Raw scores: 9+9+9+9+9+9+3 = 57/63
- Adjusted: (57/63) x 180 = **162.9/180 (90.5%)**

**Security Total: 169.1 + 162.9 = 332.0/360 (92.2%)**

### STRATEGY (30% Weight) -- Score: 260.25/270 (96.4%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | 100% of yield from Ethereum consensus + execution layer staking rewards (attestation, block proposals, MEV). 5% fee to DAO treasury. Fully aligned with ETH liquid staking mandate. ~3-4% APY. | 9 | 9 | Non-Improvable (optimal) | [P0] OsTokenVaultController: avgRewardPerSecond, [P1] [osToken docs](https://docs.stakewise.io/docs/ostoken/how-ostoken-works) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to tail events: mass validator slashing exceeding 10% overcollateralization buffer, extreme sustained negative consensus rewards, or smart contract exploit. Overcollateralization provides substantial buffer. | 9 | 9 | Non-Improvable (optimal) | [P1] [osToken docs](https://docs.stakewise.io/docs/ostoken/how-ostoken-works) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage in base osETH product. StakeWise Boost is a separate optional product. osETH minting at 90% LTV is overcollateralization, not leverage. No rehypothecation. | 9 | 9 | Non-Improvable (optimal) | [P1] Docs: Boost is separate |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- LST product. osETH has automated liquidation mechanics for positions exceeding LTV thresholds (redemption at 91.5%, liquidation at 92%), but these protect the system, not a lending position. | N/A | N/A | N/A | - |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss events for osETH or comparable ETH LST strategies in last 24 months. Balancer exploit affected LP positions, not osETH staking. osETH exchange rate has monotonically increased since launch. | 9 | 9 | Non-Improvable (optimal) | [P0] osETH exchange rate history |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | N/A -- LST product, not a managed vault. | N/A | N/A | N/A | - |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | 100% organic yield from Ethereum staking rewards. No token emissions in osETH yield. 5% protocol fee from staking rewards. Fully sustainable. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain fee structure |
| ST-PM-08 | Can the position be fully unwound without slippage turning yield negative? | osETH redeemable at fair exchange rate in-protocol. Instant if unbonded ETH available, otherwise 8-day validator exit. DEX provides additional exit path but current 24h volume very low (~$127). In-protocol redemption at fair rate ensures slippage does not flip yield negative regardless of DEX conditions. | 9 | 9 | Non-Improvable (optimal) | [P0] In-protocol redemption at fair rate, [P3] CoinGecko: ~$127 24h volume (March 2026) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | osETH backed by staked ETH with overcollateralization. Yield from staking rewards, not spreads or funding rates. Exchange rate determined by accumulated rewards, not market forces. | 9 | 9 | Non-Improvable (optimal) | [P1] Docs: repricing token |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | N/A -- osETH is an LST where users deposit ETH directly into permissionless vaults that stake to Ethereum validators. No curator/allocator layer, no automated capital allocation mechanisms, no public allocator, and no auto-rebalancers for the base osETH product. Individual vaults have a fixed strategy (stake ETH). While StakeWise V3 introduced MetaVaults with a permissionless `depositToSubVaults()` function and BalancedCurator, this is a separate product layer and does not affect the core osETH staking flow. | N/A | N/A | N/A | [P0] [v3-core contracts](https://github.com/stakewise/v3-core) |

**Protocol Mechanics Subtotal (7 of 10 scored):**
- Raw scores: 9+9+9+9+9+9+9 = 63/63
- Adjusted: (63/63) x 45 = **45.0/45 (100.0%)**

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | osETH backed exclusively by native ETH staked on Ethereum validators. ETH is a large-cap established asset (Tier-0 chain native token). No other collateral types. | 9 | 9 | Non-Improvable (optimal) | [P0] Vault contracts accept only ETH |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | osETH maintained peg stability through multiple events: +2.8% positive depeg May 2024 resolved within days; Nov 2025 Balancer hack (~6,851 osETH stolen from LP pool, 73.5% recovered in 90 min) did not break osETH's internal exchange rate. osETH exchange rate has monotonically increased. Overcollateralization buffer unbreached. | 9 | 9 | Non-Improvable (optimal) | [P0] osETH exchange rate history, [P1] Balancer hack recovery (Nov 2025) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | 10% overcollateralization buffer absorbs slashing. Genesis Vault (~171,975 ETH, ~5,374 validators) operated by multiple entities: CryptoManufaktur, T-Systems (formerly Deutsche Telekom), Finoa, StakeWise Labs. Migrating to Obol DVT (announced April 2025). Liquidation at 92% LTV. Permissionless vaults allow any operator. | 9 | 9 | Non-Improvable (optimal) | [P0] [Genesis Vault](https://app.stakewise.io/vault/mainnet/0xac0f906e433d58fa868f936e8a43230473652885), [P1] Obol DVT migration |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | 0% bridged or wrapped. osETH backed entirely by native ETH on Ethereum. No bridge dependency. | 9 | 9 | Non-Improvable (optimal) | [P0] Vault contracts hold native ETH |

**Collateral Subtotal:**
- Raw scores: 9+9+9+9 = 36/36
- Adjusted: (36/36) x 45 = **45.0/45 (100.0%)**

#### Infra Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum (Tier-0). StakeWise custom oracle network (11 operators, 7-of-11). RedStone (Tier-1) for DeFi pricing. Chainlink (Tier-0) on Arbitrum/Linea. No bridges, CEXs, or off-chain wallets. All external dependencies Tier-0/1. Internal oracle is custom. | 9 | 9 | Non-Improvable (optimal) | [P1] [RedStone integration](https://blog.redstone.finance/2024/01/05/case-study-stakewise-integrates-redstone-oracles-to-bring-oseth-to-defi/) |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | Internal oracle (11 operators, 7-of-11 consensus, open-source code) is used solely for reporting validator rewards to update the osETH exchange rate — not for pricing. DeFi pricing uses RedStone (Tier-1, aggregates 3 DEX sources) and Chainlink (Tier-0) on L2s. No bridge dependency. All external pricing oracles are Tier-0/1. Oracle values are updatable by the network, not hardcoded. No hardcoded pricing. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle GitHub](https://github.com/stakewise/oracle), [P1] RedStone |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Seven of eleven oracle operators report ISO 27000/27001 or SOC2 Type II certifications: Deutsche Telekom MMS, Finoa, DSRV, P2P.org, Chorus One, Sensei Node, StakeFish. Four remaining operators uncertified or certification status unknown. Criteria requires "all critical off-chain providers" for Low risk; 7/11 is Moderate risk. | 3 | 9 | **Improvable** | [P1] [Deutsche Telekom MMS](https://www.telekom-mms.com/ueber-uns/unternehmen), [P1] [DSRV](https://kr.aving.net/news/articleView.html?idxno=1770861), [P1] [P2P.org](https://p2p.org/economy/p2p-org-achieves-soc-2-type-ii-certification/), [P1] [Chorus One](https://security.chorus.one/), [P1] [Sensei Node](https://www.senseinode.com/en/security), [P1] [StakeFish](https://blog.stake.fish/stakefish-completes-soc-2-type-ii-certification-for-non-custodial-blockchain-staking-services/) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Protocol operational since late 2023 (V3). No documented infrastructure outages. No chain-level incidents on Ethereum affecting StakeWise. Deployed >6 months with no incidents. | 9 | 9 | Non-Improvable (optimal) | [P1] No incident reports |
| ST-IC-05 | Has the base chain recently halted block production? | Ethereum has not halted or experienced consensus failure in last 12 months. Most battle-tested smart contract platform. | 9 | 9 | Non-Improvable (optimal) | [P0] Ethereum chain stability |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | No slashing events affecting StakeWise validators through March 2026. No liquidations have occurred to date. Overcollateralization buffer unbreached. Genesis Vault maintains 99.67% performance metric. | 9 | 9 | Non-Improvable (optimal) | [P0] No slashing reports (verified March 2026), [P0] Genesis Vault performance |
| ST-IC-07 | Are validators diverse geographically and by operator? | osETH is minted from vaults run by a diverse node operator set: StakeWise Labs (Genesis Vault), Chorus One (Chorus One Max Vault), NodeSet (constellation of 100+ geographically distributed home operators via NodeSet Private Vault), and others across 40+ vaults. osETH minting and vault creation are permissionless, enabling any operator to join. Multi-vault architecture means no single operator dominates osETH backing. | 9 | 9 | Non-Improvable (optimal) | [P0] [StakeWise Vaults page](https://app.stakewise.io/vaults) |
| ST-IC-08 | Can any single infra failure block withdrawals or cause losses? | Withdrawals are permissionless via FIFO queue on every Vault contract. Oracle failure delays finalization of new requests but does not block claiming of already-finalized requests. Users have direct on-chain withdrawal path. Multiple redundancy layers exist. No single component is a permanent single point of failure for exits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Withdrawal Queue](https://github.com/stakewise/v3-core/blob/main/contracts/libraries/ExitQueue.sol) |

**Infra Counterparty Subtotal:**
- Raw scores: 9+9+3+9+9+9+9+9 = 66/72
- Adjusted: (66/72) x 45 = **41.25/45 (91.7%)**

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Staked ETH deployed only to Ethereum validators. No external protocol, CEX, or RWA deployment. All on-chain via Beacon Chain. | 9 | 9 | Non-Improvable (optimal) | [P0] Deposits to Ethereum deposit contract only |
| ST-PC-02 | Are revenue-share or incentive arrangements documented? | 5% DAO fee from staking rewards documented. Vault operators set own fees (documented). SWISE liquidity incentives documented via SWIPs. No undisclosed arrangements. | 9 | 9 | Non-Improvable (optimal) | [P1] Docs: 5% DAO fee, [P2] SWIPs |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | No external counterparty exposure. Validator deposits to Ethereum's deposit contract. Individual vault operator counts transparent on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain validator registrations |
| ST-PC-04 | How quickly can positions be unwound from each counterparty? | Unstaking from validators: 8-day escrow + Ethereum exit queue. In-protocol instant if unbonded ETH available. DEX exit immediate. Well-documented paths. | 9 | 9 | Non-Improvable (optimal) | [P1] Docs: 8-day escrow |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | N/A -- permissionless staking protocol. Users choose vault operators. Genesis Vault operators disclosed. No custody providers or asset managers. | N/A | N/A | N/A | - |

**Protocol Counterparty Subtotal (4 of 5 scored):**
- Raw scores: 9+9+9+9 = 36/36
- Adjusted: (36/36) x 45 = **45.0/45 (100.0%)**

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain redemption: burn osETH to unlock staked ETH. No pause mechanism. No address-level blocking. If unbonded ETH insufficient, validators exit (8-day escrow). Fully permissionless. | 9 | 9 | Non-Improvable (optimal) | [P0] No pause in contract code, [P1] Docs: redemption |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | osETH total supply ~$450M. DEX 24h volume ~$0.5M (March 2026). In-protocol redemption at fair rate remains functional. Demonstrated large-scale exit: 33% of TVL (91K osETH) redeemed July 20-Aug 11, 2025 without issues per Etherscan. Full TVL exit requires validator exits (8-day + Ethereum queue). Primary exit path is in-protocol, not DEX-dependent. | 9 | 9 | Non-Improvable (optimal) | [P0] In-protocol redemption, [P0] [Etherscan osETH supply history](https://etherscan.io/tokencheck-tool?t=0xf1c9acdc66974dfb6decb12aa385b9cd01190e38), [P3] CoinGecko: ~$0.5M 24h volume |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No documented withdrawal delays, queues, or freezes. Protocol operational since late 2023 (V3). Standard 8-day escrow applies as documented. | 9 | 9 | Non-Improvable (optimal) | [P1] No delay reports |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | osETH capacity limits control minting, not redemption. Redemption always available. No outflow caps. | 9 | 9 | Non-Improvable (optimal) | [P1] Docs: capacity limits minting only |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Protocol operational since 2021, navigating multiple crypto-wide stress events without outages or liquidity shortages. Balancer hack (Nov 2025) destroyed primary DEX liquidity pool but osETH holders unaffected -- in-protocol redemption remained functional throughout. New liquidity established on Fluid (Jan 2026). DEX 24h volume ~$0.5M (March 2026). In-protocol redemption at fair rate ensures exits remain viable regardless of DEX conditions. | 9 | 9 | Non-Improvable (optimal) | [P3] [CoinGecko: ~$0.5M 24h volume](https://www.coingecko.com/en/coins/stakewise-staked-eth), [P1] Balancer hack Nov 2025, [P1] [Fluid liquidity Jan 2026](https://x.com/stakewise_io/status/2012138263344300047) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | When unbonded ETH insufficient, validator exits required (8-day escrow). This is the documented withdrawal period. Less than 10% typically in exit queue. DEX provides immediate alternative. | 9 | 9 | Non-Improvable (optimal) | [P1] Docs: 8-day escrow documented |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | In-protocol redemption at fair exchange rate without DEX dependency. DEX provides supplementary exit (Balancer, Curve, Uniswap, Fluid). Most users can exit via protocol path. Secondary markets optional. | 9 | 9 | Non-Improvable (optimal) | [P1] Docs: in-protocol redemption |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | Collateral is native ETH — deep liquidity across all major venues. osETH market cap ~$407-450M with ~$0.5M DEX 24h volume (March 2026). Post-Balancer hack (Nov 2025), primary liquidity moved to Fluid (Jan 2026). DEX depth is thin relative to market cap, but in-protocol redemption at fair exchange rate provides the primary exit path and can handle large volumes (33% TVL demonstrated July-Aug 2025). Combining in-protocol + DEX, osETH can absorb >10% of TVL exits. | 9 | 9 | Non-Improvable (optimal) | [P3] [CoinGecko: ~$0.5M 24h volume](https://www.coingecko.com/en/coins/stakewise-staked-eth), [P0] In-protocol redemption at fair rate |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | 10% overcollateralization buffer provides protection. Mass exit triggers validator exits (8-day + Ethereum queue). No leverage in base product. Tested at scale: 33% of TVL (91K osETH) redeemed July 20-Aug 11, 2025 without issues per Etherscan. Design, buffers, and demonstrated unwind capability indicate rapid mass exit would primarily cause temporary queues without permanent depositor haircuts. Significant osETH concentration in Aave from leveraged staking strategies noted. | 9 | 9 | Non-Improvable (optimal) | [P0] [osETH supply history](https://etherscan.io/tokencheck-tool?t=0xf1c9acdc66974dfb6decb12aa385b9cd01190e38) |

**Liquidity Subtotal:**
- Raw scores: 9+9+9+9+9+9+9+9+9 = 81/81
- Adjusted: (81/81) x 45 = **45.0/45 (100%)**

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | osETH maintained internal exchange rate stability through 28 months of operation including: +2.8% positive depeg May 2024 (resolved in days); Balancer hack Nov 2025 (~$25M exploit on LP pool) -- osETH internal rate unaffected, DAO recovered 73.5% in 90 min. No negative depegs >2%. Exchange rate has monotonically increased since launch. Multiple ETH drawdowns navigated without incident. | 9 | 9 | Non-Improvable (optimal) | [P0] osETH exchange rate history, [P1] Balancer hack Nov 2025 recovery |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | osETH backed by staked ETH. No leverage. ETH market risk inherent to all ETH LSTs. Low-beta relative to ETH. Overcollateralization protects against slashing but not ETH price decline (which is expected by ETH stakers). | 9 | 9 | Non-Improvable (optimal) | [P1] Docs: no leverage |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Staking yield determined by Ethereum protocol. No utilization-based rate curves. Oracle-set avgRewardPerSecond based on actual validator performance. Dynamic rate adjustment prevents any LTV from exceeding 100% (oracles adjust downward if vault underperforms). No fixed APR cap -- adaptive mechanism. No reflexive incentive models. | 9 | 9 | Non-Improvable (optimal) | [P1] [Docs: avgRewardPerSecond](https://docs.stakewise.io/docs/ostoken/how-ostoken-works) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | No formal stress testing documentation published. Overcollateralization model provides implicit stress protection but formal scenario modeling undocumented. The Balancer hack (Nov 2025) was a real-world stress event but affected LPs, not osETH holders directly. No published stress-test or VaR analysis. | 3 | 9 | **Source Missing** | [P1] No stress test documentation found |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | No leverage in base osETH product. osETH position liquidation at 92% LTV protects the system, not individual holders. Base osETH holders face no liquidation risk from sharp price moves. | 9 | 9 | Non-Improvable (optimal) | [P1] Docs: liquidation protects system |

**Market Subtotal:**
- Raw scores: 9+9+9+3+9 = 39/45
- Adjusted: (39/45) x 45 = **39.0/45 (86.7%)**

**Strategy Total: 45.0 + 45.0 + 41.25 + 45.0 + 45.0 + 39.0 = 260.25/270 (96.4%)**

### OPERATIONS (30% Weight) -- Score: 196.1/270 (72.6%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes? | Hybrid: SWISE token voting via Snapshot + SafeSnap execution through 4-of-7 Gnosis Safe. SafeSnap provides 48h delay. 200K SWISE bond for proposals. DAO controls core parameters. Vault upgrades require dual approval. Multisig can execute within governance-approved bounds but also reject. | 3 | 9 | **Improvable** | [P2] [Snapshot](https://snapshot.box/#/s:stakewise.eth), [P1] SafeSnap parameters |
| O-G-02 | How concentrated is voting power among top holders? | 1B SWISE total, ~754M circulating. 25% investors (vested), 25% founders (vested), 50% community. Low voter turnout reported. Insider allocation of ~50% suggests moderate concentration. Specific top-10 data not available. | 3 | 3 | Non-Improvable | [P3] CoinMarketCap: distribution |
| O-G-03 | Are mechanisms in place to limit major changes? | SafeSnap: 48h effective delay (24h timeout + 24h cooldown). 200K SWISE bond. 4-of-7 multisig can reject transactions (4 required to reject). 48h exceeds 24h minimum. No formal veto beyond multisig rejection. | 9 | 9 | Non-Improvable (optimal) | [P1] SafeSnap parameters, [P0] SafeSnap module |
| O-G-04 | Can the protocol replace the strategy manager without blocking withdrawals? | N/A -- LST, not managed vault. | N/A | N/A | N/A | - |

**Governance Subtotal (3 of 4 scored):**
- Raw scores: 3+3+9 = 15/27
- Adjusted: (15/27) x 67.5 = **37.5/67.5 (55.6%)**

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified? | Co-founders Dmitri Tsumak (Tallinn, Estonia) and Kirill Kutakov publicly identified with LinkedIn. Legal entity: Creative Tech Free Zone Co., UAE. 7 multisig signers publicly named. Team active since 2021. | 9 | 9 | Non-Improvable (optimal) | [P4] [LinkedIn](https://ee.linkedin.com/in/dmitri-tsumak), [P4] [Crunchbase](https://www.crunchbase.com/person/dmitri-tsumak) |
| O-TL-02 | Is the protocol dependent on a single developer? | Permissionless vault model with 100+ node operators across 40+ vaults means protocol operations do not depend on a single team. 11 independent oracle operators provide service decentralization. Core smart contracts are immutable, reducing ongoing code-change dependency. While StakeWise Labs remains the primary core code contributor (v3-core repo), the protocol can run and be modified by multiple independent teams given the permissionless architecture. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub v3-core](https://github.com/stakewise/v3-core), [P0] [StakeWise Vaults](https://app.stakewise.io/vaults) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol? | Decentralized DAO structure for the open-source protocol. Creative Tech FZCO incorporated in the UAE operates StakeWise front-end to enable access to smart contracts. Entity clearly named, registered in UAE free zone, and mapped to operational responsibilities (front-end operation). Non-custodial staking does not require VARA registration. | 9 | 9 | Non-Improvable (optimal) | [P1] [StakeWise Terms of Service](https://app.stakewise.io/terms-and-conditions): UAE entity confirmed |
| O-TL-04 | Are there known investigations or regulatory actions? | No known investigations or regulatory actions. UAE VARA has not extended oversight to non-custodial staking. No enforcement actions documented. | 9 | 9 | Non-Improvable (optimal) | [P4] VARA public register checked |
| O-TL-05 | Is there an on-call and incident response process? | Demonstrated in practice: Balancer hack (Nov 2025) saw emergency multisig powers invoked within hours, 73.5% of stolen osETH recovered. Governance multisig explicitly mandated to step in to veto malicious SafeSnap transactions. Oracle set operates under SLAs. However, formal 24/7 on-call documentation with specific response SLAs not publicly available. Meets Mid (3): informal on-call with demonstrated capability but without formal documented SLAs. | 3 | 9 | **Improvable** | [P1] [StakeWise Governance Docs](https://docs.stakewise.io/docs/governance/dao-treasury#current-committee-members-multisig), [P1] [Oracle set SLAs](https://forum.stakewise.io/t/stakewise-v3-oracle-network/1321) |
| O-TL-06 | Does the team provide timely support for critical issues? | Discord and Telegram channels active. Governance forum responsive. Balancer hack (Nov 2025) response demonstrated rapid crisis management: DAO multisig recovered ~$19M in osETH within 90 minutes, communicated to community within hours. Proven real-world critical response capability. | 9 | 9 | Non-Improvable (optimal) | [P1] Balancer hack response: 90 min recovery, [P1] Active Discord/Telegram |
| O-TL-07 | Are major investors or strategic partners disclosed? | Seed round ($2M, March 2021): Greenfield Capital (lead), gumi Cryptos Capital, Collider Ventures, Lionschain Capital. Strategic round (March 2022): Boldstart Ventures, Blockdaemon Ventures. Operational partners: T-Systems (Deutsche Telekom), Finoa, CryptoManufaktur as node operators. Investors and partners comprehensively disclosed. | 9 | 9 | Non-Improvable (optimal) | [P4] [Crypto Fundraising](https://crypto-fundraising.info/projects/stakewise/), [P1] Operational partners disclosed |
| O-TL-08 | Does the strategy manager manage similar products creating conflict? | N/A -- LST, not managed vault. | N/A | N/A | N/A | - |
| O-TL-09 | Has the strategy manager been involved in products with collateral loss? | N/A -- LST, not managed vault. | N/A | N/A | N/A | - |

**Team & Legal Subtotal (7 of 9 scored):**
- Raw scores: 9+9+9+9+3+9+9 = 57/63
- Adjusted: (57/63) x 67.5 = **61.1/67.5 (90.5%)**

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation on architecture and risks? | docs.stakewise.io covers core concepts, osToken mechanics, vault system, fees, redemption. Updated for V3 and Vaults V2.0. Comprehensive official documentation. | 9 | 9 | Non-Improvable (optimal) | [P1] [Docs](https://docs.stakewise.io), [P1] [osToken docs](https://docs.stakewise.io/docs/ostoken/how-ostoken-works) |
| O-DT-02 | Is it documented how collateral is used and when loss occurs? | Documentation explains overcollateralization, LTV thresholds (90%, 91.5% redemption, 92% liquidation), slashing protection, and loss scenarios. Clear triggers documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [osToken mechanics](https://docs.stakewise.io/docs/ostoken/how-ostoken-works) |
| O-DT-03 | Are all contract addresses documented in one canonical place? | Yes. docs.stakewise.io/contracts/networks/Mainnet lists all 28+ contracts with addresses in a single canonical table. Updated for current deployment. | 9 | 9 | Non-Improvable (optimal) | [P1] [Contracts Mainnet](https://docs.stakewise.io/contracts/networks/Mainnet) |
| O-DT-04 | Are roles, permissions and timelocks documented? | SafeSnap parameters documented. Multisig signers verifiable via Safe API (4-of-7, 7 owners). OsToken owner documented. However, no central role registry with change history. SWIPs serve as partial change log but scattered. | 3 | 9 | **Improvable** | [P0] Safe API: signer addresses verifiable, [P2] SWIPs |
| O-DT-05 | Does the protocol publish proof-of-reserves? | Staked ETH fully visible on Beacon Chain. Validator counts and balances public. osETH backing verifiable via OsTokenVaultController.convertToAssets(). Full on-chain transparency. No liabilities (LST, not lending). | 9 | 9 | Non-Improvable (optimal) | [P0] Beacon Chain, [P0] convertToAssets() |
| O-DT-06 | Are all contracts verified on block explorers? | All core contracts verified on Etherscan with exact match. OsToken, Keeper, OsTokenVaultController, PriceFeed, all factories verified. Compiler v0.8.22. | 9 | 9 | Non-Improvable (optimal) | [P0] Etherscan: all verified |

**Documentation Subtotal:**
- Raw scores: 9+9+9+3+9+9 = 48/54
- Adjusted: (48/54) x 67.5 = **60.0/67.5 (88.9%)**

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | No dedicated safety module or backstop. DAO treasury (~$2.3M) has no binding activation rules for user loss coverage. Overcollateralization (10%) is per-position, not a collective backstop. No insurance fund. However, DAO multisig did recover ~$19M osETH within 90 min during Balancer hack (Nov 2025), demonstrating discretionary crisis response capability. Meets Mid (3): treasury intended for loss coverage but activation remains discretionary. | 3 | 9 | **Improvable** | [P0] Treasury: ~$2.3M, [P1] No safety module, [P1] Balancer recovery |
| O-FR-02 | How large are backstop reserves relative to TVL? | DAO treasury ~$2.3M (osETH ~$1M + SWISE ~$1.3M). osETH total supply ~$400-450M. Ratio: ~0.5%. Below 1% threshold. Large share in SWISE (illiquid). DeFiLlama treasury API returns no data. | 1 | 9 | **Improvable** | [P0] [Treasury](https://etherscan.io/address/0x144a98cb1CdBb23610501fE6108858D9B7D24934), [P3] DeFiLlama: no data |
| O-FR-03 | What is the estimated operational runway? | Protocol generating revenue from 5% treasury fee on ~$450M TVL (~2.5-3% APR staking rewards = ~$0.7M annual revenue to treasury). Total 2025 spending at $1.1M per forum post (SWIP-31). $1M liquid treasury balance reported March 2026. Runway comfortably >24 months. Trending toward profitability. | 9 | 9 | Non-Improvable (optimal) | [P3] [DefiLlama revenue](https://defillama.com/protocol/stakewise): ~$675K annual, [P0] 5% fee on staking rewards, [P3] [SWIP-31 costs breakdown](https://forum.stakewise.io/t/swip-31-issue-development-grant-for-stakewise-labs/1881) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress? | V3 TVL grew from launch to ~$881M. Balancer hack (Nov 2025) impacted LP pools but not protocol TVL directly. No major stress-driven TVL collapse. TVL correlates with ETH price. No buffer depletion. Protocol operational since 2021, navigating multiple crypto-wide downturns without depositor haircuts or emergency dilution. | 9 | 9 | Non-Improvable (optimal) | [P3] [DefiLlama TVL](https://defillama.com/protocol/stakewise) |
| O-FR-05 | Can the protocol remain safe if team disappears? | Core contracts non-upgradeable. Oracle network requires ongoing operation by 11 operators. If team disappears: reward updates stop but osETH redeemable on-chain. Vault withdrawals permissionless. DEX exits available. Moderate dependency for oracle maintenance. Could improve by documenting oracle contingency plans and automated failover. | 3 | 9 | **Improvable** | [P0] Non-upgradeable contracts |

**Financial Resilience Subtotal:**
- Raw scores: 3+1+9+9+3 = 25/45
- Adjusted: (25/45) x 67.5 = **37.5/67.5 (55.6%)**

**Operations Total: 37.5 + 61.1 + 60.0 + 37.5 = 196.1/270 (72.6%)**

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 93 | 99 | 169.1 | 180 | 93.9% |
| | Key Management (7 of 8 Q scored) | 57 | 63 | 162.9 | 180 | 90.5% |
| | **Security Subtotal** | | | **332.0** | **360** | **92.2%** |
| **Strategy** | Protocol Mechanics (7 of 10 Q scored) | 63 | 63 | 45.0 | 45 | 100.0% |
| | Collateral (4 Q) | 36 | 36 | 45.0 | 45 | 100.0% |
| | Infra Counterparty (8 Q) | 66 | 72 | 41.25 | 45 | 91.7% |
| | Protocol Counterparty (4 of 5 Q scored) | 36 | 36 | 45.0 | 45 | 100.0% |
| | Liquidity (9 Q) | 81 | 81 | 45.0 | 45 | 100.0% |
| | Market (5 Q) | 39 | 45 | 39.0 | 45 | 86.7% |
| | **Strategy Subtotal** | | | **260.25** | **270** | **96.4%** |
| **Operations** | Governance (3 of 4 Q scored) | 15 | 27 | 37.5 | 67.5 | 55.6% |
| | Team & Legal (7 of 9 Q scored) | 57 | 63 | 61.1 | 67.5 | 90.5% |
| | Documentation (6 Q) | 48 | 54 | 60.0 | 67.5 | 88.9% |
| | Financial Resilience (5 Q) | 25 | 45 | 37.5 | 67.5 | 55.6% |
| | **Operations Subtotal** | | | **196.1** | **270** | **72.6%** |
| **TOTAL** | | | | **788.4** | **900** | **87.6%** |

---
