# Moonwell Flagship USDC - Risk Rating

**Rating Date**: 2026-06-25
**Final Grade**: BB
**Total Score**: 776.9/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

## Executive Summary

Moonwell Flagship USDC is a Morpho Vaults V1 (MetaMorpho) ERC-4626 vault on Base (chainId 8453) that accepts USDC deposits and dynamically supplies liquidity across blue-chip Morpho Blue lending markets. The vault is owned by the Moonwell DAO (via the Temporal Governor cross-chain governance contract using Wormhole), curated by Block Analitica & B.Protocol (2-of-4 Safe), and protected by a Moonwell Security Council Guardian (3-of-5 Safe) — the same owner, guardian, curator Safe, 4-day timelock, and 15% performance fee as the Moonwell Flagship ETH vault. Underlying Morpho Blue is an immutable ~600-line singleton contract with extensive audit coverage from Tier-0 firms (OpenZeppelin, Spearbit, Cantina) and Certora formal verification. Vault TVL stands at approximately $9.63M with a net APY of ~4.53% and all allocated markets priced by Chainlink (Tier-0) ChainlinkOracleV2 adapters (verified live via Morpho API).

The vault shares its entire platform-level risk profile with the Flagship ETH vault: immutable Morpho Blue core with no admin keys, reputable curation by Block Analitica (originated from the MakerDAO risk team, currently advising Sky, Spark, Compound, and others), and a robust 3-of-5 Security Council Guardian. Where the USDC vault diverges is its collateral mix. Borrowers in the underlying markets post WETH (~53.1% of supplied assets), cbBTC (~45.8%), wstETH (~1.1%), and cbETH (~0%) against the vault's USDC — all at a conservative 86% LLTV. The ~45.8% allocation to cbBTC, Coinbase's custodially-wrapped BTC, raises the vault's wrapped-asset exposure into the 20–60% band, which is the single material difference versus the ETH vault (where wrapped exposure was only ~12% weETH).

The vault's structure is robust. Its own on-chain record is exploit-free, so S-SC-06 scores Low (9) — consistent with the framework (which scores realized exploits on the rated product) and with peer Morpho USDC vaults such as Gauntlet USDC Prime and Steakhouse USDC, which also scored 9 despite ecosystem incidents that did not touch their depositors. The recurring oracle-misconfiguration exploits at the Moonwell Foundation's separate Compound v2 fork ("Moonwell Core") — Oct 2025 (~$1.7M), Nov 2025 (~$1M), Feb 2026 ($1.78M) — did not affect this Morpho vault; the operator-level pattern they reveal is instead captured in the monitoring, incident-response and manager-history questions (S-SC-10/11, O-TL-05, O-TL-09), alongside the February 2025 bug-bounty removal (S-SC-09), the absence of a dedicated Morpho-vault safety module (O-FR-01), the 15% performance fee, and modest TVL. The single material collateral difference versus the ETH vault is the ~45.8% cbBTC custodial-wrapped exposure (ST-C-04), partly offset by deeper USDC redemption liquidity (ST-L-08). Net result: a BB grade (776.9/900), ~6.7 points below the ETH vault's BB (783.5).

## Rating Overview

| Category | Weight | Current Score | Potential Score | Current % | Potential % |
|----------|--------|---------------|-----------------|-----------|-------------|
| Security | 40% | 312.3 | 360.0 | 86.7% | 100.0% |
| Strategy | 30% | 229.8 | 250.0 | 85.1% | 92.6% |
| Operations | 30% | 234.8 | 265.0 | 86.9% | 98.1% |
| **Total** | **100%** | **776.9** | **875.0** | **86.3%** | **97.2%** |

**Current Grade**: BB (776.9/900 points)
**Potential Grade**: A+ (875.0/900 points) - achievable if improvements made

## Deal Breaker Assessment

No deal breakers triggered. Reviewed:
- **S-SC-01 (Audits):** Multi-firm audit coverage by Tier-0 firms (OpenZeppelin, Spearbit, Cantina, plus Certora formal verification). PASS.
- **S-SC-06 (Exploits):** No exploit has affected the Moonwell Flagship USDC Morpho vault — scored Low (9). The recent Moonwell Core exploits occurred on a separate product (Compound v2 fork lending markets) under the same operator; consistent with the framework wording and peer precedent (S-SC-06 scores realized exploits on the rated product), they are reflected in operator-track-record questions (S-SC-10/11, O-TL-05, O-TL-09) rather than scored against this vault. No Full Deal Breaker. PASS.
- **S-SC-07 (Rug-pull):** No confirmed rug-pull. PASS.
- **S-KM-02 (Single-key fund movement):** Owner is a TimelockController with 4-day timelock plus cross-chain Wormhole governance; vault funds cannot be moved by a single key. PASS.
- **ST-PM-05 (Strategy loss history):** No permanent loss event for this strategy. PASS.
- **ST-PC-05 (Third-party disclosure):** Curators and guardians publicly named with on-chain addresses. PASS.
- **O-TL-04 (Regulatory action):** No known investigations. PASS.
- **O-DT-05 (Proof-of-reserves):** Vault is fully on-chain ERC-4626; reserves are continuously verifiable on Morpho Blue. PASS.

## Improvement Summary

| Status | Count | Points Gap |
|--------|-------|------------|
| Improvable | 12 | +98.2 points |
| Source Missing | 0 | +0 points |
| Non-Improvable | 67 | - |
| N/A | 8 | - |

