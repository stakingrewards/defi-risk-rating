# Kamino Finance - Sentora PYUSD Vault Risk Rating

**Rating Date**: 2026-03-10
**Final Grade**: B-
**Total Score**: 676.1/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v1.0-alpha

---

## Detailed Analysis

### SECURITY (40% Weight) - Score: 253.6/360 (70.4%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. Kamino has undergone 18+ external audits covering core lending (KLend), vault (KVault), farming (KFarms), liquidity, and oracle aggregator (Scope) contracts. Auditing firms include OtterSec, Offside Labs, Sec3, Certora, Ackee Blockchain, OpenSec, and Rx. Additionally, 3+ formal verifications completed by Certora (Lend, Vault, Limo). Most recent: Certora formal verification February 2025. | 9 | 9 | Non-Improvable (optimal) | [GitHub Audits](https://github.com/Kamino-Finance/audits), [Certora Report](https://www.certora.com/reports/kamino-lending-security-report), [Immunefi](https://immunefi.com/bug-bounty/kamino/) listing 17 assets in scope |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent formal engagement: Certora formal verification (November 2024 - February 2025). Certora is not on the SR tier list but is an industry-recognized leader in formal verification. Ackee Blockchain, which has also audited Kamino, is listed as Tier-1 on the SR auditor tiers. Multiple Solana-ecosystem auditors (OtterSec, Offside Labs, Sec3) not on the SR tier list have also audited the protocol. | 9 | 9 | Non-Improvable (optimal) | [Certora Blog](https://www.certora.com/blog/securing-kamino-lending), [GitHub Audits](https://github.com/Kamino-Finance/audits) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Kamino V2 (May 2025) accompanied by Certora audits of Lend, Vault, and Limo. Chainlink Data Streams oracle integration (April 2025) had Multi-Price Oracle System audited by Certora and Offside Labs before deployment. Continuous audit program maintained. | 9 | 9 | Non-Improvable (optimal) | [GitHub Audits](https://github.com/Kamino-Finance/audits), [Chainlink Integration Announcement](https://gov.kamino.finance/t/kamino-integrates-chainlink-data-streams-for-high-quality-low-latency-market-data/550) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. Certora formal verification found precision loss issue in exchange rate calculations, proactively patched despite not being currently exploitable. All critical findings across 18+ audits resolved. Zero critical vulnerabilities per security page. | 9 | 9 | Non-Improvable (optimal) | [Certora Blog](https://www.certora.com/blog/securing-kamino-lending), [GitHub Audits](https://github.com/Kamino-Finance/audits) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Kamino contracts on Solana are upgradeable (standard for Solana programs). No documented timelock mechanism exists for upgrades. Research across official docs, governance forum, and third-party sources found no evidence of a timelock delay. The December 2, 2025 incident where Kamino updated smart contracts overnight to block Jupiter Lend's refinance tool demonstrates that upgrades can be executed rapidly without public advance notice or governance approval. Upgrade constraints are undocumented. | 1 | 9 | **Improvable** | Multiple sources confirm no documented timelock. Jupiter Lend blocking incident: [The Defiant](https://thedefiant.io/news/defi/kamino-blocks-jupiter-lend-refinance), [Blockworks](https://blockworks.co/news/jup-lend-vs-kamino) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploits causing user fund loss. Clean record since founding in 2022 (3+ years). Security page states "18 full audits completed with 0 critical vulnerabilities." No incidents found on Rekt.news or security incident databases. | 9 | 9 | Non-Improvable (optimal) | [Kamino Security](https://kamino.com/security), [CertiK Skynet](https://skynet.certik.com/projects/kamino-finance), exhaustive web search |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. 3+ year track record. Team publicly identified. Open source with verifiable builds. | 9 | 9 | Non-Improvable (optimal) | [Kamino Finance](https://kamino.com/), team publicly identified, no allegations found |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No documented timelock exists to reduce. No evidence of any governance protection mechanism being weakened. The absence of a timelock is penalized under S-SC-05; this question specifically addresses reductions to existing mechanisms. | 9 | 9 | Non-Improvable | Exhaustive research found no evidence of timelock reductions |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active Immunefi bounty launched October 6, 2025. Maximum payout $1,500,000 for critical smart contract bugs. 17 assets in scope (KLend, KVault, KFarms, Liquidity, Oracle Aggregator). Critical: 10% of affected funds up to $1.5M, min $150K. High: up to $100K. Medium: $10K. Payments in USDC. | 9 | 9 | Non-Improvable (optimal) | [Immunefi - Kamino](https://immunefi.com/bug-bounty/kamino/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Kamino has the Risk Assessment Framework (KRAF) providing dashboards with risk overview, loan analysis, volatility analysis, liquidity risk, and shock scenarios at risk.kamino.finance. In-house security team conducts regular penetration testing. However, no evidence of a reputable third-party 24/7 monitoring provider (Hypernative, Blockaid, etc.) was found. KRAF appears to be a risk analytics tool rather than a real-time security monitoring system with automated alerting and on-call response. | 3 | 9 | **Improvable** | [Risk Dashboard](https://risk.kamino.finance/), [KRAF Docs](https://docs.kamino.finance/risk/risk-assessment-framework) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Kamino has emergency pause/shutdown mechanisms. Risk Council can trigger auto-deleveraging via multi-sig vote with 72-hour margin call period. However, auto-deleverage is currently manual (Risk Council vote), not automated. Documentation states future automation planned but not yet implemented. Manual triggers exist with documented procedures but no automatic invariant-breach triggers. | 3 | 9 | **Improvable** | [Auto-Deleverage Docs](https://docs.kamino.finance/risk/protocol-mechanisms/automated-deleverage) |

