# Morpho - Gauntlet USDC Frontier V2 Vault Risk Rating

**Rating Date**: 2026-03-27
**Final Grade**: B
**Total Score**: 694.5/900 points
**Framework**: v0.1-beta

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 323.2/360 (89.8%)

#### Smart Contract Security (20% weight, 180 max points)

**NOTE: All Smart Contract Security scores are IDENTICAL to the other Morpho vault ratings under v0.1-beta (Steakhouse USDC/BB+, Gauntlet USDC Prime/BB+, Smokehouse USDC/BB-). S-SC-10 downgraded from 9 to 3 per the v0.1-beta verification principle -- monitoring cannot automatically trigger protective actions.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 25+ audits for Morpho Blue core. V2 vault infrastructure specifically audited by ChainSecurity (Tier-0), Spearbit (Tier-0), Zellic (Tier-0), Blackthorn, and $200K Cantina competition covering adapter model, ID/cap system, role interactions, timelocks, gates, and non-custodial mechanics. Formal verification by Certora. Vault (0x9a1D...) deployed via audited V2 Factory. All fund-custody/routing contracts covered by >=2 independent audits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [ChainSecurity V2 Audit](https://www.chainsecurity.com/security-audit/morpho-vault-v2), [P1] [Cantina V2 Competition](https://cantina.xyz/competitions/523e1540-f8c3-45ae-9c5d-b6d35d3a326c), [P1] [Sherlock - Blackthorn V2 Audit](https://sherlock.xyz/post/morpho-vaults-v2-blackthorn-audit-for-an-immutable-vault-standard), [P1] [GitHub vault-v2](https://github.com/morpho-org/vault-v2) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | ChainSecurity (Tier-0), Spearbit (Tier-0 via Cantina), Zellic (Tier-0), Blackthorn for V2 core. Certora (Tier-0) formal verification. Multiple Tier-0 auditors for most recent work on both V2 and MarketV1Adapter. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [ChainSecurity V2 Audit](https://www.chainsecurity.com/security-audit/morpho-vault-v2) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable (~600 LOC). The V2 vault infrastructure (shipped Oct 2025) was preceded by 5+ separate audit engagements from Tier-0 firms. V2 contracts are immutable post-deployment (no upgrade risk). The MarketV1AdapterV2 was separately audited. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [V2 Releases](https://github.com/morpho-org/vault-v2/releases) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 vulnerability patched immediately with OpenZeppelin. Certora formal verification of invariants. V2 Cantina competition findings ($200K pool) addressed in development with published fixes. All V2 audit findings resolved before mainnet deployment. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM), [P1] [V2 Releases](https://github.com/morpho-org/vault-v2/releases) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue core is immutable. Vault V2 contract (0x9a1D...) is immutable post-deployment -- core non-custodial guarantees cannot be changed. Market/adapter changes require Curator + timelock + Sentinel can revoke. V2 explicitly designed for immutability ("All vault contracts are immutable"). | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P0] Etherscan verified contract |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss in Gauntlet V2 Frontier vault. April 2025 frontend vulnerability ($2.6M) was intercepted by white hat c0ffeebabe.eth and all funds returned within minutes. V2 vault was not deployed during the November 2025 deUSD/Stream contagion. March 2026 Resolv USR exploit impacted V1 Frontier but NOT this V2 vault (different market allocations). | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No. Morpho (French nonprofit ADDMO). Gauntlet Networks Inc. ($41.8M raised, public leadership). No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No evidence of timelock reductions. V2 architecture specifies that after initial setup, timelock duration must be between 1 day and 2 weeks and changes are subject to their own timelock. No reductions documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Morpho runs active bounties on both Cantina ($2.5M max) and Immunefi ($1.5M max for V2 smart contract bugs). V2 contracts explicitly in scope. 236+ findings submitted on Cantina since March 2024. Standing program, not time-limited. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3), [P1] [Immunefi Bounty](https://immunefi.com/bug-bounty/morpho/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Gauntlet partners with Hypernative (real-time monitoring), ZeroShadow (24/7 vSOC), Chainalysis, and SEAL Intel. Morpho runs internal monitoring bots. However, per v0.1-beta verification principle: monitoring exists but cannot automatically trigger protective actions -- no on-chain circuit breakers, no automated pause capability. During March 2026 Resolv exploit on V1 Frontier, the Public Allocator continued auto-supplying capital to broken markets for hours, demonstrating monitoring alerts are NOT connected to automated protective actions. Same limitation applies to V2 architecture. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Building Institutional Security](https://www.gauntlet.xyz/resources/building-an-institutional-grade-security-posture-at-gauntlet), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design on Morpho Blue (immutable). V2 introduces the Sentinel role which can reactively deallocate funds, decrease caps, and revoke pending proposals -- an improvement over V1 where Guardian could only veto. However, Sentinel actions are still manual/reactive, not automatically triggered by on-chain invariant breaches. Circuit breakers do not cover automated allocation mechanisms. | 3 | 3 | Non-Improvable | [P1] [Morpho Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Smart Contract Security Subtotal: 158.2/180 (87.9%)**
- 9 questions scored 9 (sum = 81), 2 questions scored 3 (sum = 6)
- Raw sum = 87 out of max 99
- Weighted = (87/99) x 180 = 158.2

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Vault Owner is a 4-of-7 GnosisSafe multisig (0xC684...fAec, Safe v1.3.0, 522 transactions). Sentinel is a 3-of-7 GnosisSafe multisig (0x7084...f3cD, Safe v1.4.1). Curator is a 3-of-7 GnosisSafe multisig (0x9E33...0585, 330 transactions). Owner is also listed as a Curator. All changes visible on-chain via Safe Transaction Service. V2 per-function timelocks: setIsAllocator 3d, gates 7d, adapters 3-7d, fees 1d, caps 3d, abdicate 7d. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API Sentinel](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x7084bF4dB6c21e1834dD6482f6056a39A33584cD/), [P0] [Safe API Curator](https://safe-transaction-mainnet.safe.global/api/v1/safes/0x9E33faAE38ff641094fa68c65c2cE600b3410585/), [P1] [V2 Roles](https://docs.morpho.org/curate/tutorials-v2/roles/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. V2 vault is immutable post-deployment. Morpho Blue uses immutable logic. Multisig + timelock + Sentinel oversight required. Permissionless ERC4626 redemption always available. V2 non-custodial guarantees are explicitly designed to be permanent. Owner multisig is 4-of-7 (threshold >= 3, signers >= 5). | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner multisig is 4-of-7 (meets >=4-of-7 threshold for Low risk). 7 distinct EOA signers verified via Safe API. Transaction history shows 4+ different signers proposing and executing across recent transactions. Gauntlet is a publicly identified company (Tarun Chitra CEO, 50+ employees) so at least one signer is identifiable. Sentinel (3-of-7) and Curator (3-of-7) provide additional safety layers. No multisig changes in recent months. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API Owner](https://safe-transaction-mainnet.safe.global/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/), [P0] [Safe API Owner Txs](https://safe-transaction-mainnet.safe.global/api/v1/safes/0xC684c6587712e5E7BDf9fD64415F23Bd2b05fAec/multisig-transactions/) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking on Morpho Blue (immutable). V2 introduces Gates for access control but these are compliance features, not withdrawal censorship -- gates are timelocked and can be permanently disabled via abdication. V2 non-custodial guarantees preserved by design. Withdrawals always permissionless. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Gates](https://docs.morpho.org/curate/concepts/gates/), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% in non-custodial Morpho Blue contracts on Ethereum. Permissionless ERC4626 redemption. No off-chain custody. V2 explicitly designed to maintain non-custodial guarantees. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. Vault funds in Morpho Blue markets, separate from treasury/ops. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | V2 uses adapter-based allocation to Morpho Blue markets. Adapters must be enabled via addAdapter (timelocked action). Markets: syrupUSDC/USDC, sdeUSD/USDC, PT-sdeUSD/USDC, PT-sUSDE/USDC (all at 91.5% LLTV). V2 multi-dimensional ID & cap system allows both absolute and relative caps. Supply caps per market enforced on-chain. Whitelist aligned with Frontier mandate. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Adapter Docs](https://docs.morpho.org/curate/tutorials-v2/listing-adapters/), [P3] [Morpho App](https://app.morpho.org/ethereum/vault/0x9a1D6bd5b8642C41F25e0958129B85f8E1176F3e/gauntlet-usdc-frontier) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Gauntlet has ZeroShadow (24/7 SOC), Hypernative, SEAL Intel partnerships. Morpho docs include emergency procedures for vault roles. V2 Sentinel role enables faster de-risking. No public vault-specific incident playbook or tabletop exercise published. The March 2026 Resolv incident response on V1 Frontier -- specifically the failure to halt automated allocations for hours -- suggests playbook gaps. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P1] [Morpho Emergency Procedures](https://docs.morpho.org/curate/emergency/) |

**Key Management Subtotal: 165.0/180 (91.7%)**
- 7 questions scored 9 (sum = 63), 1 question scored 3 (sum = 3)
- Raw sum = 66 out of max 72
- Weighted = (66/72) x 180 = 165.0

---

### **Security Total: 323.2/360 (89.8%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 158.2 | 180 | 87.9% |
| Key Management | 165.0 | 180 | 91.7% |
| **Security Total** | **323.2** | **360** | **89.8%** |

---

### STRATEGY (30% Weight) -- Score: 149.3/270 (55.3%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield from USDC lending interest against exotic collateral + MORPHO emissions + syrupUSDC (Maple) incentives. 100% mandate-aligned (Frontier targets maximum yield). However, percent breakdown between organic and incentive yield is incomplete. Estimated 30-70% from incentives. | 3 | 9 | **Improvable** | [P1] [Gauntlet Frontier Announcement](https://www.gauntlet.xyz/resources/introducing-gauntlet-frontier-vaults-on-the-hunt-for-defi-yields), [P3] [Morpho App](https://app.morpho.org/ethereum/vault/0x9a1D6bd5b8642C41F25e0958129B85f8E1176F3e/gauntlet-usdc-frontier), [P3] [Merkl](https://app.merkl.xyz/opportunities/ethereum/ERC20LOGPROCESSOR/0x9a1D6bd5b8642C41F25e0958129B85f8E1176F3e) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss in plausible single-shock events: (1) syrupUSDC depeg if Maple borrowers default (Cayman injunction active); (2) sdeUSD already collapsed 98% in Nov 2025; (3) PT-sUSDE maturity risk if USDe depegs; (4) 91.5% LLTV provides only ~8.5% buffer. These are severe but plausible events. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault lends USDC at 1.0x effective leverage. No rehypothecation. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | V2 Frontier vault itself has not experienced bad debt. However, Gauntlet Frontier V1 (0xc582...) is a comparable variant per framework guidance ("same codebase with parameter changes only = comparable") -- same Morpho protocol, same curator (Gauntlet), same deposited asset (USDC), differing only in collateral parameters. V1 Frontier experienced confirmed bad debt (~$7.5M+) during the March 2026 Resolv USR exploit, with losses socialized to lenders (uncompensated). $7.5M is >0.5% of V1's pre-exploit peak TVL (~$115M). Additionally, the November 2025 MEV Capital sdeUSD loss (3.6%, different curator but same protocol) adds to comparable variant history. | 1 | 1 | Non-Improvable | [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit), [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025), [P4] [Coinfomania](https://coinfomania.com/morpho-delists-elixir-sdeusd-bad-debt/) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Gauntlet VaultBook with curation methodology, risk factors, due diligence, market allocation strategy. Clear Prime/Balanced/Frontier tiering. Agent-based simulations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Curation Methodology](https://vaultbook.gauntlet.xyz/morpho-vaults/curation-methodology-and-risk-factor-overview) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Partially incentive-driven. Organic yield from lending interest + MORPHO emissions + Maple syrupUSDC incentives. Estimated 30-70% from incentives/emissions. Would remain positive without incentives but materially lower. No formal taper plan published. | 3 | 9 | **Improvable** | [P1] [VaultBook Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees), [P3] [Merkl](https://app.merkl.xyz/opportunities/ethereum/ERC20LOGPROCESSOR/0x9a1D6bd5b8642C41F25e0958129B85f8E1176F3e) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Uncertain for V2. V1 Frontier demonstrated liquidity dropping below 1% for ~6 hours in Nov 2025. V2 vault has no independent unwind history. Same underlying market dynamics apply -- exotic collateral with thin secondary markets means slippage risk during stress is material. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Material dependency. Collateral values depend on: syrupUSDC peg (Maple health), sdeUSD peg (collapsed 98%), PT-sUSDE peg (Ethena USDe has depegged). ~30-70% of collateral backing depends on peg/spread maintenance. | 3 | 3 | Non-Improvable | [P4] [deUSD collapse](https://bitcoinethereumnews.com/finance/deusd-plunges-98-as-elixir-scrambles/) |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | V2 uses adapter-based allocation where the Curator multisig (3-of-7) and Allocator can adjust exposure. V2 caps system limits maximum per-market exposure with both absolute and relative caps. However, no automatic kill-switch exists for abnormal conditions (oracle deviation, collateral depeg, utilization spikes). The Sentinel can reactively decrease caps and deallocate but this requires manual human initiation, not automatic on-chain triggers. The March 2026 Resolv exploit on V1 demonstrated this exact failure mode on the V1 architecture. V2's improved Sentinel role is better than V1's Guardian but still manual. | 3 | 9 | **Improvable** | [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |

**Protocol Mechanics Subtotal: 20.6/45 (45.7%)**
- 9 applicable questions (ST-PM-04 = N/A): 2 scored 9 (sum = 18), 6 scored 3 (sum = 18), 1 scored 1 (sum = 1)
- Raw sum = 37 out of max 81
- Weighted = (37/81) x 45 = 20.6

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Higher-risk collateral: (1) syrupUSDC (Maple, Cayman injunction); (2) sdeUSD (Elixir, collapsed 98%, defunct); (3) PT-sdeUSD (inherits sdeUSD risk); (4) PT-sUSDE (Ethena CCC). All at 91.5% LLTV. Gauntlet tiering (Frontier) with explicit risk disclosures and supply caps. Collateral includes higher-risk assets but tiered with LTVs and caps. | 3 | 3 | Non-Improvable | [P3] [Morpho App](https://app.morpho.org/ethereum/vault/0x9a1D6bd5b8642C41F25e0958129B85f8E1176F3e/gauntlet-usdc-frontier) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | CRITICAL: sdeUSD/deUSD collapsed 98% in Nov 2025 (permanent impairment, lasting >7 days, unresolved). PT-sUSDE: Ethena USDe has depegged multiple times. syrupUSDC: No major depeg but Maple faces Cayman injunction. One collateral showed >10% depeg lasting >7 days (sdeUSD permanent). | 1 | 1 | Non-Improvable | [P4] [deUSD plunges 98%](https://bitcoinethereumnews.com/finance/deusd-plunges-98-as-elixir-scrambles/) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- No staking-based collateral. | N/A | N/A | N/A | Vault architecture |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | HIGH RISK: 100% of collateral is wrapped/synthetic/tokenized. syrupUSDC (yield-bearing wrapper), sdeUSD (staked synthetic, defunct), PT tokens (Pendle principal tokens). Exceeds 60% threshold maximally. | 1 | 9 | **Improvable** | [P3] [Morpho App](https://app.morpho.org/ethereum/vault/0x9a1D6bd5b8642C41F25e0958129B85f8E1176F3e/gauntlet-usdc-frontier) |

**Collateral Subtotal: 8.3/45 (18.5%)**
- 3 applicable questions (ST-C-03 = N/A): ST-C-01(3), ST-C-02(1), ST-C-04(1)
- Raw sum = 5 out of max 27
- Weighted = (5/27) x 45 = 8.3

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | All Tier-0/1: Ethereum (Tier-0), Chainlink (Tier-0 oracle). No bridges or CEX dependency. V2 adapter system adds contract complexity but all on Ethereum. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/) |
| ST-IC-02 | How redundant are oracle and bridge setups, and can oracle values be corrected under abnormal conditions? | **Mandatory immutable oracle check (v0.1-beta):** Each Morpho Blue market uses an immutable oracle that cannot be updated, overridden, or corrected post-deployment. Can the priced collateral depeg or lose value materially? YES -- sdeUSD already collapsed 98% in November 2025. syrupUSDC depends on Maple solvency (Cayman injunction active). PT tokens can depeg at maturity if underlying fails. Framework states: "If yes to both [immutable oracle AND asset can depeg], score High (1) -- the loss path is unbounded because attackers can buy the depegged asset cheaply and borrow against the stale oracle price indefinitely." This is NOT a battle-tested deep-liquidity asset scenario (which would allow Mid/3) -- these are exotic, novel tokens with demonstrated depeg history. The March 2026 Resolv exploit demonstrated this exact attack vector on V1 Frontier. | 1 | 1 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | No explicit SOC 2 Type II or ISO27001 for Gauntlet Networks disclosed. Chainlink holds enterprise certifications. Gauntlet operates off-chain risk engine and allocation models. | 3 | 9 | **Source Missing** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | V2 vault deployed after October 2025 -- less than 6 months of operational history at rating date. V2 has NOT been through a significant stress event independently. Per v0.1-beta new protocol guidance: "For protocols deployed <6 months with no chain-level incidents during their operational period, score Mid (3)." | 3 | 9 | **Source Missing** | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum: no halts >30 minutes in last 12+ months. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- No staking-based collateral. | N/A | N/A | N/A | Vault architecture |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- No staking-based collateral. | N/A | N/A | N/A | Vault architecture |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Permissionless ERC4626 redemption always available. V2 non-custodial guarantees ensure withdrawal availability. No off-chain dependency for withdrawals. However, the Resolv exploit on V1 demonstrated that oracle failure (stale pricing) combined with permissionless supply functions CAN cause losses (though not block withdrawals). | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |

**Infrastructure Counterparty Subtotal: 28.3/45 (63.0%)**
- 6 applicable questions (ST-IC-06, ST-IC-07 = N/A): ST-IC-01(9), ST-IC-02(1), ST-IC-03(3), ST-IC-04(3), ST-IC-05(9), ST-IC-08(9)
- 3x9=27, 2x3=6, 1x1=1 = 34. Max = 54.
- Weighted = (34/54) x 45 = 28.3

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All allocation to Morpho Blue (Tier-0) via V2 adapter. Collateral dependency chain extends to Maple (syrupUSDC), Elixir (sdeUSD/defunct), Pendle (PT tokens), Ethena (sUSDe). But vault only interacts with Morpho Blue directly. | 9 | 9 | Non-Improvable (optimal) | [P3] [Morpho App](https://app.morpho.org/ethereum/vault/0x9a1D6bd5b8642C41F25e0958129B85f8E1176F3e/gauntlet-usdc-frontier) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Maple provides syrupUSDC incentives to attract borrowers using syrupUSDC as collateral. MORPHO emissions distributed via Merkl. Arrangements disclosed but terms only partially detailed, creating potential conflict. | 3 | 9 | **Improvable** | [P1] [Incentives & Fees](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/incentives-and-performance-fees), [P3] [Merkl](https://app.merkl.xyz/opportunities/ethereum/ERC20LOGPROCESSOR/0x9a1D6bd5b8642C41F25e0958129B85f8E1176F3e) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. V2 introduces multi-dimensional ID & cap system enabling both absolute and relative caps based on shared risk factors. On-chain supply caps per market. Gauntlet automated models with continuous monitoring. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P1] [Market Allocation Strategy](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/curation-methodology-and-risk-factor-overview/market-allocation-strategy) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | V2 vault untested for unwind scenarios. V1 Frontier demonstrated 72% borrow reduction within hours via adaptive IRM in Nov 2025. Same underlying markets and collateral liquidation dynamics apply (thin secondary markets for exotic collateral). | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending. No external validators or custodians. Gauntlet (curator) disclosed. Per framework applicability check: no third-party service providers involved. | 9 | 9 | Non-Improvable (optimal) | Vault architecture |

**Protocol Counterparty Subtotal: 33.0/45 (73.3%)**
- 3 scored 9 (sum = 27), 2 scored 3 (sum = 6)
- Raw sum = 33 out of max 45
- Weighted = (33/45) x 45 = 33.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless ERC4626 redemption via V2 vault. V2 gates can control deposits/withdrawals for compliance but can be permanently disabled through abdication. No admin pause on Morpho Blue. Non-custodial guarantee preserved. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P1] [V2 Gates](https://docs.morpho.org/curate/concepts/gates/) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | UNTESTED for V2. V1 Frontier experienced liquidity dropping below 1% for ~6 hours in Nov 2025. V2 has the same underlying market dynamics. Exotic collateral types mean slower borrower repayment/liquidation. | 3 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025), [P0] Etherscan tx count |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | V2 vault too new to have meaningful withdrawal history. V1 Frontier experienced sub-1% liquidity for ~6 hours in Nov 2025. V2 has NOT been independently stress-tested. Cannot score Low for untested protocol. | 3 | 3 | Non-Improvable | [P0] Etherscan tx count, Scoring methodology (untested = Mid max) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | V2 multi-dimensional cap system is more flexible than V1's simple per-market caps. Caps appropriately designed based on V1 Frontier experience. No evidence of caps restricting exits. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | UNTESTED for V2. V1 Frontier showed liquidity dropping below 1% for ~6 hours in Nov 2025. V2 shares the same underlying markets. Cannot score Low for an untested vault -- maximum Mid per scoring principles (untested = Mid max for resilience questions). | 1 | 3 | Non-Improvable | Scoring methodology (V2 untested; V1 variant was stressed = reference point for 1 rather than 3) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No lockups on lender positions. PT token maturity dates affect borrower-side risk only. Less than ~10% exposure concern. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary ERC4626 redemption always available. V2 non-custodial design ensures direct redemption. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | USDC highly liquid but collateral types (syrupUSDC, PT tokens) have thin secondary markets. sdeUSD effectively worthless. V2 vault share liquidity untested. Depth supports ~3-10% of TVL at best. | 3 | 3 | Non-Improvable | [P3] Market data |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | ELEVATED and UNTESTED for V2. V1 Frontier experienced sub-1% liquidity, 20% TVL decline, 91.5% LLTV gives only ~8.5% buffer. V2 has same structural risks but no independent track record. Bank-run would likely cause significant queues and discounting. | 1 | 3 | Non-Improvable | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |

**Liquidity Subtotal: 26.1/45 (58.0%)**
- 4 scored 9 (sum = 36), 3 scored 3 (sum = 9), 2 scored 1 (sum = 2)
- Raw sum = 47 out of max 81
- Weighted = (47/81) x 45 = 26.1

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | V2 vault shares have NOT been stress-tested. V1 Frontier vault shares maintained value during Nov 2025 stress (zero bad debt). V2 uses the same ERC4626 NAV-based mechanism. However, V2 has no independent track record under stress. Cannot score Low for untested vault. | 3 | 9 | Non-Improvable | Scoring methodology (untested = Mid max), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Low directional risk. Vault lends USDC -- dollar-denominated. Risk is bad debt from collateral failure, not market direction. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Morpho's Adaptive Curve IRM is immutable and battle-tested on V1 markets. V1 Frontier demonstrated IRM reducing borrowing 72% during Nov 2025 stress. V2 uses the same underlying IRM via MarketV1Adapter. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. Gauntlet agent-based simulations. Nov 2025 served as real-world V1 stress test. Certora verified core liquidation mechanics. V2 adapter wraps the same underlying markets. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Exposure](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults/vault-curation-considerations-a-deeper-dive/risk-exposure) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side only. 91.5% LLTV gives only ~8.5% buffer. Exotic collateral liquidation less efficient than BTC/ETH. Higher bad debt risk than Prime. | 3 | 3 | Non-Improvable | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 33.0/45 (73.3%)**
- 3 scored 9 (sum = 27), 2 scored 3 (sum = 6)
- Raw sum = 33 out of max 45
- Weighted = (33/45) x 45 = 33.0

---

### **Strategy Total: 149.3/270 (55.3%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 20.6 | 45 | 45.7% |
| Collateral | 8.3 | 45 | 18.5% |
| Infra Counterparty | 28.3 | 45 | 63.0% |
| Protocol Counterparty | 33.0 | 45 | 73.3% |
| Liquidity | 26.1 | 45 | 58.0% |
| Market | 33.0 | 45 | 73.3% |
| **Strategy Total** | **149.3** | **270** | **55.3%** |

---

### OPERATIONS (30% Weight) -- Score: 222.0/270 (82.2%)

**NOTE: Operations scores updated under v0.1-beta. O-TL-05 downgraded from 9 to 3 (incident response must cover halting automated allocation). O-TL-09 downgraded from 9 to 3 (Gauntlet linked to uncompensated V1 Frontier losses from Resolv exploit).**

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid. Morpho Blue immutable. V2 vault immutable post-deployment. Changes to adapters and caps require Curator + timelock + Sentinel oversight. V2 introduces improved role segregation (Owner, Curator, Allocator, Sentinel). | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [V2 Roles](https://docs.morpho.org/curate/tutorials-v2/roles/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- No governance token voting for this vault. Concentration captured in S-KM-01/S-KM-03. | N/A | N/A | N/A | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | V2 per-function timelocks verified via Morpho GraphQL API: setIsAllocator 3 days, gates 7 days, adapters 3-7 days, fees 1 day, caps 3 days, abdicate 7 days. All functions have timelocks >= 24 hours (minimum is fees at 1 day). V2 Sentinel (3-of-7 multisig) can revoke malicious proposals before execution and decrease caps immediately -- bounded veto power. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho GraphQL API (vaultV2ByAddress query, verified 2026-03-10), [P1] [Timelock Docs](https://docs.morpho.org/curate/concepts/timelock/), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner can change roles (subject to timelock). Withdrawals remain permissionless via ERC4626. V2 non-custodial guarantees maintained. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 3 applicable (O-G-02 = N/A): 3 scored 9 (sum = 27)
- Raw sum = 27 out of max 27
- Weighted = (27/27) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Gauntlet: Tarun Chitra (CEO), Rei Chiang (Co-founder). 50+ team. Morpho: Paul Frambot (CEO). All publicly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Team](https://www.gauntlet.xyz/our-team) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Gauntlet 50+ employees. Morpho separate full team ($73.6M raised). | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet About](https://www.gauntlet.xyz/about) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Morpho: ADDMO (France). Gauntlet: Gauntlet Networks Inc. (New York, USA). Both clearly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known actions against Gauntlet Networks Inc. or Morpho entities. | 9 | 9 | Non-Improvable (optimal) | Public records |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Gauntlet has 24/7 on-call with ZeroShadow (vSOC), Hypernative, and SEAL Intel. However, per v0.1-beta framework: incident response MUST include documented procedures to halt automated allocation mechanisms. During March 2026 Resolv exploit on V1 Frontier, the Public Allocator continued auto-supplying capital to broken markets for hours -- demonstrating that incident response procedures did NOT cover halting automated allocation within SLA. V2's adapter-based allocation has the same structural gap -- no documented procedure to halt adapter-driven flows within the response SLA. | 3 | 9 | **Improvable** | [P1] [Gauntlet Security](https://www.gauntlet.xyz/vaults/security), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Detailed market reports. Active VaultBook. Rapid incident response. | 9 | 9 | Non-Improvable (optimal) | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Gauntlet: Polychain, Paradigm, Ribbit Capital. Morpho: a16z, Variant, Pantera, Coinbase Ventures. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay](https://www.clay.com/dossier/gauntlet-funding) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Gauntlet manages 70+ vaults with $1.4B+ AUM including Prime, Balanced, Frontier, and V2 vaults. Risk of routing riskier allocations to Frontier to protect Prime/Balanced. No formal quantitative CoI policy published. | 3 | 9 | **Improvable** | [P1] [Gauntlet VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | March 2026 Resolv USR exploit caused confirmed bad debt in Gauntlet-curated Frontier V1 and Core vaults (~$7.5M+ exposure). This V2 vault was unaffected, but the framework evaluates the manager entity. Gauntlet is linked to uncompensated depositor losses in products they curate. This constitutes "one historical loss incident with limited impact." Prior Aave advisory: $1.6M CRV bad debt from governance inaction, not Gauntlet decisions. | 3 | 9 | **Improvable** | [P1] [Gauntlet Nov 2025 Report](https://www.gauntlet.xyz/resources/market-report-liquidity-stress-period-nov-2025), [P4] [DeFi Prime - Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |

**Team & Legal Subtotal: 52.5/67.5 (77.8%)**
- 6 scored 9 (sum = 54), 3 scored 3 (sum = 9)
- Raw sum = 63 out of max 81
- Weighted = (63/81) x 67.5 = 52.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive Morpho V2 docs, Gauntlet VaultBook. V2 architecture well-documented including adapters, gates, sentinel, timelock. Frontier tier explicitly described with risk warnings. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P1] [VaultBook](https://vaultbook.gauntlet.xyz/vaults/morpho-vaults) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Liquidation mechanics, bad debt scenarios, oracle risks documented. V2 adapter risks documented. Frontier risk profile explicitly described. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Morpho V2 contract addresses documented in canonical registry. V2 Factory and adapter addresses listed. Vault address on Morpho App and Gauntlet App. Etherscan-verified. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Contracts](https://docs.morpho.org/get-started/resources/contracts/morpho-vaults-v2/), [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. V2 role documentation comprehensive (Owner, Curator, Allocator, Sentinel). V2 timelock mechanics well-documented. Changes visible on-chain. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Roles](https://docs.morpho.org/curate/tutorials-v2/roles/), [P1] [V2 Checklist](https://docs.morpho.org/curate/tutorials-v2/checklist/) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves. All allocations visible on Morpho App and Etherscan. V2 adapter system transparently reports current asset values. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0x9a1D6bd5b8642C41F25e0958129B85f8E1176F3e), [P3] [Morpho App](https://app.morpho.org/ethereum/vault/0x9a1D6bd5b8642C41F25e0958129B85f8E1176F3e/gauntlet-usdc-frontier) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. V2 vault contract verified on Etherscan. Full source code readable. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0x9a1D6bd5b8642C41F25e0958129B85f8E1176F3e) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated safety module. Bad debt socialized per market. Morpho DAO treasury (~$33.8M, mostly MORPHO tokens) discretionary. No Gauntlet-specific backstop. No binding activation rules. | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Insufficient. Morpho DAO treasury ~$33.8M (entirely MORPHO tokens, no stablecoins) against ~$10B+ protocol-wide TVL (0.34%). Not ring-fenced. No vault-specific reserve disclosed. | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Gauntlet $41.8M raised, $1B valuation. Morpho $73.6M raised. Combined runway >24 months. | 9 | 9 | Non-Improvable (optimal) | [P4] [Clay](https://www.clay.com/dossier/gauntlet-funding) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | V2 vault NOT stress-tested -- deployed post-Oct 2025. V1 Frontier TVL declined 20% during Nov 2025, then 88% post-Resolv exploit. V2 has no independent resilience track record. Cannot score Low for untested vault per scoring principles (untested = Mid max for resilience questions). | 1 | 3 | Non-Improvable | Scoring methodology (V2 untested; V1 reference shows structural vulnerability) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue immutable. V2 vault immutable. Permissionless ERC4626 withdrawals. V2 non-custodial guarantees ensure safe maintenance mode. No proprietary off-chain services required. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |

**Financial Resilience Subtotal: 34.5/67.5 (51.1%)**
- 2 scored 9 (sum = 18), 1 scored 3 (sum = 3), 2 scored 1 (sum = 2)
- Raw sum = 23 out of max 45
- Weighted = (23/45) x 67.5 = 34.5

---

### **Operations Total: 222.0/270 (82.2%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 67.5 | 67.5 | 100.0% |
| Team & Legal | 52.5 | 67.5 | 77.8% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 34.5 | 67.5 | 51.1% |
| **Operations Total** | **222.0** | **270** | **82.2%** |

Validation: 67.5 + 52.5 + 67.5 + 34.5 = 222.0 -- VERIFIED

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 87 | 99 | 158.2 | 180 | 87.9% |
| | Key Management (8 Q) | 66 | 72 | 165.0 | 180 | 91.7% |
| | **Security Subtotal** | | | **323.2** | **360** | **89.8%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 37 | 81 | 20.6 | 45 | 45.7% |
| | Collateral (3 of 4 Q scored) | 5 | 27 | 8.3 | 45 | 18.5% |
| | Infra Counterparty (6 of 8 Q scored) | 34 | 54 | 28.3 | 45 | 63.0% |
| | Protocol Counterparty (5 Q) | 33 | 45 | 33.0 | 45 | 73.3% |
| | Liquidity (9 Q) | 47 | 81 | 26.1 | 45 | 58.0% |
| | Market (5 Q) | 33 | 45 | 33.0 | 45 | 73.3% |
| | **Strategy Subtotal** | | | **149.3** | **270** | **55.3%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 63 | 81 | 52.5 | 67.5 | 77.8% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 23 | 45 | 34.5 | 67.5 | 51.1% |
| | **Operations Subtotal** | | | **222.0** | **270** | **82.2%** |
| **TOTAL** | | | | **694.5** | **900** | **77.2%** |

---

