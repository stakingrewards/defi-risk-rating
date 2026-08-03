# Morpho - Ethena x Steakhouse USDG Vault (Robinhood Chain) Risk Rating

**Rating Date**: 2026-07-23
**Final Grade**: CCC+
**Total Score**: 625.4/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 308.2/360 (85.6%)

#### Smart Contract Security (20% weight, 180 max points)

**NOTE: Smart Contract Security is platform-level. The VaultV2 deployed on Robinhood Chain (via the chain's V2 factory 0x0FBad985...) is the same immutable, audited codebase used across all Morpho V2 deployments; scores match the Steakhouse USDG / Turbo USDG / mainnet V2 peers (158.2/180). Deployment-configuration concerns (oracle setup, explorer verification) are scored under ST-IC-02 and O-DT-06.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | Yes. The VaultV2 codebase and immutable Morpho Blue core are audited by >=2 Tier-0/1 firms with public reports (ChainSecurity, Spearbit, Zellic, Blackthorn, $200K Cantina competition) and Certora-formally verified; the same bytecode is deployed on Robinhood Chain via the V2 factory. Caveat: the Robinhood Chain oracle/market configuration is outside the mainnet audit scope (assessed in ST-IC-02). | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/), [P1] [ChainSecurity V2](https://www.chainsecurity.com/security-audit/morpho-vault-v2), [P0] Morpho V2 API (factory 0x0FBad985...) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Most recent V2 audits by Certora (Tier-0), Spearbit (Tier-0), ChainSecurity (Tier-0), Blackthorn. Multiple Tier-0 firms. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. VaultV2 and Morpho Blue are immutable (non-upgradeable); no upgrade path exists on this vault; every V2 component was preceded by Tier-0 audits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/), [P0] Morpho V2 API |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. V2 audit findings resolved and re-verified before deployment; Certora formal verification provides mathematical proof of critical invariants. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Audits](https://docs.morpho.org/get-started/resources/audits/) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | VaultV2 is immutable (ERC-4626); Morpho Blue is immutable. Adapter/registry/cap-increase/sendAssetsGate/abdicate changes require 7-day timelocks (verified via API); vault-ownership transfer requires the Supervisor's immutable 14-day timelock (TIMELOCK = 1,209,600s read on-chain). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (18 per-function timelocks), [P0] Supervisor TIMELOCK() via Robinhood Chain RPC |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No exploit or user-fund loss in this vault or the Morpho V2 architecture. The vault's single market shows badDebt = $0 and realizedBadDebt = $0 (verified). Steakhouse vaults recorded zero losses through the March 2026 Resolv and April 2026 rsETH events. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (badDebt=0), [P2] [Steakhouse H1 2026 Update](https://kitchen.steakhouse.financial/p/defi-markets-update-2026-07-14) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho is a nonprofit (ADDMO); Steakhouse has a multi-year clean curation record; Ethena and Paxos are established issuers. No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. Deployed 2026-06-23 with 7-day timelocks on fund-routing/cap/abdicate functions; the 0-second base on fee/allocator/penalty/gate-setter functions is the original configuration, and the three withdrawal-relevant gate setters are permanently abdicated. No timelock changes since deployment. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (timelocks verified 2026-07-23) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Cantina ($2.5M max, Morpho V2 contracts in scope) and Immunefi ($2.5M Morpho Blue). Both established platforms with payout history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3), [P1] [Immunefi](https://immunefi.com/bug-bounty/morpho/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Morpho monitoring bots + Chainalysis exist at platform level, but responses require manual intervention, no automated protective action covers this vault's allocator flows, and monitoring maturity for a ~1-month-old chain and an unlisted vault is unverified. | 3 | 9 | **Improvable** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. The sole sentinel is the Supervisor contract, whose vault-level revoke is guardian-gated — and no guardians are registered — so even manual sentinel intervention is currently inert. Morpho Blue market isolation provides containment. | 3 | 3 | Non-Improvable | [P0] RPC (sole sentinel = Supervisor; getGuardians(vault) = []), [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |

**Smart Contract Security Subtotal:**
- Raw scores: 9×9 (sum 81) + 2×3 (sum 6) = 87/99
- Adjusted: (87/99) × 180 = **158.2/180 (87.9%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

**NOTE: Verified on-chain 2026-07-23 (Robinhood Chain RPC). The vault Owner (`0x261a3b7A...`) is a CONTRACT — a VaultV2Supervisor-pattern deployment (responds to owner()/TIMELOCK()=1,209,600s/getGuardians()/pendingSupervisorOwner() exactly per the Steakhouse Supervisor ABI; same architecture the Turbo USDG rating verified) — owned by a 5-of-10 Safe (`0xD062020d...`). The Owner is also the vault's sole Sentinel. Curator = 3-of-7 Safe (`0x9023FBD6...`, signers are the known Steakhouse set incl. pitmaster.eth). This is the SINGLE BIGGEST difference from the plain Steakhouse USDG sibling (single-EOA owner, KM 80.0/180): this vault's KM scores mirror the Turbo USDG sibling's multisig-backed setup. Gates: sendShares/receiveAssets/receiveShares permanently abdicated (API-verified).**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Low risk. Admin rights are held by a diversified multisig stack: Owner = Supervisor contract (immutable 14-day timelock on vault-ownership change; two-step supervisor ownership transfer) owned by a verified 5-of-10 Safe; Curator = verified 3-of-7 Safe. No role changes since the 2026-06-23 deployment; all changes leave an on-chain trail. (Supervisor source not verified on chain-4663 explorers — captured in O-DT-06.) | 9 | 9 | Non-Improvable (optimal) | [P0] RPC: vault.owner()=0x261a3b7A (contract, TIMELOCK=1209600s); Supervisor.owner()=0xD062020d (Safe 5-of-10); vault.curator()=0x9023FBD6 (Safe 3-of-7); [P1] internal [Turbo USDG Rating](Morpho-Steakhouse-Turbo-USDG.md) (same stack verified) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. VaultV2/Morpho Blue are immutable; users have permissionless ERC-4626 redemption; adapter/registry changes carry 7-day timelocks; vault-ownership transfer requires the 5-of-10 Safe + 14-day Supervisor timelock; withdrawal gates are permanently abdicated; forceDeallocate penalty verified at 0.001%. Allocators can only move funds within the single enabled market. Deal Breaker passes at Low. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (timelocks, gates abdicated), [P0] RPC (Supervisor TIMELOCK, forceDeallocatePenalty=1e13) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Mid. Thresholds/counts are robust (curator 3-of-7; Supervisor owner 5-of-10), but (a) the curator is 3-of-7 — below the 4-of-7 Low bar for a 7-signer set — and (b) signer identities are not publicly disclosed (only pitmaster.eth attributable), so independence cannot be verified; capped at Mid per the framework and consistent with the Turbo USDG sibling's identical finding on the same Safes. | 3 | 9 | **Source Missing** | [P0] RPC: curator getThreshold=3/getOwners=7; Supervisor-owner getThreshold=5/getOwners=10; [P1] internal [Turbo USDG Rating](Morpho-Steakhouse-Turbo-USDG.md) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Low risk. No pause exists on the immutable vault or Morpho Blue, and the three withdrawal-relevant gates (sendShares, receiveAssets, receiveShares) are **permanently abdicated** (API-verified) — address-level withdrawal censorship can never be introduced. Only the non-critical deposit-side sendAssetsGate remains settable, behind a 7-day timelock. Rules public in Morpho docs. Stronger than the plain sibling, whose gates were merely unset. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (gatesConfig: abdicated=true ×3), [P1] [V2 Gates](https://docs.morpho.org/curate/concepts/gates/) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of vault assets held in non-custodial on-chain Morpho contracts (vault -> MarketV1 adapter -> USDe/USDG market). USDG's fiat reserves at Paxos are issuer custody (counterparty risk), not vault custody. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API, [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. On-chain segregation; performance and management fees are 0% with zero-address recipients (verified). No co-mingling. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (fees=0, recipients=0x0) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain enforced whitelist: one MarketV1 adapter (`0x19E02D4a...`) routing only to the whitelisted USDe/USDG Morpho market; adapter additions and the adapter registry require 7-day timelocks with on-chain event logs, controlled by the multisig-backed roles. (The absence of cap limits within the whitelist is penalized in ST-PC-03.) | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (1 adapter, timelocks), [P1] [V2 Adapter Docs](https://docs.morpho.org/curate/tutorials-v2/listing-adapters/) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Limited. The Supervisor provides guardian-veto and key-recovery rails, but NO guardians are registered for this vault, and no published, tested playbook covers key rotation, signer loss, or allocator-halt procedures for this deployment on a new chain. | 3 | 9 | **Improvable** | [P0] RPC (getGuardians(vault)=[]), [P2] [Supervisor V2 Blog](https://kitchen.steakhouse.financial/p/launching-supervisor-v2-and-migration) |

**Key Management Subtotal:**
- Raw scores: 6×9 (sum 54) + 2×3 (sum 6) = 60/72
- Adjusted: (60/72) × 180 = **150.0/180 (83.3%)**

**Security Total: 158.2 + 150.0 = 308.2/360 (85.6%)**

---

### STRATEGY (30% Weight) -- Score: 138.7/270 (51.4%)

**NOTE: Strategy is the weakest category and the driver of the CCC+ grade: 100% single-market concentration in USDe (a synthetic dollar internally rated CCC+/600.0) at 91.5% LLTV with NO enforceable caps, priced by a meta-oracle whose active feed is hardcoded 1:1 with a 16-hour permissionless correction lag, on a ~1-month-old single-sequencer L2 with no stress history and a depositor base of effectively one address.**

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | Yield is 100% borrower interest from a single on-chain market (USDe/USDG at ~90.0% utilization) — fully visible via the API, with zero rewards (avgNetApy 4.21% = avgNetApyExcludingRewards; rewards array empty) and 0% fees. Mandate-aligned: the vault's explicit purpose (name, Ethena partnership announcements) is USDG lending against Ethena collateral to seed Robinhood Chain's USDe market. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (allocations, APY, rewards=[]), [P4] [CryptoAdventure: Ethena seeds Robinhood Chain](https://cryptoadventure.com/ethena-drives-robinhood-chain-tvl-spike-as-morpho-absorbs-usdg-flows/) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Mid. With 91.5% LLTV (~8.5% buffer), 100% USDe concentration, and a 16-hour oracle-correction lag, a plausible single-shock event — a USDe depeg or Ethena counterparty failure (events the internal Ethena rating classes as severe-but-plausible) — would socialize bad debt to lenders across the entire vault. Loss is not limited to rare tail shocks. | 3 | 3 | Non-Improvable | [P0] Morpho V2 API (LLTV 91.5%, 100% USDe), [P0] meta-oracle config via RPC, [P1] internal [Ethena sUSDe Rating](Ethena-sUSDe.md) (CCC+/600.0) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. The vault is a 1.0x lender; no leverage or rehypothecation of depositor funds. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API, analytical assessment |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- the vault is a lender, not a borrower. Liquidation risk applies to borrowers. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No. Zero bad debt across all Steakhouse-curated stablecoin-lending vaults since January 2024, explicitly confirmed through H1 2026 (including ~$234M of Steakhouse-vault liquidations processed without loss). This vault's market shows $0 bad debt on-chain. Deal Breaker passes. | 9 | 9 | Non-Improvable (optimal) | [P2] [Steakhouse H1 2026 Update](https://kitchen.steakhouse.financial/p/defi-markets-update-2026-07-14), [P0] Morpho V2 API (badDebt=0) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Steakhouse publishes its curation risk framework (DDQ with internal + external review, quantitative and secondary-liquidity modeling) applied across its vaults, and Morpho V2 mechanics are formally documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Organic. Yield is on-chain borrower interest at ~90% utilization with zero incentives/emissions (avgNetApyExcludingRewards = avgNetApy = 4.21%) and 0% fees. Demand comes from USDe-collateralized USDG borrowing (carry loopers); sustainability of demand is tied to Ethena's carry regime (captured in ST-PM-09). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (utilization, APY breakdown) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Mid. Only ~$16.0M (~32% of TVL) is immediately liquid — the market's entire available liquidity (supply $159.7M − borrow $143.7M); the remaining ~68% depends on borrower repayment (rate-incentivized) in a single ~90%-utilization market on a new L2 with thin secondary liquidity. forceDeallocatableLiquidity reported at $0 via API. Matures with liquidity depth per the sibling convention. | 3 | 9 | Time-Based | [P0] Morpho V2 API (liquidityUsd $15.98M, idle $5K, forceDeallocatable $0, utilization 90.0%) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Mid. Lending interest itself cannot invert, but ~100% of borrower demand comes from USDe carry-loopers, and the collateral's value depends on Ethena's funding-rate/basis regime — an inversion would compress yield toward zero and raise collateral risk, though it would not directly turn lender yield negative. Consistent with the sibling's Mid on the same USDe-dominant dependency. | 3 | 3 | Non-Improvable | [P0] Morpho V2 API (single USDe market), [P1] internal [Ethena sUSDe Rating](Ethena-sUSDe.md) |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Mid. Three appointed allocators — a 1-of-7 Safe (single-key effective), an automation proxy contract, and an EOA — can move idle funds into the market without real-time approval; with NO caps of any kind (see ST-PC-03), allocator flows are unbounded within the single market and no automatic kill-switch exists; halting requires manual multisig action and the sentinel path is inert (no guardians). | 3 | 9 | **Improvable** | [P0] Morpho V2 API (allocators, caps), [P0] RPC (allocator Safe threshold=1) |

**Protocol Mechanics Subtotal:**
- 9 applicable (ST-PM-04 = N/A): 5×9 (sum 45) + 4×3 (sum 12) = 57/81
- Adjusted: (57/81) × 45 = **31.7/45 (70.4%)**

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | High risk. Collateral is 100% USDe — Ethena's synthetic dollar, internally rated CCC+ (Ethena sUSDe, 600.0/900) — at an aggressive 91.5% LLTV with NO exposure limits: the USDe collateral cap is the 1e18 sentinel (effectively unlimited), relative caps are 100%, and the adapter cap is unlimited. Single-asset, no tiering diversity, no hard on-chain limits — worse than the plain sibling's mixed (USDe/syrupUSDG/spUSDG) capped set. The mono-USDe design is the vault's stated purpose, capping potential at Mid. | 1 | 3 | **Improvable** | [P0] Morpho V2 API (caps: USDe absoluteCap=1e18 sentinel, relativeCap=100%), [P1] internal [Ethena sUSDe Rating](Ethena-sUSDe.md) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | Mid. Within the last 12 months USDe suffered a documented stress dislocation (Oct 10-11, 2025 liquidation cascade): ~$0.65 prints on Binance (venue-specific order-book failure) while primary/on-chain venues held near $1 with recovery within hours; USDe supply contracted ~$8.3B afterward on confidence loss. On Robinhood Chain, USDe has ~1 month of history. | 3 | 9 | Time-Based | [P4] [CoinDesk Oct 11 2025](https://www.coindesk.com/markets/2025/10/11/ethena-s-usde-briefly-loses-peg-during-usd19b-crypto-liquidation-cascade), [P4] [CoinDesk analysis](https://www.coindesk.com/markets/2025/10/13/no-ethena-s-usde-didn-t-de-peg), [P4] [Cointelegraph outflows](https://www.tradingview.com/news/cointelegraph:4bc2a9faa094b:0-ethena-s-usde-loses-8-3b-since-october-crash-amid-loss-of-confidence/) |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | N/A -- USDe is not a staking LST; depositors bear no direct slashing risk on the vault collateral (Ethena's internal staked-ETH backing is Ethena counterparty risk, covered in ST-C-01/PC-01). | N/A | N/A | N/A | Vault architecture |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | Mid. USDe on Robinhood Chain sits at the same address as on other L2s (`0x5d3a1Ff2...`), consistent with an omnichain (LayerZero OFT-style) deployment, and USDG is a proxy contract — but the native-vs-bridged issuance mechanism of both tokens on this ~1-month-old chain could not be verified from official documentation. Conservative Mid pending confirmation (consistent with the sibling's identical Source Missing finding). | 3 | 9 | **Source Missing** | [P0] RPC/API (USDe address matches cross-chain OFT deployments), [P1] internal [Steakhouse USDG Rating](Morpho-Steakhouse-USDG.md) |

**Collateral Subtotal:**
- 3 applicable (ST-C-03 = N/A): 1×1 (sum 1) + 2×3 (sum 6) = 7/27
- Adjusted: (7/27) × 45 = **11.7/45 (25.9%)**

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

**NOTE: Chain-level scores mirror the Steakhouse USDG sibling (same chain, rated 2026-07-22): Robinhood Chain is a ~1-month-old Arbitrum Orbit L2 (mainnet July 1, 2026) with a single centralized sequencer and no operating track record. ONE DOCUMENTED DEVIATION: ST-IC-02 scores 3 here versus the sibling's 1 — deeper on-chain verification shows the shared USDe/USDG oracle is correctable (see row).**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Mid. Dependencies disclosed but include non-Tier-0/1 components: Robinhood Chain (new Arbitrum Orbit L2, not on the SR chain list) and a custom Steakhouse meta-oracle whose backup "USDE / USD" feed's provider could not be identified (not a named Tier-0/1 oracle deployment). USDG (Paxos) disclosed. | 3 | 9 | Time-Based | [P0] RPC (chainId 4663), [P0] feed 0xD9B1F295 description "USDE / USD" (provider unidentified), [P4] [L2Beat Robinhood](https://l2beat.com/scaling/projects/robinhood) |
| ST-IC-02 | How redundant are oracle setups, and can oracle values be corrected under abnormal conditions? | Mid — with a material correction to the sibling ratings' record. The USDe/USDG oracle (`0xE64849bd...`) is NOT an uncorrectable constant: its 45-byte code is an EIP-1167 proxy to a Steakhouse **MetaOracleDeviationTimelock** (impl `0x6a16d6fe...`, Sourcify-verified on chain 4663). Active primary = hardcoded 1:1 (price() = exactly 1e24, feedless); backup = live "USDE / USD" feed (currently $0.99992); a **permissionless challenge switches to the backup after a >0.5% deviation persists 16 hours** (24h healing back). The correction path defeats the automatic High(1) of the mandatory hardcoded-oracle check, but a 16-hour liquidation-blind window on a depeggable synthetic at 91.5% LLTV covering 100% of the vault, plus zero redundancy per market and an unidentified backup provider, caps this at Mid. Structural — and verified immutable: the Sourcify-matched implementation ABI exposes NO owner and NO setter functions (primary/backup/threshold/timelock durations are fixed at `initialize()`; only the permissionless challenge/heal transitions can change state), and the EIP-1167 proxy is non-upgradeable, so the hardcoded primary cannot be replaced within this market; a better oracle would require deploying a new market and migrating the vault's allocation. **Flag: the Steakhouse USDG sibling rating scored this same oracle 1 ("cannot be corrected") based on the proxy's constant price without delegatecall inspection — recommend reconciliation.** | 3 | 3 | Non-Improvable | [P0] RPC: meta-oracle config (primary 0x68b60430 hardcoded, backup 0xCEe05Fd6 -> feed 0xD9B1F295 "USDE / USD" = $0.99992, threshold 0.5%, challenge 57,600s, heal 86,400s), [P0] [Sourcify impl match chain 4663](https://sourcify.dev/server/v2/contract/4663/0x6a16d6fe1ba26e6ba52fda03972b1fe2e31ca729) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Mid. No public SOC 2 Type II / ISO 27001 for Morpho Labs or Steakhouse; the Robinhood Chain sequencer operator's IT certifications for this chain are not disclosed. Paxos is a regulated issuer. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Mid. Robinhood Chain is <6 months old (mainnet July 1, 2026) with no incidents during its short operational period — per the new-protocol guidance, a data gap scores Mid rather than High. | 3 | 9 | Time-Based | [P4] [thirdweb: Robinhood Chain](https://blog.thirdweb.com/robinhood-chain-inside-the-ethereum-l2-bringing-tokenized-stocks-to-120-countries/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Mid. Robinhood Chain is ~1 month old with a single centralized sequencer; no halt >30 minutes has occurred, but there is essentially no track record to support Low. (The Base-chain halt findings from the superseded Base-vault assessment do NOT apply to this chain.) | 3 | 9 | Time-Based | [P4] [L2Beat Robinhood](https://l2beat.com/scaling/projects/robinhood), [P4] [thirdweb](https://blog.thirdweb.com/robinhood-chain-inside-the-ethereum-l2-bringing-tokenized-stocks-to-120-countries/) |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | N/A -- no staking-based collateral in this vault. | N/A | N/A | N/A | Vault architecture |
| ST-IC-07 | Are validators diverse geographically and by operator? | N/A -- no staking validator set relevant to the vault collateral; sequencer centralization is assessed under ST-IC-01/05/08. | N/A | N/A | N/A | Vault architecture |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | Mid. Users have permissionless on-chain redemption, but the chain relies on a single sequencer — a sequencer/DA failure could delay withdrawals until L1 force-inclusion via an escape hatch that is unproven on a ~1-month-old chain. | 3 | 9 | Time-Based | [P4] [L2Beat Robinhood](https://l2beat.com/scaling/projects/robinhood) |
| ST-IC-09 | How robust is the cross-chain messaging or bridge verification setup? | N/A -- the vault operates on a single chain and performs no cross-chain messaging itself (collateral bridging status assessed under ST-C-04). | N/A | N/A | N/A | Vault architecture |
| ST-IC-10 | Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting? | N/A -- no cross-chain escrow/minting performed by the vault. | N/A | N/A | N/A | Vault architecture |
| ST-IC-11 | Is the off-chain verification infrastructure resilient to data-source manipulation? | N/A -- the vault relies on no off-chain verifiers; oracle data is consumed on-chain. | N/A | N/A | N/A | Vault architecture |

**Infrastructure Counterparty Subtotal:**
- 6 applicable (ST-IC-06/07/09/10/11 = N/A): 6×3 = 18/54
- Adjusted: (18/54) × 45 = **15.0/45 (33.3%)**

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | Mid. Deployment is only into Morpho Blue (Tier-0), but 100% of collateral value depends on a single untiered counterparty — Ethena (major, >$5B, but a synthetic-dollar issuer internally rated CCC+) — with no diversification. Disclosure is full. | 3 | 3 | Non-Improvable | [P0] Morpho V2 API (single USDe market), [P1] internal [Ethena sUSDe Rating](Ethena-sUSDe.md) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Mid. Fees are 0% (verified) and the Ethena seed is publicly reported — but the vault embodies an undocumented structural conflict: **Ethena is simultaneously the ~sole depositor (99.99% of shares) and the issuer of 100% of the collateral** its deposit is lent against, bootstrapping its own token's market. The commercial terms among Ethena/Steakhouse/Robinhood are not published; conflict mitigation is described only at high level. | 3 | 9 | **Improvable** | [P0] Morpho V2 API (positions: one address holds $50.059M of $50.056M), [P4] [CryptoAdventure](https://cryptoadventure.com/ethena-drives-robinhood-chain-tvl-spike-as-morpho-absorbs-usdg-flows/) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | High risk. NO enforceable limits exist: the USDe collateral cap is the 1e18 sentinel (effectively unlimited), the relative cap is 100%, and the adapter cap is unlimited — 100% single-counterparty concentration is realized on-chain with no hard cap, unlike the plain sibling (absolute caps ~$200-500M). Concentration relies entirely on curator discretion. | 1 | 9 | **Improvable** | [P0] Morpho V2 API (caps: absoluteCap=1e18 sentinel, relativeCap=1e18, adapter cap 1e21) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Mid. Unwind depends on borrower repayment at ~90% utilization in one market; ~32% of TVL is immediately available (the market's entire free liquidity); new-chain secondary liquidity is thin; no discretionary approvals needed. Matures as liquidity deepens and exits are demonstrated. | 3 | 9 | Time-Based | [P0] Morpho V2 API (liquidityUsd $15.98M of $50.06M, utilization 90.0%) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Low risk. On-chain lending with no third-party custody of vault assets; curator (Steakhouse), USDG issuer (Paxos), collateral issuer (Ethena), and chain operator (Robinhood) all disclosed. Deal Breaker passes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho: Robinhood](https://morpho.org/blog/robinhood-chooses-morpho-to-power-new-earn-product), [P1] [USDG/Paxos](https://docs.paxos.com/guides/stablecoin/usdg) |

**Protocol Counterparty Subtotal:**
- 5 questions: 1×9 (sum 9) + 3×3 (sum 9) + 1×1 (sum 1) = 19/45
- Adjusted: (19/45) × 45 = **19.0/45 (42.2%)**

---

#### Liquidity (5% weight, 45 max points)

**Withdrawal baseline: design-implied instant/permissionless (ERC-4626), subject to underlying market liquidity. Immediate liquidity ≈ $16.0M (~32% of TVL); the single market runs ~90.0% utilization; the depositor base is effectively one address (99.99%).**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain ERC-4626 redemption; the three withdrawal-relevant gates are **permanently abdicated** (can never be set); no admin pause on the immutable vault; forceDeallocate exists as a permissionless in-kind path (penalty verified at 0.001%). Structurally stronger than the sibling (whose gates were merely unset). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (gatesConfig abdicated ×3), [P1] [V2 Gates](https://docs.morpho.org/curate/concepts/gates/) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Mid. Immediate liquidity ≈ $16.0M (~32% of $50.06M TVL) — which is the market's ENTIRE free liquidity; near-total exit depends on borrower repayment at ~90% utilization in a single market. The sole depositor (99.99%) could demand a full exit at once. Untested at scale. | 3 | 3 | Non-Improvable | [P0] Morpho V2 API (liquidityUsd, positions concentration) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | Mid. The vault is ~4.5 weeks old; no delays observed, but there is insufficient (<6-12 month) time-series to support Low — consistent with the sibling convention. | 3 | 9 | Time-Based | [P0] Morpho V2 API (creationTimestamp 1782552273 = 2026-06-23) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Low. Morpho V2 caps are allocation-side and structurally cannot gate withdrawals; cap increases require a 7-day timelock; no history of caps restricting exits. Platform-consistent with the siblings. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (caps, timelocks) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | Mid. No stress history on this new chain/vault; behavior under volatility or congestion is unknown — scored Mid per the untested principle, reachable once functional exits are demonstrated through actual stress. | 3 | 9 | Time-Based | [P0] Morpho V2 API (vault age), Scoring methodology (untested = Mid) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No structural lockups, vesting, or bridge exits on the vault position; exit depends on borrower repayment, not time-locks; forceDeallocate provides an in-kind backstop. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Primary redemption is via ERC-4626 (always available); no secondary-market dependency for exit; the vault share has no secondary market (single holder). | 9 | 9 | Non-Improvable (optimal) | Vault mechanics, [P0] Morpho V2 API |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | Mid. USDG and USDe have thin on-chain secondary depth on a ~1-month-old L2; the vault's exit capacity equals the market's $16M free liquidity (~32% of TVL); depth supports staggered rather than near-total exits. | 3 | 3 | Non-Improvable | [P0] Morpho V2 API (market state), [P4] [CryptoBriefing: Steakhouse on Robinhood Chain](https://cryptobriefing.com/steakhousefi-vaults-robinhood-chain-users/) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Mid. A "run" here is one decision: a single depositor holds 99.99% of shares, and an exit beyond ~32% of TVL would queue behind borrower repayment at ~90% utilization; the adaptive rate model and market isolation constrain permanent loss, and the sole-depositor's strategic alignment (Ethena seeding its own market) reduces run probability but concentrates it. Untested. | 3 | 3 | Non-Improvable | [P0] Morpho V2 API (positions, liquidity, utilization), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Liquidity Subtotal:**
- 9 questions: 4×9 (sum 36) + 5×3 (sum 15) = 51/81
- Adjusted: (51/81) × 45 = **28.3/45 (63.0%)**

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | Mid. The vault share (USDG-denominated ERC-4626, sharePrice 1.0014) is ~4.5 weeks old, held ~entirely by one address, and has not been tested under redemption or market stress on this new chain. | 3 | 9 | Time-Based | [P0] Morpho V2 API (sharePrice, vault age, positions) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Low. The vault lends USDG against stablecoin collateral — dollar-denominated throughout, no directional BTC/ETH beta for lenders. The risk is collateral depeg/counterparty (captured in ST-C-01/ST-IC-02/ST-PM-02), not market direction. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Low. Immutable Adaptive Curve IRM; rates rise with utilization; no governance manipulation; current ~90.0% utilization is below the >=95% prolonged-stress threshold; no incentive reflexivity (zero emissions). | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API (utilization), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Mid. Morpho liquidation is formally verified and Steakhouse does scenario modeling, but the key tail — a USDe depeg during the 16-hour oracle-challenge window at 91.5% LLTV on 100% of the vault — is not liquidation-protected during that window, leaving the dominant loss path unmitigated by modeling. | 3 | 9 | **Improvable** | [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/), [P0] meta-oracle config (RPC) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Low (borrower-side). The vault has no leverage and is not itself liquidated; lenders benefit from liquidations. The collateral-depeg/bad-debt path is captured in ST-IC-02/ST-PM-02. | 9 | 9 | Non-Improvable (optimal) | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal:**
- 5 questions: 3×9 (sum 27) + 2×3 (sum 6) = 33/45
- Adjusted: (33/45) × 45 = **33.0/45 (73.3%)**

**Strategy Total: 31.7 + 11.7 + 15.0 + 19.0 + 28.3 + 33.0 = 138.7/270 (51.4%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 31.7 | 45 | 70.4% |
| Collateral | 11.7 | 45 | 25.9% |
| Infra Counterparty | 15.0 | 45 | 33.3% |
| Protocol Counterparty | 19.0 | 45 | 42.2% |
| Liquidity | 28.3 | 45 | 63.0% |
| Market | 33.0 | 45 | 73.3% |
| **Strategy Total** | **138.7** | **270** | **51.4%** |

---

### OPERATIONS (30% Weight) -- Score: 178.5/270 (66.1%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Low risk. Core contracts (VaultV2, Morpho Blue) are immutable — fund-custody logic cannot be upgraded. Role segregation: Supervisor owner (14-day ownership timelock, 5-of-10 Safe), 3-of-7 curator Safe (7-day timelocks on fund-routing), bounded allocators. Withdrawal gates permanently abdicated. No single entity can unilaterally change custody logic. Materially stronger than the plain sibling's single-EOA owner (which scored Mid). | 9 | 9 | Non-Improvable (optimal) | [P0] RPC (Supervisor + Safes verified), [P0] Morpho V2 API (timelocks, gates) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | N/A -- no governance token or on-chain voting; multisig concentration captured under S-KM-01/03. | N/A | N/A | N/A | [P0] RPC |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Mid. Fund-routing functions carry 7-day timelocks and vault-ownership transfer 14 days — but fee functions, fee recipients, setIsAllocator, and the force-deallocate penalty have 0-second timelocks, and the veto layer is INERT: the sole sentinel is the Supervisor, whose vault-level revoke is guardian-gated while zero guardians are registered — no party can currently veto a pending timelocked action except by the owner replacing the curator within the window. Weaker than the plain sibling's functioning 1-of-7 Safe sentinel. | 3 | 9 | **Improvable** | [P0] Morpho V2 API (18 timelocks; sole sentinel = Supervisor), [P0] RPC (getGuardians=[]) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Low risk. The Supervisor owner (5-of-10 Safe) can replace the curator (setCurator, no timelock) while withdrawals remain permissionless throughout (ERC-4626; gates abdicated). | 9 | 9 | Non-Improvable (optimal) | [P0] RPC (Supervisor interface), [P1] [V2 Roles](https://docs.morpho.org/curate/concepts/roles/) |

**Governance Subtotal:**
- 3 applicable (O-G-02 = N/A): 2×9 (sum 18) + 1×3 (sum 3) = 21/27
- Adjusted: (21/27) × 67.5 = **52.5/67.5 (77.8%)**

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Low risk. Steakhouse (adcv, Sebastien Derivaux — ex-MakerDAO), Morpho (Paul Frambot et al.), Robinhood (US public company, chain operator), Paxos (regulated USDG issuer), and Ethena (public team, collateral issuer/seeder) are all publicly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse](https://www.steakhouse.financial/), [P1] [Morpho](https://morpho.org/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | Low risk. Multiple substantial organizations (Morpho, Steakhouse, Robinhood, Paxos, Ethena) support the product; no single-developer dependency. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Low risk. Morpho (ADDMO/Morpho Labs, France), Steakhouse (Panama/Cayman), Robinhood (US), Paxos Digital Singapore (USDG, MAS-regulated). Entities and jurisdictions clearly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Legal Notice](https://morpho.org/legal-notice/), [P1] [USDG/Paxos](https://docs.paxos.com/guides/stablecoin/usdg) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | Mid. Curator/infra (Steakhouse/Morpho) are clean, but entities integral to this product have past resolved enforcement: Robinhood Crypto (NYDFS $30M, 2022) and Paxos (NYDFS BUSD wind-down, 2023). No ongoing material action impairing this product. Deal Breaker passes. Consistent with the sibling. | 3 | 3 | Non-Improvable | [P4] Public regulatory records (Robinhood Crypto NYDFS 2022; Paxos BUSD 2023), [P1] internal [Steakhouse USDG Rating](Morpho-Steakhouse-USDG.md) |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Mid. Platform monitoring exists, but no public 24/7 on-call SLA or incident runbook covers this vault's allocator flows on a new chain, including steps to halt allocation (the sentinel path is inert). | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Low risk. Morpho/Steakhouse have demonstrated rapid incident response (April 2025: 4-minute rollback) and publish frequent updates (Kitchen newsletter); the effective counterparties here (Ethena/Robinhood) are large organizations with dedicated channels. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P2] [Steakhouse Kitchen](https://kitchen.steakhouse.financial/p/defi-markets-update-2026-07-14) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Low risk. Morpho's investors are public; the Robinhood/Morpho/Steakhouse arrangement is publicly announced; Ethena's role as collateral issuer and seeder is publicly reported. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho: Robinhood](https://morpho.org/blog/robinhood-chooses-morpho-to-power-new-earn-product), [P4] [CryptoAdventure](https://cryptoadventure.com/ethena-drives-robinhood-chain-tvl-spike-as-morpho-absorbs-usdg-flows/) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Mid. Steakhouse curates THREE USDG vaults on this chain alone (Steakhouse USDG ~$170M, Turbo USDG, and this vault) competing for the same borrower demand, plus the structural conflict of curating a vault whose sole depositor is also its sole collateral issuer. DDQ provides qualitative controls but no published hard conflict rules. | 3 | 9 | **Improvable** | [P1] internal [Steakhouse USDG Rating](Morpho-Steakhouse-USDG.md), [P0] Morpho V2 API (positions) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | Low risk. Zero bad debt across all Steakhouse-curated vaults since inception (Jan 2024), reconfirmed for H1 2026 through the Resolv/rsETH events and ~$234M of own-vault liquidations. | 9 | 9 | Non-Improvable (optimal) | [P2] [Steakhouse H1 2026 Update](https://kitchen.steakhouse.financial/p/defi-markets-update-2026-07-14), [P2] [$238M Liquidations Analysis](https://kitchen.steakhouse.financial/p/238m-liquidations-of-onchain-lending) |

**Team & Legal Subtotal:**
- 9 questions: 6×9 (sum 54) + 3×3 (sum 9) = 63/81
- Adjusted: (63/81) × 67.5 = **52.5/67.5 (77.8%)**

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

**NOTE: Documentation scores 45.0/67.5 — BELOW the siblings' 67.5 — on three verified, vault-specific gaps: the vault is UNLISTED on Morpho (`listed: false`, absent from the Morpho app and docs registry), has no vault-specific documentation anywhere, and its Supervisor/oracle/Safe contracts are not source-verified on chain-4663 public explorers (only the meta-oracle implementation has a Sourcify match).**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Mid. Morpho V2 platform docs are comprehensive and Steakhouse's general risk framework is public, but there is NO vault-specific documentation for this $50M product — no product page, no mandate document, no risk disclosure; its existence and purpose are documented only in third-party news coverage and on-chain data. vaults.fyi labels it "NOT RATED — too new". | 3 | 9 | **Improvable** | [P3] [vaults.fyi page](https://app.vaults.fyi/opportunity/robinhood/0xbEeFF0fb1Dc19344A87b8479dAb60A2e16160737), [P1] [Steakhouse docs](https://www.steakhouse.financial/docs) (no page for this vault) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Low risk. Morpho platform docs cover liquidation/bad-debt mechanics and V2 security considerations; Ethena publishes USDe risk documentation; the loss mechanics of this vault (91.5% LLTV lending, per-market socialized bad debt) are the standard documented Morpho model. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Mid. The vault is **listed: false** on Morpho — absent from the Morpho app and the docs address registry; the Supervisor, meta-oracle stack, and Safes are not consolidated in any canonical public registry. Addresses are discoverable only via the API/RPC/vaults.fyi. Consistent with the Turbo sibling's Mid for unregistered deployments. | 3 | 9 | **Improvable** | [P0] Morpho V2 API (listed=false), [P3] [vaults.fyi](https://app.vaults.fyi/opportunity/robinhood/0xbEeFF0fb1Dc19344A87b8479dAb60A2e16160737) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Low risk. Morpho V2 role/timelock documentation is comprehensive; all 18 per-function timelocks and role assignments are on-chain queryable via the API with event history; the Supervisor pattern is documented by Steakhouse. | 9 | 9 | Non-Improvable (optimal) | [P1] [Roles & Capabilities](https://docs.morpho.org/curate/concepts/roles/), [P0] Morpho V2 API, [P2] [Supervisor V2 Blog](https://kitchen.steakhouse.financial/p/launching-supervisor-v2-and-migration) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Low risk. Full on-chain proof-of-reserves (vault position, market state, bad debt auditable in real time); USDG reserves attested monthly by Paxos; Ethena publishes USDe proof-of-reserves. Deal Breaker passes. | 9 | 9 | Non-Improvable (optimal) | [P0] Morpho V2 API, [P1] [USDG/Paxos](https://docs.paxos.com/guides/stablecoin/usdg) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Mid. The deployed logic corresponds to public, audited open-source code, and the MetaOracleDeviationTimelock implementation has a Sourcify exact-match on chain 4663 — but the vault, adapter, Supervisor, both Safes, the primary/backup oracles, and the USDE/USD feed have NO Sourcify match on chain 4663, and explorer-level verification could not be confirmed (the chain's Blockscout API was unreachable programmatically). Consistent with the Turbo sibling's Mid ("hoodexplorer: source not verified"). | 3 | 9 | **Improvable** | [P0] Sourcify chain-4663 checks (impl 0x6a16d6fe = match; vault/adapter/Supervisor/oracles = none), [P1] internal [Turbo USDG Rating](Morpho-Steakhouse-Turbo-USDG.md) |

**Documentation Subtotal:**
- 6 questions: 3×9 (sum 27) + 3×3 (sum 9) = 36/54
- Adjusted: (36/54) × 67.5 = **45.0/67.5 (66.7%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Mid. No dedicated safety module; bad debt is socialized among market lenders. The Morpho DAO treasury is discretionary; no Steakhouse/Ethena/Robinhood-specific backstop is disclosed for this vault. | 3 | 9 | **Improvable** | [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/), [P3] [DeFiLlama Treasury](https://api.llama.fi/treasury/morpho) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | High risk. The Morpho DAO treasury is ~$26.6M per DeFiLlama (2026-07-23), ~100% MORPHO own-token ($25.5M Base + $1.1M Ethereum; ~$2.3K non-native) — <1% of Morpho's multi-billion protocol TVL, dominated by the volatile native token (independently meeting the High criterion), and not ring-fenced for this vault. No dedicated liquid reserve disclosed. | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama Treasury API](https://api.llama.fi/treasury/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Low risk. Morpho is well-funded ($73.6M raised, nonprofit); Steakhouse earns curation revenue across ~$1.70B of deposits (this vault charges 0%); Robinhood and Ethena are large, well-capitalized organizations. Runway comfortably >24 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/), [P2] [Steakhouse H1 2026 Update](https://kitchen.steakhouse.financial/p/defi-markets-update-2026-07-14) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | Mid. The vault is ~4.5 weeks old and has not operated through any stress event; its TVL is a single partner's seed deposit (not organic diversified demand), so no resilience is demonstrated. The vault token is not composed into external protocols, limiting contagion surface. | 3 | 9 | Time-Based | [P0] Morpho V2 API (vault age, TVL, positions), [P4] [CryptoAdventure](https://cryptoadventure.com/ethena-drives-robinhood-chain-tvl-spike-as-morpho-absorbs-usdg-flows/) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Mid. VaultV2/Morpho Blue are immutable and withdrawals permissionless (gates abdicated), but continued chain operation depends on Robinhood running the single sequencer; if abandoned, exit relies on an unproven L1 force-inclusion escape hatch on a ~1-month-old chain. Consistent with the sibling. | 3 | 9 | Time-Based | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P4] [L2Beat Robinhood](https://l2beat.com/scaling/projects/robinhood) |

**Financial Resilience Subtotal:**
- 5 questions: 1×9 (sum 9) + 3×3 (sum 9) + 1×1 (sum 1) = 19/45
- Adjusted: (19/45) × 67.5 = **28.5/67.5 (42.2%)**

**Operations Total: 52.5 + 52.5 + 45.0 + 28.5 = 178.5/270 (66.1%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 52.5 | 67.5 | 77.8% |
| Team & Legal | 52.5 | 67.5 | 77.8% |
| Documentation | 45.0 | 67.5 | 66.7% |
| Financial Resilience | 28.5 | 67.5 | 42.2% |
| **Operations Total** | **178.5** | **270** | **66.1%** |

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 87 | 99 | 158.2 | 180 | 87.9% |
| | Key Management (8 Q) | 60 | 72 | 150.0 | 180 | 83.3% |
| | **Security Subtotal** | | | **308.2** | **360** | **85.6%** |
| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 57 | 81 | 31.7 | 45 | 70.4% |
| | Collateral (3 of 4 Q scored) | 7 | 27 | 11.7 | 45 | 25.9% |
| | Infra Counterparty (6 of 11 Q scored) | 18 | 54 | 15.0 | 45 | 33.3% |
| | Protocol Counterparty (5 Q) | 19 | 45 | 19.0 | 45 | 42.2% |
| | Liquidity (9 Q) | 51 | 81 | 28.3 | 45 | 63.0% |
| | Market (5 Q) | 33 | 45 | 33.0 | 45 | 73.3% |
| | **Strategy Subtotal** | | | **138.7** | **270** | **51.4%** |
| **Operations** | Governance (3 of 4 Q scored) | 21 | 27 | 52.5 | 67.5 | 77.8% |
| | Team & Legal (9 Q) | 63 | 81 | 52.5 | 67.5 | 77.8% |
| | Documentation (6 Q) | 36 | 54 | 45.0 | 67.5 | 66.7% |
| | Financial Resilience (5 Q) | 19 | 45 | 28.5 | 67.5 | 42.2% |
| | **Operations Subtotal** | | | **178.5** | **270** | **66.1%** |
| **TOTAL** | | | | **625.4** | **900** | **69.5%** |

*Total = 308.2 + 138.7 + 178.5 = 625.4.*

---