**Smart Contract Security Subtotal:**
- Raw scores: 9+9+9+9+1+9+9+9+9+3+3 = 79
- Max raw: 11 x 9 = 99
- Weighted: (79/99) x 180 = 143.6

**Smart Contract Security: 143.6/180 (79.8%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Kamino uses a multisig for administrative operations. Multisig address identified as 6hhBGCtmg7tPWUSgp3LG6X2rsmYWAc4tNsA6G4CnfQbM. Critical details are missing: signer identities, threshold (M-of-N), independence of signers not publicly documented. KMNO on-chain governance not yet activated (scheduled Q1 2026). Risk Council has emergency powers. Admin configuration change history is not publicly documented. | 1 | 9 | **Source Missing** | Multisig address found via [GitHub](https://github.com/Kamino-Finance). Signer details, threshold, and change history not found in official docs, governance forum, or third-party sources. |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No evidence of single-key control. Multisig required for admin actions. User assets held in non-custodial lending market contracts. Vault curators have allocation discretion but cannot directly withdraw user funds. Risk Council operates via multi-sig vote. | 9 | 9 | Non-Improvable (optimal) | [Kamino Docs](https://docs.kamino.finance), non-custodial contract architecture, multiple sources confirm multisig |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Multisig configuration not comprehensively disclosed. Third-party analysis (Exponential DeFi) reported fewer than 4 signers. Signer identities, independence, and threshold not publicly documented. This suggests a small multisig (possibly 2-of-3 or similar) with partial independence. | 3 | 9 | **Improvable** | [Exponential DeFi](https://exponential.fi/protocols/kamino-lend/) reported <4 signers |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Risk Council can pause markets via multisig. Auto-deleverage provides 72-hour margin call. No evidence of arbitrary address-level withdrawal censorship. Withdrawals permissionless based on pool liquidity. December 2025 Jupiter blocking restricted protocol interactions, not individual user withdrawals. | 9 | 9 | Non-Improvable (optimal) | [Auto-Deleverage Docs](https://docs.kamino.finance/risk/protocol-mechanisms/automated-deleverage) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. All user assets in non-custodial on-chain lending contracts on Solana. No off-chain custody. Verifiable builds ensure deployed code matches audited source. | 9 | 9 | Non-Improvable (optimal) | [Kamino Lend Litepaper](https://docs.kamino.finance/kamino-lend-litepaper), [GitHub klend](https://github.com/Kamino-Finance/klend) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. User funds in lending pool contracts, segregated from KMNO treasury (10% token allocation). Protocol revenue accrues separately. No evidence of co-mingling. | 9 | 9 | Non-Improvable (optimal) | [Token Info](https://docs.kamino.finance/kmno/token-info) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | Sentora PYUSD vault deploys exclusively into Kamino's own lending markets. Risk Council reviews all parameter changes from curators. Whitelist effectively limited to Kamino internal markets. However, on-chain enforcement mechanism and market addition governance not documented with timelock. Curator has allocation discretion within the vault. | 3 | 9 | **Improvable** | [Gauntlet Vault Curation](https://gov.kamino.finance/t/introducing-gauntlet-as-official-vault-curators/856) -- "Any parameter changes are reviewed by Kamino's Risk Council" |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No evidence found. No public incident response playbook, key rotation procedures, emergency response SLAs, or tabletop exercises documented. | 1 | 9 | **Source Missing** | Exhaustive search of docs, governance forum, GitHub, third-party sources found nothing |

**Key Management Subtotal:**
- Raw scores: 1+9+3+9+9+9+3+1 = 44
- Max raw: 8 x 9 = 72
- Weighted: (44/72) x 180 = 110.0

**Key Management: 110.0/180 (61.1%)**

---

**SECURITY TOTAL: 143.6 + 110.0 = 253.6/360 (70.4%)**

---

### STRATEGY (30% Weight) - Score: 225.5/270 (83.5%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield sources: (1) PYUSD lending interest from borrowers in Kamino markets, (2) PayPal/Paxos PYUSD growth incentives ($700K/month across Kamino). Both sources are mandate-aligned for a stablecoin lending strategy. September 2025 data showed stablecoin supply rates of 4.7% (organic) with incentives boosting total APY to approximately 14%. | 9 | 9 | Non-Improvable (optimal) | [Blockworks](https://blockworks.co/news/kamino-seeing-benefits-from-liquidity-incentives-on-pyusd), [Kamino Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to tail scenarios: smart contract exploit, oracle failure, severe collateral liquidation cascade in Kamino markets, or PYUSD depeg. Vault is on the lending side (not borrowing), so no direct liquidation risk. Overcollateralized lending model provides buffer. September 2025 stress test showed $10.6M potential bad debt at 30% market drawdown on $2.8B TVL (~0.4%). | 9 | 9 | Non-Improvable (optimal) | [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843), [Oracle Docs](https://docs.kamino.finance/risk/oracles) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage or rehypothecation. Vault lends PYUSD to borrowers. Effective leverage 1.0x. Borrowers may leverage but the vault itself is unleveraged. | 9 | 9 | Non-Improvable (optimal) | [Kamino Lend Litepaper](https://docs.kamino.finance/kamino-lend-litepaper) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is on the lending side, not borrowing. No direct liquidation risk for depositors. Borrower liquidations handled by Kamino's soft liquidation mechanism (20% partial, 2-10% penalty). | N/A | N/A | N/A | [Liquidation Docs](https://docs.kamino.finance/products/borrow-lend/position-risk-and-liquidations) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent loss events for PYUSD lending on Kamino. Clean track record since vault launch. September 2025 showed 2,289 liquidation events but all executed efficiently without generating bad debt for lenders. | 9 | 9 | Non-Improvable (optimal) | [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Sentora provides institutional risk framework built from IntoTheBlock's 1,000+ risk models and 300+ strategies across 60+ protocols. Kamino has KRAF (Kamino Risk Assessment Framework) with comprehensive dashboard. Quantitative limits for utilization, shock scenarios, and per-asset risk tiers are defined. | 9 | 9 | Non-Improvable (optimal) | [Sentora](https://sentora.com/), [KRAF Docs](https://docs.kamino.finance/risk/risk-assessment-framework) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Approximately 14% APY with organic stablecoin supply rates around 4.7%. PayPal incentives contribute approximately $700K/month. This suggests 55-65% of yield may be incentive-driven. Borrowing demand (utilization 76.6%) provides organic base but incentive dependency is material. Incentives appear to be slowly tapering. | 3 | 9 | **Improvable** | [Blockworks](https://blockworks.co/news/kamino-seeing-benefits-from-liquidity-incentives-on-pyusd), [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes. PYUSD is highly liquid (total supply $3.6B). Withdrawal depends on lending pool utilization. Interest rate model creates steep rate increases at high utilization, incentivizing borrower repayment. Pool utilization was 76.6% in September 2025, leaving adequate buffer. | 9 | 9 | Non-Improvable (optimal) | [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Strategy relies on PYUSD maintaining peg to USD. PYUSD is Paxos-issued, NYDFS-regulated, with monthly attestations (now by WithumSmith+Brown). Historical all-time low was approximately $0.955 during stress, with quick recovery. Peg risk is low for a regulated stablecoin but non-zero -- contributes minority of risk. | 3 | 3 | Non-Improvable | [PYUSD Transparency](https://www.paxos.com/pyusd-transparency), price history data |

**Protocol Mechanics Subtotal:**
- Raw scores (8 applicable): 9+9+9+9+9+3+9+3 = 60
- Max raw: 8 x 9 = 72
- Weighted: (60/72) x 45 = 37.5

**Protocol Mechanics: 37.5/45 (83.3%)**

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Kamino accepts blue-chip collateral with risk tiering: General (SOL, stablecoins), Isolated Collateral, and Isolated Debt categories. Per-asset LTVs: SOL 80%, LSTs 90-95% in eMode. Deposit/borrow caps adjusted based on volatility, liquidity, and security metrics. PYUSD itself is a regulated stablecoin. | 9 | 9 | Non-Improvable (optimal) | [Position Risk & Liquidations](https://docs.kamino.finance/products/borrow-lend/position-risk-and-liquidations) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | This question evaluates vault share (receipt token) behavior versus the underlying PYUSD. While PYUSD itself maintained its peg during September 2025 stress, vault shares are subject to utilization-dependent redemption constraints. At 76.6% utilization, only ~23% of supplied assets are immediately available for withdrawal. During high utilization periods, vault shares effectively trade at a discount to NAV since they cannot be redeemed at full value immediately. The vault has not experienced a severe stress test comparable to proven protocols. Per scoring principles, untested vault share behavior should score Mid (3). | 3 | 3 | Non-Improvable | [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843), [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- Vault holds PYUSD stablecoin, not staking derivatives. Solana does not currently have slashing for validators. | N/A | N/A | N/A |  |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | PYUSD is native on Solana (issued directly by Paxos via the Solana Token Extensions framework). Not bridged. Approximately 0% bridged asset exposure for the vault. | 9 | 9 | Non-Improvable (optimal) | [PayPal PYUSD on Solana](https://newsroom.paypal-corp.com/2024-05-29-PayPal-USD-Stablecoin-Now-Available-on-Solana-Blockchain) |

**Collateral Subtotal:**
- Raw scores (3 applicable): 9+3+9 = 21
- Max raw: 3 x 9 = 27
- Weighted: (21/27) x 45 = 35.0

**Collateral: 35.0/45 (77.8%)**

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Solana (Tier-0), Pyth Network (Tier-0), Chainlink Data Streams (Tier-0). No bridges. No CEX dependency. Paxos (NYDFS-regulated) for PYUSD issuance/redemption. All critical dependencies are Tier-0. | 9 | 9 | Non-Improvable (optimal) | [Oracle Docs](https://docs.kamino.finance/risk/oracles), [Chainlink Integration](https://gov.kamino.finance/t/kamino-integrates-chainlink-data-streams-for-high-quality-low-latency-market-data/550) |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | Multi-oracle system aggregates Pyth + Chainlink with cross-verification. TWAP/EWMA for manipulation resistance. Price bands (1% for USD stables). Double-audited by Certora and Offside Labs. No bridge dependency. Both oracles are Tier-0. | 9 | 9 | Non-Improvable (optimal) | [Oracle Docs](https://docs.kamino.finance/risk/oracles), [Scope GitHub](https://github.com/Kamino-Finance/scope) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Paxos (PYUSD issuer) is NYDFS-regulated with regular compliance audits. Kamino team SOC2/ISO27001 certifications not disclosed. Sentora certifications not publicly available. | 3 | 9 | **Source Missing** | [Paxos](https://www.paxos.com/pyusd) (regulatory status verified), Kamino/Sentora certifications not found |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Solana's last major outage was February 6, 2025 (approximately 5 hours). Since then, 12 months of continuous uptime achieved. No Kamino-specific infrastructure failures reported during that incident or subsequently. Oracle system maintained integrity. | 9 | 9 | Non-Improvable (optimal) | [Solana Status](https://status.solana.com/), [Helius Blog](https://www.helius.dev/blog/solana-outages-complete-history) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Solana's last major halt was February 6, 2025 (approximately 5 hours). As of March 2026, the chain has achieved over 13 months of continuous uptime with no further consensus failures. Firedancer client diversity further reducing halt risk. The February 2025 outage is now outside the 12-month lookback window. | 9 | 9 | Non-Improvable (optimal) | [Solana Status](https://status.solana.com/), [Solana Status Uptime History](https://status.solana.com/uptime) |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- PYUSD vault does not hold staking derivatives. Solana does not currently implement slashing. | N/A | N/A | N/A |  |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- Not applicable for PYUSD stablecoin lending vault. | N/A | N/A | N/A |  |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No single point of failure identified. Withdrawals are permissionless on-chain. Oracle failure: multi-oracle fallback. Chain halt: temporary. Paxos failure: PYUSD has independent redemption path. Users can interact directly with contracts. | 9 | 9 | Non-Improvable (optimal) | [Kamino Docs](https://docs.kamino.finance) |

**Infrastructure Counterparty Subtotal:**
- Raw scores (6 applicable): 9+9+3+9+9+9 = 48
- Max raw: 6 x 9 = 54
- Weighted: (48/54) x 45 = 40.0

**Infrastructure Counterparty: 40.0/45 (88.9%)**

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Kamino Lend markets only. No external protocol deployment. PYUSD backed by Paxos (US Treasuries + cash deposits). Apollo ACRED RWA integration announced but separate from this vault. | 9 | 9 | Non-Improvable (optimal) | [Kamino Lend](https://kamino.com/lend/sentora-pyusd) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | PayPal/Paxos PYUSD incentives ($700K/month) are publicly acknowledged. Kamino vault fee structure partially documented -- "Zero management & performance fees for all strategies except Re7's vault" per June 2025 data. Sentora-specific fee terms not fully transparent. | 3 | 9 | **Improvable** | [Blockworks](https://blockworks.co/news/kamino-seeing-benefits-from-liquidity-incentives-on-pyusd), [OnChain Times](https://www.onchaintimes.com/kamino-v2-composability-at-scale/) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Kamino enforces per-asset deposit and borrow caps. Dynamic limits adjusted by Risk Council based on KRAF analytics. Market-level exposure limits documented. Caps auto-adjusted based on risk signals. | 9 | 9 | Non-Improvable (optimal) | [Risk Docs](https://docs.kamino.finance/risk) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Lending positions withdrawable subject to pool utilization. Interest rate model creates steep rate increases at high utilization to incentivize repayment. No discretionary approvals needed. PYUSD liquidity is deep ($3.6B total supply). | 9 | 9 | Non-Improvable (optimal) | [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Sentora as vault manager fully disclosed with team backgrounds. Paxos as PYUSD custodian disclosed. Kamino as protocol layer disclosed. All third-party roles clearly defined. | 9 | 9 | Non-Improvable (optimal) | [Sentora](https://sentora.com/), [Paxos](https://www.paxos.com/pyusd) |

**Protocol Counterparty Subtotal:**
- Raw scores: 9+3+9+9+9 = 39
- Max raw: 5 x 9 = 45
- Weighted: (39/45) x 45 = 39.0

**Protocol Counterparty: 39.0/45 (86.7%)**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain redemption from lending pools. Risk Council can pause markets in emergency (protocol-wide, requires multisig). No arbitrary user blocking. All pauses visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [Kamino Docs](https://docs.kamino.finance) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Depends on pool utilization. September 2025 stablecoin utilization was 76.6%, meaning 23.4% of supplied assets are immediately available. High utilization delays exits. Interest rate model incentivizes repayment at high utilization. PYUSD has deep external liquidity ($3.6B supply) but in-pool liquidity is constrained by utilization. | 3 | 3 | Non-Improvable | [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates), [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No reported withdrawal delays or freezes for PYUSD markets on Kamino. No freeze events found in research. | 9 | 9 | Non-Improvable (optimal) | Exhaustive research found no incidents |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Caps exist but sized to balance risk and access. Interest rates spike at high utilization to incentivize repayment. Withdrawal caps are safety measures. No history of caps blocking exits. | 9 | 9 | Non-Improvable (optimal) | [Risk Docs](https://docs.kamino.finance/risk) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Exit liquidity is constrained by lending pool utilization. September 2025 showed 76.6% utilization, meaning only ~23% of supplied assets immediately available. During stress, borrowers may not repay quickly, creating exit delays. While PYUSD itself is stable, the lending pool mechanics create utilization-dependent exit constraints similar to other lending protocols. The protocol has not experienced a severe bank-run stress test comparable to Lido's July 2025 event. Per scoring principles, untested protocols should not score higher than battle-tested alternatives. | 3 | 3 | Non-Improvable | [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843), [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure lending with no lockups or vesting. Exit depends on pool liquidity only. | 9 | 9 | Non-Improvable (optimal) | [Kamino Lend Litepaper](https://docs.kamino.finance/kamino-lend-litepaper) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Primary redemption through Kamino pools always available (subject to utilization). Secondary markets optional. PYUSD has deep DEX liquidity on Solana. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | PYUSD total supply $3.6B with deep liquidity across Solana DEXs. Receipt tokens (vault shares) redeemable against pool assets. Adequate depth for normal operations. | 9 | 9 | Non-Improvable (optimal) | [CoinGecko PYUSD](https://www.coingecko.com/en/coins/paypal-usd) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Bank run causes temporary queues via high utilization. Interest rates escalate steeply to incentivize repayment. Poly-linear curve with up to 11 knot points provides gradual rate adjustment. No permanent loss expected but delays possible. Design includes buffers but significant queuing likely in bank-run. | 3 | 3 | Non-Improvable | [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates) |

**Liquidity Subtotal:**
- Raw scores: 9+3+9+9+3+9+9+9+3 = 63
- Max raw: 9 x 9 = 81
- Weighted: (63/81) x 45 = 35.0

**Liquidity: 35.0/45 (77.8%)**

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | The question evaluates receipt token (vault shares) behavior, not the underlying stablecoin. While PYUSD maintains its peg well, the vault's receipt tokens are subject to utilization-dependent redemption constraints. During high utilization periods (76.6% in Sept 2025), vault shares cannot be redeemed at full value immediately -- this is functionally a "depeg" from the underlying. The protocol has not experienced a severe stress test comparable to Lido's July 2025 event. Per scoring principles, untested protocols should score Mid (3) on resilience questions, while protocols with proven track records under stress can score Low (9). The vault mechanism is untested under extreme conditions. | 3 | 3 | Non-Improvable | [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Strategy has no crypto directional exposure. Vault lends PYUSD stablecoin. No leverage. Depositors receive PYUSD regardless of market conditions. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Kamino uses poly-linear interest rate curves with up to 11 knot points. Rates auto-increase with utilization. No history of prolonged >=95% utilization. Risk Council calibrates curves per market. September 2025 showed stable functioning during SOL volatility. | 9 | 9 | Non-Improvable (optimal) | [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. KRAF provides shock scenario analysis including uniform shocks, individual token shocks, correlated shocks, and historical event simulations. September 2025 report modeled 30% and 60% market drawdowns. Certora formal verification mathematically verified edge cases. | 9 | 9 | Non-Improvable (optimal) | [KRAF](https://docs.kamino.finance/risk/risk-assessment-framework), [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Not for this vault (lender side). Borrowers face liquidation risk. Vault benefits from continued lending capacity and liquidation execution. No leverage in vault strategy. | 9 | 9 | Non-Improvable (optimal) | [Liquidation Docs](https://docs.kamino.finance/products/borrow-lend/position-risk-and-liquidations) |

**Market Subtotal:**
- Raw scores: 3+9+9+9+9 = 39
- Max raw: 5 x 9 = 45
- Weighted: (39/45) x 45 = 39.0

**Market: 39.0/45 (86.7%)**

---

**STRATEGY TOTAL: 37.5 + 35.0 + 40.0 + 39.0 + 35.0 + 39.0 = 225.5/270 (83.5%)**

---

### OPERATIONS (30% Weight) - Score: 197.0/270 (73.0%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Currently a hybrid model. KMNO token governance planned for Q1 2026 but not yet activated on-chain. Risk Council provides operational oversight and parameter review. Multisig controls immediate changes and upgrades. Governance forum active for community discussion. Major decisions discussed publicly but ultimately executed by multisig/team. | 3 | 9 | **Improvable** | [Kamino Forum](https://gov.kamino.finance/), governance activation scheduled Q1 2026 |
| O-G-02 | How concentrated is voting power among top holders or delegates? | Highly concentrated. Top 10 wallets control over 70% of KMNO total supply. Over 80% held in a few wallets. Token distribution: 35% stakeholders/advisors, 20% core contributors, 35% community/grants, 10% liquidity/treasury. Significant insider holdings with vesting schedules still in progress. | 1 | 9 | **Improvable** | Multiple crypto analytics sources report >70% concentration, [Token Info](https://docs.kamino.finance/kmno/token-info), [Tokenomist](https://tokenomist.ai/kamino) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | No documented on-chain timelock for governance/parameter changes. Risk Council provides informal oversight and review of parameter changes by curators. Auto-deleverage has 72-hour margin call period (a form of delay). However, no formal veto mechanism with defined scope and triggers. | 3 | 9 | **Improvable** | [Gauntlet Curation](https://gov.kamino.finance/t/introducing-gauntlet-as-official-vault-curators/856), [Auto-Deleverage](https://docs.kamino.finance/risk/protocol-mechanisms/automated-deleverage) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Vault manager changes do not affect underlying Kamino markets. Withdrawals remain permissionless via on-chain redemption from lending pools regardless of vault curator status. | 9 | 9 | Non-Improvable (optimal) | V2 architecture separates Market Layer from Vault Layer |

**Governance Subtotal:**
- Raw scores: 3+1+3+9 = 16
- Max raw: 4 x 9 = 36
- Weighted: (16/36) x 67.5 = 30.0

**Governance: 30.0/67.5 (44.4%)**

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Kamino founders: Asaf Meir (CEO, ex-ConsenSys/Orbs), Tal Zelig (CTO, ex-Bancor/Orbs), Roy Keyes (COO, ex-Hubble Protocol). Sentora: Anthony DeMartino (CEO, ex-Coinbase Head of DeFi Trading), Jesus Rodriguez (CTO, ex-IntoTheBlock CEO). All identifiable with verifiable track records. | 9 | 9 | Non-Improvable (optimal) | [The Org - Kamino](https://theorg.com/org/kamino-finance/org-chart/asaf-meir), [Sentora](https://sentora.com/about), [The Block](https://www.theblock.co/post/353220/intotheblock-trident-merger-institutional-defi-platform-sentora-25-million-usd-series-a) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Kamino has a full engineering team with 35+ GitHub repos. Sentora has separate team from IntoTheBlock + Trident merger. Multiple vault curators (Gauntlet, Steakhouse, Allez Labs, MEV Capital, Sentora) provide redundancy. | 9 | 9 | Non-Improvable (optimal) | [GitHub Kamino-Finance](https://github.com/Kamino-Finance) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Kamino Finance based in Panama (founded 2022). Sentora is an incorporated entity formed from merger of IntoTheBlock and Trident Digital. Paxos Trust Company (NYDFS-regulated) issues PYUSD. | 9 | 9 | Non-Improvable (optimal) | [PitchBook](https://pitchbook.com/profiles/company/557633-98) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No enforcement actions found for Kamino Finance or Sentora. PYUSD is regulated (Paxos under NYDFS). No regulatory issues identified. | 9 | 9 | Non-Improvable (optimal) | Exhaustive research found no actions |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Risk Council monitors and can pause markets. In-house security team conducts regular penetration testing. However, no public 24/7 on-call SLA documented. No published incident runbooks with response times. | 3 | 9 | **Improvable** | [Solana Compass](https://solanacompass.com/projects/Kamino_Finance) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Active Discord, governance forum, and social media. December 2025 Jupiter Lend dispute saw rapid public engagement and communication from Kamino team. Support channels responsive. | 9 | 9 | Non-Improvable (optimal) | [Kamino Forum](https://gov.kamino.finance/) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Sentora: $25M Series A from New Form Capital, Tribe Capital, Ripple, Curved Ventures, Flare, Bankai Ventures. Kamino backed by investors (less detailed but acknowledged). Strategic partnerships with Chainlink, PayPal/Paxos, Apollo/Securitize disclosed. | 9 | 9 | Non-Improvable (optimal) | [The Block](https://www.theblock.co/post/353220/intotheblock-trident-merger-institutional-defi-platform-sentora-25-million-usd-series-a) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Sentora manages $3B+ across 300+ strategies across 60+ protocols and 16 blockchains. On Kamino, multiple vault curators operate. Sentora's institutional risk framework provides qualitative conflict controls but no hard-coded per-vault constraints preventing preferential allocation are documented. | 3 | 9 | **Improvable** | [Sentora](https://sentora.com/) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | No known collateral loss events. Sentora formed May 2025 from IntoTheBlock (since 2018) and Trident Digital. IntoTheBlock had clean track record. No loss incidents reported. | 9 | 9 | Non-Improvable (optimal) | [Sentora](https://sentora.com/), exhaustive research |

**Team & Legal Subtotal:**
- Raw scores: 9+9+9+9+3+9+9+3+9 = 69
- Max raw: 9 x 9 = 81
- Weighted: (69/81) x 67.5 = 57.5

**Team & Legal: 57.5/67.5 (85.2%)**

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive docs at docs.kamino.finance including Lend Litepaper, risk guides, oracle documentation, interest rate mechanics, liquidation docs. Updated for V2 in 2025. Monthly risk reports published on governance forum. | 9 | 9 | Non-Improvable (optimal) | [Kamino Docs](https://docs.kamino.finance) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Detailed liquidation documentation, interest rate mechanics, risk parameters, position risk simulation tools, and monthly risk insights reports with stress testing. Loss scenarios documented and quantified. | 9 | 9 | Non-Improvable (optimal) | [Position Risk & Liquidations](https://docs.kamino.finance/products/borrow-lend/position-risk-and-liquidations), [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Program IDs published: KLend mainnet (KLend2g3cP87fffoy8q1mQqGKjrxjC8boSyAYavgmjD). GitHub contains all contract source. SDK documentation includes addresses. | 9 | 9 | Non-Improvable (optimal) | [GitHub klend](https://github.com/Kamino-Finance/klend), [SDK Docs](https://docs.kamino.finance/build-on-kamino/sdk-and-smart-contracts) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Risk Council role documented at high level. Specific admin roles, permissions, and timelock configurations not fully detailed. No public change log for role/permission changes. Curator roles partially documented via governance forum posts. | 3 | 9 | **Improvable** | [Kamino Docs](https://docs.kamino.finance), [Gauntlet Post](https://gov.kamino.finance/t/introducing-gauntlet-as-official-vault-curators/856) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. All positions on-chain and visible via Risk Dashboard. PYUSD has Paxos attestations (monthly, by WithumSmith+Brown). Vault balances verifiable on Solana explorers. | 9 | 9 | Non-Improvable (optimal) | [PYUSD Transparency](https://www.paxos.com/pyusd-transparency), [Risk Dashboard](https://risk.kamino.finance/) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. Open source on GitHub. Verifiable builds ensure deployed programs match audited code. "Kamino Lend and Earn Vaults use Verifiable Builds, which guarantees that the programs running on Solana are the exact same versions published and audited on GitHub." | 9 | 9 | Non-Improvable (optimal) | [GitHub Kamino-Finance](https://github.com/Kamino-Finance), verifiable builds documented |

**Documentation Subtotal:**
- Raw scores: 9+9+9+3+9+9 = 48
- Max raw: 6 x 9 = 54
- Weighted: (48/54) x 67.5 = 60.0

**Documentation: 60.0/67.5 (88.9%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | No dedicated safety module or ring-fenced backstop fund disclosed. 10% KMNO token allocation for "liquidity & treasury" but no binding activation rules for user loss coverage. Bug bounty ($1.5M) indicates some reserves but no committed loss-coverage mechanism. | 3 | 9 | **Improvable** | [Token Info](https://docs.kamino.finance/kmno/token-info) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Treasury size not publicly disclosed. KMNO treasury allocation is 10% of token supply (~1B KMNO). At current KMNO price, this has some value but composition and liquid reserves are unknown. Bug bounty ($1.5M) and daily fee revenue ($300K+) suggest operational reserves but no published reserve target. | 3 | 9 | **Source Missing** | [Token Info](https://docs.kamino.finance/kmno/token-info), no public treasury balance disclosure |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong for both entities. Sentora has $25M Series A. Kamino generates $300K+ daily fees ($57M annualized) with $13.23M 30-day annualized revenue. Protocol is revenue-positive. Combined entities well-funded for >24 months. | 9 | 9 | Non-Improvable (optimal) | [The Block](https://www.theblock.co/post/353220/intotheblock-trident-merger-institutional-defi-platform-sentora-25-million-usd-series-a), DeFiLlama fee data |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Kamino maintained dominant Solana position through market fluctuations. TVL grew from ~$2B to $3.7B peak in October 2025, dropped to $2.33B after December 2025 Jupiter dispute and market conditions, then stabilized around $2.7B. Revenue remains strong at $300K+ daily. September 2025 SOL drawdown (-25%) handled without bad debt. February 5-6, 2026 stress event (SOL -18%) triggered 55,649 liquidations ($19.36M collateral seized) across all Kamino markets with zero bad debt generated. The Sentora PYUSD vault TVL declined from ~$189M to ~$38M primarily due to PayPal incentive tapering, not security failures. | 9 | 9 | Non-Improvable (optimal) | [DeFiLlama](https://defillama.com/protocol/kamino), [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | On-chain contracts would continue operating. Withdrawals remain permissionless. Users can interact directly with contracts via documented SDK. However, Risk Council and governance would be impaired. Vault curation would stop but underlying lending markets continue. Open source code allows community maintenance. | 9 | 9 | Non-Improvable (optimal) | [Kamino Docs](https://docs.kamino.finance), open source codebase, permissionless withdrawal architecture |

**Financial Resilience Subtotal:**
- Raw scores: 3+3+9+9+9 = 33
- Max raw: 5 x 9 = 45
- Weighted: (33/45) x 67.5 = 49.5

**Financial Resilience: 49.5/67.5 (73.3%)**

---

**OPERATIONS TOTAL: 30.0 + 57.5 + 60.0 + 49.5 = 197.0/270 (73.0%)**

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Raw Max | Weighted Score | Max Weighted |
|----------|-------------|-----------|---------|----------------|--------------|
| **Security** | Smart Contract Security | 79 | 99 | 143.6 | 180 |
| | Key Management | 44 | 72 | 110.0 | 180 |
| | **Security Total** | **123** | **171** | **253.6** | **360** |
| **Strategy** | Protocol Mechanics | 60 | 72 | 37.5 | 45 |
| | Collateral | 21 | 27 | 35.0 | 45 |
| | Infra Counterparty | 48 | 54 | 40.0 | 45 |
| | Protocol Counterparty | 39 | 45 | 39.0 | 45 |
| | Liquidity | 63 | 81 | 35.0 | 45 |
| | Market | 39 | 45 | 39.0 | 45 |
| | **Strategy Total** | **270** | **324** | **225.5** | **270** |
| **Operations** | Governance | 16 | 36 | 30.0 | 67.5 |
| | Team & Legal | 69 | 81 | 57.5 | 67.5 |
| | Documentation | 48 | 54 | 60.0 | 67.5 |
| | Financial Resilience | 33 | 45 | 49.5 | 67.5 |
| | **Operations Total** | **166** | **216** | **197.0** | **270** |
| **TOTAL** | | | | **676.1** | **900** |

---