**Top Improvement Opportunities:**
1. **Restart Moonwell bug bounty program** — Moonwell removed its Immunefi bug bounty in February 2025; this materially affects S-SC-09 and feeds into the operator-level exploit history (+9 raw pts via S-SC-09, plus second-order safety benefit).
2. **Publish curator-level risk monitoring SLAs** — Block Analitica produces dashboards but documented response SLAs for vault-specific incident handling are not publicly verifiable (S-SC-10).
3. **Document curator-level incident response runbook** — Strengthen O-TL-05 by publishing explicit halting procedures for the Public Allocator if enabled and curator-level response SLAs.

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 312.3/360 (86.7%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | MetaMorpho audited by OpenZeppelin (Nov 2023), Spearbit (Nov 2023), and Cantina contest (Jan 2024). Underlying Morpho Blue audited by OpenZeppelin (Oct 2023), Spearbit (Oct 2023), and Cantina contest (Nov-Dec 2023). Vault deployment params (markets, supply caps, LLTV, oracle types) are public on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [MetaMorpho audits](https://github.com/morpho-org/metamorpho/tree/main/audits), [P1] [Morpho Blue audits](https://github.com/morpho-org/morpho-blue/tree/main/audits) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent audits performed by Cantina (Tier-0/competitive), OpenZeppelin (Tier-0), and Spearbit (Tier-0). Certora formal verification also applied. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho audits page](https://docs.morpho.org/get-started/resources/audits/), [P1] [Certora verification](https://morpho.mirror.xyz/pk_jXDlq-pv8TcHeN7X4-zZcYa7TLRmgv87UBCjG4i8) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Morpho Blue and MetaMorpho V1 contracts are immutable (no upgrades possible). Vault parameter changes (markets, caps) go through timelocked governance. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Blue is immutable](https://morpho.org/blog/morpho-blue-and-how-it-enables-our-vision-for-defi-lending/) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | All audit findings remediated and re-verified by competitive contests at Cantina. No outstanding critical or high findings in published reports. | 9 | 9 | Non-Improvable (optimal) | [P1] [MetaMorpho audit reports](https://github.com/morpho-org/metamorpho/tree/main/audits) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue and MetaMorpho V1 are immutable (no upgrade mechanism). Vault parameter changes are subject to a 4-day (345,600s) timelock enforced on-chain; Guardian (3-of-5 Security Council Safe) can veto. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain `timelock = 345600` via Morpho API; [P1] [Morpho roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No on-chain exploit or critical bug has affected this vault's user funds since inception (June 2024) → Low (9). The parent Moonwell DAO's separate Compound v2 fork ("Moonwell Core") suffered oracle-misconfiguration exploits (Oct 2025 ~$1.7M, Nov 2025 ~$1M, Feb 2026 $1.78M), but those hit a different product's depositors, not this Morpho vault. Per the framework, S-SC-06 scores realized exploits on the rated product; peer Morpho USDC vaults (Gauntlet USDC Prime, Steakhouse USDC) likewise scored 9 despite ecosystem incidents not touching their depositors. Operator-level risk from those events is carried in S-SC-10/11, O-TL-05 and O-TL-09. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain vault history (no loss events) via Morpho API / [BaseScan](https://basescan.org/address/0xc1256Ae5FF1cf2719D4937adb3bbCCab2E00A2Ca); [P4] [Moonwell Core incidents — separate product](https://www.halborn.com/blog/post/explained-the-moonwell-hack-november-2025) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No confirmed rug-pull involving Moonwell, Morpho, Block Analitica, or B.Protocol. All teams publicly identified with multi-year on-chain history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Block Analitica](https://blockanalitica.com/), [P1] [Moonwell Foundation Mirror](https://mirror.xyz/moonwellfoundation.eth) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | Current timelock = 345,600s (4 days), well above 24h minimum. No documented timelock reductions in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain `timelock = 345600` via Morpho API |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Moonwell removed its Immunefi bug bounty program in February 2025 (months before the Oct/Nov 2025 and Feb 2026 exploits). Morpho's $2.5M Immunefi bounty does cover MetaMorpho V1 contracts, so the underlying vault code is in scope, but Moonwell's curator/operator layer has no active bounty. | 3 | 9 | **Improvable** | [P4] [Bounty removal context](https://www.ainvest.com/news/moonwell-suffers-1-78m-loss-oracle-misconfiguration-ai-code-vulnerability-2602/), [P1] [Morpho Immunefi](https://immunefi.com/bug-bounty/morpho/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Block Analitica publishes public dashboards monitoring Moonwell vault risk. Moonwell has a Security Council for emergency response. However, no documented real-time monitoring SLA or automated alert-to-pause integration is publicly verifiable for the vault. | 3 | 9 | **Improvable** | [P1] [Block Analitica dashboards](https://blockanalitica.com/), [P1] [Security Council docs](https://docs.moonwell.fi) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Guardian (3-of-5) can revoke pending market cap increases and timelock decreases instantly. Curator can drop supply caps to zero immediately (no timelock on decreases). However, no automated circuit breaker on Public Allocator-driven flows. | 3 | 9 | **Improvable** | [P1] [Morpho roles](https://docs.morpho.org/curate/concepts/roles/), [P0] On-chain guardian = 0xB9d4acf1...AB38 |

**Smart Contract Security Subtotal:**
- Raw scores: 9+9+9+9+9+9+9+9+3+3+3 = 81/99
- Adjusted: (81/99) x 180 = **147.3/180 (81.8%)**

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Vault Owner = Moonwell Temporal Governor (cross-chain Wormhole governance contract, DAO-controlled). Guardian = 3-of-5 Moonwell Security Council Safe. Curator = 2-of-4 Block Analitica/B.Protocol Safe. All addresses verified on-chain via Safe Transaction API. | 9 | 9 | Non-Improvable (optimal) | [P0] [Owner](https://basescan.org/address/0x8b621804a7637b781e2BbD58e256a591F2dF7d51), [P0] [Guardian Safe API](https://safe-transaction-base.safe.global/api/v1/safes/0xB9d4acf113a423Bc4A64110B8738a52E51C2AB38/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Underlying Morpho Blue is immutable; vault contract has no upgrade path. Material parameter changes (new markets, cap increases) require 4-day timelock through Temporal Governor. Curator (2-of-4) can only allocate WITHIN already-enabled markets and decrease caps; cannot route to arbitrary contracts. | 9 | 9 | Non-Improvable (optimal) | [P0] [On-chain timelock = 345600](https://api.morpho.org/graphql), [P1] [Morpho roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Guardian = 3-of-5 Safe (Moonwell Security Council, publicly identified individuals — Gauntlet, Elliot Friedman, Luke Youngblood, X0s0l, Coolhorsegirl), verified 3-of-5 via Safe API. Curator = 2-of-4 Safe (Block Analitica/B.Protocol), verified 2-of-4 via Safe API. Owner = on-chain governance via Temporal Governor. Independent identities verifiable. | 9 | 9 | Non-Improvable (optimal) | [P0] [Guardian Safe = 3-of-5](https://safe-transaction-base.safe.global/api/v1/safes/0xB9d4acf113a423Bc4A64110B8738a52E51C2AB38/), [P0] [Curator Safe = 2-of-4](https://safe-transaction-base.safe.global/api/v1/safes/0x08eDEbFFaE68970DCf751baa826182b3a4aCFC05/) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause not available on MetaMorpho V1 — withdrawals are always permissionless. No address-level blocklist. Curator can only decrease caps. Guardian can veto pending governance changes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | 100% of vault assets held in MetaMorpho ERC-4626 contract supplying to immutable Morpho Blue singleton on Base. No off-chain custody. | 9 | 9 | Non-Improvable (optimal) | [P0] [Vault contract on Basescan](https://basescan.org/address/0xc1256Ae5FF1cf2719D4937adb3bbCCab2E00A2Ca) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | User funds (~$9.63M USDC) are isolated in MetaMorpho vault contract. Moonwell Foundation treasury (9.47M USDC, 415.9 wstETH) held in separate Foundation wallets. Curator/Guardian Safes hold no user funds — only signing rights. | 9 | 9 | Non-Improvable (optimal) | [P0] [Vault on-chain](https://basescan.org/address/0xc1256Ae5FF1cf2719D4937adb3bbCCab2E00A2Ca) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | Strictly enforced on-chain: vault can only supply to Morpho Blue markets explicitly added by Curator + timelock. Currently allocated to 4 active markets (WETH, cbBTC, wstETH, cbETH collateral) plus an idle market, all on Morpho Blue with USDC as loan asset. New markets require 4-day timelock; Guardian can veto. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain allocation queue (Morpho API), [P1] [Morpho roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Moonwell Security Council exists as 3-of-5 multisig for emergency response. However, no publicly documented tabletop test or signer-replacement runbook for this Curator/Guardian Safe specifically. Block Analitica/B.Protocol incident procedures not publicly documented. | 3 | 9 | **Improvable** | [P1] [Security Council docs](https://docs.moonwell.fi) — describes responsibilities but no tested playbook |

**Key Management Subtotal:**
- Raw scores: 9+9+9+9+9+9+9+3 = 66/72
- Adjusted: (66/72) x 180 = **165.0/180 (91.7%)**

**Security Total: 147.3 + 165.0 = 312.3/360 (86.7%)**

### STRATEGY (30% Weight) -- Score: 229.8/270 (85.1%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield is USDC borrowing interest paid across 4 disclosed Morpho Blue markets (WETH, cbBTC, wstETH, cbETH collateral). Net APY ~4.53% (gross ~4.37% excl. rewards, before fee); organic borrower interest after the 15% fee is ~3.7%, so reward-token incentives contribute under ~20% of net. Fully aligned with the stated "USDC lending" mandate. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain allocation + `netApy = 0.0453`, `apy = 0.0437` via Morpho API; [P1] [Vault page](https://app.morpho.org/base/vault/0xc1256Ae5FF1cf2719D4937adb3bbCCab2E00A2Ca/moonwell-flagship-usdc) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss requires (a) bad debt in a Morpho Blue market due to oracle failure or fast collateral depeg, or (b) a collateral crash of WETH/cbBTC/wstETH/cbETH versus USDC beyond the 86% LLTV liquidation thresholds outrunning liquidators. Fee drag (15%) reduces but never inverts yield in normal conditions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho security considerations](https://docs.morpho.org/curate/concepts/security-considerations/) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage at vault level. The vault supplies USDC 1:1 to Morpho Blue markets. Effective leverage = 1.0x. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain allocation |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A — vault is a supplier, not a borrower. Liquidation risk applies to borrowers in underlying Morpho Blue markets (who borrow USDC against WETH/BTC/LST collateral); their liquidation supports vault solvency rather than threatens it. | N/A | N/A | N/A | Question applies to leveraged strategies |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | Moonwell Flagship vaults have operated since June 2024 with no negative-yield event for the USDC vault. The MetaMorpho strategy template has been used by 500+ vaults; ~15 vaults with high-risk long-tail collateral suffered bad debt in the Resolv USR exploit (March 2026), but blue-chip vaults including this one were unaffected. | 9 | 9 | Non-Improvable (optimal) | [P4] [Resolv impact analysis](https://www.panewslab.com/en/articles/019d18ac-26dc-74d5-8f5d-56771dc1a43e); [P1] [Vault history on Morpho](https://app.morpho.org/base/vault/0xc1256Ae5FF1cf2719D4937adb3bbCCab2E00A2Ca/moonwell-flagship-usdc) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Block Analitica publishes risk methodology and per-vault dashboards. Monthly recaps posted on Moonwell forum. Quantitative supply caps and LLTV documented per market. However, no single canonical risk framework document with hard quantitative limits is published. | 3 | 9 | **Improvable** | [P1] [Block Analitica](https://blockanalitica.com/), [P2] [Forum monthly recaps](https://forum.moonwell.fi/t/block-analitica-b-protocol-moonwell-flagship-vaults-monthly-recap-october-2024/1372) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yield is primarily organic borrower interest on Morpho Blue USDC markets. Reward-token incentives add ~0.8% APY (under ~20% of the ~4.53% net APY), below the 30% threshold; base yield remains positive after removing incentives. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain `netApy = 0.0453` vs `apy = 0.0437` from Morpho API |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Withdrawals are instant when idle liquidity sufficient. ~99% of TVL is in WETH and cbBTC markets which have very deep liquidity on Base. Under stress, withdrawals may queue if Morpho Blue markets are at high utilization — but USDC unwinds 1:1 (no slippage), not at a discount. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho V1 design](https://docs.morpho.org/learn/concepts/vault/) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Yield is borrower interest, not a carry or spread trade. Cannot invert to negative in any market regime. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain yield source |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Public Allocator status not confirmed enabled for this vault, but if enabled it would allow permissionless reallocation within Curator-set flow caps. New market additions and cap increases still require 4-day timelock + Guardian veto. No flash-loanable vault takeover. | 3 | 9 | **Improvable** | [P1] [Public Allocator security considerations](https://docs.morpho.org/curate/concepts/security-considerations/) |

**Protocol Mechanics Subtotal:**
- Raw scores: 9+9+9+N/A+9+3+9+9+9+3 = 69/81
- Adjusted: (69/81) x 45 = **38.3/45 (85.2%)**

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Borrowers post: WETH (~53.1% of supplied assets), cbBTC (~45.8%), wstETH (~1.1%), cbETH (~0%). All are blue-chip large-cap assets (ETH, BTC, top LSTs) with established peg/price history, each mapped to an on-chain 86% LLTV and per-market supply cap (cbBTC ~$100M, WETH ~$50M, wstETH ~$30M, cbETH ~$50M). Low-risk by SR collateral criteria. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain allocation + supply caps via Morpho API |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | WETH is ETH itself (no peg to maintain). cbBTC has tracked BTC within <2% since Coinbase launched it (Sept 2024), including the Oct 2025 crash. wstETH and cbETH maintained <2% deviation through 2024-2026 stress events with any brief deviations recovering within hours. | 9 | 9 | Non-Improvable (optimal) | [P3] DefiLlama price history, [P4] LST/cbBTC market data |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A — the vault is a USDC supplier. Slashing risk on wstETH/cbETH is borne by borrowers; if their LST collateral loses value from slashing, they get liquidated and the vault receives USDC back. | N/A | N/A | N/A | LST/staking risk borne by borrowers, not supplier |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | Vault asset is native Circle-issued USDC on Base (no bridge/wrap risk). Of the underlying collateral, cbBTC — Coinbase-custodied wrapped BTC — represents ~45.8% of supplied assets, placing wrapped exposure in the 20–60% band. WETH (~53.1%) is excluded as a thin wrapper of native ETH; wstETH/cbETH are protocol receipt tokens covered elsewhere. cbBTC carries documented on-chain supply caps but single-entity (Coinbase) custody, not a multi-verifier bridge. | 3 | 3 | Non-Improvable | [P0] On-chain allocation via Morpho API (cbBTC supplyAssetsUsd ~$4.41M of ~$9.63M); [P1] [cbBTC overview (Coinbase)](https://www.coinbase.com/cbbtc) |

**Collateral Subtotal:**
- Raw scores: 9+9+N/A+3 = 21/27
- Adjusted: (21/27) x 45 = **35.0/45 (77.8%)**

#### Infra Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Base (Tier-2 chain), Morpho Blue (Tier-0 protocol), Chainlink oracles (Tier-0), Safe multisig infra (Tier-0), Wormhole bridge for Moonwell governance (Tier-2). All disclosed and reputable. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain dependencies |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | All 4 active markets use ChainlinkOracleV2 adapters (verified via Morpho API: WETH/USDC uses ETH/USD feed 0x71041ddd..., cbBTC/USDC uses BTC/USD feed 0x64c91199..., wstETH/USDC chains wstETH/ETH + ETH/USD). Chainlink (Tier-0) is the primary feed; no hardcoded prices. Oracles per market are fixed at market creation (immutable Morpho Blue design) — if an oracle fails, the supply cap can be dropped instantly but the oracle cannot be swapped, so the curator must migrate to a new market. | 3 | 3 | Non-Improvable | [P0] On-chain oracle types/feeds via Morpho API; [P1] [Morpho oracle design](https://github.com/morpho-org/morpho-blue-oracles) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | No critical off-chain providers in the fund flow. Allocation can be triggered via Block Analitica's keeper but the vault operates correctly without any off-chain component. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho V1 design](https://docs.morpho.org/learn/concepts/vault/) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Base has had brief congestion events (Nov 2023 launch issues, Jul 2024 sequencer pause <1h) but no incidents preventing on-chain withdrawals. Morpho Blue has had no outages. Chainlink feeds remained operational through stress events on Base. | 9 | 9 | Non-Improvable (optimal) | [P3] [L2Beat Base stats](https://l2beat.com/scaling/projects/base), [P1] Morpho status |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Base: brief sequencer pause September 5, 2023 (~1h) — pre-vault deployment. No halts >30min in last 12 months affecting normal operations. | 9 | 9 | Non-Improvable (optimal) | [P3] [L2Beat Base](https://l2beat.com/scaling/projects/base) |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A — vault is a USDC supplier; slashing risk borne by borrowers in LST markets. | N/A | N/A | N/A | LST risk borne by borrowers |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A — Base sequencer is Coinbase-operated (single sequencer L2), but this is a chain-level concern not vault-level. | N/A | N/A | N/A | Not applicable to ERC-4626 vault |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | Base sequencer is single point of failure for withdrawal latency (could delay txn but users can force-exit via L1 after 7-day window). Morpho Blue is immutable so no contract risk. Chainlink oracle failure on a market could block borrows but not vault withdrawals. | 3 | 3 | Non-Improvable | [P3] [L2Beat Base risks](https://l2beat.com/scaling/projects/base) |
| ST-IC-09 | How robust is the cross-chain messaging or bridge verification setup? | N/A — vault operates solely on Base; no cross-chain messaging for fund movement. Moonwell governance uses Wormhole but governance messages only affect parameters, not user funds. | N/A | N/A | N/A | Single-chain vault |
| ST-IC-10 | Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting? | N/A — vault is not a cross-chain product. | N/A | N/A | N/A | Single-chain vault |
| ST-IC-11 | Is the off-chain verification infrastructure resilient to data-source manipulation? | N/A — no off-chain verifiers in vault operations. | N/A | N/A | N/A | No off-chain verification |

**Infra Counterparty Subtotal:**
- Raw scores: 9+3+9+9+9+N/A+N/A+3+N/A+N/A+N/A = 42/54
- Adjusted: (42/54) x 45 = **35.0/45 (77.8%)**

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Vault deploys 100% to Morpho Blue (Tier-0 protocol). Borrowers post collateral from Coinbase (cbBTC, cbETH), Lido (wstETH), and native ETH (WETH). All Tier-0/1 venues/issuers. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain markets; [P1] [Morpho ecosystem](https://docs.morpho.org) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Curator fee = 15% of vault interest, paid to Block Analitica/B.Protocol Safe. Moonwell DAO and Foundation receive performance fees per governance proposal. Documented but exact revenue-share split between Block Analitica and B.Protocol not publicly itemized. | 3 | 9 | **Improvable** | [P0] On-chain `fee = 0.15` via Morpho API; [P2] [Forum vault listing](https://forum.morpho.org/t/block-analitica-b-protocol-flagship-eth-and-usdc-metamorpho-vaults-whitelisting/372) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Each Morpho Blue market has an on-chain supply cap set by Curator (cbBTC/USDC ~$100M, WETH/USDC ~$50M, wstETH/USDC ~$30M, cbETH/USDC ~$50M). Cap increases require 4-day timelock. Curator can decrease caps instantly. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain supply caps via Morpho API |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Vault redeems from Morpho Blue markets in real-time when idle liquidity exists. If full unwind needed and markets are at high utilization, curator can drop caps to force borrowers to repay; otherwise users wait for natural repayment or partial exits. No discretionary approvals needed. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho V1 docs](https://docs.morpho.org/curate/concepts/security-considerations/) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Curators (Block Analitica + B.Protocol, 2-of-4 Safe) and Guardian (Moonwell Security Council, 3-of-5 Safe) named publicly with on-chain Safe addresses. Owner (Temporal Governor) is DAO-controlled. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain addresses via Safe API; [P1] [Moonwell vault docs](https://docs.moonwell.fi/moonwell/moonwell-overview/vaults) |

**Protocol Counterparty Subtotal:**
- Raw scores: 9+3+9+9+9 = 39/45
- Adjusted: (39/45) x 45 = **39.0/45 (86.7%)**

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless ERC-4626 `withdraw()` and `redeem()`. No pause function on MetaMorpho V1. No address-level blocking. Available liquidity = idle USDC + repayments in underlying markets. | 9 | 9 | Non-Improvable (optimal) | [P0] [Vault contract](https://basescan.org/address/0xc1256Ae5FF1cf2719D4937adb3bbCCab2E00A2Ca) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Vault TVL ~$9.63M is small relative to USDC liquidity on Base (the deepest stablecoin on the chain) and to aggregate Morpho Blue USDC market liquidity. Withdrawals can absorb >10% of TVL instantly. Full unwind possible within hours under normal utilization. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain TVL + market liquidity |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No documented withdrawal delays for Moonwell Flagship USDC since inception (June 2024). | 9 | 9 | Non-Improvable (optimal) | [P3] On-chain history; [P2] Block Analitica monthly recaps |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | No caps on withdrawals themselves. Withdrawals are limited only by available liquidity in underlying markets. Curator can decrease supply caps to drive repayments, but this is recovery action not restriction. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho roles](https://docs.morpho.org/curate/concepts/roles/) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | March 2026 USR depeg event and Oct 2024 BTC crash both saw Morpho Blue continue serving withdrawals normally on Base. Flagship USDC unaffected. Vault is too small to test multi-hundred-million-dollar stress directly. | 9 | 9 | Non-Improvable (optimal) | [P2] [USR incident impact summary](https://www.panewslab.com/en/articles/019d18ac-26dc-74d5-8f5d-56771dc1a43e) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Vault holds liquid USDC (idle or supplied to immediate-repayment Morpho markets). No unstaking queue. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain asset = USDC |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Primary redemption is in-protocol (vault burn share -> USDC). Secondary mwUSDC market is small but unnecessary for exits. | 9 | 9 | Non-Improvable (optimal) | [P0] Vault ERC-4626 redeem path |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | mwUSDC is redeemed in-protocol 1:1 (not via secondary market); the underlying USDC is the deepest stablecoin on Base and the WETH/cbBTC collateral is deeply liquid, so each can absorb far more than ~10% of the vault's ~$9.63M TVL (~$0.96M) with negligible price impact → Low (9). Consistent with blue-chip Morpho USDC peers (Steakhouse USDC, Gauntlet USDC Prime) scored 9 on the same in-protocol-redemption basis. | 9 | 9 | Non-Improvable (optimal) | [P0] Vault ERC-4626 1:1 redemption path; [P3] [DefiLlama Base/Morpho TVL](https://defillama.com/protocol/morpho) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | If all underlying markets simultaneously hit 100% utilization, withdrawals queue until borrowers repay. Borrowing rates spike steeply at high utilization (Morpho Blue IRM design), incentivizing repayment. No expected permanent haircuts. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho IRM design](https://docs.morpho.org) |

**Liquidity Subtotal:**
- Raw scores: 9+9+9+9+9+9+9+9+9 = 81/81
- Adjusted: (81/81) x 45 = **45.0/45 (100%)**

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | mwUSDC is a yield-bearing ERC-4626 share, not a pegged token — it accrues value (>1.0 USDC per share). No peg to maintain. | N/A | N/A | N/A | Vault share is yield-bearing not pegged |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Vault is a non-leveraged USDC lender denominated in USDC. Crypto price moves do not affect vault solvency directly; only a catastrophic collateral depeg/crash or oracle failure beyond the 86% LLTV buffer in an underlying market would cause loss. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain exposure |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Morpho Blue IRM curves are kinked at ~90% utilization with sharp rate spikes thereafter. No history of sustained 100% utilization in this vault's markets. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho IRM](https://docs.morpho.org) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Block Analitica publishes risk assessments and stress tests on their dashboards. Specific public stress-test reports for Moonwell Flagship USDC are not separately published (covered in monthly recaps at high level). | 3 | 9 | **Improvable** | [P1] [Block Analitica](https://blockanalitica.com/), [P2] [Monthly recaps](https://forum.moonwell.fi/t/block-analitica-b-protocol-moonwell-flagship-vaults-monthly-recap-october-2024/1372) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Vault has no leveraged position. Underlying markets carry an 86% LLTV (a ~14% buffer); if collateral falls vs USDC by more than ~14% suddenly, liquidations occur and the vault receives a bonus. Tail risk = collateral depeg/crash + thin liquidator response. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain LLTV; [P1] Morpho design |

**Market Subtotal:**
- Raw scores: N/A+9+9+3+9 = 30/36
- Adjusted: (30/36) x 45 = **37.5/45 (83.3%)**

**Strategy Total: 38.3 + 35.0 + 35.0 + 39.0 + 45.0 + 37.5 = 229.8/270**

### OPERATIONS (30% Weight) -- Score: 234.8/270 (86.9%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Vault Owner = Moonwell Temporal Governor on Base, controlled by Moonwell DAO (WELL token holders vote on Moonbeam; messages relayed via Wormhole). All major parameter changes (new markets, fees, timelock changes) require on-chain governance. | 9 | 9 | Non-Improvable (optimal) | [P0] [Owner = Temporal Governor](https://basescan.org/address/0x8b621804a7637b781e2BbD58e256a591F2dF7d51); [P1] [Moonwell governance docs](https://docs.moonwell.fi) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | WELL token circulating supply ~4.5B; some concentration among delegates including Gauntlet, Block Analitica, Luke Youngblood. Top-10 voting concentration not separately published in real-time but governance forum shows broad delegate participation. | 3 | 9 | **Improvable** | [P3] CoinGecko market cap; [P2] [Governance forum](https://forum.moonwell.fi) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Vault has 4-day on-chain timelock for parameter changes. Moonwell governance flow: Moonbeam vote -> 24h vote collection -> Wormhole relay -> 24h Temporal Governor timelock -> execution. Guardian (3-of-5 Safe) can veto pending changes. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain `timelock = 345600`; [P1] [Moonwell governance proposals](https://docs.moonwell.fi/moonwell/governance/moonwell-governance/proposals) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Owner (Temporal Governor) can replace Curator via governance + timelock without blocking withdrawals. Withdrawals are independent of curator activity. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho roles](https://docs.morpho.org/curate/concepts/roles/) |

**Governance Subtotal:**
- Raw scores: 9+3+9+9 = 30/36
- Adjusted: (30/36) x 67.5 = **56.25/67.5 (83.3%)**

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Moonwell Foundation = Cayman Islands foundation. Security Council members publicly named (Gauntlet, Elliot Friedman, Luke Youngblood, X0s0l, Coolhorsegirl). Block Analitica founders public (Primoz Kordez et al., based in Ljubljana). B.Protocol founder ex-CTO of Kyber Network. | 9 | 9 | Non-Improvable (optimal) | [P1] [Moonwell Foundation Mirror](https://mirror.xyz/moonwellfoundation.eth); [P1] [Block Analitica About](https://blockanalitica.com/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Three distinct organizations involved: Moonwell Foundation (governance), Block Analitica (curation), B.Protocol (co-curation), Morpho Labs (underlying protocol). No single key-person dependency. | 9 | 9 | Non-Improvable (optimal) | [P1] Multiple team disclosures |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Moonwell Foundation = Cayman Islands foundation company with named directors. Morpho Labs = French legal entity. Block Analitica = Slovenia-based company. | 9 | 9 | Non-Improvable (optimal) | [P1] [Moonwell Foundation intro](https://mirror.xyz/moonwellfoundation.eth) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known regulatory actions against Moonwell Foundation, Morpho Labs, Block Analitica, or B.Protocol. | 9 | 9 | Non-Improvable (optimal) | [P4] News search returns no enforcement actions |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Moonwell Security Council acts as 24/7 emergency multisig (5 members across regions). Block Analitica has dedicated risk team. However, no documented response SLA or runbook for halting Public Allocator-driven flows specifically for this vault. | 3 | 9 | **Improvable** | [P1] [Security Council docs](https://docs.moonwell.fi) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Active Discord, governance forum, and X presence. Monthly recaps posted on forum. Past incidents on Moonwell Core received same-day public disclosure and recovery proposals. | 9 | 9 | Non-Improvable (optimal) | [P2] [Forum activity](https://forum.moonwell.fi); [P4] Public incident disclosures |
| O-TL-07 | Are major investors or strategic partners disclosed? | Original Moonbeam Foundation grant publicly documented. Partnerships with Morpho Labs, Block Analitica, B.Protocol, Coinbase (cbBTC/cbETH), and Wormhole disclosed. | 9 | 9 | Non-Improvable (optimal) | [P1] [Moonwell partnerships](https://docs.moonwell.fi) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Block Analitica curates multiple vaults across Spark, Compound, Morpho, Summer.fi, HyperLend. B.Protocol manages backstop pools. Roles disclosed; conflicts addressed by per-vault risk parameters and on-chain caps. No documented circular incentive. | 3 | 9 | **Improvable** | [P1] [Block Analitica protocols list](https://blockanalitica.com/) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | Block Analitica curated Spark DAI Pool which experienced no loss events. Block Analitica oversight at Sky/MakerDAO has been incident-free. Some Morpho vaults with Block Analitica involvement saw bad debt from Resolv USR (March 2026) — those were higher-risk long-tail vaults, not Flagship. No uncompensated user loss directly attributable to Block Analitica curation. | 3 | 3 | Non-Improvable | [P4] [Resolv impact](https://www.panewslab.com/en/articles/019d18ac-26dc-74d5-8f5d-56771dc1a43e); [P1] [Block Analitica](https://blockanalitica.com/) |

**Team & Legal Subtotal:**
- Raw scores: 9+9+9+9+3+9+9+3+3 = 63/81
- Adjusted: (63/81) x 67.5 = **52.5/67.5 (77.8%)**

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Moonwell docs cover vaults, governance, Security Council, contracts. Morpho docs cover MetaMorpho V1 architecture, roles, security considerations. Block Analitica publishes monthly recaps. | 9 | 9 | Non-Improvable (optimal) | [P1] [Moonwell docs](https://docs.moonwell.fi); [P1] [Morpho docs](https://docs.morpho.org) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Morpho security considerations doc explicitly lists scenarios. Block Analitica monthly recaps describe market allocations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho security considerations](https://docs.morpho.org/curate/concepts/security-considerations/) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Moonwell contracts page on docs lists all Base contracts including all Morpho vault addresses. | 9 | 9 | Non-Improvable (optimal) | [P1] [Moonwell contracts page](https://docs.moonwell.fi/moonwell/protocol-information/contracts) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Morpho docs explain four roles (Owner, Curator, Allocator, Guardian). On-chain timelock visible. Role assignments published via governance proposals. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | ERC-4626 vault on immutable Morpho Blue — assets and liabilities continuously verifiable on-chain via `totalAssets()` and share supply. Block Analitica dashboard shows real-time allocations. | 9 | 9 | Non-Improvable (optimal) | [P0] [Vault contract](https://basescan.org/address/0xc1256Ae5FF1cf2719D4937adb3bbCCab2E00A2Ca); [P1] [Block Analitica](https://blockanalitica.com/) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | mwUSDC vault verified on BaseScan. Morpho Blue verified. Safe contracts verified. All key infrastructure verified. | 9 | 9 | Non-Improvable (optimal) | [P0] [BaseScan verified](https://basescan.org/address/0xc1256Ae5FF1cf2719D4937adb3bbCCab2E00A2Ca#code) |

**Documentation Subtotal:**
- Raw scores: 9+9+9+9+9+9 = 54/54
- Adjusted: (54/54) x 67.5 = **67.5/67.5 (100%)**

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Moonwell Foundation treasury (9.47M USDC, 415.9 wstETH) historically used to cover Moonwell Core losses (e.g., $2.68M cbETH recovery plan Feb 2026, $1.7M Oct 2025 reserve coverage). No dedicated safety module for Morpho vaults specifically, but Foundation has demonstrated willingness to cover losses. | 3 | 9 | **Improvable** | [P1] [Moonwell Foundation](https://mirror.xyz/moonwellfoundation.eth); [P4] [cbETH recovery plan](https://blockonomi.com/moonwell-proposes-2-68m-recovery-plan-after-cbeth-liquidation-incident-harms-181-borrowers-on-base/) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Foundation treasury: 9.47M USDC + 415.9 wstETH (~$915k) = ~$10.4M liquid, plus WELL/MFAM tokens (~$4M+). Total Moonwell TVL across products ~$65.57M (DefiLlama). Liquid treasury / total TVL = ~16% (well above 5% threshold). Treasury / this vault TVL ($9.63M) = ~108%. | 9 | 9 | Non-Improvable (optimal) | [P3] [DefiLlama Moonwell TVL $65.57M](https://defillama.com/protocol/moonwell); [P1] [Moonwell Foundation treasury](https://mirror.xyz/moonwellfoundation.eth) |
| O-FR-03 | What is the estimated operational runway at current burn? | Foundation maintains 9.47M USDC and 415.9 wstETH. Moonwell annualized fees $1.76M, revenue $448K (DefiLlama). At reasonable burn assumptions (~$2-3M/year for Foundation operations), liquid runway exceeds 3 years. | 9 | 9 | Non-Improvable (optimal) | [P1] [Moonwell Foundation](https://mirror.xyz/moonwellfoundation.eth); [P3] [DefiLlama revenue data](https://defillama.com/protocol/moonwell) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | Moonwell Flagship USDC vault TVL has held steady through Oct 2025, Nov 2025, Feb 2026 Moonwell Core incidents and the March 2026 Resolv crisis on Morpho. Foundation treasury used to cover Moonwell Core losses ($2.68M cbETH recovery). mwUSDC token has limited external composability surface. | 9 | 9 | Non-Improvable (optimal) | [P3] On-chain TVL history; [P4] Incident recoveries |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | If Moonwell Foundation, Block Analitica, B.Protocol all disappear: Morpho Blue is immutable, vault contract is immutable, withdrawals continue permissionlessly. No curator means no new market additions but existing positions repay normally and users can exit. Underlying Morpho contract has no admin. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Blue immutable](https://morpho.org/blog/morpho-blue-and-how-it-enables-our-vision-for-defi-lending/) |

**Financial Resilience Subtotal:**
- Raw scores: 3+9+9+9+9 = 39/45
- Adjusted: (39/45) x 67.5 = **58.5/67.5 (86.7%)**

**Operations Total: 56.25 + 52.5 + 67.5 + 58.5 = 234.75/270**

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 81 | 99 | 147.3 | 180 | 81.8% |
| | Key Management (8 Q) | 66 | 72 | 165.0 | 180 | 91.7% |
| | **Security Subtotal** | | | **312.3** | **360** | **86.7%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 69 | 81 | 38.3 | 45 | 85.2% |
| | Collateral (3 of 4 Q scored) | 21 | 27 | 35.0 | 45 | 77.8% |
| | Infra Counterparty (6 of 11 Q scored) | 42 | 54 | 35.0 | 45 | 77.8% |
| | Protocol Counterparty (5 Q) | 39 | 45 | 39.0 | 45 | 86.7% |
| | Liquidity (9 Q) | 81 | 81 | 45.0 | 45 | 100.0% |
| | Market (4 of 5 Q scored) | 30 | 36 | 37.5 | 45 | 83.3% |
| | **Strategy Subtotal** | | | **229.8** | **270** | **85.1%** |
| **Operations** | Governance (4 Q) | 30 | 36 | 56.3 | 67.5 | 83.3% |
| | Team & Legal (9 Q) | 63 | 81 | 52.5 | 67.5 | 77.8% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 39 | 45 | 58.5 | 67.5 | 86.7% |
| | **Operations Subtotal** | | | **234.8** | **270** | **86.9%** |
| **TOTAL** | | | | **776.9** | **900** | **86.3%** |

---

## Validation Checklist

- [x] Smart Contract Security: 8×9 + 3×3 = 72+9 = 81/99 (scores 9,9,9,9,9,9,9,9,3,3,3). 81/99 × 180 = 147.27 (verified)
- [x] Key Management: 7×9 + 1×3 = 63+3 = 66/72. 66/72 × 180 = 165.00 (verified)
- [x] Security subtotal: 147.27 + 165.00 = 312.27 (verified)
- [x] Protocol Mechanics: 7×9 + 2×3 + 1×N/A = 63+6 = 69/81. 69/81 × 45 = 38.33 (verified)
- [x] Collateral: 2×9 + 1×3 + 1×N/A = 18+3 = 21/27. 21/27 × 45 = 35.00 (verified)
- [x] Infra Counterparty: 4×9 + 2×3 + 5×N/A = 36+6 = 42/54. 42/54 × 45 = 35.00 (verified)
- [x] Protocol Counterparty: 4×9 + 1×3 = 36+3 = 39/45. 39/45 × 45 = 39.00 (verified)
- [x] Liquidity: 9×9 = 81/81. 81/81 × 45 = 45.00 (verified)
- [x] Market: 3×9 + 1×3 + 1×N/A = 27+3 = 30/36. 30/36 × 45 = 37.50 (verified)
- [x] Strategy subtotal: 38.33 + 35.00 + 35.00 + 39.00 + 45.00 + 37.50 = 229.83 (verified)
- [x] Governance: 3×9 + 1×3 = 27+3 = 30/36. 30/36 × 67.5 = 56.25 (verified)
- [x] Team & Legal: 6×9 + 3×3 = 54+9 = 63/81. 63/81 × 67.5 = 52.50 (verified)
- [x] Documentation: 6×9 = 54/54. 54/54 × 67.5 = 67.50 (verified)
- [x] Financial Resilience: 4×9 + 1×3 = 36+3 = 39/45. 39/45 × 67.5 = 58.50 (verified)
- [x] Operations subtotal: 56.25 + 52.50 + 67.50 + 58.50 = 234.75 (verified)
- [x] Total: 312.27 + 229.83 + 234.75 = 776.85 (verified)
- [x] All percentages ≤ 100%: Yes (verified)
- [x] No score exceeds its maximum: Yes (verified)
- [x] Grade check: 776.85 → BB range is 760-785. 776.85 falls in BB.

## Rating Determination

| Grade | Range | This Protocol |
|-------|-------|---------------|
| BB+ | 785-810 | - |
| **BB** | **760-785** | **776.9 points** |
| BB- | 735-760 | - |

## **FINAL RATING: BB**

*Moderately elevated risk; resilience is more scenario-dependent. The Moonwell Flagship USDC vault inherits strong infrastructure from Morpho Blue (immutable, multi-firm audited, Tier-0 oracles) and reputable curation from Block Analitica/B.Protocol, sharing its entire platform-level profile with the Flagship ETH vault. At 776.9/900 it sits ~6.7 points below the ETH vault (783.5): its higher cbBTC custodial-wrapped collateral share (~46%, ST-C-04=3) is partly offset by deeper USDC redemption liquidity (ST-L-08=9). Its own on-chain record is exploit-free (S-SC-06=9); the operator-level risk from the parent Moonwell Foundation's separate Moonwell Core exploits and the 2025 bug-bounty removal is reflected in monitoring, incident-response and manager-history questions (S-SC-09/10/11, O-TL-05, O-TL-09).*

---

## Key Risks

- **~46% custodial-wrapped cbBTC collateral**: ~$4.41M of ~$9.63M supplied assets (~45.8%) backs USDC loans against cbBTC, Coinbase-custodied wrapped BTC dependent on single-entity custody, raising wrapped-asset exposure into the 20–60% band (ST-C-04=3) — the primary differentiator from the Flagship ETH vault — [Morpho API on-chain allocation](https://api.morpho.org/graphql).
- **Parent-operator exploit history (not on this vault)**: the Moonwell Foundation's separate Compound v2 fork ("Moonwell Core") suffered three oracle exploits in 7 months (Oct 2025 $1.7M, Nov 2025 $1M, Feb 2026 $1.78M); this Morpho vault was not affected, so its own S-SC-06 is a clean 9, but the operator-level pattern is captured in the monitoring, incident-response and manager-history scores (S-SC-10/11, O-TL-05, O-TL-09) — [Halborn analysis](https://www.halborn.com/blog/post/explained-the-moonwell-hack-november-2025).
- **No active bug bounty**: Moonwell removed its Immunefi bug bounty in February 2025 before the subsequent exploits; only Morpho's underlying $2.5M Immunefi covers MetaMorpho contract code, leaving the curator/operator layer without bounty incentives — [AInvest report](https://www.ainvest.com/news/moonwell-suffers-1-78m-loss-oracle-misconfiguration-ai-code-vulnerability-2602/).
- **Oracle adapter immutability**: All allocated markets use ChainlinkOracleV2 adapters which are immutable per market; if an oracle misconfiguration is discovered the only remediation is dropping the supply cap to zero and migrating, not swapping the oracle in place — [Morpho oracle design](https://github.com/morpho-org/morpho-blue-oracles).
- **15% performance fee**: Vault charges 15% on interest accrued — at the high end among Morpho vaults — reducing user net yield (net APY ~4.53% vs gross ~4.37% before fee plus reward incentives) — [Morpho API on-chain `fee = 0.15`](https://api.morpho.org/graphql).
- **Modest TVL (~$9.63M)**: Vault is small relative to leading Morpho ecosystem USDC vaults (Steakhouse/Gauntlet flagship USDC vaults exceed $50M+), reducing stress-test data — [Morpho API](https://api.morpho.org/graphql).
- **Public Allocator status uncertain**: If Public Allocator is enabled (status not publicly confirmed for this vault), permissionless reallocation within flow caps becomes possible, increasing the surface for atypical-condition exposure adjustments — [Morpho security considerations](https://docs.morpho.org/curate/concepts/security-considerations/).

## Improvement Roadmap

### Quick Wins (High Impact, Low Effort)
1. **Restart Immunefi bug bounty for Moonwell** - Current: 3, Potential: 9 (S-SC-09)
2. **Publish curator-level risk monitoring SLAs** - Current: 3, Potential: 9 (S-SC-10)
3. **Document automated circuit breaker triggers for vault** - Current: 3, Potential: 9 (S-SC-11)
4. **Publish incident response runbook including Public Allocator halt procedures** - Current: 3, Potential: 9 (O-TL-05)
5. **Publish canonical risk framework document with hard quantitative limits** - Current: 3, Potential: 9 (ST-PM-06)

### Medium-Term Improvements (High Impact, Moderate Effort)
1. **Document/test incident playbook for admin-key compromise or signer loss** - Current: 3, Potential: 9 (S-KM-08)
2. **Document explicit conflict-of-interest controls for Block Analitica's multi-protocol curation** - Current: 3, Potential: 9 (O-TL-08)
3. **Publish vault-specific stress test reports** - Current: 3, Potential: 9 (ST-M-04)
4. **Add automated circuit breaker on Public Allocator-driven flows** - Current: 3, Potential: 9 (ST-PM-10)
5. **Itemize curator revenue-share between Block Analitica and B.Protocol** - Current: 3, Potential: 9 (ST-PC-02)

### Long-Term Structural Changes (Variable Impact, High Effort)
1. **Set up dedicated Morpho-vault safety module / loss reserve** - Current: 3, Potential: 9 (O-FR-01)
2. **Publish formal voting concentration analysis for WELL governance** - Current: 3, Potential: 9 (O-G-02)
3. **Reduce cbBTC custodial-wrapped concentration below 20% of collateral** - Current: 3, Potential: 3 (Non-Improvable structural; reflects collateral composition, ST-C-04)

### Evidence Gaps (Source Missing Items)
None identified. All scoring based on verifiable on-chain or published evidence.

**Maximum Achievable Grade:** A+ (875.0/900 if all 12 improvable items addressed)
**Points to Next Grade Tier:** 8.2 points needed to reach BB+ (785-810 range)

## Smart Contract Addresses

| Role | Address | Explorer Link |
|------|---------|---------------|
| VaultContract | 0xc1256Ae5FF1cf2719D4937adb3bbCCab2E00A2Ca | https://basescan.org/address/0xc1256Ae5FF1cf2719D4937adb3bbCCab2E00A2Ca |
| OwnerGovernor | 0x8b621804a7637b781e2BbD58e256a591F2dF7d51 | https://basescan.org/address/0x8b621804a7637b781e2BbD58e256a591F2dF7d51 |
| GuardianMultisig | 0xB9d4acf113a423Bc4A64110B8738a52E51C2AB38 | https://basescan.org/address/0xB9d4acf113a423Bc4A64110B8738a52E51C2AB38 |
| CuratorMultisig | 0x08eDEbFFaE68970DCf751baa826182b3a4aCFC05 | https://basescan.org/address/0x08eDEbFFaE68970DCf751baa826182b3a4aCFC05 |
| MorphoBlue | 0xBBBBBbbBBb9cC5e90e3b3Af64bdAF62C37EEFFCb | https://basescan.org/address/0xBBBBBbbBBb9cC5e90e3b3Af64bdAF62C37EEFFCb |
| Oracle_WETH-USDC | 0xFEa2D58cEfCb9fcb597723c6bAE66fFE4193aFE4 | https://basescan.org/address/0xFEa2D58cEfCb9fcb597723c6bAE66fFE4193aFE4 |
| Oracle_cbBTC-USDC | 0x663BECd10daE6C4A3Dcd89F1d76c1174199639B9 | https://basescan.org/address/0x663BECd10daE6C4A3Dcd89F1d76c1174199639B9 |
| Oracle_wstETH-USDC | 0xD7A1abA119a236Fea5BBC5cAC6836465cbe9289A | https://basescan.org/address/0xD7A1abA119a236Fea5BBC5cAC6836465cbe9289A |
| Oracle_cbETH-USDC | 0xb40d93F44411D8C09aD17d7F88195eF9b05cCD96 | https://basescan.org/address/0xb40d93F44411D8C09aD17d7F88195eF9b05cCD96 |
| EcosystemReserve | 0x65A633E8E379F9358C389c75ff1D913a92ab95B8 | https://basescan.org/address/0x65A633E8E379F9358C389c75ff1D913a92ab95B8 |

## Additional Info

| Field | Value |
|-------|-------|
| Infrastructure Provider | Morpho |
| Protocol Base | _none_ |
| Stated Withdrawal Time | Instant |
| Treasury | 10400000 |
| Treasury Addresses | _none_ |

### Code Audits

| Auditor | Report Link |
|---------|-------------|
| OpenZeppelin (MetaMorpho) | https://github.com/morpho-org/metamorpho/tree/main/audits |
| Spearbit (MetaMorpho) | https://github.com/morpho-org/metamorpho/tree/main/audits |
| Cantina Competition (MetaMorpho) | https://github.com/morpho-org/metamorpho/tree/main/audits |
| OpenZeppelin (Morpho Blue) | https://github.com/morpho-org/morpho-blue/tree/main/audits |
| Spearbit (Morpho Blue) | https://github.com/morpho-org/morpho-blue/tree/main/audits |
| Cantina Competition (Morpho Blue) | https://github.com/morpho-org/morpho-blue/tree/main/audits |
| Certora Formal Verification | https://morpho.mirror.xyz/pk_jXDlq-pv8TcHeN7X4-zZcYa7TLRmgv87UBCjG4i8 |

### Oracles Used

| Oracle | Documentation Link |
|--------|-------------------|
| Chainlink ETH/USD (via ChainlinkOracleV2 adapter, WETH/USDC market) | https://docs.morpho.org/get-started/resources/contracts/oracles/ |
| Chainlink BTC/USD (via ChainlinkOracleV2 adapter, cbBTC/USDC market) | https://docs.morpho.org/get-started/resources/contracts/oracles/ |
| Chainlink wstETH/ETH + ETH/USD (via ChainlinkOracleV2 adapter, wstETH/USDC market) | https://docs.morpho.org/get-started/resources/contracts/oracles/ |
| Chainlink cbETH/ETH + ETH/USD (via ChainlinkOracleV2 adapter, cbETH/USDC market) | https://docs.morpho.org/get-started/resources/contracts/oracles/ |

## Sources

1. Morpho GraphQL API on-chain data for vault 0xc1256Ae5FF1cf2719D4937adb3bbCCab2E00A2Ca on Base (chainId 8453) — accessed 2026-06-25 (owner, guardian, curator, timelock=345600, fee=0.15, totalAssetsUsd≈$9.63M, netApy≈0.0453, apy≈0.0437, allocation, oracle types/feeds)
2. [Safe Transaction Service API — Guardian Safe 0xB9d4acf1...AB38 (3-of-5)](https://safe-transaction-base.safe.global/api/v1/safes/0xB9d4acf113a423Bc4A64110B8738a52E51C2AB38/)
3. [Safe Transaction Service API — Curator Safe 0x08eDEb...FC05 (2-of-4)](https://safe-transaction-base.safe.global/api/v1/safes/0x08eDEbFFaE68970DCf751baa826182b3a4aCFC05/)
4. [BaseScan — mwUSDC vault verified contract](https://basescan.org/address/0xc1256Ae5FF1cf2719D4937adb3bbCCab2E00A2Ca#code)
5. [BaseScan — Moonwell Temporal Governor](https://basescan.org/address/0x8b621804a7637b781e2BbD58e256a591F2dF7d51)
6. [Morpho App — Moonwell Flagship USDC vault page](https://app.morpho.org/base/vault/0xc1256Ae5FF1cf2719D4937adb3bbCCab2E00A2Ca/moonwell-flagship-usdc)
7. [Morpho MetaMorpho audits (GitHub)](https://github.com/morpho-org/metamorpho/tree/main/audits)
8. [Morpho Blue audits (GitHub)](https://github.com/morpho-org/morpho-blue/tree/main/audits)
9. [Morpho audits & security reviews page](https://docs.morpho.org/get-started/resources/audits/)
10. [Morpho Blue immutability blog](https://morpho.org/blog/morpho-blue-and-how-it-enables-our-vision-for-defi-lending/)
11. [Morpho V1 roles documentation](https://docs.morpho.org/curate/concepts/roles/)
12. [Morpho V1 security considerations](https://docs.morpho.org/curate/concepts/security-considerations/)
13. [Morpho Public Allocator docs](https://docs.morpho.org/get-started/resources/contracts/public-allocator/)
14. [Morpho Immunefi bug bounty](https://immunefi.com/bug-bounty/morpho/)
15. [Certora formal verification of Morpho Blue](https://morpho.mirror.xyz/pk_jXDlq-pv8TcHeN7X4-zZcYa7TLRmgv87UBCjG4i8)
16. [Moonwell vault documentation](https://docs.moonwell.fi/moonwell/moonwell-overview/vaults)
17. [Moonwell contracts page](https://docs.moonwell.fi/moonwell/protocol-information/contracts)
18. [Moonwell Foundation introduction (Mirror)](https://mirror.xyz/moonwellfoundation.eth/_u03ooO6jbqLJsZ2U1KcKhPQEs9lPpkHtn76ngiNxQA)
19. [Block Analitica & B.Protocol Flagship Vaults whitelisting forum post](https://forum.morpho.org/t/block-analitica-b-protocol-flagship-eth-and-usdc-metamorpho-vaults-whitelisting/372)
20. [Block Analitica monthly recap October 2024 (Moonwell forum)](https://forum.moonwell.fi/t/block-analitica-b-protocol-moonwell-flagship-vaults-monthly-recap-october-2024/1372)
21. [Block Analitica website](https://blockanalitica.com/)
22. [Coinbase cbBTC overview](https://www.coinbase.com/cbbtc)
23. [DefiLlama — Moonwell TVL ($65.57M)](https://defillama.com/protocol/moonwell)
24. [Halborn — Moonwell hack November 2025](https://www.halborn.com/blog/post/explained-the-moonwell-hack-november-2025)
25. [Blockonomi — cbETH liquidation incident Feb 2026 recovery plan](https://blockonomi.com/moonwell-proposes-2-68m-recovery-plan-after-cbeth-liquidation-incident-harms-181-borrowers-on-base/)
26. [AInvest — Moonwell $1.78M loss from AI-assisted oracle config](https://www.ainvest.com/news/moonwell-suffers-1-78m-loss-oracle-misconfiguration-ai-code-vulnerability-2602/)
27. [PANews — Morpho co-founder on Resolv USR impact (~15 vaults affected, blue-chip vaults unaffected)](https://www.panewslab.com/en/articles/019d18ac-26dc-74d5-8f5d-56771dc1a43e)
28. [L2Beat — Base scaling project stats and risks](https://l2beat.com/scaling/projects/base)
29. [Moonwell GitHub — moonwell-contracts-v2](https://github.com/moonwell-fi/moonwell-contracts-v2)
