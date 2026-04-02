# Aave - USDe (Ethereum Core Market) Risk Rating

**Rating Date**: 2026-04-01
**Final Grade**: BB
**Total Score**: 769.2/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-beta

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 342.9/360 (95.2%)

**NOTE: All Security scores are IDENTICAL to other Aave Ethereum V3 Core Market ratings (WETH, USDC, USDT, WBTC, wstETH, weETH, cbBTC). Same smart contracts, same governance, same key management.**

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. 30+ audits from Tier-0/1 firms: OpenZeppelin (2021), Trail of Bits (2022), Sigma Prime (2022, 2023), PeckShield (2022), ABDK (2022), Certora (continuous formal verification through V3.6), MixBytes (V3.1+), Pashov (V3.2+), Sherlock (V3.3), Oxorio (V3.2-V3.3). Latest V3.6 audits include Certora and StErMi. All reports public on GitHub. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [GitHub Audits](https://github.com/aave/aave-v3-core/tree/master/audits), [P1] [aave-v3-origin repo](https://github.com/aave-dao/aave-v3-origin) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | V3.4 (June 2025): Certora (Tier-0, formal verification), StErMi. V3.3 (Jan 2025): Certora (Tier-0), Sherlock (Tier-0), Oxorio, StErMi. Multiple Tier-0 auditors on latest versions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [Certora Reports](https://www.certora.com/reports/aave-v3-risk-steward) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Every major version (V3.0 through V3.6) has been audited. Umbrella Safety Module (June 2025), GHO (7 audits), Governance V3 all received dedicated audits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Security](https://aave.com/security), [P1] [GitHub aave-v3-origin](https://github.com/aave-dao/aave-v3-origin) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. November 2023 critical vulnerability (stable rate bug) patched immediately via emergency governance action. All findings tracked with remediation. Certora formal verification validates invariants. Sherlock contest on V3.3 validated remediation. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P1] [Aave Security](https://aave.com/security) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Upgradeable via transparent proxy pattern managed through PoolAddressesProvider. Upgrades require full DAO governance vote (AAVE/stkAAVE/aAAVE token voting with quorum) followed by 1-day standard timelock or 7-day critical timelock. Two 5-of-9 Guardian multisigs can veto malicious proposals. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No user fund losses in protocol history. Nov 2023: Critical stable rate vulnerability patched before exploitation. Aug 2024: Periphery contract incident ($56K tip jar -- not user deposits). Feb 2025: $210M liquidations processed with zero bad debt. Feb 2026: $429M record liquidations with zero bad debt. March 2026: CAPO oracle misconfiguration caused $27.78M wstETH liquidations but USDe suppliers were completely unaffected and DAO committed to 100% reimbursement of affected wstETH positions. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Post-Mortem](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P2] [CAPO Post-Mortem](https://governance.aave.com/t/post-mortem-exchange-rate-misallignment-on-wsteth-core-and-prime-instances/24269) |
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
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user USDe deposits held in Pool V3 contract (0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2). Permissionless supply/withdraw via smart contract. aEthUSDe tokens represent user positions. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation: Pool V3 contract holds all user funds. DAO treasury managed separately by Karpatkey with independent wallet structure. No co-mingling of user deposits with treasury operations. | 9 | 9 | Non-Improvable (optimal) | [P2] [DAO Financial Reports](https://governance.aave.com/t/aave-dao-financial-reports-financial-metrics/5575), [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- Aave is a lending protocol, not a vault. Users deposit assets directly to pools. No external protocol routing of user funds. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | **Partial.** November 2023 incident demonstrated rapid emergency response (pools secured within hours). Feb 2026 WETH utilization spike handled through automated Slope2 Oracle + Chaos Labs Risk Steward intervention. However, no comprehensive public playbook for key rotation or signer replacement procedures is documented. | 3 | 9 | **Improvable** | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335) |

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

### STRATEGY (30% Weight) -- Score: 170.3/270 (63.1%)

**NOTE: Strategy scores differ significantly from other Aave pools due to USDe's synthetic dollar risk profile. USDe is backed by Ethena's delta-neutral derivative positions, NOT by traditional fiat reserves like USDC or institutional custody like WBTC.**

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | USDe supply yield comes from overcollateralized borrower interest. The displayed ~4.06% APY includes ~3.11% from Aave Merit/Merkl incentives. The organic supply APR is approximately 0.95%. Borrowing demand for USDe is partially driven by looping strategies (borrow USDe to stake as sUSDe for Ethena yield). Yield is aligned with the lending mandate -- suppliers earn from borrower interest. | 3 | 3 | Non-Improvable | [P3] [Aave App USDe Reserve](https://app.aave.com/reserve-overview/?underlyingAsset=0x4c9edd5852cd905f086c759e8383e09bff1e68b3&marketName=proto_mainnet_v3), [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Principal loss can occur in non-tail or recurring conditions: (1) USDe depeg if Ethena's funding rates go persistently negative, destabilizing the delta-neutral hedge and reducing USDe's backing below $1; (2) OES custodian failure (Copper, Ceffu, Cobo, Anchorage Digital, Kraken) could render USDe partially unbacked; (3) CEX counterparty default (Binance, Bybit, OKX, Deribit, Bitget exposure); (4) Ethena operational failure. These are NOT rare tail events -- funding rate inversions are recurring conditions in crypto markets. Structural fragility is fundamentally different from USDC (fiat reserves) or WBTC (BTC custody). | 1 | 1 | Non-Improvable | [P1] [Ethena Docs Risk](https://docs.ethena.fi/solution-overview/risks), [P2] [Ethena sUSDe Rating CCC+/600.0](https://stakingrewards.com) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No protocol-level leverage or rehypothecation at the Aave level. User deposits remain in the Pool contract. Users can individually construct leveraged positions. Protocol itself maintains overcollateralized lending. However, the underlying USDe asset is itself a leveraged product (delta-neutral derivative positions). | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | Yes. Two-slope interest rate model with Slope2 Risk Oracle incentivizes repayment at high utilization. V3.3 bad debt verification prevents new bad debt post-liquidation. USDe has 0% LTV for new borrows (cannot be used as collateral), with existing positions having a 75% liquidation threshold and 8.5% liquidation penalty. These conservative parameters reflect USDe's risk profile. | 9 | 9 | Non-Improvable (optimal) | [P2] [Chaos Labs Slope2 Oracle](https://chaoslabs.xyz/posts/introducing-the-aave-slope2-risk-oracle), [P3] [Aave App USDe Reserve](https://app.aave.com/reserve-overview/?underlyingAsset=0x4c9edd5852cd905f086c759e8383e09bff1e68b3&marketName=proto_mainnet_v3) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | USDe has experienced brief depegs during market stress events. Ethena's delta-neutral mechanism depends on funding rates that HAVE gone negative historically. The February 2025 Bybit hack tested Ethena's resilience -- $123M in redemptions processed within 24 hours, protocol survived, but the stress event demonstrated the fragility of CEX counterparty dependency. No permanent losses to Aave USDe suppliers to date, but the strategy variant (lending a synthetic dollar backed by a carry trade) has well-documented episodes of stress. Score Mid (3) as one historical permanent-loss equivalent event (brief depegs) below 0.5% with clear market-wide drivers. | 3 | 3 | Non-Improvable | [P1] [Ethena Docs Risk](https://docs.ethena.fi/solution-overview/risks), [P4] [Bybit Hack Ethena Impact](https://rekt.news) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Chaos Labs and LlamaRisk provide continuous quantitative risk analysis. USDe-specific parameters: LTV 0% (disabled for new borrows), liquidation threshold 75%, supply cap 2.70B. E-Mode categories and Isolation Mode documented with clear risk tiering. Risk framework includes USDe-specific considerations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters), [P1] [Risks Documentation](https://aave.com/docs/resources/risks) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | The organic supply APR (~0.95%) from borrower interest is sustainable but minimal. The displayed ~4.06% APY includes Aave Merit/Merkl incentives (~3.11% of the total), meaning approximately 77% of the displayed yield is incentive-driven (above the 70% threshold for High risk). Borrowing demand for USDe is partially reflexive -- driven by sUSDe looping strategies that depend on Ethena's own incentive structure and funding rate carry. Without incentives, yield would be ~1% APR. Score High (1) as yield is predominantly incentive-driven (above 70%) and would become near-zero without incentive programs. | 1 | 1 | Non-Improvable | [P3] [Aave App USDe Reserve](https://app.aave.com/reserve-overview/?underlyingAsset=0x4c9edd5852cd905f086c759e8383e09bff1e68b3&marketName=proto_mainnet_v3) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes under normal conditions. USDe withdrawal is direct from Pool contract based on available liquidity ($541M available at 54.26% utilization). At current utilization, ~45.74% of TVL is available for immediate withdrawal -- significantly better than USDC (17.5%). USDe itself can be redeemed through Ethena's mechanism but this adds a layer of counterparty and operational risk. During stress, USDe secondary market liquidity could thin significantly. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aave App USDe Reserve](https://app.aave.com/reserve-overview/?underlyingAsset=0x4c9edd5852cd905f086c759e8383e09bff1e68b3&marketName=proto_mainnet_v3) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Yes. USDe IS fundamentally a carry/peg trade. Its value depends on maintaining a 1:1 USD peg backed by delta-neutral positions that rely on perpetual futures funding rates. When funding rates invert (which is a recurring condition in crypto markets, not a tail event), USDe's backing mechanism is directly threatened. USDe suppliers on Aave are lending an asset whose fundamental value depends on an invertible funding rate. The lending yield itself (borrower interest) is not directly a carry trade, but the underlying asset's viability is. Score High (1) as the strategy is primarily dependent on an asset that is a carry trade with yield driven by invertible funding rates above 70%. | 1 | 1 | Non-Improvable | [P1] [Ethena Docs Risk](https://docs.ethena.fi/solution-overview/risks), [P1] [Ethena Funding Rate Data](https://app.ethena.fi/dashboards/hedging) |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | N/A -- Aave is a base-layer lending protocol where users deposit directly. No curator/allocator layer. All allocation changes are user-initiated. | N/A | N/A | N/A | - |

**Protocol Mechanics Subtotal: 25.0/45 (55.6%)**
- 4 questions at score 9 = 36 points
- 2 questions at score 3 = 6 points
- 3 questions at score 1 = 3 points
- 1 question N/A (ST-PM-10)
- Raw: 45/81, Weighted: (45/81) x 45 = 25.0

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | USDe pool: borrowers supply collateral from the full Aave Core Market asset set. Primary collateral against USDe borrows: ETH/WETH, wstETH, weETH, WBTC, cbBTC, USDC, USDT, other established assets. All are established large-cap assets with E-Mode categories providing risk tiering. Isolation Mode for newer/riskier assets with strict caps. Collateral quality is high at the Aave level. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P1] [Parameters Dashboard](https://aave.com/docs/resources/parameters) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | USDe itself (the asset being supplied) has experienced brief depegs during market stress. USDe's backing can deteriorate rapidly if Ethena's funding rates go negative or an OES custodian fails. Unlike USDC (US Treasury-backed reserves) or WBTC (BTC in custody), USDe's collateral backing is actively managed derivative positions with off-chain custody. The asset has demonstrated >2% deviations during stress periods. Score High (1) as the supplied asset has shown meaningful depeg risk. | 1 | 1 | Non-Improvable | [P1] [Ethena Docs Risk](https://docs.ethena.fi/solution-overview/risks), [P3] [CoinGecko USDe Price History](https://www.coingecko.com/en/coins/ethena-usde) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- USDe is not a staking-based collateral. The underlying asset is a synthetic dollar, not an LST. | N/A | N/A | N/A | - |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | The USDe pool is 100% USDe -- a synthetic dollar that is neither bridged nor wrapped in the traditional sense. However, USDe's backing relies on off-chain OES custody arrangements (Copper, Ceffu, Cobo, Anchorage Digital, Kraken) which create counterparty dependencies analogous to wrapped asset risk. USDe is not a natively issued stablecoin like USDC. Per the methodology, USDe does not fit the bridged/wrapped definition (no bridge contract), but its OES-backed structure creates similar custody risk. Score as Low (9) per strict methodology definition -- USDe is not bridged or wrapped. | 9 | 9 | Non-Improvable (optimal) | [P1] [Ethena Docs Architecture](https://docs.ethena.fi/solution-overview/usde-overview) |

**Collateral Subtotal: 31.7/45 (70.4%)**
- 2 questions at score 9 = 18 points
- 1 question at score 1 = 1 point
- 1 question N/A (ST-C-03)
- Raw: 19/27, Weighted: (19/27) x 45 = 31.667 = 31.7

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

**NOTE: Infrastructure scores are identical to other Aave Ethereum V3 Core Market ratings. Same chain, same infrastructure.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum (Tier-0 chain). Chainlink price feeds (Tier-0 oracle) for USDe/USD pricing with CAPO validation. No bridge dependencies for Ethereum deployment. No CEX custody at Aave level (though USDe itself depends on CEX counterparties). All critical Aave infrastructure is Tier-0. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P0] [Chainlink Data](https://data.chain.link/) |
| ST-IC-02 | How redundant are oracle and bridge setups, and can oracle values be corrected under abnormal conditions? | Chainlink CAPO oracle for USDe provides pricing with deviation thresholds and heartbeat monitoring. The oracle can reflect USDe depegs since it is not hardcoded. However, USDe's fair value is harder to determine than traditional stablecoins given the derivative-backed structure -- pricing relies on secondary market rather than verifiable reserves. Chainlink is Tier-0 with fallback mechanisms. Oracle values can be corrected under abnormal conditions. Score Mid (3) due to the inherent difficulty of pricing a derivative-backed synthetic dollar vs a fiat-reserve stablecoin, even with a Tier-0 oracle. | 3 | 3 | Non-Improvable | [P1] [Chainlink USDe Feed](https://data.chain.link/), [P1] [LlamaRisk CAPO Analysis](https://www.llamarisk.com/research/2025-03-07t22-20-26-000z) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | **Unknown.** Chainlink has enterprise certifications. Aave Labs and BGD Labs: no public SOC 2/ISO27001 documentation found. Chaos Labs: no public certification documentation. | 3 | 9 | **Source Missing** | [P1] [Aave Security](https://aave.com/security) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Highly resilient. Protocol operational through all major Ethereum events including The Merge (2022). Nov 2023: infrastructure responded within hours to critical vulnerability. Feb 2025: $210M liquidations processed smoothly. Feb 2026: $429M record liquidations processed with zero bad debt. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335), [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain-level halts >30 min in 12+ months. Tier-0 reliability. | 9 | 9 | Non-Improvable (optimal) | Ethereum Tier-0 status, public knowledge |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- USDe is not a staking-based product. No validator set relevant to USDe supply. | N/A | N/A | N/A | - |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- USDe is not a staking-based product. No validator set relevant to USDe supply. | N/A | N/A | N/A | - |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No permanent blocks from single Aave infrastructure failure. Withdrawals are permissionless via Pool contract. Oracle failure may trigger Guardian pause but does not block withdrawal of available liquidity. However, at the USDe level, failure of Ethena's OES custodians (Copper, Ceffu, Cobo, Anchorage Digital, Kraken) or CEX counterparties (Binance, Bybit, OKX, Deribit, Bitget) could cause USDe to depeg, creating losses for suppliers even if Aave infrastructure functions perfectly. | 3 | 3 | Non-Improvable | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P1] [Ethena Docs Risk](https://docs.ethena.fi/solution-overview/risks) |

**Infrastructure Counterparty Subtotal:**
- Scored questions: 6 (ST-IC-06, ST-IC-07 are N/A)
- 3x9=27, 3x3=9 = 36 raw
- Max raw: 6x9=54
- Adj: (36/54) x 45 = 30.0

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | At the Aave level, user USDe deposits remain in the Pool V3 contract -- no external deployment. However, the USDe asset itself is backed by positions on centralized exchanges (Binance, Bybit, OKX, Deribit, Bitget) through OES custody providers (Copper, Ceffu, Cobo, Anchorage Digital, Kraken). These are NOT Tier-0/1 per the SR Protocol Tiers list. This represents a significant structural counterparty exposure embedded within the asset itself. USDe suppliers are indirectly exposed to these CEX counterparties. Score High (1) due to material reliance on CEX/OES venues embedded in the asset's backing. | 1 | 1 | Non-Improvable | [P1] [Ethena Docs Custodians](https://docs.ethena.fi/solution-overview/custodians), [P1] [Ethena Docs Exchanges](https://docs.ethena.fi/solution-overview/exchanges) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | The displayed yield includes Aave Merit/points multiplier. The organic yield (~1.01% APR) comes from borrower interest -- transparent and on-chain. The Aave Merit points program is a protocol-wide incentive. Ethena's incentive programs (sUSDe staking rewards) create indirect demand for USDe borrowing, which supports supply yield but also creates reflexive dynamics. Arrangements are partially documented. | 3 | 3 | Non-Improvable | [P3] [Aave App USDe Reserve](https://app.aave.com/reserve-overview/?underlyingAsset=0x4c9edd5852cd905f086c759e8383e09bff1e68b3&marketName=proto_mainnet_v3) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes at the Aave level. Supply cap ($2.70B for USDe) and borrow caps enforced on-chain. USDe is currently at 43.81% of the supply cap. Risk Stewards actively manage caps. However, within USDe's backing, Ethena's counterparty limits across CEXs are not transparently enforced or verifiable on-chain. | 3 | 3 | Non-Improvable | [P3] [Aave App USDe Reserve](https://app.aave.com/reserve-overview/?underlyingAsset=0x4c9edd5852cd905f086c759e8383e09bff1e68b3&marketName=proto_mainnet_v3), [P1] [Ethena Docs Risk](https://docs.ethena.fi/solution-overview/risks) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | At Aave level: instant for available liquidity. USDe withdrawal is permissionless from Pool contract. $541M currently available. At USDe level: Ethena's redemption process requires unwinding derivative positions, which can take time and may be constrained during stress. Exit feasibility during a USDe depeg is uncertain -- suppliers could withdraw USDe from Aave instantly but the USDe itself may trade at a discount. | 3 | 3 | Non-Improvable | [P1] [Ethena Docs Redemption](https://docs.ethena.fi/solution-overview/usde-overview) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Yes. Ethena discloses OES custody providers (Copper, Ceffu, Cobo, Anchorage Digital, Kraken) and exchange counterparties (Binance, Bybit, OKX, Deribit, Bitget). Roles and operational flows are described in Ethena documentation. Aave's own service providers (Chaos Labs, LlamaRisk, BGD Labs, Karpatkey) are all publicly disclosed. | 9 | 9 | Non-Improvable (optimal) | [P1] [Ethena Docs Custodians](https://docs.ethena.fi/solution-overview/custodians), [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |

**Protocol Counterparty Subtotal:**
- 1x9=9, 3x3=9, 1x1=1 = 19 raw
- Max raw: 5x9=45
- Adj: (19/45) x 45 = 19.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | All USDe withdrawals are permissionless via Pool V3 contract based on available liquidity. Guardians can pause in emergency (5-of-9 multisig required) but pause is protocol-wide, not address-specific. No selective blocking at Aave level. Note: USDe itself has Ethena's FULL_RESTRICTED_STAKER_ROLE which can selectively block addresses at the token level, but this does not affect Aave withdrawal mechanics. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Under normal conditions, yes. $1.18B supplied, ~$641M borrowed. Available liquidity = $541M at 54.26% utilization, representing ~45.7% of supplied TVL. This is favorable utilization compared to most Aave pools. Rate model incentivizes repayment to restore liquidity. USDe has ~$5.9B market cap providing deep secondary market under normal conditions. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aave App USDe Reserve](https://app.aave.com/reserve-overview/?underlyingAsset=0x4c9edd5852cd905f086c759e8383e09bff1e68b3&marketName=proto_mainnet_v3) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No known withdrawal delays, queues, or freezes for the Aave USDe pool. USDe was listed on Aave relatively recently and the pool has operated within normal utilization ranges. Nov 2023 Aave-wide asset freezes during vulnerability patch resolved within days. >95% of withdrawals completed within stated period over lookback. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aave App USDe Reserve](https://app.aave.com/reserve-overview/?underlyingAsset=0x4c9edd5852cd905f086c759e8383e09bff1e68b3&marketName=proto_mainnet_v3) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Supply cap ($2.70B) is well above current supply ($1.18B = 43.81% of cap). Interest rate model penalizes high utilization with higher borrow rates. No history of USDe-specific caps blocking withdrawals. Risk Stewards actively manage caps. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aave App USDe Reserve](https://app.aave.com/reserve-overview/?underlyingAsset=0x4c9edd5852cd905f086c759e8383e09bff1e68b3&marketName=proto_mainnet_v3) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | USDe liquidity could deteriorate significantly during stress if USDe depegs and suppliers rush to exit. While utilization is moderate (54.26%), USDe is NOT as liquid as USDC during stress -- its secondary market depends on confidence in Ethena's backing mechanism. During the February 2025 Bybit hack, Ethena processed $123M in USDe redemptions (2% of supply) within 24 hours, but this was a contained event. A broader crisis of confidence in USDe's backing could cause cascading exits. Score Mid (3) due to stress behavior uncertainty for a synthetic dollar asset. | 3 | 3 | Non-Improvable | [P1] [Ethena Docs Risk](https://docs.ethena.fi/solution-overview/risks), [P4] [Bybit Hack Impact](https://rekt.news) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. USDe withdrawals from Aave are based on available pool liquidity only. No lockups, vesting, or unstaking delays. Instant withdrawal if liquidity available. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave V3 Overview](https://aave.com/docs/aave-v3/overview) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Primary USDe redemption through Aave Pool contract is always available (subject to pool liquidity). Secondary market USDe liquidity is generally sufficient under normal conditions (~$5.9B market cap, Curve/Uniswap pools). However, during stress, secondary market liquidity could thin significantly as market makers reduce exposure. USDe is less liquid than USDC or USDT during stress. | 3 | 3 | Non-Improvable | [P3] [CoinGecko USDe](https://www.coingecko.com/en/coins/ethena-usde), [P3] [DeFiLlama USDe Pools](https://defillama.com/stablecoin/usde) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | USDe has approximately $5.9B market cap with significant Curve and Uniswap pool liquidity. Depth supports ~3-10% of Aave USDe pool TVL without major impact under normal conditions. aEthUSDe is directly 1:1 redeemable from Pool. However, during stress, USDe liquidity could thin significantly vs top stablecoins. | 3 | 3 | Non-Improvable | [P3] [CoinGecko USDe](https://www.coingecko.com/en/coins/ethena-usde), [P3] [DeFiLlama USDe Pools](https://defillama.com/stablecoin/usde) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Moderate to high. While Aave's rate model and liquidation mechanics mitigate bank-run risk at the protocol level, a USDe-specific crisis (funding rate inversion, OES failure, CEX counterparty default) could trigger a rush to exit the USDe pool specifically. In such a scenario: (1) utilization would spike as suppliers withdraw, (2) USDe borrowers may not repay if USDe is depegging (why repay a depreciating loan?), (3) remaining suppliers face declining asset value. Score Mid (3) -- bank-run would cause significant queues and discounting but caps and rate mechanisms would contain losses. | 3 | 3 | Non-Improvable | [P3] [Aave App USDe Reserve](https://app.aave.com/reserve-overview/?underlyingAsset=0x4c9edd5852cd905f086c759e8383e09bff1e68b3&marketName=proto_mainnet_v3), [P1] [Ethena Docs Risk](https://docs.ethena.fi/solution-overview/risks) |

**Liquidity Subtotal:**
- 5x9=45, 4x3=12 = 57 raw
- Max raw: 9x9=81
- Adj: (57/81) x 45 = 31.667 = 31.7

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | aEthUSDe represents a claim on underlying USDe plus accrued interest. The receipt token itself tracks USDe 1:1 by design. However, USDe itself can depeg under stress -- during market stress events, USDe has shown brief deviations from $1.00. The aEthUSDe receipt token is only as stable as USDe. Score Mid (3) as the underlying asset has shown ~2-10% deviation potential during stress with recovery within days. | 3 | 3 | Non-Improvable | [P3] [CoinGecko USDe Price History](https://www.coingecko.com/en/coins/ethena-usde), [P3] [Aave App USDe Reserve](https://app.aave.com/reserve-overview/?underlyingAsset=0x4c9edd5852cd905f086c759e8383e09bff1e68b3&marketName=proto_mainnet_v3) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | While the Aave lending pool itself is not directional, USDe's backing is sensitive to crypto market conditions. Funding rates correlate strongly with market sentiment -- during bear markets, funding rates go negative, threatening USDe's backing. Aave suppliers face indirect directional exposure through USDe's derivative-backed structure. A severe, prolonged crypto downturn could cause USDe to depeg, resulting in permanent losses for suppliers who cannot exit in time. Score Mid (3) as the strategy has moderate directional exposure through the underlying asset. | 3 | 3 | Non-Improvable | [P1] [Ethena Docs Risk](https://docs.ethena.fi/solution-overview/risks), [P1] [Ethena Funding Rate Data](https://app.ethena.fi/dashboards/hedging) |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Two-slope model with Slope2 Risk Oracle. USDe utilization at 54.26% is well below the optimal kink. No history of prolonged >=95% utilization for USDe pool. Rate curves become steep as utilization approaches critical levels, incentivizing borrower repayment. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aave App USDe Reserve](https://app.aave.com/reserve-overview/?underlyingAsset=0x4c9edd5852cd905f086c759e8383e09bff1e68b3&marketName=proto_mainnet_v3) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. Chaos Labs and LlamaRisk provide continuous stress testing across all Aave pools including USDe. The protocol has been stress-tested through multiple severe events (Feb 2025: $210M liquidations, Feb 2026: $429M liquidations, March 2026: CAPO incident). USDe-specific scenarios (funding rate inversion, OES failure) are assessed by risk providers. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations), [P1] [Risks Documentation](https://aave.com/docs/resources/risks) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | USDe has 0% Max LTV (cannot be used as collateral for new borrows). Existing positions with 75% liquidation threshold and 8.5% penalty reflect conservative parameterization. For USDe suppliers: no leverage, no liquidation risk on supply positions. For USDe borrowers: liquidation occurs if collateral drops, which protects the protocol. The USDe asset itself could depeg, but this is an asset quality risk, not a leveraged liquidation risk. | 9 | 9 | Non-Improvable (optimal) | [P3] [Aave App USDe Reserve](https://app.aave.com/reserve-overview/?underlyingAsset=0x4c9edd5852cd905f086c759e8383e09bff1e68b3&marketName=proto_mainnet_v3) |

**Market Subtotal:**
- 3x9=27, 2x3=6 = 33 raw
- Max raw: 5x9=45
- Adj: (33/45) x 45 = 33.0

---

### **Strategy Total: 170.3/270 (63.1%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 25.0 | 45 | 55.6% |
| Collateral | 31.7 | 45 | 70.4% |
| Infra Counterparty | 30.0 | 45 | 66.7% |
| Protocol Counterparty | 19.0 | 45 | 42.2% |
| Liquidity | 31.7 | 45 | 70.4% |
| Market | 33.0 | 45 | 73.3% |
| **Strategy Total** | **170.3** | **270** | **63.1%** |

**Precise Strategy calculation:**
- Protocol Mechanics: (45/81) x 45 = 25.0
- Collateral: (19/27) x 45 = 31.667
- Infra Counterparty: (36/54) x 45 = 30.0
- Protocol Counterparty: (19/45) x 45 = 19.0
- Liquidity: (57/81) x 45 = 31.667
- Market: (33/45) x 45 = 33.0
- **Total: 25.0 + 31.667 + 30.0 + 19.0 + 31.667 + 33.0 = 170.333 = 170.3**

---

### OPERATIONS (30% Weight) -- Score: 256.0/270 (94.8%)

**NOTE: All Operations scores are IDENTICAL to other Aave Ethereum V3 Core Market ratings. Same governance, same team, same docs, same treasury, same backstop.**

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | On-chain DAO governance via AAVE, stkAAVE, aAAVE token voting. Structured proposal process: Temp Check (Snapshot) -> ARFC (forum) -> AIP (on-chain vote). Cross-chain voting via storage proofs. Risk Stewards (Chaos Labs) handle parameter adjustments within governance-approved bounds. Two 5-of-9 Guardian multisigs provide emergency controls. No single entity can unilaterally change core fund-custody logic. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [Aave Governance Forum](https://governance.aave.com/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | Moderate concentration typical of large DAOs. However, robust checks: two 5-of-9 Guardian multisigs with diverse independent membership, Risk Steward system distributing parameter control, structured proposal process requiring community discussion. Recent governance activity demonstrates active participation. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P2] [Governance Forum Activity](https://governance.aave.com/) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. 1-day standard timelock, 7-day for critical changes. Two Guardian multisigs (5-of-9 each) with veto powers. Structured proposal process (Temp Check -> ARFC -> AIP). Certora reviews all governance proposals for security. No timelock reductions in recent history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A -- Aave has no "strategy manager" in the vault sense. Risk providers (Chaos Labs, LlamaRisk) can be changed via governance without any impact on user withdrawals. | N/A | N/A | N/A | - |

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
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | **CLEARED.** SEC closed 4-year investigation December 16, 2025 without enforcement action. No charges, fines, or further action. No ongoing or past material enforcement actions in major jurisdictions. | 9 | 9 | Non-Improvable (optimal) | [P4] [Yahoo Finance](https://finance.yahoo.com/news/sec-closes-4-long-investigation-091715487.html) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Yes. Nov 2023: demonstrated rapid response (pools secured within hours). Feb 2026: Chaos Labs Risk Stewards adjusted parameters in real-time during market crash. March 2026: CAPO incident response included post-mortem and reimbursement plan within days. BGD Labs provides continuous monitoring. Guardian multisigs on standby. | 9 | 9 | Non-Improvable (optimal) | [P2] [Nov 2023 Incident](https://governance.aave.com/t/aave-v2-v3-security-incident-04-11-2023/15335) |
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
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive documentation covering V3 architecture, smart contracts, risk parameters, governance, interest rate models. Updated through V3.6 (Nov 2025). Risks page explicitly covers liquidation mechanics, oracle risks, smart contract risks. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Docs](https://aave.com/docs/aave-v3/overview), [P1] [Risks](https://aave.com/docs/resources/risks) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Detailed documentation: health factor mechanics, liquidation process, bad debt scenarios, interest rate models. V3.3 bad debt features documented. Loss conditions clearly explained with specific scenarios. | 9 | 9 | Non-Improvable (optimal) | [P1] [Health Factor & Liquidations](https://aave.com/help/borrowing/liquidations), [P1] [Risks](https://aave.com/docs/resources/risks) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Pool V3: 0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2. PoolAddressesProvider: 0x2f39d218133AFaB8F2B819B1066c7E434Ad94E9e. All verified on Etherscan. BGD Address Book GitHub repo provides canonical registry. | 9 | 9 | Non-Improvable (optimal) | [P1] [Smart Contracts Docs](https://aave.com/docs/aave-v3/smart-contracts), [P1] [BGD Address Book](https://github.com/bgd-labs/aave-address-book) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Guardian roles (Protocol and Governance Emergency Guardians), timelock durations (1-day standard, 7-day critical), Risk Steward permissions and bounds, proposal process all documented. All changes visible on-chain and in governance forum. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full on-chain transparency for Aave pool. All USDe pool balances verifiable via Pool V3 contract. Protocol Data Provider contract enables programmatic verification of all reserve states including borrows (proof-of-liabilities). Note: Ethena also provides Chaos Labs Edge PoR oracle for USDe backing, though this is at the USDe level, not Aave level. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2), [P3] [DeFiLlama Aave V3](https://defillama.com/protocol/aave-v3) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. All core contracts verified on Etherscan: Pool V3, PoolConfigurator, PoolAddressesProvider, aTokens, variable debt tokens, ProtocolDataProvider. Full source code readable and verified. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Pool V3](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2#code) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Yes. Umbrella Safety Module launched June 2025 with ~$282M in staked assets. Automated slashing mechanism. Clear published activation rules -- automated, not discretionary. | 9 | 9 | Non-Improvable (optimal) | [P1] [Umbrella Docs](https://aave.com/docs/aave-v3/umbrella), [P2] [LlamaRisk Umbrella Coverage](https://governance.aave.com/t/llamarisk-insights-umbrella-coverage-principles-and-slashing-logic/23527) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | **Modest relative to scale.** Umbrella: ~$282M (automated backstop). DAO Treasury: ~$133M (excl. AAVE tokens). Combined ~$415M vs $34.5B Ethereum TVL = ~1.2%. Below 5% threshold for Low Risk; within 1-5% range = Mid Risk. | 3 | 9 | **Improvable** | [P2] [DAO Funding Insights](https://governance.aave.com/t/aave-dao-funding-insights/24192), [P2] [TokenLogic Treasury Reports](https://aave.tokenlogic.xyz/treasury) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. DAO Treasury ~$133M (excl. AAVE tokens). Protocol generated ~$885M in fees in 2025. Revenue broadly covers expenses. Runway >24 months. | 9 | 9 | Non-Improvable (optimal) | [P2] [DAO Funding Insights](https://governance.aave.com/t/aave-dao-funding-insights/24192), [P3] [Coinlaw Statistics](https://coinlaw.io/aave-statistics/) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | Highly resilient across multiple severe stress events. Survived 2022 bear market (FTX collapse, Terra/Luna, SVB crisis). Feb 2025: $210M liquidations, zero bad debt. Feb 2026: record $429M liquidations, zero bad debt. Protocol has demonstrated resilience across every major market stress event over 8+ years. | 9 | 9 | Non-Improvable (optimal) | [P1] [Aave Historical Liquidations](https://aave.com/blog/historical-liquidations) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Smart contracts are permissionless and non-custodial. USDe withdrawals always available via direct Pool contract interaction based on available liquidity. Governance via on-chain voting (no off-chain dependency). Multiple independent development teams provide redundancy. | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance Docs](https://aave.com/docs/ecosystem/governance), [P0] [Pool V3 Contract](https://etherscan.io/address/0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2) |

**Financial Resilience Subtotal: 58.5/67.5 (86.7%)**
- 4 questions at score 9 = 36, 1 question at score 3 = 3
- Raw: 39/45, Weighted: (39/45) x 67.5 = 58.5

---

### **Operations Total: 256.0/270 (94.8%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 67.5 | 67.5 | 100.0% |
| Team & Legal | 62.5 | 67.5 | 92.6% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 58.5 | 67.5 | 86.7% |
| **Operations Total** | **256.0** | **270** | **94.8%** |

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 99 | 99 | 180.0 | 180 | 100.0% |
| | Key Management (7 of 8 Q scored) | 57 | 63 | 162.9 | 180 | 90.5% |
| | **Security Subtotal** | | | **342.9** | **360** | **95.2%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 45 | 81 | 25.0 | 45 | 55.6% |
| | Collateral (3 of 4 Q scored) | 19 | 27 | 31.7 | 45 | 70.4% |
| | Infra Counterparty (6 of 8 Q scored) | 36 | 54 | 30.0 | 45 | 66.7% |
| | Protocol Counterparty (5 Q) | 19 | 45 | 19.0 | 45 | 42.2% |
| | Liquidity (9 Q) | 57 | 81 | 31.7 | 45 | 70.4% |
| | Market (5 Q) | 33 | 45 | 33.0 | 45 | 73.3% |
| | **Strategy Subtotal** | | | **170.3** | **270** | **63.1%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 75 | 81 | 62.5 | 67.5 | 92.6% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 39 | 45 | 58.5 | 67.5 | 86.7% |
| | **Operations Subtotal** | | | **256.0** | **270** | **94.8%** |
| **TOTAL** | | | | **769.2** | **900** | **85.5%** |

---

