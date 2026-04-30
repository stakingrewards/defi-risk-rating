# Lido - EarnUSD Vault Risk Rating

**Rating Date**: 2026-04-29
**Final Grade**: CCC+
**Total Score**: 635.25/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 271.4/360 (75.4%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | **v0.1-gamma criteria change: now requires deployment configuration review.** Mellow Core Vault infrastructure audited by: (1) Sherlock contest (Tier-0, July 2025), (2) Nethermind (Tier-1, September 2025). 2 independent audits with public reports. However, **deployment configuration** (oracle setup, permission parameters, subvault configuration specific to EarnUSD) is NOT explicitly documented as being in audit scope. Prior rating incorrectly cited Veda/BoringVault audits (Spearbit, 0xMacro, etc.) which do NOT apply to this Mellow-based vault. Score Mid: >=2 code audits but deployment configuration not confirmed in audit scope. | 3 | 9 | **Improvable** | [P1] [Mellow Security](https://docs.mellow.finance/security), [P0] [EarnUSD Contract](https://etherscan.io/address/0x4Ce1ac8F43E0E5BD7A346A98aF777bF8fbeA1981) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Nethermind (Tier-1) performed the most recent Core Vault audit (September 2025). Sherlock (Tier-0) performed the competitive audit contest (July 2025). At least one Tier-0 or Tier-1 auditor. | 9 | 9 | Non-Improvable (optimal) | [P1] [Mellow Security](https://docs.mellow.finance/security) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | EarnUSD vault contract (0x4Ce1ac8F43E0E5BD7A346A98aF777bF8fbeA1981) is a TransparentUpgradeableProxy. The implementation (BurnableTokenizedShareManager) has been upgraded once since deployment (53 days ago). Core Vault audits predate deployment. No evidence of post-deployment upgrade requiring new audit. Score Low: no core upgrade in last 12 months requiring audit beyond initial deployment. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Vault Proxy](https://etherscan.io/address/0x4Ce1ac8F43E0E5BD7A346A98aF777bF8fbeA1981) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Sherlock contest identified MEV vulnerability in modifyVaultBalance (Medium severity). No publicly available remediation report confirming resolution. Nethermind report findings not publicly accessible. Remediation status partially unclear. Score Mid: no confirmed unresolved critical/high, but remediation verification incomplete. | 3 | 9 | **Source Missing** | [P1] [Sherlock Contest](https://github.com/sherlock-audit/2025-07-mellow-flexible-vaults), [P1] [Mellow Security](https://docs.mellow.finance/security) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Both the Vault (0x014e6DA8) and ShareManager (0x4Ce1ac8F) are TransparentUpgradeableProxy contracts. TimelockController at 0xdA6Da82D controls upgrades. Timelock delay not publicly documented but OpenZeppelin TimelockController deployed. Admin multisig (5/8) required. Score Low: upgradeable via governance/multisig with timelock and narrow upgrade roles. | 9 | 9 | Non-Improvable (optimal) | [P0] [TimelockController](https://etherscan.io/address/0xdA6Da82DFF8cD29D828e4775Cc003f504A968845), [P1] [Mellow Deployments](https://docs.mellow.finance/core-vaults/core-deployments) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploits affecting EarnUSD user funds. EarnUSD was explicitly confirmed unaffected by the April 2026 rsETH/KelpDAO exploit. EarnETH (separate vault, same Lido brand) was affected but EarnUSD had zero rsETH exposure. | 9 | 9 | Non-Improvable (optimal) | [P4] [Blockonomi](https://blockonomi.com/lido-reports-9-rseth-exposure-after-kelpdao-exploit) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No. Lido DAO backed by a16z ($70M), Paradigm ($73M), Dragonfly ($25M). Core contributors publicly identified. Mellow Protocol is a separate BVI-registered company. | 9 | 9 | Non-Improvable (optimal) | [P4] [CoinDesk -- a16z funding](https://www.coindesk.com/business/2022/03/03/a16z-investing-70m-into-ethereum-staking-provider-lido-finance) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions detected. TimelockController deployed 53 days ago. Only 7 Schedule transactions on day of deployment (initial configuration), 2 RenounceRole transactions. No subsequent modifications. Dual Governance dynamic timelocks (3-day min to 45-day max) unchanged. | 9 | 9 | Non-Improvable (optimal) | [P0] [TimelockController Txns](https://etherscan.io/address/0xdA6Da82DFF8cD29D828e4775Cc003f504A968845) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Lido: $2M max on Immunefi. Lido ran an Immunefi audit competition for Mellow Vault (August-September 2024, $100K pool) covering 12 contracts. However, the Immunefi competition was time-limited (finished) and covered the older Mellow LRT contracts, not Core Vaults. Lido's main $2M bounty covers Lido core contracts. Mellow does not have its own active bounty listed on Immunefi. Score Low: Lido's active $2M bounty exceeds $100K threshold; Mellow vault code partially covered through the completed competition. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido Immunefi](https://immunefi.com/bug-bounty/lido/), [P1] [Mellow Vault Immunefi Competition](https://immunefi.com/audit-competition/boost-lido/scope/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Mellow uses Hypernative for monitoring. Hypernative sends notifications during critical operations including changes in multisig settings. However, specific configuration details for EarnUSD (monitored invariants, alert thresholds, response SLAs) are not publicly disclosed. Score Mid: monitoring provider engaged but configuration details not publicly verifiable. | 3 | 9 | **Source Missing** | [P1] [Mellow Core Vaults launch announcement](https://blockchainmagazine.com/press-release/mellow-launches-core-vaults-modular-infrastructure-for-institutional-onchain-strategies/) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Mellow Core Vault has ShareManager pause flags (hasMintPause, hasBurnPause, hasTransferPause) controlled via SET_FLAGS_ROLE. Oracle deviation thresholds (maxAbsoluteDeviation, suspiciousAbsoluteDeviation) can reject suspicious price reports. However, no documented automatic circuit breakers triggered by Hypernative alerts. Pause appears to require manual multisig intervention. Curator rebalancing does not have documented automatic kill-switches. Score Mid: manual triggers documented (pause flags), but automatic triggers for abnormal conditions unclear. | 3 | 9 | **Source Missing** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture), [P0] [Oracle Contract](https://etherscan.io/address/0x0000000F0d3d1c31b72368366a4049c05e291d58#code) |

**Smart Contract Security Subtotal:**
- 11 questions: 7x9 + 4x3 = 63 + 12 = 75/99
- Adjusted: (75/99) x 180 = **136.4/180 (75.8%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Admin Multisig (5/8) at 0x0Dd73341d6158a72b4D224541f1094188f57076E. 8 named signers: tamtamchik, TheDZhon, George, psirex, DeFiYaco, Marin, Armin, skelneko. Controls role management, TimelockController. Curator Safe (0x9745F161) manages daily strategy operations. Changes documented in governance proposal. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Admin Multisig](https://etherscan.io/address/0x0Dd73341d6158a72b4D224541f1094188f57076E), [P2] [Governance Proposal](https://research.lido.fi/t/lido-earn-competing-on-trust-5m-treasury-allocation/11228) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Admin multisig 5/8 threshold. Curator multisig at 0x9745F161 is a Safe contract (confirmed on Etherscan). TimelockController adds delay. No single key can move user funds. Threshold >=3, signers >=5. | 9 | 9 | Non-Improvable (optimal) | [P0] [Admin Safe](https://etherscan.io/address/0x0Dd73341d6158a72b4D224541f1094188f57076E), [P0] [Curator Safe](https://etherscan.io/address/0x9745F161b0160a99924845BeFCE1d7b9Daee6899) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Admin: 5/8 with 8 named signers (distinct individuals based on different ENS/forum handles). Curator: Safe at 0x9745F161 -- threshold and signer count not publicly displayed on Etherscan page. Governance proposal lists Curator as 3/5 for the original Curator Safe (0xe5abcc), but EarnUSD uses a DIFFERENT Curator Safe (0x9745F161). Signer details for the actual EarnUSD Curator are undisclosed. Score Mid: Admin exceeds Low criteria, but actual EarnUSD Curator signer identities and threshold unverifiable. | 3 | 9 | **Source Missing** | [P0] [EarnUSD Curator Safe](https://etherscan.io/address/0x9745F161b0160a99924845BeFCE1d7b9Daee6899), [P2] [Governance Proposal](https://research.lido.fi/t/lido-earn-competing-on-trust-5m-treasury-allocation/11228) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Mellow ShareManager has per-account flags: canDeposit, canTransfer, isBlacklisted. Global pause via hasMintPause, hasBurnPause, hasTransferPause controlled by SET_FLAGS_ROLE. GateSeal (3/6 multisig) for Lido-level emergency pause. However, SET_ACCOUNT_INFO_ROLE can set isBlacklisted on individual addresses -- this allows address-level withdrawal censorship. The holder of this role is not publicly documented. Score Mid: pause exists with broad scope including address-level blocking capability via isBlacklisted, requires multisig, but scope of address-level censorship not fully documented. | 3 | 9 | **Improvable** | [P0] [ShareManager Implementation](https://etherscan.io/address/0x000000000c79d2b5cd58ae545afc83030233d7b6#code), [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. All user assets in Mellow Core Vault contract (0x014e6DA8) on Ethereum, deployed into Subvaults. Architecture explicitly non-custodial. 100% non-custodial. | 9 | 9 | Non-Improvable (optimal) | [P0] [Vault Contract](https://etherscan.io/address/0x014e6DA8F283C4aF65B2AA0f201438680A004452), [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | DAO treasury in Aragon Agent (0x3e40D73E...). Earn vault holds user assets separately in Mellow Vault contract. $2M DAO first-loss allocation co-deposited as vault shares (by design, disclosed). Meta Treasury (0xcCf2daba) handles fees separately. Clear on-chain segregation. | 9 | 9 | Non-Improvable (optimal) | [P0] [Aragon Agent](https://etherscan.io/address/0x3e40D73EB977Dc6a537aF587D48316feE66E9C8c), [P2] [Governance Proposal](https://research.lido.fi/t/lido-earn-competing-on-trust-5m-treasury-allocation/11228) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | Mellow Core Vault uses a Verifier module with four verification methods including ONCHAIN_COMPACT and MERKLE_COMPACT for call authorization. Each Subvault has a dedicated Verifier contract (Verifier 0: 0xB65A8E09). Known venues: Aave, Morpho. Changes require Admin multisig with TimelockController. On-chain enforced whitelist via Verifier module. | 9 | 9 | Non-Improvable (optimal) | [P0] [Verifier Contract](https://etherscan.io/address/0xB65A8E0937c77a76C3f4F86A1110f81A299CB481), [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Lido DAO demonstrated incident response in May 2025 (Chorus One oracle key compromise) and April 2026 (EarnETH pause within hours of rsETH exploit). GateSeal and emergency committees exist. The EarnETH response to the rsETH exploit demonstrates capability. But no specific documented and tested playbook for Earn vault Admin/Curator key compromise published. Score Mid: informal capability demonstrated but formal Earn-specific playbook absent. | 3 | 9 | **Improvable** | [P4] [CoinDesk -- oracle key incident](https://www.coindesk.com/tech/2025/05/12/ethereum-staking-giant-lido-loses-just-14-eth-in-hacking-attempt), [P4] [EarnETH pause](https://blockonomi.com/lido-reports-9-rseth-exposure-after-kelpdao-exploit) |

**Key Management Subtotal:**
- 8 questions: 5x9 + 3x3 = 45 + 9 = 54/72
- Adjusted: (54/72) x 180 = **135.0/180 (75.0%)**

**CHANGE LOG vs prior rating:**
- S-KM-03: 9 -> 3. Prior rating used Curator Safe 0xe5abcc (3/5, named signers). EarnUSD actually uses DIFFERENT Curator Safe 0x9745F161 (Mellow deployments page). Signer details for this address are not publicly documented.
- S-KM-04: 9 -> 3. Prior rating did not identify Mellow's isBlacklisted flag in ShareManager contract, which allows address-level withdrawal censorship. The role holder for SET_ACCOUNT_INFO_ROLE is undocumented.
- S-SC-01: 9 -> 3. Prior rating cited Veda/BoringVault audits that do not apply. Mellow Core Vault has 2 audits (Sherlock, Nethermind) but deployment configuration not confirmed in scope.
- S-SC-04: 9 -> 3. Prior rating assumed no unresolved findings across Veda audits. Mellow Core Vault Sherlock contest identified MEV vulnerability; remediation status not confirmed.

**Security Total: 136.4 + 135.0 = 271.4/360 (75.4%)**

---

### STRATEGY (30% Weight) -- Score: 174.6/270 (64.7%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | EarnUSD allocates USDC/USDT to conservative lending on Aave/Morpho (borrower interest -- organic). Blog mentions RWA integrations and structured positions. Yield aligns with "USD-denominated reward strategies" mandate. Fee structure: 10% performance fee, 1% platform fee (visible on deposit page). However, percent breakdown of yield sources not published. Score Mid: main sources listed but percent breakdown incomplete. | 3 | 9 | **Improvable** | [P1] [Lido Earn Blog](https://blog.lido.fi/lido-earn-expands-with-earneth-and-earnusd/), [P0] [Lido Earn Deposit Page](https://stake.lido.fi/earn/usd/deposit) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Stablecoin lending on Tier-0 protocols: negative yield limited to rare tail shocks (smart contract exploit in Aave/Morpho, stablecoin depeg, oracle failure). $2M first-loss buffer provides additional protection. Conservative lending with major stablecoins. | 9 | 9 | Non-Improvable (optimal) | [P2] [Governance Proposal](https://research.lido.fi/t/lido-earn-competing-on-trust-5m-treasury-allocation/11228) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage or rehypothecation. USDC/USDT are lent as supply-side deposits. Governance proposal describes "conservative lending positions." Effective leverage 1.0x. | 9 | 9 | Non-Improvable (optimal) | [P2] [Governance Proposal](https://research.lido.fi/t/lido-earn-competing-on-trust-5m-treasury-allocation/11228) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Supply-side stablecoin lending vault. No LTV or liquidation threshold for the vault itself. | N/A | N/A | N/A | - |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | EarnUSD launched March 12, 2026. Strategy type (passive USDC/USDT lending on Aave/Morpho) well-established with no permanent-loss events in comparable variants over last 24 months. The EarnETH vault (different strategy -- leveraged staking/restaking) experienced 400-600 ETH in borrow-rate losses from the rsETH incident, but EarnETH's strategy (leveraged restaking) is NOT comparable to EarnUSD's strategy (passive stablecoin lending). | 9 | 9 | Non-Improvable (optimal) | [P2] [Loss Coverage Proposal](https://research.lido.fi/t/authorise-loss-coverage-below-the-1-threshold-for-the-kelp-incident/11527) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Governance proposal: >=1% mark-to-market loss triggers halt, first-loss shares burned, 7-day incident reports, quarterly reporting. Mellow Core Vault architecture enforces asset whitelists, per-strategy permissions, oracle checks. But comprehensive quantitative limits for concentration, drawdown, and counterparty exposure not published. Score Mid: partial framework with some limits but not comprehensive. | 3 | 9 | **Improvable** | [P2] [Governance Proposal](https://research.lido.fi/t/lido-earn-competing-on-trust-5m-treasury-allocation/11228) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Stablecoin lending yields on Aave/Morpho are organic (borrower interest). No incentive-driven yield or emissions for EarnUSD. Yield is fundamentally organic. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido Feb 2026 Update](https://blog.lido.fi/recap-lido-tokenholder-update-february-2026/) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | USDC/USDT most liquid stablecoins on Ethereum. Withdrawal from Aave/Morpho generally instant for stablecoin markets. Under conservative assumptions, most of position can unwind within stated horizon with low slippage. | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama -- USDC/USDT deep liquidity |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Strategy relies on USDC/USDT maintaining USD pegs -- both most established stablecoins. Lending yield from borrower interest, not peg arbitrage. Peg reliance limited. | 9 | 9 | Non-Improvable (optimal) | [P3] Historical USDC/USDT peg data |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Mellow Core Vault Curator can push/pull assets between Subvaults and execute verified calls to external protocols. These are human-initiated multisig transactions (Curator Safe at 0x9745F161). No evidence of permissionless functions that can increase exposure. The Verifier module restricts what calls can be made. However, whether automatic kill-switches for abnormal conditions are documented is unclear. Score Mid: caps exist via Verifier whitelist, human-initiated, but no documented automatic kill-switch for abnormal conditions. | 3 | 9 | **Source Missing** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |

**Protocol Mechanics Subtotal:**
- 9 scored (1 N/A): 6x9 + 3x3 = 54 + 9 = 63/81
- Adjusted: (63/81) x 45 = **35.0/45 (77.8%)**

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | USDC (Circle, $40B+ mcap, regulated, reserve-backed) and USDT (Tether, $140B+ mcap, reserve-backed). Both established large-cap stablecoins. Top-tier stablecoin assets only. | 9 | 9 | Non-Improvable (optimal) | [P3] CoinGecko -- USDC/USDT market data |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | USDC: March 2023 depeg to ~$0.87 during SVB collapse (>10% depeg), recovered within 3 days. Over 24 months ago, mitigated by Circle diversifying bank exposure. USDT: brief 1-2% deviations during stress, recovers within hours. Score Mid: USDC showed 2-10%+ depeg with full recovery, historical event now mitigated. | 3 | 3 | Non-Improvable | [P3] Historical USDC/USDT price data |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- USDC/USDT stablecoins, not staking-based collateral. | N/A | N/A | N/A | - |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | **v0.1-gamma criteria change: now includes bridge security quality assessment when bridged assets exceed 10% TVL.** USDC and USDT are natively issued on Ethereum (not bridged). 0% bridged or wrapped assets. No change to score. | 9 | 9 | Non-Improvable (optimal) | [P0] Native ERC-20 tokens on Ethereum |

**Collateral Subtotal:**
- 3 scored (1 N/A): 2x9 + 1x3 = 18 + 3 = 21/27
- Adjusted: (21/27) x 45 = **35.0/45 (77.8%)**

---

#### Infra Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum (Tier-0). No bridges. Mellow Oracle contract uses off-chain consensus group for price submission (proprietary, not Chainlink -- discussed in ST-IC-02). No CEX dependency. Chain dependency is Tier-0. However, Mellow oracle is proprietary (not tiered in SR oracle list). Score Mid: chain is Tier-0 but oracle is proprietary/untiered. | 3 | 9 | **Improvable** | [P0] [Oracle Contract](https://etherscan.io/address/0x827044735c9708a2cf850e7Ea37EBa43bc786028), [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | **v0.1-gamma criteria change: MANDATORY hardcoded oracle check + oracle-focused only.** Mellow Oracle is NOT hardcoded -- it accepts dynamic price submissions from authorized roles (SUBMIT_REPORTS_ROLE). Prices can be updated and corrected. Oracle has deviation thresholds (maxAbsoluteDeviation, suspiciousAbsoluteDeviation, maxRelativeDeviationD18) and timeout mechanisms. Suspicious reports require Admin approval (ACCEPT_REPORT_ROLE). However, this is a single proprietary oracle system with no independent fallback oracle. Not Tier-0/1. Score Mid: single primary provider (Mellow proprietary oracle) with partial fallback (Admin can accept suspicious reports), but not Tier-0/1 per SR oracle list. | 3 | 9 | **Improvable** | [P0] [Oracle Implementation](https://etherscan.io/address/0x0000000F0d3d1c31b72368366a4049c05e291d58#code), [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Mellow Oracle uses off-chain consensus group for price submissions. OracleSubmitter (0xB105DaEe) and OracleUpdater (0x93a79764) submit reports off-chain. This constitutes critical off-chain infrastructure. Mellow's security certifications (SOC 2, ISO27001) are not disclosed. Score High: critical off-chain oracle provider with no disclosed certifications. | 1 | 9 | **Improvable** | [P0] [OracleSubmitter](https://etherscan.io/address/0xB105DaEeFEb1390ce49172c99E3e12C607367156), [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | EarnUSD launched March 12, 2026 (~7 weeks). No chain incidents during this period. Ethereum has had no significant halts in 12+ months. Per v0.1-gamma guidance: deployed <6 months with no chain-level incidents, score Mid. The rsETH crisis (April 18-20) is NOT a chain incident -- it was a protocol-level exploit that did not affect EarnUSD or Ethereum infrastructure. | 3 | 9 | Non-Improvable | [P3] Ethereum chain history, [P4] [EarnUSD unaffected](https://blockonomi.com/lido-reports-9-rseth-exposure-after-kelpdao-exploit) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has not experienced any halt >30 minutes in last 12 months. Tier-0 chain. | 9 | 9 | Non-Improvable (optimal) | [P3] Ethereum consensus history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- USDC/USDT stablecoins, no staking collateral. | N/A | N/A | N/A | - |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- USDC/USDT stablecoins, no validator dependency. | N/A | N/A | N/A | - |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | Ethereum is sole chain dependency (Tier-0). Mellow vault withdrawals are on-chain via RedeemQueue. If Curator stops, assets remain in Subvaults/Vault. However, the off-chain Oracle consensus group is needed for processing redemptions (oracle reports required after redeemInterval). If the Oracle goes down, new redemptions cannot be priced. This is a single-point dependency that could delay withdrawals. Score Mid: Oracle failure could temporarily delay withdrawals, but funds remain safe in vault. | 3 | 9 | **Improvable** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| ST-IC-09 | How robust is the cross-chain messaging or bridge verification setup? | N/A -- EarnUSD operates exclusively on Ethereum with no cross-chain messaging or bridge dependency. | N/A | N/A | N/A | - |
| ST-IC-10 | Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting? | N/A -- No cross-chain bridge/minting exists. | N/A | N/A | N/A | - |
| ST-IC-11 | Is the off-chain verification infrastructure resilient to data-source manipulation? | N/A -- EarnUSD has no off-chain verifiers making cross-chain attestations. The Mellow Oracle consensus group submits share prices (not cross-chain attestations), and is assessed in ST-IC-02/ST-IC-03. | N/A | N/A | N/A | - |

**Infra Counterparty Subtotal:**
- 6 scored (5 N/A): 1x9 + 4x3 + 1x1 = 9 + 12 + 1 = 22/54
- Adjusted: (22/54) x 45 = **18.3/45 (40.7%)**

**CHANGE LOG vs prior rating:**
- ST-IC-01: 9 -> 3. Prior rating cited Chainlink Price Feeds (Tier-0). EarnUSD actually uses Mellow's proprietary Oracle contract, not Chainlink. The Chainlink feeds are used in the broader Lido ecosystem for stETH pricing, not for EarnUSD share pricing.
- ST-IC-02: 9 -> 3. Prior rating described redundant Chainlink feeds. EarnUSD uses Mellow's single proprietary oracle with no independent fallback. The oracle is not hardcoded (prices can be corrected) so it avoids High (1), but it's a single system without Tier-0/1 fallback.
- ST-IC-03: 9 -> 1. Prior rating stated "no critical off-chain providers." The Mellow Oracle uses off-chain consensus group for price submissions -- this IS critical off-chain infrastructure with no disclosed certifications.
- ST-IC-08: 9 -> 3. Prior rating stated no single-point-of-failure. The Mellow Oracle consensus group is required for processing redemptions; its failure would delay withdrawals.
- ST-IC-09/10/11: NEW questions, all N/A for Ethereum-only vault.

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Aave (Tier-0) and Morpho (Tier-0) disclosed. Blog mentions "RWA integrations and structured positions" without naming specific venues. Score Mid: most venues disclosed but some described only in general terms. | 3 | 9 | **Improvable** | [P1] [Lido Earn Blog](https://blog.lido.fi/lido-earn-expands-with-earneth-and-earnusd/) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Deposit page: 10% performance fee, 1% platform fee. Meta Treasury (0xcCf2daba) handles fee collection/distribution. First-loss mechanism aligns DAO with depositors. However, full fee terms, distribution between Lido DAO and Mellow, and any Mellow revenue-share not detailed. Score Mid: fee percentages visible but terms and distribution only partially disclosed. | 3 | 9 | **Source Missing** | [P0] [Lido Earn Deposit Page](https://stake.lido.fi/earn/usd/deposit), [P2] [Governance Proposal](https://research.lido.fi/t/lido-earn-competing-on-trust-5m-treasury-allocation/11228) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Mellow Subvault architecture with per-Subvault deposit limits (Vault Limit and Subvault Limit parameters). Verifier module restricts which calls are allowed. However, specific per-counterparty concentration caps (e.g., max % to Aave vs Morpho) are not publicly documented. Score Mid: Subvault limits exist but concentration caps per counterparty not documented. | 3 | 9 | **Source Missing** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | USDC/USDT lending on Aave/Morpho: typically instant withdrawal (subject to utilization). Both have well-documented exit paths. Mellow RedeemQueue processes withdrawals with stated "up to 72 hours" timeline. | 9 | 9 | Non-Improvable (optimal) | [P0] [Lido Earn Deposit Page](https://stake.lido.fi/earn/usd/deposit) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Mellow (infrastructure provider), Curator Safe (0x9745F161, strategy manager), Aave/Morpho (deployment venues) all disclosed. No third-party custodians. All key third parties disclosed with roles. | 9 | 9 | Non-Improvable (optimal) | [P0] [Mellow Deployments](https://docs.mellow.finance/core-vaults/core-deployments), [P2] [Governance Proposal](https://research.lido.fi/t/lido-earn-competing-on-trust-5m-treasury-allocation/11228) |

**Protocol Counterparty Subtotal:**
- 5 questions: 2x9 + 3x3 = 18 + 9 = 27/45
- Adjusted: (27/45) x 45 = **27.0/45 (60.0%)**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Mellow RedeemQueue: shares burned immediately upon request; Curator pulls liquidity and processes after redeemInterval; users claim assets. ShareManager hasTransferPause/hasBurnPause for protocol-wide pause. isBlacklisted flag exists for address-level blocking (SET_ACCOUNT_INFO_ROLE). Stated "up to 72 hours." Score Mid: on-chain withdrawal path exists but address-level discretion via isBlacklisted, controlled by multisig, with limited documentation of constraints. | 3 | 9 | **Improvable** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture), [P0] [ShareManager Code](https://etherscan.io/address/0x000000000c79d2b5cd58ae545afc83030233d7b6#code) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | USDC/USDT are the most liquid assets in DeFi ($10B+ daily volume each on Ethereum). Underlying Aave/Morpho stablecoin markets typically have low utilization. Credible path for near-total exits within 72-hour window. | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama -- USDC/USDT liquidity |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | Launched March 12, 2026 -- ~7 weeks of history. No issues reported. EarnUSD continued operating normally through the rsETH crisis (April 18-29). Still insufficient time-series data to confirm 95%+ completion rate over 6-12 months. Score Mid: missing time-series data, but positive signal from continued operation during ecosystem stress. | 3 | 9 | Non-Improvable | [P4] [Blockonomi -- EarnUSD unaffected](https://blockonomi.com/lido-reports-9-rseth-exposure-after-kelpdao-exploit) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Mellow RedeemQueue has redeemInterval parameter controlling minimum time before processing. Withdrawal timeline stated as "up to 72 hours." Specific redeemInterval value and any caps on redemption amounts not publicly documented. Score Mid: caps likely exist but specifics not documented. | 3 | 9 | **Source Missing** | [P0] [Lido Earn Deposit Page](https://stake.lido.fi/earn/usd/deposit) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | ~7 weeks history. EarnUSD continued operating normally during the April 18-29 rsETH crisis period (a significant ecosystem stress event). While EarnUSD was not directly stressed (no rsETH exposure), its continued normal operation during a period where sibling vault EarnETH was paused is a partial positive signal. However, this is not a direct stress test of EarnUSD's own exit liquidity. Score Mid: untested for direct stress, partial positive signal from continued operation during ecosystem stress. | 3 | 3 | Non-Improvable | [P4] [EarnUSD unaffected during rsETH crisis](https://blockonomi.com/lido-reports-9-rseth-exposure-after-kelpdao-exploit) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No unstaking, vesting, or bridge exits. USDC/USDT lending on Aave/Morpho can be withdrawn instantly (subject to utilization). Less than 10% of assets locked longer than stated 72-hour withdrawal terms. | 9 | 9 | Non-Improvable (optimal) | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | In-protocol redemption via RedeemQueue is primary exit. Secondary market optional. USDC/USDT extremely liquid. | 9 | 9 | Non-Improvable (optimal) | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | USDC/USDT: $10B+ daily volume each, deepest-liquidity DeFi assets. Can absorb far >10% of protocol TVL with low impact. | 9 | 9 | Non-Improvable (optimal) | [P3] CoinGecko USDC/USDT volume |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Stablecoin lending vault: bank-run risk limited to Aave/Morpho utilization spikes. Both have steep interest rate curves at high utilization, incentivizing repayment. $2M DAO first-loss buffer. Vault is ~7 weeks old and has NOT survived a direct bank-run-like event. Per framework: untested protocols score Mid (3) max on resilience questions. | 3 | 9 | Non-Improvable | [P1] Aave/Morpho interest rate models |

**Liquidity Subtotal:**
- 9 questions: 4x9 + 5x3 = 36 + 15 = 51/81
- Adjusted: (51/81) x 45 = **28.3/45 (62.9%)**

**CHANGE LOG vs prior rating:**
- ST-L-01: 9 -> 3. Prior rating did not identify Mellow's isBlacklisted flag allowing address-level blocking.

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | earnUSD token is ~7 weeks old (launched March 12, 2026). No major stress event has directly impacted the earnUSD token. The rsETH crisis (April 18-29) did NOT affect EarnUSD (zero rsETH exposure). earnUSD maintained normal operations throughout this period, but this is not equivalent to surviving a direct stress test of the token's peg. Score High: "real stress history too short/unclear" -- no direct stress test of earnUSD peg. | 1 | 9 | Non-Improvable | Vault launched ~7 weeks ago; rsETH crisis did not directly stress earnUSD |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Stablecoin lending strategy, no directional exposure. USDC/USDT pegged to USD. No leverage. Low-beta, no forced liquidation risk from market moves. | 9 | 9 | Non-Improvable (optimal) | Strategy description -- stablecoin lending only |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Underlying Aave/Morpho have well-tested interest rate curves (steep at high utilization). No reflexive incentives. No prolonged >=95% utilization in stablecoin markets. | 9 | 9 | Non-Improvable (optimal) | [P3] Aave/Morpho utilization data |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | No published stress testing for EarnUSD. Governance proposal mentions risk controls (1% loss trigger) but no formal stress testing results. Score Mid: underlying protocols tested by proxy but no vault-specific testing. | 3 | 9 | **Improvable** | [P2] [Governance Proposal](https://research.lido.fi/t/lido-earn-competing-on-trust-5m-treasury-allocation/11228) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | No leverage or borrowing. Supply-side stablecoin lending only. No liquidation risk for vault. | 9 | 9 | Non-Improvable (optimal) | Strategy description |

**Market Subtotal:**
- 5 questions: 3x9 + 1x3 + 1x1 = 27 + 3 + 1 = 31/45
- Adjusted: (31/45) x 45 = **31.0/45 (68.9%)**

**Strategy Total: 35.0 + 35.0 + 18.3 + 27.0 + 28.3 + 31.0 = 174.6/270 (64.7%)**

---

### OPERATIONS (30% Weight) -- Score: 189.25/270 (70.1%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Lido DAO: on-chain tokenholder governance via Aragon + Dual Governance (live July 2025). LDO holders vote with 5% minimum participation. Easy Track for routine ops (72h auto-pass). Dynamic timelock (3-day min, up to 45 days). No single entity can unilaterally change core fund-custody logic. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido Governance](https://lido.fi/governance), [P1] [Dual Governance GitHub](https://github.com/lidofinance/dual-governance) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | Top 5 wallets hold ~50% of LDO voting power (a16z, Paradigm, Dragonfly have significant positions). Top 10 likely control >33% but <=66%. Dual Governance provides stETH holder counterbalance. Score Mid: moderate capture risk. | 3 | 3 | Non-Improvable | [P3] LDO token distribution |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Dual Governance: dynamic timelocks (3-day min to 45-day max). Emergency Protected Timelock at 0xCE0425301C85c5Ea2A0873A2dEe44d78E02D2316. GateSeal (3/6). stETH rage quit at 10% threshold. Mellow TimelockController (0xdA6Da82D) for vault-specific changes. All major upgrades subject to >=24h timelock with bounded veto powers. | 9 | 9 | Non-Improvable (optimal) | [P0] [Emergency Timelock on Etherscan](https://etherscan.io/address/0xCE0425301C85c5Ea2A0873A2dEe44d78E02D2316), [P0] [Mellow Timelock](https://etherscan.io/address/0xdA6Da82DFF8cD29D828e4775Cc003f504A968845) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Curator role can be reassigned through Admin multisig (5/8) with TimelockController. Mellow architecture allows Curator replacement via role management. User withdrawals via RedeemQueue remain functional -- Curator stopping freezes rebalancing but pending redemptions can still be claimed. | 9 | 9 | Non-Improvable (optimal) | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |

**Governance Subtotal:**
- 4 questions: 3x9 + 1x3 = 27 + 3 = 30/36
- Adjusted: (30/36) x 67.5 = **56.25/67.5 (83.3%)**

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Lido Labs Foundation (Cayman Islands). Core contributors with public GitHub profiles. Mellow Protocol (BVI): separate entity, team from "Yandex, McKinsey, and VC funds." Both entities identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido GitHub](https://github.com/lidofinance), [P4] [SEC filing](https://www.sec.gov/files/ctf-input-lido-labs-foundation-3-24-25.pdf), [P4] [CryptoJobsList -- Mellow](https://cryptojobslist.com/companies/mellow-protocol) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Lido: large contributor base (100+ GitHub contributors). Multiple committees. Mellow Protocol: separately funded team ($2.75M raised). Two independent teams maintaining the system. No key-person dependency for Lido; Mellow team size less transparent. Score Low: multiple teams, no key-person dependency. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido Committees](https://docs.lido.fi/multisigs/committees/) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Lido Labs Foundation, Grand Cayman KY1-1106, Cayman Islands. Mellow Protocol, Tortola, British Virgin Islands. Both entities clearly named with jurisdictions disclosed. | 9 | 9 | Non-Improvable (optimal) | [P4] [SEC filing](https://www.sec.gov/files/ctf-input-lido-labs-foundation-3-24-25.pdf), [P1] [Mellow Terms of Service](https://mellow.finance/Mellow-Terms-of-Service.pdf) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | Samuels v. Lido DAO: private civil lawsuit in N.D. California. Court ruled DAO may be general partnership (Nov 2024); case ongoing vs Paradigm, a16z, Dragonfly. Securities classification dispute, not operational enforcement. No known regulatory actions against Mellow. Score Mid: past inquiry ongoing but not major government enforcement. | 3 | 3 | Non-Improvable | [P4] [FindLaw -- Samuels v. Lido DAO](https://caselaw.findlaw.com/court/us-dis-crt-n-d-cal/116694517.html) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Demonstrated incident response in April 2026: EarnETH was paused within hours of the rsETH exploit detection, leverage reduced, wETH debt cut. GateSeal committee (3/6), Dual Governance Emergency/Activation Committees with defined quorums. However, Earn-specific runbooks (including procedures to halt Curator rebalancing in EarnUSD) not published. Mellow's Hypernative integration sends notifications during critical operations. Score Mid: informal on-call exists, demonstrated capability, but formal Earn-specific runbooks absent. | 3 | 9 | **Improvable** | [P4] [Blockonomi -- EarnETH response](https://blockonomi.com/lido-reports-9-rseth-exposure-after-kelpdao-exploit) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Active support channels (help.lido.fi), governance forum (research.lido.fi), social media. April 2026 rsETH incident communicated promptly with public updates. Critical issues acknowledged within 24 hours. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido Help](https://help.lido.fi), [P2] [Governance Forum](https://research.lido.fi) |
| O-TL-07 | Are major investors or strategic partners disclosed? | a16z ($70M), Paradigm ($73M), Dragonfly ($25M) disclosed for Lido. Mellow raised $2.75M (investors not detailed). Score Low: Lido investors fully disclosed; Mellow's smaller raise less detailed but no evidence of opaque control. | 9 | 9 | Non-Improvable (optimal) | [P4] [CoinDesk -- a16z funding](https://www.coindesk.com/business/2022/03/03/a16z-investing-70m-into-ethereum-staking-provider-lido-finance) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | **Critical change since prior rating.** The Curator (Mellow, Safe 0x9745F161) manages both EarnETH and EarnUSD. EarnETH has been paused since April 20 due to rsETH exposure, with 400-600 ETH in borrow-rate losses confirmed. The same entity managing a vault with confirmed losses creates a potential conflict of interest: (1) incentive to take on risk to recover losses elsewhere, (2) attention divided between crisis management on EarnETH and operations on EarnUSD. However, EarnUSD continued normal operations throughout, and the loss coverage proposal shows transparent governance response. Score Mid: other mandates exist with partial disclosure, EarnETH crisis creates potential conflict, but transparent governance. | 3 | 9 | **Improvable** | [P2] [Loss Coverage Proposal](https://research.lido.fi/t/authorise-loss-coverage-below-the-1-threshold-for-the-kelp-incident/11527), [P4] [EarnETH paused](https://blockonomi.com/lido-reports-9-rseth-exposure-after-kelpdao-exploit) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | **Critical change since prior rating.** The Curator managing EarnUSD also manages EarnETH, which experienced 400-600 ETH in borrow-rate losses from the rsETH incident (April 2026). The DAO is activating first-loss coverage. This is one historical loss incident with limited impact (borrow-rate losses, not direct exploit of Curator's strategy), compensation is being provided (first-loss fund), and process improvements are being implemented (loss coverage proposal). Score Mid: one historical loss incident with limited impact, being compensated, process improvements underway. | 3 | 3 | Non-Improvable | [P2] [Loss Coverage Proposal](https://research.lido.fi/t/authorise-loss-coverage-below-the-1-threshold-for-the-kelp-incident/11527) |

**Team & Legal Subtotal:**
- 9 questions: 5x9 + 4x3 = 45 + 12 = 57/81
- Adjusted: (57/81) x 67.5 = **47.5/67.5 (70.4%)**

**CHANGE LOG vs prior rating:**
- O-TL-08: 9 -> 3. The Curator now has confirmed losses on a sibling vault (EarnETH 400-600 ETH).
- O-TL-09: 9 -> 3. Same -- Curator linked to EarnETH losses.

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Lido has extensive docs (docs.lido.fi) covering core protocol, governance, PRD. Mellow has Core Vault architecture docs (docs.mellow.finance). But EarnUSD-specific documentation limited to blog post, governance proposal, and generic Mellow docs -- no dedicated Lido EarnUSD technical docs page. Score Mid: protocol-level docs exist but EarnUSD-specific incomplete. | 3 | 9 | **Improvable** | [P1] [Lido Docs](https://docs.lido.fi), [P1] [Mellow Docs](https://docs.mellow.finance) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Lido PRD: comprehensive risk disclosure. Governance proposal: 1% loss trigger, first-loss mechanism. Blog: conservative lending + selective exposure. Mellow docs: architecture and flow of funds. End-to-end collateral flow and loss scenarios documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido PRD](https://docs.lido.fi/prd/), [P2] [Governance Proposal](https://research.lido.fi/t/lido-earn-competing-on-trust-5m-treasury-allocation/11228) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | **Significant improvement since prior rating.** Vault contract now visible on stake.lido.fi/earn/usd/deposit (0x4Ce1ac8F43E0E5BD7A346A98aF777bF8fbeA1981). Mellow Core Deployments page lists all EarnUSD addresses (Vault, Oracle, ShareManager, FeeManager, RiskManager, Timelock, DepositQueues, RedeemQueue, Subvault, Verifier). Admin multisig from governance proposal. Score Mid: addresses documented but spread across multiple sources (Lido product page, Mellow docs, governance proposal) rather than one canonical place. | 3 | 9 | **Improvable** | [P0] [Lido Earn Page](https://stake.lido.fi/earn/usd/deposit), [P1] [Mellow Deployments](https://docs.mellow.finance/core-vaults/core-deployments) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Governance proposal documents Admin (5/8), Curator roles and powers. Mellow Architecture docs describe role types (Curator, Admin, Oracle roles). But Earn-specific roles not in central registry, specific role assignments (who holds SET_FLAGS_ROLE, ACCEPT_REPORT_ROLE, etc.) not documented. Score Mid: exists but scattered and incomplete. | 3 | 9 | **Improvable** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture), [P2] [Governance Proposal](https://research.lido.fi/t/lido-earn-competing-on-trust-5m-treasury-allocation/11228) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Mellow vault holdings verifiable on-chain at 0x014e6DA8. Oracle publishes share price on-chain. Lending positions on Aave/Morpho are on-chain and verifiable. The vault contracts ARE the proof-of-reserves. | 9 | 9 | Non-Improvable (optimal) | [P0] [Vault Contract](https://etherscan.io/address/0x014e6DA8F283C4aF65B2AA0f201438680A004452) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | ShareManager (0x4Ce1ac8F), Vault (0x014e6DA8), TimelockController (0xdA6Da82D), Oracle (0x827044735), Admin Safe (0x0Dd73341), Curator Safe (0x9745F161) -- ALL verified on Etherscan. Implementation contracts also verified (BurnableTokenizedShareManager, Oracle). Score Low: all core contracts verified. | 9 | 9 | Non-Improvable (optimal) | [P0] [ShareManager verified](https://etherscan.io/address/0x4Ce1ac8F43E0E5BD7A346A98aF777bF8fbeA1981), [P0] [Vault verified](https://etherscan.io/address/0x014e6DA8F283C4aF65B2AA0f201438680A004452) |

**Documentation & Transparency Subtotal:**
- 6 questions: 3x9 + 3x3 = 27 + 9 = 36/54
- Adjusted: (36/54) x 67.5 = **45.0/67.5 (66.7%)**

**CHANGE LOG vs prior rating:**
- O-DT-03: unchanged at 3, but reasoning improved -- vault address now publicly visible, but addresses still scattered.
- O-DT-06: 3 -> 9. Prior rating could not verify the vault contract because the address was unknown. Address is now publicly visible and ALL contracts are verified on Etherscan.

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | $2M USDC DAO first-loss in EarnUSD. Governance proposal: DAO shares burned up to 100% post-confirmed loss. Loss pause at >=1% MTM. However, activation is via governance/multisig decision, not automatic binding rules. The DAO's first-loss mechanism is being actively tested on EarnETH (loss coverage proposal below 1% threshold). Score Mid: backstop exists and intended for loss coverage, activation discretionary, but mechanism actively being used (on EarnETH). | 3 | 9 | **Improvable** | [P2] [Governance Proposal](https://research.lido.fi/t/lido-earn-competing-on-trust-5m-treasury-allocation/11228), [P2] [Loss Coverage Proposal](https://research.lido.fi/t/authorise-loss-coverage-below-the-1-threshold-for-the-kelp-incident/11527) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Lido DAO treasury (Aragon Agent): ~$125.9M total ($75.5M stETH, $38.1M LDO, $5.9M USDT, $3.8M sUSDS, $1.9M DAI, $0.6M USDC). Note: 2,500 stETH (~$5.8M) allocated to DeFi United relief (Vote #200, passed April 26), pending execution. Post-allocation: ~$120M. Non-LDO liquid: ~$86M. Against total Lido TVL (~$14B), treasury <1%. Against Earn TVL, treasury is significant. $2M first-loss is meaningful for early-stage vault. Score Mid: 1-5% of Earn TVL, <1% of total protocol TVL, concentrated in stETH. | 3 | 3 | Non-Improvable | [P0] [Aragon Agent on Etherscan](https://etherscan.io/address/0x3e40D73EB977Dc6a537aF587D48316feE66E9C8c) |
| O-FR-03 | What is the estimated operational runway at current burn? | Projected DAO revenue $40.6-53.9M (2026). 2025 expenses: $45.5M. $20M LDO buyback program approved. ~$86M non-LDO liquid + $40M+ annual revenue. Runway well over 24 months even after DeFi United allocation. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido Feb 2026 Update](https://blog.lido.fi/recap-lido-tokenholder-update-february-2026/) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | **v0.1-gamma criteria change: now includes composability contagion assessment.** Lido stETH TVL: $42B ATH (Aug 2025) to ~$14B (primarily ETH price). Revenue adjusted with ETH price. No depositor haircuts. stETH June 2022 depeg resolved without protocol losses. The rsETH crisis (April 2026) did NOT directly impact EarnUSD. Regarding composability contagion: earnUSD is NOT widely composed into external lending markets -- it is a new receipt token with minimal external integrations. Composability contagion risk is negligible. Lido DAO's 2,500 stETH contribution to DeFi United shows proactive crisis management. Score Low: stress events showed temporary TVL/revenue decline without depositor loss; EarnUSD has negligible composability surface area. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido Feb 2026 Update](https://blog.lido.fi/recap-lido-tokenholder-update-february-2026/), [P3] [DeFiLlama](https://defillama.com/protocol/lido), [P2] [DeFi United Proposal](https://research.lido.fi/t/lido-dao-contribution-to-coordinated-rseth-relief-effort/11483) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Mellow Core Vault contract (non-upgradeable underlying assets in Aave/Morpho remain accessible). BoringQueue-equivalent (RedeemQueue) is on-chain. Curator stopping freezes rebalancing but funds remain accessible via direct contract interaction (RedeemQueue claim functions). Lido Dual Governance ensures no single entity controls DAO. However, the off-chain Oracle consensus group is needed for new price reports, which are required for processing new redemptions. Score Mid: most core functions continue but off-chain Oracle dependency may degrade new redemption processing. | 3 | 3 | Non-Improvable | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |

**Financial Resilience Subtotal:**
- 5 questions: 2x9 + 3x3 = 18 + 9 = 27/45
- Adjusted: (27/45) x 67.5 = **40.5/67.5 (60.0%)**

**CHANGE LOG vs prior rating:**
- O-FR-04: unchanged at 9, but analysis updated per v0.1-gamma to include composability contagion (negligible for earnUSD).
- O-FR-05: 9 -> 3. Prior rating stated "BoringVault core non-upgradeable" and "BoringQueue on-chain." Mellow Core Vault has an off-chain Oracle dependency for processing new redemptions, which means full maintenance mode is degraded.

**Operations Total: 56.25 + 47.5 + 45.0 + 40.5 = 189.25/270 (70.1%)**

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 75 | 99 | 136.4 | 180 | 75.8% |
| | Key Management (8 Q) | 54 | 72 | 135.0 | 180 | 75.0% |
| | **Security Subtotal** | | | **271.4** | **360** | **75.4%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 63 | 81 | 35.0 | 45 | 77.8% |
| | Collateral (3 of 4 Q scored) | 21 | 27 | 35.0 | 45 | 77.8% |
| | Infra Counterparty (6 of 11 Q scored) | 22 | 54 | 18.3 | 45 | 40.7% |
| | Protocol Counterparty (5 Q) | 27 | 45 | 27.0 | 45 | 60.0% |
| | Liquidity (9 Q) | 51 | 81 | 28.3 | 45 | 62.9% |
| | Market (5 Q) | 31 | 45 | 31.0 | 45 | 68.9% |
| | **Strategy Subtotal** | | | **174.6** | **270** | **64.7%** |
| **Operations** | Governance (4 Q) | 30 | 36 | 56.25 | 67.5 | 83.3% |
| | Team & Legal (9 Q) | 57 | 81 | 47.5 | 67.5 | 70.4% |
| | Documentation (6 Q) | 36 | 54 | 45.0 | 67.5 | 66.7% |
| | Financial Resilience (5 Q) | 27 | 45 | 40.5 | 67.5 | 60.0% |
| | **Operations Subtotal** | | | **189.25** | **270** | **70.1%** |
| **TOTAL** | | | | **635.25** | **900** | **70.6%** |

---

