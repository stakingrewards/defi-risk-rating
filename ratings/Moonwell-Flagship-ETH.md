# Moonwell Flagship ETH - Risk Rating

**Rating Date**: 2026-05-22
**Final Grade**: BB
**Total Score**: 772.6/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 301.4/360 (83.7%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | MetaMorpho audited by OpenZeppelin (Nov 2023), Spearbit (Nov 2023), and Cantina contest (Jan 2024). Underlying Morpho Blue audited by OpenZeppelin (Oct 2023), Spearbit (Oct 2023), and Cantina contest (Nov-Dec 2023). Vault deployment params (markets, supply caps, LLTV, oracle types) are public on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [MetaMorpho audits](https://github.com/morpho-org/metamorpho/tree/main/audits), [P1] [Morpho Blue audits](https://github.com/morpho-org/morpho-blue/tree/main/audits) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent audits performed by Cantina (Tier-0/competitive), OpenZeppelin (Tier-0), and Spearbit (Tier-0). Certora formal verification also applied. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho audits page](https://docs.morpho.org/get-started/resources/audits/), [P1] [Certora verification](https://morpho.mirror.xyz/pk_jXDlq-pv8TcHeN7X4-zZcYa7TLRmgv87UBCjG4i8) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Morpho Blue and MetaMorpho V1 contracts are immutable (no upgrades possible). Vault parameter changes (markets, caps) go through timelocked governance. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Blue is immutable](https://morpho.org/blog/morpho-blue-and-how-it-enables-our-vision-for-defi-lending/) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | All audit findings remediated and re-verified by competitive contests at Cantina. No outstanding critical or high findings in published reports. | 9 | 9 | Non-Improvable (optimal) | [P1] [MetaMorpho audit reports](https://github.com/morpho-org/metamorpho/tree/main/audits) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue and MetaMorpho V1 are immutable (no upgrade mechanism). Vault parameter changes are subject to a 4-day (345,600s) timelock enforced on-chain; Guardian (3-of-5 Security Council Safe) can veto. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain `timelock = 345600` via Morpho API; [P1] [Morpho roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | The Moonwell Flagship ETH Morpho vault has had no exploit. However, the parent Moonwell DAO operates a separate Compound v2 fork ("Moonwell Core") that suffered three oracle-misconfiguration exploits: Oct 2025 (~$1.7M, covered by reserves), Nov 2025 (~$1M, 292 ETH), and Feb 2026 ($1.78M cbETH). Those events did not touch this vault but reflect operator-level risk patterns. | 3 | 3 | Non-Improvable | [P4] [Halborn Nov 2025 incident](https://www.halborn.com/blog/post/explained-the-moonwell-hack-november-2025), [P4] [Feb 2026 cbETH incident](https://blockonomi.com/moonwell-proposes-2-68m-recovery-plan-after-cbeth-liquidation-incident-harms-181-borrowers-on-base/) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No confirmed rug-pull involving Moonwell, Morpho, Block Analitica, or B.Protocol. All teams publicly identified with multi-year on-chain history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Block Analitica](https://blockanalitica.com/), [P1] [Moonwell Foundation Mirror](https://mirror.xyz/moonwellfoundation.eth) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | Current timelock = 345,600s (4 days), well above 24h minimum. No documented timelock reductions in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain `timelock = 345600` via Morpho API |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Moonwell removed its Immunefi bug bounty program in February 2025 (months before the Oct/Nov 2025 and Feb 2026 exploits). Morpho's $2.5M Immunefi bounty does cover MetaMorpho V1 contracts, so the underlying vault code is in scope, but Moonwell's curator/operator layer has no active bounty. | 3 | 9 | **Improvable** | [P4] [Bounty removal context](https://www.ainvest.com/news/moonwell-suffers-1-78m-loss-oracle-misconfiguration-ai-code-vulnerability-2602/), [P1] [Morpho Immunefi](https://immunefi.com/bug-bounty/morpho/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Block Analitica publishes public dashboards monitoring Moonwell vault risk. Moonwell has a Security Council for emergency response. However, no documented real-time monitoring SLA or automated alert-to-pause integration is publicly verifiable for the vault. | 3 | 9 | **Improvable** | [P1] [Block Analitica dashboards](https://blockanalitica.com/), [P1] [Security Council docs](https://docs.moonwell.fi) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Guardian (3-of-5) can revoke pending market cap increases and timelock decreases instantly. Curator can drop supply caps to zero immediately (no timelock on decreases). However, no automated circuit breaker on Public Allocator-driven flows. | 3 | 9 | **Improvable** | [P1] [Morpho roles](https://docs.morpho.org/curate/concepts/roles/), [P0] On-chain guardian = 0xB9d4acf1...AB38 |

**Smart Contract Security Subtotal:**
- Raw scores: 9+9+9+9+9+3+9+9+3+3+3 = 75/99
- Adjusted: (75/99) x 180 = **136.4/180 (75.8%)**

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Vault Owner = Moonwell Temporal Governor (cross-chain Wormhole governance contract, DAO-controlled). Guardian = 3-of-5 Moonwell Security Council Safe. Curator = 2-of-4 Block Analitica/B.Protocol Safe. All addresses verified on-chain via Safe Transaction API. | 9 | 9 | Non-Improvable (optimal) | [P0] [Owner](https://basescan.org/address/0x8b621804a7637b781e2BbD58e256a591F2dF7d51), [P0] [Guardian Safe API](https://safe-transaction-base.safe.global/api/v1/safes/0xB9d4acf113a423Bc4A64110B8738a52E51C2AB38/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Underlying Morpho Blue is immutable; vault contract has no upgrade path. Material parameter changes (new markets, cap increases) require 4-day timelock through Temporal Governor. Curator (2-of-4) can only allocate WITHIN already-enabled markets and decrease caps; cannot route to arbitrary contracts. | 9 | 9 | Non-Improvable (optimal) | [P0] [On-chain timelock = 345600](https://api.morpho.org/graphql), [P1] [Morpho roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Guardian = 3-of-5 Safe (Moonwell Security Council: Gauntlet, Elliot Friedman, Luke Youngblood, X0s0l, Coolhorsegirl — publicly identified, multiple independent individuals). Curator = 2-of-4 Safe (Block Analitica/B.Protocol). Owner = on-chain governance via Temporal Governor. Independent identities verifiable. | 9 | 9 | Non-Improvable (optimal) | [P0] [Guardian Safe = 3-of-5](https://safe-transaction-base.safe.global/api/v1/safes/0xB9d4acf113a423Bc4A64110B8738a52E51C2AB38/), [P1] [Security Council](https://docs.moonwell.fi) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause not available on MetaMorpho V1 — withdrawals are always permissionless. No address-level blocklist. Curator can only decrease caps. Guardian can veto pending governance changes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | 100% of vault assets held in MetaMorpho ERC-4626 contract supplying to immutable Morpho Blue singleton on Base. No off-chain custody. | 9 | 9 | Non-Improvable (optimal) | [P0] [Vault contract on Basescan](https://basescan.org/address/0xa0E430870c4604CcfC7B38Ca7845B1FF653D0ff1) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | User funds (~$8.1M WETH) are isolated in MetaMorpho vault contract. Moonwell Foundation treasury (9.47M USDC, 415.9 wstETH) held in separate Foundation wallets. Curator/Guardian Safes hold no user funds — only signing rights. | 9 | 9 | Non-Improvable (optimal) | [P0] [Vault on-chain](https://basescan.org/address/0xa0E430870c4604CcfC7B38Ca7845B1FF653D0ff1) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | Strictly enforced on-chain: vault can only supply to Morpho Blue markets explicitly added by Curator + timelock. Currently allocated to 7 markets, all on Morpho Blue with WETH as loan asset. New markets require 4-day timelock; Guardian can veto. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain allocation queue (Morpho API), [P1] [Morpho roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Moonwell Security Council exists as 3-of-5 multisig for emergency response. However, no publicly documented tabletop test or signer-replacement runbook for this Curator/Guardian Safe specifically. Block Analitica/B.Protocol incident procedures not publicly documented. | 3 | 9 | **Improvable** | [P1] [Security Council docs](https://docs.moonwell.fi) — describes responsibilities but no tested playbook |

**Key Management Subtotal:**
- Raw scores: 9+9+9+9+9+9+9+3 = 66/72
- Adjusted: (66/72) x 180 = **165.0/180 (91.7%)**

**Security Total: 136.4 + 165.0 = 301.4/360 (83.7%)**

### STRATEGY (30% Weight) -- Score: 236.5/270 (87.6%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | 100% of yield from WETH borrowing interest paid in 7 disclosed Morpho Blue markets (cbETH, wstETH, weETH, rETH, cbBTC, USDC collateral). Fully aligned with stated mandate of "optimized lending in blue-chip collateral markets." Net APY ~1.92%. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain allocation data; [P1] [Vault description](https://app.morpho.org/base/vault/0xa0E430870c4604CcfC7B38Ca7845B1FF653D0ff1/moonwell-flagship-eth) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss requires (a) bad debt in a Morpho Blue market due to oracle failure or fast collateral depeg, or (b) market-wide LST depeg of wstETH/weETH/cbETH lasting beyond liquidation thresholds (LLTV 94.5%). Fee drag (15%) reduces but never inverts yield in normal conditions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho security considerations](https://docs.morpho.org/curate/concepts/security-considerations/) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage at vault level. The vault supplies WETH 1:1 to Morpho Blue markets. Effective leverage = 1.0x. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain allocation |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A — vault is a supplier, not a borrower. Liquidation risk applies to borrowers in underlying Morpho Blue markets (who borrow WETH against LST collateral); their liquidation supports vault solvency rather than threatens it. | N/A | N/A | N/A | Question applies to leveraged strategies |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | Moonwell Flagship vaults have operated since June 2024 with no negative-yield event for the ETH vault. The MetaMorpho strategy template has been used by 500+ vaults; ~15 vaults with high-risk long-tail collateral suffered bad debt in the Resolv USR exploit (March 2026), but blue-chip vaults including this one were unaffected. | 9 | 9 | Non-Improvable (optimal) | [P4] [Resolv impact analysis](https://www.panewslab.com/en/articles/019d18ac-26dc-74d5-8f5d-56771dc1a43e); [P1] [Vault history on Morpho](https://app.morpho.org/base/vault/0xa0E430870c4604CcfC7B38Ca7845B1FF653D0ff1/moonwell-flagship-eth) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Block Analitica publishes risk methodology and per-vault dashboards. Monthly recaps posted on Moonwell forum. Quantitative supply caps and LLTV documented per market. However, no single canonical risk framework document with hard quantitative limits is published. | 3 | 9 | **Improvable** | [P1] [Block Analitica](https://blockanalitica.com/), [P2] [Forum monthly recaps](https://forum.moonwell.fi/t/block-analitica-b-protocol-moonwell-flagship-vaults-monthly-recap-october-2024/1372) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yield is 100% organic from borrower interest on Morpho Blue markets. Moonwell does run a WELL incentive program for some vaults, but the base yield (~1.92% net APY) is independent of emissions. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain Net APY = 1.92% from API |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Withdrawals are instant when idle liquidity sufficient. ~91% of TVL is in wstETH and weETH markets which have very deep secondary markets on Base. Under stress, withdrawals may queue if Morpho Blue markets are at high utilization — but assets unwind 1:1 (no slippage), not at a discount. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho V1 design](https://docs.morpho.org/learn/concepts/vault/) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Yield is borrower interest, not a carry or spread trade. Cannot invert to negative in any market regime. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain yield source |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Public Allocator status not confirmed enabled for this vault, but if enabled it would allow permissionless reallocation within Curator-set flow caps. New market additions and cap increases still require 4-day timelock + Guardian veto. No flash-loanable vault takeover. | 3 | 9 | **Improvable** | [P1] [Public Allocator security considerations](https://docs.morpho.org/curate/concepts/security-considerations/) |

**Protocol Mechanics Subtotal:**
- Raw scores: 9+9+9+N/A+9+3+9+9+9+3 = 69/81
- Adjusted: (69/81) x 45 = **38.3/45 (85.2%)**

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Borrowers post: wstETH (~79% of TVL exposure), weETH (~12%), cbETH (~7%), rETH (~1%), cbBTC (~0.5%), USDC (~0.2%). All are blue-chip large-cap assets with established peg history. LLTV is 94.5% for major LSTs, 91.5% for cbBTC, 86% for USDC. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain allocation via Morpho API |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | Major LSTs (wstETH, weETH, cbETH, rETH) all maintained <2% deviation through 2024-2026 stress events. weETH had brief deviations in mid-2024 but recovered within hours. cbBTC has maintained tight peg to BTC since Coinbase launched it. | 9 | 9 | Non-Improvable (optimal) | [P3] DefiLlama price history, [P4] LST market data |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A — the vault is a WETH supplier. Slashing risk on wstETH/weETH/cbETH/rETH is borne by borrowers; if their LST collateral loses value from slashing, they get liquidated and the vault receives WETH back. | N/A | N/A | N/A | LST risk borne by borrowers, not supplier |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | Vault asset is WETH on Base (canonical Base bridge for ETH = native L2 bridge with fraud proofs/rollup design). No third-party bridged assets. cbBTC is custodial-wrapped BTC issued by Coinbase. cbETH is LST issued natively on Base. weETH is bridged from Ethereum (LayerZero/EigenLayer-managed). Total non-native-or-canonical-bridge exposure (weETH only) is ~12% of TVL — well within Low threshold. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain market data; [P1] [weETH bridging](https://docs.morpho.org) |

**Collateral Subtotal:**
- Raw scores: 9+9+N/A+9 = 27/27
- Adjusted: (27/27) x 45 = **45.0/45 (100%)**

#### Infra Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Base (Tier-2 chain), Morpho Blue (Tier-0 protocol), Chainlink oracles (Tier-0), Safe multisig infra (Tier-0), Wormhole bridge for Moonwell governance (Tier-2). All disclosed and reputable. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain dependencies |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | All 7 markets use ChainlinkOracleV2 adapters (verified on Morpho API). Chainlink (Tier-0) is the primary feed. No hardcoded prices. Markets can be removed by Curator with 4-day timelock; oracles per market are fixed at market creation (immutable Morpho Blue design) — if oracle fails, supply cap can be dropped instantly but oracle cannot be swapped, so curator must migrate to a new market. | 3 | 3 | Non-Improvable | [P0] On-chain oracle types via Morpho API; [P1] [Morpho oracle design](https://github.com/morpho-org/morpho-blue-oracles) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | No critical off-chain providers in the fund flow. Allocation can be triggered via Block Analitica's keeper but vault operates correctly without any off-chain component. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho V1 design](https://docs.morpho.org/learn/concepts/vault/) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Base has had brief congestion events (Nov 2023 launch issues, Jul 2024 sequencer pause <1h) but no incidents preventing on-chain withdrawals. Morpho Blue has had no outages. Chainlink feeds remained operational through stress events on Base. | 9 | 9 | Non-Improvable (optimal) | [P3] [L2Beat Base stats](https://l2beat.com/scaling/projects/base), [P1] Morpho status |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Base: brief sequencer pause September 5, 2023 (~1h) — pre-vault deployment. No halts >30min in last 12 months affecting normal operations. | 9 | 9 | Non-Improvable (optimal) | [P3] [L2Beat Base](https://l2beat.com/scaling/projects/base) |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A — vault is a WETH supplier; slashing risk borne by borrowers in LST markets. | N/A | N/A | N/A | LST risk borne by borrowers |
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
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Vault deploys 100% to Morpho Blue (Tier-0 protocol). Borrowers post collateral from Coinbase (cbETH, cbBTC), Lido (wstETH), Ether.fi (weETH), Rocket Pool (rETH), Circle (USDC). All Tier-0/1 venues. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain markets; [P1] [Morpho ecosystem](https://docs.morpho.org) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Curator fee = 15% of vault interest, paid to Block Analitica/B.Protocol Safe. Moonwell DAO and Foundation receive performance fees per governance proposal. Documented but exact revenue-share split between Block Analitica and B.Protocol not publicly itemized. | 3 | 9 | **Improvable** | [P0] On-chain `fee = 0.15` via Morpho API; [P2] [Forum vault listing](https://forum.morpho.org/t/block-analitica-b-protocol-flagship-eth-and-usdc-metamorpho-vaults-whitelisting/372) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Each Morpho Blue market has an on-chain supply cap set by Curator (e.g., wstETH/WETH market cap = 30,000 WETH). Cap increases require 4-day timelock. Curator can decrease caps instantly. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain supply caps via Morpho API |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Vault redeems from Morpho Blue markets in real-time when idle liquidity exists. If full unwind needed and markets are at high utilization, curator can drop caps to force borrowers to repay; otherwise users wait for natural repayment or partial exits. No discretionary approvals needed. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho V1 docs](https://docs.morpho.org/curate/concepts/security-considerations/) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Curators (Block Analitica + B.Protocol) and Guardian (Moonwell Security Council) named publicly with on-chain Safe addresses. Owner (Temporal Governor) and DAO-controlled. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain addresses via Safe API; [P1] [Moonwell vault docs](https://docs.moonwell.fi/moonwell/moonwell-overview/vaults) |

**Protocol Counterparty Subtotal:**
- Raw scores: 9+3+9+9+9 = 39/45
- Adjusted: (39/45) x 45 = **39.0/45 (86.7%)**

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless ERC-4626 `withdraw()` and `redeem()`. No pause function on MetaMorpho V1. No address-level blocking. Available liquidity = idle WETH + repayments in underlying markets. | 9 | 9 | Non-Improvable (optimal) | [P0] [Vault contract](https://basescan.org/address/0xa0E430870c4604CcfC7B38Ca7845B1FF653D0ff1) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Vault TVL ~$8.1M is small relative to Morpho Blue WETH market liquidity on Base (>$50M aggregate). Withdrawals can absorb >10% of TVL instantly. Full unwind possible within hours under normal utilization. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain TVL + market liquidity |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No documented withdrawal delays for Moonwell Flagship ETH since inception (June 2024). | 9 | 9 | Non-Improvable (optimal) | [P3] On-chain history; [P2] Block Analitica monthly recaps |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | No caps on withdrawals themselves. Withdrawals are limited only by available liquidity in underlying markets. Curator can decrease supply caps to drive repayments, but this is recovery action not restriction. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho roles](https://docs.morpho.org/curate/concepts/roles/) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | March 2026 USR depeg event and Oct 2024 BTC crash both saw Morpho Blue continue serving withdrawals normally on Base. Flagship ETH unaffected. Vault is too small to test multi-hundred-million-dollar stress directly. | 9 | 9 | Non-Improvable (optimal) | [P2] [USR incident impact summary](https://www.panewslab.com/en/articles/019d18ac-26dc-74d5-8f5d-56771dc1a43e) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Vault holds liquid WETH (idle or supplied to immediate-repayment Morpho markets). No unstaking queue. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain asset = WETH |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Primary redemption is in-protocol (vault burn share -> WETH). Secondary mwETH market is small but unnecessary for exits. | 9 | 9 | Non-Improvable (optimal) | [P0] Vault ERC-4626 redeem path |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | mwETH receipt token has <$10M secondary market depth. WETH on Base has deep liquidity (>$500M aggregate DEX TVL). Primary redemption sufficient — secondary market is optional. | 3 | 3 | Non-Improvable | [P3] [DefiLlama Base TVL](https://defillama.com/protocol/morpho) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | If all 7 underlying markets simultaneously hit 100% utilization, withdrawals queue until borrowers repay. Borrowing rates spike steeply at high utilization (Morpho Blue IRM design), incentivizing repayment. No expected permanent haircuts. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho IRM design](https://docs.morpho.org) |

**Liquidity Subtotal:**
- Raw scores: 9+9+9+9+9+9+9+3+9 = 75/81
- Adjusted: (75/81) x 45 = **41.7/45 (92.6%)**

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | mwETH is a yield-bearing ERC-4626 share, not a pegged token — it accrues value (>1.0 WETH per share). No peg to maintain. | N/A | N/A | N/A | Vault share is yield-bearing not pegged |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Vault is non-leveraged WETH lender. ETH price moves don't affect vault solvency (vault denominated in WETH). Only catastrophic LST depeg or oracle failure in underlying market would cause loss. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain exposure |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Morpho Blue IRM curves are kinked at 90% utilization with sharp rate spikes thereafter. No history of sustained 100% utilization in this vault's markets. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho IRM](https://docs.morpho.org) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Block Analitica publishes risk assessments and stress tests on their dashboards. Specific public stress-test reports for Moonwell Flagship ETH not separately published (covered in monthly recaps at high level). | 3 | 9 | **Improvable** | [P1] [Block Analitica](https://blockanalitica.com/), [P2] [Monthly recaps](https://forum.moonwell.fi/t/block-analitica-b-protocol-moonwell-flagship-vaults-monthly-recap-october-2024/1372) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Vault has no leveraged position. Underlying markets have 94.5% LLTV; if LST falls vs WETH by more than ~5.5% suddenly, liquidations occur and vault receives bonus. Tail risk = LST depeg + thin liquidator response. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain LLTV; [P1] Morpho design |

**Market Subtotal:**
- Raw scores: N/A+9+9+3+9 = 30/36
- Adjusted: (30/36) x 45 = **37.5/45 (83.3%)**

**Strategy Total: 38.3 + 45.0 + 35.0 + 39.0 + 41.7 + 37.5 = 236.5/270**

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
| O-TL-07 | Are major investors or strategic partners disclosed? | Original Moonbeam Foundation grant publicly documented. Partnerships with Morpho Labs, Block Analitica, B.Protocol, Coinbase (cbETH/cbBTC), and Wormhole disclosed. | 9 | 9 | Non-Improvable (optimal) | [P1] [Moonwell partnerships](https://docs.moonwell.fi) |
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
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | ERC-4626 vault on immutable Morpho Blue — assets and liabilities continuously verifiable on-chain via `totalAssets()` and share supply. Block Analitica dashboard shows real-time allocations. | 9 | 9 | Non-Improvable (optimal) | [P0] [Vault contract](https://basescan.org/address/0xa0E430870c4604CcfC7B38Ca7845B1FF653D0ff1); [P1] [Block Analitica](https://blockanalitica.com/) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | mwETH vault verified on BaseScan. Morpho Blue verified. Safe contracts verified. All key infrastructure verified. | 9 | 9 | Non-Improvable (optimal) | [P0] [BaseScan verified](https://basescan.org/address/0xa0E430870c4604CcfC7B38Ca7845B1FF653D0ff1#code) |

**Documentation Subtotal:**
- Raw scores: 9+9+9+9+9+9 = 54/54
- Adjusted: (54/54) x 67.5 = **67.5/67.5 (100%)**

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Moonwell Foundation treasury (9.47M USDC, 415.9 wstETH) historically used to cover Moonwell Core losses (e.g., $2.68M cbETH recovery plan Feb 2026, $1.7M Oct 2025 reserve coverage). No dedicated safety module for Morpho vaults specifically, but Foundation has demonstrated willingness to cover losses. | 3 | 9 | **Improvable** | [P1] [Moonwell Foundation](https://mirror.xyz/moonwellfoundation.eth); [P4] [cbETH recovery plan](https://blockonomi.com/moonwell-proposes-2-68m-recovery-plan-after-cbeth-liquidation-incident-harms-181-borrowers-on-base/) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Foundation treasury: 9.47M USDC + 415.9 wstETH (~$915k at ETH ~$2,200) = ~$10.4M liquid, plus WELL/MFAM tokens (~$4M+ at current prices). Total Moonwell TVL across products ~$65.57M (DefiLlama). Liquid treasury / TVL = ~16% (well above 5% threshold). Treasury / this vault TVL ($8.1M) = ~128%. | 9 | 9 | Non-Improvable (optimal) | [P3] [DefiLlama Moonwell TVL $65.57M](https://defillama.com/protocol/moonwell); [P1] [Moonwell Foundation treasury](https://mirror.xyz/moonwellfoundation.eth) |
| O-FR-03 | What is the estimated operational runway at current burn? | Foundation maintains 9.47M USDC and 415.9 wstETH. Moonwell annualized fees $1.76M, revenue $448K (DefiLlama). At reasonable burn assumptions (~$2-3M/year for Foundation operations), liquid runway exceeds 3 years. | 9 | 9 | Non-Improvable (optimal) | [P1] [Moonwell Foundation](https://mirror.xyz/moonwellfoundation.eth); [P3] [DefiLlama revenue data](https://defillama.com/protocol/moonwell) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | Moonwell Flagship ETH vault TVL has held steady through Oct 2025, Nov 2025, Feb 2026 Moonwell Core incidents and the March 2026 Resolv crisis on Morpho. Foundation treasury used to cover Moonwell Core losses ($2.68M cbETH recovery). mwETH token has limited external composability surface. | 9 | 9 | Non-Improvable (optimal) | [P3] On-chain TVL history; [P4] Incident recoveries |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | If Moonwell Foundation, Block Analitica, B.Protocol all disappear: Morpho Blue is immutable, vault contract is immutable, withdrawals continue permissionlessly. No curator means no new market additions but existing positions repay normally and users can exit. Underlying Morpho contract has no admin. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Blue immutable](https://morpho.org/blog/morpho-blue-and-how-it-enables-our-vision-for-defi-lending/) |

**Financial Resilience Subtotal:**
- Raw scores: 3+9+9+9+9 = 39/45
- Adjusted: (39/45) x 67.5 = **58.5/67.5 (86.7%)**

**Operations Total: 56.25 + 52.5 + 67.5 + 58.5 = 234.75/270**

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 75 | 99 | 136.4 | 180 | 75.8% |
| | Key Management (8 Q) | 66 | 72 | 165.0 | 180 | 91.7% |
| | **Security Subtotal** | | | **301.4** | **360** | **83.7%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 69 | 81 | 38.3 | 45 | 85.2% |
| | Collateral (3 of 4 Q scored) | 27 | 27 | 45.0 | 45 | 100.0% |
| | Infra Counterparty (6 of 11 Q scored) | 42 | 54 | 35.0 | 45 | 77.8% |
| | Protocol Counterparty (5 Q) | 39 | 45 | 39.0 | 45 | 86.7% |
| | Liquidity (9 Q) | 75 | 81 | 41.7 | 45 | 92.6% |
| | Market (4 of 5 Q scored) | 30 | 36 | 37.5 | 45 | 83.3% |
| | **Strategy Subtotal** | | | **236.5** | **270** | **87.6%** |
| **Operations** | Governance (4 Q) | 30 | 36 | 56.3 | 67.5 | 83.3% |
| | Team & Legal (9 Q) | 63 | 81 | 52.5 | 67.5 | 77.8% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 39 | 45 | 58.5 | 67.5 | 86.7% |
| | **Operations Subtotal** | | | **234.8** | **270** | **86.9%** |
| **TOTAL** | | | | **772.6** | **900** | **85.8%** |

---

