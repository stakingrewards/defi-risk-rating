# Aave - EURC (Ethereum Core Market) Risk Rating

**Rating Date**: 2026-04-02
**Final Grade**: A-
**Total Score**: 848.5/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-beta

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 342.9/360 (95.2%)

**NOTE: All Security scores are IDENTICAL to other Aave Ethereum V3 Core Market ratings (WETH, USDT, USDC, WBTC, wstETH, weETH, cbBTC, USDe). Same smart contracts, same governance, same key management.**

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 30+ audits from Tier-0/1 firms: OpenZeppelin (2021), Trail of Bits (2022), Sigma Prime (2022, 2023), PeckShield (2022), ABDK (2022), Certora (continuous formal verification through V3.6), MixBytes (V3.1+), Pashov (V3.2+), Sherlock (V3.3), Oxorio (V3.2-V3.3). Latest V3.6 audits include Certora and StErMi. All reports public on GitHub. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [GitHub Audits](https://github.com/aave/aave-v3-core/tree/master/audits), [P1] [aave-v3-origin repo](https://github.com/aave-dao/aave-v3-origin) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | V3.4 (June 2025): Certora (Tier-0, formal verification), StErMi. V3.3 (Jan 2025): Certora (Tier-0), Sherlock (Tier-0), Oxorio, StErMi. Multiple Tier-0 auditors on latest versions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [Certora Reports](https://www.certora.com/reports/aave-v3-risk-steward) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Every major version (V3.0 through V3.6) has been audited. Umbrella Safety Module (June 2025), GHO (7 audits), Governance V3 all received dedicated audits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [GitHub aave-v3-origin](https://github.com/aave-dao/aave-v3-origin) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. November 2023 critical vulnerability (stable rate bug) patched immediately via emergency governance action. All findings tracked with remediation. Certora formal verification validates invariants. Sherlock contest on V3.3 validated remediation. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P1] [Aave Security](https://aave.com/security) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Upgradeable via transparent proxy pattern managed through PoolAddressesProvider. Upgrades require full DAO governance vote (AAVE/stkAAVE/aAAVE token voting with quorum) followed by 1-day standard timelock or 7-day critical timelock. Two 5-of-9 Guardian multisigs can veto malicious proposals. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No user fund losses in protocol history. Nov 2023: Critical stable rate vulnerability patched before exploitation. Aug 2024: Periphery contract incident ($56K tip jar -- not user deposits). Feb 2025: $210M liquidations processed with zero bad debt. Feb 2026: $429M record liquidations with zero bad debt. March 2026: CAPO oracle misconfiguration caused $27.78M wstETH liquidations but EURC suppliers were completely unaffected and DAO committed to 100% reimbursement of affected wstETH positions. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Post-Mortem](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269), [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Founded by Stani Kulechov in 2017 (ETHLend). 8+ year track record with fully transparent governance, audited code, and publicly identified team. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P3] [Crunchbase](https://www.crunchbase.com/organization/ethlend) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. Standard proposals maintain 1-day delay, critical changes require 7-day delay. Governance V3 introduced cross-chain voting via storage proofs, maintaining or strengthening timelock protections. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Immunefi bounty up to $1M for critical smart contract vulnerabilities. 83+ assets in scope. Active since October 2023, last updated September 2025. Bug bounty actively used -- Nov 2023 critical vulnerability reported through program. | 9 | 9 | Non-Improvable (optimal) | [P1] [Immunefi](https://immunefi.com/bug-bounty/aave/), [P2] [BGD Bounty Payout Aug 2025](https://governance.aave.com/t/bgd-request-for-bounty-payout-august-2025/23096) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. DDoS protection, DNSSEC authentication, intrusion detection, CSP/SRI checks documented. BGD Labs provides continuous monitoring. Chaos Labs operates Risk Stewards with 1,100+ automated risk parameter adjustments since late 2024. Slope2 Risk Oracle provides automated interest rate response to utilization spikes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P2] [Chaos Labs Slope2 Oracle](https://chaoslabs.xyz/posts/introducing-the-aave-slope2-risk-oracle) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | Yes. Protocol Emergency Guardian (5-of-9) can pause markets. V3.3 bad debt verification prevents new bad debt post-liquidation. Slope2 Risk Oracle automatically adjusts borrow rates during high utilization. Feb 2026: $429M record liquidations processed via automated mechanisms. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Features](https://github.com/aave-dao/aave-v3-origin/blob/main/docs/3.3/Aave-v3.3-features.md), [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |

**Smart Contract Security Subtotal: 180.0/180 (100.0%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | DAO governance via AAVE/stkAAVE/aAAVE token voting. All changes require on-chain vote with quorum, then 1-7 day timelock execution. Protocol Emergency Guardian (5-of-9) and Governance Emergency Guardian (5-of-9) provide emergency controls with documented signer composition. Risk Stewards (Chaos Labs) adjust parameters within governance-approved bounds. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Requires DAO vote (quorum required) + timelock execution. Guardians can only pause/veto, not move funds or upgrade custody. Protocol is non-custodial with permissionless withdrawals. No single entity can unilaterally access or redirect user funds. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2#code) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Protocol Emergency Guardian: 5-of-9 (Chaos Labs, LlamaRisk, Karpatkey, TokenLogic, Certora, BGD Labs, ACI, 2 DAO delegates). Governance Emergency Guardian: 5-of-9 (Zapper, ParaSwap, Standard Crypto, DeFi Saver, Balancer, Chainlink, Lido, security firms). Diverse set of independent entities. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [Guardian Renewal](https://governance.aave.com/t/arfc-renewal-of-aave-guardian-2024/17523) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause limited to Guardians via 5-of-9 multisig. No address-level blocking capability. Withdrawals are permissionless via Pool contract based on available liquidity. No arbitrary censorship mechanism. Risk Stewards can adjust supply/borrow caps within governance-approved bounds. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user EURC deposits held in Pool V3 contract (0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2). Permissionless supply/withdraw via smart contract. aEthEURC tokens (0xAA6e91C82942aeAE040303Bf96c15a6dBcB82CA0) represent user positions. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P0] [Etherscan aEthEURC](https://etherscan.io/address/0xAA6e91C82942aeAE040303Bf96c15a6dBcB82CA0) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation: Pool V3 contract holds all user funds. DAO treasury managed separately by Karpatkey with independent wallet structure. No co-mingling of user deposits with treasury operations. | 9 | 9 | Non-Improvable (optimal) | [P2] [DAO Financial Reports](https://governance.aave.com/t/aave-dao-financial-reports-financial-metrics/5575), [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- Aave is a lending protocol, not a vault. Users deposit assets directly to pools. No external protocol routing of user funds. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | **Partial.** November 2023 incident demonstrated rapid emergency response (pools secured within hours). Feb 2026: Chaos Labs Risk Stewards adjusted parameters in real-time during market crash. March 2026: CAPO incident response included post-mortem and reimbursement plan within days. However, no comprehensive public playbook for key rotation or signer replacement procedures is documented. | 3 | 9 | **Improvable** | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335) |

**Key Management Subtotal: 162.9/180 (90.5%)**
- 6 questions at score 9 = 54 points
- 1 question at score 3 = 3 points
- 1 question N/A (S-KM-07)
- Raw: 57/63, Weighted: (57/63) x 180 = 162.857 = 162.9

---

### **Security Total: 342.9/360 (95.2%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 180.0 | 180 | 100.0% |
| Key Management | 162.9 | 180 | 90.5% |
| **Security Total** | **342.9** | **360** | **95.2%** |

---

### STRATEGY (30% Weight) -- Score: 249.6/270 (92.4%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yes. All EURC supply yield comes from overcollateralized borrower interest. EURC borrowers primarily post ETH, wstETH, WBTC, and other blue-chip collateral. Borrowing demand driven by: (1) EUR-denominated leverage, (2) FX carry trades (borrow EUR to hold USD assets), (3) operational liquidity. Pool has $71.7M supplied, $39.9M borrowed at 55.66% utilization. Supply APY 1.70%, 100% organic from borrower demand. No emissions required. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan EURC](https://aavescan.com/ethereum-v3/eurc), [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Negative yield or principal loss can occur in severe but plausible scenarios: (1) Bad debt from cascading liquidations during extreme volatility; (2) Smart contract exploit; (3) Oracle manipulation; (4) EURC issuer risk -- Circle can freeze user addresses (same issuer as USDC but smaller scale and less battle-tested); (5) EUR/USD FX risk for non-EUR denominated allocators. While reserves are 100% euro-denominated at regulated institutions (EUR 362.34M at Feb 2026 attestation), EURC is newer and less battle-tested than USDC. Umbrella Safety Module provides coverage. | 3 | 3 | Non-Improvable | [P1] [Circle Transparency](https://www.circle.com/transparency), [P1] [Umbrella Docs](https://aave.com/docs/aave-v3/umbrella), [P2] [ARFC EURC Core](https://governance.aave.com/t/arfc-add-eurc-to-aave-v3-core-instance/21837) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No protocol-level leverage or rehypothecation. User deposits remain in the Pool contract. Users can individually construct leveraged positions but that is user-level risk. Protocol itself maintains overcollateralized 1:1 backing. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | Yes. Two-slope interest rate model (Uoptimal 90%, base 0%, slope1 6%, slope2 50%). V3.3 bad debt verification prevents new bad debt post-liquidation. 100% close factor below 0.95 health factor ensures full debt coverage. Current utilization at 55.66% is well below the 90% kink. Risk Stewards actively manage EURC interest rate curves. | 9 | 9 | Non-Improvable (optimal) | [P2] [ARFC EURC Core](https://governance.aave.com/t/arfc-add-eurc-to-aave-v3-core-instance/21837), [P1] [Aave V3 Features](https://github.com/aave-dao/aave-v3-origin/blob/main/docs/3.3/Aave-v3.3-features.md) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent losses to EURC lenders. EURC pool is relatively new on Aave Core Instance (~mid-2025 onboarding). However, Aave V3 USDC/USDT lending (directly comparable variant -- same codebase, same risk mechanics, same chain) has 8+ year track record without depositor principal loss. Feb 2025: $210M liquidations processed, zero bad debt. Feb 2026: $429M record liquidations, zero bad debt. No comparable loss events on any Aave V3 stablecoin pool. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P3] [Aavescan EURC](https://aavescan.com/ethereum-v3/eurc) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Chaos Labs and LlamaRisk provide continuous quantitative risk analysis. EURC-specific parameters: LTV 75%, LT 78%, liquidation penalty 5%, reserve factor 10%. Supply cap 105M, borrow cap 96M, actively managed. Chaos Labs endorsed listing noting EURC's structural risk profile is similar to USDC's. Cap increases tracked via Risk Stewards governance. | 9 | 9 | Non-Improvable (optimal) | [P2] [ARFC EURC Core](https://governance.aave.com/t/arfc-add-eurc-to-aave-v3-core-instance/21837), [P2] [Cap Increase Jan 2026](https://governance.aave.com/t/chaos-labs-risk-stewards-interest-rate-curve-and-caps-adjustments-on-aave-v3-26-01-26/23940) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. EURC supply APY (~1.70%) is 100% organic from borrower demand. No emissions required. Borrowing demand driven by EUR-denominated leverage and FX carry trades (borrow EURC, hold USD-denominated assets for carry). Lower yield than USDC (~2.70%) reflects lower EUR interest rate environment and smaller market. Revenue sustainable without incentive dependency. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan EURC](https://aavescan.com/ethereum-v3/eurc), [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Under normal conditions, yes for in-protocol withdrawal. EURC withdrawal is direct from Pool contract based on available liquidity ($31.8M available at 55.66% utilization). However, converting EURC to USD or other assets involves thin DEX liquidity: Chaos Labs noted only 6M EURC can be sold for USDC with <5% slippage. For exits staying in EURC, pool has favorable utilization. For exits requiring conversion to non-EUR assets, larger positions face material slippage. | 3 | 9 | Non-Improvable | [P3] [Aavescan EURC](https://aavescan.com/ethereum-v3/eurc), [P2] [Chaos Labs EURC Assessment](https://governance.aave.com/t/chaos-labs-risk-stewards-increase-supply-and-borrow-caps-on-aave-v3-08-05-25/22828) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | EURC lending yield is pure interest from overcollateralized borrower demand -- no basis trade or funding rate dependency. However, EURC borrowing demand partially depends on EUR/USD carry trade dynamics. If EUR interest rates rise materially above USD rates, EURC borrow demand could decrease, compressing yield. EUR/USD FX peg dependency exists but EURC maintains robust 1:1 EUR peg via Circle's full reserve model. This spread/rate dependency contributes a minority of overall strategy risk. | 9 | 9 | Non-Improvable (optimal) | [P1] [Circle EURC](https://www.circle.com/eurc), [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | N/A -- Aave is a base-layer lending protocol where users deposit directly. No curator/allocator layer, no Public Allocator, no automated capital allocation mechanism. All deposits are user-initiated. | N/A | N/A | N/A | - |

**Protocol Mechanics Subtotal: 38.3/45 (85.2%)**
- 7 questions at score 9 = 63 points
- 2 questions at score 3 = 6 points
- 1 question N/A (ST-PM-10)
- Raw: 69/81, Weighted: (69/81) x 45 = 38.333 = 38.3

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | EURC pool: borrowers supply collateral from the full Aave Core Market asset set. Primary collateral against EURC borrows: ETH/WETH, wstETH, weETH, cbETH, rETH (ETH-correlated LSTs), WBTC, cbBTC (BTC-correlated), USDC, USDT, DAI, GHO (stablecoins). All are established large-cap assets. E-Mode categories provide risk tiering. Isolation Mode for newer/riskier assets with strict caps. EURC itself has LTV 75%, LT 78% with 5% liquidation penalty. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P2] [ARFC EURC Core](https://governance.aave.com/t/arfc-add-eurc-to-aave-v3-core-instance/21837) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | Major collateral assets (wstETH, weETH, cbETH, rETH) maintained pegs through Feb 2025 and Feb 2026 stress events. WBTC maintained peg. Stablecoin collateral (USDC, USDT, DAI) maintained pegs. EURC itself has maintained its EUR peg without any documented deviations >2% -- no stress events recorded for EURC on Aave. However, EURC's time on Aave Core Instance is limited (~mid-2025), reducing the stress-test data set. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P3] [DeFiLlama EURC](https://defillama.com/stablecoin/eurc) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | LST collaterals (wstETH, cbETH, rETH, weETH) have conservative LTVs accounting for slashing risk. Underlying protocols diversify operators: Lido (600+ operators), Rocket Pool (2,700+ operators). CAPO implementation for LSTs provides additional protection. Risk is immaterial to EURC lenders as it only affects borrower collateral value. | 9 | 9 | Non-Improvable (optimal) | [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters), [P1] [LlamaRisk CAPO Analysis](https://www.llamarisk.com/research/2025-03-07t22-20-26-000z) |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | EURC itself is a native Circle issuance on Ethereum (0x1abaea1f7c830bd89acc67ec4af516284b1bc33c) -- not bridged or wrapped. Per the methodology, natively issued stablecoins are excluded from "bridged/wrapped" definition. Primary collateral assets are also native to Ethereum. WBTC (wrapped BTC via BitGo custody) represents a portion of collateral but is not the majority. Estimated <30% bridged/wrapped when excluding native stablecoins and WETH. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan EURC](https://etherscan.io/address/0x1abaea1f7c830bd89acc67ec4af516284b1bc33c), [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |

**Collateral Subtotal: 45.0/45 (100.0%)**

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

**NOTE: All Infrastructure Counterparty scores are IDENTICAL to other Aave Ethereum V3 ratings. Same chain, same oracles, same infrastructure.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum (Tier-0 chain). Chainlink price feeds (Tier-0 oracle) for all asset pricing including EURC/USD feed (0x04F84020Fdf10d9ee64D1dcC2986EDF2F556DA11) with 16 oracle nodes, 24h heartbeat, 0.3% deviation threshold. No bridge dependencies for Ethereum deployment. No CEX custody. All critical infrastructure is Tier-0. | 9 | 9 | Non-Improvable (optimal) | [P1] [Chainlink EURC/USD Feed](https://data.chain.link/feeds/ethereum/mainnet/eurc-usd), [P0] [Etherscan EURC/USD Oracle](https://etherscan.io/address/0x04F84020Fdf10d9ee64D1dcC2986EDF2F556DA11) |
| ST-IC-02 | How redundant are oracle and bridge setups, and can oracle values be corrected under abnormal conditions? | Chainlink EURC/USD feed is a reference price feed with 16 oracle nodes (Deutsche Telekom MMS, Everstake, stake.fish, etc.). Classified as "Medium Market Risk" by Chainlink (compared to ETH/USD or USDC/USD which are higher tier). The feed can be updated/corrected under abnormal conditions. However, EURC/USD has a 24-hour heartbeat (vs 1-hour for major feeds like ETH/USD), meaning price staleness risk is higher during volatile FX periods. No bridge dependencies. | 9 | 9 | Non-Improvable (optimal) | [P1] [Chainlink EURC/USD Feed](https://data.chain.link/feeds/ethereum/mainnet/eurc-usd), [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | **Unknown.** Chainlink has enterprise certifications. Aave Labs and BGD Labs: no public SOC 2/ISO27001 documentation found. Chaos Labs: no public certification documentation. | 3 | 9 | **Source Missing** | [P1] [Aave Security](https://aave.com/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Highly resilient. Protocol operational through all major Ethereum events including The Merge (2022). Nov 2023: infrastructure responded within hours to critical vulnerability. Feb 2025: $210M liquidations processed smoothly. Feb 2026: $429M record liquidations processed with zero bad debt. Chainlink oracles functioned correctly throughout. EURC-specific: no infrastructure incidents since EURC onboarding. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain-level halts >30 min in 12+ months. Tier-0 reliability. | 9 | 9 | Non-Improvable (optimal) | Ethereum Tier-0 status, public knowledge |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Minor slashing events in Ethereum validator set; all compensated by underlying LST protocols. No impact on Aave EURC depositors. Conservative LTV parameters for LST collateral account for slashing risk. | 9 | 9 | Non-Improvable (optimal) | [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters) |
| ST-IC-07 | Are validators diverse geographically and by operator? | For LST collaterals backing EURC borrows: Lido (600+ operators, multi-region), Coinbase (institutional), Rocket Pool (2,700+ operators globally), Etherfi (diversified DVT). Ethereum validator set is highly distributed (>900K validators). Chainlink EURC/USD oracle network includes 16 geographically diverse operators. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lido Operators](https://lido.fi/ethereum), [P1] [Chainlink EURC/USD Feed](https://data.chain.link/feeds/ethereum/mainnet/eurc-usd) |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No permanent blocks from single failure. Withdrawals are permissionless via Pool contract. Oracle failure may trigger Guardian pause but does not block withdrawal of available liquidity. Chainlink redundancy prevents single oracle failure. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |

**Infrastructure Counterparty Subtotal: 41.25/45 (91.7%)**
- 7 questions at score 9 = 63 points
- 1 question at score 3 = 3 points
- Raw: 66/72, Weighted: (66/72) x 45 = 41.25

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | None. User EURC deposits remain in Aave Pool V3 contract. No external deployment of user collateral. Flash loans are atomic (same-block return). Liquidators operate permissionlessly but do not route user deposits externally. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Yes. Protocol fees publicly visible on-chain. DAO treasury managed by Karpatkey with transparent reporting. Fee dispute regarding ~$10M/year CowSwap interface fees: highlighted governance tension but all arrangements are ultimately visible on-chain. Feb 2026: Aave Labs proposed directing 100% of Aave-branded revenue to DAO treasury. | 9 | 9 | Non-Improvable (optimal) | [P2] [DAO Financial Reports](https://governance.aave.com/t/aave-dao-financial-reports-financial-metrics/5575) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. Supply cap (105M EURC) and borrow cap (96M EURC) enforced on-chain. Caps actively managed by Chaos Labs Risk Stewards -- increased from 70M to 105M supply cap in January 2026 after 95% utilization. Per-counterparty exposure limits via isolation mode and E-Mode categories. | 9 | 9 | Non-Improvable (optimal) | [P2] [Cap Increase Jan 2026](https://governance.aave.com/t/chaos-labs-risk-stewards-interest-rate-curve-and-caps-adjustments-on-aave-v3-26-01-26/23940), [P2] [ARFC EURC Core](https://governance.aave.com/t/arfc-add-eurc-to-aave-v3-core-instance/21837) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Instant for available liquidity. EURC withdrawal is permissionless from Pool contract. $31.8M currently available (55.66% utilization, more favorable than USDC's 82.46%). Rate model incentivizes rapid repayment. However, converting large EURC positions to USD stablecoins faces thin DEX liquidity constraints (~6M EURC sellable with <5% slippage per Chaos Labs). | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan EURC](https://aavescan.com/ethereum-v3/eurc), [P2] [Chaos Labs EURC Assessment](https://governance.aave.com/t/chaos-labs-risk-stewards-increase-supply-and-borrow-caps-on-aave-v3-08-05-25/22828) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | N/A for core EURC lending (no external custody by Aave). Circle as EURC issuer is publicly known. For collateral: underlying operators fully disclosed (Lido, Coinbase, Rocket Pool, Etherfi). Chainlink oracle operators disclosed. Treasury manager Karpatkey disclosed. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |

**Protocol Counterparty Subtotal: 45.0/45 (100.0%)**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | All EURC withdrawals are permissionless via Pool V3 contract based on available liquidity. Guardians can pause in emergency (5-of-9 multisig required) but pause is protocol-wide, not address-specific. No selective blocking capability. Users interact directly with on-chain contracts. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Under normal conditions, mostly yes. $71.7M supplied, $39.9M borrowed. Available liquidity = $31.8M at 55.66% utilization, representing ~44.3% of supplied TVL -- more favorable ratio than USDC (17.5%). At current utilization, >10% of TVL can be redeemed immediately. Rate model incentivizes repayment to restore liquidity. However, total pool size is much smaller than USDC ($71.7M vs $3.34B), meaning absolute available liquidity is lower. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan EURC](https://aavescan.com/ethereum-v3/eurc) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | EURC pool is relatively new (~mid-2025 onboarding). No withdrawal delays, queues, or freezes reported for EURC specifically. The broader Aave protocol has a clean record: Nov 2023 temporary asset freezes during vulnerability patch (resolved within days) affected other pools. >95% of withdrawals complete within reasonable timeframe over the pool's operational history. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan EURC](https://aavescan.com/ethereum-v3/eurc), [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Supply cap (105M EURC) is above current supply (62.2M = 59.2% of cap). Previously, supply cap was hit at 100% utilization (Aug 2025), triggering Chaos Labs to increase caps. Risk Stewards actively manage. Currently no cap-related withdrawal restrictions. Interest rate model penalizes high utilization with higher borrow rates. | 9 | 9 | Non-Improvable (optimal) | [P2] [Cap Increase Jan 2026](https://governance.aave.com/t/chaos-labs-risk-stewards-interest-rate-curve-and-caps-adjustments-on-aave-v3-26-01-26/23940), [P3] [Aavescan EURC](https://aavescan.com/ethereum-v3/eurc) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | **Limited stress data for EURC specifically.** EURC pool was not operational during major stress events (Feb 2025, March 2023 SVB). The broader Aave platform performed well during Feb 2026 stress ($429M liquidations, $1.7B stablecoin withdrawals). However, EURC-specific stress behavior is untested. Per the framework, untested protocols should score Mid (3). EURC's thin secondary market ($6.35M DEX liquidity) could exacerbate exit challenges during stress if borrowers need to repay and EURC liquidity dries up. | 3 | 3 | Non-Improvable | [P3] [Aavescan EURC](https://aavescan.com/ethereum-v3/eurc), [P3] [GeckoTerminal EURC/USDC](https://www.geckoterminal.com/eth/pools/0x95dbb3c7546f22bce375900abfdd64a4e5bd73d6) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. EURC withdrawals based on available pool liquidity only. No lockups, vesting, or unstaking delays. Instant withdrawal if liquidity available. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary EURC redemption through Pool contract is always available (subject to pool liquidity). aEthEURC tokens can technically be transferred but the primary exit mechanism is direct protocol redemption. However, if users need to convert EURC to USD stablecoins after withdrawal, they are dependent on thin secondary market liquidity (~$6.35M in Uniswap pools). Primary in-protocol exit is sound; post-exit conversion is constrained. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P3] [GeckoTerminal EURC/USDC](https://www.geckoterminal.com/eth/pools/0x95dbb3c7546f22bce375900abfdd64a4e5bd73d6) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | **Thin secondary market.** EURC market cap ~$450M -- significantly smaller than USDC (~$60B). Uniswap EURC/USDC pool has ~$6.35M liquidity. Total Ethereum EURC DEX liquidity likely under $15M across all venues. Chaos Labs estimated 6M EURC sellable for USDC with <5% slippage. For the $71.7M pool, this means less than ~8.4% of TVL can be absorbed by secondary markets with low impact. aEthEURC is directly 1:1 redeemable from Pool. Below the ~10% threshold for Low Risk. Roughly in the 3-10% range = Mid (3). | 3 | 3 | Non-Improvable | [P3] [GeckoTerminal EURC/USDC](https://www.geckoterminal.com/eth/pools/0x95dbb3c7546f22bce375900abfdd64a4e5bd73d6), [P2] [Chaos Labs EURC Assessment](https://governance.aave.com/t/chaos-labs-risk-stewards-increase-supply-and-borrow-caps-on-aave-v3-08-05-25/22828) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | **Moderate, with EURC-specific constraints.** At 55.66% utilization, EURC pool has healthier buffer than USDC (82.46%). A mass exit would cause utilization to spike, rates to increase dramatically (Slope2 at 50%), and borrowers would repay, restoring liquidity. However, EURC's thin secondary market means borrowers may face difficulty sourcing EURC to repay during a bank-run (circular liquidity problem). Supply concentration risk: top supplier holds ~30% of supply. V3.3 bad debt verification prevents cascading. Bank-run risk is inherent to lending but slightly elevated for a thin-market asset like EURC. | 3 | 3 | Non-Improvable | [P3] [Aavescan EURC](https://aavescan.com/ethereum-v3/eurc), [P2] [Chaos Labs EURC Assessment](https://governance.aave.com/t/chaos-labs-risk-stewards-increase-supply-and-borrow-caps-on-aave-v3-08-05-25/22828) |

**Liquidity Subtotal: 35.0/45 (77.8%)**
- 6 questions at score 9 = 54 points
- 3 questions at score 3 = 9 points
- Raw: 63/81, Weighted: (63/81) x 45 = 35.0

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | aEthEURC maintains 1:1 with underlying EURC by design (interest-bearing token, not a traded peg). No peg deviation possible as aEthEURC represents a claim on Pool liquidity plus accrued interest. The "peg" is architectural, not market-dependent. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P0] [Etherscan aEthEURC](https://etherscan.io/address/0xAA6e91C82942aeAE040303Bf96c15a6dBcB82CA0) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Low for EURC lenders from crypto market moves. Overcollateralized design protects suppliers. Borrowers face liquidation risk, not lenders. However, EURC adds EUR/USD FX exposure: EUR/USD has ~0.23% daily volatility with typical daily ranges of 50-100 pips. A 10% EUR/USD move (plausible in extreme stress) would affect dollar-denominated value but not EURC-denominated principal. For EUR-denominated allocators, directional exposure is minimal. For USD-denominated allocators, FX risk is structural but bounded. Score reflects stablecoin lending's inherent low directional exposure. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Interest rate model: Uoptimal 90%, base 0%, slope1 6%, slope2 50%. Current utilization at 55.66% is well below the 90% kink. Supply cap hit 100% in Aug 2025, prompting cap increases -- demonstrates model responsiveness. No history of prolonged >=95% utilization for EURC. Rate curves become steep as utilization approaches critical levels. However, EURC is newer with less stress-test data than USDC/USDT. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aavescan EURC](https://aavescan.com/ethereum-v3/eurc), [P2] [ARFC EURC Core](https://governance.aave.com/t/arfc-add-eurc-to-aave-v3-core-instance/21837) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Chaos Labs and LlamaRisk provided risk assessments for EURC onboarding, including analysis of on-chain liquidity, user behavior, and liquidation risk. Chaos Labs noted EURC's structural risk profile is similar to USDC's. Multiple real-world Aave stress tests for the platform (Feb 2025, Feb 2026), though EURC-specific pool was not under stress during those events. Formal verification by Certora validates invariants. | 9 | 9 | Non-Improvable (optimal) | [P2] [ARFC EURC Core](https://governance.aave.com/t/arfc-add-eurc-to-aave-v3-core-instance/21837), [P2] [Chaos Labs EURC Assessment](https://governance.aave.com/t/chaos-labs-risk-stewards-increase-supply-and-borrow-caps-on-aave-v3-08-05-25/22828) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | For EURC borrowers: yes -- if collateral value drops, borrowers get liquidated (this protects EURC lenders). For EURC lenders/suppliers: no, protected by overcollateralization. Stablecoin lending advantage: EURC is borrowed against volatile collateral, so collateral decline triggers protective liquidations. Feb 2026: $429M total Aave liquidations with zero bad debt (though EURC pool was not a material contributor given its smaller size). | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P1] [Aave V3 Features](https://github.com/aave-dao/aave-v3-origin/blob/main/docs/3.3/Aave-v3.3-features.md) |

**Market Subtotal: 45.0/45 (100.0%)**

---

### **Strategy Total: 249.6/270 (92.4%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 38.3 | 45 | 85.2% |
| Collateral | 45.0 | 45 | 100.0% |
| Infra Counterparty | 41.25 | 45 | 91.7% |
| Protocol Counterparty | 45.0 | 45 | 100.0% |
| Liquidity | 35.0 | 45 | 77.8% |
| Market | 45.0 | 45 | 100.0% |
| **Strategy Total** | **249.6** | **270** | **92.4%** |

**Precise Strategy calculation:**
- Protocol Mechanics: (69/81) x 45 = 38.333
- Collateral: (36/36) x 45 = 45.0
- Infra Counterparty: (66/72) x 45 = 41.25
- Protocol Counterparty: (45/45) x 45 = 45.0
- Liquidity: (63/81) x 45 = 35.0
- Market: (45/45) x 45 = 45.0
- **Total: 38.333 + 45.0 + 41.25 + 45.0 + 35.0 + 45.0 = 249.583 = 249.6**

---

### OPERATIONS (30% Weight) -- Score: 256.0/270 (94.8%)

**NOTE: All Operations scores are IDENTICAL to other Aave Ethereum V3 Core Market ratings. Same governance, same team, same docs, same treasury, same backstop.**

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | On-chain DAO governance via AAVE, stkAAVE, aAAVE token voting. Structured proposal process: Temp Check (Snapshot) -> ARFC (forum) -> AIP (on-chain vote). Cross-chain voting via storage proofs. Risk Stewards (Chaos Labs) handle parameter adjustments within governance-approved bounds. Two 5-of-9 Guardian multisigs provide emergency controls. No single entity can unilaterally change core fund-custody logic. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [Aave Governance Forum](https://governance.aave.com/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | Moderate concentration typical of large DAOs. However, robust checks: two 5-of-9 Guardian multisigs with diverse independent membership, Risk Steward system distributing parameter control, structured proposal process requiring community discussion. Recent governance activity demonstrates active participation (Feb 2026 "Aave Will Win" proposal generated extensive debate). | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [Governance Forum Activity](https://governance.aave.com/) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. 1-day standard timelock, 7-day for critical changes. Two Guardian multisigs (5-of-9 each) with veto powers. Structured proposal process (Temp Check -> ARFC -> AIP). Certora reviews all governance proposals for security. No timelock reductions in recent history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A -- Aave has no "strategy manager" in the vault sense. Risk providers (Chaos Labs, LlamaRisk) can be changed via governance without any impact on user withdrawals. EURC pool withdrawals are always permissionless and independent of any service provider changes. | N/A | N/A | N/A | - |

**Governance Subtotal: 67.5/67.5 (100.0%)**
- 3 questions at score 9 = 27 points
- 1 question N/A (O-G-04)
- Raw: 27/27, Weighted: (27/27) x 67.5 = 67.5

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Founder: Stani Kulechov (Finnish, law degree, publicly identified since 2017). Aave Labs (Aave SAGL, Swiss entity). BGD Labs: Ernesto Boado (former Aave CTO) + team (127 GitHub repositories). Key contributors publicly identified and active in governance forums. | 9 | 9 | Non-Improvable (optimal) | [P3] [Crunchbase](https://www.crunchbase.com/organization/ethlend), [P1] [BGD Labs GitHub](https://github.com/bgd-labs) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Multiple independent development teams: Aave Labs, BGD Labs, and other contributors. BGD Labs alone has 127 repositories. Certora provides formal verification independently. Chaos Labs handles risk independently. Large ecosystem of service providers. | 9 | 9 | Non-Improvable (optimal) | [P1] [BGD Labs GitHub](https://github.com/bgd-labs), [P2] [BGD Phase 4 Recap](https://governance.aave.com/t/bgd-aave-bgd-labs-phase-4-recap/21667) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Aave SAGL (Swiss entity, Zug). Aave Labs based in London, UK. DAO structure with decentralized governance. Multiple jurisdictional presence. Clear legal entity mapping to operational responsibilities. | 9 | 9 | Non-Improvable (optimal) | [P3] [Tracxn](https://tracxn.com/d/companies/aave/__JiXfiPZKVkx7021dCR937XH3M5d2vj-Cy3z3dnIPJ00) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | **CLEARED.** SEC closed 4-year investigation December 16, 2025 without enforcement action. No charges, fines, or further action. No ongoing or past material enforcement actions in major jurisdictions. | 9 | 9 | Non-Improvable (optimal) | [P4] [Yahoo Finance](https://finance.yahoo.com/news/sec-closes-4-long-investigation-091715487.html), [P4] [Unchained Crypto](https://unchainedcrypto.com/sec-ends-four-year-probe-into-aave/) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Yes. Nov 2023: demonstrated rapid response (pools secured within hours). Feb 2026: Chaos Labs Risk Stewards adjusted parameters in real-time during market crash. March 2026: CAPO incident response included post-mortem and reimbursement plan within days. BGD Labs provides continuous monitoring. Guardian multisigs on standby. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. Active governance forum with regular updates. Nov 2023 vulnerability resolved within hours. Feb 2026 stress: Chaos Labs published retrospective analysis. Regular development updates from BGD Labs and Aave Labs. Discord and community channels active. | 9 | 9 | Non-Improvable (optimal) | [P2] [AL Development Update](https://governance.aave.com/t/al-development-update-november-2025/23484) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. $29.5M raised from 41 investors including Standard Crypto, Blockchain Coinvestors, ParaFi, Framework Ventures, Three Arrows Capital (pre-collapse). Transparent cap table. Service providers (Chaos Labs, LlamaRisk, Karpatkey, BGD Labs) all publicly disclosed. | 9 | 9 | Non-Improvable (optimal) | [P3] [Tracxn](https://tracxn.com/d/companies/aave/__JiXfiPZKVkx7021dCR937XH3M5d2vj-Cy3z3dnIPJ00/funding-and-investors) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | **Governance tension exists.** Dec 2025: DAO-Labs conflict over ~$10M/year CowSwap interface fees redirected from DAO treasury. Feb 2026: Aave Labs proposed "Aave Will Win" plan to send 100% revenue to DAO in exchange for $25M funding + 75,000 AAVE tokens. Debate ongoing. Conflict represents a governance health issue but has not impacted user fund safety. | 3 | 9 | **Improvable** | [P4] [CoinDesk Dec 2025](https://www.coindesk.com/tech/2025/12/15/aave-dao-pushes-back-as-interface-fees-shift-away-from-treasury), [P4] [CoinDesk Feb 2026](https://www.coindesk.com/business/2026/02/12/aave-labs-proposes-aave-will-win-plan-to-send-100-of-product-revenue-to-dao) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | No. 8+ year track record without user fund losses. Nov 2023 vulnerability patched before exploitation. Feb 2025: $210M liquidations without bad debt. Feb 2026: $429M record liquidations without bad debt. March 2026: CAPO incident caused wstETH collateral losses but DAO committed to 100% reimbursement. Clean operational history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |

**Team & Legal Subtotal: 62.5/67.5 (92.6%)**
- 8 questions at score 9 = 72 points
- 1 question at score 3 = 3 points
- Raw: 75/81, Weighted: (75/81) x 67.5 = 62.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive documentation covering V3 architecture, smart contracts, risk parameters, governance, interest rate models. Updated through V3.6 (Nov 2025). Risks page explicitly covers liquidation mechanics, oracle risks, smart contract risks. EURC-specific parameters documented in governance proposals. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Docs](https://aave.com/docs/aave-v3/overview), [P1] [Risks](https://aave.com/docs/resources/risks) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Detailed documentation: health factor mechanics, liquidation process, bad debt scenarios, interest rate models. V3.3 bad debt features documented. Loss conditions clearly explained with specific scenarios. EURC-specific parameters (LTV 75%, LT 78%, 5% liquidation penalty) documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [Health Factor & Liquidations](https://aave.com/help/borrowing/liquidations), [P1] [Risks](https://aave.com/docs/resources/risks) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Pool V3: 0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2. PoolAddressesProvider: 0x2f39d218133AFaB8F2B819B1066c7E434Ad94E9e. aEthEURC: 0xAA6e91C82942aeAE040303Bf96c15a6dBcB82CA0. EURC Token: 0x1abaea1f7c830bd89acc67ec4af516284b1bc33c. All verified on Etherscan. BGD Address Book GitHub repo provides canonical registry. | 9 | 9 | Non-Improvable (optimal) | [P1] [Smart Contracts Docs](https://aave.com/docs/aave-v3/smart-contracts), [P1] [BGD Address Book](https://github.com/bgd-labs/aave-address-book) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Guardian roles (Protocol and Governance Emergency Guardians), timelock durations (1-day standard, 7-day critical), Risk Steward permissions and bounds, proposal process all documented. All changes visible on-chain and in governance forum. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full on-chain transparency. All EURC pool balances verifiable via Pool V3 contract. aEthEURC supply verifiable on Etherscan. DeFiLlama tracking. Protocol Data Provider contract enables programmatic verification of all reserve states including borrows (proof-of-liabilities). | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P3] [DeFiLlama Aave V3](https://defillama.com/protocol/aave-v3) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. All core contracts verified on Etherscan: Pool V3, PoolConfigurator, PoolAddressesProvider, aEthEURC, variableDebtEURC, ProtocolDataProvider. Full source code readable and verified. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2#code) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Yes. Umbrella Safety Module launched June 2025 with ~$263M in staked assets (93.3M USDC, 120.8M USDT, 35.2K WETH, 14.4M GHO per LlamaRisk Dec 2025). Automated slashing mechanism. Clear published activation rules -- automated, not discretionary. Note: EURC is not currently a staked asset in Umbrella, but the system provides cross-asset coverage. | 9 | 9 | Non-Improvable (optimal) | [P1] [Umbrella Docs](https://aave.com/docs/aave-v3/umbrella), [P2] [LlamaRisk Umbrella Coverage](https://governance.aave.com/t/llamarisk-insights-umbrella-coverage-principles-and-slashing-logic/23527) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | **Modest relative to overall scale.** Umbrella: ~$263M (automated backstop). DAO Treasury: ~$125M. Combined ~$388M vs $34.5B Ethereum TVL = ~1.1%. Below 5% threshold for Low Risk; within 1-5% range = Mid Risk. DAO Treasury requires governance vote to deploy for user losses. For EURC pool specifically: $388M backstop vs $71.7M EURC TVL = ~541%, but the backstop is shared across all Aave markets. | 3 | 9 | **Improvable** | [P2] [DAO Funding Insights](https://governance.aave.com/t/aave-dao-funding-insights/24192), [P2] [LlamaRisk Umbrella Coverage](https://governance.aave.com/t/llamarisk-insights-umbrella-coverage-principles-and-slashing-logic/23527) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. DAO Treasury ~$125M. 2026 projected budget ~$164.4M (includes $75M Ahab growth ceiling). Protocol generated $885M in fees in 2025, estimated ~$143M revenue for 2026. $50M/year permanent AAVE buyback program approved. Revenue broadly covers expenses. Runway >24 months. | 9 | 9 | Non-Improvable (optimal) | [P2] [DAO Funding Insights](https://governance.aave.com/t/aave-dao-funding-insights/24192), [P3] [Coinlaw Statistics](https://coinlaw.io/aave-statistics/) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Highly resilient across multiple severe stress events. Survived 2022 bear market (FTX collapse, Terra/Luna, SVB crisis). Feb 2025: $210M liquidations, zero bad debt. Feb 2026: record $429M liquidations, zero bad debt. Ethereum TVL recovered to $34.5B. Protocol has demonstrated resilience across every major market stress event over 8+ years. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P3] [DeFiLlama Aave V3](https://defillama.com/protocol/aave-v3) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Smart contracts are permissionless and non-custodial. EURC withdrawals always available via direct Pool contract interaction based on available liquidity. Governance via on-chain voting (no off-chain dependency). Multiple independent development teams provide redundancy. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |

**Financial Resilience Subtotal: 58.5/67.5 (86.7%)**
- 4 questions at score 9 = 36, 1 question at score 3 = 3
- Raw: 39/45, Weighted: (39/45) x 67.5 = 58.5

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 99 | 99 | 180.0 | 180 | 100.0% |
| | Key Management (7 of 8 Q scored) | 57 | 63 | 162.9 | 180 | 90.5% |
| | **Security Subtotal** | | | **342.9** | **360** | **95.2%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 69 | 81 | 38.3 | 45 | 85.2% |
| | Collateral (4 Q) | 36 | 36 | 45.0 | 45 | 100.0% |
| | Infra Counterparty (8 Q) | 66 | 72 | 41.25 | 45 | 91.7% |
| | Protocol Counterparty (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity (9 Q) | 63 | 81 | 35.0 | 45 | 77.8% |
| | Market (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | **Strategy Subtotal** | | | **249.6** | **270** | **92.4%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 75 | 81 | 62.5 | 67.5 | 92.6% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 39 | 45 | 58.5 | 67.5 | 86.7% |
| | **Operations Subtotal** | | | **256.0** | **270** | **94.8%** |
| **TOTAL** | | | | **848.5** | **900** | **94.3%** |

---

