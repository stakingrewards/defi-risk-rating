# Ondo Finance - USDY Risk Rating

**Rating Date**: 2026-03-13
**Final Grade**: CCC+
**Total Score**: 581.4/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v1.0-alpha

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 205.7/360 (57.1%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 8+ independent audits: Spearbit (Mar 2025), Halborn (Feb 2025), Code4rena (Mar 2024, Sep 2023, Jan 2023), Cyfrin (Apr 2024), Nethermind (Apr 2023), Zokyo (Aug 2023). All core USDY contracts covered. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/audits; [P1] https://code4rena.com/reports/2024-03-ondo-finance; [P1] https://code4rena.com/reports/2023-09-ondo; [P0] https://github.com/ondoprotocol/usdy |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent: Spearbit (Mar 2025), operating through Cantina (Tier-0). Also Code4rena (Tier-0), Cyfrin (Tier-1), Halborn (Tier-1), Nethermind (Tier-1). Multiple Tier-0/1 auditors. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/audits; Spearbit/Cantina Tier-0; Code4rena Tier-0 |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Spearbit (Mar 2025) and Halborn (Feb 2025) are the most recent. Current implementation at 0xea0f7ee... deployed post-audit. No evidence of unaudited post-audit upgrades. | 9 | 9 | Non-Improvable (optimal) | [P0] Implementation: 0xea0f7eebdc2ae40edfe33bf03d332f8a7f617528 (verified on-chain); [P1] Spearbit Mar 2025 |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | C4A Jan 2023 found 1 High and 5 Medium. Subsequent audits (C4A Sep 2023, Cyfrin Apr 2024, Halborn Feb 2025, Spearbit Mar 2025) provide remediation coverage. Cyfrin report states findings addressed. | 9 | 9 | Non-Improvable (optimal) | [P1] https://code4rena.com/reports/2023-01-ondo; [P1] https://docs.ondo.finance/pdf/Ondo-Cyfrin-Audit-April-2024.pdf |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | USDY uses OZ TransparentUpgradeableProxy. ProxyAdmin (0x3ed616...) owned by 4-of-7 Safe (0x1a694a...). No on-chain timelock. Upgrades require 4/7 multisig but execute immediately. No public upgrade policy. | 1 | 9 | **Improvable** | [P0] ProxyAdmin: 0x3ed61633057da0bc58f84b2b9002845e56f94c19; [P0] Owner: 4-of-7 Safe at 0x1a694a... (verified via RPC eth_call) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit or critical bug in 2.5 years of operation (since Aug 2023). No incidents on Rekt.news, CertiK Skynet, or on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] No suspicious transactions on Etherscan; [P1] https://skynet.certik.com/projects/ondofinance |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No confirmed rug-pull. SEC investigation closed Nov 2025 without charges. Team publicly identified. VC-backed ($24M from Founders Fund, Pantera, Coinbase). | 9 | 9 | Non-Improvable (optimal) | [P2] https://genfinity.io/2025/12/08/sec-closes-ondo-finance-investigation-no-charges/ |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No on-chain timelock exists to reduce. No reduction event occurred. Absence of timelock penalized in S-SC-05. | 9 | 9 | Non-Improvable | [P0] No timelock contract associated with USDY ProxyAdmin on-chain |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active Immunefi bounty: max payout $250K for critical smart contract bugs, min $25K for criticals. Covers USDY across multiple chains. Immunefi Standard Badge. | 9 | 9 | Non-Improvable (optimal) | [P1] https://immunefi.com/bug-bounty/ondofinance/; max $250K, USDC on Ethereum |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | No public evidence of specific real-time on-chain monitoring (Hypernative, Blockaid) for USDY contracts. Ondo mentions "information security audits" generally but no details on 24/7 monitoring or on-call response. | 1 | 9 | **Source Missing** | [P1] https://docs.ondo.finance/trust-and-security -- mentions security audits but not monitoring details |
| S-SC-11 | Are automatic safety controls (e.g. pause, circuit breakers) triggered by monitoring alerts? | USDY has ERC20 pause capability (PAUSER_ROLE). Oracle has built-in constraints: MAX_ABSOLUTE_DIFF_BPS=200 (2%), MAX_CHANGE_DIFF_BPS=74 (0.74%), MIN_PRICE_UPDATE_WINDOW=23h. These provide price manipulation protection but pause is manual, not automatic. | 3 | 9 | **Improvable** | [P0] USDY.sol: ERC20PresetMinterPauserUpgradeable; [P0] RWAOracleExternalComparisonCheck.sol: MAX_ABSOLUTE_DIFF_BPS=200 |

**Smart Contract Security Subtotal:**
- Raw scores: 9+9+9+9+1+9+9+9+9+1+3 = 77/99
- Adjusted: (77/99) x 180 = **140.0/180 (77.8%)**

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | DEFAULT_ADMIN_ROLE held by 4-of-7 Safe (0x1a694a...). ProxyAdmin also owned by this Safe. Management Multisig (0xaed4ca...) is separate 4-of-7 Safe for operational roles. Both verified on-chain. Signer identities not publicly disclosed. | 3 | 9 | **Source Missing** | [P0] DEFAULT_ADMIN: 0x1a694a09494e214a3be3652e4b343b7b81a73ad7 (4-of-7, verified); [P0] Management: 0xaed4caf2e535d964165b4392342f71bac77e8367 (4-of-7, verified) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No single key can move funds or upgrade. ProxyAdmin owner is 4-of-7 Safe. Minting requires MINTER_ROLE granted by DEFAULT_ADMIN (4-of-7). Threshold >= 3 AND signers >= 5 met. However, no timelock >= 24h for upgrades. | 3 | 9 | **Improvable** | [P0] ProxyAdmin owner: 4-of-7 Safe (threshold=4, owners=7, verified via RPC); no timelock |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | 4-of-7 threshold exceeds 3-of-5 requirement. Two multisigs share 6/7 signers. Signer identities not disclosed -- independence unverifiable. Per framework, unverifiable independence caps at Mid (3). | 3 | 9 | **Source Missing** | [P0] ProxyAdmin owner: 7 owners, threshold 4; Management: 7 owners, threshold 4; 6/7 overlap; no identity disclosure |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | USDY enforces allowlist (KYC), blocklist, sanctions list on all transfers. Admin can add/remove from lists. PAUSER_ROLE can pause globally. BURNER_ROLE can burn from any address. Broad controls required by securities compliance. Require multisig but broadly scoped. | 3 | 3 | Non-Improvable | [P0] USDY.sol: _beforeTokenTransfer checks all lists; BURNER_ROLE can burn any address; securities compliance |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | No. 100% of underlying assets (T-bills, bank deposits) held off-chain by Morgan Stanley Smith Barney LLC and in bank demand deposit accounts. USDY tokens represent claims against Ondo USDY LLC SPV. | 1 | 1 | Non-Improvable | [P1] https://app.rwa.xyz/assets/USDY: Morgan Stanley custodian; [P1] Ondo docs: off-chain custody |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Ondo USDY LLC is bankruptcy-remote SPV with: independent director, separate bank accounts, separate accounting/tax records, no co-mingling with Ondo Finance Inc. Legal opinion affirms non-consolidation. Ankura Trust holds first-priority security interest. | 9 | 9 | Non-Improvable (optimal) | [P1] https://blog.ondo.finance/protecting-investors-what-happens-if-ondo-goes-bankrupt/; [P1] https://docs.ondo.finance/general-access-products/usdy/faq/trust-and-transparency |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A. USDY is not a vault deploying into DeFi protocols. Underlying assets are T-bills and bank deposits at traditional custodians. | N/A | N/A | N/A | Fund invests in T-bills and bank deposits only |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No public evidence of a documented incident playbook for admin-key compromise or signer loss. No tabletop exercises or key-rotation procedures publicly disclosed. | 1 | 9 | **Source Missing** | [P1] https://docs.ondo.finance/trust-and-security -- no incident playbook details found |

**Key Management Subtotal (7 scored, 1 N/A):**
- Raw scores: 3+3+3+3+1+9+1 = 23/63
- Adjusted: (23/63) x 180 = **65.7/180 (36.5%)**

**Security Total: 140.0 + 65.7 = 205.7/360 (57.1%)**

---

### STRATEGY (30% Weight) -- Score: 230.0/270 (85.2%)

#### Protocol Mechanics (5%) - 40.7/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | 100% of yield from US Treasury interest and bank deposit interest. Fully organic, aligned with stated mandate of providing "yield to the global on-chain economy." No token emissions, incentives, or leverage. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/general-access-products/usdy/basics; [P3] https://app.rwa.xyz/assets/USDY |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Negative yield limited to extreme tail: (1) federal funds rate dropping below management fee (~0.15-0.35%), requiring near-zero rate policy; (2) US Treasury default (unprecedented). Short-duration T-bill portfolio has minimal interest rate risk. | 9 | 9 | Non-Improvable (optimal) | [P1] Fund invests in short-term T-bills and bank deposits; management fee 0.15-0.35% |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage or rehypothecation. 103%+ overcollateralization enforced. Effective leverage is 1.0x (actually <1.0x given overcollateralization). | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/general-access-products/usdy/faq/trust-and-transparency: 103%+ overcollateralization |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A. Not a lending protocol; no LTV ratios, collateral, or liquidation mechanics. | N/A | N/A | N/A | - |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | N/A. Not applicable per Vault product type modifier (applies to Lending only). | N/A | N/A | N/A | - |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Partial framework: 103% overcollateralization requirement enforced quarterly, Ankura Trust daily verification, investment limited to T-bills and bank deposits. But no formal published quantitative risk framework with explicit concentration limits, drawdown thresholds, or change-control procedures. | 3 | 9 | **Improvable** | [P1] https://docs.ondo.finance/general-access-products/usdy/faq/trust-and-transparency; offering document terms |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | 100% organic from US Treasury/bank deposit interest. Zero dependence on incentives, emissions, or token rewards. Yield tracks federal funds rate minus fees. Sustainable economic model. | 9 | 9 | Non-Improvable (optimal) | [P1] Yield ~4% APY tracking Fed rate; [P3] https://app.rwa.xyz/assets/USDY |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes. Underlying T-bills and bank demand deposits are among the most liquid instruments globally. Entire portfolio unwinds within days with near-zero price impact. | 9 | 9 | Non-Improvable (optimal) | [P1] T-bill market depth >$25T; bank demand deposits available on-demand |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. Yield comes directly from US Treasury and bank deposit interest rates. No carry trade, peg dependency, or funding rate arbitrage. | 9 | 9 | Non-Improvable (optimal) | [P1] Direct T-bill/bank deposit ownership |

**PM Subtotal (7 scored, 2 N/A): 9+9+9+3+9+9+9 = 57/63 -> (57/63) x 45 = 40.7**

#### Collateral (5%) - 45.0/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | USDY is backed by short-term US Treasury bills (AAA-rated by all major agencies), iShares Short Treasury Bond ETF shares, and bank demand deposits at FDIC-insured institutions. Highest-quality assets globally. 103%+ overcollateralization. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/general-access-products/usdy/basics; [P1] Ankura daily reports |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | US T-bills are the ultimate safe-haven asset; they appreciate during crises. USDY has maintained expected NAV trajectory since Aug 2023. Overcollateralization buffer never breached per Ankura verification. | 9 | 9 | Non-Improvable (optimal) | [P1] Ankura Trust daily verification reports; [P3] https://app.rwa.xyz/assets/USDY |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A. No staking-based collateral. | N/A | N/A | N/A | - |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | On Ethereum (primary chain), USDY is a native ERC-20 token. Cross-chain deployments use LayerZero OFT standard (burn-and-mint, not wrapped). Underlying T-bill assets are not bridged. 0% bridged on primary chain. | 9 | 9 | Non-Improvable (optimal) | [P0] Etherscan: native ERC-20; [P1] LayerZero OFT burn-and-mint model |

**C Subtotal (3 scored, 1 N/A): 9+9+9 = 27/27 -> (27/27) x 45 = 45.0**

#### Infra Counterparty Exposures (5%) - 30.0/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum (Tier-0), LayerZero bridge (Tier-1), custom Ondo RWA Oracle with Chainlink SHV comparison check (Chainlink Tier-0 as reference), Coinbase Prime (custodian wallets), Morgan Stanley (off-chain custodian). All dependencies disclosed. Oracle is Ondo-controlled (SETTER_ROLE) with Chainlink as sanity check -- not purely Tier-0/1 oracle. | 3 | 9 | **Improvable** | [P0] RWAOracleExternalComparisonCheck: Chainlink comparison; [P1] LayerZero Tier-1; [P0] Ethereum Tier-0 |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | Oracle: Ondo-controlled primary with Chainlink SHV as comparison (single primary provider, partial fallback). Bridge: LayerZero Tier-1 with Ondo custom DVN. Oracle has built-in constraints (MAX_ABSOLUTE_DIFF_BPS=200). Operational 2.5 years without issues. | 3 | 9 | **Improvable** | [P0] Oracle code: Chainlink comparison check; [P1] LayerZero integration; [P1] Ondo custom DVN |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Yes. Morgan Stanley: SEC-registered, FINRA-regulated broker-dealer. Coinbase: SOC 2 Type II certified. Ankura Trust: regulated trust company. All critical off-chain providers are institutional-grade with standard certifications. | 9 | 9 | Non-Improvable (optimal) | [P1] Morgan Stanley FINRA registration; [P1] Coinbase SOC 2; [P1] Ankura Trust regulated |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | USDY operational since Aug 2023 (~2.5 years). No reported infrastructure failures. Ethereum no significant halt. LayerZero no exploits. Deployed >= 6 months with no incidents. | 9 | 9 | Non-Improvable (optimal) | [P0] Continuous operations on Etherscan since Aug 2023; no incidents found |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Ethereum has not experienced a chain halt > 30 minutes in the last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P0] Ethereum continuous block production |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A. No staking-based collateral. | N/A | N/A | N/A | - |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A. No proprietary validator set. | N/A | N/A | N/A | - |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | Ondo (SETTER_ROLE, minting/redemption processing) is a critical single point of failure for token operations. If Ondo's operational systems fail, oracle updates, minting, and redemptions all halt. However, underlying assets at Morgan Stanley are independent. Ankura Trust can take control per collateral agreement. Single failure delays but does not permanently block recovery. | 3 | 3 | Non-Improvable | [P0] SETTER_ROLE required for oracle; [P1] Ondo sole operator for minting/redemption; Ankura Trust as fallback |

**IC Subtotal (6 scored, 2 N/A): 3+3+9+9+9+3 = 36/54 -> (36/54) x 45 = 30.0**

#### Protocol Counterparty Exposures (5%) - 45.0/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Assets deployed into US T-bills (via Morgan Stanley), iShares Short Treasury Bond ETF, and FDIC-insured bank demand deposits. Standard institutional financial infrastructure. No DeFi protocol deployment. | 9 | 9 | Non-Improvable (optimal) | [P1] Ondo docs: T-bills, bank deposits; [P1] https://app.rwa.xyz/assets/USDY |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Management fee (~0.15-0.35%) disclosed. Ondo USDY LLC earns fees from the spread between T-bill yields and USDY yield. Standard institutional arrangement with aligned incentives. | 9 | 9 | Non-Improvable (optimal) | [P1] Fee disclosed in offering docs; [P3] RWA.xyz fee data |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Investment limited to US Treasuries, iShares Short Treasury Bond ETF, and bank deposits. 103% overcollateralization enforced. Concentration governed by offering memorandum terms and Ankura Trust oversight. | 9 | 9 | Non-Improvable (optimal) | [P1] Offering terms; [P1] Ankura Trust daily verification |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | US T-bills trade in a $25T+ market. Bank demand deposits available on-demand. iShares SHV ETF highly liquid. Portfolio can unwind within 1-2 business days. | 9 | 9 | Non-Improvable (optimal) | [P1] T-bill market depth; demand deposit liquidity |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | All fully disclosed: Morgan Stanley Smith Barney LLC (custodian), Ankura Trust (collateral agent/verification agent), Coinbase Prime (deposit address), BitGo and Zodia Custody (additional custody support). | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/general-access-products/usdy/faq/trust-and-transparency; [P1] https://blog.ondo.finance/bitgo-extends-custody-support-for-ousg-usdy/ |

**PC Subtotal (5 scored): 9+9+9+9+9 = 45/45 -> (45/45) x 45 = 45.0**

#### Liquidity (5%) - 36.3/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Redemptions processed through Ondo off-chain (fiat wire transfers). Admin can pause transfers globally (PAUSER_ROLE) and selectively block addresses (blocklist). Allowlist restricts to KYC-approved addresses only. 40-50 day initial minting delay. Withdrawals rely on off-chain approval and can be selectively blocked. | 1 | 1 | Non-Improvable | [P1] https://docs.ondo.finance/general-access-products/usdy/faq/investing-and-redeeming; [P0] USDY.sol: allowlist/blocklist/sanctions checks |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Yes. Stated withdrawal time is 5 business days. Underlying T-bills and bank deposits are the most liquid instruments globally. For $1.5B TVL, the underlying can easily be liquidated within the stated period. | 9 | 9 | Non-Improvable (optimal) | [P1] T-bill market >$25T; demand deposits instant; 5 business day processing |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No reported delays, queues, or freezes in 2.5 years of operation. No public complaints found. USDY TVL grew from $0 to ~$1.5B with continuous operations. | 9 | 9 | Non-Improvable (optimal) | [P0] No delay reports found; continuous operations since Aug 2023 |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | No formal redemption caps beyond $250 minimum. No gates, no withdrawal limits. All redemptions processed within stated 5 business day window per offering terms. | 9 | 9 | Non-Improvable (optimal) | [P1] $250 minimum redemption; no caps documented |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Off-chain redemption operates independently of blockchain congestion. T-bill underlying benefits during volatility (flight to safety). Primary exit route (direct Ondo redemption) unaffected by on-chain conditions. Secondary market thin but not the primary exit path. | 9 | 9 | Non-Improvable (optimal) | [P1] Off-chain redemption independent of on-chain; T-bill flight-to-safety |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. T-bills mature within days-to-weeks. Bank demand deposits available on-demand. No unstaking, vesting, or bridge delays for underlying assets. 5 business day stated period covers full processing. | 9 | 9 | Non-Improvable (optimal) | [P1] Short-term T-bills; demand deposits |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary redemption through Ondo directly (fiat wire). Secondary market optional. DEX volume ~$2M daily is thin but primary exit does not depend on it. | 9 | 9 | Non-Improvable (optimal) | [P1] Direct redemption through Ondo; secondary market optional |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | Underlying collateral (T-bills) has virtually unlimited depth. USDY token secondary market is thin: ~$2M daily volume, ~$4.3M DEX liquidity on Solana. For $1.5B TVL, secondary market absorbs <1% of TVL. | 3 | 9 | **Improvable** | [P3] CoinGecko: ~$2M daily volume; [P3] DEX liquidity ~$4.3M |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | N/A. No lending utilization mechanic. All assets are liquid T-bills and bank deposits with no leverage. If all holders redeemed simultaneously, underlying assets could be liquidated within days. | N/A | N/A | N/A | - |

**L Subtotal (8 scored, 1 N/A): 1+9+9+9+9+9+9+3 = 58/72 -> (58/72) x 45 = 36.3**

#### Market (5%) - 33.0/45

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | USDY is an accumulating token (not pegged to $1). Reference value is the oracle redemption price. CoinGecko shows ATL of $0.9342 (Jan 2024) when oracle price was ~$1.00-1.01 -- >6% secondary market discount early in product life (4 months old, thin liquidity). Since then, price has tracked NAV closely. The Jan 2024 deviation was a thin-market artifact but exceeded 2% threshold. | 3 | 9 | **Improvable** | [P3] CoinGecko: ATL $0.9342 Jan 2024; [P0] Oracle price monotonically increasing; thin early market |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Zero crypto-directional exposure. 100% US Treasuries, bank deposits, and iShares SHV ETF. Crypto drawdowns have no impact on underlying NAV. | 9 | 9 | Non-Improvable (optimal) | [P1] Fund mandate: 100% T-bills, bank deposits, iShares SHV |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yield tracks federal funds rate minus management fee. No utilization curve, no incentive model, no reflexive dynamics. Rate is purely exogenous (set by Fed policy). | 9 | 9 | Non-Improvable (optimal) | [P1] T-bill interest rate tracks Fed policy |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | No public evidence of formal high-volatility scenario testing for USDY. The underlying strategy (short-term T-bills) is inherently low-volatility, limiting relevance. However, no published stress test documentation. | 3 | 9 | **Improvable** | [P1] No stress testing documentation found; inherently low-vol strategy |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | No. No leverage, no liquidation mechanics. US T-bills cannot be liquidated. 1.0x effective leverage with 103%+ overcollateralization. | 9 | 9 | Non-Improvable (optimal) | [P1] Zero leverage; 103%+ overcollateralization |

**M Subtotal (5 scored): 3+9+9+3+9 = 33/45 -> (33/45) x 45 = 33.0**

**Strategy Total: 40.7 + 45.0 + 30.0 + 45.0 + 36.3 + 33.0 = 230.0/270 (85.2%)**

---

### OPERATIONS (30% Weight) -- Score: 145.7/270 (54.0%)

#### Governance (7.5%) - 22.5/67.5

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | USDY controlled by Ondo team multisig (4-of-7 Safe). ONDO token governance exists (Compound Governor Bravo fork) but primarily governs Flux Finance, not USDY directly. No on-chain governance for USDY contract changes. Team multisig can change/upgrade core contracts unilaterally. | 3 | 9 | **Improvable** | [P0] Multisig control verified on-chain; [P1] https://docs.ondo.foundation/ondo-dao -- Ondo DAO governs Flux |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A. No governance token controls USDY. ONDO token governs Flux Finance, not USDY operations. Pure multisig governance for USDY. | N/A | N/A | N/A | - |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | No on-chain timelock for USDY. Off-chain: USDY LLC corporate governance, independent director requirement, Ankura Trust oversight, offering memorandum terms. No advance notice mechanism for on-chain changes. | 3 | 9 | **Improvable** | [P0] No timelock on-chain; [P1] USDY LLC governance structure |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A. Not a vault with replaceable strategy manager. Investment mandate governed by USDY LLC offering terms. | N/A | N/A | N/A | - |

**G Subtotal (2 scored, 2 N/A): 3+3 = 6/18 -> (6/18) x 67.5 = 22.5**

#### Team & Legal & Compliance (7.5%) - 48.2/67.5

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Nathan Allman (CEO): ex-Goldman Sachs, Stanford MBA, Brown BA. Pinku Surana: co-founder. Full team page at ondo.finance/team. Ondo Finance Inc (Delaware). Acquired Oasis Pro Markets (SEC-registered broker-dealer). SEC-registered investment advisor. | 9 | 9 | Non-Improvable (optimal) | [P1] https://ondo.finance/team; [P1] LinkedIn: Nathan Allman; [P1] Oasis Pro Markets acquisition |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Team growing (~50-100+ employees). Acquired Oasis Pro Markets (additional staff). Engineering depth demonstrated by multi-chain deployment. Some key-person risk around Nathan Allman. Partial redundancy. | 3 | 9 | **Improvable** | [P1] Team page; Oasis Pro acquisition; [P4] hiring activity |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Ondo USDY LLC (Delaware SPV). Ondo Finance Inc (Delaware). Oasis Pro Markets LLC (SEC-registered broker-dealer). Clear jurisdictions and legal structure disclosed. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/general-access-products/usdy/faq/eligibility; Delaware entities |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | SEC investigation (Oct 2023 - Nov 2025) closed without charges. No other known enforcement actions. Ondo registered as investment advisor. Oasis Pro Markets SEC-registered. | 9 | 9 | Non-Improvable (optimal) | [P2] https://genfinity.io/2025/12/08/sec-closes-ondo-finance-investigation-no-charges/; [P1] SEC registrations |
| O-TL-05 | Is there an on-call and incident response process for core teams? | No public evidence of documented 24/7 on-call or incident runbooks. Ondo has a global team but no explicit SLAs, escalation procedures, or response commitments disclosed. | 3 | 9 | **Improvable** | [P1] No on-call documentation found; global team implied |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Support available via support@ondo.finance and through the app. No formal SLA on response times. Ondo's Discord and documentation provide self-service support. Response quality not independently verified. | 3 | 9 | **Improvable** | [P1] support@ondo.finance; Discord community; no SLA |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Founders Fund, Pantera Capital, Coinbase Ventures, Tiger Global, Wintermute, GoldenTree Asset Management, Flow Traders all disclosed. Total $24M raised. | 9 | 9 | Non-Improvable (optimal) | [P1] https://ondo.finance/blog/ondo-raises-20m-in-series-a-investment-round-led-by-founders-fund-and-pantera-capital |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | N/A. Not a vault with external strategy manager. | N/A | N/A | N/A | - |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | N/A. Not a vault with external strategy manager. | N/A | N/A | N/A | - |

**TL Subtotal (7 scored, 2 N/A): 9+3+9+9+3+3+9 = 45/63 -> (45/63) x 67.5 = 48.2**

#### Documentation & Transparency (7.5%) - 52.5/67.5

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Comprehensive documentation at docs.ondo.finance: USDY basics, technology FAQ, trust & transparency, investing & redeeming, smart contract addresses, audits. GitHub repo public. Updated with each chain expansion. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/general-access-products/usdy/basics; [P1] https://github.com/ondoprotocol/usdy |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Documentation explains: USDC -> Coinbase Prime -> T-bills/bank deposits via Morgan Stanley. Loss scenarios: issuer default, custodian failure, smart contract exploit. 103% overcollateralization documented. Ankura Trust daily verification. | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/general-access-products/usdy/faq/trust-and-transparency |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Addresses at docs.ondo.finance/addresses. Lists USDY token across chains, managers, oracles. But does not list ProxyAdmin address, implementation addresses, or role-holder addresses. Spread across chains without comprehensive proxy/implementation mapping. | 3 | 9 | **Improvable** | [P1] https://docs.ondo.finance/addresses; missing ProxyAdmin, implementation, role details |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Roles visible in source code (MINTER_ROLE, BURNER_ROLE, PAUSER_ROLE, LIST_CONFIGURER_ROLE). Multisig addresses labeled on Etherscan. But no central registry of role assignments, no change log, no documentation mapping addresses to roles. | 3 | 9 | **Improvable** | [P0] Roles in USDY.sol source; [P0] Etherscan labels; no central role registry |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Ankura Trust provides daily verification reports on USDY reserves. Monthly reports also published. First-priority security interest structure. 103%+ overcollateralization verified daily. Proof-of-liabilities N/A (no borrowing). | 9 | 9 | Non-Improvable (optimal) | [P1] https://docs.ondo.finance/general-access-products/usdy/faq/trust-and-transparency; Ankura daily reports |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. USDY proxy (0x96F6eF...) verified on Etherscan with Solidity v0.8.16 source code. Implementation (0xea0f7e...) verified. USDY Manager (0x25A103...) verified. Oracle (0xa0219a...) verified. | 9 | 9 | Non-Improvable (optimal) | [P0] https://etherscan.io/address/0x96F6eF951840721AdBF46Ac996b59E0235CB985C |

**DT Subtotal (6 scored): 9+9+3+3+9+9 = 42/54 -> (42/54) x 67.5 = 52.5**

#### Financial Resilience (7.5%) - 22.5/67.5

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Ondo USDY LLC is bankruptcy-remote SPV. Ankura Trust is collateral agent with legal right to take control of assets upon defined "events of default." 103%+ overcollateralization provides structural buffer. However, this is an off-chain legal backstop, not an on-chain safety module with binding automatic activation. | 3 | 9 | **Improvable** | [P1] https://docs.ondo.finance/general-access-products/usdy/faq/trust-and-transparency; Ankura Trust collateral agreement |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Overcollateralization buffer: ~3%+ of $1.5B TVL = ~$45M. Ondo Finance Inc: $24M in VC funding plus ONDO token revenues (~$4-9M annual management fees). No DeFiLlama treasury data. Combined backstop roughly $70M, ~4.6% of USDY TVL. Holdings include VC cash and overcollateralization (mostly T-bills = liquid). Falls in 1-5% range. | 3 | 3 | Non-Improvable | [P3] No DeFiLlama treasury data; [P1] $24M VC funding; ~3% overcollateralization buffer |
| O-FR-03 | What is the estimated operational runway at current burn? | Ondo earns ~0.15-0.35% management fee on ~$2.7B TVL = ~$4-9M annual revenue. $24M VC funding. Runway appears >12 months but specific burn rate and costs not disclosed. Assumption-dependent. | 3 | 9 | **Improvable** | [P1] Management fee disclosed; [P1] $24M VC; specific costs not disclosed |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | USDY TVL grew from $0 to $1.5B over 2.5 years. No stress-related issues. No depositor haircuts or emergency dilution. Growth trajectory positive. But no documented stress test and no major redemption wave tested. Untested protocol on resilience questions scores Mid. | 3 | 9 | **Improvable** | [P3] DeFiLlama TVL data; no stress documentation published |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | If Ondo team disappeared: token transfers could continue (if not paused). But oracle updates stop (SETTER_ROLE needed), minting/redemption halts. Ankura Trust can take control per collateral agreement (off-chain legal process). Users could transfer on secondary market but cannot redeem for fiat without Ondo. Off-chain dependencies critical. | 3 | 3 | Non-Improvable | [P0] SETTER_ROLE needed for oracle; [P1] Ondo sole operator for redemptions; [P1] Ankura Trust fallback |

**FR Subtotal (5 scored): 3+3+3+3+3 = 15/45 -> (15/45) x 67.5 = 22.5**

**Operations Total: 22.5 + 48.2 + 52.5 + 22.5 = 145.7/270 (54.0%)**

---

## Final Score Calculation

| Category | Subcategory | Questions | Scored | N/A | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|--------|-----|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security | 11 | 11 | 0 | 77 | 99 | 140.0 | 180 | 77.8% |
| | Key Management | 8 | 7 | 1 | 23 | 63 | 65.7 | 180 | 36.5% |
| | **Security Subtotal** | **19** | **18** | **1** | | | **205.7** | **360** | **57.1%** |
| **Strategy** | Protocol Mechanics (7 of 9 Q scored) | 9 | 7 | 2 | 57 | 63 | 40.7 | 45 | 90.5% |
| | Collateral (3 of 4 Q scored) | 4 | 3 | 1 | 27 | 27 | 45.0 | 45 | 100.0% |
| | Infra Counterparty (6 of 8 Q scored) | 8 | 6 | 2 | 36 | 54 | 30.0 | 45 | 66.7% |
| | Protocol Counterparty (5 Q) | 5 | 5 | 0 | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity (8 of 9 Q scored) | 9 | 8 | 1 | 58 | 72 | 36.3 | 45 | 80.6% |
| | Market (5 Q) | 5 | 5 | 0 | 33 | 45 | 33.0 | 45 | 73.3% |
| | **Strategy Subtotal** | **40** | **34** | **6** | | | **230.0** | **270** | **85.2%** |
| **Operations** | Governance (2 of 4 Q scored) | 4 | 2 | 2 | 6 | 18 | 22.5 | 67.5 | 33.3% |
| | Team & Legal (7 of 9 Q scored) | 9 | 7 | 2 | 45 | 63 | 48.2 | 67.5 | 71.4% |
| | Documentation (6 Q) | 6 | 6 | 0 | 42 | 54 | 52.5 | 67.5 | 77.8% |
| | Financial Resilience (5 Q) | 5 | 5 | 0 | 15 | 45 | 22.5 | 67.5 | 33.3% |
| | **Operations Subtotal** | **24** | **20** | **4** | | | **145.7** | **270** | **54.0%** |
| **TOTAL** | | **83** | **72** | **11** | | | **581.4** | **900** | **64.6%** |

---
