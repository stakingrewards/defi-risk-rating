# Morpho - Gauntlet USDC Prime V2 Vault (Ethereum) Risk Rating

**Rating Date**: 2026-06-23
**Final Grade**: BB
**Total Score**: 778.0/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 323.2/360 (89.8%)

#### Smart Contract Security (20% weight, 180 max points)

**NOTE: All Smart Contract Security scores are platform-level and IDENTICAL to the other Morpho Vault V2 ratings under v0.1-gamma (Gauntlet USDC Prime V2 on Base, Steakhouse Prime Instant V2 USDC, Gauntlet USDC Frontier V2) and the Gauntlet USDC Prime V1. The V2 codebase is immutable post-deployment and was independently audited by ChainSecurity/Spearbit/Zellic/Blackthorn + Cantina competition with Certora formal verification. S-SC-10 and S-SC-11 score 3 per the v0.1-gamma verification principle (monitoring cannot automatically trigger protective actions).**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | Yes. Vault V2 infrastructure independently audited by ChainSecurity (Tier-0), Spearbit (Tier-0), Zellic (Tier-0), Blackthorn, and a $200K Cantina competition, with Certora formal verification, on top of 25+ ecosystem audits and the immutable Morpho Blue core (~600 LOC). This vault (0x8c106EE...) deployed via the audited V2 Factory (0xA1D94F74...). The MarketV1 adapter (0xDF62f57E...) is a V2-audited adapter type. All fund-custody/routing contracts covered by ≥2 independent audits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/), [P1] [ChainSecurity V2 Audit](https://www.chainsecurity.com/security-audit/morpho-vault-v2), [P1] [Cantina V2 Competition](https://cantina.xyz/competitions/523e1540-f8c3-45ae-9c5d-b6d35d3a326c) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent V2 work (Sep-Nov 2025): Spearbit (Tier-0), ChainSecurity (Tier-0), with Certora (Tier-0) formal verification. Multiple Tier-0 auditors. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/), [P1] [ChainSecurity V2 Audit](https://www.chainsecurity.com/security-audit/morpho-vault-v2) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable (~600 LOC). Vault V2 (shipped 2025) was preceded by 5+ Tier-0 audit engagements. The deployed VaultV2 contract is immutable post-deployment (no upgrade risk). MarketV1AdapterV2 was separately audited. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/), [P1] [GitHub vault-v2](https://github.com/morpho-org/vault-v2) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 ecosystem vulnerability patched with OpenZeppelin. ChainSecurity V2 asset-solvency findings fixed before deployment; Certora formal verification of invariants; Cantina competition findings addressed in development. All V2 findings resolved before mainnet. | 9 | 9 | Non-Improvable (optimal) | [P1] [ChainSecurity V2 Audit](https://www.chainsecurity.com/security-audit/morpho-vault-v2), [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue is immutable. The VaultV2 contract (0x8c106EE...) is immutable post-deployment -- non-custodial guarantees cannot be changed. Market/adapter changes require Curator + timelock (7 days for addAdapter/removeAdapter/registry; 3 days for caps), with Sentinel revoke. Verified via V2 API. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P0] Morpho V2 GraphQL API (timelocks) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss in this vault or in Morpho/Vault V2 smart contracts. April 2025 frontend issue ($2.6M) was intercepted by a white hat and fully returned. The March 2026 Resolv USR exploit caused bad debt in OTHER Gauntlet vaults (USR collateral) but NOT this Prime vault (blue-chip-only). Morpho liquidations fired per spec in every incident. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P4] [DeFi Prime - Resolv](https://defiprime.com/resolv-usr-exploit) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No. Morpho operates as ADDMO (French nonprofit). Gauntlet Networks Inc. ($1B valuation, public leadership). No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No. V2 timelock framework requires timelock changes to themselves be timelocked (decreaseTimelock is the only 0s function but any decrease still subject to its own process). Most governance functions at 7 days; no reductions documented since deployment. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (timelocks verified 2026-06-23), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Dual standing bounties: Cantina ($2.5M max) and Immunefi ($2.5M Morpho Blue). V2 contracts in scope. Both Tier-0 platforms with payout history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3), [P1] [Immunefi Bounty](https://immunefi.com/bug-bounty/morpho/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Gauntlet partners with Hypernative (real-time monitoring), ZeroShadow (24/7 vSOC), Chainalysis, SEAL Intel; Morpho runs internal monitoring bots. However, per v0.1-gamma verification principle, monitoring cannot automatically trigger protective actions -- no on-chain circuit breakers, no automated pause. The March 2026 Resolv exploit showed the Public Allocator continued auto-supplying capital to broken markets for ~10 hours, proving alerts are not connected to automated protections. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P4] [DeFi Prime - Resolv](https://defiprime.com/resolv-usr-exploit) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design (Morpho prioritizes immutability). V2 introduces the Sentinel role which can reactively deallocate, decrease caps, and revoke pending proposals -- an improvement over V1's Guardian -- but Sentinel actions are manual/reactive, not auto-triggered by invariant breaches, and do not cover automated allocation flows. | 3 | 3 | Non-Improvable | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Smart Contract Security Subtotal:**
- Raw scores: 9×9 (sum 81) + 2×3 (sum 6) = 87/99
- Adjusted: (87/99) × 180 = **158.2/180 (87.9%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

**NOTE: This vault's roles are Safe multisigs verified on-chain via the Safe Transaction Service (Ethereum) -- Owner 4-of-7 (v1.3.0), Curator 3-of-7 (v1.4.1, the Gauntlet multisig), Sentinel 3-of-7 Safe + one EOA Sentinel. This matches the Gauntlet USDC Prime V2 (Base) and V1 governance posture (NOT the unverified Aragon-DAO owner of the Steakhouse Prime Instant V2 vault). KM scores therefore mirror the other Gauntlet vaults.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Owner is a 4-of-7 GnosisSafe (0xC684c658..., Safe v1.3.0, 7 distinct signers, verified via Safe API on Ethereum). Curator is a 3-of-7 GnosisSafe (0x9E33faAE..., v1.4.1 -- the Gauntlet multisig). Owner is also listed among curators. Changes visible on-chain via Safe Tx Service. V2 per-function timelocks: most 7 days, fees/cap-increases 3 days, penalty 1 day. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API Curator](https://api.safe.global/tx-service/eth/api/v1/safes/0x9E33faAE38ff641094fa68c65c2cE600b3410585/), [P0] Morpho V2 GraphQL API |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. VaultV2 is immutable post-deployment; Morpho Blue logic immutable. Moving funds requires going through immutable contract logic; allocators move only to/from enabled adapters within curator-set caps. Owner is 4-of-7 (threshold ≥3, signers ≥5) with 7-day timelock on critical functions. Permissionless ERC4626 redemption plus forceDeallocate always available. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner multisig is 4-of-7 (meets ≥4-of-7 Low-risk threshold). 7 distinct EOA signers verified via Safe API. Gauntlet is a publicly identified company (Tarun Chitra CEO, 50+ employees), so signers are attributable to a known operator. Curator (3-of-7) and a 3-of-7 Sentinel Safe add further layers. One Sentinel is an EOA (single-key) but Sentinel powers are bounded (revoke/deallocate/decrease-cap only, cannot move funds). No multisig changes reducing independence observed. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API Sentinel](https://api.safe.global/tx-service/eth/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking on Morpho Blue (immutable). V2 Gates exist for compliance access control but are timelocked (7 days) and can be permanently disabled via abdication; gates are not currently set to restrict withdrawals. No admin pause. Withdrawals always permissionless. Rules public. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Gates](https://docs.morpho.org/curate/concepts/gates/), [P0] Morpho V2 GraphQL API (gate timelocks = 604800s) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% in non-custodial Morpho Blue contracts on Ethereum. Permissionless ERC4626 redemption + forceDeallocate. No off-chain custody. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P0] Morpho V2 GraphQL API |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation; vault funds in Morpho Blue markets via the adapter, separate from treasury/ops. Both fees 0% (V2 API). Morpho is a nonprofit with no profit extraction. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (performanceFee=0, managementFee=0), [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain adapter whitelist: a single MorphoMarketV1 adapter (0xDF62f57E...) accessing Morpho Blue markets only. Adapter additions require Curator + 7-day timelock; multi-dimensional absolute & relative caps enforce per-market/collateral limits on-chain. Aligned to the Prime blue-chip mandate (cbBTC, WBTC, wstETH markets). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (adapters, caps), [P1] [V2 Adapter Docs](https://docs.morpho.org/curate/tutorials-v2/listing-adapters/) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Gauntlet has ZeroShadow (24/7 SOC), Hypernative, SEAL Intel partnerships; Morpho docs include emergency procedures; V2 Sentinel enables faster de-risking. But no public, vault-specific incident playbook with explicit key-rotation steps or tabletop results published. The Resolv incident response (failure to halt automated allocation for hours) suggests playbook gaps. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Morpho Emergency Procedures](https://docs.morpho.org/curate/emergency/) |

**Key Management Subtotal:**
- Raw scores: 7×9 (sum 63) + 1×3 (sum 3) = 66/72
- Adjusted: (66/72) × 180 = **165.0/180 (91.7%)**

**Security Total: 158.2 + 165.0 = 323.2/360 (89.8%)**

---

### STRATEGY (30% Weight) -- Score: 229.8/270 (85.1%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from overcollateralized USDC lending against blue-chip collateral (cbBTC 88.4%, WBTC 7.5%, wstETH 4.0%) via Morpho Blue. 100% mandate-aligned (Prime = large-cap, high-liquidity collateral). Net APY ~3.74%. Core yield is organic lending interest. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (allocations, avgNetApy), [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail shocks: a BTC crash exceeding the ~14% liquidation buffer (86% LLTV), oracle manipulation on an immutable market oracle, or catastrophic wrapped-asset custodian failure (cbBTC via Coinbase, WBTC via BitGo). Bad debt is isolated and socialized per market. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault lends USDC at 1.0x effective leverage. No rehypothecation of depositor funds. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment, [P0] Morpho V2 GraphQL API |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. Liquidation risk applies to borrowers; liquidations protect lenders. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | This Ethereum V2 vault has zero bad debt since 2025-09-30 (it held ~$74M through the March 2026 Resolv window with no loss). However, Gauntlet-curated Frontier/Core vaults (comparable variant: same curator, same Morpho protocol, same deposited asset USDC, differing only in collateral parameters) experienced confirmed bad debt (~$7.5M+) in the March 2026 Resolv USR exploit, initially socialized to lenders (partial later compensation via Merkl). The root cause (USR collateral) is structurally excluded from Prime's blue-chip mandate, so the loss-relevant variant is the conservative Prime tier (zero loss). Scored Mid (3): comparable variant had a limited-impact loss, but Prime mandate isolates the cause. | 3 | 9 | **Improvable** | [P4] [DeFi Prime - Resolv](https://defiprime.com/resolv-usr-exploit), [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Gauntlet VaultBook publishes curation methodology, risk-factor overview, due-diligence process, market-allocation strategy, and Prime/Balanced/Frontier tiering with quantitative insolvency targets (<10 bps of TVL). Agent-based simulations inform allocations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Curation Methodology](https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Primarily organic from USDC lending demand against blue-chip collateral. 0% vault fee enhances net yield. Core yield is organic and remains positive without incentives. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (avgNetApy, fees=0), [P1] [VaultBook Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes (with caveat). USDC is the most liquid stablecoin; immediately-available liquidity is ~$34.4M (~42% of TVL) and idle is $0. forceDeallocate provides a permissionless in-kind backstop (penalty up to ~2%) over an additional ~$9.4M. However, this specific vault has not been stress-tested under direct withdrawal pressure; underlying market utilization is high (~88-91%), so a near-total instant exit would require borrower repayment or staggering. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (liquidityUsd≈$34.4M, forceDeallocatableLiquidityUsd≈$9.4M), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) (forceDeallocate) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. Pure overcollateralized lending interest. No basis trade, peg arbitrage, or funding-rate dependency. Rates set by immutable Adaptive Curve IRM. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment, [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Yes. V2 adapter-based allocation lets appointed allocators move funds to the enabled adapter within multi-dimensional caps, without real-time human approval. Caps limit per-market/collateral exposure, but no automatic kill-switch exists for abnormal conditions (oracle deviation, depeg, utilization spike). Sentinel can reactively deallocate/decrease caps but this is manual. The March 2026 Resolv exploit demonstrated this exact failure mode on Gauntlet vaults. | 3 | 9 | **Improvable** | [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/), [P4] [DeFi Prime - Resolv](https://defiprime.com/resolv-usr-exploit) |

**Protocol Mechanics Subtotal:**
- 9 applicable (ST-PM-04 = N/A): 7×9 (sum 63) + 2×3 (sum 6) = 69/81
- Adjusted: (69/81) × 45 = **38.3/45 (85.2%)**

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Blue-chip only, but BTC-heavy: cbBTC (Coinbase-custodied wrapped BTC, 88.4%), WBTC (BitGo/BiT-Global-custodied wrapped BTC, 7.5%), wstETH (Lido LST, 4.0%). All large-cap, high-liquidity, tiered with on-chain LLTVs (86%) and caps. Mandate-aligned. cbBTC/WBTC carry single-custodian dependencies (Coinbase and BitGo respectively); the ~96% combined wrapped-BTC weight is a notable concentration. Low risk per the established large-cap criterion. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (per-market allocations), [P3] [Morpho App](https://app.morpho.org/ethereum/vault/0x8c106EEDAd96553e64287A5A6839c3Cc78afA3D0/) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | cbBTC: no depeg >2% since Sep 2024 launch. WBTC: despite the Aug 2024 BitGo/BiT-Global custody controversy that caused brief minor discounts, no sustained >2% depeg over 12 months and full recovery. wstETH: tracked the stETH/ETH ratio with no >2% sustained depeg in 12 months. No collateral here showed >2% depeg lasting >24h. Battle-tested blue-chip assets. | 9 | 9 | Non-Improvable (optimal) | [P3] Market price history, [P0] Morpho V2 GraphQL API |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Only wstETH (~4.0%) carries staking exposure; cbBTC/WBTC are BTC (no staking). Lido (30+ operators, coverage fund) manages slashing; exposure is immaterial at this allocation. | 9 | 9 | Non-Improvable (optimal) | [P3] Lido operator data |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | HIGH: cbBTC (~88.4%, Coinbase-custodied wrapped BTC) + WBTC (~7.5%, BitGo-custodied wrapped BTC) ≈ 96% of collateral exposure is wrapped/custodial BTC per the framework definition (wstETH excluded as a protocol receipt token; its risk lives in ST-C-01/02/ST-IC-02). Far exceeds the 60% threshold. Concentrated dual custodial dependency on Coinbase and BitGo. | 1 | 9 | **Improvable** | [P0] Morpho V2 GraphQL API (cbBTC $72.7M + WBTC $6.2M of $82.1M) |

**Collateral Subtotal:**
- 4 questions: 3×9 (sum 27) + 1×1 (sum 1) = 28/36
- Adjusted: (28/36) × 45 = **35.0/45 (77.8%)**

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum Mainnet (Tier-1 chain), Chainlink (Tier-0 oracle; ChainlinkOracleV2 for the cbBTC market, ChainlinkOracle for WBTC and wstETH markets). No bridges in the strategy; no CEX dependency. All dependencies disclosed and Tier-0/Tier-1. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (oracle types), [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | Mandatory immutable-oracle check: each Morpho Blue market uses one immutable oracle with no fallback and no post-deployment correction. Can the priced collateral depeg? cbBTC/WBTC are wrapped custodial assets that could theoretically depeg on custodian failure; wstETH prices via the stETH/ETH ratio plus ETH/USD. Underlying Chainlink feeds price battle-tested deep-liquidity assets where material depeg is historically unprecedented → capped at Mid (3) by the hardcoded/immutable rule. Zero redundancy by design. | 3 | 3 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/), [P0] Morpho V2 GraphQL API (Chainlink oracle types per market) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | No public SOC 2 Type II or ISO27001 for Gauntlet Networks or Morpho Labs/ADDMO disclosed. Chainlink holds enterprise certifications; Coinbase (cbBTC custodian) is SOC 2 certified / NY DFS regulated. Gauntlet runs an off-chain risk engine and allocation models. | 3 | 9 | **Source Missing** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Ethereum L1 has not halted block production in the trailing 12 months; the last notable consensus event (May 2023 finality delay, >3 years ago) did not stop block production. Morpho: April 2025 frontend issue (rollback, funds returned). March 2026 Resolv exploit did not affect this Prime vault. No prolonged inability to withdraw. Deployed >8 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P4] [Ethereum May 2023 Finality Incident](https://www.coindesk.com/tech/2023/05/12/ethereum-beacon-chain-experiences-second-finality-incident-in-24-hours/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum Mainnet has not halted block production or suffered a consensus failure within the last 12 months. Ethereum is a Tier-1 chain with the most decentralized validator set in the ecosystem; the May 2023 finality-delay incidents (>3 years ago, outside the window) did not stop block production. → Low (9). (Note: the Base V2 deployment of this same vault scores 3 here owing to Base's Aug 2025 sequencer halt; this Ethereum vault is not affected.) | 9 | 9 | Non-Improvable (optimal) | [P4] [Ethereum May 2023 Finality Incident](https://www.coindesk.com/tech/2023/05/12/ethereum-beacon-chain-experiences-second-finality-incident-in-24-hours/), Public chain uptime records |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Minimal exposure (wstETH ~4.0%). No material slashing events affecting Lido relevant to this vault in 12 months; trivial events absorbed by buffers. | 9 | 9 | Non-Improvable (optimal) | [P3] Lido slashing data |
| ST-IC-07 | Are validators diverse geographically and by operator? | For the small LST exposure: Lido (wstETH) uses 30+ independent operators across regions. Ethereum's L1 validator set is the most diverse in the ecosystem. LST validator distribution is diverse for the material share. | 9 | 9 | Non-Improvable (optimal) | [P3] Lido operator data |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Permissionless ERC4626 redemption + forceDeallocate always available; no off-chain dependency for withdrawals. An oracle failure halts new borrows/liquidations on a market but does not block lender withdrawals; the Resolv loss required a multi-factor failure (collateral collapse + hardcoded oracle + donation/supplyOnBehalf), not a single component. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-IC-09 | How robust is the cross-chain messaging or bridge verification setup? | N/A -- The vault operates exclusively on Ethereum with no cross-chain messaging or bridge dependency. | N/A | N/A | N/A | Vault architecture |
| ST-IC-10 | Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting? | N/A -- No cross-chain escrow or minting mechanism for this vault. | N/A | N/A | N/A | Vault architecture |
| ST-IC-11 | Is the off-chain verification infrastructure resilient to data-source manipulation? | N/A -- The vault does not rely on off-chain verifiers or cross-chain attestation; oracle data is consumed on-chain via Morpho oracle adapters. | N/A | N/A | N/A | Vault architecture |

**Infrastructure Counterparty Subtotal:**
- 8 applicable (ST-IC-09/10/11 = N/A): 6×9 (ST-IC-01/04/05/06/07/08, sum 54) + 2×3 (ST-IC-02/03, sum 6) = 60/72
- Adjusted: (60/72) × 45 = **37.5/45 (83.3%)**

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All allocation to Morpho Blue markets (Tier-0 protocol) via the adapter. No CEX or RWA exposure. Markets: cbBTC/USDC, WBTC/USDC, wstETH/USDC on Ethereum. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (allocations) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Both performance and management fees are 0% (V2 API). Any Morpho incentives are public via Morpho/Merkl. No hidden rebates identified. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (fees=0), [P1] [VaultBook Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. V2 multi-dimensional absolute & relative caps per market/collateral enforced on-chain. Cap increases require 3-day timelock; cap decreases are instant (risk-reducing). Gauntlet runs continuous automated optimization within caps. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (caps, timelocks), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Positions unwind as borrowers repay; ~$34.4M (~42%) immediately available plus ~$9.4M force-deallocatable. forceDeallocate provides a permissionless in-kind backstop. No discretionary approvals. This specific vault is untested for large-scale unwind, but the underlying blue-chip markets have deep liquidity. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (liquidityUsd, forceDeallocatableLiquidityUsd), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending; no external validators, custodians, or asset managers in vault operations. Gauntlet (curator) disclosed. Collateral custodians (Coinbase for cbBTC, BitGo for WBTC, Lido for wstETH) publicly known. | 9 | 9 | Non-Improvable (optimal) | Vault architecture, [P0] Morpho V2 GraphQL API |

**Protocol Counterparty Subtotal:**
- 5 questions: 5×9 = 45/45
- Adjusted: (45/45) × 45 = **45.0/45 (100.0%)**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless ERC4626 redemption via the immutable V2 vault, plus forceDeallocate in-kind backstop. V2 gates (compliance) are not set to restrict and can be permanently disabled via abdication. No admin pause on Morpho Blue. Non-custodial guarantee preserved. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P1] [V2 Gates](https://docs.morpho.org/curate/concepts/gates/) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Moderate-to-tight. ~$34.4M (~42% of $82.1M TVL) immediately available; idle $0. Markets run at ~88-91% utilization, so near-total exit during stress would require borrower repayment or face queues. forceDeallocate provides ~$9.4M of additional in-kind exit. Can absorb large but not near-total instant exits under stress. | 3 | 3 | Non-Improvable | [P0] Morpho V2 GraphQL API (liquidityUsd≈$34.4M, utilization≈88-91%) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | This vault has no reported delays or freezes in its operating history. It has not been independently stress-tested at scale (it was near-empty during Nov 2025), so a clean record cannot yet evidence Low under stress, but no freeze events have occurred. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API, vault operating history |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | V2 multi-dimensional caps are designed for risk control, not exit restriction; cap decreases are instant and increases timelocked. No evidence of caps used to block exits. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API, [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | UNTESTED for this vault. It held only ~$1 (dust seed) throughout the Nov 2025 liquidity-stress period and scaled to material TVL only in Feb/Mar 2026, so it has experienced no independent withdrawal-stress event. Per the "Favor Demonstrated History" principle, an untested ~88-91%-utilization lending vault caps at Mid (3). Underlying blue-chip markets are deep, supporting recovery, but resilience is not demonstrated -- and even the battle-tested V1 Prime stayed at Mid here after surviving Nov 2025. | 3 | 3 | Non-Improvable | Scoring methodology (untested = Mid; high-utilization lending structurally caps at Mid) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure USDC lending with no lockups, vesting, or bridge dependencies on the lender side. forceDeallocate available. <10% longer-dated exposure. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics, [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary ERC4626 redemption always available; no secondary market required. forceDeallocate is an additional in-kind path. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | USDC is the most liquid stablecoin. cbBTC/WBTC/wstETH are deep-liquidity blue-chip collaterals on Ethereum. In-protocol redemption is the primary exit path; depth comfortably supports staggered exits and most normal-condition sizes. | 9 | 9 | Non-Improvable (optimal) | [P3] Market data, [P0] Morpho V2 GraphQL API |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Moderate / UNTESTED for this vault. ~42% immediate liquidity and 86% LLTV (~14% buffer) plus utilization-based IRM create repayment incentives, suggesting temporary queues rather than permanent haircuts in a run. But this vault has no demonstrated bank-run survival (near-empty during Nov 2025); capped at Mid (3) per scoring principles. | 3 | 3 | Non-Improvable | [P0] Morpho V2 GraphQL API, Scoring methodology (untested = Mid; high-utilization lending caps at Mid) |

**Liquidity Subtotal:**
- 9 questions: 6×9 (sum 54) + 3×3 (sum 9) = 63/81
- Adjusted: (63/81) × 45 = **35.0/45 (77.8%)**

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | The vault share is an ERC4626 NAV-based claim on USDC plus yield. It has NOT yet been tested under direct redemption/withdrawal stress (near-empty during the Nov 2025 stress; scaled up only afterward), so per the "Favor Demonstrated History" principle it currently scores Mid (3). Unlike a leveraged or peg token, the NAV-based share holds par by construction: the battle-tested Gauntlet USDC Prime V1 on Ethereum scored Low (9) here after its share stayed stable through Nov 2025 and the March 2026 Resolv crisis. This distinct V2 vault can reach Low (9) once it survives a comparable direct withdrawal-stress event with NAV intact. | 3 | 9 | **Improvable** | [P0] Morpho V2 GraphQL API, Scoring methodology (untested = Mid now; demonstrated NAV stability = Low 9) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Very low. Vault lends USDC -- dollar-denominated; no directional BTC/ETH exposure for lenders. Risk is borrower bad debt, not market direction. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Immutable Adaptive Curve IRM per market; rates auto-increase with utilization. No governance manipulation possible. No history of prolonged ≥95% utilization on these blue-chip markets beyond brief spikes (current ~88-91%). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (utilization), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. Gauntlet agent-based simulations and VaultBook risk-exposure modeling; Certora formally verified Morpho Blue liquidation mechanics; 86% LLTV gives ~14% buffer. Blue-chip collateral with deep liquidation markets. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side only. Liquidations protect lenders by restoring market solvency; the LIF goes to liquidators. 86% LLTV (~14% buffer) on deep-liquidity blue-chip collateral makes lender bad debt unlikely outside extreme gaps. | 9 | 9 | Non-Improvable (optimal) | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal:**
- 5 questions: 4×9 (sum 36) + 1×3 (sum 3) = 39/45
- Adjusted: (39/45) × 45 = **39.0/45 (86.7%)**

**Strategy Total: 38.3 + 35.0 + 37.5 + 45.0 + 35.0 + 39.0 = 229.8/270 (85.1%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 38.3 | 45 | 85.2% |
| Collateral | 35.0 | 45 | 77.8% |
| Infra Counterparty | 37.5 | 45 | 83.3% |
| Protocol Counterparty | 45.0 | 45 | 100.0% |
| Liquidity | 35.0 | 45 | 77.8% |
| Market | 39.0 | 45 | 86.7% |
| **Strategy Total** | **229.8** | **270** | **85.1%** |

---

### OPERATIONS (30% Weight) -- Score: 225.0/270 (83.3%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid with strong checks. Morpho Blue immutable; VaultV2 immutable post-deployment. Adapter/cap changes require Curator + timelock (7 days for adapters, 3 for cap increases) + Sentinel revoke. Role segregation (Owner, Curator, Allocator, Sentinel). No single entity can unilaterally change fund-custody logic. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/), [P0] Morpho V2 GraphQL API |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- No governance-token voting for this vault; controlled by Safe multisigs + Sentinel. Concentration captured in S-KM-01/S-KM-03. | N/A | N/A | N/A | [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. Per-function timelocks verified via V2 API (2026-06-23): setIsAllocator/gates/registry/addAdapter/removeAdapter/increaseTimelock/abdicate = 7 days; setPerformanceFee/setManagementFee/increaseAbsoluteCap/increaseRelativeCap = 3 days; setForceDeallocatePenalty = 1 day; decreaseTimelock & fee-recipient setters = 0s. All material/upgrade functions ≥24h. Sentinel (3-of-7 Safe + EOA) can revoke pending actions and decrease caps. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API (timelocks verified), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner (4-of-7) can change Curator/roles subject to timelock; withdrawals remain permissionless via ERC4626 + forceDeallocate throughout. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Governance Subtotal:**
- 3 applicable (O-G-02 = N/A): 3×9 = 27/27
- Adjusted: (27/27) × 67.5 = **67.5/67.5 (100.0%)**

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Gauntlet: Tarun Chitra (CEO/co-founder, ex-D.E. Shaw Research), Rei Chiang (co-founder), 50+ team. Morpho: Paul Frambot (CEO). All publicly identified with verifiable track records. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Team](https://www.gauntlet.xyz/our-team), [P1] [Morpho](https://morpho.org/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Gauntlet has 50+ employees; Morpho is a separate full team ($73.6M raised). Multiple independent parties can operate the vault. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet About](https://www.gauntlet.xyz/about) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Morpho: ADDMO (French nonprofit) + Morpho Labs SAS (France). Gauntlet: Gauntlet Networks Inc. (New York, USA). Both clearly identified. (SEC action vs unrelated "Gauntlet Holdings, LLC" is a different entity.) | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P1] [Gauntlet](https://www.gauntlet.xyz/) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known material enforcement actions against Gauntlet Networks Inc. or Morpho entities in major jurisdictions. | 9 | 9 | Non-Improvable (optimal) | Public records |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Gauntlet has 24/7 on-call (ZeroShadow vSOC, Hypernative, SEAL Intel); Morpho demonstrated 4-min response (April 2025). However, per v0.1-gamma automation override, incident response MUST include documented procedures to halt automated allocation. The March 2026 Resolv exploit showed the Public Allocator kept supplying capital to broken markets for hours -- response did not halt automated allocation within SLA. Same structural gap applies to V2 adapter-driven flows. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P4] [DeFi Prime - Resolv](https://defiprime.com/resolv-usr-exploit) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Gauntlet publishes detailed market reports within days; active VaultBook; rapid incident communication during Nov 2025 and March 2026 events. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Gauntlet: Polychain, Paradigm, Ribbit Capital ($1B valuation). Morpho: a16z, Variant, Pantera, Coinbase Ventures (29 investors, $73.6M). All disclosed. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet $1B Valuation](https://www.gauntlet.xyz/resources/announcing-our-1-billion-valuation-and-next-steps-for-the-gauntlet-platform) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Gauntlet manages many vaults across chains and tiers (Prime/Balanced/Frontier; $1B+ AUM). Tiered risk system, automated allocation, and VaultBook provide structural mitigations, but no formal quantitative conflict-of-interest policy with hard constraints is published. The Resolv incident raised cross-vault risk-management questions. | 3 | 9 | **Improvable** | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | The March 2026 Resolv USR exploit caused confirmed bad debt (~$7.5M+) in Gauntlet-curated Frontier/Core vaults, initially uncompensated (partial later compensation via Merkl). This Prime vault had zero loss (blue-chip-only), but the framework evaluates the manager entity -- Gauntlet is linked to depositor losses in products it curates. Constitutes "one historical loss incident with limited impact" followed by risk isolation (tiered system worked) and partial compensation. Prior Aave advisory CRV bad debt was advisory, not curation. | 3 | 9 | **Improvable** | [P4] [DeFi Prime - Resolv](https://defiprime.com/resolv-usr-exploit), [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |

**Team & Legal Subtotal:**
- 9 questions: 6×9 (sum 54) + 3×3 (sum 9) = 63/81
- Adjusted: (63/81) × 67.5 = **52.5/67.5 (77.8%)**

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive Morpho V2 docs and Gauntlet VaultBook; V2 architecture (adapters, gates, sentinel, timelocks, forceDeallocate) documented; Prime mandate described. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P1] [VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Liquidation mechanics, bad-debt socialization, oracle risks, and V2 adapter/security considerations documented across Morpho docs. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Security Considerations](https://docs.morpho.org/curate/concepts/security-considerations/) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Morpho V2 contract registry (VaultV2Factory, adapter factories, registry) documented; vault address listed on the Morpho app and addresses page. Etherscan-verified. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Contracts](https://docs.morpho.org/get-started/resources/contracts/morpho-vaults-v2/), [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Comprehensive V2 role/capability matrix; per-function timelock durations documented; changes visible via on-chain event logs and Safe Tx Service. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/), [P0] Morpho V2 GraphQL API |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves; all adapter/market allocations visible via V2 API, Morpho app, and Etherscan. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 GraphQL API, [P0] [Etherscan](https://etherscan.io/address/0x8c106EEDAd96553e64287A5A6839c3Cc78afA3D0) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. The VaultV2 contract is deployed and listed/recognized by Morpho (V2 API `listed: true`); the adapter and factory are deployed contracts on Ethereum; Morpho V2 contracts are verified on Etherscan with public source. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0x8c106EEDAd96553e64287A5A6839c3Cc78afA3D0), [P0] Morpho V2 GraphQL API (listed=true) |

**Documentation Subtotal:**
- 6 questions: 6×9 = 54/54
- Adjusted: (54/54) × 67.5 = **67.5/67.5 (100.0%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated safety module for this vault or Morpho generally; bad debt is socialized per Morpho Blue market. Morpho DAO treasury exists but activation for loss coverage is discretionary; no Gauntlet-specific backstop with binding rules. | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/), [P3] [DeFiLlama Treasury](https://api.llama.fi/treasury/morpho) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Insufficient. Morpho DAO treasury ≈ $24.8M per DeFiLlama, ~100% MORPHO tokens (volatile native, negligible stables), against ~$14B+ protocol-wide TVL ≈ 0.17%. Not ring-fenced for this $82.1M vault. Below the 1% threshold and dominated by a volatile native token. | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho), [P3] [DeFiLlama Morpho TVL](https://api.llama.fi/protocol/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Gauntlet ($1B valuation, well-funded) and Morpho ($73.6M raised, nonprofit structure) both have multi-year runway. Curator fees and protocol revenue growing. Runway comfortably >24 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet $1B Valuation](https://www.gauntlet.xyz/resources/announcing-our-1-billion-valuation-and-next-steps-for-the-gauntlet-platform), [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | This vault has NOT independently survived a major stress event with material TVL: it was near-empty (~$1) during the Nov 2025 liquidity stress and scaled to ~$74M only by March 2026 (when it was unaffected by Resolv but not stress-tested under withdrawal pressure). The broader Morpho protocol grew TVL through 2025 stress with isolated-market containment, but per the "Favor Demonstrated History" principle this untested vault cannot score Low. The vault share is not widely composed into external protocols, limiting contagion surface. | 3 | 9 | **Improvable** | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/), Scoring methodology (untested = Mid max) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue and the VaultV2 contract are immutable; permissionless ERC4626 withdrawals + forceDeallocate always available; no proprietary off-chain service required for exits. Sentinel can veto pending changes. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |

**Financial Resilience Subtotal:**
- 5 questions: 2×9 (sum 18) + 2×3 (sum 6) + 1×1 (sum 1) = 25/45
- Adjusted: (25/45) × 67.5 = **37.5/67.5 (55.6%)**

**Operations Total: 67.5 + 52.5 + 67.5 + 37.5 = 225.0/270 (83.3%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 67.5 | 67.5 | 100.0% |
| Team & Legal | 52.5 | 67.5 | 77.8% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 37.5 | 67.5 | 55.6% |
| **Operations Total** | **225.0** | **270** | **83.3%** |

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 87 | 99 | 158.2 | 180 | 87.9% |
| | Key Management (8 Q) | 66 | 72 | 165.0 | 180 | 91.7% |
| | **Security Subtotal** | | | **323.2** | **360** | **89.8%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 69 | 81 | 38.3 | 45 | 85.2% |
| | Collateral (4 Q) | 28 | 36 | 35.0 | 45 | 77.8% |
| | Infra Counterparty (8 of 11 Q scored) | 60 | 72 | 37.5 | 45 | 83.3% |
| | Protocol Counterparty (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity (9 Q) | 63 | 81 | 35.0 | 45 | 77.8% |
| | Market (5 Q) | 39 | 45 | 39.0 | 45 | 86.7% |
| | **Strategy Subtotal** | | | **229.8** | **270** | **85.1%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 63 | 81 | 52.5 | 67.5 | 77.8% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 25 | 45 | 37.5 | 67.5 | 55.6% |
| | **Operations Subtotal** | | | **225.0** | **270** | **83.3%** |
| **TOTAL** | | | | **778.0** | **900** | **86.4%** |

*Total = 323.2 + 229.8 + 225.0 = 778.0.*

---

