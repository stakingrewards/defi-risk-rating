# Morpho - Re7 USDT Vault Risk Rating

**Rating Date**: 2026-06-23
**Final Grade**: B-
**Total Score**: 680.8/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 293.2/360 (81.4%)

#### Smart Contract Security (20% weight, 180 max points)

**NOTE: All Smart Contract Security scores are platform-level and IDENTICAL to the other Morpho V1 MetaMorpho vault ratings (Steakhouse USDT/USDC, Smokehouse USDC). The Morpho Blue core is immutable (~600 LOC) and the MetaMorpho V1 vault is a non-upgradeable ERC4626 contract. S-SC-10 and S-SC-11 score 3 per the v0.1-gamma verification principle (monitoring cannot automatically trigger protective actions). The Nov 2025 Re7 loss was a credit/curation failure, NOT a smart-contract exploit, so it does not affect S-SC scoring.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | Yes. 25+ audits from Tier-0/1 firms including ChainSecurity, Spearbit/OpenZeppelin, Zellic, Certora for Morpho Blue and the MetaMorpho framework. Formal verification by Certora. This vault is a standard MetaMorpho V1 ERC4626 deployed from the audited factory. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/), [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent ecosystem audits by Tier-0 firms (ChainSecurity, Spearbit/OpenZeppelin via Cantina, Certora formal verification). Multiple Tier-0 auditors. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. Morpho Blue core is immutable. The MetaMorpho V1 vault (0x95EeF…) is non-upgradeable; no core upgrades to audit. All framework changes preceded by Tier-0 audits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/security-reviews/) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. June 2023 vulnerability patched immediately with OpenZeppelin; Certora formal verification proves critical invariants. All findings resolved before deployment. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vulnerability Report](https://morpho.mirror.xyz/QVPDZEgNZqQeBIw0Vr7KNsw-0J4RIws9FflWv6X96yM) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Morpho Blue core is immutable. The MetaMorpho vault is a non-upgradeable ERC4626 contract. Market/parameter changes require Owner multisig + 3-day timelock (259,200s, verified via Morpho API) + Guardian veto. Meets the Low criterion (timelock >=24h, narrow roles, immutable core). | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) (timelock=259200), [P0] [Etherscan](https://etherscan.io/address/0x95EeF579155cd2C5510F312c8fA39208c3Be01a8) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed smart-contract exploit causing user fund loss in Morpho/MetaMorpho contracts. April 2025 frontend issue ($2.6M) was intercepted by a white hat and fully returned. The Nov 2025 Re7 bad-debt event was a credit/curation failure (illiquid exotic collateral), not a contract bug; Morpho liquidations fired per spec. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P4] [Cryptodamus - Stream/Re7](https://cryptodamus.io/en/articles/news/stream-finance-collapse-27m-defi-fallout-re7-labs-under-fire) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull. Morpho = ADDMO (French nonprofit). Re7 Capital is an identified UK investment firm. The Nov 2025 losses were due-diligence/curation failures, not misappropriation by Re7. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions observed. The vault uses the 3-day (259,200s) timelock, the Morpho V1 protocol minimum; no evidence of a reduction in the last 12 months. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active public bounty on Cantina with $2.5M max payout covering Morpho Blue and MetaMorpho contracts. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Morpho runs internal monitoring bots performing invariant checks; Re7 claims liquidity monitoring and price alerts. However, per the v0.1-gamma verification principle, monitoring cannot automatically trigger protective actions -- all responses require manual human intervention, and the Public Allocator's automated flows are not covered by any automated halt. The Nov 2025 event showed Re7's monitoring did not trigger timely protective action. Platform-level Mid. | 3 | 9 | **Improvable** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P2] [Re7 USDT Forum](https://forum.morpho.org/t/re7-usdt-metamorpho-vault/518) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. Morpho Blue prioritizes immutability over admin controls. Guardian can manually veto pending timelocked actions but cannot pause the protocol. Market-level isolation provides containment but does not cover automated allocation flows. | 3 | 3 | Non-Improvable | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Smart Contract Security Subtotal:**
- Raw scores: 9x9 (sum 81) + 2x3 (sum 6) = 87/99
- Adjusted: (87/99) x 180 = **158.2/180 (87.9%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

**NOTE: Unlike the flagship Morpho curators, Re7's Owner multisig is only a 2-of-5 Gnosis Safe (verified threshold=2, 5 owners, Safe v1.3.0, via the Safe Transaction Service). This is BELOW the framework's >=3-of-5 Low-risk threshold, driving S-KM-02 and S-KM-03 to Mid (3). No separate Curator Safe is configured (curator role resolves to the Owner / RE7 Labs). The 3-day timelock (259,200s) meets >=24h.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Owner: Gnosis Safe 2-of-5 multisig (0xE86399fE…, verified via Safe API: threshold 2, 5 owners). Guardian: ERC1967/Aragon DAO proxy (0x2F80ba89…). Curator role not separately set (resolves to Owner). All changes visible on-chain with 3-day timelock. Diversified multisig with on-chain trail. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API - Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xE86399fE6d7007FdEcb08A2ee1434Ee677a04433/), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No single key can move user funds: the vault is a non-upgradeable ERC4626 and Morpho Blue logic is immutable; permissionless redemption always available. However, the Owner is a 2-of-5 Safe (threshold 2 < 3), which FAILS the Low criterion (requires threshold >=3 AND signers >=5 AND timelock >=24h). Because no single key can move funds, the High trigger does not fire, but the sub-threshold multisig caps this at Mid (3). | 3 | 9 | **Improvable** | [P0] [Safe API - Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xE86399fE6d7007FdEcb08A2ee1434Ee677a04433/) (threshold=2, owners=5), [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner multisig is 2-of-5 (verified via Safe API: 5 distinct owner addresses). This is below the >=3-of-5 (or >=4-of-7) Low-risk threshold. Signer identities are not publicly disclosed (curator = RE7 Labs), so full independence cannot be confirmed. Maps to Mid (3): "2-of-4 or 3-of-3 with partial independence" tier (a 2-of-5 with undisclosed signers is best-cased at Mid). | 3 | 9 | **Improvable** | [P0] [Safe API - Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xE86399fE6d7007FdEcb08A2ee1434Ee677a04433/) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking capability. No pause function on Morpho Blue (immutable). Guardian can only revoke pending timelocked actions. Withdrawals always permissionless via direct ERC4626 interaction. Rules publicly documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets held in non-custodial Morpho Blue contracts on Ethereum. Permissionless ERC4626 redemption. No off-chain custody. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P0] [Etherscan](https://etherscan.io/address/0x95EeF579155cd2C5510F312c8fA39208c3Be01a8) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. Vault funds held in Morpho Blue markets, separate from Re7/Morpho treasury or operational wallets. Performance fee (5%) accrues on-chain transparently. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/), [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) (fee=0.05) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain enforced whitelist of Morpho Blue markets only (currently a USDe/USDT market; historically USDe/sUSDe/deUSD/sdeUSD/wstETH markets). New market additions require Owner multisig + 3-day timelock + Guardian veto. Supply caps per market enforced on-chain (the USDe market cap has been set to 0). | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) (allocation), [P2] [Re7 USDT Forum](https://forum.morpho.org/t/re7-usdt-metamorpho-vault/518) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | No public, vault-specific incident playbook with key-rotation steps or tabletop results. Re7's Nov 2025 incident response was reactive and criticized, indicating playbook gaps. No documented tested process for rapid key rotation / signer replacement. | 3 | 9 | **Improvable** | [P4] [CryptoRank - Re7 Criticism](https://cryptorank.io/news/feed/1c712-re7-labs-criticism-from-stream-insolvency), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Key Management Subtotal:**
- Raw scores: 6x9 (sum 54) + 2x3 (sum 6) = ... actually 5x9 + 3x3. Let me itemize: S-KM-01=9, 02=3, 03=3, 04=9, 05=9, 06=9, 07=9, 08=3 -> 5x9 (sum 45) + 3x3 (sum 9) = 54/72
- Adjusted: (54/72) x 180 = **135.0/180 (75.0%)**

**Security Total: 158.2 + 135.0 = 293.2/360 (81.4%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 158.2 | 180 | 87.9% |
| Key Management | 135.0 | 180 | 75.0% |
| **Security Total** | **293.2** | **360** | **81.4%** |

---

### STRATEGY (30% Weight) -- Score: 177.3/270 (65.7%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield from overcollateralized USDT lending against interest-bearing/exotic stablecoin collateral (USDe/sUSDe, historically deUSD/sdeUSD). 100% mandate-aligned to the stated "above-market USDT yield via interest-bearing-stablecoin lending" mandate. Sources documented on the Morpho app and Re7 forum post. | 9 | 9 | Non-Improvable (optimal) | [P2] [Re7 USDT Forum](https://forum.morpho.org/t/re7-usdt-metamorpho-vault/518), [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss can occur in severe-but-plausible single-shock events that are MORE likely than for a blue-chip vault: exotic stablecoin depeg (USDe/deUSD), failed liquidations on illiquid collateral, plus USDT issuer risk. The Nov 2025 Stream/Elixir event demonstrated exactly this loss path materializing for Re7 markets. Mid given exotic-collateral mandate. | 3 | 3 | Non-Improvable | [P4] [Cryptopolitan - Re7 Criticism](https://www.cryptopolitan.com/re7-labs-criticism-from-stream-insolvency/), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No vault-level leverage or rehypothecation of depositor funds. The vault simply lends USDT (1.0x). Borrowers may take leverage, but that is borrower-side overcollateralized risk. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment, [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. Liquidation risk applies to borrowers. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | YES -- uncompensated permanent-loss event. In Nov 2025 Re7-curated USDT/USDT0-vs-interest-bearing-stablecoin markets (deUSD/sdeUSD across four Euler and Morpho markets, ~$12.75M; plus ~$14.65M xUSD/USDT0 on Plasma) incurred bad debt with partial socialization (reported ~70% immediate withdrawal, ~30% retained pending uncertain recovery). Same curator, same strategy type as this vault. Framework High (1): "Any uncompensated permanent-loss event." Category Deal Breaker triggered. | 1 | 9 | **Improvable** (decays to 9 only with a 24-36 month clean, compensated record) | [P4] [Cryptodamus - $27M Re7](https://cryptodamus.io/en/articles/news/stream-finance-collapse-27m-defi-fallout-re7-labs-under-fire), [P4] [Protos - Curator Reckoning](https://protos.com/stream-finance-meltdown-winners-and-losers-in-defi-risk-curator-reckoning/) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Partial and demonstrably inadequate. Re7 publishes a proprietary "Re7 Risk Index" (technical/economic/systemic dimensions) and claims monitoring tooling, but it failed to flag the circular-collateral and oracle-lag risk that caused the Nov 2025 loss, and lacks published, enforced quantitative limits. Mid (3). | 3 | 9 | **Improvable** | [P1] [Hindenrank - Re7 Risk Analysis](https://hindenrank.com/blog/how-does-re7-labs-work), [P2] [Re7 USDT Forum](https://forum.morpho.org/t/re7-usdt-metamorpho-vault/518) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Primarily organic lending interest from borrower demand for leverage against interest-bearing stablecoins. Not predominantly incentive-driven. Remains positive without incentives. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) (netApy ~2.65%), [P2] [Re7 USDT Forum](https://forum.morpho.org/t/re7-usdt-metamorpho-vault/518) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Mid. The loan asset USDT is highly liquid, but the exotic stablecoin collateral markets proved hard to unwind in stress -- the Nov 2025 event demonstrated illiquid collateral and stuck positions producing ~2-5%+ (in fact larger) penalties on affected markets. Under conservative assumptions, stress exits could materially compress returns. | 3 | 3 | Non-Improvable | [P4] [Protos - Curator Reckoning](https://protos.com/stream-finance-meltdown-winners-and-losers-in-defi-risk-curator-reckoning/) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | The vault is a USDT lender (interest, not spread). However, its collateral values depend materially on exotic stablecoin pegs (USDe/deUSD) that can invert, which indirectly drives bad-debt risk. Yield mechanism itself is not a carry/peg trade, so reliance is minority; scored Low but flagged. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment, [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Yes. The vault uses Public Allocator + Curator-appointed allocators. Supply caps per market limit max per-market exposure, but no automatic kill-switch exists for abnormal conditions (oracle deviation, depeg, utilization spikes). The March 2026 Resolv exploit demonstrated this failure mode on Morpho vaults. Halting requires manual intervention. | 3 | 9 | **Improvable** | [P1] [Public Allocator](https://docs.morpho.org/curate/concepts/public-allocator/), [P4] [Resolv Exploit](https://defiprime.com/resolv-usr-exploit) |

**Protocol Mechanics Subtotal:**
- 9 applicable (ST-PM-04 = N/A): 5x9 (ST-PM-01/03/07/09 + ... ) -- itemize: 01=9,02=3,03=9,05=1,06=3,07=9,08=3,09=9,10=3 -> 4x9 (sum 36) + 4x3 (sum 12) + 1x1 (sum 1) = 49/81
- Adjusted: (49/81) x 45 = **27.2/45 (60.5%)**

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Exotic / interest-bearing stablecoins: USDe and sUSDe (Ethena synthetic dollar), historically deUSD/sdeUSD (Elixir). These are higher-risk synthetic stablecoins (CCC-tier risk profile), not blue-chip. Each market has on-chain LLTVs and supply caps (e.g., USDe/USDT at 91.5% LLTV), but the asset set is exotic. Mid (3): includes higher-risk assets each tiered with on-chain LTVs/caps (consistent with the Smokehouse exotic-collateral treatment). | 3 | 3 | Non-Improvable | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) (USDe/USDT, lltv 0.915), [P2] [Re7 USDT Forum](https://forum.morpho.org/t/re7-usdt-metamorpho-vault/518) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | HIGH RISK. Re7's exotic stablecoin collateral depegged materially in the last 12 months: deUSD (Elixir) collapsed ~98% in Nov 2025; xUSD (Stream) collapsed; USDe has depegged on prior occasions. Depeg >10% lasting more than brief periods is squarely the High (1) criterion. | 1 | 9 | **Improvable** (historical/time-decay; decays to 9 with a 24-36 month clean record) | [P4] [BlockEden - $285M Contagion](https://blockeden.xyz/blog/2025/11/08/m-defi-contagion/), [P4] [Cryptodamus](https://cryptodamus.io/en/articles/news/stream-finance-collapse-27m-defi-fallout-re7-labs-under-fire) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | USDe/sUSDe are synthetic-dollar (delta-neutral) tokens, not validator-staked, so there is no direct validator/slashing risk to the vault's collateral. (Any historical wstETH market exposure is immaterial.) | 9 | 9 | Non-Improvable (optimal) | [P2] [Re7 USDT Forum](https://forum.morpho.org/t/re7-usdt-metamorpho-vault/518) |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | Low on the bridged/wrapped axis. Current and historical collateral (USDe/sUSDe/deUSD/sdeUSD) are protocol receipt / synthetic tokens, which the framework EXCLUDES from "bridged or wrapped" (handled under other questions). No material wrapped-BTC or third-party-bridge exposure. <=20% bridged/wrapped. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) (collateral = USDe), [P2] [Re7 USDT Forum](https://forum.morpho.org/t/re7-usdt-metamorpho-vault/518) |

**Collateral Subtotal:**
- 4 questions: 2x9 (sum 18) + 1x3 (sum 3) + 1x1 (sum 1) = 22/36
- Adjusted: (22/36) x 45 = **27.5/45 (61.1%)**

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Ethereum (Tier-0 chain), Chainlink and Morpho oracle adapters (Tier-0) per market. No bridges; no CEX dependency for operations. Dependencies disclosed and Tier-0. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/), [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | HIGH RISK. Each Morpho Blue market uses a single immutable oracle with no fallback and no post-deployment correction. Per the mandatory hardcoded/immutable-oracle check: this vault prices EXOTIC stablecoins (USDe/deUSD) that CAN and DID depeg materially -- the Mid (3) carve-out applies only to battle-tested deep-liquidity assets where depeg is historically unprecedented (BTC/ETH), which is NOT the case here. Immutable oracle on a materially-depeggable asset = High (1). | 1 | 1 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/), [P4] [BlockEden - oracle lag](https://blockeden.xyz/blog/2025/11/08/m-defi-contagion/) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | No public SOC 2 Type II or ISO27001 certification found for Re7 Labs or Morpho Labs/ADDMO. Chainlink holds enterprise certifications. Re7 runs off-chain risk/monitoring tooling without disclosed certification. | 3 | 9 | **Source Missing** | [P1] [Hindenrank - Re7](https://hindenrank.com/blog/how-does-re7-labs-work), [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Ethereum/Chainlink/Morpho infra behaved correctly through past incidents: April 2025 frontend issue resolved in 4 minutes; Nov 2025 market isolation worked and on-chain withdrawals were never blocked at the infra level (the Re7 loss was a credit/curation failure, not infra). Deployed >6 months with no infra-driven losses. | 9 | 9 | Non-Improvable (optimal) | [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain halts >30 minutes in the last 12+ months. Tier-0 chain reliability. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | No material slashing exposure -- collateral is synthetic-dollar (USDe), not validator-staked. No depositor impact. | 9 | 9 | Non-Improvable (optimal) | [P2] [Re7 USDT Forum](https://forum.morpho.org/t/re7-usdt-metamorpho-vault/518) |
| ST-IC-07 | Are validators diverse geographically and by operator? | Ethereum validator set is highly distributed across geographies and operators. No single operator >25% of relevant stake. (Minimal direct staking exposure for this vault.) | 9 | 9 | Non-Improvable (optimal) | Ethereum validator data |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Permissionless on-chain ERC4626 redemption is always available via direct contract interaction. No off-chain dependency for withdrawals. A frontend or oracle failure does not block lender withdrawals. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-IC-09 | How robust is the cross-chain messaging or bridge verification setup? | N/A -- The vault operates exclusively on Ethereum with no cross-chain messaging or bridge dependency. | N/A | N/A | N/A | Vault architecture |
| ST-IC-10 | Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting? | N/A -- No cross-chain escrow or minting mechanism for this vault. | N/A | N/A | N/A | Vault architecture |
| ST-IC-11 | Is the off-chain verification infrastructure resilient to data-source manipulation? | N/A -- The vault does not rely on off-chain verifiers or cross-chain attestation; oracle data is consumed on-chain via Morpho oracle adapters. | N/A | N/A | N/A | Vault architecture |

**Infrastructure Counterparty Subtotal:**
- 8 applicable (ST-IC-09/10/11 = N/A): itemize 01=9,02=1,03=3,04=9,05=9,06=9,07=9,08=9 -> 6x9 (sum 54) + 1x3 (sum 3) + 1x1 (sum 1) = 58/72
- Adjusted: (58/72) x 45 = **36.25/45 (80.6%)**

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All allocation is to Morpho Blue markets (Tier-0 protocol), listed with on-chain caps. No CEX or RWA platform deployment. The collateral-issuer counterparties (Ethena/Elixir) are established but introduce exotic-stablecoin risk, captured under ST-C. Venues themselves are Tier-0 Morpho Blue. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) (allocations) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Performance fee is 5% (verified via Morpho API), accruing on-chain. No undisclosed rebates identified. Fee changes subject to timelock. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) (fee=0.05) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. On-chain supply caps per market enforced by the MetaMorpho contract; cap increases require 3-day timelock; cap decreases are instant (risk-reducing -- the USDe market cap was reduced to 0). | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) (supplyCap), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Mid. Vault-level ERC4626 redemption remains permissionless, but the Nov 2025 event demonstrated that Re7's exotic-collateral positions could NOT be unwound safely in stress (illiquid collateral led to bad debt and stuck positions requiring partial loss socialization). Some counterparties required longer lead times / secondary liquidity under stress. | 3 | 3 | Non-Improvable | [P4] [Protos - Curator Reckoning](https://protos.com/stream-finance-meltdown-winners-and-losers-in-defi-risk-curator-reckoning/) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending -- no external validators, custodians, or asset managers in vault operations. Re7 Labs (curator) is disclosed. Collateral issuers (Ethena, Elixir) publicly known. | 9 | 9 | Non-Improvable (optimal) | Vault architecture, [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) |

