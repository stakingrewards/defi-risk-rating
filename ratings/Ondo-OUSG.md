# Ondo Finance - OUSG Risk Rating

**Rating Date**: 2026-03-13
**Final Grade**: CCC+
**Total Score**: 587.4/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v1.0-alpha

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 205.7/360 (57.1%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 8+ independent audits: Spearbit (Mar 2025), Halborn (Feb 2025), Code4rena (Mar 2024, Sep 2023, Jan 2023), Cyfrin (Apr 2024), Nethermind (Apr 2023), Zokyo (Aug 2023). Mar 2024 C4A specifically covered OUSG contracts (ousgInstantManager, rOUSG). All core contracts covered. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/audits; [P1] https://code4rena.com/reports/2024-03-ondo-finance; [P1] https://github.com/code-423n4/2024-03-ondo-finance |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent: Spearbit (Mar 2025), operating through Cantina (Tier-0). Also Code4rena (Tier-0), Cyfrin (Tier-1), Halborn (Tier-1), Nethermind (Tier-1). Multiple Tier-0/1 auditors. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/audits; Spearbit/Cantina Tier-0; Code4rena Tier-0 |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Spearbit (Mar 2025) and Halborn (Feb 2025) are the most recent. OUSG implementation at 0x1ceb44b6... deployed post-audit. OUSG Instant Manager 2 (0x93358db7...) deployed after Mar 2024 C4A audit. | 9 | 9 | Non-Improvable (optimal) | [P0] OUSG Implementation: 0x1ceb44b6e515abf009e0ccb6ddafd723886cf3ff (verified on-chain); [P1] Spearbit Mar 2025 |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | C4A Jan 2023 found 1 High and 5 Medium. C4A Mar 2024 OUSG-specific audit found issues around USDC depeg assumption in OUSGInstantManager -- Ondo confirmed adding Chainlink USDC/USD oracle as mitigation. Subsequent audits (Halborn Feb 2025, Spearbit Mar 2025) provide remediation coverage. | 9 | 9 | Non-Improvable (optimal) | [P1] https://code4rena.com/reports/2024-03-ondo-finance; [P1] https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/278 |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | OUSG uses OZ TransparentUpgradeableProxy. ProxyAdmin (0xba80aa44...) owned by 4-of-7 Safe (0xaed4ca...). No on-chain timelock. Upgrades require 4/7 multisig but execute immediately. No public upgrade policy. | 1 | 9 | **Improvable** | [P0] ProxyAdmin: 0xba80aa44cc25e85cc30359150dfb1c7d041cf6d5; [P0] Owner: 4-of-7 Safe at 0xaed4ca... (verified via RPC getThreshold=4, getOwners=7) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit or critical bug in 3+ years of OUSG operation (since Jan 2023). No incidents on Rekt.news, CertiK Skynet, or on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] No suspicious transactions on Etherscan; [P1] https://immunefi.com/bug-bounty/ondofinance/ |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No confirmed rug-pull. SEC investigation closed Nov 2025 without charges. Team publicly identified. VC-backed ($24M from Founders Fund, Pantera, Coinbase). | 9 | 9 | Non-Improvable (optimal) | [P2] SEC investigation closure Nov 2025 |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No on-chain timelock exists to reduce. No reduction event occurred. Absence of timelock penalized in S-SC-05. | 9 | 9 | Non-Improvable | [P0] No timelock contract associated with OUSG ProxyAdmin on-chain |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active Immunefi bounty: max payout $250K for critical smart contract bugs. Covers OUSG across multiple chains. Immunefi Standard Badge. | 9 | 9 | Non-Improvable (optimal) | [P1] https://immunefi.com/bug-bounty/ondofinance/ |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | No public evidence of specific real-time on-chain monitoring (Hypernative, Blockaid) for OUSG contracts. Ondo mentions "information security audits" generally but no details on 24/7 monitoring or on-call response. | 1 | 9 | **Source Missing** | [P1] https://docs.ondo.finance/trust-and-security -- mentions security audits but not monitoring details |
| S-SC-11 | Are automatic safety controls (e.g. pause, circuit breakers) triggered by monitoring alerts? | OUSG has ERC20 pause capability (PAUSER_ROLE). OUSGInstantManager has rate limits ($50M global/24h mint and redeem). Oracle has built-in constraints: MAX_ABSOLUTE_DIFF_BPS and MAX_CHANGE_DIFF_BPS for price manipulation protection. But pause is manual, not automatic. | 3 | 9 | **Improvable** | [P0] OUSG.sol: pause capability; [P0] OUSGInstantManager: InstantMintTimeBasedRateLimiter; [P1] https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol |

**Smart Contract Security Subtotal:**
- Raw scores: 9+9+9+9+1+9+9+9+9+1+3 = 77/99
- Adjusted: (77/99) x 180 = **140.0/180 (77.8%)**

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | OUSG ProxyAdmin (0xba80aa44...) owned by 4-of-7 Safe (0xaed4ca..., Management Multisig). Same multisig holds operational roles. 6/7 signers overlap with the USDY ProxyAdmin owner multisig (0x1a694a...). Signer identities not publicly disclosed. | 3 | 9 | **Source Missing** | [P0] ProxyAdmin owner: 0xaed4caf2e535d964165b4392342f71bac77e8367 (4-of-7, verified via RPC); [P0] 6/7 signer overlap with USDY multisig confirmed |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No single key can move funds or upgrade. ProxyAdmin owner is 4-of-7 Safe. Minting requires MINTER_ROLE granted by admin multisig. Threshold >= 3 AND signers >= 5 met. However, no timelock >= 24h for upgrades. | 3 | 9 | **Improvable** | [P0] ProxyAdmin owner: 4-of-7 Safe (threshold=4, owners=7, verified via RPC); no timelock |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | 4-of-7 threshold exceeds 3-of-5 requirement. Signer identities not disclosed -- independence unverifiable. Per framework, unverifiable independence caps at Mid (3). | 3 | 9 | **Source Missing** | [P0] ProxyAdmin owner: 7 owners, threshold 4; no identity disclosure |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | OUSG enforces KYC registry (allowlist), blocklist, and sanctions list on all transfers. Admin can add/remove from lists. PAUSER_ROLE can pause globally. BURNER_ROLE can burn from any address. Broad controls required by securities compliance. Require multisig but broadly scoped. | 3 | 3 | Non-Improvable | [P0] OUSG source: _beforeTokenTransfer checks KYC registry, blocklist, sanctions; BURNER_ROLE; securities compliance |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | No. 100% of underlying assets held off-chain -- primarily in BlackRock BUIDL fund shares, plus allocations in Fidelity, Franklin Templeton, WisdomTree funds, and bank deposits. Clear Street LLC serves as prime broker. OUSG tokens represent LP interests in Ondo I LP. | 1 | 1 | Non-Improvable | [P1] https://docs.ondo.finance/qualified-access-products/ousg/overview; [P3] https://app.rwa.xyz/assets/OUSG |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Ondo I LP is a separate legal entity (Delaware LP) with segregated accounts. Clear Street holds fund assets separately. GP/LP structure provides legal segregation. Ankura Trust daily verification of reserves. | 9 | 9 | Non-Improvable (optimal) | [P1] Ondo I LP fund structure; [P2] https://forum.arbitrum.foundation/t/ondo-finance-ondo-i-lp-ousg-step-application/23594 |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A. OUSG is not a vault deploying into DeFi protocols. Underlying assets are fund shares (BUIDL, Fidelity, etc.) and bank deposits at traditional custodians. | N/A | N/A | N/A | Fund invests in money market fund shares and bank deposits only |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No public evidence of a documented incident playbook for admin-key compromise or signer loss. No tabletop exercises or key-rotation procedures publicly disclosed. | 1 | 9 | **Source Missing** | [P1] https://docs.ondo.finance/trust-and-security -- no incident playbook details found |

**Key Management Subtotal (7 scored, 1 N/A):**
- Raw scores: 3+3+3+3+1+9+1 = 23/63
- Adjusted: (23/63) x 180 = **65.7/180 (36.5%)**

**Security Total: 140.0 + 65.7 = 205.7/360 (57.1%)**

---

### STRATEGY (30% Weight) -- Score: 236.0/270 (87.4%)

#### Protocol Mechanics (5%) - 40.7/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | 100% of yield from underlying fund distributions (BlackRock BUIDL, Fidelity, Franklin Templeton, WisdomTree fund returns) which themselves invest in US Treasuries and repos. Fully organic, aligned with OUSG's stated mandate as a short-term US government bond fund. No token emissions or leverage. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/qualified-access-products/ousg/overview; [P1] https://docs.ondo.finance/qualified-access-products/ousg/yield |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Negative yield limited to extreme tail: (1) federal funds rate dropping below combined management fees (~0.15% OUSG + underlying fund fees), requiring near-zero rate policy; (2) US Treasury default (unprecedented); (3) BlackRock BUIDL fund failure (extremely unlikely given BlackRock's scale). Short-duration portfolio has minimal interest rate risk. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/qualified-access-products/ousg/fees-and-taxes: 0.15% management fee |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage or rehypothecation. OUSG holds fund shares and bank deposits. Effective leverage is 1.0x. Underlying funds (BUIDL etc.) invest in short-term T-bills and repos without leverage. | 9 | 9 | Non-Improvable (optimal) | [P1] Fund invests in money market fund shares; no leverage |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A. Not a lending protocol; no LTV ratios, collateral, or liquidation mechanics. | N/A | N/A | N/A | - |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | N/A. Not applicable per Vault product type modifier (applies to Lending only). | N/A | N/A | N/A | - |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Partial framework: investment limited to funds from leading asset managers (BlackRock, Fidelity, Franklin Templeton, WisdomTree). Ankura Trust daily verification. But no formal published quantitative risk framework with explicit concentration limits per underlying fund, drawdown thresholds, or change-control procedures. | 3 | 9 | **Improvable** | [P1] https://docs.ondo.finance/qualified-access-products/ousg/overview; [P2] Arbitrum STEP application |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | 100% organic from underlying fund distributions (US Treasury interest). Zero dependence on incentives or token rewards. Yield tracks federal funds rate minus combined fees. 0.15% management fee waived until July 2026. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/qualified-access-products/ousg/fees-and-taxes; [P3] https://app.rwa.xyz/assets/OUSG |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes. Underlying fund shares (primarily BUIDL) are designed for instant redemption. T-bill-backed money market funds are among the most liquid instruments globally. Entire portfolio unwinds within hours to days with near-zero price impact. | 9 | 9 | Non-Improvable (optimal) | [P1] BUIDL instant settlement; T-bill market depth >$25T |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. Yield comes from US Treasury interest transmitted through underlying fund shares. No carry trade, peg dependency, or funding rate arbitrage. | 9 | 9 | Non-Improvable (optimal) | [P1] Direct fund share ownership; US Treasury-backed |

**PM Subtotal (7 scored, 2 N/A): 9+9+9+3+9+9+9 = 57/63 -> (57/63) x 45 = 40.7**

#### Collateral (5%) - 45.0/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | OUSG is backed by BlackRock BUIDL (itself backed by US T-bills, repos, and cash -- BlackRock is the world's largest asset manager), plus fund shares from Fidelity, Franklin Templeton, WisdomTree, and FundBridge Capital, along with bank deposits and USDC. All are institutional-grade money market instruments with minimal credit risk. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/qualified-access-products/ousg/overview; [P3] https://app.rwa.xyz/assets/OUSG |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | Underlying BUIDL maintains $1.00 per share with daily accrual. US T-bill-backed money market funds are flight-to-safety instruments that benefit during crises. OUSG NAV has tracked expected trajectory since Jan 2023. No deviations. OUSG price on CoinGecko shows monotonic increase from ATL $95.09 (Mar 2023 at launch) to current $114.57. | 9 | 9 | Non-Improvable (optimal) | [P3] CoinGecko OUSG: ATL $95.09 at launch, monotonically increasing; [P1] Ankura daily verification |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A. No staking-based collateral. | N/A | N/A | N/A | - |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | On Ethereum (primary chain), OUSG is a native ERC-20 token. Underlying assets are off-chain fund shares (not bridged). OUSG uses LayerZero OFT for cross-chain (burn-and-mint, not wrapped). 0% bridged on primary chain. | 9 | 9 | Non-Improvable (optimal) | [P0] Etherscan: native ERC-20; [P1] LayerZero OFT model |

**C Subtotal (3 scored, 1 N/A): 9+9+9 = 27/27 -> (27/27) x 45 = 45.0**

#### Infra Counterparty Exposures (5%) - 30.0/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum (Tier-0), LayerZero bridge (Tier-1), custom Ondo RWA Oracle with Chainlink SHV comparison check (Chainlink Tier-0 as reference), Coinbase (USDC conversion), Clear Street LLC (prime broker). All dependencies disclosed. Oracle is Ondo-controlled (SETTER_ROLE) with Chainlink as sanity check -- not purely Tier-0/1. | 3 | 9 | **Improvable** | [P0] RWAOracleExternalComparisonCheck; [P1] LayerZero Tier-1; [P0] Ethereum Tier-0 |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | Oracle: Ondo-controlled primary with Chainlink SHV as comparison (single primary provider, partial fallback). Bridge: LayerZero Tier-1 with Ondo custom DVN. Oracle has built-in constraints (MAX_ABSOLUTE_DIFF_BPS). Operational 3+ years without issues. | 3 | 9 | **Improvable** | [P0] Oracle code: Chainlink comparison check; [P1] LayerZero integration |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Yes. Clear Street LLC: FINRA/SIPC member broker-dealer, SEC-regulated. Coinbase: SOC 2 Type II certified. Ankura Trust: regulated trust company. BlackRock: world's largest asset manager, fully regulated. All critical off-chain providers are institutional-grade. | 9 | 9 | Non-Improvable (optimal) | [P1] Clear Street FINRA BrokerCheck CRD#288933; [P1] Coinbase SOC 2; [P1] BlackRock regulated |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | OUSG operational since Jan 2023 (~3+ years). No reported infrastructure failures. Ethereum no significant halt. LayerZero no exploits. BUIDL integration (Mar 2024) functioning smoothly. Deployed >= 6 months with no incidents. | 9 | 9 | Non-Improvable (optimal) | [P0] Continuous operations on Etherscan since Jan 2023; no incidents found |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Ethereum has not experienced a chain halt > 30 minutes in the last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P0] Ethereum continuous block production |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A. No staking-based collateral. | N/A | N/A | N/A | - |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A. No proprietary validator set. | N/A | N/A | N/A | - |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | Ondo (SETTER_ROLE, minting/redemption processing) is a critical single point of failure for token operations. However, OUSG has the OUSGInstantManager which provides 24/7 instant USDC redemption via BUIDL integration, reducing reliance on manual processing. If Ondo's systems fail, oracle updates and new minting halt, but instant redemption may continue until USDC reserves deplete. Ankura Trust can take control per agreement. | 3 | 3 | Non-Improvable | [P0] SETTER_ROLE required for oracle; [P1] OUSGInstantManager provides instant path; Ankura Trust fallback |

**IC Subtotal (6 scored, 2 N/A): 3+3+9+9+9+3 = 36/54 -> (36/54) x 45 = 30.0**

#### Protocol Counterparty Exposures (5%) - 45.0/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Assets deployed into BlackRock BUIDL (primary), Fidelity, Franklin Templeton (FOBXX), WisdomTree, FundBridge Capital money market funds, and bank deposits. All Tier-0/1 institutional venues. No DeFi protocol deployment. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/qualified-access-products/ousg/overview; [P3] https://app.rwa.xyz/assets/OUSG |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Management fee 0.15% disclosed (waived until July 2026). Underlying fund fees borne by funds themselves. Standard institutional arrangement with aligned incentives. Fee structure transparent. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/qualified-access-products/ousg/fees-and-taxes |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Investment limited to specific named institutional funds (BlackRock BUIDL, Fidelity, Franklin Templeton, WisdomTree, FundBridge). Concentration governed by fund mandate and Ankura Trust oversight. Majority in BUIDL. | 9 | 9 | Non-Improvable (optimal) | [P1] Fund mandate; [P1] Ankura daily verification |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | BlackRock BUIDL provides instant on-chain redemption for USDC. Other money market fund shares can be liquidated within 1-2 business days. Bank deposits available on-demand. Portfolio can unwind within hours to days. | 9 | 9 | Non-Improvable (optimal) | [P1] BUIDL instant settlement; [P1] Money market fund liquidity |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | All fully disclosed: Clear Street LLC (prime broker, FINRA/SIPC member), BlackRock (BUIDL fund manager), Ankura Trust (verification agent), Coinbase (USDC conversion), Fidelity, Franklin Templeton, WisdomTree (underlying fund managers). | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/qualified-access-products/ousg/overview; [P1] Clear Street FINRA CRD#288933 |

**PC Subtotal (5 scored): 9+9+9+9+9 = 45/45 -> (45/45) x 45 = 45.0**

#### Liquidity (5%) - 36.3/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | OUSG offers two redemption paths: (1) Instant 24/7 via OUSGInstantManager with USDC ($50M global/24h, $25M individual/24h); (2) Non-instant via Ondo (T+1 with 4PM ET cutoff, min $50K). Admin can pause transfers globally (PAUSER_ROLE) and selectively block addresses (KYC registry, blocklist). Allowlist restricts to KYC-approved only. Instant path is permissionless within rate limits; non-instant requires off-chain processing. | 3 | 3 | Non-Improvable | [P1] https://docs.ondo.finance/qualified-access-products/ousg/instant-limits; [P0] OUSGInstantManager contract |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Yes. OUSG instant redemption limited to $50M/day globally. For $723M TVL, full redemption via instant path takes ~15 days. However, underlying BUIDL and money market funds can be liquidated rapidly. Non-instant T+1 path processes larger amounts. Combined paths provide credible near-total exit within weeks. | 9 | 9 | Non-Improvable (optimal) | [P1] $50M/day instant limit; BUIDL instant settlement; T+1 non-instant |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No reported delays, queues, or freezes in 3+ years of OUSG operation. No public complaints found. Instant redemption functioning since March 2024. | 9 | 9 | Non-Improvable (optimal) | [P0] No delay reports found; continuous operations since Jan 2023 |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Instant redemption caps: $50M global/24h, $25M individual/24h. These reset daily. Non-instant minimum $50K. Caps sized so meaningful share of TVL (~7% daily via instant) can exit on schedule. Non-instant path (T+1) supplements for larger amounts. No history of caps blocking exits. Caps are transparent, documented, and governed. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/qualified-access-products/ousg/instant-limits; $50M/24h global cap; non-instant supplement |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Instant redemption via OUSGInstantManager relies on on-chain USDC reserves in the contract; this could be depleted during high-demand periods. Non-instant redemption operates independently of blockchain congestion. Underlying T-bill-backed funds benefit during volatility (flight to safety). Primary instant path is an improvement over USDY's 5-day processing but could face USDC depletion under stress. | 9 | 9 | Non-Improvable (optimal) | [P1] Instant redemption via on-chain contract; off-chain non-instant path independent of on-chain conditions |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Underlying fund shares (BUIDL) provide instant settlement. Other money market funds settle within 1-2 business days. No unstaking, vesting, or bridge delays. | 9 | 9 | Non-Improvable (optimal) | [P1] BUIDL instant; money market fund T+1 |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary redemption through OUSGInstantManager (instant, on-chain) and non-instant (Ondo direct). Secondary market is essentially non-existent -- CoinGecko reports $0 24h trading volume. However, primary exit does not depend on secondary market at all. | 9 | 9 | Non-Improvable (optimal) | [P3] CoinGecko: $0 trading volume; [P1] Direct redemption via OUSGInstantManager |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | Underlying collateral (BUIDL, money market fund shares) has deep institutional liquidity. OUSG token secondary market is essentially non-existent: $0 daily volume on CoinGecko. For $723M market cap, secondary market absorbs 0% of TVL. Direct instant redemption path ($50M/day) provides the exit but this question evaluates market depth specifically. | 1 | 9 | **Improvable** | [P3] CoinGecko: $0 daily OUSG volume; no DEX pairs; secondary market depth effectively zero |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | N/A. No lending utilization mechanic. OUSG instant redemption capped at $50M/day, which creates a natural queue. If all $723M holders redeemed simultaneously, instant path queues for ~15 days while non-instant path processes larger amounts. Underlying BUIDL and money market funds can be liquidated rapidly. No leverage. | N/A | N/A | N/A | - |

**L Subtotal (8 scored, 1 N/A): 3+9+9+9+9+9+9+1 = 58/72 -> (58/72) x 45 = 36.3**

#### Market (5%) - 39.0/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | OUSG is an accumulating token (not pegged to $1). Reference value is the oracle NAV price. CoinGecko shows ATL of $95.09 (Mar 2023 at launch) -- this was the initial NAV, not a depeg. OUSG price has increased monotonically from ~$95 to ~$114.57 as yield accrues. No secondary market stress events because there is essentially no secondary market. Since there is no meaningful secondary market trading, peg performance cannot be evaluated under stress. However, the instant redemption mechanism at NAV (via OUSGInstantManager) effectively anchors value. Score 9 because NAV tracking has been consistent and direct redemption prevents dislocation. | 9 | 9 | Non-Improvable (optimal) | [P3] CoinGecko OUSG: monotonic price increase from $95.09 to $114.57; [P0] OUSGInstantManager provides NAV-based redemption |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Zero crypto-directional exposure. 100% fund shares backed by US Treasuries, repos, and cash. Crypto drawdowns have no impact on underlying NAV. | 9 | 9 | Non-Improvable (optimal) | [P1] Fund mandate: 100% money market fund shares backed by T-bills |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yield tracks federal funds rate minus management fees. No utilization curve, no incentive model, no reflexive dynamics. Rate is purely exogenous (set by Fed policy through underlying fund returns). | 9 | 9 | Non-Improvable (optimal) | [P1] T-bill interest rate tracks Fed policy |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | No public evidence of formal high-volatility scenario testing for OUSG. The underlying strategy (short-term money market funds) is inherently low-volatility, limiting relevance. However, no published stress test documentation. | 3 | 9 | **Improvable** | [P1] No stress testing documentation found |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | No. No leverage, no liquidation mechanics. Fund shares in BUIDL and money market funds cannot be liquidated. 1.0x effective leverage. | 9 | 9 | Non-Improvable (optimal) | [P1] Zero leverage; money market fund shares |

**M Subtotal (5 scored): 9+9+9+3+9 = 39/45 -> (39/45) x 45 = 39.0**

**Strategy Total: 40.7 + 45.0 + 30.0 + 45.0 + 36.3 + 39.0 = 236.0/270 (87.4%)**

---

### OPERATIONS (30% Weight) -- Score: 145.7/270 (54.0%)

#### Governance (7.5%) - 22.5/67.5

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | OUSG controlled by Ondo team multisig (4-of-7 Safe). ONDO token governance exists (Compound Governor Bravo fork) but governs Flux Finance, not OUSG. No on-chain governance for OUSG contract changes. Team multisig can change/upgrade core contracts unilaterally. | 3 | 9 | **Improvable** | [P0] Multisig control verified on-chain; [P1] https://docs.ondo.foundation/ondo-dao |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A. No governance token controls OUSG. ONDO token governs Flux Finance, not OUSG operations. Pure multisig governance for OUSG. | N/A | N/A | N/A | - |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | No on-chain timelock for OUSG. Off-chain: Ondo I LP partnership agreement, GP fiduciary duties, Ankura Trust oversight. No advance notice mechanism for on-chain changes. | 3 | 9 | **Improvable** | [P0] No timelock on-chain; [P1] GP/LP governance structure |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A. Not a vault with replaceable strategy manager. Investment mandate governed by Ondo I LP partnership terms and GP. | N/A | N/A | N/A | - |

**G Subtotal (2 scored, 2 N/A): 3+3 = 6/18 -> (6/18) x 67.5 = 22.5**

#### Team & Legal & Compliance (7.5%) - 48.2/67.5

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Nathan Allman (CEO): ex-Goldman Sachs, Stanford MBA. Pinku Surana: co-founder. Full team page at ondo.finance/team. Ondo Finance Inc (Delaware). Acquired Oasis Pro Markets (SEC-registered broker-dealer). Ondo Capital Management LLC is SEC-registered investment advisor. | 9 | 9 | Non-Improvable (optimal) | [P1] https://ondo.finance/team; [P1] LinkedIn: Nathan Allman |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Team growing (~50-100+ employees). Acquired Oasis Pro Markets (additional staff). Engineering depth demonstrated by multi-chain deployment and BUIDL integration. Some key-person risk around Nathan Allman. | 3 | 9 | **Improvable** | [P1] Team page; Oasis Pro acquisition |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Ondo I LP (Delaware LP). Ondo I GP LLC (Delaware). Ondo Capital Management LLC (SEC-registered investment advisor, Delaware). Clear jurisdictions and legal structure disclosed. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/qualified-access-products/ousg/overview; [P2] Arbitrum STEP application |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | SEC investigation (Oct 2023 - Nov 2025) closed without charges. No other known enforcement actions. Ondo Capital Management is registered investment advisor. Oasis Pro Markets is SEC-registered broker-dealer. | 9 | 9 | Non-Improvable (optimal) | [P2] SEC investigation closure Nov 2025 |
| O-TL-05 | Is there an on-call and incident response process for core teams? | No public evidence of documented 24/7 on-call or incident runbooks. Ondo has a global team but no explicit SLAs, escalation procedures, or response commitments disclosed. | 3 | 9 | **Improvable** | [P1] No on-call documentation found; global team implied |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Support available via support@ondo.finance and through the app. No formal SLA on response times. Ondo's Discord and documentation provide self-service support. OUSG qualified purchaser base likely receives institutional-grade support. | 3 | 9 | **Improvable** | [P1] support@ondo.finance; Discord community; no SLA |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Founders Fund, Pantera Capital, Coinbase Ventures, Tiger Global, Wintermute, GoldenTree Asset Management, Flow Traders all disclosed. Total $24M+ raised. BlackRock is a key strategic partner (BUIDL integration). | 9 | 9 | Non-Improvable (optimal) | [P1] https://ondo.finance/blog/ondo-raises-20m-in-series-a-investment-round-led-by-founders-fund-and-pantera-capital |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | N/A. Not a vault with external strategy manager. | N/A | N/A | N/A | - |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | N/A. Not a vault with external strategy manager. | N/A | N/A | N/A | - |

**TL Subtotal (7 scored, 2 N/A): 9+3+9+9+3+3+9 = 45/63 -> (45/63) x 67.5 = 48.2**

#### Documentation & Transparency (7.5%) - 52.5/67.5

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Comprehensive documentation at docs.ondo.finance/qualified-access-products/ousg: overview, yield, investing, redeeming, rebasing, technical, eligibility, fees. GitHub repo public (Code4rena). Updated with BUIDL integration and instant redemption feature additions. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/qualified-access-products/ousg/overview; [P1] https://github.com/code-423n4/2024-03-ondo-finance |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Documentation explains: USDC -> fund shares (BUIDL, Fidelity, etc.) -> underlying T-bills/repos. Loss scenarios: underlying fund default, custodian failure, smart contract exploit. Ankura Trust daily verification of reserves. Instant redemption mechanism clearly documented. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/qualified-access-products/ousg/overview; [P1] https://docs.ondo.finance/qualified-access-products/ousg/investing |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Addresses at docs.ondo.finance/addresses. Lists OUSG token, managers, across chains. But does not list ProxyAdmin address (0xba80aa44...), implementation addresses, or role-holder addresses. Missing comprehensive proxy/implementation mapping. | 3 | 9 | **Improvable** | [P1] https://docs.ondo.finance/addresses; missing ProxyAdmin, implementation details |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Roles visible in source code (MINTER_ROLE, BURNER_ROLE, PAUSER_ROLE, KYC registry roles). Multisig addresses identifiable on Etherscan. But no central registry of role assignments, no change log, no documentation mapping addresses to roles. | 3 | 9 | **Improvable** | [P0] Roles in OUSG source; [P0] Etherscan labels; no central role registry |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Ankura Trust provides daily verification reports on OUSG reserves. OUSG Holdings 1 address (0x72Be8C14...) holds verifiable BUIDL tokens on-chain (~$142M visible). Monthly reports also published. Proof-of-liabilities N/A (no borrowing structure). | 9 | 9 | Non-Improvable (optimal) | [P0] https://etherscan.io/address/0x72be8c14b7564f7a61ba2f6b7e50d18dc1d4b63d (BUIDL holdings); [P1] Ankura daily reports |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. OUSG proxy (0x1B19C193...) verified on Etherscan. OUSG Manager (0xF16c188c...) verified. OUSG Instant Manager (0x28269899...) verified. OUSG Instant Manager 2 (0x93358db7...) verified. Implementation contracts verified. | 9 | 9 | Non-Improvable (optimal) | [P0] https://etherscan.io/address/0x1B19C19393e2d034D8Ff31ff34c81252FcBbee92 |

**DT Subtotal (6 scored): 9+9+3+3+9+9 = 42/54 -> (42/54) x 67.5 = 52.5**

#### Financial Resilience (7.5%) - 22.5/67.5

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Ondo I LP has GP/LP fund structure. Ondo Capital Management LLC as investment advisor has fiduciary duties. Ankura Trust is verification agent with daily reporting. But no dedicated on-chain safety module or ring-fenced backstop with binding activation rules for user losses. | 3 | 9 | **Improvable** | [P1] GP/LP fund structure; Ankura Trust oversight; no on-chain safety module |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Same entity as USDY -- Ondo Finance Inc: $24M+ in VC funding plus ONDO token revenues. No DeFiLlama treasury data found. Management fees 0.15% (waived until July 2026). Combined backstop roughly similar to USDY context. Against OUSG's $723M: ~3.3% if counting VC + management fees. However, specific treasury breakdown not disclosed. Falls in 1-5% range. | 3 | 3 | Non-Improvable | [P3] No DeFiLlama treasury data; [P1] $24M VC funding; 0.15% management fee (waived) |
| O-FR-03 | What is the estimated operational runway at current burn? | Ondo earns management fees across $2.7B total TVL = ~$4-9M annual revenue (when fees active). $24M VC funding. OUSG fees waived until July 2026. Runway appears >12 months but specific burn rate not disclosed. Assumption-dependent. | 3 | 9 | **Improvable** | [P1] Fee disclosure; [P1] $24M VC; costs not disclosed |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | OUSG TVL grew from $0 to ~$723M over 3+ years. Successfully transitioned underlying from SHV ETF to BUIDL (Mar 2024) without disruption. No stress-related issues or redemption delays. But no documented major stress test or significant redemption wave tested. Untested resilience on bank-run scenarios. | 3 | 9 | **Improvable** | [P3] CoinGecko market cap data; [P4] No stress events documented |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | If Ondo team disappeared: OUSGInstantManager could continue functioning for instant redemptions as long as USDC reserves remain in the contract and oracle prices are still valid. Oracle updates stop (SETTER_ROLE needed), new minting halts. Ankura Trust and underlying fund managers (BlackRock etc.) operate independently. GP obligations continue under partnership law. Off-chain dependencies critical but BUIDL shares held in disclosed custodial accounts. | 3 | 3 | Non-Improvable | [P0] OUSGInstantManager can function without team for existing USDC reserves; [P1] BUIDL and fund shares held independently |

**FR Subtotal (5 scored): 3+3+3+3+3 = 15/45 -> (15/45) x 67.5 = 22.5**

**Operations Total: 22.5 + 48.2 + 52.5 + 22.5 = 145.7/270 (54.0%)**

---

## Final Score Calculation

| Category | Subcategory | Questions | Scored | N/A | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|--------|-----|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security | 11 | 11 | 0 | 77 | 99 | 140.0 | 180 | 77.8% |
| | Key Management (7 of 8 Q scored) | 8 | 7 | 1 | 23 | 63 | 65.7 | 180 | 36.5% |
| | **Security Subtotal** | **19** | **18** | **1** | | | **205.7** | **360** | **57.1%** |
| **Strategy** | Protocol Mechanics (7 of 9 Q scored) | 9 | 7 | 2 | 57 | 63 | 40.7 | 45 | 90.5% |
| | Collateral (3 of 4 Q scored) | 4 | 3 | 1 | 27 | 27 | 45.0 | 45 | 100.0% |
| | Infra Counterparty (6 of 8 Q scored) | 8 | 6 | 2 | 36 | 54 | 30.0 | 45 | 66.7% |
| | Protocol Counterparty (5 Q) | 5 | 5 | 0 | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity (8 of 9 Q scored) | 9 | 8 | 1 | 58 | 72 | 36.3 | 45 | 80.6% |
| | Market (5 Q) | 5 | 5 | 0 | 39 | 45 | 39.0 | 45 | 86.7% |
| | **Strategy Subtotal** | **40** | **34** | **6** | | | **236.0** | **270** | **87.4%** |
| **Operations** | Governance (2 of 4 Q scored) | 4 | 2 | 2 | 6 | 18 | 22.5 | 67.5 | 33.3% |
| | Team & Legal (7 of 9 Q scored) | 9 | 7 | 2 | 45 | 63 | 48.2 | 67.5 | 71.4% |
| | Documentation (6 Q) | 6 | 6 | 0 | 42 | 54 | 52.5 | 67.5 | 77.8% |
| | Financial Resilience (5 Q) | 5 | 5 | 0 | 15 | 45 | 22.5 | 67.5 | 33.3% |
| | **Operations Subtotal** | **24** | **20** | **4** | | | **145.7** | **270** | **54.0%** |
| **TOTAL** | | **83** | **72** | **11** | | | **587.4** | **900** | **65.3%** |

---
