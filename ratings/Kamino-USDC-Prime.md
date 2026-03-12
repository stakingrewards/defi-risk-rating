# Kamino Finance - USDC Prime Vault Risk Rating

**Rating Date**: 2026-03-10
**Final Grade**: B
**Total Score**: 688.1/900 points

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
- **Answer**: Most recent formal engagement: Certora formal verification (November 2024 - February 2025). Certora is not on the SR tier list but is an industry-recognized leader in formal verification. Ackee Blockchain, which has also audited Kamino, is listed as Tier-1 on the SR auditor tiers. Multiple Solana-ecosystem auditors (OtterSec, Offside Labs, Sec3) have also audited the protocol.
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
- **Answer**: No confirmed exploits causing user fund loss. Clean record since founding in 2022 (3+ years). Security page states "18 full audits completed with 0 critical vulnerabilities." No incidents found on Rekt.news or security incident databases. February 2026 stress event (55,649 liquidations, $19.36M collateral seized) processed with zero bad debt.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Security](https://kamino.com/security), [Feb 2026 Risk Event](https://gov.kamino.finance/t/kamino-risk-event-analysis-feb-5-6-2026/868)
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
- **Answer**: Kamino has the Risk Assessment Framework (KRAF) providing dashboards with risk overview, loan analysis, volatility analysis, liquidity risk, and shock scenarios at risk.kamino.finance. However, no evidence of a reputable third-party 24/7 monitoring provider (Hypernative, Blockaid, etc.) was found for the Kamino platform itself. KRAF is a risk analytics tool rather than real-time security monitoring with automated alerting. Steakhouse Financial claims to "monitor situations across chains and reallocate 24/7 with redundant real-time controls" but specific monitoring provider details for their Kamino deployment are not disclosed.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Risk Dashboard](https://risk.kamino.finance/), [KRAF Docs](https://docs.kamino.finance/risk/risk-assessment-framework), [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1976976208962158617)
- **Evidence Status**: Partial -- KRAF dashboard verified, Steakhouse 24/7 claim unverified with no specific provider named
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
- **Answer**: Kamino uses a Squads multisig for administrative operations. Multisig address identified as 6hhBGCtmg7tPWUSgp3LG6X2rsmYWAc4tNsA6G4CnfQbM. Critical details are missing: signer identities, threshold (M-of-N), independence of signers not publicly documented. KMNO on-chain governance not yet activated (planned for 2026). Risk Council has emergency powers. Admin configuration change history is not publicly documented.
- **Current Score**: 1
- **Potential Score**: 9
- **Classification**: Source Missing
- **Evidence**: Multisig address found via [GitHub](https://github.com/Kamino-Finance). Signer details, threshold, and change history not found in official docs, governance forum, or third-party sources. [Squads Integration](https://squads.xyz/blog/squadsx-kamino)
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

**[S-KM-07] What are the whitelisted protocols the vault strategy can interact with?**
- **Answer**: Steakhouse USDC Prime vault deploys exclusively into Kamino's own lending markets (Main and JLP markets). Risk Council reviews all parameter changes from curators. Whitelist effectively limited to Kamino internal markets. However, on-chain enforcement mechanism and market addition governance not documented with timelock. Curator has allocation discretion within the vault for rebalancing across approved markets.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Kamino V2 Introduction](https://gov.kamino.finance/t/introducing-kamino-lend-v2/58), [Steakhouse Partnership](https://gov.kamino.finance/t/introducing-steakhouse-financial-as-official-risk-contributors/653)
- **Evidence Status**: Partial -- curator constraint exists but enforcement not documented with timelock
- **Path to Potential**: Document and enforce on-chain whitelist with governance/multisig and timelock

**[S-KM-08] Is there a tested incident playbook for admin-key compromise or signer loss?**
- **Answer**: No evidence found. No public incident response playbook, key rotation procedures, emergency response SLAs, or tabletop exercises documented for Kamino platform. Steakhouse Financial has internal monitoring and response capabilities but no public playbook specific to Kamino deployment.
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

### STRATEGY (30% Weight) - Score: 237.5/270 (88.0%)

#### Protocol Mechanics (5% weight, 45 max points)

**[ST-PM-01] What are the sources of yield and is it aligned with the mandate?**
- **Answer**: Yield sources: (1) USDC lending interest from borrowers in Kamino markets (Main and JLP markets), (2) KMNO token rewards (Season 5: up to 100M KMNO over 3 months with 6-month vesting). Both sources are mandate-aligned for a stablecoin lending strategy focused on "high-activity markets." Steakhouse structures USDC Prime as the stability-focused product line. APY ranges 11-17%.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino USDC Prime](https://kamino.com/lend/usdc-prime), [Steakhouse Partnership](https://gov.kamino.finance/t/introducing-steakhouse-financial-as-official-risk-contributors/653)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-02] Under which conditions does net yield become negative or cause loss?**
- **Answer**: Loss limited to tail scenarios: smart contract exploit, oracle failure, severe collateral liquidation cascade in Kamino markets, or USDC depeg. Vault is on the lending side (not borrowing), so no direct liquidation risk. Overcollateralized lending model provides buffer. February 2026 stress test showed zero bad debt despite 55,649 liquidations and $19.36M collateral seized across markets. September 2025 stress test showed $10.6M potential bad debt at 30% market drawdown on $2.8B TVL (~0.4%).
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Feb 2026 Risk Event](https://gov.kamino.finance/t/kamino-risk-event-analysis-feb-5-6-2026/868), [Oracle Docs](https://docs.kamino.finance/risk/oracles)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-03] Is leverage or rehypothecation used and up to what effective level?**
- **Answer**: No leverage or rehypothecation. Vault lends USDC to borrowers. Effective leverage 1.0x. Borrowers may leverage but the vault itself is unleveraged.
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
- **Answer**: No permanent loss events for USDC lending on Kamino. Clean track record since vault launch. November 2025 stress: 16,228 liquidation events, $26.5M collateral seized, zero bad debt for lenders. February 2026 stress: 55,649 liquidation events, $19.36M seized, zero bad debt. Steakhouse claims to be "the only major curator with no bad debt events" across all mandates.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Nov 2025 Report](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-november-2025/859), [Feb 2026 Risk Event](https://gov.kamino.finance/t/kamino-risk-event-analysis-feb-5-6-2026/868), [Steakhouse Wrapped 2025](https://kitchen.steakhouse.financial/p/steakhouse-wrapped-2025)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-06] Is a risk framework for vault curation or protocol mechanics documented?**
- **Answer**: Yes. Steakhouse Financial provides a comprehensive multi-layer risk framework documented at steakhouse.financial/docs/risk-management with three layers: (1) Asset Rating (issuer, credit, operational risk), (2) Platform Rating (protocol resilience), (3) Market Rating (oracle, liquidity, LLTV, credit enhancement). Kamino additionally has KRAF (Kamino Risk Assessment Framework) with comprehensive dashboard at risk.kamino.finance. Quantitative limits for utilization, shock scenarios, and per-asset risk tiers are defined.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Steakhouse Risk Framework](https://www.steakhouse.financial/docs/risk-management), [KRAF Docs](https://docs.kamino.finance/risk/risk-assessment-framework)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-07] Is current yield sustainable relative to underlying economics?**
- **Answer**: APY of 11-17% partially depends on KMNO incentives. Season 5 distributed up to 100M KMNO over 3 months with 6-month vesting. Organic lending demand exists (Kamino ~60% of Solana lending) but the precise organic vs incentive yield breakdown is not clearly published for this specific vault. Steakhouse's USDC Prime is structured as the conservative product line, suggesting lower incentive dependency than High Yield vaults. However, without explicit data separating organic from incentive yield, we must score conservatively.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Kamino Seasons](https://docs.kamino.finance/kmno/points/seasons), [Steakhouse Wrapped 2025](https://kitchen.steakhouse.financial/p/steakhouse-wrapped-2025)
- **Evidence Status**: Partial -- total APY verified, organic vs incentive split not published for this vault
- **Path to Potential**: Publish transparent yield decomposition showing organic vs incentive contributions

**[ST-PM-08] Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative?**
- **Answer**: Yes. USDC is the most liquid stablecoin on Solana. Withdrawal depends on lending pool utilization. Interest rate model creates steep rate increases at high utilization, incentivizing borrower repayment. Under normal conditions, exit slippage is negligible.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-09] Does the strategy rely on a spread, peg, or funding rate that can invert?**
- **Answer**: Strategy relies on USDC maintaining peg to USD. USDC is Circle-issued, NYDFS-regulated, with monthly attestations. Historical all-time low during March 2023 SVB crisis (depegged to ~$0.87) with full recovery within days. Peg risk is low for a regulated stablecoin but non-zero -- contributes minority of risk.
- **Current Score**: 3
- **Potential Score**: 3
- **Classification**: Non-Improvable (inherent to stablecoin lending strategy)
- **Evidence**: [Circle USDC](https://www.circle.com/usdc), [USDC SVB Depeg](https://coinmarketcap.com/academy/article/explaining-the-silicon-valley-bank-fallout-and-usdc-de-peg)
- **Evidence Status**: Verified
- **Path to Potential**: N/A -- inherent to USDC strategy

**Protocol Mechanics Subtotal:**
- Raw scores (8 applicable, 1 N/A): 9+9+9+9+9+3+9+3 = 60
- Max raw: 8 x 9 = 72
- Weighted: (60/72) x 45 = 37.5

**Protocol Mechanics: 37.5/45 (83.3%)**

---

#### Collateral (5% weight, 45 max points)

**[ST-C-01] Which assets are accepted as collateral and how are they risk rated?**
- **Answer**: Kamino accepts blue-chip collateral with risk tiering: General (SOL, stablecoins), Isolated Collateral, and Isolated Debt categories. Per-asset LTVs configured with 80% liquidation threshold for SOL. LSTs (JitoSOL, mSOL) in eMode with 90-95% LTV. JLP accepted in dedicated market. Deposit and borrow caps adjusted by Risk Council based on volatility, liquidity, and security metrics. All major collateral types are established assets appropriate for Solana lending.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Position Risk & Liquidations](https://docs.kamino.finance/products/borrow-lend/position-risk-and-liquidations)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-C-02] How did each collateral behave versus its underlying during past stress or depegs?**
- **Answer**: This question evaluates vault share (receipt token) behavior versus the underlying USDC. While USDC itself maintains its peg, vault shares are subject to utilization-dependent redemption constraints. During the November 2025 stress (SOL -29%), Kamino processed liquidations cleanly with zero bad debt, and Steakhouse claims "no Solana users of Steakhouse vaults were affected." However, during high utilization periods, vault shares cannot be redeemed at full NAV immediately -- this is functionally a discount from underlying. The February 2026 stress event (SOL -18%) also showed zero bad debt. While Kamino has now survived two significant stress events, the vault share redemption constraint during high utilization is inherent to the lending design.
- **Current Score**: 3
- **Potential Score**: 3
- **Classification**: Non-Improvable (inherent to lending vault design)
- **Evidence**: [Nov 2025 Report](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-november-2025/859), [Feb 2026 Risk Event](https://gov.kamino.finance/t/kamino-risk-event-analysis-feb-5-6-2026/868), [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1976976208962158617)
- **Evidence Status**: Verified
- **Comments**: Vault share redemption constrained by pool utilization is inherent to the lending design. Two stress events survived but utilization-dependent constraints remain.
- **Path to Potential**: N/A -- inherent to lending vault mechanics

**[ST-C-03] How is validator or slashing risk handled for staking-based collaterals?**
- **Answer**: N/A -- Vault holds USDC stablecoin, not staking derivatives. Solana does not currently have slashing for validators.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A

**[ST-C-04] What share of TVL relies on bridged or wrapped assets?**
- **Answer**: USDC is native on Solana (Circle-issued directly via Solana Token Extensions framework). Not bridged. Approximately 0% bridged asset exposure for the vault.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Circle USDC](https://www.circle.com/usdc)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**Collateral Subtotal:**
- Raw scores (3 applicable, 1 N/A): 9+3+9 = 21
- Max raw: 3 x 9 = 27
- Weighted: (21/27) x 45 = 35.0

**Collateral: 35.0/45 (77.8%)**

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

**[ST-IC-01] Which chains, bridges, oracles, wallets and CEXs does the strategy depend on?**
- **Answer**: Solana (Tier-0), Pyth Network (Tier-0), Chainlink Data Streams (Tier-0). No bridges. No CEX dependency. Circle (NYDFS-regulated) for USDC issuance/redemption. All critical dependencies are Tier-0.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Oracle Docs](https://docs.kamino.finance/risk/oracles), [Chainlink Integration](https://gov.kamino.finance/t/kamino-integrates-chainlink-data-streams-for-high-quality-low-latency-market-data/550)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-IC-02] How redundant and battle-tested are the oracle and bridge setups?**
- **Answer**: Multi-oracle system aggregates Pyth + Chainlink with cross-verification. TWAP/EWMA for manipulation resistance. Price bands (1% for USD stables). Double-audited by Certora and Offside Labs via the Scope oracle aggregator. No bridge dependency. Both oracles are Tier-0.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Oracle Docs](https://docs.kamino.finance/risk/oracles), [Scope GitHub](https://github.com/Kamino-Finance/scope)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-IC-03] Are off-chain infrastructure providers certified by standard IT security audits?**
- **Answer**: Circle (USDC issuer) is NYDFS-regulated with regular compliance audits. Kamino team SOC2/ISO27001 certifications not disclosed. Steakhouse Financial certifications not publicly available.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Source Missing
- **Evidence**: [Circle](https://www.circle.com/usdc) (regulatory status verified), Kamino/Steakhouse certifications not found
- **Evidence Status**: Partial -- Circle regulatory compliance verified, Kamino/Steakhouse IT security certifications unverified
- **Path to Potential**: Obtain and publish SOC2/ISO27001 for Kamino and Steakhouse operations

**[ST-IC-04] How did these infra components behave in past outages or chain incidents?**
- **Answer**: Solana's last major outage was February 6, 2025 (~5 hours). Since then, 13+ months of continuous uptime achieved. November 2025 and February 2026 market stress events processed smoothly with zero bad debt. Oracle system maintained integrity throughout both events. Steakhouse claims 24/7 monitoring with redundant controls across chains.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Solana Status](https://status.solana.com/), [Feb 2026 Risk Event](https://gov.kamino.finance/t/kamino-risk-event-analysis-feb-5-6-2026/868)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-IC-05] Has the base chain recently halted block production or experienced consensus failure?**
- **Answer**: Solana's last major halt was February 6, 2025 (~5 hours). As of March 10, 2026, this is now more than 12 months ago. The chain has achieved 13+ months of continuous uptime. No chain halt or consensus failure above 30 minutes in the last 12 months.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Solana Status](https://status.solana.com/), [Helius Blog](https://www.helius.dev/blog/solana-outages-complete-history)
- **Evidence Status**: Verified
- **Comments**: Previous rating (Feb 5, 2026) scored this Mid (3) because the Feb 6, 2025 outage was within the 12-month window. As of March 10, 2026, it is now outside the window, scoring Low (9).
- **Path to Potential**: N/A

**[ST-IC-06] Has the validator set experienced slashing events that could impact staked collateral?**
- **Answer**: N/A -- USDC vault does not hold staking derivatives. Solana does not currently implement slashing.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A

**[ST-IC-07] Are validators diverse geographically and by operator?**
- **Answer**: N/A -- Not applicable for USDC stablecoin lending vault.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A

**[ST-IC-08] Can any single infra component failure alone block withdrawals or cause losses?**
- **Answer**: No single point of failure identified. Withdrawals are permissionless on-chain. Oracle failure: multi-oracle fallback (Pyth + Chainlink). Chain halt: temporary, not permanent (last halt Feb 2025 was ~5 hours). Users can interact directly with lending contracts.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Docs](https://docs.kamino.finance)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**Infrastructure Counterparty Subtotal:**
- Raw scores (6 applicable, 2 N/A): 9+9+3+9+9+9 = 48
- Max raw: 6 x 9 = 54
- Weighted: (48/54) x 45 = 40.0

**Infrastructure Counterparty: 40.0/45 (88.9%)**

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

**[ST-PC-01] Into which external protocols, CEXs or RWA platforms is collateral deployed?**
- **Answer**: Kamino Lend markets only (Main and JLP markets). No external protocol deployment. USDC backed by Circle (regulated, fiat reserves + US Treasuries). No CEX or RWA exposure.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino USDC Prime](https://kamino.com/lend/usdc-prime)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PC-02] Are revenue-share or incentive arrangements documented and do they create conflicts?**
- **Answer**: KMNO rewards program publicly documented (Seasons structure with vesting). Steakhouse vault fee structure on Kamino: research indicates zero management and performance fees for most Kamino vaults (consistent with previous vault rating findings). Steakhouse-Kamino partnership terms described at governance level but specific revenue-share details between Steakhouse and Kamino not fully transparent.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Steakhouse Partnership](https://gov.kamino.finance/t/introducing-steakhouse-financial-as-official-risk-contributors/653), [Kamino Seasons](https://docs.kamino.finance/kmno/points/seasons)
- **Evidence Status**: Verified at high level; specific fee terms between Steakhouse and Kamino partially disclosed
- **Path to Potential**: N/A

**[ST-PC-03] Are there hard limits and rebalancing rules per counterparty?**
- **Answer**: Kamino enforces per-asset deposit and borrow caps. Dynamic limits adjusted by Risk Council based on KRAF analytics. Market-level exposure limits documented. Steakhouse applies its multi-layer risk framework with quantitative limits for utilization, concentration, and drawdown.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Risk Docs](https://docs.kamino.finance/risk), [Steakhouse Risk Framework](https://www.steakhouse.financial/docs/risk-management)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PC-04] How quickly and safely can positions be unwound from each counterparty?**
- **Answer**: Lending positions withdrawable subject to pool utilization. Interest rate model creates steep rate increases at high utilization to incentivize repayment. No discretionary approvals needed. USDC has deep external liquidity. November 2025 stress and February 2026 stress both processed without impairments to lenders. Steakhouse claims: "Liquidity remains available across Prime and High Yield vaults for USDC and USDG."
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates), [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1976976208962158617)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PC-05] Are third-party validators, custody providers or asset managers disclosed?** (Deal Breaker)
- **Answer**: Steakhouse Financial as vault curator fully disclosed with team backgrounds and risk framework documentation. Circle as USDC custodian disclosed. Kamino as protocol layer disclosed. All third-party roles clearly defined with public documentation.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Steakhouse](https://www.steakhouse.financial/), [Steakhouse Partnership](https://gov.kamino.finance/t/introducing-steakhouse-financial-as-official-risk-contributors/653), [Circle USDC](https://www.circle.com/usdc)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**Protocol Counterparty Subtotal:**
- Raw scores: 9+9+9+9+9 = 45
- Max raw: 5 x 9 = 45
- Weighted: (45/45) x 45 = 45.0

**Protocol Counterparty: 45.0/45 (100.0%)**

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
- **Answer**: Depends on pool utilization. During normal conditions, meaningful share of TVL is available for withdrawal. However, during high-utilization periods (such as the November 2025 stress when utilization averaged ~53-59%), only a portion of supplied assets are immediately available. Interest rate model incentivizes repayment at high utilization. The vault deploys into Main and JLP markets -- total available liquidity depends on aggregate utilization across these markets.
- **Current Score**: 3
- **Potential Score**: 3
- **Classification**: Non-Improvable (inherent to lending protocol design)
- **Evidence**: [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates), [Nov 2025 Report](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-november-2025/859)
- **Evidence Status**: Verified
- **Path to Potential**: N/A -- inherent to lending model

**[ST-L-03] Have there been past withdrawal delays, queues or freezes?**
- **Answer**: No reported withdrawal delays or freezes for USDC markets on Kamino. November 2025 and February 2026 stress events processed without freeze events. Steakhouse confirmed "Liquidity remains available across Prime and High Yield vaults for USDC and USDG" during stress.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Feb 2026 Risk Event](https://gov.kamino.finance/t/kamino-risk-event-analysis-feb-5-6-2026/868), [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1976976208962158617)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-04] Do caps or limits restrict timely redemptions during high utilization?**
- **Answer**: Caps sized appropriately. Interest rates spike at high utilization to incentivize repayment. No history of caps blocking exits during stress events.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Risk Docs](https://docs.kamino.finance/risk)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-05] How does exit liquidity behave during volatility and network congestion?**
- **Answer**: Exit liquidity is constrained by lending pool utilization. During the November 2025 stress (SOL -29%), USDC pool utilization averaged ~53-59%, and Steakhouse confirmed vaults remained functional with available liquidity. During February 2026 stress (SOL -18%), zero bad debt occurred across 55,649 liquidations. While two stress events have been survived, exit constraints during high utilization remain inherent to the lending model. The vault has demonstrated resilience but the utilization-dependent exit constraint is structural.
- **Current Score**: 3
- **Potential Score**: 3
- **Classification**: Non-Improvable (inherent to lending pool design)
- **Evidence**: [Nov 2025 Report](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-november-2025/859), [Feb 2026 Risk Event](https://gov.kamino.finance/t/kamino-risk-event-analysis-feb-5-6-2026/868)
- **Evidence Status**: Verified
- **Comments**: Two real stress events survived with functional liquidity, but utilization-based exit constraints are inherent to lending protocol design. Scoring Mid (3) because while stress has been survived, exit liquidity was materially constrained.
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
- **Answer**: No. Primary redemption through Kamino lending pools always available. Secondary markets (DEXs) optional for faster exits. Users can interact directly with smart contracts.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: Vault mechanics
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-08] What is the liquidity depth of collateral and receipt tokens?**
- **Answer**: USDC is the most liquid stablecoin on Solana with deep liquidity across DEXs (Jupiter, Orca, Raydium). Receipt tokens are redeemable 1:1 for USDC via the vault mechanism subject to pool utilization.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [DeFiLlama Stablecoins](https://defillama.com/stablecoins/Solana)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-09] What is the risk of bank-run scenarios under full utilization?**
- **Answer**: Bank run causes temporary queues via high utilization. Interest rates spike to incentivize borrower repayment. No permanent loss expected from bank-run dynamics alone (overcollateralized lending), but delays are possible. The February 2026 stress (SOL -18%) showed the protocol can handle significant deleveraging without bad debt, though a full bank-run on the USDC lending pool specifically has not been tested.
- **Current Score**: 3
- **Potential Score**: 3
- **Classification**: Non-Improvable (inherent to lending pool design)
- **Evidence**: [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates), [Feb 2026 Risk Event](https://gov.kamino.finance/t/kamino-risk-event-analysis-feb-5-6-2026/868)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**Liquidity Subtotal:**
- Raw scores: 9+3+9+9+3+9+9+9+3 = 63
- Max raw: 9 x 9 = 81
- Weighted: (63/81) x 45 = 35.0

**Liquidity: 35.0/45 (77.8%)**

---

#### Market (5% weight, 45 max points)

**[ST-M-01] How has the LST or receipt token peg performed under market stress?**
- **Answer**: This question evaluates vault share (receipt token) behavior versus the underlying USDC. During the November 2025 (SOL -29%) and February 2026 (SOL -18%) stress events, Steakhouse confirmed "no Solana users of Steakhouse vaults were affected" and "Liquidity remains available across Prime and High Yield vaults for USDC." The vault generated zero bad debt during both events. However, vault shares are still subject to utilization-dependent redemption constraints during high utilization periods. The vault has now survived two real stress events with no permanent deviation, though utilization constraints technically create a temporary discount to NAV.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Nov 2025 Report](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-november-2025/859), [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1976976208962158617), [Feb 2026 Risk Event](https://gov.kamino.finance/t/kamino-risk-event-analysis-feb-5-6-2026/868)
- **Evidence Status**: Verified
- **Comments**: Two real stress events survived with zero bad debt and Steakhouse confirming vault users unaffected. This meets the Low (9) criteria: "During major stress, token stayed within ~2% of reference/NAV and any deviations resolved within ~24 hours." While utilization constraints exist, they did not cause a permanent or prolonged deviation.
- **Path to Potential**: N/A

**[ST-M-02] How likely can adverse crypto market moves cause permanent losses due to directional exposure?**
- **Answer**: Low. USDC strategy has no crypto directional exposure. Vault lends stablecoins. Depositors receive USDC regardless of crypto market conditions. No leverage or directional bets.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: Vault mechanics -- pure stablecoin lending
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-M-03] Are interest rate/incentive models robust during TVL shifts or volatility spikes?**
- **Answer**: Yes. Kamino uses poly-linear interest rate curves that become steep as utilization approaches critical levels. Rates auto-increase with utilization to incentivize repayment. No evidence of prolonged >= 95% utilization or yield cliffs under stress.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Interest Rates](https://docs.kamino.finance/risk/liquidity-risk/interest-rates)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-M-04] Have historic scenarios with high market volatility been explicitly modeled?**
- **Answer**: Yes. Kamino has formal verification by Certora. KRAF dashboard includes shock scenarios. September 2025 stress testing showed $10.6M potential bad debt at 30% market drawdown on $2.8B TVL (~0.4%). Actual stress events (Nov 2025, Feb 2026) validated the models with zero bad debt. Steakhouse applies its own quantitative risk modeling across vault curation.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Certora Report](https://www.certora.com/blog/securing-kamino-lending), [Nov 2025 Report](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-november-2025/859), [KRAF](https://risk.kamino.finance)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-M-05] Can sharp price moves trigger forced liquidations that crystallize losses?**
- **Answer**: Not for this vault (lender side). Borrowers face liquidation risk. Vault benefits from liquidations via continued lending capacity. February 2026: 55,649 liquidations processed efficiently, zero bad debt for lenders.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Liquidation Docs](https://docs.kamino.finance/products/borrow-lend/position-risk-and-liquidations), [Feb 2026 Risk Event](https://gov.kamino.finance/t/kamino-risk-event-analysis-feb-5-6-2026/868)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**Market Subtotal:**
- Raw scores: 9+9+9+9+9 = 45
- Max raw: 5 x 9 = 45
- Weighted: (45/45) x 45 = 45.0

**Market: 45.0/45 (100.0%)**

---

**STRATEGY TOTAL: 37.5 + 35.0 + 40.0 + 45.0 + 35.0 + 45.0 = 237.5/270 (88.0%)**

---

### OPERATIONS (30% Weight) - Score: 197.0/270 (73.0%)

#### Governance (7.5% weight, 67.5 max points)

**[O-G-01] What governance model controls protocol changes and upgrades?**
- **Answer**: Hybrid model, not yet on-chain. KMNO token governance planned for 2026 as part of "Road to $10B" but not yet activated. Risk Council handles operational parameters. Squads multisig for immediate changes. Major decisions discussed publicly on governance forum but executed by multisig/team.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Kamino Forum](https://gov.kamino.finance/), [KMNO Token Info](https://docs.kamino.finance/kmno/token-info)
- **Evidence Status**: Verified
- **Path to Potential**: Activate on-chain KMNO token governance

**[O-G-02] How concentrated is voting power among top holders or delegates?**
- **Answer**: Highly concentrated. Top 10 wallets control over 70% of KMNO total supply. Token distribution: 35% stakeholders/advisors, 20% core contributors, 35% community/grants (10% liquidity/treasury). As of March 2026, ~39.27% of total supply unlocked. On-chain governance not yet activated, but the concentration level indicates significant capture risk if governance launches.
- **Current Score**: 1
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Tokenomist](https://tokenomist.ai/kamino), [Token Info](https://docs.kamino.finance/kmno/token-info)
- **Evidence Status**: Verified
- **Path to Potential**: Increase community token distribution and reduce insider concentration below 50%

**[O-G-03] Are mechanisms in place to limit major changes like timelocks and veto?**
- **Answer**: No documented on-chain timelock for governance/parameter changes. Risk Council provides informal oversight and review. Auto-deleverage has 72-hour margin call period but no formal veto mechanism with defined scope. No timelock on upgrades (penalized under S-SC-05).
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Kamino Docs](https://docs.kamino.finance)
- **Evidence Status**: Verified
- **Path to Potential**: Implement on-chain timelock >=24h and formal veto mechanism

**[O-G-04] Can the protocol replace the strategy manager without blocking user withdrawals?**
- **Answer**: Yes. Kamino V2 architecture separates Market Layer (permissionless) from curated Vault Layer. Vault manager changes do not affect underlying Kamino markets. Withdrawals always permissionless via on-chain redemption from the lending pools. Multiple curators operate on Kamino (Steakhouse, Gauntlet, Allez Labs, MEV Capital, Sentora).
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino V2](https://gov.kamino.finance/t/introducing-kamino-lend-v2/58)
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
- **Answer**: Yes. Kamino: Asaf Meir (CEO, ex-ConsenSys), Tal Zelig (CTO, ex-Bancor), Roy Keyes (COO, ex-Hubble). Kamino Finance headquartered in Panama. Steakhouse Financial: Sebastien Derivaux (Co-Founder, ex-MakerDAO Head of RWF) and Adrian Cachinero Vasiljevic (Co-Founder). Steakhouse Financial Ltd registered in Cayman Islands; Carniciera Tropical Inc. registered in Panama. Both entities have verifiable track records.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [The Org - Kamino](https://theorg.com/org/kamino-finance), [Crunchbase - Derivaux](https://www.crunchbase.com/person/s%C3%A9bastien-derivaux-af07), [Steakhouse](https://www.steakhouse.financial/)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-02] Is the protocol dependent on a single developer or small team?**
- **Answer**: No. Kamino has a full engineering team with 35+ GitHub repos and active development. Steakhouse Financial has a team of crypto-native collaborators across multiple disciplines. Both entities maintain independent operations with no single-person dependency.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [GitHub Kamino](https://github.com/Kamino-Finance), [Steakhouse GitHub](https://github.com/Steakhouse-Financial)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-03] What legal entity and jurisdiction operate the protocol and/or assets?**
- **Answer**: Kamino Finance headquartered in Panama. Steakhouse Financial operates via Carniciera Tropical Inc. (Panama) and Steakhouse Financial Ltd (Cayman Islands). Both jurisdictions and entities clearly identified with mapped operational responsibilities.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [PitchBook - Kamino](https://pitchbook.com/profiles/company/557633-98), [INATBA - Steakhouse](https://inatba.org/steakhouse-financial-limited/)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-04] Are there known investigations or regulatory actions related to the entity?** (Deal Breaker)
- **Answer**: No enforcement actions found against Kamino Finance or Steakhouse Financial. USDC issuer Circle is fully regulated (NYDFS). No regulatory issues identified for either entity.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: Research -- no actions found across major regulatory databases
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-05] Is there an on-call and incident response process for core teams?**
- **Answer**: Partial. Risk Council monitors and can pause markets. Steakhouse claims 24/7 monitoring with "redundant real-time controls" and demonstrated real-time response during stress events. However, no formal public on-call SLA, runbook, or incident response process is documented for either Kamino or Steakhouse.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Steakhouse Twitter](https://x.com/SteakhouseFi/status/1976976208962158617), [KRAF](https://docs.kamino.finance/risk/risk-assessment-framework)
- **Evidence Status**: Partial -- 24/7 monitoring claimed but no formal documentation
- **Path to Potential**: Publish documented 24/7 on-call procedures and incident runbooks

**[O-TL-06] Does the team provide timely support for critical user or integrator issues?**
- **Answer**: Yes. Active Discord, governance forum, and community support channels for both Kamino and Steakhouse. Steakhouse publishes weekly DeFi Markets Updates via Substack with relevant risk information.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Forum](https://gov.kamino.finance/), [Steakhouse Kitchen](https://kitchen.steakhouse.financial/)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-07] Are major investors or strategic partners disclosed?**
- **Answer**: Kamino backed by investors but specific funding details less disclosed than some peers. Steakhouse Financial does not appear to have external VC funding -- the firm was "founded by DAO contributors" and operates as an independent advisory/curation firm. No undisclosed investor influence detected. Per scoring rationale, "No investors" means no external influence risk, scoring Low (9).
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Steakhouse About](https://www.steakhouse.financial/about), [Crunchbase - Steakhouse](https://www.crunchbase.com/organization/steakhouse-financial)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-08] Does the strategy manager manage similar vaults creating conflict of interest?**
- **Answer**: Yes. Steakhouse Financial manages $1.26B+ across protocols including Morpho (35+ vaults), Sky/Grove (~$2B), and Kamino (4 vaults). They curate multiple USDC vaults (Steakhouse USDC on Morpho, USDC Prime on Kamino) which could create allocation competition. Steakhouse has qualitative conflict policies through their multi-layer risk framework and segment structuring (Prime vs High Yield) but no hard-coded per-vault allocation constraints are documented.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Steakhouse Wrapped 2025](https://kitchen.steakhouse.financial/p/steakhouse-wrapped-2025), [Steakhouse Risk Framework](https://www.steakhouse.financial/docs/risk-management)
- **Evidence Status**: Verified
- **Comments**: Multiple overlapping USDC lending mandates across protocols (Morpho + Kamino) create potential allocation conflicts. Qualitative controls exist but no hard constraints.
- **Path to Potential**: Implement hard-coded conflict controls and per-vault allocation rules

**[O-TL-09] Has the strategy manager previously been involved in products with collateral loss?**
- **Answer**: No. Steakhouse Financial claims to be "the only major curator with no bad debt events" across all mandates. During the Stream Finance and Elixir collapses in 2025, Steakhouse had zero exposure. Zero bad debt across all Kamino vaults during Nov 2025 and Feb 2026 stress events. Clean track record.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Steakhouse Wrapped 2025](https://kitchen.steakhouse.financial/p/steakhouse-wrapped-2025), [Feb 2026 Risk Event](https://gov.kamino.finance/t/kamino-risk-event-analysis-feb-5-6-2026/868)
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
- **Answer**: Yes. Comprehensive Kamino docs at docs.kamino.finance. Litepaper, risk guides, oracle documentation. Updated for V2 in May 2025. Steakhouse provides additional risk framework documentation at steakhouse.financial/docs. Monthly risk insight reports published on governance forum.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Docs](https://docs.kamino.finance), [Steakhouse Docs](https://www.steakhouse.financial/docs)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-DT-02] Is it clearly documented how collateral is used and when loss occurs?**
- **Answer**: Yes. Detailed liquidation docs, interest rate mechanics, risk parameters. Loss scenarios documented. KRAF dashboard with shock scenarios available. Steakhouse's risk framework adds additional collateral assessment documentation with layers and pillars.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Risk Docs](https://docs.kamino.finance/products/borrow-lend/position-risk-and-liquidations), [KRAF](https://risk.kamino.finance), [Steakhouse Collateral](https://www.steakhouse.financial/docs/risk-management/collateral/layers-pillars-and-criteria)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-DT-03] Are all contract, proxy and implementation addresses documented in one canonical place?**
- **Answer**: Yes. Program IDs published in docs. GitHub contains all contracts. KLend mainnet: KLend2g3cP87fffoy8q1mQqGKjrxjC8boSyAYavgmjD. Vault-specific address (USDC Prime): HDsayqAsDWy3QvANGqh2yNraqcD8Fnjgh73Mhb3WRS5E.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [GitHub klend](https://github.com/Kamino-Finance/klend), [SDK Docs](https://docs.kamino.finance/build-on-kamino/sdk-and-smart-contracts)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-DT-04] Are roles, permissions and timelocks documented with visible change history?**
- **Answer**: Partial. Risk Council role documented. Specific admin roles and timelock durations not fully detailed. No visible change history for role assignments. Curator roles described at high level but detailed permission registry missing.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Kamino Docs](https://docs.kamino.finance)
- **Evidence Status**: Partial
- **Path to Potential**: Publish detailed role registry with timelock configurations and change history

**[O-DT-05] Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities?** (Deal Breaker)
- **Answer**: Yes. Real-time Risk Dashboard at risk.kamino.finance shows all positions on-chain. All lending positions verifiable. USDC has Circle monthly attestations. Proof-of-liabilities applicable (lending protocol with outstanding borrows) and visible via dashboard and on-chain data.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [KRAF](https://risk.kamino.finance), [Circle Transparency](https://www.circle.com/en/usdc#transparency)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-DT-06] Are all contracts verified on the leading block explorers?**
- **Answer**: Yes. Open-source code on GitHub. Solana explorer verification. Verifiable builds ensure deployed code matches audited source. 18+ audit reports publicly available.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [GitHub](https://github.com/Kamino-Finance), [Kamino Security](https://kamino.com/security)
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
- **Answer**: No dedicated safety module disclosed. 10% KMNO token allocation for liquidity/treasury but no ring-fenced loss coverage fund with binding activation rules. No explicit commitment to use reserves for user losses.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [Token Info](https://docs.kamino.finance/kmno/token-info)
- **Evidence Status**: Verified
- **Path to Potential**: Create dedicated safety module with binding activation rules

**[O-FR-02] How large and liquid are the backstop reserves and treasury relative to TVL?**
- **Answer**: Treasury size not publicly disclosed. DeFiLlama does not track Kamino treasury separately. 10% of KMNO supply (1B tokens) allocated to liquidity/treasury, but current liquid balance and composition are unknown. $1.5M bug bounty indicates some reserves exist. No treasury dashboard or public wallet disclosure found.
- **Current Score**: 3
- **Potential Score**: 9
- **Classification**: Source Missing
- **Evidence**: DeFiLlama treasury page does not exist for Kamino. [Token Info](https://docs.kamino.finance/kmno/token-info) mentions 10% allocation but no current balances.
- **Evidence Status**: Missing -- no verifiable treasury data
- **Path to Potential**: Publish treasury composition, wallet addresses, and establish reserve target relative to TVL

**[O-FR-03] What is the estimated operational runway at current burn?**
- **Answer**: Both entities appear well-funded. Kamino generates sustainable protocol fees from $2.1B+ TVL (dominant Solana lending protocol). Steakhouse Financial is independent and self-sustaining, managing $1.26B+ across protocols with fee revenue. No public burn rate data, but revenue from dominant market position suggests >24 month runway.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [DeFiLlama - Kamino](https://defillama.com/protocol/kamino), [Steakhouse Wrapped 2025](https://kitchen.steakhouse.financial/p/steakhouse-wrapped-2025)
- **Evidence Status**: Verified at high level
- **Path to Potential**: N/A

**[O-FR-04] How have TVL, revenue and buffers behaved in past stress events?**
- **Answer**: Resilient. November 2025: Kamino supply contracted to $3.6B (-19%) and debt declined to $1.3B (-18%) during SOL drawdown from $188 to $134 (-29%), but zero bad debt generated. February 2026: Protocol maintained $2.70B supply and $1.00B borrow post-event with zero bad debt across 55,649 liquidations. Steakhouse confirmed vaults maintained liquidity throughout both events.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Nov 2025 Report](https://gov.kamino.finance/t/kamino-lend-monthly-risk-insights-november-2025/859), [Feb 2026 Risk Event](https://gov.kamino.finance/t/kamino-risk-event-analysis-feb-5-6-2026/868)
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-FR-05] Can the protocol remain safe in maintenance mode if team disappears?**
- **Answer**: Partially. On-chain contracts would continue. Withdrawals permissionless via direct contract interaction. However, vault curation (Steakhouse) and risk monitoring (Risk Council) would cease. Users could still exit via the underlying lending pools. No proprietary off-chain services are required for basic withdrawal functionality.
- **Current Score**: 9
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [Kamino Docs](https://docs.kamino.finance)
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
| | **Security Subtotal** | **123** | **171** | **253.6** | **360** |
| **Strategy** | Protocol Mechanics | 60 | 72 | 37.5 | 45 |
| | Collateral | 21 | 27 | 35.0 | 45 |
| | Infra Counterparty | 48 | 54 | 40.0 | 45 |
| | Protocol Counterparty | 45 | 45 | 45.0 | 45 |
| | Liquidity | 63 | 81 | 35.0 | 45 |
| | Market | 45 | 45 | 45.0 | 45 |
| | **Strategy Subtotal** | **282** | **324** | **237.5** | **270** |
| **Operations** | Governance | 16 | 36 | 30.0 | 67.5 |
| | Team & Legal | 69 | 81 | 57.5 | 67.5 |
| | Documentation | 48 | 54 | 60.0 | 67.5 |
| | Financial Resilience | 33 | 45 | 49.5 | 67.5 |
| | **Operations Subtotal** | **166** | **216** | **197.0** | **270** |
| **TOTAL** | | | | **688.1** | **900** |

---


---
