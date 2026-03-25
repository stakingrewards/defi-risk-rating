# Maple Finance - syrupUSDT Risk Rating

**Rating Date**: 2026-03-17
**Final Grade**: CCC+
**Total Score**: 614.0/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v1.0-alpha

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 271.4/360 (75.4%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. Maple-Core V2 has undergone 7+ audits: Trail of Bits (Dec 2022), Spearbit/Cantina (Dec 2022, Jun 2023), Three Sigma (Dec 2022, Jun 2023, Dec 2023, Aug 2024), 0xMacro (Dec 2023, Aug 2024, Dec 2024), Sherlock (Sep 2025, Nov 2025), Dedaub (Jan 2026), Sigma Prime (Jan 2026). The syrupUSDT pool uses identical core contracts as syrupUSDC, all covered by the same audit program. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security docs](https://docs.maple.finance/technical-resources/security/security); [P1] [Audit repo](https://github.com/maple-labs/maple-v2-audits); [P0] Verified contracts on Etherscan |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent audits (Jan 2026) by Dedaub and Sigma Prime (Tier-0). Nov 2025 by Spearbit (Tier-0) and Sherlock (Tier-0). Multiple Tier-0 auditors in recent history. Trail of Bits (Tier-0) in historical audits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security docs](https://docs.maple.finance/technical-resources/security/security); [P1] [Audit repo](https://github.com/maple-labs/maple-v2-audits) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Every release in the last 12 months has been audited before deployment: Aug 2024 (Three Sigma, 0xMacro), Dec 2024 (Three Sigma, 0xMacro), Sep 2025 (Sherlock, 0xMacro), Nov 2025 (Spearbit, Sherlock), Jan 2026 (Dedaub, Sigma Prime). | 9 | 9 | Non-Improvable (optimal) | [P1] [Security docs](https://docs.maple.finance/technical-resources/security/security) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Per security documentation: "all relevant issues identified by auditors were addressed prior to" each release. Reports publicly available in maple-v2-audits repository. Consistent across all releases. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security docs](https://docs.maple.finance/technical-resources/security/security); [P1] [Audit repo](https://github.com/maple-labs/maple-v2-audits) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Core contracts use MapleProxyFactory proxy pattern. Upgrades require GovernorTimelock (0x2eFFf88...) with MIN_DELAY = 86400 seconds (24h). Only pre-approved upgrade paths via factory validation. Factory allowlisting controlled by Governor. | 9 | 9 | Non-Improvable (optimal) | [P0] GovernorTimelock at [Etherscan](https://etherscan.io/address/0x2eFFf88747EB5a3FF00d4d8d0f0800E306C0426b) (MIN_DELAY = 86400); [P1] [Proxy docs](https://docs.maple.finance/technical-resources/protocol-overview/proxies-and-upgradeability) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | Yes. Orthogonal Trading defaulted $36M (Dec 2022), Babel Finance defaulted $10M (Jul 2022) under V1 undercollateralized lending. Total permanent uncompensated losses: ~$46M. V2 (launched Dec 2022) has zero losses. Per criteria: "High-scoring events (permanent uncompensated loss) are never mitigated by age alone." | 1 | 1 | Non-Improvable | [P4] [CoinDesk](https://www.coindesk.com/markets/2022/12/05/maple-finance-severs-ties-with-orthogonal-trading-alleging-it-misrepresented-financial-position); [P1] [V2 architecture](https://docs.maple.finance/technical-resources/protocol-overview/smart-contract-architecture) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No confirmed rug-pull. The 2022 defaults were borrower defaults, not protocol/team misconduct. Maple pursued legal action against defaulting parties. | 9 | 9 | Non-Improvable (optimal) | [P4] CoinDesk reporting on defaults; [P2] M11 Credit Medium post on Orthogonal Trading |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. GovernorTimelock deployed Sep/Oct 2025 with MIN_DELAY = 86400 (1 day). This was a governance improvement adding formal timelock controls. | 9 | 9 | Non-Improvable (optimal) | [P0] GovernorTimelock at [Etherscan](https://etherscan.io/address/0x2eFFf88747EB5a3FF00d4d8d0f0800E306C0426b) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active Immunefi bug bounty (live since Jan 2022, updated Nov 2025) with max payout $500,000 for critical vulnerabilities. 55 assets in scope. KYC required. | 9 | 9 | Non-Improvable (optimal) | [P1] [Immunefi Maple](https://immunefi.com/bug-bounty/maple/); [P1] [Security docs](https://docs.maple.finance/technical-resources/security/security) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. "Every block, all invariants are checked atomically" using Tenderly Web3 Actions. PagerDuty escalation and Slack notifications. 24/7 invariant-based monitoring confirmed. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security docs](https://docs.maple.finance/technical-resources/security/security); [P1] [Security of Syrup](https://maple.finance/news/security-of-syrup) |
| S-SC-11 | Are automatic safety controls (e.g. pause, circuit breakers) triggered by monitoring alerts? | Emergency pause exists via Security Admin (verified 3-of-6 Safe multisig). However, pause requires manual triggering, not automatic invariant-triggered on-chain protections. | 3 | 9 | **Improvable** | [P0] Security Admin verified via Safe API: 3-of-6 Safe; [P1] [Protocol actors](https://docs.maple.finance/technical-resources/protocol-overview/protocol-actors) |

**Smart Contract Security Subtotal:**
- Raw scores: 9+9+9+9+9+1+9+9+9+9+3 = 86/99
- Adjusted: (86/99) x 180 = **156.4/180 (86.9%)**

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Admin/upgrade rights held by GovernorTimelock managed by DAO Multisig, verified as 4-of-7 Safe wallet via Safe Global API (March 2026). Threshold=4, Owners=7, Nonce=429 (active usage). GovernorTimelock deployment in late 2025 was an improvement adding formal controls. | 9 | 9 | Non-Improvable (optimal) | [P0] DAO Multisig Safe API: 4-of-7, nonce=429; [P0] GovernorTimelock at [Etherscan](https://etherscan.io/address/0x2eFFf88747EB5a3FF00d4d8d0f0800E306C0426b); [P1] [Address registry](https://github.com/maple-labs/address-registry) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | Moving funds or upgrading requires GovernorTimelock (24h delay) managed by 4-of-7 Safe multisig. 4-of-7 exceeds criteria (>=3 threshold AND >=5 signers AND >=24h timelock). Pool Delegate can fund loans but cannot extract to arbitrary addresses. Security Admin (3-of-6 Safe) can only pause. | 9 | 9 | Non-Improvable (optimal) | [P0] DAO Multisig: 4-of-7 Safe verified; [P0] GovernorTimelock MIN_DELAY=86400; [P0] Security Admin: 3-of-6 Safe verified |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | DAO Multisig verified as 4-of-7 Safe. Configuration is strong. However, signer identities not publicly disclosed. Per criteria: "If signer identities are fully unknown, independence cannot be confirmed -- score Mid (3) at best." | 3 | 9 | **Source Missing** | [P0] Safe API: threshold=4, owners=7; [P1] No public signer identity disclosure |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause by Security Admin (verified 3-of-6 Safe multisig). Protocol-wide, not address-level selective. Scope is broad ("can temporarily disable almost all functions"). Not time-bound. Rules partially documented. | 3 | 9 | **Improvable** | [P0] Security Admin: 3-of-6 Safe; [P1] [Protocol actors](https://docs.maple.finance/technical-resources/protocol-overview/protocol-actors) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | User USDT deposits in non-custodial pool contract (ERC-4626). But borrower collateral held at institutional custodians (Anchorage, BitGo, Zodia) in tri-party arrangements. Pool itself is non-custodial; collateral enforcement depends on off-chain custody. | 3 | 3 | Non-Improvable | [P0] Pool at [Etherscan](https://etherscan.io/address/0x356B8d89c1e1239Cbbb9dE4815c39A1474d5BA7D); [P1] [FAQ](https://docs.maple.finance/syrupusdc-usdt-for-lenders/faq) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Clear on-chain segregation. syrupUSDT pool (0x356B8d89...), DAO treasury multisig (0xd6d4Bcde...), protocol treasury (0xa9466EaB...), Maple Labs ops (0x94f98416...) all separate. | 9 | 9 | Non-Improvable (optimal) | [P0] Pool, DAO, Treasury, Labs addresses verified on Etherscan; [P1] [Address registry](https://github.com/maple-labs/address-registry) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | Pool deploys via: (1) LoanManagers for institutional lending, (2) AaveStrategy (0x2b817B82...) for idle USDT. No SkyStrategy for syrupUSDT (unlike syrupUSDC). Adding new strategies requires Governor approval through GovernorTimelock with 24h delay. | 9 | 9 | Non-Improvable (optimal) | [P1] [Address registry](https://github.com/maple-labs/address-registry) -- syrupUSDT section; [P0] AaveStrategy at [Etherscan](https://etherscan.io/address/0x2b817B822B0ddd4597a92dBEd1bD0a6796CA37E0) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No documented playbook found. Maple has monitoring and pause capabilities (3-of-6 Security Admin multisig) but no formal tested playbook with key rotation steps or tabletop exercises. | 1 | 9 | **Improvable** | Searched docs.maple.finance, security page, GitHub -- no playbook found |

**Key Management Subtotal:**
- Raw scores: 9+9+3+3+3+9+9+1 = 46/72
- Adjusted: (46/72) x 180 = **115.0/180 (63.9%)**

**Security Total: 156.4 + 115.0 = 271.4/360 (75.4%)**

### STRATEGY (30% Weight) -- Score: 176.3/270 (65.3%)

#### Protocol Mechanics (5%) - 57/81 raw, 31.7/45 weighted

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield from: (1) fixed-rate overcollateralized institutional loans (~70-80%), (2) collateral enhancement via liquid staking of borrower collateral, (3) DeFi liquidity provision via Aave strategy on idle USDT, (4) futures basis trading. Well-aligned with institutional lending mandate. syrupUSDT current APY approximately 7-8%. | 9 | 9 | Non-Improvable (optimal) | [P1] [FAQ](https://docs.maple.finance/syrupusdc-usdt-for-lenders/faq); [P1] [Yield generation](https://maple.finance/insights/yield-generation-underwriting-and-risk-management) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Principal loss can occur if: (a) multiple borrowers simultaneously fail margin calls during sharp crash, (b) collateral drops below liquidation faster than OTC execution, (c) custodian failure, (d) USDT depeg event reducing real value of all USDT-denominated assets. These are severe but plausible single-shock events. Oct 2025: syrupUSDT held at 140% OC at lowest. | 3 | 3 | Non-Improvable | [P1] [Maple performance](https://maple.finance/insights/maple-performance); [P1] [Yield generation](https://maple.finance/insights/yield-generation-underwriting-and-risk-management) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage on depositor/pool side. Loans are 1:1 funded from pool. Some borrower collateral staked for yield enhancement (disclosed). Effective leverage at pool level is 1x. | 9 | 9 | Non-Improvable (optimal) | [P1] [Yield generation](https://maple.finance/insights/yield-generation-underwriting-and-risk-management) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | Automated margin call monitoring with three independent price feeds and 24/7/365 monitoring. Borrowers get 24h notice at margin call level. But actual liquidation execution is manual via OTC desks and custodian APIs. | 3 | 9 | **Improvable** | [P1] [Yield generation](https://maple.finance/insights/yield-generation-underwriting-and-risk-management); [P1] [Maple performance](https://maple.finance/insights/maple-performance) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | V1 (undercollateralized) had permanent losses. V2 (overcollateralized, launched Dec 2022) has zero losses over 3+ years. Per criteria: "Major version upgrade with architectural rewrite = NOT comparable." V2 eliminated the undercollateralized mechanism that caused V1 losses. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 architecture](https://docs.maple.finance/technical-resources/protocol-overview/smart-contract-architecture); [P1] [Maple performance](https://maple.finance/insights/maple-performance) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Partial framework: overcollateralization targets (120-170%), margin call/liquidation levels, collateral analysis criteria, borrower underwriting process, concentration limits. But not published as comprehensive formal document with all quantitative limits. | 3 | 9 | **Improvable** | [P1] [Yield generation](https://maple.finance/insights/yield-generation-underwriting-and-risk-management); [P1] [FAQ](https://docs.maple.finance/syrupusdc-usdt-for-lenders/faq) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yield primarily organic from borrower interest. $30M ARR, $65M distributed in 2025. 60 unique borrowers. SYRUP staking ended (MIP-019), replaced with buyback model. No significant emission-based yield. | 9 | 9 | Non-Improvable (optimal) | [P1] [2025 Data Review](https://maple.finance/insights/2025-data-review); [P2] MIP-019 governance vote |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Full $987M position unwind requires loan maturities. Idle USDT in Aave strategy provides immediate buffer. ~$2.9M/day secondary market. For large exits, slippage 2-5% would compress returns. | 3 | 3 | Non-Improvable | [P1] Withdrawal docs; [P3] CoinGecko: $2.9M/day syrupUSDT volume |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Fixed-rate lending; yield from borrower interest rates, not from a peg or spread trade. USDT peg is the denomination, not the yield source. | 9 | 9 | Non-Improvable (optimal) | [P1] [FAQ](https://docs.maple.finance/syrupusdc-usdt-for-lenders/faq) |

**Protocol Mechanics Subtotal:**
- Raw scores: 9+3+9+3+9+3+9+3+9 = 57/81
- Adjusted: (57/81) x 45 = **31.7/45**

#### Collateral (5%) - 21/27 raw (1 N/A), 35.0/45 weighted

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Collateral limited to BTC, ETH, top stablecoins, and select LSTs (e.g., jitoSOL). Each evaluated for liquidity, historical volatility, and technical security. Conservative LTVs with 120-170% overcollateralization. These are low-risk large-cap assets. | 9 | 9 | Non-Improvable (optimal) | [P1] [Yield generation](https://maple.finance/insights/yield-generation-underwriting-and-risk-management); [P1] [FAQ](https://docs.maple.finance/syrupusdc-usdt-for-lenders/faq) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | Oct 2025: BTC collateral caused syrupUSDT OC to drop from >150% to 140% at lowest. Nine margin calls issued, all cured within 3 hours. Borrowers proactively upgraded collateral. Recovery to ~148% within days. | 3 | 3 | Non-Improvable | [P1] [Maple performance](https://maple.finance/insights/maple-performance) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- syrupUSDT is a lending product, not a staking product. | N/A | N/A | N/A | N/A |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | User deposits are USDT on Ethereum (natively issued by Tether). Pool holds native USDT. No bridged assets in core pool. Cross-chain expansion uses Chainlink CCIP (Tier-0) but core Ethereum pool is native. | 9 | 9 | Non-Improvable (optimal) | [P0] Pool at [Etherscan](https://etherscan.io/address/0x356B8d89c1e1239Cbbb9dE4815c39A1474d5BA7D); [P1] CCIP integration docs |

**Collateral Subtotal:**
- Raw scores: 9+3+N/A+9 = 21/27 (3 scored questions)
- Adjusted: (21/27) x 45 = **35.0/45**

#### Infra Counterparty Exposures (5%) - 42/54 raw (2 N/A), 35.0/45 weighted

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Dependencies: Ethereum (Tier-0), Chainlink Price Feeds (Tier-0) with wrapper protections, Chainlink CCIP (Tier-0) for cross-chain, institutional custodians (Anchorage, BitGo, Zodia -- established but not in SR tier list). Most dependencies explicitly listed. | 3 | 9 | **Improvable** | [P1] [FAQ](https://docs.maple.finance/syrupusdc-usdt-for-lenders/faq); [P1] [Security docs](https://docs.maple.finance/technical-resources/security/security) |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | Chainlink (Tier-0) for price feeds with custom oracle wrapper protections. Three independent price feed sources for collateral monitoring. Chainlink CCIP (Tier-0) for cross-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] Security docs; [P1] FAQ (three price feed sources) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Anchorage Digital (OCC-chartered bank, SOC 2 Type II), BitGo (qualified custodian, SOC 2 Type II), Zodia Custody (Standard Chartered-backed, FCA registered). All hold relevant certifications. | 9 | 9 | Non-Improvable (optimal) | [P1] [FAQ](https://docs.maple.finance/syrupusdc-usdt-for-lenders/faq); Public records for Anchorage/BitGo/Zodia |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Protocol live >3 years on Ethereum. Oct 2025 volatility: systems functioned without disruption, $67M in redemptions processed, all margin calls cured within 3 hours. Zero losses. | 9 | 9 | Non-Improvable (optimal) | [P1] [Maple performance](https://maple.finance/insights/maple-performance) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No Ethereum chain halt or consensus failure >30 minutes in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P3] Ethereum network status |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- syrupUSDT is not a staking product. | N/A | N/A | N/A | - |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- syrupUSDT is not a staking product. | N/A | N/A | N/A | - |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | Users can request withdrawal from pool contract on-chain. But if a primary custodian fails, collateral for affected loans cannot be liquidated. Redundancy across three custodians limits single-point exposure. | 3 | 3 | Non-Improvable | [P1] [FAQ](https://docs.maple.finance/syrupusdc-usdt-for-lenders/faq); [P1] Yield generation docs |

**Infra Counterparty Subtotal:**
- Raw scores: 3+9+9+9+9+N/A+N/A+3 = 42/54 (6 scored questions)
- Adjusted: (42/54) x 45 = **35.0/45**

#### Protocol Counterparty Exposures (5%) - 27/45 raw, 27.0/45 weighted

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Idle USDT deployed to Aave (Tier-0). USDT lent to 60 unique institutional borrowers (KYC'd, names confidential). Borrower collateral at Anchorage, BitGo, Zodia. OTC desks for liquidation. Most venues disclosed but borrower identities confidential. | 3 | 9 | **Improvable** | [P1] [2025 Data Review](https://maple.finance/insights/2025-data-review); [P1] Architecture docs |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Fee structure disclosed: management fees and performance fees. 25% of protocol revenue goes to Syrup Strategic Fund (SYRUP buybacks). Revenue split documented. No apparent misalignment. | 9 | 9 | Non-Improvable (optimal) | [P2] MIP-019 |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Concentration limits applied across loan book. Individual borrower exposure capped. But enforcement partly manual by Maple Direct, not fully on-chain enforced. | 3 | 9 | **Improvable** | [P1] [Yield generation](https://maple.finance/insights/yield-generation-underwriting-and-risk-management) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Aave strategy: near-instant unwind. Institutional loans: depend on term maturity. Borrowers can repay early. Default triggers OTC liquidation. Some positions require loan maturity for full unwind. | 3 | 3 | Non-Improvable | [P1] Smart contract architecture; [P1] Withdrawal docs |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | All custodians disclosed: Anchorage Digital, BitGo, Zodia Custody. Roles described (tri-party collateral custody). Maple Direct as internal asset manager fully disclosed. | 9 | 9 | Non-Improvable (optimal) | [P1] [FAQ](https://docs.maple.finance/syrupusdc-usdt-for-lenders/faq) |

**Protocol Counterparty Subtotal:**
- Raw scores: 3+9+3+3+9 = 27/45
- Adjusted: (27/45) x 45 = **27.0/45**

#### Liquidity (5%) - 37/81 raw, 20.6/45 weighted

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Queue-based on-chain withdrawals via WithdrawalManagerQueue (0x86eBDf90...). FIFO processing as liquidity becomes available. Protocol-wide pause via Security Admin (3-of-6 Safe multisig). No address-level selective blocking. | 3 | 9 | **Improvable** | [P0] WithdrawalManagerQueue at [Etherscan](https://etherscan.io/address/0x86eBDf902d800F2a82038290B6DBb2A5eE29eB8C); [P0] Security Admin: 3-of-6 Safe |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | ~$987M TVL mostly lent out. Idle USDT in Aave strategy provides immediate liquidity buffer. Oct 2025: $67M processed smoothly (~2.5% of total protocol TVL). Near-total exit requires loan maturities. Markets can absorb ~3% without major dislocation. | 3 | 3 | Non-Improvable | [P1] [Maple performance](https://maple.finance/insights/maple-performance); [P3] CoinGecko market data |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | Since April 2025 withdrawal upgrade, average processing under 5 minutes. Oct 2025: $67M processed without delays or freezes. Nov 2025 WithdrawalManager upgrade further improved handling. | 9 | 9 | Non-Improvable (optimal) | [P1] [Built for Scale](https://maple.finance/insights/syrupusdc-and-syrupusdt-built-for-scale); [P1] [Maple performance](https://maple.finance/insights/maple-performance) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | When most USDT lent out, available liquidity limited by loan book utilization. Queue processes FIFO as repayments come in. No artificial caps but high utilization creates natural queues. | 3 | 3 | Non-Improvable | [P1] Withdrawal docs; [P1] Smart contract architecture |
| ST-L-05 | How does exit liquidity behave during volatility? | Oct 2025: during "$19B in positions unwound across exchanges," Maple processed $67M smoothly. Systems functioned without disruption. Inflows restored deposits to ATH within 48 hours. Demonstrated real-world stress resilience. | 9 | 9 | Non-Improvable (optimal) | [P1] [Maple performance](https://maple.finance/insights/maple-performance) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | Withdrawals depend on loan book liquidity. "Short duration loans" but exact composition not publicly disclosed. Estimated 10-30% of assets in loans with duration beyond immediate availability. | 3 | 3 | Non-Improvable | [P1] [FAQ](https://docs.maple.finance/syrupusdc-usdt-for-lenders/faq) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Primary exit is in-protocol queue-based redemption. Secondary on Fluid (Ethereum + Plasma) and Uniswap V4 with ~$2.9M/day combined volume. Secondary is optional for faster exits. Covers ~0.3% of $987M TVL. Sufficient for small exits but thin under stress. | 3 | 9 | **Improvable** | [P3] CoinGecko tickers: Fluid ETH $1.6M, Fluid Plasma $1.1M, Uniswap V4 $0.3M |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | USDT underlying: extremely deep across CEXs and DEXs. syrupUSDT receipt token: ~$2.9M/day secondary market, ~0.3% of TVL. Receipt token depth thin relative to protocol size. Per criteria, <3% TVL depth = High Risk. | 1 | 9 | **Improvable** | [P3] CoinGecko: syrupUSDT 24h vol $2.9M; Market cap ~$987M |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | In a bank-run, most USDT is lent to institutional borrowers. Idle cash provides first-come liquidity. Queue processes FIFO. Overcollateralization (148%) means eventual full recovery but significant queues and temporary discounting likely. No expected permanent haircuts. | 3 | 3 | Non-Improvable | [P1] Smart contract architecture; [P1] [Maple performance](https://maple.finance/insights/maple-performance) |

**Liquidity Subtotal:**
- Raw scores: 3+3+9+3+9+3+3+1+3 = 37/81
- Adjusted: (37/81) x 45 = **20.6/45**

#### Market (5%) - 27/45 raw, 27.0/45 weighted

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under stress? | syrupUSDT is a yield-bearing ERC-4626 token trading at ~$1.12 (above $1.00, reflecting accrued yield). CoinGecko shows consistent pricing. No documented depeg events. However, secondary market depth is thin ($2.9M/day for $987M TVL). Oct 2025 stress: zero losses but limited secondary market stress-test data. | 3 | 9 | **Improvable** | [P3] CoinGecko: syrupUSDT price $1.12; [P1] [Maple performance](https://maple.finance/insights/maple-performance) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Strategy is low-beta from crypto directional perspective (USDT claim, not directional BTC/ETH exposure). However, USDT denomination creates material Tether counterparty risk: if Tether faces regulatory action or reserve issues causing USDT depeg, all syrupUSDT holders suffer permanent principal loss in USD terms. Tether's reserve transparency and regulatory status are less clear than Circle's (USDC). This is a plausible moderate-severity risk. | 3 | 3 | Non-Improvable | [P1] [FAQ](https://docs.maple.finance/syrupusdc-usdt-for-lenders/faq); [P4] Ongoing regulatory scrutiny of Tether |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Fixed-rate lending model not subject to utilization-based rate curves. Borrower rates set at loan origination. No reflexive incentive models. No history of rate cliff issues. | 9 | 9 | Non-Improvable (optimal) | [P1] [FAQ](https://docs.maple.finance/syrupusdc-usdt-for-lenders/faq) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Oct 2025 event served as real-world stress test. Maple published detailed performance analysis. However, formal stress testing documentation (modeled scenarios, tail assumptions) not publicly available. | 3 | 9 | **Improvable** | [P1] [Maple performance](https://maple.finance/insights/maple-performance) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | No leverage on depositor side. 148% overcollateralization provides large buffer. BTC collateral would need >48% drop to breach liquidation. Margin calls at intermediate levels provide early warning. | 9 | 9 | Non-Improvable (optimal) | [P1] [Maple performance](https://maple.finance/insights/maple-performance) (140% at lowest) |

**Market Subtotal:**
- Raw scores: 3+3+9+3+9 = 27/45
- Adjusted: (27/45) x 45 = **27.0/45**

**Strategy Total: 31.7 + 35.0 + 35.0 + 27.0 + 20.6 + 27.0 = 176.3/270 (65.3%)**

### OPERATIONS (30% Weight) -- Score: 166.3/270 (61.6%)

#### Governance (7.5%) - 22/36 raw, 41.3/67.5 weighted

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes? | Hybrid model. Major decisions via SYRUP token Snapshot governance (MIPs) with 5% quorum. On-chain execution via GovernorTimelock managed by DAO multisig (4-of-7 Safe). Multisig executes within governance-approved bounds. No single entity can unilaterally change core logic. | 3 | 9 | **Improvable** | [P1] [DAO Governance](https://maple.finance/insights/maple-dao-governance-process/); [P0] GovernorTimelock; [P2] Snapshot |
| O-G-02 | How concentrated is voting power among top holders or delegates? | MIP-019 had only 26 participating wallets. Single address controlled 30% of voting power. Top 10 voting addresses likely control >66% of power. High concentration. | 1 | 3 | **Improvable** | [P2] MIP-019 vote results; [P4] The Defiant reporting |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | GovernorTimelock with MIN_DELAY = 86400 (24h) for all major upgrades. Guardian/Security Admin powers limited to emergency pause (narrow scope). Timelock publicly visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P0] GovernorTimelock at [Etherscan](https://etherscan.io/address/0x2eFFf88747EB5a3FF00d4d8d0f0800E306C0426b) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Pool Delegate replaceable by Governor through GovernorTimelock with timelock. WithdrawalManagerQueue operates independently. Replacement subject to 1-day+ timelock with transparent change logs. | 9 | 9 | Non-Improvable (optimal) | [P1] [Protocol actors](https://docs.maple.finance/technical-resources/protocol-overview/protocol-actors); [P1] Architecture docs |

**Governance Subtotal:**
- Raw scores: 3+1+9+9 = 22/36
- Adjusted: (22/36) x 67.5 = **41.3/67.5**

#### Team & Legal & Compliance (7.5%) - 51/81 raw, 42.5/67.5 weighted

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Core team fully identified: Sidney Powell (CEO/Co-Founder, ex-banking, $3B+ bond issuance), Joe Flanagan (Chairman), Matt Collum (CTO), Ryan O'Shea (COO). Backgrounds from J.P. Morgan, BofA, Deutsche Bank, Amazon, BlackRock, Galaxy. | 9 | 9 | Non-Improvable (optimal) | [P1] [About page](https://maple.finance/about); [P2] Conference profiles |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Maple Labs has dedicated engineering team (76 GitHub repos). 4 named leaders. But relatively small team for ~$2.46B protocol. Key-person risk with Sid Powell as primary public figure. | 3 | 9 | **Improvable** | [P1] [GitHub](https://github.com/maple-labs); [P1] [About](https://maple.finance/about) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Core Foundation lawsuit references Cayman Islands jurisdiction. Maple Labs appears to be operating entity. Team relocated from Australia to Miami. Specific legal entity name and registration not explicitly disclosed. | 3 | 9 | **Source Missing** | [P4] Core Foundation lawsuit; [P1] [About page](https://maple.finance/about) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known regulatory enforcement actions. Core Foundation lawsuit (Nov 2025) is a civil/commercial dispute over syrupBTC exclusivity, NOT regulatory enforcement. Cayman Islands court issued injunction blocking syrupBTC. Maple denies allegations. | 9 | 9 | Non-Improvable | [P4] [CoinDesk](https://www.coindesk.com/policy/2025/11/20/core-foundation-wins-injunction-against-maple-finance-on-alleged-confidentiality-breach) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | 24/7/365 monitoring with PagerDuty escalation and Slack notifications. Three independent price feeds for collateral monitoring. However, formal documented runbooks with defined SLAs not publicly available. | 3 | 9 | **Source Missing** | [P1] [Security docs](https://docs.maple.finance/technical-resources/security/security); [P1] [Yield generation](https://maple.finance/insights/yield-generation-underwriting-and-risk-management) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | contact@maple.finance listed. Help center exists. Oct 2025: detailed performance analysis published within days. Active partnerships with Aave, Fluid, Pendle suggest responsive support. | 9 | 9 | Non-Improvable (optimal) | [P1] [maple.finance](https://maple.finance/); [P1] [Maple performance](https://maple.finance/insights/maple-performance) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Investors disclosed: BlockTower Capital, Circle, Tioga Capital, Spartan Group, Castle Island Ventures, Framework Ventures, and others. Roles clear as financial investors. | 9 | 9 | Non-Improvable (optimal) | [P1] [About](https://maple.finance/about); [P1] [Strategic Funding](https://maple.finance/insights/maple-closes-strategic-funding-round) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Maple Direct manages syrupUSDC (~$1.47B), syrupUSDT (~$987M), and Maple Institutional Secured Lending. All share lending infrastructure and borrower pool. Potential allocation conflicts between pools exist. No formal conflict-of-interest policy published. | 3 | 9 | **Improvable** | [P1] [maple.finance](https://maple.finance/) (three products listed) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | Maple Labs operated V1 where $46M in defaults occurred. However, V1 pool management was by third-party pool delegates (M11 Credit, Orthogonal Trading). Maple Direct created June 2023 after V1 failures, implementing overcollateralized-only lending. Demonstrates clear process improvements. | 3 | 3 | Non-Improvable | [P4] News sources on 2022 defaults; [P1] [Maple Direct](https://maple.finance/insights/introducing-maple-direct/) |

**Team & Legal Subtotal:**
- Raw scores: 9+3+3+9+3+9+9+3+3 = 51/81
- Adjusted: (51/81) x 67.5 = **42.5/67.5**

#### Documentation & Transparency (7.5%) - 36/54 raw, 45.0/67.5 weighted

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Comprehensive documentation at docs.maple.finance covering protocol architecture, smart contract design, proxy upgradeability, protocol actors, fee structure, lending mechanics, withdrawal process. Updated with each release. | 9 | 9 | Non-Improvable (optimal) | [P1] [docs.maple.finance](https://docs.maple.finance/) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Collateral flow described: USDT deposited -> pool -> loans -> borrowers. Loss scenarios mentioned but not systematically mapped with quantitative triggers or scenario tables. | 3 | 9 | **Improvable** | [P1] [Yield generation](https://maple.finance/insights/yield-generation-underwriting-and-risk-management); [P1] [FAQ](https://docs.maple.finance/syrupusdc-usdt-for-lenders/faq) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | GitHub address-registry (maple-labs/address-registry) provides canonical listing including syrupUSDT pool, PoolManager, LoanManagers, WithdrawalManagerQueue, strategies. Updated with each deployment. | 9 | 9 | Non-Improvable (optimal) | [P1] [Address registry](https://github.com/maple-labs/address-registry) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Roles documented in protocol actors page: Governor, Security Admin, Operational Admin, Pool Delegate. GovernorTimelock provides on-chain change trail. But no centralized registry with explanations for all changes. | 3 | 9 | **Improvable** | [P1] [Protocol actors](https://docs.maple.finance/technical-resources/protocol-overview/protocol-actors); [P0] GovernorTimelock on-chain history |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Real-time collateral visibility on app.maple.finance. Collateral levels published during events (e.g., 148% OC). But no formal PoR methodology, no independent attestation, no systematic PoL. This is a lending protocol so PoL IS applicable. | 3 | 9 | **Improvable** | [P1] [FAQ](https://docs.maple.finance/syrupusdc-usdt-for-lenders/faq); [P1] [Maple performance](https://maple.finance/insights/maple-performance) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Core contracts verified on Etherscan: syrupUSDT Pool (0x356B8d89...), PoolManager (0x0cdA32E0...), GovernorTimelock, MapleGlobals, SyrupRouter. Proxy and implementation both verified. | 9 | 9 | Non-Improvable (optimal) | [P0] Etherscan verification confirmed for key contracts |

**Documentation Subtotal:**
- Raw scores: 9+3+9+3+3+9 = 36/54
- Adjusted: (36/54) x 67.5 = **45.0/67.5**

#### Financial Resilience (7.5%) - 25/45 raw, 37.5/67.5 weighted

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | No dedicated safety module with binding activation rules. DAO treasury (~$10M per DeFiLlama across two addresses) could theoretically cover losses via governance but no formal binding rules. Syrup Strategic Fund (25% revenue) is for buybacks, not loss coverage. | 3 | 9 | **Improvable** | [P3] DeFiLlama treasury: ~$10M across 0xa9466EaB... and 0xd6d4Bcde...; [P2] MIP-019 |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | DeFiLlama treasury data: ~$10M across two addresses (0xa9466EaBd096449d650D5AEB0dD3dA6F52FD0B19 protocol treasury, 0xd6d4Bcde6c816F17889f1Dd3000aF0261B03a196 DAO multisig). Total protocol TVL: ~$2.46B. Ratio: ~0.41% of TVL. Far below 1% threshold for Mid score. | 1 | 9 | **Improvable** | [P3] DeFiLlama: ~$10M treasury; [P3] DeFiLlama: $2.46B protocol TVL |
| O-FR-03 | What is the estimated operational runway at current burn? | $30M ARR. Multiple funding rounds completed. Revenue growing consistently. Protocol appears revenue-positive. Runway comfortably >24 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [2025 Data Review](https://maple.finance/insights/2025-data-review) ($30M ARR) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Oct 2025: TVL temporarily declined ($67M in redemptions) but recovered to ATH within 48 hours. Revenue maintained. Overcollateralization held (140% lowest for syrupUSDT). No buffer depletion. No depositor haircuts. | 9 | 9 | Non-Improvable (optimal) | [P1] [Maple performance](https://maple.finance/insights/maple-performance) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Pool contracts allow permissionless on-chain withdrawal queue. But active loan management (margin calls, liquidation execution) requires off-chain team operations via custodian APIs and OTC desks. New origination would cease. Users can still exit but collateral management degrades. | 3 | 9 | **Improvable** | [P1] Architecture docs; [P1] [Protocol actors](https://docs.maple.finance/technical-resources/protocol-overview/protocol-actors) |

**Financial Resilience Subtotal:**
- Raw scores: 3+1+9+9+3 = 25/45
- Adjusted: (25/45) x 67.5 = **37.5/67.5**

**Operations Total: 41.3 + 42.5 + 45.0 + 37.5 = 166.3/270 (61.6%)**

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 86 | 99 | 156.4 | 180 | 86.9% |
| | Key Management (8 Q) | 46 | 72 | 115.0 | 180 | 63.9% |
| | **Security Subtotal** | | | **271.4** | **360** | **75.4%** |
| **Strategy** | Protocol Mechanics (9 Q) | 57 | 81 | 31.7 | 45 | 70.4% |
| | Collateral (3 of 4 Q scored) | 21 | 27 | 35.0 | 45 | 77.8% |
| | Infra Counterparty (6 of 8 Q scored) | 42 | 54 | 35.0 | 45 | 77.8% |
| | Protocol Counterparty (5 Q) | 27 | 45 | 27.0 | 45 | 60.0% |
| | Liquidity (9 Q) | 37 | 81 | 20.6 | 45 | 45.7% |
| | Market (5 Q) | 27 | 45 | 27.0 | 45 | 60.0% |
| | **Strategy Subtotal** | | | **176.3** | **270** | **65.3%** |
| **Operations** | Governance (4 Q) | 22 | 36 | 41.3 | 67.5 | 61.1% |
| | Team & Legal (9 Q) | 51 | 81 | 42.5 | 67.5 | 63.0% |
| | Documentation (6 Q) | 36 | 54 | 45.0 | 67.5 | 66.7% |
| | Financial Resilience (5 Q) | 25 | 45 | 37.5 | 67.5 | 55.6% |
| | **Operations Subtotal** | | | **166.3** | **270** | **61.6%** |
| **TOTAL** | | | | **614.0** | **900** | **68.2%** |

---
