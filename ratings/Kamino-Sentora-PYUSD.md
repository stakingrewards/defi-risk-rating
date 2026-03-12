# Kamino Finance - Sentora PYUSD Vault Risk Rating

**Rating Date**: 2026-03-10
**Final Grade**: B-
**Total Score**: 676.1/900 points

---

## Detailed Analysis

### SECURITY (40% Weight) - Score: 253.6/360 (70.4%)

#### Smart Contract Security (20% weight, 180 max points)

**[S-SC-01] Have all core contracts that hold or route funds been independently audited?** (Deal Breaker)
- **Answer**: Yes. Kamino has undergone 18+ external audits covering core lending (KLend), vault (KVault), farming (KFarms), liquidity, and oracle aggregator (Scope) contracts. Auditing firms include OtterSec, Offside Labs, Sec3, Certora, Ackee Blockchain, OpenSec, and Rx. Additionally, 3+ formal verifications completed by Certora (Lend, Vault, Limo). Most recent: Certora formal verification February 2025.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [GitHub Audits](https://github.com/Kamino-Finance/audits), [Certora Report](https://www.certora.com/reports/kamino-lending-security-report), [Immunefi](https://immunefi.com/bug-bounty/kamino/) listing 17 assets in scope
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-SC-02] Who performed the most recent audit and what is their reputation tier?**
- **Answer**: Most recent formal engagement: Certora formal verification (November 2024 - February 2025). Certora is not on the SR tier list but is an industry-recognized leader in formal verification. Ackee Blockchain, which has also audited Kamino, is listed as Tier-1 on the SR auditor tiers. Multiple Solana-ecosystem auditors (OtterSec, Offside Labs, Sec3) not on the SR tier list have also audited the protocol.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Certora Blog](https://www.certora.com/blog/securing-kamino-lending), [GitHub Audits](https://github.com/Kamino-Finance/audits)
- **Evidence Status**: Verified
- **Comments**: Ackee Blockchain is Tier-1 per SR list. The Low (9) criteria require "at least one most recent audit by a Tier-1 auditor" which is satisfied.
- **Path to Potential**: N/A

**[S-SC-03] Have upgrades to core contracts been followed by new audits?**
- **Answer**: Yes. Kamino V2 (May 2025) accompanied by Certora audits of Lend, Vault, and Limo. Chainlink Data Streams oracle integration (April 2025) had Multi-Price Oracle System audited by Certora and Offside Labs before deployment. Continuous audit program maintained.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [GitHub Audits](https://github.com/Kamino-Finance/audits), [Chainlink Integration Announcement](https://gov.kamino.finance/t/kamino-integrates-chainlink-data-streams-for-high-quality-low-latency-market-data/550)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-SC-04] Have all critical and high-severity audit findings been fully remediated and re-verified?**
- **Answer**: Yes. Certora formal verification found precision loss issue in exchange rate calculations, proactively patched despite not being currently exploitable. All critical findings across 18+ audits resolved. Zero critical vulnerabilities per security page.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Certora Blog](https://www.certora.com/blog/securing-kamino-lending), [GitHub Audits](https://github.com/Kamino-Finance/audits)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-SC-05] Are core contracts upgradeable and how tightly are upgrades constrained?**
- **Answer**: Kamino contracts on Solana are upgradeable (standard for Solana programs). No documented timelock mechanism exists for upgrades. Research across official docs, governance forum, and third-party sources found no evidence of a timelock delay. The December 2, 2025 incident where Kamino updated smart contracts overnight to block Jupiter Lend's refinance tool demonstrates that upgrades can be executed rapidly without public advance notice or governance approval. Upgrade constraints are undocumented.
- **Current Score**: 1
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: Multiple sources confirm no documented timelock. Jupiter Lend blocking incident: [The Defiant](https://thedefiant.io/news/defi/kamino-blocks-jupiter-lend-refinance), [Blockworks](https://blockworks.co/news/jup-lend-vs-kamino)
- **Evidence Status**: Verified absence of timelock
- **Comments**: The Jupiter Lend incident provides concrete evidence that contract changes can be deployed without a public timelock or advance governance notice. This is the single most impactful governance gap identified.
- **Path to Potential**: Implement and document timelock >=24h for all core contract upgrades with public on-chain visibility

**[S-SC-06] Has any on-chain exploit or critical bug affecting user funds occurred?** (Deal Breaker)
- **Answer**: No confirmed exploits causing user fund loss. Clean record since founding in 2022 (3+ years). Security page states "18 full audits completed with 0 critical vulnerabilities." No incidents found on Rekt.news or security incident databases.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Security](https://kamino.com/security), [CertiK Skynet](https://skynet.certik.com/projects/kamino-finance), exhaustive web search
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-SC-07] Has any confirmed rug-pull event occurred?** (Deal Breaker)
- **Answer**: No rug-pull events. 3+ year track record. Team publicly identified. Open source with verifiable builds.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Finance](https://kamino.com/), team publicly identified, no allegations found
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-SC-08] Were there reductions to the timelock delay that weaken governance protections?**
- **Answer**: No documented timelock exists to reduce. No evidence of any governance protection mechanism being weakened. The absence of a timelock is penalized under S-SC-05; this question specifically addresses reductions to existing mechanisms.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (no reductions occurred)
- **Evidence**: Exhaustive research found no evidence of timelock reductions
- **Evidence Status**: Verified absence
- **Path to Potential**: N/A

**[S-SC-09] Does the protocol run an active bug-bounty via a reputable platform?**
- **Answer**: Yes. Active Immunefi bounty launched October 6, 2025. Maximum payout $1,500,000 for critical smart contract bugs. 17 assets in scope (KLend, KVault, KFarms, Liquidity, Oracle Aggregator). Critical: 10% of affected funds up to $1.5M, min $150K. High: up to $100K. Medium: $10K. Payments in USDC.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Immunefi - Kamino](https://immunefi.com/bug-bounty/kamino/)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-SC-10] Are real-time security monitoring and alerting systems in place?**
- **Answer**: Kamino has the Risk Assessment Framework (KRAF) providing dashboards with risk overview, loan analysis, volatility analysis, liquidity risk, and shock scenarios at risk.kamino.finance. In-house security team conducts regular penetration testing. However, no evidence of a reputable third-party 24/7 monitoring provider (Hypernative, Blockaid, etc.) was found. KRAF appears to be a risk analytics tool rather than a real-time security monitoring system with automated alerting and on-call response.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Risk Dashboard](https://risk.kamino.finance/), [KRAF Docs](https://docs.kamino.finance/risk/risk-assessment-framework)
- **Evidence Status**: Partial -- KRAF dashboard verified, no evidence of 24/7 automated alerting via reputable provider
- **Path to Potential**: Integrate reputable 24/7 monitoring provider (Hypernative, Blockaid) with on-call response

**[S-SC-11] Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts?**
- **Answer**: Kamino has emergency pause/shutdown mechanisms. Risk Council can trigger auto-deleveraging via multi-sig vote with 72-hour margin call period. However, auto-deleverage is currently manual (Risk Council vote), not automated. Documentation states future automation planned but not yet implemented. Manual triggers exist with documented procedures but no automatic invariant-breach triggers.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Auto-Deleverage Docs](https://docs.kamino.finance/risk/protocol-mechanisms/automated-deleverage)
- **Evidence Status**: Verified -- manual triggers confirmed, automated not implemented
- **Path to Potential**: Implement automated on-chain circuit breakers

**Smart Contract Security Subtotal:**
- Raw scores: 9+9+9+9+1+9+9+9+9+3+3 = 79
- Max raw: 11 x 9 = 99
- Weighted: (79/99) x 180 = 143.6

**Smart Contract Security: 143.6/180 (79.8%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

**[S-KM-01] Who controls admin and upgrade keys for contracts holding user funds?**
- **Answer**: Kamino uses a multisig for administrative operations. Multisig address identified as 6hhBGCtmg7tPWUSgp3LG6X2rsmYWAc4tNsA6G4CnfQbM. Critical details are missing: signer identities, threshold (M-of-N), independence of signers not publicly documented. KMNO on-chain governance not yet activated (scheduled Q1 2026). Risk Council has emergency powers. Admin configuration change history is not publicly documented.
- **Current Score**: 1
- **Potential Score**: 9
- **Classification**: Source Missing
- **Evidence**: Multisig address found via [GitHub](https://github.com/Kamino-Finance). Signer details, threshold, and change history not found in official docs, governance forum, or third-party sources.
- **Evidence Status**: Claimed but unverified -- multisig exists but configuration undisclosed
- **Comments**: Per criteria, "change history unknown" triggers High (1). The multisig exists but transparency is insufficient.
- **Path to Potential**: Publicly document multisig signer identities, threshold, independence, and maintain public change log

**[S-KM-02] Can any single key move user funds or upgrade custody contracts?** (Deal Breaker)
- **Answer**: No evidence of single-key control. Multisig required for admin actions. User assets held in non-custodial lending market contracts. Vault curators have allocation discretion but cannot directly withdraw user funds. Risk Council operates via multi-sig vote.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Docs](https://docs.kamino.finance), non-custodial contract architecture, multiple sources confirm multisig
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-KM-03] How decentralized and robust is the multisig for critical actions?**
- **Answer**: Multisig configuration not comprehensively disclosed. Third-party analysis (Exponential DeFi) reported fewer than 4 signers. Signer identities, independence, and threshold not publicly documented. This suggests a small multisig (possibly 2-of-3 or similar) with partial independence.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Exponential DeFi](https://exponential.fi/protocols/kamino-lend/) reported <4 signers
- **Evidence Status**: Limited third-party data, no official disclosure
- **Comments**: Scored Mid (3) based on evidence of a small but functioning multisig. "2-of-4 or 3-of-3 with partial independence" best matches available evidence.
- **Path to Potential**: Expand to >=3-of-5 with >=3 independent entities, publish configuration

**[S-KM-04] How constrained are pause, blocklist and withdrawal-control permissions?**
- **Answer**: Risk Council can pause markets via multisig. Auto-deleverage provides 72-hour margin call. No evidence of arbitrary address-level withdrawal censorship. Withdrawals permissionless based on pool liquidity. December 2025 Jupiter blocking restricted protocol interactions, not individual user withdrawals.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Auto-Deleverage Docs](https://docs.kamino.finance/risk/protocol-mechanisms/automated-deleverage)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-KM-05] Are all user assets held in non-custodial smart contracts?**
- **Answer**: Yes. All user assets in non-custodial on-chain lending contracts on Solana. No off-chain custody. Verifiable builds ensure deployed code matches audited source.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Lend Litepaper](https://docs.kamino.finance/kamino-lend-litepaper), [GitHub klend](https://github.com/Kamino-Finance/klend)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-KM-06] Are user funds fully segregated from treasury and operational wallets?**
- **Answer**: Yes. User funds in lending pool contracts, segregated from KMNO treasury (10% token allocation). Protocol revenue accrues separately. No evidence of co-mingling.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Token Info](https://docs.kamino.finance/kmno/token-info)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-KM-07] What are the whitelisted protocols the vault strategy can interact with?** (Vault question)
- **Answer**: Sentora PYUSD vault deploys exclusively into Kamino's own lending markets. Risk Council reviews all parameter changes from curators. Whitelist effectively limited to Kamino internal markets. However, on-chain enforcement mechanism and market addition governance not documented with timelock. Curator has allocation discretion within the vault.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Gauntlet Vault Curation](https://gov.kamino.finance/t/introducing-gauntlet-as-official-vault-curators/856) -- "Any parameter changes are reviewed by Kamino's Risk Council"
- **Evidence Status**: Partial -- curator constraint exists but enforcement not documented with timelock
- **Path to Potential**: Document and enforce on-chain whitelist with governance/multisig and timelock

**[S-KM-08] Is there a tested incident playbook for admin-key compromise or signer loss?**
- **Answer**: No evidence found. No public incident response playbook, key rotation procedures, emergency response SLAs, or tabletop exercises documented.
- **Current Score**: 1
- **Potential Score**: 9
- **Classification**: Source Missing
- **Evidence**: Exhaustive search of docs, governance forum, GitHub, third-party sources found nothing
- **Evidence Status**: Missing
- **Path to Potential**: Publish and test incident response playbook

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

**[ST-PM-01] What are the sources of yield and is it aligned with the mandate?**
- **Answer**: Yield sources: (1) PYUSD lending interest from borrowers in Kamino markets, (2) PayPal/Paxos PYUSD growth incentives ($700K/month across Kamino). Both sources are mandate-aligned for a stablecoin lending strategy. September 2025 data showed stablecoin supply rates of 4.7% (organic) with incentives boosting total APY to approximately 14%.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Blockworks](https://blockworks.co/news/kamino-seeing-benefits-from-liquidity-incentives-on-pyusd), [Kamino Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-02] Under which conditions does net yield become negative or cause loss?**
- **Answer**: Loss limited to tail scenarios: smart contract exploit, oracle failure, severe collateral liquidation cascade in Kamino markets, or PYUSD depeg. Vault is on the lending side (not borrowing), so no direct liquidation risk. Overcollateralized lending model provides buffer. September 2025 stress test showed $10.6M potential bad debt at 30% market drawdown on $2.8B TVL (~0.4%).
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843), [Oracle Docs](https://docs.kamino.finance/risk/oracles)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-03] Is leverage or rehypothecation used and up to what effective level?**
- **Answer**: No leverage or rehypothecation. Vault lends PYUSD to borrowers. Effective leverage 1.0x. Borrowers may leverage but the vault itself is unleveraged.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Lend Litepaper](https://docs.kamino.finance/kamino-lend-litepaper)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-04] Are there automated mechanics to prevent Liquidation Events?**
- **Answer**: N/A -- Vault is on the lending side, not borrowing. No direct liquidation risk for depositors. Borrower liquidations handled by Kamino's soft liquidation mechanism (20% partial, 2-10% penalty).
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A
- **Evidence**: [Liquidation Docs](https://docs.kamino.finance/products/borrow-lend/position-risk-and-liquidations)
- **Evidence Status**: N/A

**[ST-PM-05] Has this strategy or a close variant ever experienced negative yield?** (Deal Breaker)
- **Answer**: No permanent loss events for PYUSD lending on Kamino. Clean track record since vault launch. September 2025 showed 2,289 liquidation events but all executed efficiently without generating bad debt for lenders.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-06] Is a risk framework for vault curation or protocol mechanics documented?** (Vault question)
- **Answer**: Yes. Sentora provides institutional risk framework built from IntoTheBlock's 1,000+ risk models and 300+ strategies across 60+ protocols. Kamino has KRAF (Kamino Risk Assessment Framework) with comprehensive dashboard. Quantitative limits for utilization, shock scenarios, and per-asset risk tiers are defined.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Sentora](https://sentora.com/), [KRAF Docs](https://docs.kamino.finance/risk/risk-assessment-framework)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-07] Is current yield sustainable relative to underlying economics?**
- **Answer**: Approximately 14% APY with organic stablecoin supply rates around 4.7%. PayPal incentives contribute approximately $700K/month. This suggests 55-65% of yield may be incentive-driven. Borrowing demand (utilization 76.6%) provides organic base but incentive dependency is material. Incentives appear to be slowly tapering.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Blockworks](https://blockworks.co/news/kamino-seeing-benefits-from-liquidity-incentives-on-pyusd), [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843)
- **Evidence Status**: Verified
- **Comments**: 55-65% incentive dependency falls within the Mid range (30-70%). Organic demand is growing but incentive removal would approximately halve returns.
- **Path to Potential**: Demonstrate yield sustainability without incentives as PYUSD adoption grows organically

**[ST-PM-08] Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative?**
- **Answer**: Yes. PYUSD is highly liquid (total supply $3.6B). Withdrawal depends on lending pool utilization. Interest rate model creates steep rate increases at high utilization, incentivizing borrower repayment. Pool utilization was 76.6% in September 2025, leaving adequate buffer.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-09] Does the strategy rely on a spread, peg, or funding rate that can invert?**
- **Answer**: Strategy relies on PYUSD maintaining peg to USD. PYUSD is Paxos-issued, NYDFS-regulated, with monthly attestations (now by WithumSmith+Brown). Historical all-time low was approximately $0.955 during stress, with quick recovery. Peg risk is low for a regulated stablecoin but non-zero -- contributes minority of risk.
- **Current Score**: 3
- **Potential Score**: 3
- **Classification**: Non-Improvable (inherent to stablecoin lending strategy)
- **Evidence**: [PYUSD Transparency](https://www.paxos.com/pyusd-transparency), price history data
- **Evidence Status**: Verified
- **Path to Potential**: N/A -- inherent to PYUSD strategy

**Protocol Mechanics Subtotal:**
- Raw scores (8 applicable): 9+9+9+9+9+3+9+3 = 60
- Max raw: 8 x 9 = 72
- Weighted: (60/72) x 45 = 37.5

**Protocol Mechanics: 37.5/45 (83.3%)**

---

#### Collateral (5% weight, 45 max points)

**[ST-C-01] Which assets are accepted as collateral and how are they risk rated?**
- **Answer**: Kamino accepts blue-chip collateral with risk tiering: General (SOL, stablecoins), Isolated Collateral, and Isolated Debt categories. Per-asset LTVs: SOL 80%, LSTs 90-95% in eMode. Deposit/borrow caps adjusted based on volatility, liquidity, and security metrics. PYUSD itself is a regulated stablecoin.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Position Risk & Liquidations](https://docs.kamino.finance/products/borrow-lend/position-risk-and-liquidations)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-C-02] How did each collateral behave versus its underlying during past stress or depegs?**
- **Answer**: This question evaluates vault share (receipt token) behavior versus the underlying PYUSD. While PYUSD itself maintained its peg during September 2025 stress, vault shares are subject to utilization-dependent redemption constraints. At 76.6% utilization, only ~23% of supplied assets are immediately available for withdrawal. During high utilization periods, vault shares effectively trade at a discount to NAV since they cannot be redeemed at full value immediately. The vault has not experienced a severe stress test comparable to proven protocols. Per scoring principles, untested vault share behavior should score Mid (3).
- **Current Score**: 3
- **Potential Score**: 3
- **Classification**: Non-Improvable (inherent to lending vault design; untested under stress)
- **Evidence**: [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843), [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates)
- **Evidence Status**: Verified
- **Comments**: Vault share redemption is constrained by pool utilization. This is functionally similar to a "depeg" from underlying when utilization is high. Untested resilience should not score higher than demonstrated resilience.
- **Path to Potential**: N/A -- inherent to lending vault mechanics and requires real-world stress testing

**[ST-C-03] How is validator or slashing risk handled for staking-based collaterals?**
- **Answer**: N/A -- Vault holds PYUSD stablecoin, not staking derivatives. Solana does not currently have slashing for validators.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A

**[ST-C-04] What share of TVL relies on bridged or wrapped assets?**
- **Answer**: PYUSD is native on Solana (issued directly by Paxos via the Solana Token Extensions framework). Not bridged. Approximately 0% bridged asset exposure for the vault.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [PayPal PYUSD on Solana](https://newsroom.paypal-corp.com/2024-05-29-PayPal-USD-Stablecoin-Now-Available-on-Solana-Blockchain)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**Collateral Subtotal:**
- Raw scores (3 applicable): 9+3+9 = 21
- Max raw: 3 x 9 = 27
- Weighted: (21/27) x 45 = 35.0

**Collateral: 35.0/45 (77.8%)**

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

**[ST-IC-01] Which chains, bridges, oracles, wallets and CEXs does the strategy depend on?**
- **Answer**: Solana (Tier-0), Pyth Network (Tier-0), Chainlink Data Streams (Tier-0). No bridges. No CEX dependency. Paxos (NYDFS-regulated) for PYUSD issuance/redemption. All critical dependencies are Tier-0.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Oracle Docs](https://docs.kamino.finance/risk/oracles), [Chainlink Integration](https://gov.kamino.finance/t/kamino-integrates-chainlink-data-streams-for-high-quality-low-latency-market-data/550)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-IC-02] How redundant and battle-tested are the oracle and bridge setups?**
- **Answer**: Multi-oracle system aggregates Pyth + Chainlink with cross-verification. TWAP/EWMA for manipulation resistance. Price bands (1% for USD stables). Double-audited by Certora and Offside Labs. No bridge dependency. Both oracles are Tier-0.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Oracle Docs](https://docs.kamino.finance/risk/oracles), [Scope GitHub](https://github.com/Kamino-Finance/scope)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-IC-03] Are off-chain infrastructure providers certified by standard IT security audits?**
- **Answer**: Paxos (PYUSD issuer) is NYDFS-regulated with regular compliance audits. Kamino team SOC2/ISO27001 certifications not disclosed. Sentora certifications not publicly available.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Source Missing
- **Evidence**: [Paxos](https://www.paxos.com/pyusd) (regulatory status verified), Kamino/Sentora certifications not found
- **Evidence Status**: Partial -- Paxos regulatory compliance verified, Kamino/Sentora IT security certifications unverified
- **Path to Potential**: Obtain and publish SOC2/ISO27001 for Kamino and Sentora operations

**[ST-IC-04] How did these infra components behave in past outages or chain incidents?**
- **Answer**: Solana's last major outage was February 6, 2025 (approximately 5 hours). Since then, 12 months of continuous uptime achieved. No Kamino-specific infrastructure failures reported during that incident or subsequently. Oracle system maintained integrity.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Solana Status](https://status.solana.com/), [Helius Blog](https://www.helius.dev/blog/solana-outages-complete-history)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-IC-05] Has the base chain recently halted block production or experienced consensus failure?**
- **Answer**: Solana's last major halt was February 6, 2025 (approximately 5 hours). As of March 2026, the chain has achieved over 13 months of continuous uptime with no further consensus failures. Firedancer client diversity further reducing halt risk. The February 2025 outage is now outside the 12-month lookback window.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Solana Status](https://status.solana.com/), [Solana Status Uptime History](https://status.solana.com/uptime)
- **Evidence Status**: Verified
- **Comments**: The February 2025 outage is now >12 months ago (outside the lookback window). No new chain halts since. Scores Low (9) per criteria.
- **Path to Potential**: N/A

**[ST-IC-06] Has the validator set experienced slashing events that could impact staked collateral?**
- **Answer**: N/A -- PYUSD vault does not hold staking derivatives. Solana does not currently implement slashing.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A

**[ST-IC-07] Are validators diverse geographically and by operator?**
- **Answer**: N/A -- Not applicable for PYUSD stablecoin lending vault.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A

**[ST-IC-08] Can any single infra component failure alone block withdrawals or cause losses?**
- **Answer**: No single point of failure identified. Withdrawals are permissionless on-chain. Oracle failure: multi-oracle fallback. Chain halt: temporary. Paxos failure: PYUSD has independent redemption path. Users can interact directly with contracts.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Docs](https://docs.kamino.finance)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**Infrastructure Counterparty Subtotal:**
- Raw scores (6 applicable): 9+9+3+9+9+9 = 48
- Max raw: 6 x 9 = 54
- Weighted: (48/54) x 45 = 40.0

**Infrastructure Counterparty: 40.0/45 (88.9%)**

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

**[ST-PC-01] Into which external protocols, CEXs or RWA platforms is collateral deployed?**
- **Answer**: Kamino Lend markets only. No external protocol deployment. PYUSD backed by Paxos (US Treasuries + cash deposits). Apollo ACRED RWA integration announced but separate from this vault.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Lend](https://kamino.com/lend/sentora-pyusd)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PC-02] Are revenue-share or incentive arrangements documented and do they create conflicts?**
- **Answer**: PayPal/Paxos PYUSD incentives ($700K/month) are publicly acknowledged. Kamino vault fee structure partially documented -- "Zero management & performance fees for all strategies except Re7's vault" per June 2025 data. Sentora-specific fee terms not fully transparent.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Blockworks](https://blockworks.co/news/kamino-seeing-benefits-from-liquidity-incentives-on-pyusd), [OnChain Times](https://www.onchaintimes.com/kamino-v2-composability-at-scale/)
- **Evidence Status**: Partial -- incentive existence verified, specific terms incomplete
- **Path to Potential**: Publish complete fee breakdown including Sentora management/performance fees

**[ST-PC-03] Are there hard limits and rebalancing rules per counterparty?**
- **Answer**: Kamino enforces per-asset deposit and borrow caps. Dynamic limits adjusted by Risk Council based on KRAF analytics. Market-level exposure limits documented. Caps auto-adjusted based on risk signals.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Risk Docs](https://docs.kamino.finance/risk)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PC-04] How quickly and safely can positions be unwound from each counterparty?**
- **Answer**: Lending positions withdrawable subject to pool utilization. Interest rate model creates steep rate increases at high utilization to incentivize repayment. No discretionary approvals needed. PYUSD liquidity is deep ($3.6B total supply).
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PC-05] Are third-party validators, custody providers or asset managers disclosed?** (Deal Breaker)
- **Answer**: Sentora as vault manager fully disclosed with team backgrounds. Paxos as PYUSD custodian disclosed. Kamino as protocol layer disclosed. All third-party roles clearly defined.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Sentora](https://sentora.com/), [Paxos](https://www.paxos.com/pyusd)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**Protocol Counterparty Subtotal:**
- Raw scores: 9+3+9+9+9 = 39
- Max raw: 5 x 9 = 45
- Weighted: (39/45) x 45 = 39.0

**Protocol Counterparty: 39.0/45 (86.7%)**

---

#### Liquidity (5% weight, 45 max points)

**[ST-L-01] How are withdrawals executed and can they be paused, blocked or delayed?**
- **Answer**: Permissionless on-chain redemption from lending pools. Risk Council can pause markets in emergency (protocol-wide, requires multisig). No arbitrary user blocking. All pauses visible on-chain.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Docs](https://docs.kamino.finance)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-02] Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time?**
- **Answer**: Depends on pool utilization. September 2025 stablecoin utilization was 76.6%, meaning 23.4% of supplied assets are immediately available. High utilization delays exits. Interest rate model incentivizes repayment at high utilization. PYUSD has deep external liquidity ($3.6B supply) but in-pool liquidity is constrained by utilization.
- **Current Score**: 3
- **Potential Score**: 3
- **Classification**: Non-Improvable (inherent to lending protocol design)
- **Evidence**: [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates), [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843)
- **Evidence Status**: Verified
- **Path to Potential**: N/A -- inherent to lending model

**[ST-L-03] Have there been past withdrawal delays, queues or freezes?**
- **Answer**: No reported withdrawal delays or freezes for PYUSD markets on Kamino. No freeze events found in research.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: Exhaustive research found no incidents
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-04] Do caps or limits restrict timely redemptions during high utilization?**
- **Answer**: Caps exist but sized to balance risk and access. Interest rates spike at high utilization to incentivize repayment. Withdrawal caps are safety measures. No history of caps blocking exits.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Risk Docs](https://docs.kamino.finance/risk)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-05] How does exit liquidity behave during volatility and network congestion?**
- **Answer**: Exit liquidity is constrained by lending pool utilization. September 2025 showed 76.6% utilization, meaning only ~23% of supplied assets immediately available. During stress, borrowers may not repay quickly, creating exit delays. While PYUSD itself is stable, the lending pool mechanics create utilization-dependent exit constraints similar to other lending protocols. The protocol has not experienced a severe bank-run stress test comparable to Lido's July 2025 event. Per scoring principles, untested protocols should not score higher than battle-tested alternatives.
- **Current Score**: 3
- **Potential Score**: 3
- **Classification**: Non-Improvable (inherent to lending pool design)
- **Evidence**: [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843), [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates)
- **Evidence Status**: Verified
- **Comments**: Utilization-based exit constraints are inherent to lending pool design. High utilization periods would stress exit liquidity regardless of stablecoin stability.
- **Path to Potential**: N/A -- inherent to lending model

**[ST-L-06] Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period?**
- **Answer**: No. Pure lending with no lockups or vesting. Exit depends on pool liquidity only.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Lend Litepaper](https://docs.kamino.finance/kamino-lend-litepaper)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-07] Does redemption depend on secondary-market liquidity and is it sufficient?**
- **Answer**: Primary redemption through Kamino pools always available (subject to utilization). Secondary markets optional. PYUSD has deep DEX liquidity on Solana.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: Vault mechanics
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-08] What is the liquidity depth of collateral and receipt tokens?**
- **Answer**: PYUSD total supply $3.6B with deep liquidity across Solana DEXs. Receipt tokens (vault shares) redeemable against pool assets. Adequate depth for normal operations.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [CoinGecko PYUSD](https://www.coingecko.com/en/coins/paypal-usd)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-09] What is the risk of bank-run scenarios under full utilization?**
- **Answer**: Bank run causes temporary queues via high utilization. Interest rates escalate steeply to incentivize repayment. Poly-linear curve with up to 11 knot points provides gradual rate adjustment. No permanent loss expected but delays possible. Design includes buffers but significant queuing likely in bank-run.
- **Current Score**: 3
- **Potential Score**: 3
- **Classification**: Non-Improvable (inherent to lending pool design)
- **Evidence**: [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates)
- **Evidence Status**: Verified
- **Path to Potential**: N/A -- inherent to lending model

**Liquidity Subtotal:**
- Raw scores: 9+3+9+9+3+9+9+9+3 = 63
- Max raw: 9 x 9 = 81
- Weighted: (63/81) x 45 = 35.0

**Liquidity: 35.0/45 (77.8%)**

---

#### Market (5% weight, 45 max points)

**[ST-M-01] How has the LST or receipt token peg performed under market stress?**
- **Answer**: The question evaluates receipt token (vault shares) behavior, not the underlying stablecoin. While PYUSD maintains its peg well, the vault's receipt tokens are subject to utilization-dependent redemption constraints. During high utilization periods (76.6% in Sept 2025), vault shares cannot be redeemed at full value immediately -- this is functionally a "depeg" from the underlying. The protocol has not experienced a severe stress test comparable to Lido's July 2025 event. Per scoring principles, untested protocols should score Mid (3) on resilience questions, while protocols with proven track records under stress can score Low (9). The vault mechanism is untested under extreme conditions.
- **Current Score**: 3
- **Potential Score**: 3
- **Classification**: Non-Improvable (inherent to lending vault design; untested under stress)
- **Evidence**: [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843)
- **Evidence Status**: Verified
- **Comments**: Scoring reflects that vault share redemption is constrained by pool utilization, which has not been stress-tested. Untested resilience should not score higher than demonstrated resilience.
- **Path to Potential**: N/A -- inherent to lending vault mechanics and requires real-world stress testing

**[ST-M-02] How likely can adverse crypto market moves cause permanent losses due to directional exposure?**
- **Answer**: Strategy has no crypto directional exposure. Vault lends PYUSD stablecoin. No leverage. Depositors receive PYUSD regardless of market conditions.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: Vault mechanics
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-M-03] Are interest rate/incentive models robust during TVL shifts or volatility spikes?**
- **Answer**: Kamino uses poly-linear interest rate curves with up to 11 knot points. Rates auto-increase with utilization. No history of prolonged >=95% utilization. Risk Council calibrates curves per market. September 2025 showed stable functioning during SOL volatility.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-M-04] Have historic scenarios with high market volatility been explicitly modeled?**
- **Answer**: Yes. KRAF provides shock scenario analysis including uniform shocks, individual token shocks, correlated shocks, and historical event simulations. September 2025 report modeled 30% and 60% market drawdowns. Certora formal verification mathematically verified edge cases.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [KRAF](https://docs.kamino.finance/risk/risk-assessment-framework), [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-M-05] Can sharp price moves trigger forced liquidations that crystallize losses?**
- **Answer**: Not for this vault (lender side). Borrowers face liquidation risk. Vault benefits from continued lending capacity and liquidation execution. No leverage in vault strategy.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Liquidation Docs](https://docs.kamino.finance/products/borrow-lend/position-risk-and-liquidations)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

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

**[O-G-01] What governance model controls protocol changes and upgrades?**
- **Answer**: Currently a hybrid model. KMNO token governance planned for Q1 2026 but not yet activated on-chain. Risk Council provides operational oversight and parameter review. Multisig controls immediate changes and upgrades. Governance forum active for community discussion. Major decisions discussed publicly but ultimately executed by multisig/team.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Kamino Forum](https://gov.kamino.finance/), governance activation scheduled Q1 2026
- **Evidence Status**: Verified -- on-chain governance not yet active
- **Comments**: Mid (3) appropriate: hybrid model where governance covers major changes via forum discussion but multisig executes upgrades within documented bounds (Risk Council oversight).
- **Path to Potential**: Activate on-chain KMNO governance with clearly defined rules

**[O-G-02] How concentrated is voting power among top holders or delegates?**
- **Answer**: Highly concentrated. Top 10 wallets control over 70% of KMNO total supply. Over 80% held in a few wallets. Token distribution: 35% stakeholders/advisors, 20% core contributors, 35% community/grants, 10% liquidity/treasury. Significant insider holdings with vesting schedules still in progress.
- **Current Score**: 1
- **Potential Score**: 9
- **Classification**: Improvable (through ongoing token distribution)
- **Evidence**: Multiple crypto analytics sources report >70% concentration, [Token Info](https://docs.kamino.finance/kmno/token-info), [Tokenomist](https://tokenomist.ai/kamino)
- **Evidence Status**: Verified
- **Comments**: Top 10 holders control >66% of voting power, triggering High (1). Community allocation (35%) is being distributed via seasons but concentration remains extreme.
- **Path to Potential**: Continue community distribution, implement delegation systems to diffuse voting power

**[O-G-03] Are mechanisms in place to limit major changes like timelocks and veto?**
- **Answer**: No documented on-chain timelock for governance/parameter changes. Risk Council provides informal oversight and review of parameter changes by curators. Auto-deleverage has 72-hour margin call period (a form of delay). However, no formal veto mechanism with defined scope and triggers.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Gauntlet Curation](https://gov.kamino.finance/t/introducing-gauntlet-as-official-vault-curators/856), [Auto-Deleverage](https://docs.kamino.finance/risk/protocol-mechanisms/automated-deleverage)
- **Evidence Status**: Verified
- **Comments**: Risk Council acts as informal veto safeguard (partially specified). Mid criteria: "veto safeguards informal or only partially specified." This justifies Mid (3).
- **Path to Potential**: Implement visible on-chain timelock >=24h for all major upgrades and parameter changes

**[O-G-04] Can the protocol replace the strategy manager without blocking user withdrawals?**
- **Answer**: Yes. Vault manager changes do not affect underlying Kamino markets. Withdrawals remain permissionless via on-chain redemption from lending pools regardless of vault curator status.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: V2 architecture separates Market Layer from Vault Layer
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**Governance Subtotal:**
- Raw scores: 3+1+3+9 = 16
- Max raw: 4 x 9 = 36
- Weighted: (16/36) x 67.5 = 30.0

**Governance: 30.0/67.5 (44.4%)**

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

**[O-TL-01] Are core team and operating entities publicly identified and credible?**
- **Answer**: Yes. Kamino founders: Asaf Meir (CEO, ex-ConsenSys/Orbs), Tal Zelig (CTO, ex-Bancor/Orbs), Roy Keyes (COO, ex-Hubble Protocol). Sentora: Anthony DeMartino (CEO, ex-Coinbase Head of DeFi Trading), Jesus Rodriguez (CTO, ex-IntoTheBlock CEO). All identifiable with verifiable track records.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [The Org - Kamino](https://theorg.com/org/kamino-finance/org-chart/asaf-meir), [Sentora](https://sentora.com/about), [The Block](https://www.theblock.co/post/353220/intotheblock-trident-merger-institutional-defi-platform-sentora-25-million-usd-series-a)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-02] Is the protocol dependent on a single developer or small team?**
- **Answer**: No. Kamino has a full engineering team with 35+ GitHub repos. Sentora has separate team from IntoTheBlock + Trident merger. Multiple vault curators (Gauntlet, Steakhouse, Allez Labs, MEV Capital, Sentora) provide redundancy.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [GitHub Kamino-Finance](https://github.com/Kamino-Finance)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-03] What legal entity and jurisdiction operate the protocol and/or assets?**
- **Answer**: Kamino Finance based in Panama (founded 2022). Sentora is an incorporated entity formed from merger of IntoTheBlock and Trident Digital. Paxos Trust Company (NYDFS-regulated) issues PYUSD.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [PitchBook](https://pitchbook.com/profiles/company/557633-98)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-04] Are there known investigations or regulatory actions related to the entity?** (Deal Breaker)
- **Answer**: No enforcement actions found for Kamino Finance or Sentora. PYUSD is regulated (Paxos under NYDFS). No regulatory issues identified.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: Exhaustive research found no actions
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-05] Is there an on-call and incident response process for core teams?**
- **Answer**: Risk Council monitors and can pause markets. In-house security team conducts regular penetration testing. However, no public 24/7 on-call SLA documented. No published incident runbooks with response times.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Solana Compass](https://solanacompass.com/projects/Kamino_Finance)
- **Evidence Status**: Partial -- Risk Council monitoring confirmed, formal SLA undocumented
- **Path to Potential**: Document and publish 24/7 on-call procedures with defined SLAs

**[O-TL-06] Does the team provide timely support for critical user or integrator issues?**
- **Answer**: Active Discord, governance forum, and social media. December 2025 Jupiter Lend dispute saw rapid public engagement and communication from Kamino team. Support channels responsive.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Forum](https://gov.kamino.finance/)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-07] Are major investors or strategic partners disclosed?**
- **Answer**: Sentora: $25M Series A from New Form Capital, Tribe Capital, Ripple, Curved Ventures, Flare, Bankai Ventures. Kamino backed by investors (less detailed but acknowledged). Strategic partnerships with Chainlink, PayPal/Paxos, Apollo/Securitize disclosed.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [The Block](https://www.theblock.co/post/353220/intotheblock-trident-merger-institutional-defi-platform-sentora-25-million-usd-series-a)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-08] Does the strategy manager manage similar vaults creating conflict of interest?**
- **Answer**: Yes. Sentora manages $3B+ across 300+ strategies across 60+ protocols and 16 blockchains. On Kamino, multiple vault curators operate. Sentora's institutional risk framework provides qualitative conflict controls but no hard-coded per-vault constraints preventing preferential allocation are documented.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Sentora](https://sentora.com/)
- **Evidence Status**: Partial -- other mandates acknowledged, conflict controls qualitative only
- **Path to Potential**: Implement hard-coded conflict controls (allocation rules, per-vault caps)

**[O-TL-09] Has the strategy manager previously been involved in products with collateral loss?**
- **Answer**: No known collateral loss events. Sentora formed May 2025 from IntoTheBlock (since 2018) and Trident Digital. IntoTheBlock had clean track record. No loss incidents reported.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Sentora](https://sentora.com/), exhaustive research
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**Team & Legal Subtotal:**
- Raw scores: 9+9+9+9+3+9+9+3+9 = 69
- Max raw: 9 x 9 = 81
- Weighted: (69/81) x 67.5 = 57.5

**Team & Legal: 57.5/67.5 (85.2%)**

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

**[O-DT-01] Is there up-to-date documentation explaining architecture, strategy mechanics, and risks?**
- **Answer**: Yes. Comprehensive docs at docs.kamino.finance including Lend Litepaper, risk guides, oracle documentation, interest rate mechanics, liquidation docs. Updated for V2 in 2025. Monthly risk reports published on governance forum.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Docs](https://docs.kamino.finance)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-DT-02] Is it clearly documented how collateral is used and when loss occurs?**
- **Answer**: Yes. Detailed liquidation documentation, interest rate mechanics, risk parameters, position risk simulation tools, and monthly risk insights reports with stress testing. Loss scenarios documented and quantified.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Position Risk & Liquidations](https://docs.kamino.finance/products/borrow-lend/position-risk-and-liquidations), [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-DT-03] Are all contract, proxy and implementation addresses documented in one canonical place?**
- **Answer**: Program IDs published: KLend mainnet (KLend2g3cP87fffoy8q1mQqGKjrxjC8boSyAYavgmjD). GitHub contains all contract source. SDK documentation includes addresses.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [GitHub klend](https://github.com/Kamino-Finance/klend), [SDK Docs](https://docs.kamino.finance/build-on-kamino/sdk-and-smart-contracts)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-DT-04] Are roles, permissions and timelocks documented with visible change history?**
- **Answer**: Risk Council role documented at high level. Specific admin roles, permissions, and timelock configurations not fully detailed. No public change log for role/permission changes. Curator roles partially documented via governance forum posts.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Kamino Docs](https://docs.kamino.finance), [Gauntlet Post](https://gov.kamino.finance/t/introducing-gauntlet-as-official-vault-curators/856)
- **Evidence Status**: Partial -- Risk Council role acknowledged, detailed role registry missing
- **Path to Potential**: Publish central role registry with all permissions, timelocks, and change history

**[O-DT-05] Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities?** (Deal Breaker)
- **Answer**: Yes. All positions on-chain and visible via Risk Dashboard. PYUSD has Paxos attestations (monthly, by WithumSmith+Brown). Vault balances verifiable on Solana explorers.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [PYUSD Transparency](https://www.paxos.com/pyusd-transparency), [Risk Dashboard](https://risk.kamino.finance/)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-DT-06] Are all contracts verified on the leading block explorers?**
- **Answer**: Yes. Open source on GitHub. Verifiable builds ensure deployed programs match audited code. "Kamino Lend and Earn Vaults use Verifiable Builds, which guarantees that the programs running on Solana are the exact same versions published and audited on GitHub."
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [GitHub Kamino-Finance](https://github.com/Kamino-Finance), verifiable builds documented
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**Documentation Subtotal:**
- Raw scores: 9+9+9+3+9+9 = 48
- Max raw: 6 x 9 = 54
- Weighted: (48/54) x 67.5 = 60.0

**Documentation: 60.0/67.5 (88.9%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

**[O-FR-01] Is there a backstop reserve or safety module for user losses?**
- **Answer**: No dedicated safety module or ring-fenced backstop fund disclosed. 10% KMNO token allocation for "liquidity & treasury" but no binding activation rules for user loss coverage. Bug bounty ($1.5M) indicates some reserves but no committed loss-coverage mechanism.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Token Info](https://docs.kamino.finance/kmno/token-info)
- **Evidence Status**: Verified absence of dedicated safety module
- **Path to Potential**: Create dedicated safety module with binding activation rules

**[O-FR-02] How large and liquid are the backstop reserves and treasury relative to TVL?**
- **Answer**: Treasury size not publicly disclosed. KMNO treasury allocation is 10% of token supply (~1B KMNO). At current KMNO price, this has some value but composition and liquid reserves are unknown. Bug bounty ($1.5M) and daily fee revenue ($300K+) suggest operational reserves but no published reserve target.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Source Missing
- **Evidence**: [Token Info](https://docs.kamino.finance/kmno/token-info), no public treasury balance disclosure
- **Evidence Status**: Missing
- **Path to Potential**: Publish treasury composition, liquid balance, and establish reserve target

**[O-FR-03] What is the estimated operational runway at current burn?**
- **Answer**: Strong for both entities. Sentora has $25M Series A. Kamino generates $300K+ daily fees ($57M annualized) with $13.23M 30-day annualized revenue. Protocol is revenue-positive. Combined entities well-funded for >24 months.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [The Block](https://www.theblock.co/post/353220/intotheblock-trident-merger-institutional-defi-platform-sentora-25-million-usd-series-a), DeFiLlama fee data
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-FR-04] How have TVL, revenue and buffers behaved in past stress events?**
- **Answer**: Kamino maintained dominant Solana position through market fluctuations. TVL grew from ~$2B to $3.7B peak in October 2025, dropped to $2.33B after December 2025 Jupiter dispute and market conditions, then stabilized around $2.7B. Revenue remains strong at $300K+ daily. September 2025 SOL drawdown (-25%) handled without bad debt. February 5-6, 2026 stress event (SOL -18%) triggered 55,649 liquidations ($19.36M collateral seized) across all Kamino markets with zero bad debt generated. The Sentora PYUSD vault TVL declined from ~$189M to ~$38M primarily due to PayPal incentive tapering, not security failures.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [DeFiLlama](https://defillama.com/protocol/kamino), [Risk Report Sept 2025](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-september-2025/843)
- **Evidence Status**: Verified
- **Comments**: TVL volatility is notable (47% drop from peak) but primarily driven by competitive dynamics, not security failures. Revenue and protocol function maintained throughout.
- **Path to Potential**: N/A

**[O-FR-05] Can the protocol remain safe in maintenance mode if team disappears?**
- **Answer**: On-chain contracts would continue operating. Withdrawals remain permissionless. Users can interact directly with contracts via documented SDK. However, Risk Council and governance would be impaired. Vault curation would stop but underlying lending markets continue. Open source code allows community maintenance.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Docs](https://docs.kamino.finance), open source codebase, permissionless withdrawal architecture
- **Evidence Status**: Verified
- **Path to Potential**: N/A

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


---