**Protocol Counterparty Subtotal:**
- 5 questions: 4x9 (sum 36) + 1x3 (sum 3) = 39/45
- Adjusted: (39/45) x 45 = **39.0/45 (86.7%)**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain ERC4626 redemption. No address-level blocking; no admin pause function (Morpho Blue immutable). Withdrawal availability depends on market liquidity, not admin discretion. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Mixed. The vault is currently almost entirely idle (~$22K, near-100% liquid now), but its mandate runs exotic high-utilization markets where, under stress, near-total exit is not guaranteed -- demonstrated in Nov 2025 when affected Re7 markets could not satisfy full redemptions. Mid. | 3 | 3 | Non-Improvable | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) (idle ~$22,044), [P4] [Protos](https://protos.com/stream-finance-meltdown-winners-and-losers-in-defi-risk-curator-reckoning/) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | YES. In Nov 2025 Re7-curated markets experienced freezes/unresolved delays -- affected depositors could withdraw only ~70% immediately, with ~30% locked pending uncertain recovery. This is well below the 80% threshold for affected markets and constitutes prolonged unresolved delays. High (1). | 1 | 9 | **Improvable** (historical/time-decay; decays to 9 with a 24-36 month clean record) | [P4] [Cryptopolitan - Re7](https://www.cryptopolitan.com/re7-labs-criticism-from-stream-insolvency/), [P4] [Cryptodamus](https://cryptodamus.io/en/articles/news/stream-finance-collapse-27m-defi-fallout-re7-labs-under-fire) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Low. Morpho supply caps limit NEW supply into a market, not redemptions of existing positions (withdrawals are permissionless ERC4626). During the Nov 2025 stress, exit delays on affected Re7 markets were driven by market UTILIZATION / illiquid exotic collateral (captured separately in ST-L-02/05/09), NOT by cap design preventing exits -- Re7 reduced caps (risk-reducing) rather than using them to block redemptions. No history of caps being used to block exits; cap increases require the 3-day timelock. Consistent with the Steakhouse/Smokehouse Morpho cap treatment (both Low (9), explicitly noting Nov 2025 delays were utilization- not cap-driven). | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) (supplyCap), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | HIGH RISK. During the Nov 2025 volatility, Re7's exotic-collateral markets suffered multi-day dysfunction and punitive discounts (~30% haircut on affected positions). Demonstrated unreliable exits under stress. High (1). | 1 | 1 | Non-Improvable | [P4] [BlockEden - Contagion](https://blockeden.xyz/blog/2025/11/08/m-defi-contagion/), [P4] [Protos](https://protos.com/stream-finance-meltdown-winners-and-losers-in-defi-risk-curator-reckoning/) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure USDT lending with no structural lockups, vesting, or bridge dependencies on the lender side. Exit depends on borrower repayment/liquidation, not structural locks. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary ERC4626 redemption is always available from the vault; secondary RE7USDT market exists but is not required for exit. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | The loan asset (USDT) and the receipt token (RE7USDT, 1:1 NAV claim) are deep/liquid for the loan side. However, the collateral side (exotic stablecoins) is shallow in stress. For the receipt/loan-asset axis the depth is adequate; scored Low with the caveat that collateral depth is the binding constraint (captured in ST-L-02/05). | 9 | 9 | Non-Improvable (optimal) | [P3] Market data (USDT), [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | HIGH RISK. Re7's Nov 2025 event was effectively a run on exotic-collateral markets that forced meaningful permanent haircuts (~30%) and prolonged withdrawal blocks on affected positions -- the High criterion ("fast bank-run likely to force meaningful permanent losses, haircuts, or prolonged withdrawal blocks"). Thin buffers (91.5% LLTV) and exotic collateral amplify this. | 1 | 1 | Non-Improvable | [P4] [BlockEden - Contagion](https://blockeden.xyz/blog/2025/11/08/m-defi-contagion/), [P4] [Cryptodamus](https://cryptodamus.io/en/articles/news/stream-finance-collapse-27m-defi-fallout-re7-labs-under-fire) |

**Liquidity Subtotal:**
- 9 questions: itemize 01=9,02=3,03=1,04=9,05=1,06=9,07=9,08=9,09=1 -> 5x9 (sum 45) + 1x3 (sum 3) + 3x1 (sum 3) = 51/81
- Adjusted: (51/81) x 45 = **28.3/45 (63.0%)**

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | HIGH RISK. The RE7USDT share is an ERC4626 NAV claim that should track USDT-plus-yield. During the Nov 2025 stress, affected Re7 vaults socialized losses (~30% haircut), so the share NAV was materially impaired (>10% impairment for affected depositors) rather than holding par. High (1). | 1 | 9 | **Improvable** (decays to 9 only with a demonstrated clean stress survival) | [P4] [Cryptodamus](https://cryptodamus.io/en/articles/news/stream-finance-collapse-27m-defi-fallout-re7-labs-under-fire), [P3] [CoinGecko RE7USDT](https://www.coingecko.com/en/coins/re7-usdt-morpho-vault) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Mid. The vault lends USDT (dollar-denominated; no directional BTC/ETH exposure for lenders). However, depositors carry USDT issuer/denomination risk -- S&P rated Tether stability "weak" (Nov 2025) -- consistent with the Steakhouse USDT precedent. Scored Mid for USDT denomination risk. | 3 | 3 | Non-Improvable | [P4] [S&P Tether Downgrade](https://www.theblock.co/post/380562/tether-usdt-stability-score-weak-sp-reserves-cant-absorb-bitcoin-drop) |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Immutable Adaptive Curve IRM per market; rates auto-increase with utilization; no governance manipulation possible. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Mid. Re7 maintains a "Re7 Risk Index" with monitoring tooling, but it demonstrably failed to model the tail scenario (circular collateral / oracle lag) that caused the Nov 2025 loss -- tail assumptions and cross-factor interactions only partially covered. Mid (3). | 3 | 3 | Non-Improvable | [P1] [Hindenrank - Re7 Risk Analysis](https://hindenrank.com/blog/how-does-re7-labs-work) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Mid. For lenders, liquidations normally protect principal, but Re7's thin buffers (91.5% LLTV) and exotic collateral mean sharp moves CAN gap past liquidation and crystallize bad debt -- as partially occurred in Nov 2025. Risk bounded by per-market caps and isolation, but elevated versus blue-chip vaults. Mid (3). | 3 | 3 | Non-Improvable | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/), [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) (lltv 0.915) |

**Market Subtotal:**
- 5 questions: itemize 01=1,02=3,03=9,04=3,05=3 -> 1x9 (sum 9) + 3x3 (sum 9) + 1x1 (sum 1) = 19/45
- Adjusted: (19/45) x 45 = **19.0/45 (42.2%)**

---

### **Strategy Total: 27.2 + 27.5 + 36.25 + 39.0 + 28.3 + 19.0 = 177.3/270 (65.7%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 27.2 | 45 | 60.5% |
| Collateral | 27.5 | 45 | 61.1% |
| Infra Counterparty | 36.25 | 45 | 80.6% |
| Protocol Counterparty | 39.0 | 45 | 86.7% |
| Liquidity | 28.3 | 45 | 63.0% |
| Market | 19.0 | 45 | 42.2% |
| **Strategy Total** | **177.3** | **270** | **65.7%** |

---

### OPERATIONS (30% Weight) -- Score: 210.3/270 (77.9%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid with checks. Morpho Blue immutable; the MetaMorpho vault is non-upgradeable. Market/parameter changes require Owner multisig (2-of-5 Safe) + 3-day timelock + Guardian (Aragon DAO) veto. No single entity can unilaterally change fund-custody logic. | 9 | 9 | Non-Improvable (optimal) | [P0] [Safe API - Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xE86399fE6d7007FdEcb08A2ee1434Ee677a04433/), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- No governance-token voting for this vault; controlled by Safe multisig + Aragon Guardian. Concentration captured in S-KM-01/S-KM-03. | N/A | N/A | N/A | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. 3-day (259,200s) timelock on all market/parameter changes (meets >=24h Low criterion), plus an Aragon DAO Guardian enabling depositor veto of pending changes. Veto powers narrow and bounded. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) (timelock=259200), [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner can appoint/replace the curator role subject to timelock; withdrawals remain permissionless via ERC4626 throughout. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Governance Subtotal:**
- 3 applicable (O-G-02 = N/A): 3x9 = 27/27
- Adjusted: (27/27) x 67.5 = **67.5/67.5 (100.0%)**

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Re7 Capital is a London-based DeFi investment firm founded 2021 by Evgeny Gokhberg (Founder/Managing Partner, 14+ years investment management, 7 in crypto), ~$800M AUM. Re7 Labs is its on-chain innovation arm. Founder publicly identified with verifiable track record. (Credibility partially dented by the Nov 2025 curation failure, but identity/track record are clear.) | 9 | 9 | Non-Improvable (optimal) | [P1] [Hedgeweek - Re7 Capital](https://www.hedgeweek.com/before-the-mainstream-re7-capitals-edge/), [P1] [Re7 Capital](https://re7.capital/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Re7 Capital is an established ~$800M-AUM firm with a multi-person team running 100+ pools across 14 chains -- not a single-developer operation. Mid given that the curation/risk function showed key-person reliance and thin operational redundancy during the Nov 2025 response, but the firm has genuine team depth. | 9 | 9 | Non-Improvable (optimal) | [P1] [Hindenrank - Re7](https://hindenrank.com/blog/how-does-re7-labs-work), [P1] [Re7 Capital](https://re7.capital/) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Partial. Re7 Capital is described as London/UK-based, but the specific legal entity operating the curator (Re7 Labs entity, registration, jurisdiction mapping) is not clearly disclosed in the vault docs or forum. Morpho = ADDMO (France). Mid (3): entity/jurisdiction mentioned but legal roles only partially clear. | 3 | 9 | **Improvable** | [P1] [Hindenrank - Re7](https://hindenrank.com/blog/how-does-re7-labs-work), [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known ongoing or past material enforcement actions against Re7 Capital or Morpho entities in major jurisdictions. (The Nov 2025 event generated criticism and possible civil exposure but no disclosed regulatory enforcement action.) | 9 | 9 | Non-Improvable (optimal) | Public records, [P4] [Cryptopolitan](https://www.cryptopolitan.com/re7-labs-criticism-from-stream-insolvency/) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Mid. Re7 claims monitoring tooling and price alerts, but its Nov 2025 incident response was reactive and criticized (no timely halt of exposure; the framework's automation-override requirement to halt automated allocation within SLA is not documented). No published 24/7 on-call SLA or runbook. | 3 | 9 | **Improvable** | [P4] [CryptoRank - Re7 Criticism](https://cryptorank.io/news/feed/1c712-re7-labs-criticism-from-stream-insolvency), [P2] [Re7 USDT Forum](https://forum.morpho.org/t/re7-usdt-metamorpho-vault/518) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Mid. Re7 did publish updates during the Nov 2025 crisis but was widely criticized for "sharing a report rather than providing a solution" and slow proactive action -- inconsistent crisis support. Mid (3). | 3 | 9 | **Improvable** | [P4] [CryptoRank - Re7 Criticism](https://cryptorank.io/news/feed/1c712-re7-labs-criticism-from-stream-insolvency), [P4] [bitcoinethereumnews - backlash](https://bitcoinethereumnews.com/tech/re7-labs-update-on-stream-finance-insolvency-draws-defi-community-backlash/) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Re7 Capital operates as an identified investment firm; there is no evidence of opaque external parties exerting control over the curator's decisions. No undisclosed strategic-partner influence identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Re7 Capital](https://re7.capital/), [P1] [Token Terminal - Re7 interview](https://tokenterminal.com/resources/interview/re7capital) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Re7 manages 100+ pools across 14 chains and competing high-yield vaults. Conflicts (allocation/yield-chasing across vaults) exist with no published quantitative conflict-of-interest policy or hard constraints. Mid (3), consistent with peer curators; the demonstrated reckless curation is scored under O-TL-09. | 3 | 9 | **Improvable** | [P1] [Hindenrank - Re7](https://hindenrank.com/blog/how-does-re7-labs-work) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | YES -- High (1). Re7 was directly responsible, as curator, for ~$27.4M of bad debt in Nov 2025 (including deUSD/sdeUSD markets ON Morpho), with uncompensated/partially-compensated depositor losses (~30% haircut) and widespread criticism for materially reckless curation (accepting circular/illiquid collateral on CEO assurances). Framework High: "any uncompensated depositor losses, or history of materially reckless curation decisions." | 1 | 9 | **Improvable** (decays to 9 only with 24-36 months clean record + compensation) | [P4] [Cryptodamus - $27M Re7](https://cryptodamus.io/en/articles/news/stream-finance-collapse-27m-defi-fallout-re7-labs-under-fire), [P4] [Protos](https://protos.com/stream-finance-meltdown-winners-and-losers-in-defi-risk-curator-reckoning/) |

**Team & Legal Subtotal:**
- 9 questions: itemize 01=9,02=9,03=3,04=9,05=3,06=3,07=9,08=3,09=1 -> 4x9 (sum 36) + 4x3 (sum 12) + 1x1 (sum 1) = 49/81
- Adjusted: (49/81) x 67.5 = **40.83 ≈ 40.8/67.5 (60.5%)**

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

**NOTE: Documentation of architecture, addresses, roles, proof-of-reserves, and contract verification is platform-level (Morpho) and identical to the other Morpho V1 vault ratings. Re7's risk-framework transparency gap is captured separately in ST-PM-06 / ST-M-04, not here.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Comprehensive Morpho docs (architecture, mechanics, risks) plus a Re7 vault description / forum post explaining the mandate and risk approach. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Docs](https://docs.morpho.org/), [P2] [Re7 USDT Forum](https://forum.morpho.org/t/re7-usdt-metamorpho-vault/518) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. Morpho docs detail liquidation mechanics, bad-debt socialization, oracle and liquidity risks, and vault-specific loss conditions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Morpho docs maintain a canonical address registry (Morpho Blue, vault factories, periphery). The vault address is identified on the Morpho app. | 9 | 9 | Non-Improvable (optimal) | [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Owner/Curator/Guardian/Allocator roles and timelock durations are documented; changes are visible on-chain via Safe Tx Service and event logs. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Roles](https://docs.morpho.org/curate/concepts/roles/), [P0] [Safe API - Owner](https://api.safe.global/tx-service/eth/api/v1/safes/0xE86399fE6d7007FdEcb08A2ee1434Ee677a04433/) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves -- all vault allocations, TVL, and utilization are auditable on-chain at any time via the Morpho app and Etherscan. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0x95EeF579155cd2C5510F312c8fA39208c3Be01a8), [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. The vault, Morpho Blue singleton, factories, and periphery are all verified on Etherscan with public source. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan Vault](https://etherscan.io/address/0x95EeF579155cd2C5510F312c8fA39208c3Be01a8), [P0] [Etherscan Morpho Blue](https://etherscan.io/address/0xbbbbbbbbbb9cc5e90e3b3af64bdaf62c37eeffcb) |

**Documentation Subtotal:**
- 6 questions: 6x9 = 54/54
- Adjusted: (54/54) x 67.5 = **67.5/67.5 (100.0%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | No dedicated safety module. Bad debt is socialized among lenders within each Morpho Blue market; the Nov 2025 event demonstrated there was no backstop to absorb Re7's losses (they were passed to depositors). Morpho DAO treasury exists but activation is discretionary with no binding rules. Mid (3). | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/), [P4] [Cryptodamus](https://cryptodamus.io/en/articles/news/stream-finance-collapse-27m-defi-fallout-re7-labs-under-fire) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Insufficient. No ring-fenced Re7 reserve for this vault. Morpho DAO treasury (~$24.8M, ~100% volatile MORPHO per DeFiLlama) is ~0.17% of protocol TVL. Below 1% and dominated by a volatile native token; not ring-fenced for this vault. High (1). | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong at the operator level. Re7 Capital (~$800M AUM, 4+ years) and Morpho (~$73.6M raised, nonprofit structure) both have multi-year runway. Runway comfortably >24 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [Re7 Capital](https://re7.capital/), [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | HIGH RISK. Re7's vaults suffered structural TVL collapse and buffer depletion in the Nov 2025 contagion: ~$27.4M bad debt, ~30% haircuts on affected positions, and this vault's TVL collapsed to a residual ~$22K. Buffer depletion directly increased depositor loss. High (1). | 1 | 9 | **Improvable** (decays with demonstrated resilient recovery) | [P4] [BlockEden - $285M Contagion](https://blockeden.xyz/blog/2025/11/08/m-defi-contagion/), [P0] [Morpho GraphQL API](https://api.morpho.org/graphql) (TVL ~$22K) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue and the MetaMorpho vault are immutable / non-upgradeable; permissionless ERC4626 withdrawals are always available; the Aragon Guardian can veto pending changes. No proprietary off-chain service required for exits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Financial Resilience Subtotal:**
- 5 questions: itemize 01=3,02=1,03=9,04=1,05=9 -> 2x9 (sum 18) + 1x3 (sum 3) + 2x1 (sum 2) = 23/45
- Adjusted: (23/45) x 67.5 = **34.5/67.5 (51.1%)**

**Operations Total: 67.5 + 40.8 + 67.5 + 34.5 = 210.3/270 (77.9%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 67.5 | 67.5 | 100.0% |
| Team & Legal | 40.8 | 67.5 | 60.5% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 34.5 | 67.5 | 51.1% |
| **Operations Total** | **210.3** | **270** | **77.9%** |

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 87 | 99 | 158.2 | 180 | 87.9% |
| | Key Management (8 Q) | 54 | 72 | 135.0 | 180 | 75.0% |
| | **Security Subtotal** | | | **293.2** | **360** | **81.4%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 49 | 81 | 27.2 | 45 | 60.5% |
| | Collateral (4 Q) | 22 | 36 | 27.5 | 45 | 61.1% |
| | Infra Counterparty (8 of 11 Q scored) | 58 | 72 | 36.25 | 45 | 80.6% |
| | Protocol Counterparty (5 Q) | 39 | 45 | 39.0 | 45 | 86.7% |
| | Liquidity (9 Q) | 51 | 81 | 28.3 | 45 | 63.0% |
| | Market (5 Q) | 19 | 45 | 19.0 | 45 | 42.2% |
| | **Strategy Subtotal** | | | **177.3** | **270** | **65.7%** |
| **Operations** | Governance (3 of 4 Q scored) | 27 | 27 | 67.5 | 67.5 | 100.0% |
| | Team & Legal (9 Q) | 49 | 81 | 40.8 | 67.5 | 60.5% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 23 | 45 | 34.5 | 67.5 | 51.1% |
| | **Operations Subtotal** | | | **210.3** | **270** | **77.9%** |
| **TOTAL** | | | | **680.84** | **900** | **75.6%** |

*Total = 293.2 + 177.3 + 210.3 = 680.84 ≈ 680.8/900.*

---

