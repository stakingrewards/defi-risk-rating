# BENQI - sAVAX (Staked AVAX) Risk Rating

**Rating Date**: 2026-06-20
**Final Grade**: CCC
**Total Score**: 557.7/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 214.1/360 (59.5%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | sAVAX `StakedAvax` core contract audited by Halborn (Nov 2021-Feb 2022) and formally verified by Certora (April 2022); oracle contracts by Zellic; Chaos Labs dual-oracle audit (May 2025). >=2 independent firms with public reports. Deployment-configuration scope (MPC custody bot, role assignments) not explicitly stated as in audit scope -> Mid criteria for config. | 3 | 9 | **Improvable** | [P1] Risks & Audits (docs.benqi.fi/resources/risks) [P0] Verified implementation 0xB791C7A4...79719FA53 on Snowtrace |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent sAVAX-relevant audit is Chaos Labs dual-oracle (May 2025); core verifications by Certora (Tier-0) and Halborn (Tier-1); oracle review by Zellic (Tier-0). At least one recent audit by a Tier-0/1 firm. | 9 | 9 | Non-Improvable (optimal) | [P1] docs.benqi.fi/resources/risks; Certora/Halborn/Zellic are Tier-0/1 per SR list |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | sAVAX implementation was upgraded (current 0xB791C7A4..., last upgrade 2024-10-31; prior impls 0x0ce7f6.../0x0ebc3e...). No public audit report or published diff tied specifically to the 2024 upgrade could be located. | 3 | 9 | **Source Missing** | [P0] Snowscan proxy upgrade to 0xB791C7A4... dated 2024-10-31. [P1] No matching audit/diff found in docs |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Halborn and Certora engagements report no unresolved critical/high issues for sAVAX core; Certora formal verification confirms contract invariants. No open critical/high findings identified. | 9 | 9 | Non-Improvable (optimal) | [P1] docs.benqi.fi/resources/risks (Halborn + Certora reports) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | `TransparentUpgradeableProxy` — upgradeable. A team multisig is documented (Aave ARC 2022), but the current upgrade-admin threshold and any timelock could not be verified on-chain and are not documented. Upgrade constraints undocumented. | 3 | 9 | **Improvable** | [P0] Proxy=1 verified on Snowtrace (admin slot not publicly labeled). [P2] Aave ARC: "4/7 multisig held by the team" |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss across BENQI's full history (since Aug 2021 / sAVAX since Feb 2022). No rekt.news entry for sAVAX; survived 2022-2023 market collapses operationally intact. | 9 | 9 | Non-Improvable (optimal) | [P4] No rekt.news / DeFiLlama-hacks entry for BENQI sAVAX. [P0] No exploit tx pattern on contract |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull and no unresolved credible allegations. Team is publicly identified (Rome Blockchain Labs; JD Gagnon, Hannu Kuusi, Alexander Szul). | 9 | 9 | Non-Improvable (optimal) | [P4] CB Insights / NewsBTC team coverage; no allegations found |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No on-chain timelock is documented for sAVAX upgrades, so no reduction has occurred; absence of a documented timelock is penalized under S-SC-05/O-G-03 rather than here. Criteria "no reductions / only increases" technically met. | 9 | 9 | Non-Improvable (optimal) | [P0] No timelock contract identified; [P1] no disclosed reduction event |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Active Immunefi bug bounty, max payout $500,000, BENQI Liquid Staking (BLS/sAVAX) explicitly in scope; live since Aug 2021, last updated Nov 27, 2025. Well above the $100k Low threshold. | 9 | 9 | Non-Improvable (optimal) | [P1] immunefi.com/bug-bounty/benqi (max $500k, BLS in scope) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | BENQI partners with Chaos Labs for continuous risk-parameter monitoring (dashboard). No disclosure that monitoring covers sAVAX-specific invariants (abnormal minting, exchange-rate deviation) or is wired to automated protective actions / response SLAs. | 3 | 9 | **Source Missing** | [P1] docs.benqi.fi/resources/risks (Chaos Labs dashboard). No invariant/SLA detail for sAVAX |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | `pause()`/`resume()` and `pauseMinting()` exist (role-restricted), so pause capability is present, but no evidence these are auto-triggered by monitoring; trigger procedures undocumented -> manual triggers. | 3 | 9 | **Improvable** | [P0] ROLE_PAUSE / ROLE_PAUSE_MINTING in verified StakedAvax. [P1] No documented auto-trigger rules |

**Smart Contract Security Subtotal:**
- Scores: S-SC-01(3), S-SC-02(9), S-SC-03(3), S-SC-04(9), S-SC-05(3), S-SC-06(9), S-SC-07(9), S-SC-08(9), S-SC-09(9), S-SC-10(3), S-SC-11(3)
- Count: 6 x 9 = 54, 5 x 3 = 15
- Raw: 54 + 15 = 69 out of max 99
- Adjusted: (69/99) x 180 = **125.5/180 (69.7%)**

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Admin/upgrade rights held by a documented team multisig (Aave ARC 2022: 4/7, expanding to external partners). Current configuration and role-change history not published or independently verifiable on-chain (admin resolves to an unverified deployer/admin contract performing Grant/Revoke Role). | 3 | 9 | **Source Missing** | [P2] Aave ARC 7892 ("4/7 multisig held by team"). [P0] Admin contract 0xb5d72f... (unverified; Grant/Revoke Role txns) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | A multisig is documented and sAVAX cannot be minted without staking AVAX (no arbitrary issuance). However, threshold >=3-of-5 AND a >=24h timelock could not be confirmed on-chain, so the Low bar is not met; no single-key control was demonstrated either. | 3 | 9 | **Improvable** | [P2] Aave ARC multisig; [P0] minting requires `submit()` staking AVAX (verified). Timelock not verifiable |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Documented multisig with named external partners (Avalaunch, Pendle, Aave) in the 2022 expansion, but the current signer set and threshold are not published in docs nor verifiable on-chain — independence cannot be confirmed. Per criteria, cap at Mid (3) when signer identities are unverifiable. | 3 | 9 | **Source Missing** | [P2] Aave ARC names some signers (2022). [P1] No current canonical signer registry in docs |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause/resume and pause-minting are role-restricted (multisig roles). No address-level blocklist/censorship function in the sAVAX contract. Pause scope is protocol-wide, not address-selective; rules only partially documented. | 9 | 9 | Non-Improvable (optimal) | [P0] StakedAvax has ROLE_PAUSE/ROLE_RESUME, no blacklist function in verified source |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Staked AVAX is bridged to the P-Chain and delegated to validators; per docs "funds are secured via MPC encryption on the P-Chain." A material portion of underlying AVAX is therefore held via an MPC custody bridge rather than a fully non-custodial C-Chain contract. | 3 | 3 | Non-Improvable | [P1] docs architecture: "MPC encryption ... bridged to the C-Chain"; P-Chain delegation off the C-Chain contract |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | sAVAX staking pool (`StakedAvax`) is distinct from the QI DAO treasury and operational wallets; on-chain the staking contract holds pooled AVAX/shares separate from the QI token contract and treasury. No evidence of co-mingling. | 9 | 9 | Non-Improvable (optimal) | [P0] Separate contracts: sAVAX 0x2b2C..., QI 0x8729..., treasury holds QI only |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- sAVAX is a liquid staking token, not a managed vault strategy. Staked AVAX is delegated only to Avalanche validators via Node Voting; users deploy sAVAX across DeFi at their own discretion. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No published incident-response playbook for sAVAX admin-key compromise or signer loss; no evidence of a tabletop/simulation in the last 12 months. | 1 | 9 | **Improvable** | [P1] No incident playbook found in docs.benqi.fi/resources/risks or elsewhere |

**Key Management Subtotal (7 scored questions, 1 N/A):**
- Scores: S-KM-01(3), S-KM-02(3), S-KM-03(3), S-KM-04(9), S-KM-05(3), S-KM-06(9), S-KM-08(1)
- Count: 2 x 9 = 18, 4 x 3 = 12, 1 x 1 = 1
- Raw: 18 + 12 + 1 = 31 out of max 63
- Adjusted: (31/63) x 180 = **88.6/180 (49.2%)**

**Security Total: 125.5 + 88.6 = 214.1/360 (59.5%)**

Potential Security: SC 180.0 + KM 162.9 = **342.9/360 (95.3%)** — KM potential: S-KM-01/02/03 -> 9, S-KM-04 -> 9 (already), S-KM-05 capped at 3 (MPC custody, Non-Improvable), S-KM-06 -> 9 (already), S-KM-08 -> 9 = 6 x 9 + 1 x 3 = 57/63 x 180 = 162.9.

### STRATEGY (30% Weight) -- Score: 219.5/270 (81.3%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | 100% of yield is native Avalanche staking rewards from delegating pooled AVAX to P-Chain validators; protocol takes ~10% of validator rewards. Fully aligned with the "AVAX liquid staking" mandate; value accrues into the sAVAX exchange rate. | 9 | 9 | Non-Improvable (optimal) | [P1] docs overview ("protocol earns 10% of rewards"); [P0] exchange-rate accrual via getPooledAvaxByShares |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail events: mass validator slashing/penalties on Avalanche (historically minimal — delegators are not slashed for principal), an sAVAX contract exploit, or MPC-custody failure. No leverage. | 9 | 9 | Non-Improvable (optimal) | [P1] docs architecture; Avalanche delegation has no principal slashing for delegators |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage or rehypothecation at the protocol level; sAVAX is a 1:1 claim on staked AVAX plus accrued rewards (effective leverage 1.0x). Users may lever sAVAX externally at their own risk. | 9 | 9 | Non-Improvable (optimal) | [P0] StakedAvax mints only against submitted AVAX; no borrow logic |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- sAVAX is a liquid staking token, not a leveraged/borrowing position; no LTV, liquidation threshold, or deleveraging mechanic. | N/A | N/A | N/A | - |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss events for sAVAX or comparable AVAX-LST variant over its full history; exchange rate has increased monotonically since Feb 2022. AVAX delegation does not slash delegator principal. | 9 | 9 | Non-Improvable (optimal) | [P0] Monotonic exchange rate (getPooledAvaxByShares); [P4] no loss events recorded |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | N/A -- sAVAX is a liquid staking token, not a curated vault strategy. | N/A | N/A | N/A | - |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yield (~4.94% APY) is 100% organic Avalanche staking rewards; no token emissions or incentive dependency in the sAVAX yield. Sustainable as long as Avalanche PoS operates. | 9 | 9 | Non-Improvable (optimal) | [P3] ~4.94% APY; [P1] docs: yield = validator rewards (no emissions) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Native redemption (15-day cooldown + 48h claim) returns AVAX 1:1 at the exchange rate with no slippage; instant exit via AMM incurs only modest discount/fees. Conservative unwind well within 1-2% cost. | 9 | 9 | Non-Improvable (optimal) | [P1] docs: 15-day cooldown direct claim; AMM instant swap |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. sAVAX yield is 100% organic Avalanche staking rewards from P-Chain validator delegation — no spread, peg, or funding-rate carry drives yield (0% reliance, far below the 30% Low threshold). sAVAX is value-accruing with deterministic native redemption at the exchange rate; secondary-market discount under stress is a market/liquidity risk captured in ST-M-01, not a strategy yield dependency. Consistent with value-accruing LSTs Lido stETH, RocketPool rETH, Etherfi eETH, Stader ETHx, StakeWise osETH (all 9). | 9 | 9 | Non-Improvable (optimal) | [P1] docs overview (yield = 100% validator staking rewards); secondary discount captured in ST-M-01 |

**Protocol Mechanics Subtotal (7 scored questions, 2 N/A):**
- Scores: 7 x 9 = 63
- Raw: 63 out of max 63
- Adjusted: (63/63) x 45 = **45.0/45 (100%)**

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Native AVAX only. AVAX is the native gas/staking asset of Avalanche (Tier-1 chain per SR list), a large-cap, deeply liquid asset. Single-asset, highest-quality available for an Avalanche-native LST; no exotic or illiquid assets accepted -> low risk by this reasoning. | 9 | 9 | Non-Improvable (optimal) | [P0] StakedAvax `submit()` accepts only AVAX; [P1] docs |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | sAVAX is value-accruing; native redemption tracks the exchange rate exactly. No documented sAVAX-vs-AVAX secondary deviation >2% lasting >24h within the last 12 months. Long history but no specific quantified stress-survival event documented -> Mid per the cautious "demonstrated history" standard. | 3 | 9 | **Source Missing** | [P3] CoinGecko sAVAX price tracking; [P4] no documented >2% sustained deviation in 12m |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Avalanche delegation does not slash delegator principal (uptime-based rewards only); BENQI diversifies across many validators via the 35/65 Node Voting split. Slashing risk is structurally minimal; mitigation via diversification but no explicit insurance/reserve buffer for the rare penalty case. | 3 | 9 | **Improvable** | [P1] docs node-voting (35/65 split); Avalanche has no delegator slashing but no documented buffer |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | Underlying is native AVAX staked on Avalanche's own P-Chain via BENQI's internal MPC custody movement (C<->P), not a third-party token bridge. No third-party bridged/wrapped tokens back sAVAX. | 9 | 9 | Non-Improvable (optimal) | [P1] docs architecture (native AVAX, internal MPC C/P movement, no wrapped backing) |

**Collateral Subtotal:**
- Scores: 2 x 9 = 18, 2 x 3 = 6
- Raw: 18 + 6 = 24 out of max 36
- Adjusted: (24/36) x 45 = **30.0/45 (66.7%)**

#### Infra Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Dependencies: Avalanche C-Chain + P-Chain (Tier-1), Chainlink + Edge oracles (Tier-0/1), MPC custody bot (internal). All named; only Tier-0/1 external counterparts. No third-party bridge or CEX dependency. | 9 | 9 | Non-Improvable (optimal) | [P1] docs price-feeds (Chainlink sAVAX 0x2854Ca...); architecture (Avalanche P-Chain) |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | sAVAX redemption value is computed on-chain from totalPooledAvax/totalShares (not oracle-dependent). For external pricing, a Chainlink feed plus an Edge dual-oracle (Chaos Labs reconciliation, May 2025) provide redundancy; both are updatable Tier-0/1 feeds with no hardcoded pricing. | 9 | 9 | Non-Improvable (optimal) | [P1] Chainlink sAVAX + Edge oracle addresses; Chaos Labs dual-oracle audit May 2025 |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | BENQI runs an off-chain MPC custody/delegation system. No SOC 2 / ISO 27001 certification for this off-chain infrastructure is disclosed. Certification status not published. | 3 | 9 | **Source Missing** | [P1] docs describe MPC bot but disclose no SOC2/ISO27001 certification |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Avalanche C-Chain has had brief outages (Feb 2024 ~5-6h; March 2023 ~1h). These caused temporary degraded access but no sAVAX user losses or permanently blocked withdrawals; recovered fully. >6 months operated, transparent impact. | 9 | 9 | Non-Improvable (optimal) | [P4] Blockworks/DLNews Avalanche outage coverage; no sAVAX loss; recovered |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Avalanche C-Chain had no halt >30 min in the last 12 months (June 2025-June 2026). The Feb 2024 (~5-6h) and March 2023 (~1h) outages are outside the 12-month lookback window. | 9 | 9 | Non-Improvable (optimal) | [P4] Feb 2024 / March 2023 outages both >12 months ago; none since |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | No slashing events affecting BENQI-delegated validators that impacted sAVAX value in the last 12 months. Avalanche delegation does not slash principal; uptime penalties only marginally reduce rewards. | 9 | 9 | Non-Improvable (optimal) | [P1] Avalanche staking model (no delegator principal slashing); no reported events |
| ST-IC-07 | Are validators diverse geographically and by operator? | AVAX is delegated across many Avalanche validators via Node Voting (35% Miles Pool + 65% Open Pool to performance-qualified validators), avoiding single-operator concentration. Exact per-operator shares not published, but design distributes broadly with no single operator >25% evident. | 9 | 9 | Non-Improvable (optimal) | [P1] docs node-voting/delegation-pools (35/65 distribution across many validators) |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | The MPC custody/delegation system is operationally important: a failure could delay native unstake settlement. However, sAVAX holders retain an independent on-chain exit via AMM secondary markets, and native redemption is queue-based; a single component failure would at most delay (not permanently block) within 24-48h. | 3 | 3 | Non-Improvable | [P1] MPC bot processes P-Chain redemptions; [P3] AMM secondary markets provide alternate exit |

**Infra Counterparty Subtotal:**
- Scores: ST-IC-01(9), ST-IC-02(9), ST-IC-03(3), ST-IC-04(9), ST-IC-05(9), ST-IC-06(9), ST-IC-07(9), ST-IC-08(3)
- Count: 6 x 9 = 54, 2 x 3 = 6
- Raw: 54 + 6 = 60 out of max 72
- Adjusted: (60/72) x 45 = **37.5/45 (83.3%)**

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Pooled AVAX is delegated exclusively to Avalanche P-Chain validators (the native staking layer) — not to external lending/CEX/RWA venues. Validator set governed via Node Voting; the only "venue" is Avalanche staking itself (Tier-1 chain). | 9 | 9 | Non-Improvable (optimal) | [P1] docs: AVAX delegated to Avalanche validators only |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Fee structure disclosed: protocol earns ~10% of validator rewards (incl. a portion of delegator fees). Transparent, applied via the exchange rate; no hidden venue rebates. | 9 | 9 | Non-Improvable (optimal) | [P1] docs overview ("protocol earns 10% of the rewards generated by validators") |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Node Voting governs delegation distribution across validators with performance/infrastructure requirements (Open Pool) and randomized distribution (Miles Pool), bounding per-validator concentration. Limits are policy-based rather than hard on-chain per-validator caps published. | 3 | 9 | **Improvable** | [P1] docs delegation-pools (35/65, randomized distribution); no published hard per-validator cap |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Native unstake follows the 15-day cooldown + 48h claim (validator delegation exit), a documented and routinely executed path; instant exit available via AMM. No discretionary approval required for native redemption. | 9 | 9 | Non-Improvable (optimal) | [P1] docs unstaking (15-day cooldown, executed continuously); AMM instant exit |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Validators are Avalanche network validators selected via on-chain Node Voting (transparent). Custody is BENQI's own MPC system (disclosed in architecture docs). No undisclosed third-party asset manager. Deal Breaker does not trigger. | 9 | 9 | Non-Improvable (optimal) | [P1] docs node-voting + architecture (MPC custody disclosed) |

**Protocol Counterparty Subtotal:**
- Scores: 4 x 9 = 36, 1 x 3 = 3
- Raw: 36 + 3 = 39 out of max 45
- Adjusted: (39/45) x 45 = **39.0/45 (86.7%)**

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain redemption via `requestUnlock()` + `redeem()` after the 15-day cooldown. Pause is protocol-wide (role-restricted multisig), not address-selective; no blacklist function. Withdrawals cannot be selectively blocked per address. | 9 | 9 | Non-Improvable (optimal) | [P0] StakedAvax requestUnlock/redeem are permissionless; ROLE_PAUSE is global only |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Native redemption returns AVAX 1:1 from the staking pool within the 15-day window for effectively 100% of TVL (delegation exits processed by the protocol). Secondary AMM markets add absorption for faster partial exits. Credible path to near-total exit over the stated window. | 9 | 9 | Non-Improvable (optimal) | [P1] docs: native redemption settles staked AVAX over cooldown; on-chain pool backs 1:1 |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No reports of native sAVAX redemption failing the stated 15-day window or of protocol-imposed freezes. The cooldown is by design, not a delay/queue overrun. | 9 | 9 | Non-Improvable (optimal) | [P1] No documented redemption freeze; cooldown is the stated baseline |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Redemption is backed 1:1 by staked AVAX; there is no utilization-driven cap on native unstaking (unlike a lending pool). A totalPooledAvax cap can limit new deposits but not exits. No history of caps blocking exits. | 9 | 9 | Non-Improvable (optimal) | [P0] ROLE_SET_TOTAL_POOLED_AVAX_CAP affects deposits, not redemptions |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | sAVAX has multi-year history through the 2022-2023 deleveraging; native redemption remained functional (queue-based by design) and AMM exit remained available, though secondary discounts can widen in stress. No specific quantified stress-survival event with sustained-discount data documented -> Mid per the cautious "demonstrated history" standard. | 3 | 9 | **Source Missing** | [P4] sAVAX operated through 2022-23 stress; no quantified discount/withdrawal time-series published |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | Native exit IS the 15-day unstaking period (the stated withdrawal term), so it is matched by design; instant AMM exit available for those unwilling to wait. Not "longer than stated." | 9 | 9 | Non-Improvable (optimal) | [P1] docs: 15-day cooldown is the stated withdrawal term |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Most users can exit via in-protocol native redemption (1:1 at exchange rate). Secondary AMM markets are optional for instant exits and reasonably deep for a top-Avalanche asset, though thinner than ETH LSTs. | 9 | 9 | Non-Improvable (optimal) | [P1] in-protocol redemption primary; [P3] sAVAX AMM pools (Trader Joe/Pangolin/Curve) secondary |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | AVAX itself is deeply liquid (Tier-1). sAVAX secondary depth supports staggered exits but, at ~$161M TVL with modest DEX volume (~$214k/24h), deep instant exits beyond a few percent of TVL would face impact. Mid per depth supporting ~3-10% of TVL. | 3 | 3 | Non-Improvable | [P3] sAVAX ~$214k 24h trading volume; modest DEX depth vs TVL |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | A mass exit primarily produces a 15-day queue (rate spikes/discounts on AMM), not permanent haircuts, because redemptions are backed 1:1 by staked AVAX with no leverage. Long operating history without a bank-run failure, but no extreme-scale stress test documented. | 3 | 9 | **Improvable** | [P0] 1:1 backing, no leverage limits permanent-loss risk; [P4] no extreme bank-run test on record |

**Liquidity Subtotal:**
- Scores: 6 x 9 = 54, 3 x 3 = 9
- Raw: 54 + 9 = 63 out of max 81
- Adjusted: (63/81) x 45 = **35.0/45 (77.8%)**

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | sAVAX is value-accruing (tracks the exchange rate, not a 1:1 peg). Secondary price can dip to a discount during stress (known, documented risk), but no >10% sustained sAVAX-specific dislocation is documented. Lacking a quantified stress-survival peg dataset -> Mid (3), consistent with how comparable untested-peg LSTs (Etherfi eETH, Stader ETHx) are scored. | 3 | 9 | **Source Missing** | [P4] Exponential/IQ.wiki "sAVAX can trade at a discount" in stress; no quantified >10% event |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | sAVAX is a 1:1 AVAX claim with no protocol leverage; AVAX price moves affect USD value but not the AVAX-denominated claim. Low-beta to AVAX, no forced liquidation at protocol level. | 9 | 9 | Non-Improvable (optimal) | [P0] No leverage in StakedAvax; 1:1 AVAX backing |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yield derives from Avalanche protocol staking rewards, not an internal utilization curve, so there is no reflexive rate model that can break. A deposit cap exists but does not trap withdrawals. No history of yield cliffs. | 9 | 9 | Non-Improvable (optimal) | [P0] Rewards set by Avalanche protocol; no internal rate curve |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | No published sAVAX-specific stress-test / scenario modeling (e.g., mass unstake under 30-50% AVAX gaps). Chaos Labs provides risk monitoring for parameters but no public sAVAX stress-loss modeling is disclosed. | 3 | 9 | **Source Missing** | [P1] Chaos Labs dashboard exists; no published sAVAX stress-scenario results |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | No protocol-level leverage, borrowing, or liquidation mechanism in sAVAX. Sharp AVAX moves do not force liquidations within the BENQI staking system (external leveraged users bear their own risk). | 9 | 9 | Non-Improvable (optimal) | [P0] No liquidation/borrow logic in StakedAvax |

**Market Subtotal:**
- Scores: ST-M-01(3), ST-M-02(9), ST-M-03(9), ST-M-04(3), ST-M-05(9)
- Count: 3 x 9 = 27, 2 x 3 = 6
- Raw: 27 + 6 = 33 out of max 45
- Adjusted: (33/45) x 45 = **33.0/45 (73.3%)**

**Strategy Total: 45.0 + 30.0 + 37.5 + 39.0 + 35.0 + 33.0 = 219.5/270 (81.3%)**

Potential Strategy: 45.0 + 45.0 + 41.2 + 45.0 + 41.7 + 45.0 = **262.9/270 (97.4%)** (Source-Missing/Improvable Strategy items resolved; ST-IC-08, ST-L-08 remain Non-Improvable at 3)

### OPERATIONS (30% Weight) -- Score: 124.1/270 (45.9%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Core sAVAX contract upgrades are controlled by a team multisig (documented), not by binding on-chain tokenholder governance. QI/Miles governance covers validator Node Voting (delegation), not contract upgrades. Hybrid: multisig executes upgrades within undocumented bounds. | 3 | 9 | **Improvable** | [P2] Aave ARC multisig; [P1] node-voting governs delegation only, not upgrades |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- QI/Miles voting governs validator delegation (Node Voting), not protocol contract upgrades; there is no on-chain tokenholder vote over fund-custody logic. Multisig concentration is captured in S-KM-01/S-KM-03. | N/A | N/A | N/A | - |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | No on-chain timelock on sAVAX upgrades is documented or verifiable, and no veto/guardian mechanism is published. Major changes can be executed by the multisig without a disclosed delay. | 1 | 9 | **Improvable** | [P0] No timelock contract identified for sAVAX proxy admin; [P1] none documented |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A -- sAVAX is a liquid staking token, not a vault with a replaceable external strategy manager. | N/A | N/A | N/A | - |

**Governance Subtotal (2 scored questions, 2 N/A):**
- Scores: 1 x 3 = 3, 1 x 1 = 1
- Raw: 3 + 1 = 4 out of max 18
- Adjusted: (4/18) x 67.5 = **15.0/67.5 (22.2%)**

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Founders publicly identified (JD Gagnon, Hannu Kuusi, Alexander Szul) via Rome Blockchain Labs Inc. Long, credible track record as Avalanche's first major DeFi protocol (since 2021). No unresolved credibility red flags. | 9 | 9 | Non-Improvable (optimal) | [P4] NewsBTC/CB Insights team coverage; Rome Blockchain Labs |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | BENQI is an established multi-product protocol (Liquidity Markets, Liquid Staking, Ignite) with a dedicated engineering organization, not a single-developer project. Some key-person concentration typical of mid-size DeFi teams. | 9 | 9 | Non-Improvable (optimal) | [P4] Team/company coverage; multi-product engineering org |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Rome Blockchain Labs Inc is the named development/incubation entity (Canada-based founders). A dedicated foundation/operating entity for BENQI with mapped responsibilities is only partially clear in public disclosures. | 3 | 9 | **Improvable** | [P4] Rome Blockchain Labs named; precise BENQI operating entity/jurisdiction not fully mapped in docs |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known material regulatory enforcement actions, sanctions, or investigations against BENQI or Rome Blockchain Labs in major jurisdictions. | 9 | 9 | Non-Improvable (optimal) | [P4] No enforcement actions found in searches |
| O-TL-05 | Is there an on-call and incident response process for core teams? | BENQI has demonstrated operational continuity through chain outages and 4+ years of operation, and partners with Chaos Labs for monitoring, but no documented 24/7 on-call runbook with response SLAs is published. | 3 | 9 | **Source Missing** | [P1] Chaos Labs monitoring; no published on-call/incident SLA docs |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | BENQI maintains active support channels (Discord, docs, knowledge base) and integrator relationships (Aave, Pendle, Trader Joe). Responsive given long operating history, though no formal SLA published. | 9 | 9 | Non-Improvable (optimal) | [P1] docs + knowledge base; active integrations (Aave v3 sAVAX listing) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Strategic partners and ecosystem backers are disclosed (Ava Labs ecosystem; partner protocols named in the multisig expansion: Avalaunch, Pendle, Aave). Major-investor influence is reasonably transparent. | 9 | 9 | Non-Improvable (optimal) | [P2] Aave ARC names partner signers; ecosystem partnerships public |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | N/A -- sAVAX is not an externally-curated vault; BENQI operates its own protocol with no third-party manager running competing mandates. | N/A | N/A | N/A | - |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | N/A -- no external strategy manager; BENQI's own history shows no uncompensated sAVAX collateral-loss event. | N/A | N/A | N/A | - |

**Team & Legal Subtotal (7 scored questions, 2 N/A):**
- Scores: 5 x 9 = 45, 2 x 3 = 6
- Raw: 45 + 6 = 51 out of max 63
- Adjusted: (51/63) x 67.5 = **54.6/67.5 (81.0%)**

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Comprehensive public docs (docs.benqi.fi): Liquid Staking overview, architecture, getting-started, Risks & Audits, contracts, price-feeds, node-voting. Maintained and current (audit list updated through 2025). | 9 | 9 | Non-Improvable (optimal) | [P1] docs.benqi.fi (architecture, risks, contracts pages all current) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Docs explain staking flow (submit -> delegate to P-Chain -> rewards accrue -> unstake) and include a risk/audit section, but loss scenarios are described at a high level rather than via systematic scenario mapping. | 3 | 9 | **Improvable** | [P1] docs architecture + risks; general risk warning, limited scenario mapping |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Docs list the sAVAX token, veQI, QI, price-feed and market addresses across `resources/contracts/*` pages, but the proxy ADMIN, implementation, timelock and multisig addresses are NOT included in the canonical registry. | 3 | 9 | **Improvable** | [P1] docs contracts pages list token/oracle addresses; admin/impl/multisig absent |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | AccessControl roles exist on-chain (verified source) but are not explained in docs, and there is no published role-holder registry or role-change history (Grant/Revoke Role events are on-chain but undocumented). | 1 | 9 | **Improvable** | [P0] Roles in verified StakedAvax; [P1] no docs registry of role holders/changes |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Reserves are on-chain verifiable (totalPooledAvax / staked AVAX vs sAVAX supply), but no formal published proof-of-reserves methodology/dashboard exists. Proof-of-liabilities is largely N/A (no rehypothecation/borrow against user assets). | 3 | 9 | **Improvable** | [P0] totalPooledAvax/totalShares readable on-chain; [P1] no published PoR methodology |
| O-DT-06 | Are all contracts verified on the leading block explorers? | sAVAX proxy (verified, partial match) and implementation (verified, Exact Match) are both verified on Snowtrace; oracle and token contracts verified. Core fund-custody/oracle contracts verified. | 9 | 9 | Non-Improvable (optimal) | [P0] Snowtrace: proxy verified, implementation 0xB791C7A4... Exact Match |

**Documentation Subtotal:**
- Scores: 2 x 9 = 18, 3 x 3 = 9, 1 x 1 = 1
- Raw: 18 + 9 + 1 = 28 out of max 54
- Adjusted: (28/54) x 67.5 = **35.0/67.5 (51.9%)**

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | No dedicated, ring-fenced safety module with binding activation rules for sAVAX losses. The DAO QI treasury could in principle cover losses but only discretionarily. Avalanche delegation's no-principal-slashing reduces the need, but no formal backstop exists. | 3 | 9 | **Improvable** | [P3] DeFiLlama treasury (QI only); no documented safety module |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | DeFiLlama-tracked treasury ~$2.96M (~1.8% of ~$161.67M TVL) but composed 100% of the protocol's own QI token — illiquid and highly volatile, down from a ~$85M April-2024 peak. Per criteria, native-token-dominated reserves score High regardless of ratio band. | 1 | 3 | Non-Improvable | [P3] api.llama.fi/treasury/benqi (~$2.96M, 100% QI); TVL ~$161.67M |
| O-FR-03 | What is the estimated operational runway at current burn? | BENQI earns ~$1.66M annualized protocol revenue (DeFiLlama) from sAVAX fees plus lending-market revenue, supporting ongoing operations, but disclosed cost/runway figures are not published. Runway likely >12 months from recurring revenue but not clearly evidenced. | 3 | 9 | **Source Missing** | [P3] DeFiLlama annualized revenue ~$1.66M; no published cost/runway disclosure |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | sAVAX survived the 2022-2023 market collapse and multiple Avalanche outages with no depositor haircuts and continued reward accrual. TVL has declined (largely AVAX USD-price-driven), and sAVAX is composed across Avalanche DeFi (Aave v3, Pendle), but no contagion-driven bad debt event has materialized. Recoverable stress behavior. | 3 | 9 | **Improvable** | [P4] operated through 2022-23 stress with no haircut; [P3] TVL declined with AVAX price; no contagion event |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | sAVAX redemption (requestUnlock/redeem) is permissionless on-chain, but completing native unstaking depends on the off-chain MPC delegation system to return AVAX from the P-Chain; loss of operators could impair native redemptions, though AMM exit remains. Mixed: on-chain exit exists but off-chain dependency for native settlement. | 3 | 3 | Non-Improvable | [P0] permissionless redeem(); [P1] native settlement depends on MPC/P-Chain operations |

**Financial Resilience Subtotal:**
- Scores: 4 x 3 = 12, 1 x 1 = 1
- Raw: 12 + 1 = 13 out of max 45
- Adjusted: (13/45) x 67.5 = **19.5/67.5 (28.9%)**

**Operations Total: 15.0 + 54.6 + 35.0 + 19.5 = 124.1/270 (45.9%)**

Potential Operations: Governance 67.5 + Team & Legal 67.5 + Documentation 67.5 + Financial Resilience 49.5 (O-FR-02 capped at 3, O-FR-05 capped at 3 -> 3 x 9 + 2 x 3 = 33/45 x 67.5) = **252.0/270 (93.3%)**

---

## Final Score Calculation

| Category | Subcategory | Questions | Scored | N/A | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|--------|-----|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security | 11 | 11 | 0 | 69 | 99 | 125.5 | 180 | 69.7% |
| | Key Management | 8 | 7 | 1 | 31 | 63 | 88.6 | 180 | 49.2% |
| | **Security Subtotal** | **19** | **18** | **1** | | | **214.1** | **360** | **59.5%** |
| **Strategy** | Protocol Mechanics | 9 | 7 | 2 | 63 | 63 | 45.0 | 45 | 100% |
| | Collateral | 4 | 4 | 0 | 24 | 36 | 30.0 | 45 | 66.7% |
| | Infra Counterparty | 8 | 8 | 0 | 60 | 72 | 37.5 | 45 | 83.3% |
| | Protocol Counterparty | 5 | 5 | 0 | 39 | 45 | 39.0 | 45 | 86.7% |
| | Liquidity | 9 | 9 | 0 | 63 | 81 | 35.0 | 45 | 77.8% |
| | Market | 5 | 5 | 0 | 33 | 45 | 33.0 | 45 | 73.3% |
| | **Strategy Subtotal** | **40** | **38** | **2** | | | **219.5** | **270** | **81.3%** |
| **Operations** | Governance | 4 | 2 | 2 | 4 | 18 | 15.0 | 67.5 | 22.2% |
| | Team & Legal | 9 | 7 | 2 | 51 | 63 | 54.6 | 67.5 | 81.0% |
| | Documentation | 6 | 6 | 0 | 28 | 54 | 35.0 | 67.5 | 51.9% |
| | Financial Resilience | 5 | 5 | 0 | 13 | 45 | 19.5 | 67.5 | 28.9% |
| | **Operations Subtotal** | **24** | **20** | **4** | | | **124.1** | **270** | **45.9%** |
| **TOTAL** | | **83** | **76** | **7** | | | **557.7** | **900** | **62.0%** |

### Potential Score Calculation

| Category | Subcategory | Potential Raw | Max Raw | Potential Adj | Max Points |
|----------|-------------|---------------|---------|---------------|------------|
| **Security** | Smart Contract Security | 99 | 99 | 180.0 | 180 |
| | Key Management (KM-05 capped at 3) | 57 | 63 | 162.9 | 180 |
| | **Security Subtotal** | | | **342.9** | **360** |
| **Strategy** | Protocol Mechanics | 63 | 63 | 45.0 | 45 |
| | Collateral | 36 | 36 | 45.0 | 45 |
| | Infra Counterparty (IC-08 capped at 3) | 66 | 72 | 41.2 | 45 |
| | Protocol Counterparty | 45 | 45 | 45.0 | 45 |
| | Liquidity (L-08 capped at 3) | 75 | 81 | 41.7 | 45 |
| | Market | 45 | 45 | 45.0 | 45 |
| | **Strategy Subtotal** | | | **262.9** | **270** |
| **Operations** | Governance | 18 | 18 | 67.5 | 67.5 |
| | Team & Legal | 63 | 63 | 67.5 | 67.5 |
| | Documentation | 54 | 54 | 67.5 | 67.5 |
| | Financial Resilience (FR-02=3, FR-05=3) | 33 | 45 | 49.5 | 67.5 |
| | **Operations Subtotal** | | | **252.0** | **270** |
| **POTENTIAL TOTAL** | | | | **857.8** | **900** |

> Potential note: Security potential 342.9 + Strategy 262.9 + Operations 252.0 = **857.8/900**, which falls in the A- range (846-858). Authoritative potential grade: **A- (857.8/900)**.

---

