# Sky Protocol - sUSDS (Savings USDS) Risk Rating

**Rating Date**: 2026-02-12
**Final Grade**: BB+
**Total Score**: 806.8/900 points

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 318.2/360 (88.4%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. The sUSDS contract follows the same ERC-4626 pattern as the extensively audited sDAI (SavingsDai) contract. The MakerDAO/Sky system has been audited by multiple Tier-0/1 firms over 8+ years: ChainSecurity (Tier-0) audited the DSR and sDAI contracts, Trail of Bits (Tier-0) conducted comprehensive MakerDAO audits, ABDK performed formal verification, Quantstamp audited core contracts, and PeckShield provided additional reviews. The USDS/sUSDS contracts, being part of the Sky rebrand, were audited by ChainSecurity and Cantina prior to the September 2024 launch. Multiple independent audits (>=2) confirmed. | 9 | 9 | Non-Improvable (optimal) | [P1] ChainSecurity audit of Sky/USDS rebrand contracts (2024), [P1] Trail of Bits MakerDAO core audits, [P1] ABDK formal verification, [P1] Historical audit portfolio at security.makerdao.com |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | ChainSecurity (Tier-0) audited the Sky rebrand contracts including sUSDS prior to September 2024 launch. Cantina (Tier-1) also conducted reviews. The most recent audits involve Tier-0 auditors. | 9 | 9 | Non-Improvable (optimal) | [P1] ChainSecurity Sky/USDS audit report, [P1] Cantina review |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | The sUSDS contract is non-upgradeable (pure ERC-4626 vault with no proxy pattern). The savings rate parameter (SSR/DSR) is adjusted via governance through the Pot/SSR contract, which has been part of the audited core MakerDAO system since 2019. No upgrades to the savings contract itself in the last 12 months requiring re-audit. The September 2024 rebrand deployment was audited prior to launch. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS contract is non-upgradeable, [P1] Sky rebrand audited before deployment |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. The MakerDAO/Sky system has an 8+ year track record of systematic audit finding remediation. Critical findings from Trail of Bits and ChainSecurity audits have been resolved and re-verified through subsequent audit engagements. The iterative multi-firm audit approach across 8 years provides strong confidence in remediation. No outstanding critical/high findings known. | 9 | 9 | Non-Improvable (optimal) | [P1] Multi-year audit portfolio with remediation, [P1] No outstanding critical findings in public reports |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | The sUSDS contract itself is non-upgradeable (immutable ERC-4626 vault). The underlying Pot/SSR module (which sets the savings rate) can only be modified via governance executive votes that pass through the 48-hour GSM timelock. This is among the most constrained upgrade mechanisms in DeFi -- all parameter changes require: (1) MKR holder vote reaching quorum, (2) 48-hour mandatory delay in GSM, (3) public on-chain visibility during the entire process. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS is immutable ERC-4626, [P0] GSM 48h timelock at 0x9eF05f7F6deB616fd37aC3c959a2dDD25A108B90, [P1] MakerDAO governance documentation |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit affecting the DSR/SSR savings mechanism (sDAI/sUSDS) in the protocol's entire 8+ year history. The March 2020 "Black Thursday" event resulted in $8.3M in undercollateralized vault liquidations due to auction system failures during extreme network congestion, but this affected the CDP/vault borrowing system, NOT the savings rate mechanism. The savings rate mechanism (Pot/DSR/SSR) has operated flawlessly since its introduction in November 2019. Black Thursday occurred over 5 years ago and led to comprehensive remediation: liquidation system rewrite (Liquidations 2.0), circuit breakers, and auction improvements. Per the timeframe guidance, events older than 24 months may be mitigated if all three conditions are met (root cause remediated, code rewritten, no recurrence) -- all three conditions are met. | 9 | 9 | Non-Improvable (optimal) | [P0] No savings rate exploits in on-chain history, [P1] Black Thursday post-mortem (forum.makerdao.com), [P1] Liquidations 2.0 rewrite fully deployed |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. MakerDAO/Sky has operated transparently since 2017 with publicly identified founders (Rune Christensen), open governance, and extensive institutional participation. The protocol is backed by major venture firms (a16z, Paradigm, Dragonfly) and has been a cornerstone of DeFi infrastructure. No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] Public founder (Rune Christensen), [P2] Active governance since 2017, [P4] No credible allegations in 8+ years |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. The GSM timelock has been at 48 hours for an extended period and represents one of the longest governance timelocks in DeFi. The timelock was actually increased from 24h to 48h historically, strengthening protections. No changes weakening governance protections in the last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P0] GSM timelock remains at 48h, [P1] No governance proposals to reduce timelock |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. MakerDAO/Sky has maintained a bug bounty program on Immunefi (immunefi.com/bug-bounty/makerdao/) with maximum payout up to $10M for critical smart contract vulnerabilities. This is one of the largest bug bounty programs in DeFi, well exceeding the $100K threshold. Immunefi is an established platform with track record of payouts. | 9 | 9 | Non-Improvable (optimal) | [P1] Immunefi MakerDAO bounty page: up to $10M payout, [P1] Active program covering all core contracts |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | No specific third-party monitoring provider (Hypernative, Blockaid, or equivalent) has been publicly disclosed for Sky Protocol's savings rate mechanism. The protocol operates keepers and monitoring bots for the broader system (oracle prices, liquidations, PSM operations), but formal 24/7 monitoring with invariant coverage and on-call response for the sUSDS mechanism specifically is not publicly documented. The protocol's design simplicity (pure savings rate accrual) reduces the attack surface, but monitoring documentation is lacking. | 3 | 9 | Source Missing | [P1] No monitoring provider named in official docs, [P1] Keeper network operates for broader protocol but sUSDS-specific monitoring undocumented |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | The broader MakerDAO/Sky system has multiple safety controls: the GSM timelock acts as a de facto circuit breaker on governance changes, the Emergency Shutdown Module (ESM) allows MKR holders to trigger a global protocol shutdown if 75,000 MKR is deposited (protecting against governance attacks), and individual vault types can be frozen via governance. The sUSDS contract itself has no pause function (immutable), but the underlying SSR rate can be set to 0 via governance through the GSM. The ESM provides the ultimate circuit breaker. These are manual triggers (governance-based) with clearly documented procedures, but governance could adopt automated objective triggers (e.g., Hypernative integration) to enhance protection. | 3 | 9 | Improvable | [P0] Emergency Shutdown Module (ESM) at known address, [P0] GSM provides governance delay, [P1] MakerDAO Emergency Shutdown documentation |

**Smart Contract Security Subtotal: 158.2/180 (87.9%)**
- 9 questions scored 9 (sum = 81), 2 questions scored 3 (sum = 6)
- Raw sum = 87 out of max 99
- Weighted = (87/99) x 180 = 158.2

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | The sUSDS contract is non-upgradeable. The savings rate parameter (SSR) is controlled exclusively by Sky governance through MKR token holder executive votes. All changes must pass through the 48-hour GSM timelock. There are no admin keys in the traditional sense -- only governance has the ability to modify protocol parameters. The governance process is transparent, on-chain, and publicly documented. Any changes in the last 12 months (SSR rate adjustments) were publicly documented through governance votes visible on vote.makerdao.com. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS is immutable -- no admin keys for the contract itself, [P0] SSR parameter controlled via governance Pot/Jug module, [P2] vote.makerdao.com shows all executive votes |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No single key can move user funds or upgrade the sUSDS contract (it is immutable). The only way to modify the savings rate is through MKR governance vote + 48h GSM timelock. Moving funds from the DSR/SSR requires the user themselves to call withdraw/redeem. No admin, multisig, or single entity can access user deposits. The governance process requires broad MKR holder participation to reach quorum, well above the 3-of-5 threshold. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS contract: permissionless withdraw/redeem, [P0] No admin withdrawal function exists, [P1] GSM 48h timelock on all governance actions |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Sky does not use a traditional multisig for critical actions. Instead, all critical actions require MKR token holder governance votes with quorum requirements, followed by the 48-hour GSM timelock. This is MORE decentralized than any multisig -- it requires broad token holder participation. The MKR token has thousands of holders across hundreds of delegates. The governance facilitators (GovAlpha) coordinate but cannot execute unilateral changes. While MKR voting power concentration exists (see O-G-02), the governance mechanism itself is highly robust. Per the criteria, governance with diverse token holders exceeds 3-of-5 threshold. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain governance via MKR voting, [P2] vote.makerdao.com, [P1] Delegate system with 20+ active delegates |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | The sUSDS contract has no pause function and no address-level blocking capability. Withdrawals are fully permissionless via ERC-4626 standard (redeem/withdraw). No admin can block individual addresses from withdrawing. The only system-level control is the Emergency Shutdown Module (ESM), which is a protocol-wide emergency mechanism requiring 75,000 MKR to activate -- designed as a last-resort defense against governance attacks, not for routine operations. No address-level arbitrary withdrawal censorship exists. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS contract: no pause function, permissionless redeem/withdraw, [P0] ESM requires 75,000 MKR to activate, [P1] Emergency Shutdown documentation |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of sUSDS deposits are held in non-custodial on-chain smart contracts. When users deposit USDS into the sUSDS contract, the underlying USDS is held in the DSR/SSR module (Pot contract) within the MakerDAO/Sky core system. All fund custody is fully on-chain. The protocol's RWA (Real World Assets) backing involves off-chain assets, but these back the overall DAI/USDS supply at the system level, not individual sUSDS deposits. sUSDS depositors interact purely with on-chain contracts. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS contract holds USDS on-chain, [P0] Pot/SSR module is non-custodial smart contract, [P1] Architecture documentation |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. sUSDS deposits flow into the Pot/SSR module, which is separate from the protocol's Surplus Buffer (treasury) and operational wallets. The Surplus Buffer accumulates protocol revenue and is governed separately from user deposits. MakerDAO/Sky has always maintained clear separation between user funds (DAI/USDS in DSR/SSR, vault collateral) and protocol treasury (Surplus Buffer). | 9 | 9 | Non-Improvable (optimal) | [P0] Pot/SSR module holds DSR/SSR deposits, [P0] Surplus Buffer (vow contract) is separate, [P1] MakerDAO architecture documentation |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- sUSDS is a pure savings vault that earns the Sky Savings Rate (SSR) set by governance. It does not deploy user funds into external protocols. User USDS sits in the DSR/SSR module within the MakerDAO/Sky core system. There is no external protocol routing or whitelist mechanism needed. The yield comes from the protocol's systemic revenue, not from deploying user funds externally. | N/A | N/A | N/A | Not applicable -- pure savings rate product with no external deployment |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | The protocol has the Emergency Shutdown Module (ESM) as the ultimate incident response mechanism, and the broader MakerDAO system has demonstrated crisis response capability during Black Thursday (March 2020), coordinating governance response within days. However, no formal publicly documented incident playbook for governance key compromise or signer loss exists. The 48h GSM timelock provides time to respond to malicious governance attacks, and the ESM provides the nuclear option, but a structured playbook with tabletop exercises is not publicly available. | 3 | 9 | Source Missing | [P0] ESM exists as emergency mechanism, [P1] Black Thursday response demonstrated crisis capability, but no formal playbook documented |

**Key Management Subtotal: 160.0/180 (88.9%)**
- 6 scored questions (S-KM-07 = N/A): 5 scored 9 (sum = 45), 1 scored 3
- Raw sum = 48 out of max 54
- Weighted = (48/54) x 180 = 160.0

**Improvement Opportunities:**
- **S-KM-08** (+13.3 weighted points): Publish comprehensive incident response playbook covering governance key scenarios; conduct tabletop exercise

---

### **Security Total: 318.2/360 (88.4%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 158.2 | 180 | 87.9% |
| Key Management | 160.0 | 180 | 88.9% |
| **Security Total** | **318.2** | **360** | **88.4%** |

---

### STRATEGY (30% Weight) -- Score: 258.0/270 (95.6%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | The Sky Savings Rate (SSR) is funded by the protocol's systemic revenue which comes from three organic sources: (1) Stability fees from overcollateralized crypto vaults/CDPs (borrowers pay interest on DAI/USDS minted against crypto collateral), (2) Revenue from RWA investments (US Treasuries and other yield-bearing instruments held through partners like BlockTower, Monetalis, Centrifuge, estimated to generate ~60-70% of protocol revenue), (3) PSM operations and liquidation proceeds. All sources are organic and mandate-aligned for a "savings vault" product. The yield is set by governance as a fixed rate (SSR) that can be adjusted via executive vote. 100% organic yield with no token emission dependency. | 9 | 9 | Non-Improvable (optimal) | [P1] Sky/MakerDAO documentation: SSR funded by protocol revenue, [P2] Governance votes set SSR rate, [P3] DeFiLlama: ~4-8% APY historically organic |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Principal loss for sUSDS depositors is limited to extreme tail scenarios: (1) Systemic protocol insolvency where the entire MakerDAO/Sky system becomes undercollateralized across all vault types simultaneously (would require massive, simultaneous collateral value collapse beyond liquidation capacity), (2) Governance attack where malicious MKR holders drain the system (mitigated by ESM and 48h timelock), (3) Smart contract exploit in the core DSR/SSR module (8+ years without incident). The SSR never produces negative yield -- it can be set to 0% but cannot go negative. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS contract: rate is always >= 0, [P1] SSR/DSR mechanism design, [P1] ESM protects against governance attacks |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage or rehypothecation. sUSDS is a pure savings product. Users deposit USDS and earn the SSR rate. No leverage is applied to user deposits. The yield comes from the protocol's systemic revenue, not from leveraged strategies. Effective leverage = 1.0x. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS contract: simple deposit/redeem with no leverage mechanics, [P1] SSR mechanism design |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- sUSDS is a savings vault with no borrowing or liquidation risk for depositors. | N/A | N/A | N/A | Not applicable to pure savings vault |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss events for the DSR/sDAI/SSR/sUSDS savings mechanism in its entire history since November 2019 (when DSR was introduced). The DSR/SSR has always produced positive or zero yield. The mechanism has operated continuously through every major crypto crisis: Black Thursday (March 2020), Terra/Luna (May 2022), FTX (November 2022), USDC depeg (March 2023). sDAI was the direct predecessor and represents a comparable variant using the same underlying mechanism. 6+ year clean track record. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain history shows continuous positive or zero DSR/SSR since Nov 2019, [P1] No loss events documented in 6+ years |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | N/A -- sUSDS is not a curated vault. It is a protocol-level savings product where the rate is set by governance. | N/A | N/A | N/A | Not applicable -- protocol-level savings product, not curated vault |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. The SSR yield (historically ~4-8% for USDS) is entirely funded by organic protocol revenue from crypto vault stability fees and RWA yield (primarily US Treasuries). No token emissions or incentive dependency. The protocol generates hundreds of millions in annual revenue. The SSR rate is set by governance to be sustainable within the protocol's revenue capacity. | 9 | 9 | Non-Improvable (optimal) | [P2] Governance adjusts SSR based on protocol revenue, [P3] DeFiLlama: organic yield, [P1] MakerDAO annual revenue |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes. sUSDS redemption is instant via ERC-4626 withdraw/redeem. Users receive USDS which can be converted 1:1 to DAI via the PSM with no slippage. No lockup, no cooldown, no queue. Under conservative assumptions, the strategy can unwind 100% of position immediately with negligible slippage. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS: instant withdraw/redeem, [P0] PSM provides 1:1 USDS/DAI conversion |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. The SSR is a governance-set rate that is always >= 0. It does not depend on any market spread, peg maintenance, or funding rate. The yield is funded by protocol revenue, not by market-based spreads. There is no carry trade, basis trade, or funding rate dependency. | 9 | 9 | Non-Improvable (optimal) | [P0] SSR contract: rate >= 0 by design, [P1] Yield funded by protocol revenue |

**Protocol Mechanics Subtotal: 45.0/45 (100.0%)**
- 7 applicable questions (ST-PM-04, ST-PM-06 = N/A), all scored 9
- Raw sum = 63 out of max 63
- Weighted = (63/63) x 45 = 45.0

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | sUSDS accepts only USDS (Sky's stablecoin, formerly DAI). USDS is a top-tier stablecoin with $5B+ supply, backed by overcollateralized crypto assets (ETH, WBTC, stETH) and RWAs (US Treasuries). USDS/DAI has maintained its peg since 2017 with only brief deviations. USDS/DAI is among the highest-quality stablecoin collateral, with a longer operating history than any other decentralized stablecoin. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS accepts only USDS, [P3] USDS/DAI: $5B+ supply, 8+ year peg history |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | Evaluation target: sUSDS receipt token vs USDS NAV. The DSR/sDAI mechanism (comparable variant, same underlying mechanism) has operated since November 2019 and has maintained NAV perfectly through every stress event: Black Thursday (March 2020), Terra/Luna (May 2022), FTX (November 2022), USDC depeg (March 2023). The share price monotonically increases by design. sUSDS itself has operated since September 2024 (~17 months) without any NAV deviation. Combined with sDAI predecessor, this provides 6+ years of battle-tested operation. | 9 | 9 | Non-Improvable (optimal) | [P0] sDAI/sUSDS: monotonically increasing share price by design, [P0] No NAV deviation in combined 6-year on-chain history |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- sUSDS is a USDS savings vault with no staking-based collateral. | N/A | N/A | N/A | Not applicable |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | Minimal. USDS on Ethereum is natively issued by the Sky Protocol. Per the framework definition, natively issued stablecoins are excluded from the bridged/wrapped category. No bridged tokens in the deposit flow. | 9 | 9 | Non-Improvable (optimal) | [P0] USDS is natively issued on Ethereum, [P1] Framework definition excludes natively issued stablecoins |

**Collateral Subtotal: 45.0/45 (100.0%)**
- 3 applicable questions (ST-C-03 = N/A), all scored 9
- Raw sum = 27 out of max 27
- Weighted = (27/27) x 45 = 45.0

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Primary chain: Ethereum (Tier-0). No bridge dependency. No oracle dependency for the savings rate mechanism -- the SSR is set by governance as a fixed parameter. No CEX dependency. All critical dependencies are Tier-0. | 9 | 9 | Non-Improvable (optimal) | [P0] All contracts on Ethereum (Tier-0), [P0] SSR is governance-set, no oracle |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | The sUSDS savings rate mechanism has zero dependency on oracles or bridges. The SSR is a governance-set parameter. Qualifies for "No dependency on off-chain infra" = Low (9). | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS: no oracle or bridge dependency |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | The sUSDS mechanism operates fully on-chain with no critical off-chain providers. Per applicability check: "no critical off-chain providers" = Low (9). | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS operates fully on-chain |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | The DSR/SSR mechanism has operated through every major Ethereum event since November 2019 without disruption. Deployed well over 6 months with no incidents. | 9 | 9 | Non-Improvable (optimal) | [P0] Continuous operation since Nov 2019 through all Ethereum events |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain halts or consensus failures above 30 minutes in the last 12+ months. Tier-0 chain. | 9 | 9 | Non-Improvable (optimal) | [P0] Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- no staking-based collateral or validator dependency. | N/A | N/A | N/A | Not applicable |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- no staking-based collateral or direct validator dependency. | N/A | N/A | N/A | Not applicable |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Users have permissionless on-chain withdrawal via ERC-4626 standard. No dependency on any off-chain component for withdrawals. The only scenario where withdrawals would be affected is Ethereum chain halt or Emergency Shutdown activation -- both extreme tail events. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS: permissionless redeem/withdraw, no off-chain dependency |

**Infrastructure Counterparty Subtotal: 45.0/45 (100.0%)**
- 6 applicable questions (ST-IC-06, ST-IC-07 = N/A), all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 45 = 45.0

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | sUSDS does not deploy user funds into external protocols. The deposited USDS sits in the DSR/SSR module. However, at the system level, the protocol's revenue (which funds the SSR) comes partly from RWA investments. RWA counterparties include: BlockTower Andromeda (US Treasuries), Monetalis Clydesdale (US Treasuries via Sygnum), Centrifuge (structured credit). These are disclosed through governance and represent system-level exposure, not direct deployment of sUSDS deposits. Scoring Mid (3) due to the indirect but material dependency on untiered RWA counterparties for yield generation. | 3 | 3 | Non-Improvable | [P2] Governance proposals disclose all RWA counterparties, [P0] sUSDS deposits remain in Pot/SSR module |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | The SSR is set by MKR governance. There is no curator fee, no revenue-share arrangement with external parties. Protocol revenue flows to the Surplus Buffer, and governance decides how much to allocate to the SSR. Transparent and documented. No conflicts. | 9 | 9 | Non-Improvable (optimal) | [P2] Governance votes set SSR rate, [P0] Surplus Buffer transparent on-chain |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | At the system level, MakerDAO/Sky governance sets debt ceilings per vault type and RWA allocation limits, enforced on-chain through the DC-IAM. Each RWA arrangement has a specific approved allocation cap. Changes require governance votes. For sUSDS specifically, there are no per-counterparty caps because sUSDS does not directly interact with counterparties. System-level caps are governance-enforced. | 9 | 9 | Non-Improvable (optimal) | [P0] DC-IAM enforces per-vault debt ceilings on-chain, [P2] Governance defines RWA allocation limits |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | sUSDS deposits can be withdrawn instantly. At the system level, crypto vault collateral can be liquidated rapidly. RWA positions (US Treasuries) are highly liquid. The PSM provides instant conversion. No discretionary approvals needed. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS: instant withdrawal, [P0] PSM provides instant conversion |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | For sUSDS specifically, there are no third-party validators, custody providers, or asset managers -- it is a pure on-chain savings product. At the system level, RWA counterparties are fully disclosed through governance. Per applicability check: sUSDS itself does not use third-party service providers = Low (9). | 9 | 9 | Non-Improvable (optimal) | [P2] All RWA counterparties disclosed via governance, [P0] sUSDS requires no third-party providers |

**Protocol Counterparty Subtotal: 39.0/45 (86.7%)**
- 4 questions scored 9 (sum = 36), 1 question scored 3
- Raw sum = 39 out of max 45
- Weighted = (39/45) x 45 = 39.0

---

#### Liquidity (5% weight, 45 max points)

**Withdrawal period baseline:** Instant -- sUSDS is an ERC-4626 vault with no lockup, cooldown, or queue.

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | All users have permissionless on-chain redemption via ERC-4626 standard. No pause function on the sUSDS contract. No address-level blocking capability. No admin approval required. The only theoretical disruption is Emergency Shutdown. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS contract: permissionless redeem/withdraw, no pause function |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Yes. sUSDS withdrawals are instant and draw from the Pot/SSR module which holds all deposited USDS. Near-100% of TVL can be withdrawn at any time. Additionally, USDS can be swapped 1:1 for DAI via the PSM, and the combined DAI/USDS liquidity is among the deepest in DeFi. | 9 | 9 | Non-Improvable (optimal) | [P0] All deposits in Pot/SSR module, fully withdrawable, [P0] PSM provides 1:1 conversion |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No withdrawal delays, queues, or freezes for the DSR/sDAI/sUSDS mechanism in its 6+ year history. The mechanism has operated continuously through every major crisis. During Black Thursday (March 2020), the DSR continued functioning normally with uninterrupted withdrawals. | 9 | 9 | Non-Improvable (optimal) | [P0] No delays in 6+ year on-chain history |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | No caps on withdrawals. No utilization-based restrictions. The entire deposited amount is always available. No history of caps blocking exits. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS: no withdrawal cap, no utilization-based restriction |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | The DSR/sDAI mechanism has been battle-tested through severe volatility and congestion: Black Thursday (March 2020) saw extreme Ethereum congestion, yet DSR withdrawals continued. Throughout every major market crash since 2019, the savings rate mechanism maintained withdrawal functionality. This represents proven resilience under real stress. | 9 | 9 | Non-Improvable (optimal) | [P0] Continuous withdrawal functionality during Black Thursday and all major crashes |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Withdrawals are instant. No lockup, no cooldown, no unstaking period. 0% of assets have any duration longer than the instant withdrawal term. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS: instant withdraw/redeem, no lockup |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary redemption through the ERC-4626 vault is always available. No secondary market dependency. USDS/DAI have deep secondary market liquidity if users choose that route. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS: ERC-4626 standard redemption |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | USDS/DAI is one of the most liquid stablecoins with $5B+ combined supply. The PSM provides essentially unlimited 1:1 conversion to USDC. Liquidity depth can absorb well over 10% of sUSDS TVL with negligible impact. | 9 | 9 | Non-Improvable (optimal) | [P3] DAI/USDS: $5B+ supply, [P0] PSM provides 1:1 conversion |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | The DSR/sDAI mechanism has been tested through multiple de facto bank-run scenarios. During the USDC depeg in March 2023, significant DSR withdrawals occurred -- the system processed all without delays or losses. By design, there is no "utilization" -- all deposits are always fully available. A mass exit reduces DSR TVL but does not cause queues, haircuts, or permanent losses. | 9 | 9 | Non-Improvable (optimal) | [P0] All deposits always fully available, [P1] Demonstrated through USDC depeg March 2023 mass withdrawals |

**Liquidity Subtotal: 45.0/45 (100.0%)**
- 9 questions, all scored 9
- Raw sum = 81 out of max 81
- Weighted = (81/81) x 45 = 45.0

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | Evaluation target: sUSDS receipt token. sUSDS is an accumulating ERC-4626 token whose share price monotonically increases by design (SSR >= 0). The predecessor sDAI operated from June 2023 to September 2024 and maintained perfect NAV. sUSDS has operated since September 2024 (~17 months) with no NAV deviation. Combined sDAI + sUSDS track record spans nearly 3 years. During the March 2023 USDC depeg, while DAI briefly deviated from $1, the DSR mechanism continued to function correctly and sDAI share price was never impacted. This represents battle-tested performance. | 9 | 9 | Non-Improvable (optimal) | [P0] sDAI/sUSDS: monotonically increasing share price by design, [P0] No NAV deviation in combined 3-year history |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Very low. sUSDS is USDS-denominated with no directional crypto exposure. Sharp crypto market movements do not affect sUSDS share price. No leverage, no directional exposure. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS: USDS-denominated, no directional exposure |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | The SSR is a governance-set fixed rate, not an algorithmic or utilization-dependent rate. It does not spike, compress, or become reflexive. Governance adjusts periodically based on protocol revenue capacity. No utilization-based model. | 9 | 9 | Non-Improvable (optimal) | [P0] SSR is governance-set fixed rate |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | The MakerDAO/Sky system has survived every major crypto crash since 2017. However, explicit published stress test results specifically for the sUSDS/SSR mechanism under high-volatility scenarios are not publicly available. The protocol's real-world track record through actual crises is the strongest possible "stress test" -- but formal published scenario analysis specifically for the savings rate is lacking. | 3 | 9 | Improvable | [P1] Real-world stress survival over 6+ years, but no published formal stress test for SSR/sUSDS specifically |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | No. sUSDS has no leverage and no liquidation mechanics for depositors. Sharp crypto price moves do not trigger any liquidation for sUSDS holders. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS: no leverage, no liquidation mechanics |

**Market Subtotal: 39.0/45 (86.7%)**
- 4 questions scored 9 (sum = 36), 1 question scored 3
- Raw sum = 39 out of max 45
- Weighted = (39/45) x 45 = 39.0

---

### **Strategy Total: 258.0/270 (95.6%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 45.0 | 45 | 100.0% |
| Collateral | 45.0 | 45 | 100.0% |
| Infra Counterparty | 45.0 | 45 | 100.0% |
| Protocol Counterparty | 39.0 | 45 | 86.7% |
| Liquidity | 45.0 | 45 | 100.0% |
| Market | 39.0 | 45 | 86.7% |
| **Strategy Total** | **258.0** | **270** | **95.6%** |

---

### OPERATIONS (30% Weight) -- Score: 230.6/270 (85.4%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | All changes controlled by on-chain MKR token holder governance with clearly defined rules. Executive votes require MKR holders to deposit MKR to vote on spells. Approved spells pass through the 48-hour GSM timelock. No single entity can unilaterally change core logic. Operating since 2017. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain governance via MKR voting, [P0] GSM 48h timelock, [P2] vote.makerdao.com |
| O-G-02 | How concentrated is voting power among top holders or delegates? | MKR governance has known concentration concerns. Large holders (a16z, early investors) can significantly influence outcomes. The delegate system introduced in 2022 has improved participation. The 48h GSM timelock and ESM provide structural checks. Top 10 addresses likely control 33-66% of active voting power. | 3 | 3 | Non-Improvable | [P2] vote.makerdao.com voting records, [P1] Known concentration concerns |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. Robust mechanisms: (1) 48-hour GSM timelock -- one of the longest in DeFi, (2) ESM acts as ultimate veto requiring 75,000 MKR, (3) Structured governance process. All well-documented and operational for years. | 9 | 9 | Non-Improvable (optimal) | [P0] GSM 48h timelock, [P0] ESM threshold at 75,000 MKR |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A -- sUSDS is not managed by an external strategy manager. It is a protocol-level savings product controlled by MKR governance. | N/A | N/A | N/A | Not applicable |

**Governance Subtotal: 52.5/67.5 (77.8%)**
- 3 applicable questions (O-G-04 = N/A): 2 scored 9 (sum = 18), 1 scored 3
- Raw sum = 21 out of max 27
- Weighted = (21/27) x 67.5 = 52.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Rune Christensen is the publicly identified founder, one of the most well-known figures in DeFi. Multiple contributing teams with verifiable track records over 8+ years. | 9 | 9 | Non-Improvable (optimal) | [P1] Rune Christensen publicly identified since 2015, [P2] Active governance forum |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Hundreds of contributors across multiple organizations. Open-source codebase. Multiple independent teams can maintain the protocol. Successfully transitioned from MakerDAO Foundation to decentralized DAO. | 9 | 9 | Non-Improvable (optimal) | [P1] Open source codebase, [P2] Multiple contributing teams |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | The MakerDAO Foundation (Cayman Islands) was dissolved in 2021, transferring all operations to the DAO. Current structure operates as a decentralized autonomous organization with various legal entities for specific functions. Endgame plan restructured governance into SubDAOs. | 9 | 9 | Non-Improvable (optimal) | [P1] Foundation dissolved 2021, [P2] DAO governance structure documented |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known ongoing or past material enforcement actions against MakerDAO/Sky entities. The protocol has operated openly since 2017 without regulatory enforcement. | 9 | 9 | Non-Improvable (optimal) | [P4] No enforcement actions found |
| O-TL-05 | Is there an on-call and incident response process for core teams? | The protocol has demonstrated incident response capability during Black Thursday. Multiple active teams monitor the system. However, no formal publicly documented 24/7 on-call SLA or incident runbooks exist. | 3 | 9 | Source Missing | [P1] Black Thursday demonstrated crisis response, but no formal on-call SLA documented |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Active governance forum, Discord, and community resources. One of the most active governance forums in DeFi. Support is community-driven but effective. | 9 | 9 | Non-Improvable (optimal) | [P2] Active governance forum, [P1] Comprehensive documentation |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. a16z, Paradigm, Dragonfly, Polychain Capital publicly known. RWA partnerships disclosed through governance. One of the most transparent investor/partner ecosystems in DeFi. | 9 | 9 | Non-Improvable (optimal) | [P2] Governance forum discloses partnerships |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | N/A -- sUSDS is not an externally curated vault. MKR governance directly controls the SSR rate. | N/A | N/A | N/A | Not applicable |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | N/A -- no external strategy manager. MakerDAO savings products (DSR/SSR) have never experienced collateral loss. | N/A | N/A | N/A | Not applicable |

**Team & Legal Subtotal: 61.1/67.5 (90.5%)**
- 7 applicable questions (O-TL-08, O-TL-09 = N/A): 6 scored 9 (sum = 54), 1 scored 3
- Raw sum = 57 out of max 63
- Weighted = (57/63) x 67.5 = 61.1

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive documentation at developers.sky.money and historical MakerDAO documentation maintained since 2017. Risk documentation covers collateral types, stability mechanisms, and governance processes. | 9 | 9 | Non-Improvable (optimal) | [P1] developers.sky.money, [P1] Historical MakerDAO documentation |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Extensive documentation on collateral flows, liquidation mechanics, and risk scenarios. For sUSDS, clearly documented that USDS sits in the Pot/SSR module earning the governance-set SSR rate. Loss scenarios documented. | 9 | 9 | Non-Improvable (optimal) | [P1] Technical documentation on DSR/SSR mechanism, [P1] Risk documentation |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Key contracts documented. sUSDS at 0xa3931d71877C0E7a3148CB7Eb4463524FEc27fbD. The developers.sky.money documentation and changelog.makerdao.com provide contract addresses. Some complexity from rebrand creating parallel references, but core addresses are documented. | 9 | 9 | Non-Improvable (optimal) | [P1] developers.sky.money, [P1] changelog.makerdao.com, [P0] Etherscan verified |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Governance roles (MKR holders, facilitators, delegates), permissions (GSM timelock, ESM), and change history (all executive votes on vote.makerdao.com) are well-documented. MakerDAO has one of the most transparent governance change histories in DeFi. | 9 | 9 | Non-Improvable (optimal) | [P0] vote.makerdao.com: complete history, [P0] GSM timelock documented and on-chain |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. For crypto assets: full on-chain transparency. Tools like daistats.com and makerburn.com provide real-time system-wide transparency. For RWA assets: reporting via governance through regular attestations. The protocol publishes both proof of reserves and proof of liabilities (total system debt visible on-chain). | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain crypto asset verification, [P3] daistats.com/makerburn.com |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. The sUSDS contract is verified on Etherscan. Core MakerDAO/Sky contracts are all verified. Full source code is readable. The MakerDAO codebase is one of the most scrutinized in DeFi. | 9 | 9 | Non-Improvable (optimal) | [P0] Etherscan: sUSDS contract verified, [P1] GitHub: open source |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions, all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Sky has a layered backstop: the Surplus Buffer (~$16.5-20M as of late 2025) absorbs bad debt first, with Flop Auctions (minting SKY to cover shortfalls) as a codified last resort. However, there is no dedicated sUSDS safety module with binding activation criteria. S&P characterized the non-dynamic surplus reserve buffer as a "noteworthy weakness." Parameters remain governance-controlled and there is no binding framework guaranteeing coverage for sUSDS-specific losses. Mid (3) because backstop exists but activation is discretionary. | 3 | 9 | Improvable | [P0] Surplus Buffer on-chain, [P1] info.sky.money/capital-backstop, [P2] S&P Global assessment (spglobal.com/ratings), [P3] medium.com/@Scoper Sky Protocol analysis |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Surplus Buffer is ~$16.5-20M (late 2025), with broader treasury ~$135.8M per DefiLlama, against ~$5.4B TVL. S&P assessed a risk-adjusted capital ratio of just 0.4% (July 2025) and identified the limited surplus as a key weakness. Protocol generates $435M annualized revenue and $168M annualized profit, with $102M+ in SKY buybacks since Feb 2025. However, the Surplus Buffer is not ring-fenced for sUSDS. Mid (3) because reserves are thin relative to TVL and not sUSDS-specific. | 3 | 9 | Improvable | [P2] S&P Global capital ratio assessment (spglobal.com/ratings), [P1] info.sky.money/capital-backstop, [P3] DefiLlama treasury data, [P0] On-chain Surplus Buffer |
| O-FR-03 | What is the estimated operational runway at current burn? | Very strong. $435M annualized revenue and $168M annualized profit in 2025. Over $102M deployed in SKY token buybacks since February 2025. Operationally sustainable since 2020. Foundation successfully dissolved 2021 with transition to DAO-funded operations. Runway comfortably above 24 months. | 9 | 9 | Non-Improvable (optimal) | [P3] ainvest.com: Sky revenue data, [P3] CoinMarketCap: SKY buyback data, [P2] DAO operational budgets |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Exceptionally resilient. Survived 2022 bear market, FTX collapse, USDC depeg. During Black Thursday (March 2020), the Surplus Buffer was depleted and Flop Auctions were triggered (minting MKR to cover ~$5.4M bad debt), but the system recovered fully with no DAI holder losses. Revenue has grown from ~$20M in 2020 to $435M annualized in 2025. The Flop Auction remains a codified last-resort backstop though rarely used. | 9 | 9 | Non-Improvable (optimal) | [P0] On-chain history through all crises, [P3] DeFiLlama TVL history, [P3] medium.com/@Scoper: Flop Auction analysis |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. sUSDS is immutable with permissionless withdrawals. SSR continues accruing at last set rate. ESM allows orderly wind-down. Open-source codebase enables community maintenance. System has operated through team transitions (Foundation dissolution, Core Unit changes) without disruption. | 9 | 9 | Non-Improvable (optimal) | [P0] sUSDS: immutable, permissionless, [P0] ESM provides orderly shutdown, [P1] Open source |

**Financial Resilience Subtotal: 49.5/67.5 (73.3%)**
- 3 questions scored 9 (sum = 27), 2 questions scored 3 (sum = 6)
- Raw sum = 33 out of max 45
- Weighted = (33/45) x 67.5 = 49.5

---

### **Operations Total: 230.6/270 (85.4%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 52.5 | 67.5 | 77.8% |
| Team & Legal | 61.1 | 67.5 | 90.5% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 49.5 | 67.5 | 73.3% |
| **Operations Total** | **230.6** | **270** | **85.4%** |

---

## Final Score Calculation

| Category | Subcategory | Current Points | Max Points | Potential Points |
|----------|-------------|----------------|------------|------------------|
| **Security** | Smart Contract Security | 158.2 | 180 | 180.0 |
| | Key Management | 160.0 | 180 | 180.0 |
| | **Security Subtotal** | **318.2** | **360** | **360.0** |
| **Strategy** | Protocol Mechanics | 45.0 | 45 | 45.0 |
| | Collateral | 45.0 | 45 | 45.0 |
| | Infra Counterparty | 45.0 | 45 | 45.0 |
| | Protocol Counterparty | 39.0 | 45 | 39.0 |
| | Liquidity | 45.0 | 45 | 45.0 |
| | Market | 39.0 | 45 | 45.0 |
| | **Strategy Subtotal** | **258.0** | **270** | **264.0** |
| **Operations** | Governance | 52.5 | 67.5 | 52.5 |
| | Team & Legal | 61.1 | 67.5 | 67.5 |
| | Documentation | 67.5 | 67.5 | 67.5 |
| | Financial Resilience | 49.5 | 67.5 | 67.5 |
| | **Operations Subtotal** | **230.6** | **270** | **255.0** |
| **TOTAL** | | **806.8** | **900** | **879.0** |

---


---
