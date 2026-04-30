# Lido - EarnETH Vault Risk Rating

**Rating Date**: 2026-04-29
**Final Grade**: CCC-
**Total Score**: 471.7/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 207.7/360 (57.7%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | Yes. Mellow Core Vault architecture audited by Sherlock (Tier-0, $70k competitive audit, Jul 2025), Nethermind (Tier-1, Sept 2025 and March 2, 2026 for EarnETH), ChainSecurity (Tier-0), StateMind, MixBytes (Tier-1), Decurity. >=2 independent external firms with public reports. **v0.1-gamma change**: Criteria now requires deployment configuration review. Audit reports from Sherlock and Nethermind cover contract code but there is no evidence that the deployed TimelockController delay (2 seconds), specific oracle signer configuration, or verifier target/function whitelists were explicitly reviewed in audit scope. Code audited but deployed configuration NOT confirmed in audit scope. Score Mid (3). | 3 | 9 | **Improvable** | [P1] [Mellow Security](https://docs.mellow.finance/security), [P1] [Sherlock Contest](https://audits.sherlock.xyz/contests/964), [P0] [Etherscan Timelock](https://etherscan.io/address/0x363Ba8843d06BA5968f55C26aB055162eDd62189) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent: Nethermind (Tier-1) audit of EarnETH March 2, 2026. Sherlock (Tier-0) competitive audit of Mellow Core Vaults Jul 2025. ChainSecurity (Tier-0). Multiple Tier-0 and Tier-1 auditors. | 9 | 9 | Non-Improvable (optimal) | [P1] [Mellow Security](https://docs.mellow.finance/security) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | EarnETH deployed Feb 2, 2026 received Nethermind audit March 2, 2026 (within 30 days). Core Vault architecture had Sherlock (Jul 2025) and Nethermind (Sept 2025) before deployment. | 9 | 9 | Non-Improvable (optimal) | [P1] [Mellow Security](https://docs.mellow.finance/security) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Nethermind Mellow LRT audit found minor rounding issue. However, specific findings counts and remediation status for the March 2026 EarnETH Nethermind audit are not publicly detailed. Cannot confirm all critical/high resolved without seeing the report. | 3 | 9 | **Source Missing** | [P1] [Mellow Security](https://docs.mellow.finance/security) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | EarnETH vault (0x6a37725) is a TransparentUpgradeableProxy (ERC-1967). TimelockController (0x363Ba884) exists but has a **confirmed minimum delay of 2 seconds** -- effectively no meaningful timelock. 5-of-8 multisig governs upgrades but the 2-second delay means upgrades can be executed near-instantly. Criteria requires >=24h for Low, 2-24h for Mid. 2 seconds is <2h. **Score High (1).** **v0.1-gamma: criteria unchanged but on-chain verification now reveals 2-second delay that was previously "Source Missing."** | 1 | 9 | **Improvable** | [P0] [Etherscan Timelock](https://etherscan.io/address/0x363Ba8843d06BA5968f55C26aB055162eDd62189) -- getMinDelay() = 2 seconds |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | The rsETH exploit (April 18, 2026) did NOT directly exploit EarnETH's smart contracts. KelpDAO's LayerZero bridge was the target. However, EarnETH held ~9% of TVL in rsETH ($21.6M), which is now potentially impaired. The vault is paused with unresolved losses. Scoring criteria: "Any confirmed exploit with permanent user loss" = High (1). While EarnETH was not directly exploited, user funds ARE at material risk of permanent loss via counterparty exposure. The loss event is more precisely a strategy failure (ST-PM-05) than an exploit of EarnETH code. However, under the broadest reading, users face potential permanent uncompensated loss. Scoring conservatively: the vault code itself had no exploit, but the rsETH incident caused the vault to become non-functional. The exploit affected a held asset, not the vault contract. Score Mid (3) -- one confirmed loss event from counterparty exposure, with partial compensation (DAO backstop), post-mortem published via governance forum. | 3 | 3 | Non-Improvable | [P2] [Lido Governance Forum](https://research.lido.fi/t/potential-losses-to-earneth-in-connection-with-rseth-incident/11473), [P4] [CryptoBriefing](https://cryptobriefing.com/lido-kelpdao-fallout-impact/) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No. Lido DAO and Mellow Protocol have no rug-pull allegations. Both are publicly identified, institutionally backed entities. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido Governance](https://lido.fi/governance), [P1] [Mellow Docs](https://docs.mellow.finance/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | The TimelockController was deployed with a 2-second delay from inception -- it was never reduced because it was always minimal. No reductions occurred. However, deploying with a 2-second delay from the start is itself a governance protection weakness. The question asks about "reductions" specifically; since the delay was never higher, technically there were no reductions. Score Low (9) per the literal criteria ("No timelock reductions in last 12 months OR only increases"). The underlying weakness is captured in S-SC-05. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Timelock](https://etherscan.io/address/0x363Ba8843d06BA5968f55C26aB055162eDd62189) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | No active bounty covering EarnETH or Mellow Core Vault contracts. Lido's $2M Immunefi bounty scopes only core protocol (stETH, validators, oracles) -- EarnETH/Mellow contracts are NOT listed in scope. The 2024 Immunefi Boost for Mellow Vault ($100k) ended September 2024 and covered old Mellow LRT contracts, not Core Vault architecture. | 1 | 9 | **Improvable** | [P1] [Immunefi Lido Scope](https://immunefi.com/bug-bounty/lido/scope/), [P1] [Immunefi Boost Finished](https://immunefi.com/audit-competition/boost-lido/scope/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Mellow has confirmed Hypernative integration for monitoring: notifications sent to team during critical operations, authority to halt withdrawals on suspicious activity. However, per v0.1-gamma verification principle: "Claiming to use a monitoring provider is NOT sufficient for Low (9)." Monitoring configuration details (what invariants are checked, what triggers exist, response SLAs) are not publicly verifiable. The rsETH incident revealed that monitoring did NOT prevent the vault from holding ~9% in an asset that collapsed -- no automatic protective action was taken before the curator manually paused. Score Mid (3). | 3 | 9 | **Source Missing** | [P4] [Mellow Substack - Hypernative](https://mellowprotocol.substack.com/p/introducing-multivaults), [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | ShareManager supports mint/burn/transfer pause via SET_FLAGS_ROLE. Oracle rejects anomalous reports. RiskManager enforces asset/subvault limits. However, during the rsETH crisis, no automatic circuit breaker halted the vault or reduced rsETH exposure. The curator had to manually pause. Per v0.1-gamma scope: "Circuit breakers must cover ALL automated capital flows." The vault's monitoring-to-pause pathway required manual multisig intervention, not automatic triggers. The rsETH incident proves that existing controls did NOT automatically protect user funds. Score High (1). | 1 | 9 | **Improvable** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture), [P4] [CryptoBriefing rsETH pause](https://cryptobriefing.com/lido-kelpdao-fallout-impact/) |

**Smart Contract Security Subtotal:**
- Raw scores: 4x9 + 4x3 + 3x1 = 36 + 12 + 3 = 51/99
- Adjusted: (51/99) x 180 = **92.7/180 (51.5%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Subvaults controlled by 5-of-8 multisig shared between Mellow and Lido. TimelockController manages governance actions. Changes documented via on-chain transactions. Diversified multisig governance. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Timelock](https://etherscan.io/address/0x363Ba8843d06BA5968f55C26aB055162eDd62189) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. 5-of-8 multisig (exceeds 3-of-5 minimum). However, timelock is only 2 seconds, which means upgrades can be executed near-instantly. The criteria requires "multisig/governance with threshold >=3 AND total signers >=5 AND timelock >=24h" for Low. The 5-of-8 threshold exceeds >=3/>=5 requirement but timelock is 2 seconds, far below 24h. Single key cannot move funds (Mid criterion met: "Single key can adjust limited parameters but cannot move user funds or upgrade custody"). Score Mid (3) -- multisig exists and exceeds threshold requirements, but the timelock >=24h criterion for Low is not met. | 3 | 9 | **Improvable** | [P0] [Etherscan Timelock](https://etherscan.io/address/0x363Ba8843d06BA5968f55C26aB055162eDd62189), [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | 5-of-8 multisig shared between Mellow and Lido teams, exceeding 3-of-5 threshold. However, specific signer identities are not publicly disclosed. Per framework: "If signer identities are fully unknown, independence cannot be confirmed -- score Mid (3) at best." | 3 | 9 | **Source Missing** | [P1] [Mellow Docs](https://docs.mellow.finance/) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | ShareManager supports mint/burn/transfer pause via SET_FLAGS_ROLE requiring multisig. No address-level withdrawal blocking. RedeemQueue processes FIFO without discrimination. Pause scope documented. However, the rsETH incident shows pause was used to block ALL withdrawals indefinitely (ongoing 9+ days as of April 29). While protocol-wide and multisig-controlled, the indefinite duration is notable. Still meets Low criteria: "Pause is time-bound, scope-limited, and requires multisig." The pause IS multisig-controlled and protocol-wide. | 9 | 9 | Non-Improvable (optimal) | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of assets in verified on-chain contracts. No off-chain custody. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Vault](https://etherscan.io/address/0x6a37725ca7f4CE81c004c955f7280d5C704a249e) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. EarnETH vault contracts are separate from Lido DAO treasury and Insurance Fund. FeeManager collects fees separately. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Vault](https://etherscan.io/address/0x6a37725ca7f4CE81c004c955f7280d5C704a249e) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | Vault deploys across Aave, Morpho, Uniswap, Pendle, Gearbox, Maple. Verifier contracts validate external calls against pre-approved targets/functions. RiskManager enforces per-subvault allowlists. However, no on-chain enforced timelock for whitelist additions; multisig can update without delay (2-second timelock). Additionally, rsETH (Kelp) was accessible as a strategy asset, and the lack of per-asset concentration limits allowed 9% allocation to a single counterparty token. Whitelist exists but is broad and updatable by multisig without meaningful timelock. Score Mid (3). | 3 | 9 | **Improvable** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture), [P0] [Etherscan Verifier](https://etherscan.io/address/0xBc46B79d79fCac1F4232D4Da1BA31aCED0AABFE0) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No public incident playbook for EarnETH or Mellow Core Vault operations. The rsETH crisis response was ad-hoc: curator manually paused, team communicated via governance forum, DAO activated $3M backstop through governance vote. No evidence of pre-existing playbook. However, the ad-hoc response WAS effective (pause within ~2 days, governance proposal within 5 days). Still, "No documented playbook exists" = High (1). | 1 | 9 | **Improvable** | [P2] [Lido Governance Forum](https://research.lido.fi/t/potential-losses-to-earneth-in-connection-with-rseth-incident/11473) |

**Key Management Subtotal:**
- Raw scores: 4x9 + 3x3 + 1x1 = 36 + 9 + 1 = 46/72
- Adjusted: (46/72) x 180 = **115.0/180 (63.9%)**

---

**Security Total: 92.7 + 115.0 = 207.7/360 (57.7%)**

---

### STRATEGY (30% Weight) -- Score: 125.92/270 (46.6%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield from lending interest (Aave, Morpho), LP fees (Uniswap), yield trading (Pendle), leveraged staking (Gearbox), institutional lending (Maple). rsETH leveraged staking was part of yield strategy. Mandate is ETH-denominated DeFi yield optimization. Percent contributions not disclosed. | 3 | 9 | **Improvable** | [P1] [Help Center](https://help.lido.fi/en/articles/14038913-vault-overview-earneth) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Multiple plausible loss vectors: liquidation from leveraged positions (Gearbox), impermanent loss (Uniswap), counterparty protocol exploits, oracle manipulation, borrower defaults (Maple). The rsETH exploit DEMONSTRATED that counterparty protocol failure can cause material losses. These are severe but plausible events. | 3 | 3 | Non-Improvable | [P1] [Help Center](https://help.lido.fi/en/articles/14038913-vault-overview-earneth), [P4] [CryptoBriefing](https://cryptobriefing.com/lido-kelpdao-fallout-impact/) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | Yes. Vault uses leveraged staking via Gearbox (up to ~3x). Also used leveraged rsETH/ETH looping on Aave. Leverage disclosed but caps not documented. "Moderate leverage with enforceable caps above 1.2x and up to 3x." | 3 | 3 | Non-Improvable | [P1] [Help Center](https://help.lido.fi/en/articles/14038913-vault-overview-earneth) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | RiskManager enforces per-subvault limits on-chain. Underlying protocols have liquidation mechanics. However, the rsETH crisis showed that the vault's leveraged rsETH/ETH position on Aave was at risk of liquidation due to rsETH price collapse. Curator had to manually deleverage. No EarnETH-specific automated LTV monitoring. | 3 | 9 | **Improvable** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | **YES. The rsETH exposure constitutes a confirmed loss event.** The vault held a leveraged rsETH/ETH position on Aave (~9% of TVL, ~$21.6M). The rsETH bridge exploit caused rsETH to trade at ~24% discount. Potential losses estimated up to 9,000 ETH. $3M first-loss buffer activated; Lido DAO approved and forwarded 2,500 stETH to DeFi United coordinated relief effort. DeFi United has secured sufficient ETH commitments to restore rsETH backing and published a technical implementation plan covering clearing of ~107,000 rsETH of exploiter positions across Aave and Compound. If successful, depositor losses may be fully avoided. However, execution remains subject to governance approvals and operational risks. The loss event exceeds the 0.5% of peak TVL threshold (9% >> 0.5%) regardless of compensation outcome. Score High (1). **Deal Breaker triggered.** | 1 | 1 | Non-Improvable | [P2] [Lido Governance Forum](https://research.lido.fi/t/potential-losses-to-earneth-in-connection-with-rseth-incident/11473), [P2] [DeFi United via Aave](https://x.com/aave/status/2048958367658332413), [P2] [Lido DAO rsETH Relief](https://research.lido.fi/t/lido-dao-contribution-to-coordinated-rseth-relief-effort/11483) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Mellow Core Vault includes RiskManager with per-subvault limits, asset allowlists, oracle deviation bounds, and Verifier-restricted callable functions. Partial framework with on-chain enforcement. However, no published document with quantitative limits for leverage, counterparty concentration, or drawdown thresholds. The rsETH incident revealed that per-counterparty concentration was not adequately limited (~9% in a single counterparty token). | 3 | 9 | **Improvable** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Vault is currently paused -- no yield being generated. Pre-pause, base yield from DeFi lending rates and staking rewards (~3-4% APR) was largely organic. Mellow points program supplemented yield. Without data on incentive share, sustainability cannot be confirmed. | 3 | 9 | **Source Missing** | [P1] [Help Center](https://help.lido.fi/en/articles/14038913-vault-overview-earneth) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Vault is currently PAUSED with positions unable to be unwound by users. Leveraged rsETH position cannot be unwound at fair value due to rsETH trading at discount. DeFi United's restoration plan aims to restore rsETH backing to its nominal 1.07 ETH ratio, which would allow positions to unwind at fair value if successful. However, execution is not yet complete. Under current conditions, slippage >5-10% is likely for the rsETH portion. Score High (1). | 1 | 3 | Non-Improvable | [P2] [Lido Governance Forum](https://research.lido.fi/t/potential-losses-to-earneth-in-connection-with-rseth-incident/11473), [P2] [DeFi United via Aave](https://x.com/aave/status/2048958367658332413) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | stETH/ETH peg dependency for leveraged staking. rsETH/ETH peg was critical for the leveraged rsETH position -- and it inverted catastrophically (24% discount). However, rsETH exposure was ~9% of vault, and the remaining strategy has <30% peg reliance. Pre-crisis: Low. Post-crisis with rsETH exposure still on books: the rsETH peg has already inverted. Score Mid (3) given demonstrated peg inversion on a material position. | 3 | 9 | Non-Improvable | [P4] [CryptoBriefing](https://cryptobriefing.com/lido-kelpdao-fallout-impact/) |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Curator pushes assets via pushAssets() validated by Verifier contracts. Oracle submissions by permissioned OracleSubmitter. No permissionless external functions can increase exposure. All allocation changes require human-initiated curator action. | 9 | 9 | Non-Improvable (optimal) | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |

**Protocol Mechanics Subtotal:**
- Scores: PM-01(3), PM-02(3), PM-03(3), PM-04(3), PM-05(1), PM-06(3), PM-07(3), PM-08(1), PM-09(3), PM-10(9)
- Raw: 1x9 + 7x3 + 2x1 = 9 + 21 + 2 = 32/90
- Adjusted: (32/90) x 45 = **16.0/45 (35.6%)**

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Deposits: ETH (Tier-0), WETH (thin wrapper), stETH/wstETH (BBB+ rated, most established LST). All are large-cap, well-established assets. However, the vault's STRATEGY allocates into rsETH (Kelp, rated D), which is not an input asset but is a held position. Collateral accepted for deposits is highest quality. | 9 | 9 | Non-Improvable (optimal) | [P1] [Help Center](https://help.lido.fi/en/articles/14038913-vault-overview-earneth) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | The vault's earnETH share token: vault is currently paused with shares not redeemable. Underlying deposit collateral (stETH/wstETH): July 2025 depeg ~0.3-0.6% lasting ~10 days, fully recovered within 2% threshold. However, the vault HOLDS rsETH which depegged ~24% -- this is a strategy position, not input collateral. Evaluating the vault share: shares are currently unredeemable (paused), which is worse than a depeg. Score High (1) for vault share behavior. | 1 | 3 | Non-Improvable | [P4] [CryptoBriefing](https://cryptobriefing.com/lido-kelpdao-fallout-impact/) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Applicable: stETH/wstETH collateral. Lido: 680+ operators, 3 modules, excellent client diversity, DVT adoption, Insurance Fund ~$15M. Historical slashing fully compensated. | 9 | 9 | Non-Improvable (optimal) | [P1] [Q3 2025 Metrics](https://blog.lido.fi/lido-validator-and-node-operator-metrics-q3-2025/) |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | 0% of deposited collateral is bridged/wrapped. All accepted assets (ETH, WETH, stETH, wstETH) are native Ethereum tokens. However, the strategy ALLOCATED ~9% to rsETH, which is a receipt token (not a bridged asset by definition). The rsETH loss stemmed from bridge security failure at KelpDAO, but rsETH itself is not a "bridged or wrapped asset" per the framework definition (it's a protocol receipt token). Score Low (9) per definition exclusions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Help Center](https://help.lido.fi/en/articles/14038913-vault-overview-earneth) |

**Collateral Subtotal:**
- Scores: C-01(9), C-02(1), C-03(9), C-04(9)
- Raw: 3x9 + 1x1 = 27 + 1 = 28/36
- Adjusted: (28/36) x 45 = **35.0/45 (77.8%)**

---

#### Infra Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum mainnet (Tier-0). Mellow permissioned Oracle. Counterparty protocols: Aave (Tier-0), Morpho (Tier-0), Uniswap. No external bridges or CEX. All critical infrastructure Tier-0/1. | 9 | 9 | Non-Improvable (optimal) | [P1] [Deployment Contracts](https://github.com/lidofinance/docs/blob/main/earn/deployment-contracts.md) |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | **v0.1-gamma: MANDATORY hardcoded oracle check.** Mellow Oracle (0xAda1f4c2) uses permissioned consensus signers with deviation bounds, timeouts, and suspicious report validation. Oracle is NOT hardcoded -- values CAN be updated and corrected by permissioned signers. Passes the hardcoded check. However, this is a custom permissioned oracle (not Tier-0 Chainlink/Pyth). Single primary provider without independent fallback. No secondary oracle source. Score Mid (3): "Single primary provider used with partial fallback AND only Tier-0/1." | 3 | 9 | **Improvable** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture), [P0] [Etherscan Oracle](https://etherscan.io/address/0xAda1f4c24603aB2fe5aBd35BCD12370e98A20358) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | No critical off-chain infrastructure. Vault operates entirely on-chain. Per applicability check: no critical off-chain providers. | 9 | 9 | Non-Improvable (optimal) | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | The rsETH crisis (April 18-present) is the first major incident. The oracle and vault infrastructure functioned correctly -- the curator was able to pause the vault, reduce leverage, and cut debt. Infrastructure components performed their designed function during the crisis. However, the crisis is still ongoing with vault paused. The incident caused "temporary delays" (ongoing) but has not caused "prolonged inability to access" PERMANENTLY -- the vault pause is expected to be temporary. Score Mid (3): "Past incidents caused temporary delays or degraded access but recovered without permanent user losses." | 3 | 9 | Non-Improvable | [P4] [CryptoBriefing](https://cryptobriefing.com/lido-kelpdao-fallout-impact/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain halt >30 minutes in the last 12+ months. Tier-0 reliability. | 9 | 9 | Non-Improvable (optimal) | Ethereum Tier-0 status |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Applicable for stETH collateral. Lido: Launchnodes Oct 2023, RockLogic Apr 2023 -- both >12 months ago. No events in last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido Post-Mortems](https://blog.lido.fi/category/postmortem/) |
| ST-IC-07 | Are validators diverse geographically and by operator? | Applicable for stETH collateral. Lido: 680+ operators, multi-region, excellent client diversity. No single operator >25%. | 9 | 9 | Non-Improvable (optimal) | [P1] [Q3 2025 Metrics](https://blog.lido.fi/lido-validator-and-node-operator-metrics-q3-2025/) |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | The rsETH incident demonstrated that a single counterparty asset failure CAN block withdrawals (vault paused 9+ days and counting). Oracle signer unavailability could also delay exits. While the vault code didn't fail, the curator's response to a counterparty failure resulted in blocked withdrawals. "Single infra component failure can realistically block withdrawals for more than 48 hours." The pause is curator-initiated, not infrastructure failure per se, but the effect is the same -- users cannot withdraw. Score Mid (3) as the component that failed was an external protocol (rsETH), not EarnETH's own infrastructure. Withdrawals blocked due to curator decision, not infra failure. | 3 | 9 | **Improvable** | [P4] [CryptoTimes](https://www.cryptotimes.io/2026/04/21/21-million-on-lido-earneth-at-risk-in-kelp-dao-exploit/) |
| ST-IC-09 | How robust is the cross-chain messaging or bridge verification setup? | **v0.1-gamma new question.** N/A -- EarnETH operates exclusively on Ethereum mainnet with no cross-chain messaging or bridge dependency. The rsETH bridge failure was in KelpDAO's infrastructure, not EarnETH's. | N/A | N/A | N/A | - |
| ST-IC-10 | Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting? | **v0.1-gamma new question.** N/A -- No bridge/cross-chain minting exists in EarnETH. | N/A | N/A | N/A | - |
| ST-IC-11 | Is the off-chain verification infrastructure resilient to data-source manipulation? | **v0.1-gamma new question.** N/A -- EarnETH is fully on-chain with no off-chain verification component. Oracle submissions are on-chain by permissioned signers. | N/A | N/A | N/A | - |

**Infra Counterparty Subtotal (8 of 11 Q scored):**
- Scores: IC-01(9), IC-02(3), IC-03(9), IC-04(3), IC-05(9), IC-06(9), IC-07(9), IC-08(3)
- Raw: 5x9 + 3x3 = 45 + 9 = 54/72
- Adjusted: (54/72) x 45 = **33.75/45 (75.0%)**

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All venues disclosed: Aave (Tier-0), Morpho (Tier-0), Uniswap, Pendle, Gearbox, Maple. Also held rsETH (Kelp, now rated D). No CEX or RWA. The inclusion of rsETH/Kelp in the strategy -- a protocol that turned out to have catastrophic bridge vulnerability -- is notable. Mix of Tier-0 and untiered venues with some high-risk exposure. "Most venues disclosed with partial tiering and some Tier-2 venues or untiered but established venues." | 3 | 9 | **Improvable** | [P1] [Blog](https://blog.lido.fi/lido-earn-expands-with-earneth-and-earnusd/) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Fees disclosed: 1% platform fee, 10% performance fee. Fee split between Mellow and Lido partially known. Mellow points program exists. Specific revenue-share terms not fully detailed. | 3 | 9 | **Source Missing** | [P1] [Help Center](https://help.lido.fi/en/articles/14038913-vault-overview-earneth) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | RiskManager enforces per-subvault limits and asset allowlists on-chain. However, the rsETH incident revealed that ~9% of TVL was concentrated in a single counterparty token (rsETH via leveraged looping on Aave). Specific per-counterparty caps not publicly documented. The 9% concentration in rsETH suggests limits were either too high or non-existent for individual asset exposure. Score High (1): "No clear per-counterparty limits exist or limits informal without breach handling." | 1 | 9 | **Improvable** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture), [P2] [Lido Governance Forum](https://research.lido.fi/t/potential-losses-to-earneth-in-connection-with-rseth-incident/11473) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Currently: positions CANNOT be unwound -- vault is paused. The rsETH position cannot be unwound at fair value (rsETH trading at ~24% discount). Even before the crisis, Gearbox positions required deleveraging time and Pendle had maturity constraints. Under current conditions, positions cannot be unwound within the stated 72h horizon without accepting significant haircuts. Score High (1). | 1 | 3 | Non-Improvable | [P2] [Lido Governance Forum](https://research.lido.fi/t/potential-losses-to-earneth-in-connection-with-rseth-incident/11473) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Mellow Protocol identified as infrastructure provider. Lido DAO as protocol partner. Veda mentioned as co-curator. Underlying protocols are public DeFi platforms. | 9 | 9 | Non-Improvable (optimal) | [P1] [Blog](https://blog.lido.fi/lido-earn-expands-with-earneth-and-earnusd/) |

**Protocol Counterparty Subtotal:**
- Scores: PC-01(3), PC-02(3), PC-03(1), PC-04(1), PC-05(9)
- Raw: 1x9 + 2x3 + 2x1 = 9 + 6 + 2 = 17/45
- Adjusted: 17.0/45 (37.8%)

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Withdrawals via RedeemQueue. Pause requires 5-of-8 multisig, protocol-wide, no address-level blocking. However, the vault IS currently paused with all withdrawals blocked as of April 29, 2026 (9+ days). While the pause mechanism itself is properly governed (multisig-controlled, publicly visible), the EFFECT is that users cannot withdraw. The criteria evaluates the mechanism, not the current state. Score Low (9) for withdrawal mechanism design. | 9 | 9 | Non-Improvable (optimal) | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Currently NO -- vault is paused, zero liquidity available for redemptions. Even if unpaused, the rsETH position (~9%) cannot be liquidated at fair value. Remaining ~91% of positions (Aave, Morpho, Uniswap) are liquid under normal conditions. Near-total exits would stress leveraged components. Under current conditions, 0% of TVL can be redeemed. Score High (1). | 1 | 3 | Non-Improvable | [P2] [Lido Governance Forum](https://research.lido.fi/t/potential-losses-to-earneth-in-connection-with-rseth-incident/11473) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | YES. The vault is currently in an indefinite freeze (9+ days as of April 29, 2026). All deposits and withdrawals paused. This is the first and ongoing freeze in the vault's 3-month history. Score High (1): "prolonged freezes, unresolved delays." | 1 | 3 | Non-Improvable | [P1] [Lido Earn Page](https://stake.lido.fi/earn) -- "Deposits and withdrawal processing for EarnETH are currently paused" |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Vault is paused -- no redemptions possible regardless of caps. Even if unpaused, the rsETH position creates an effective cap on full redemptions at fair value. Score High (1). | 1 | 9 | **Improvable** | [P4] [CryptoTimes](https://www.cryptotimes.io/2026/04/21/21-million-on-lido-earneth-at-risk-in-kelp-dao-exploit/) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | The rsETH crisis IS the first real stress test, and the result was catastrophic for exit liquidity: vault fully paused, zero exits possible. This is a confirmed stress event with the worst possible liquidity outcome (total freeze). Score High (1). | 1 | 3 | Non-Improvable | [P4] [CryptoBriefing](https://cryptobriefing.com/lido-kelpdao-fallout-impact/) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | Stated withdrawal: up to 72h. Currently, vault has been paused >9 days (far exceeding 72h). The rsETH position may require weeks or months to resolve. Estimated >30% of assets effectively longer-dated than promised. Score High (1). | 1 | 3 | Non-Improvable | [P2] [Lido Governance Forum](https://research.lido.fi/t/potential-losses-to-earneth-in-connection-with-rseth-incident/11473) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Primary redemption via RedeemQueue returning wstETH. wstETH has deep secondary market. Users do not depend on secondary markets for earnETH tokens. However, protocol redemption is currently unavailable (paused). Score Mid (3) -- mechanism exists but is currently non-functional. | 3 | 9 | Non-Improvable | [P1] [Deployment Contracts](https://github.com/lidofinance/docs/blob/main/earn/deployment-contracts.md) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | Collateral (ETH, stETH, wstETH): deepest liquidity in DeFi. Receipt token (earnETH): no secondary market, and in-protocol redemption paused. Adequate for collateral but receipt token currently illiquid. Score Mid (3). | 3 | 9 | Non-Improvable | [P3] [DeFiLlama Lido](https://defillama.com/protocol/lido) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | The rsETH crisis demonstrated a bank-run-like scenario: users cannot withdraw, vault paused, losses anticipated. The leveraged component was particularly vulnerable. The $3M backstop is insufficient for estimated 9,000 ETH losses. Score High (1): "Fast bank-run likely to force meaningful permanent losses, haircuts, or prolonged withdrawal blocks." | 1 | 3 | Non-Improvable | [P2] [Lido Governance Forum](https://research.lido.fi/t/potential-losses-to-earneth-in-connection-with-rseth-incident/11473) |

**Liquidity Subtotal:**
- Scores: L-01(9), L-02(1), L-03(1), L-04(1), L-05(1), L-06(1), L-07(3), L-08(3), L-09(1)
- Raw: 1x9 + 2x3 + 6x1 = 9 + 6 + 6 = 21/81
- Adjusted: (21/81) x 45 = **11.67/45 (25.9%)**

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | N/A. earnETH is a share token reflecting underlying positions, not a pegged token. Redemptions return wstETH at oracle-determined NAV. No meaningful secondary market. | N/A | N/A | N/A | - |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Strategy uses leverage (Gearbox ~2-3x, plus rsETH looping on Aave). The rsETH crisis DEMONSTRATED that leveraged positions CAN cause permanent losses. Moderate directional exposure with demonstrated loss realization. | 3 | 3 | Non-Improvable | [P1] [Help Center](https://help.lido.fi/en/articles/14038913-vault-overview-earneth) |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | EarnETH inherits rate dynamics from underlying protocols (Aave, Morpho rate curves). During rsETH crisis, elevated borrowing rates across lending markets caused additional yield compression and negative carry on leveraged positions. The vault experienced a real rate stress event. Score Mid (3). | 3 | 9 | Non-Improvable | [P4] [CryptoNewsZ](https://www.cryptonewsz.com/lido-halts-earneth-rseth-breach-3m-buffer/) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | No public stress testing. The rsETH crisis was effectively an unmodeled tail event that hit the vault. No evidence of prior scenario analysis for counterparty protocol exploits or leveraged position unwinding under stress. Score High (1). | 1 | 9 | **Improvable** | No public modeling found |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Yes. Gearbox leveraged positions can be liquidated. The rsETH price collapse (24% discount) put the leveraged rsETH/ETH position at risk of Aave liquidation. Curators manually deleveraged to avoid liquidation. Moderate leverage with demonstrated near-liquidation event. Score Mid (3). | 3 | 3 | Non-Improvable | [P4] [CryptoBriefing](https://cryptobriefing.com/lido-kelpdao-fallout-impact/) |

**Market Subtotal (4 of 5 Q scored):**
- Scores: M-02(3), M-03(3), M-04(1), M-05(3)
- Raw: 3x3 + 1x1 = 9 + 1 = 10/36
- Adjusted: (10/36) x 45 = **12.5/45 (27.8%)**

---

**Strategy Total: 16.0 + 35.0 + 33.75 + 17.0 + 11.67 + 12.5 = 125.92/270 (46.6%)**

---

### OPERATIONS (30% Weight) -- Score: 138.08/270 (51.1%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid model. EarnETH subvaults governed by 5-of-8 multisig. Broader Lido DAO on-chain governance (LDO + Dual Governance) controls strategic decisions. Major vault changes may require DAO vote. Day-to-day multisig-controlled. | 3 | 9 | **Improvable** | [P1] [Lido Governance](https://lido.fi/governance) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | LDO governance token exists. Initial distribution: founding members 64%. Dual Governance gives stETH holders veto power. Top 10 LDO addresses likely control >33% but <=66%. Score Mid (3). | 3 | 3 | Non-Improvable | [P1] [Dual Governance](https://blog.lido.fi/dual-governance-101-explainer/) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | TimelockController (0x363Ba884) exists BUT with only 2-second delay. This is effectively no timelock. Broader Lido has Dual Governance with 5-45 day dynamic delays, but that applies to Lido DAO decisions, not EarnETH-specific operations. The EarnETH-specific timelock is 2 seconds. Score High (1): "Timelocks missing, easily bypassed, or reduced to very short windows." 2 seconds is a "very short window." | 1 | 9 | **Improvable** | [P0] [Etherscan Timelock](https://etherscan.io/address/0x363Ba8843d06BA5968f55C26aB055162eDd62189) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Strategy curator can be replaced through defined role updates. RedeemQueue continues independently. However, vault is currently paused (withdrawals blocked) due to strategy-related crisis. The replacement mechanism exists but the current situation demonstrates that strategy failures can block withdrawals. Score Mid (3). | 3 | 9 | **Improvable** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |

**Governance Subtotal:**
- Scores: G-01(3), G-02(3), G-03(1), G-04(3)
- Raw: 3x3 + 1x1 = 9 + 1 = 10/36
- Adjusted: (10/36) x 67.5 = **18.75/67.5 (27.8%)**

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Lido: Founded by Konstantin Lomashuk, Vasiliy Shapovalov, Jordan Fish (Cobie). Mellow: Founded 2021, BVI-registered, team from Yandex, McKinsey backgrounds. Both teams verifiable. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido](https://lido.fi/), [P4] [PitchBook Mellow](https://pitchbook.com/profiles/company/484848-82) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Lido has large contributor ecosystem. Mellow has dedicated team. Multiple contributors to both codebases. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido Governance](https://lido.fi/governance) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Lido: Lido Labs Foundation, Cayman Islands. Mellow: BVI-registered. Both jurisdictions disclosed. | 9 | 9 | Non-Improvable (optimal) | [P2] [SEC Filing](https://www.sec.gov/files/ctf-input-lido-labs-foundation-3-24-25.pdf) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | Samuels v. Lido DAO class action pending. Civil matter, not regulatory enforcement. Fact discovery closed Feb 2026, expert reports April 2026, summary judgment August 2026. | 3 | 9 | **Source Missing** | [P2] [CourtListener](https://www.courtlistener.com/docket/68095676/samuels-v-lido-dao/) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | The rsETH crisis response demonstrated SOME incident response capability: curator paused vault within ~2 days, DAO backstop activated within 5 days, governance proposal for relief within 5 days. However, no formal pre-existing playbook. Response was ad-hoc but effective. Informal on-call with partial playbooks. Score Mid (3). | 3 | 9 | **Improvable** | [P2] [Lido Governance Forum](https://research.lido.fi/t/potential-losses-to-earneth-in-connection-with-rseth-incident/11473) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Active Discord, governance forum, Help Center. During rsETH crisis, Lido communicated via governance forum and social media within 2-3 days. Critical issues acknowledged within 24 hours. | 9 | 9 | Non-Improvable (optimal) | [P1] [Help Center](https://help.lido.fi/), [P2] [Research Forum](https://research.lido.fi/) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Lido: $145M+ from a16z, Paradigm. Mellow: $2.75M+ from ParaFi, Arrington XRP Capital. Partnership publicly disclosed. | 9 | 9 | Non-Improvable (optimal) | [P4] [CoinDesk a16z](https://www.coindesk.com/business/2022/03/03/a16z-investing-70m-into-ethereum-staking-provider-lido-finance) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Mellow operates multiple vaults (EarnETH, EarnUSD, strETH, DVV). During rsETH crisis, DVV and EarnUSD were confirmed unaffected -- different strategy exposure. Partial disclosure with qualitative conflict policies. | 3 | 9 | **Improvable** | [P1] [Blog](https://blog.lido.fi/lido-earn-expands-with-earneth-and-earnusd/) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | **YES. The rsETH exposure in EarnETH represents an ongoing loss event.** Potential losses up to 9,000 ETH. $3M first-loss buffer activated but insufficient. This is a current loss event under the same manager (Mellow/Veda curators). Score High (1): "Any uncompensated depositor losses." | 1 | 1 | Non-Improvable | [P2] [Lido Governance Forum](https://research.lido.fi/t/potential-losses-to-earneth-in-connection-with-rseth-incident/11473) |

**Team & Legal Subtotal:**
- Scores: TL-01(9), TL-02(9), TL-03(9), TL-04(3), TL-05(3), TL-06(9), TL-07(9), TL-08(3), TL-09(1)
- Raw: 5x9 + 3x3 + 1x1 = 45 + 9 + 1 = 55/81
- Adjusted: (55/81) x 67.5 = **45.83/67.5 (67.9%)**

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Mellow Core Vault architecture docs comprehensive. Lido Help Center has EarnETH overview. However, the Help Center article omits material information: no mention of rsETH/Kelp exposure, leverage details minimal, risk disclosures generic. Docs do not mention specific counterparty protocols beyond Aave, Uniswap, Morpho. Partially incomplete. | 3 | 9 | **Improvable** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture), [P1] [Help Center](https://help.lido.fi/en/articles/14038913-vault-overview-earneth) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Help Center describes strategy types and mentions generic risks. No systematic scenario mapping. The rsETH exposure and its risk profile were not disclosed in pre-crisis documentation. Score Mid (3). | 3 | 9 | **Improvable** | [P1] [Help Center](https://help.lido.fi/en/articles/14038913-vault-overview-earneth) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. deployment-contracts.md lists all 24 EarnETH contracts in one place. | 9 | 9 | Non-Improvable (optimal) | [P1] [Deployment Contracts](https://github.com/lidofinance/docs/blob/main/earn/deployment-contracts.md) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Mellow docs describe roles. TimelockController visible on Etherscan. However, role documentation scattered. The 2-second timelock delay is NOT disclosed in documentation (only discoverable on-chain). Score Mid (3). | 3 | 9 | **Improvable** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | On-chain vault holdings verifiable via Etherscan. Subvault balances visible. Oracle publishes share prices. However, vault is currently paused making real-time reserve status uncertain (rsETH portion impaired). Still, on-chain verification is possible. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Vault](https://etherscan.io/address/0x6a37725ca7f4CE81c004c955f7280d5C704a249e) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. All core contracts verified on Etherscan with readable source code. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Vault](https://etherscan.io/address/0x6a37725ca7f4CE81c004c955f7280d5C704a249e) |

**Documentation Subtotal:**
- Scores: DT-01(3), DT-02(3), DT-03(9), DT-04(3), DT-05(9), DT-06(9)
- Raw: 3x9 + 3x3 = 27 + 9 = 36/54
- Adjusted: (36/54) x 67.5 = **45.0/67.5 (66.7%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Lido DAO activated $3M first-loss capital for EarnETH (DAO burns vault shares to absorb losses). Additionally, the DAO approved and forwarded a one-time 2,500 stETH (~$5.8M) contribution to the DeFi United coordinated relief effort. Insurance Fund (~$15M) also exists. The backstop was activated via discretionary governance vote, not binding criteria. Combined DAO commitment (~$8.8M) still below potential 9,000 ETH (~$21M) loss, but DeFi United's broader plan (with secured ETH commitments from ecosystem participants) aims to make rsETH whole. Backstop activation demonstrated but remains discretionary and undersized relative to full exposure. Score Mid (3). | 3 | 9 | **Improvable** | [P2] [Lido Governance Forum](https://research.lido.fi/t/lido-dao-contribution-to-coordinated-rseth-relief-effort/11483), [P2] [DeFi United via Aave](https://x.com/aave/status/2048958367658332413) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Lido treasury ~$133.5M (including ~$79.3M stETH, ~$34.9M LDO, ~$11.9M USDT, ~$1.97M DAI). Insurance Fund ~$15M. Combined ~$148.5M against ~$19B total Lido TVL = ~0.8%. Below 1% threshold. Against EarnETH's ~$240M TVL, reserves appear substantial but total protocol ratio is low. Score Mid (3). | 3 | 9 | **Source Missing** | [P0] [Etherscan Agent](https://etherscan.io/address/0x3e40D73EB977Dc6a537aF587D48316feE66E9C8c), [P3] DeFiLlama Treasury API |
| O-FR-03 | What is the estimated operational runway at current burn? | Lido generating ~$55-74M annual revenue. Treasury ~$133.5M+. Runway >24 months. $60M GOOSE-3 budget approved for 2026. | 9 | 9 | Non-Improvable (optimal) | [P2] [Tokenholder Update](https://blog.lido.fi/recap-lido-tokenholder-update-february-2026/) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | **v0.1-gamma: now includes composability contagion assessment.** The rsETH crisis IS a major stress event for EarnETH. Vault TVL effectively frozen (paused). Revenue = 0 during pause. Buffers deployed: $3M first-loss activated, 2,500 stETH forwarded to DeFi United relief. The vault EXPERIENCED contagion FROM the rsETH/Kelp exploit -- a victim of composability contagion from another protocol's failure. The coordinated DeFi United restoration plan (Aave, Kelp, LayerZero, Lido) demonstrates strong ecosystem response, but the stress event did cause structural TVL freeze, revenue impairment, and buffer depletion. Score High (1) per current state. | 1 | 3 | Non-Improvable | [P2] [Lido Governance Forum](https://research.lido.fi/t/potential-losses-to-earneth-in-connection-with-rseth-incident/11473), [P2] [DeFi United via Aave](https://x.com/aave/status/2048958367658332413) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Core vault contracts on-chain. However, oracle submissions require permissioned signers. If signers disappear, new redemption batches cannot be processed. The rsETH crisis shows the vault requires active team intervention to resolve. Score Mid (3). | 3 | 9 | **Improvable** | [P1] [Mellow Architecture](https://docs.mellow.finance/core-vaults/architecture) |

**Financial Resilience Subtotal:**
- Scores: FR-01(3), FR-02(3), FR-03(9), FR-04(1), FR-05(3)
- Raw: 1x9 + 3x3 + 1x1 = 9 + 9 + 1 = 19/45
- Adjusted: (19/45) x 67.5 = **28.5/67.5 (42.2%)**

---

**Operations Total: 18.75 + 45.83 + 45.0 + 28.5 = 138.08/270 (51.1%)**

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 51 | 99 | 92.7 | 180 | 51.5% |
| | Key Management (8 Q) | 46 | 72 | 115.0 | 180 | 63.9% |
| | **Security Subtotal** | | | **207.7** | **360** | **57.7%** |
| **Strategy** | Protocol Mechanics (10 Q) | 32 | 90 | 16.0 | 45 | 35.6% |
| | Collateral (4 Q) | 28 | 36 | 35.0 | 45 | 77.8% |
| | Infra Counterparty (8 of 11 Q scored) | 54 | 72 | 33.75 | 45 | 75.0% |
| | Protocol Counterparty (5 Q) | 17 | 45 | 17.0 | 45 | 37.8% |
| | Liquidity (9 Q) | 21 | 81 | 11.67 | 45 | 25.9% |
| | Market (4 of 5 Q scored) | 10 | 36 | 12.5 | 45 | 27.8% |
| | **Strategy Subtotal** | | | **125.92** | **270** | **46.6%** |
| **Operations** | Governance (4 Q) | 10 | 36 | 18.75 | 67.5 | 27.8% |
| | Team & Legal (9 Q) | 55 | 81 | 45.83 | 67.5 | 67.9% |
| | Documentation (6 Q) | 36 | 54 | 45.0 | 67.5 | 66.7% |
| | Financial Resilience (5 Q) | 19 | 45 | 28.5 | 67.5 | 42.2% |
| | **Operations Subtotal** | | | **138.08** | **270** | **51.1%** |
| **TOTAL** | | | | **471.7** | **900** | **52.4%** |

---

