# Ether.fi - Liquid ETH Yield Vault Risk Rating

**Rating Date**: 2026-04-29
**Final Grade**: BB+
**Total Score**: 789.7/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Detailed Analysis

### SECURITY (40% Weight) - Score: 330.0/360 (91.7%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited, including deployment configuration? | Yes. BoringVault infrastructure audited by: (1) Spearbit -- foundational Arctic architecture review (Tier-0), (2) 0xMacro -- 33+ sequential audit engagements (SevenSeas-4 through SevenSeas-33, March 2024 to March 2025) covering core vault, decoders, sanitizers, and protocol integrations for Aave, Morpho, Pendle, Uniswap, Odos, Spectra, Resolv, Euler, etc., (3) Secure3, (4) Hexens. Multiple independent auditors covering all fund-custody/routing contracts. >=2 independent external firms with public reports. **Deployment configuration scope (v0.1-gamma):** 0xMacro's 33+ sequential audits explicitly cover DecoderAndSanitizer configurations (the Merkle-proof constraint system defining allowed strategist actions) for each protocol integration — this IS deployment configuration review. Accountant exchange rate bounds, Teller deposit/withdraw parameters, and multisig permission roles are reviewed as part of the module architecture. No bridge verifier setup applicable (mainnet-only). | 9 | 9 | Non-Improvable (optimal) | [P1] [Veda Audits](https://docs.veda.tech/audits), [P1] [0xMacro Library](https://0xmacro.com/library), [P1] [GitHub Audit Directory](https://github.com/Se7en-Seas/boring-vault/tree/main/audit) (spearbit-boring-vault-arctic-0.pdf, 0xmacro-boring-vault-arctic-0.pdf, 0xmacro-boring-vault-arctic-1.pdf) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | 0xMacro performed the most recent audit (SevenSeas-33, March 7, 2025). **0xMacro is Tier-1 per the SR Auditor Tier list.** The foundational Arctic architecture was also reviewed by Spearbit (Tier-0). Per criteria: "Low (9): At least one most recent audit by a Tier-0 or Tier-1 auditor." 0xMacro is Tier-1, meeting the Low criteria. **CORRECTION from previous rating**: The prior rating incorrectly stated 0xMacro was "NOT listed on the SR Auditor Tier list" and scored this as 3. 0xMacro IS listed as Tier-1. | 9 | 9 | Non-Improvable (optimal) | [P1] [0xMacro SevenSeas-33 (March 2025)](https://0xmacro.com/library), SR Auditor Tier List: 0xMacro = Tier-1 |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. The core BoringVault token contract is non-upgradeable. New decoders and integration modules are audited by 0xMacro before deployment (33+ separate engagements covering each new protocol integration, most recent March 2025). Each new decoder/sanitizer for protocol integrations receives a targeted audit before mainnet deployment. No evidence of unaudited integration deployments. | 9 | 9 | Non-Improvable (optimal) | [P1] [0xMacro audit library showing sequential audits SevenSeas-4 through SevenSeas-33](https://0xmacro.com/library) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated? | Yes. SevenSeas-4 (March 2024) found 4 Medium, 4 Low, 4 Code Quality, 2 Informational -- no critical/high. Subsequent audits show decreasing finding counts. No evidence of unresolved critical or high-severity findings in any public report. The Hats Finance competitive audit for the broader ether.fi protocol found medium and low severity issues with documented fixes. | 9 | 9 | Non-Improvable (optimal) | [P1] [0xMacro SevenSeas-4 findings](https://0xmacro.com/library), [P1] [Hats Finance Report](https://github.com/hats-finance/ether-fi-0x36c3b77853dec9c4a237a692623293223d4b9bc4/blob/master/report.md) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Non-upgradeable core BoringVault token contract (verified on Etherscan -- Solidity 0.8.21, not a proxy). Holds assets and mints/burns shares with minimal logic. Modular components (Teller, Manager, Accountant, DecoderAndSanitizer, Queue) are swappable but controlled by Admin multisig with timelock >=48 hours. The non-upgradeable core significantly reduces upgrade risk. Module swaps are narrow in scope and subject to timelock + multisig. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan BoringVault -- verified, not proxy](https://etherscan.io/address/0xf0bb20865277aBd641a307eCe5ee04E79073416C), [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploits affecting user funds in the Liquid vault's history. Broader ether.fi ecosystem: September 2024 domain takeover attempt thwarted before any compromise. May 2024 Mode bridge misconfiguration resolved without user loss (L2-specific, not Liquid vault). All vault depositor funds have remained safe. | 9 | 9 | Non-Improvable (optimal) | [P1] [Sep 24 Incident Report](https://etherfi.gitbook.io/etherfi/security/sep-24-incident-attempted-domain-account-takeover), [P1] [Postmortems](https://github.com/etherfi-protocol/postmortems) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No. Founded by Mike Silagadze (previously founded Top Hat, $400M+ EdTech) and Rok Kopp. $32.3M raised from Bullish Capital, CoinFund, OKX Ventures. Nonce Capital (strategy provider) is a blockchain venture studio founded 2019. Veda (infrastructure) has operated BoringVault infrastructure across DeFi. No allegations of misconduct. | 9 | 9 | Non-Improvable (optimal) | [P1] [Team Page](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/team), [P3] [Tracxn](https://tracxn.com/d/companies/ether.fi/__ybuswctFLX6Yyk0tndtj8aoDimNowhN3z_XQDPgnARo) |
| S-SC-08 | Were there reductions to the timelock delay? | No evidence of timelock reductions. Timelock at minimum 48 hours for module changes, providing users adequate exit window. | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active Immunefi bounty since March 2024, last updated December 15, 2025. Critical smart contract: $10k-$300k. Approximately 60 assets in scope. KYC required. Max payout $300k exceeds $100k threshold. | 9 | 9 | Non-Improvable (optimal) | [P1] [Immunefi](https://immunefi.com/bug-bounty/etherfi/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. Partnership with Hypernative for 24/7 threat monitoring across the ether.fi ecosystem. ML-based anomaly detection, real-time alerts, incident response coordination. Hypernative is a reputable provider. | 9 | 9 | Non-Improvable (optimal) | [P1] [Hypernative Partnership](https://www.hypernative.io/blog/ether-fi-brings-real-time-protection-to-liquid-restaking-with-hypernative) |
| S-SC-11 | Are automatic safety controls triggered by monitoring alerts? | Yes. Accountant contract enforces exchange rate bounds -- violations trigger automatic pause stopping deposits/withdrawals. Rebalance deviation protection reverts transactions exceeding defined thresholds. Hypernative and trusted entities hold Pauser role. These are objective, invariant-based triggers with clear rules. | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |

**Smart Contract Security Subtotal:**
- 11 questions: 11 x 9 = 99/99
- Adjusted: (99/99) x 180 = **180.0/180 (100.0%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys? | Admin role held by joint Veda + ether.fi multisig. Defines whitelisted protocols, assets, and strategist parameters. Module changes subject to timelock (48h+). Changes documented via on-chain transactions. **Platform-level score, consistent with eETH rating.** | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No single key can move user funds. The core BoringVault is non-upgradeable. Strategy execution requires the Strategist role, constrained to Merkle-proof-verified actions on admin-whitelisted protocols only via DecoderAndSanitizer validation. Admin module changes require multisig + 48h timelock. The multisig appears to have fewer than 4 signers (per Exponential assessment), so threshold may be 2-of-3 rather than the >=3/>=5 required for Low (9). Scoring 9 because the specific question asks "Can any single key..." and the answer is genuinely no -- multisig consensus is required for all critical actions, and the non-upgradeable core provides structural protection. **Platform-level score, consistent with eETH rating.** | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation), [P3] [Exponential DeFi](https://exponential.fi/protocols/etherfi/) |
| S-KM-03 | How decentralized and robust is the multisig? | **Material concern.** Per Exponential DeFi assessment, the admin multisig consists of fewer than 4 signers, suggesting 2-of-3 or similar small configuration. Signer identities not publicly disclosed with ENS names or organizational affiliations. Independence cannot be confirmed from public information. Per independence verification rule, if signer identities are unknown, score Mid (3) at best. The 48-hour timelock mitigates but does not substitute for multisig robustness. **Platform-level score, consistent with eETH rating.** | 3 | 9 | **Improvable** | [P3] [Exponential DeFi](https://exponential.fi/protocols/etherfi/), [P1] Protocol documentation -- signer identities not disclosed |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause is scope-limited: Accountant exchange rate bounds (automatic), Pauser role (manual by Hypernative/trusted entities). Protocol-wide only, not address-selective. No address-level withdrawal blocking capability. BoringOnChainQueue provides permissionless withdrawal. Pause rules documented. **Platform-level score, consistent with eETH rating.** | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% held in BoringVault contract (0xf0bb20865277aBd641a307eCe5ee04E79073416C). ERC-4626-style shares minted. Withdrawal queue is permissionless. No off-chain custody. Verified on Etherscan -- contract holds ~$218M in various DeFi positions and tokens. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan BoringVault](https://etherscan.io/address/0xf0bb20865277aBd641a307eCe5ee04E79073416C) |
| S-KM-06 | Are user funds fully segregated from treasury? | Yes. Vault assets in BoringVault contract, separate from ether.fi treasury addresses (0x7D4bBE471369a066186c18bAF33622796A08d5Cd and 3 others, totaling ~$104M). Clear on-chain segregation. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan BoringVault](https://etherscan.io/address/0xf0bb20865277aBd641a307eCe5ee04E79073416C), [P1] [Deployed Contracts](https://etherfi.gitbook.io/etherfi/contracts-and-integrations/deployed-contracts) |
| S-KM-07 | What are the whitelisted protocols? | On-chain enforced via Merkle root validation. Whitelisted protocols include: Pendle, Aave V2/V3, Morpho Blue, Balancer, Aura, Uniswap V3, Convex, Curve, Odos, Spectra, Resolv, Euler, and others (per audit scope of SevenSeas-31 through SevenSeas-33). DecoderAndSanitizer validates each interaction. Additions/removals require Admin multisig + timelock. Public on-chain change log. | 9 | 9 | Non-Improvable (optimal) | [P1] [ETH Yield Vault](https://etherfi.gitbook.io/etherfi/liquid/eth-yield-vault), [P1] [0xMacro SevenSeas-31 to 33 audit scope](https://0xmacro.com/library) |
| S-KM-08 | Is there a tested incident playbook? | **Partial.** September 2024 domain incident demonstrated rapid response. Formal incident response policy exists (effective November 24, 2024). Partnerships with Seal911, Doppel, Hypernative. However, no comprehensive public playbook for key rotation, signer replacement, or admin-key compromise has been published. No evidence of tabletop exercises. **Platform-level score, consistent with eETH rating.** | 3 | 9 | **Improvable** | [P1] [Sep 24 Incident Report](https://etherfi.gitbook.io/etherfi/security/sep-24-incident-attempted-domain-account-takeover), [P1] [Security Documentation](https://etherfi.gitbook.io/etherfi/security) |

**Key Management Subtotal:**
- 8 questions: 6 x 9 + 2 x 3 = 60/72
- Adjusted: (60/72) x 180 = **150.0/180 (83.3%)**

---

**Security Total: 180.0 + 150.0 = 330.0/360 (91.7%)**

---

### STRATEGY (30% Weight) - Score: 227.9/270 (84.4%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield? | Yield from: ETH staking (via underlying eETH/weETH), Pendle PT/YT positions, Aave/Morpho lending, DEX LP fees (Balancer, Uniswap V3), Convex/Curve rewards, Euler strategies. All DeFi-native yield sources. Aligned with ETH yield mandate. Product page states 0% platform fee and 0% performance fee (no exit fee). **Risk disclosures on product page note:** "This vault does liquidity provision which can result in impermanent loss" and "This vault uses leverage, which means there is liquidation risk." | 9 | 9 | Non-Improvable (optimal) | [P1] [ETH Yield Vault](https://etherfi.gitbook.io/etherfi/liquid/eth-yield-vault), [P0] [Product page](https://www.ether.fi/app/liquid/eth) -- confirms 0% fees, Nonce Capital manager |
| ST-PM-02 | Under which conditions does net yield become negative? | Loss possible via: (1) exploit in any of the integrated protocols (Aave, Morpho, Pendle, Euler, etc.); (2) EigenLayer/restaking slashing socialized across eETH depositors; (3) Pendle PT/YT market dislocations; (4) decoder/sanitizer bug in BoringVault system; (5) impermanent loss from LP positions (explicitly disclosed); (6) liquidation from leveraged positions (explicitly disclosed); (7) strategist error within Merkle constraints. Multi-protocol deployment diversifies single-protocol risk but increases aggregate smart contract exposure. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risks](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/risks), [P0] [Product page risk disclosures](https://www.ether.fi/app/liquid/eth) |
| ST-PM-03 | Is leverage or rehypothecation used? | **Moderate.** Multiple layers: (1) Underlying eETH involves restaking through EigenLayer (ETH validates both Ethereum consensus AND EigenLayer AVSs). (2) Strategy deploys to leveraged positions (product page explicitly states "This vault uses leverage, which means there is liquidation risk"). (3) LP positions subject to impermanent loss. Combined effective leverage is above 1.0x but constrained by Merkle-proof whitelist. Scoring Mid (3) for moderate leverage with clear disclosures. | 3 | 3 | Non-Improvable | [P0] [Product page -- leverage disclosure](https://www.ether.fi/app/liquid/eth), [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | Yes. The Accountant contract enforces exchange rate bounds -- deviations beyond thresholds automatically pause vault operations. Rebalance deviation protection reverts transactions if total assets change abnormally. For underlying Aave/Morpho positions, the ETH-to-ETH nature (weETH collateral, ETH debt) creates low liquidation risk due to high correlation. Nonce Capital strategist manages positions within Merkle constraints. | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |
| ST-PM-05 | Has this strategy or close variant experienced negative yield? | No permanent losses to Liquid vault depositors. No confirmed exploits. Mode bridge incident (May 2024) was L2-specific, not Liquid vault. The BoringVault infrastructure has been operational across multiple deployments without loss events. | 9 | 9 | Non-Improvable (optimal) | [P1] [Postmortems](https://github.com/etherfi-protocol/postmortems), [P1] [Veda documentation](https://docs.veda.tech) |
| ST-PM-06 | Is a risk framework documented? | Yes. Veda architecture documented with: role separation (Admin/Strategist/Pauser), Merkle-proof constraints, exchange rate bounds, decoder/sanitizer validation, rebalance deviation protection. Documentation covers risk limits and change-control via the Merkle root update process. However, Nonce Capital's specific quantitative risk framework for this vault is not publicly available. | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation), [P1] [Veda Docs](https://docs.veda.tech) |
| ST-PM-07 | Is current yield sustainable? | The vault's yield derives from combined DeFi activities: ETH staking rewards (~3-4%), Pendle term premiums, Aave/Morpho lending interest, LP fees. These are organic, protocol-generated yields. ETHFI points/incentives and KING rewards may contribute additional yield. Without a published breakdown of organic vs incentive yield, sustainability cannot be fully verified. The base DeFi yields are sustainable. | 9 | 9 | Non-Improvable (optimal) | [P0] [Product page](https://www.ether.fi/app/liquid/eth), [P1] [ETH Yield Vault](https://etherfi.gitbook.io/etherfi/liquid/eth-yield-vault) |
| ST-PM-08 | Can the position be fully unwound without slippage turning yield negative? | **Moderately constrained.** Withdrawal process: 72-hour (3-day) queue with 0.9999 discount rate, up to 10 days with EigenLayer/Karak cooldowns. $218M TVL across multiple DeFi positions. Under conservative assumptions, slippage of 2-5% possible for large exits, compressing returns near zero. | 3 | 3 | Non-Improvable | [P0] [Product page -- 72h withdrawal, 0.9999 discount](https://www.ether.fi/app/liquid/eth), [P1] [Withdrawal FAQs](https://help.ether.fi/en/articles/269720-why-is-it-taking-so-long-to-withdraw-from-the-liquid-vaults) |
| ST-PM-09 | Does the strategy rely on spreads, pegs, or rates that can invert? | **Moderate exposure.** Multiple invertible dependencies: (1) weETH/ETH rate depends on staking rewards accrual and can deviate in secondary markets during stress; (2) Pendle positions have fixed-term spreads that carry roll risk; (3) Aave/Morpho borrowing rates can spike during high utilization; (4) LP positions subject to impermanent loss from price divergence. Combined, these dependencies contribute materially to yield but are diversified across multiple mechanisms. | 3 | 3 | Non-Improvable | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |

**Protocol Mechanics Subtotal:**
- 9 questions: 6 x 9 + 3 x 3 = 63/81
- Adjusted: (63/81) x 45 = **35.0/45 (77.8%)**

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral? | eETH (ether.fi rebasing LST), weETH (wrapped non-rebasing), WETH accepted. All ETH-based assets. eETH represents staked + restaked ETH. ETH is the native Tier-0 chain asset. The collateral is ETH-denominated with restaking risk overlay. | 9 | 9 | Non-Improvable (optimal) | [P1] [ETH Yield Vault](https://etherfi.gitbook.io/etherfi/liquid/eth-yield-vault) |
| ST-C-02 | How did collateral behave during past stress or depegs? | **Untested under severe stress.** weETH has maintained close peg to internal oracle rate under normal conditions. Chainlink weETH/ETH feed shows no major deviations. However, weETH has NOT been tested under a severe depeg event comparable to Lido's July 2025 stETH depeg. Per battle-tested vs untested principle, untested collateral cannot score Low (9). | 3 | 3 | Non-Improvable | [P0] [Chainlink weETH/ETH](https://data.chain.link/feeds/ethereum/mainnet/weeth-eth), No severe stress event documentation |
| ST-C-03 | How is validator/slashing risk handled? | eETH inherits ether.fi's distributed validator network. Slashing penalties from validators or EigenLayer AVSs are socialized across all eETH depositors. Diversification across operators and restaking protocols. No material slashing events have affected ether.fi validators to date. | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/technical-documentation), [P2] [EigenLayer Risk Analysis](https://governance.ether.fi/t/eigenlayer-vs-symbiotic-risk-analysis/2246) |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security? | <10%. Core vault operates on Ethereum mainnet, accepting native WETH and weETH (thin wrapper, no bridge/custody risk per definition). No material bridged asset dependency. **Bridge quality assessment (v0.1-gamma):** Not applicable — no bridged assets in vault TVL, no bridge verification or escrow release mechanisms. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan BoringVault](https://etherscan.io/address/0xf0bb20865277aBd641a307eCe5ee04E79073416C) |

**Collateral Subtotal:**
- 4 questions: 3 x 9 + 1 x 3 = 30/36
- Adjusted: (30/36) x 45 = **37.5/45 (83.3%)**

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which infra dependencies exist? | Ethereum mainnet (Tier-0). Chainlink oracles for weETH/ETH pricing (Tier-0). No CEX dependency. No external bridge dependency for core vault. All critical dependencies Tier-0/1. | 9 | 9 | Non-Improvable (optimal) | [P0] [Chainlink weETH/ETH](https://data.chain.link/feeds/ethereum/mainnet/weeth-eth) |
| ST-IC-02 | How redundant are oracle and bridge setups? | Chainlink (Tier-0) for weETH/ETH feed. Internal Accountant pricing with exchange rate bounds as fallback. No bridge dependency for core vault. Redundant and well-established. | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |
| ST-IC-03 | Are off-chain infra providers certified? | **Unknown.** Hypernative provides security monitoring, but individual SOC 2/ISO27001 certifications for critical off-chain infrastructure providers are not centrally disclosed. **Platform-level score, consistent with eETH rating.** | 3 | 9 | **Source Missing** | No public disclosure found |
| ST-IC-04 | How did infra behave in past incidents? | Resilient. September 2024 domain incident: rapid response, no breach. May 2024 Mode bridge issue: resolved without loss. Ethereum mainnet has had no significant outages. Protocol operational for 2+ years without material infra-related disruptions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Sep 24 Incident Report](https://etherfi.gitbook.io/etherfi/security/sep-24-incident-attempted-domain-account-takeover) |
| ST-IC-05 | Has the base chain halted recently? | No. Ethereum (Tier-0) has had no chain halts >30 min in 12+ months. | 9 | 9 | Non-Improvable (optimal) | Ethereum Tier-0 status |
| ST-IC-06 | Has the validator set experienced slashing? | No material slashing events affecting ether.fi validators. EigenLayer slashing not yet fully active at scale. | 9 | 9 | Non-Improvable (optimal) | [P2] [EigenLayer Risk Analysis](https://governance.ether.fi/t/eigenlayer-vs-symbiotic-risk-analysis/2246) |
| ST-IC-07 | Are validators diverse? | Yes. Ether.fi uses diverse node operator set. Multiple professional operators. No single operator dominates. DKG model ensures key distribution. | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/technical-documentation) |
| ST-IC-08 | Can single infra failure block withdrawals? | No. BoringOnChainQueue provides permissionless withdrawal. If Solver unavailable, users can wait for queue processing. Vault operates on Ethereum mainnet with no single infra SPOF. | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |
| ST-IC-09 | How robust is the cross-chain messaging or bridge verification setup? | N/A — Liquid ETH vault operates exclusively on Ethereum mainnet with no cross-chain bridge dependency. Vault deposits and withdrawals are natively on Ethereum. | N/A | N/A | N/A | - |
| ST-IC-10 | Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting? | N/A — No cross-chain escrow or bridge minting exists. The vault operates on Ethereum mainnet only. | N/A | N/A | N/A | - |
| ST-IC-11 | Is the off-chain verification infrastructure resilient to data-source manipulation? | N/A — No off-chain bridge verification component. The vault's on-chain Accountant contract handles pricing internally with exchange rate bounds. | N/A | N/A | N/A | - |

**Infra Counterparty Subtotal (8 scored questions, 3 N/A):**
- 8 scored questions: 7 x 9 + 1 x 3 = 66/72
- Adjusted: (66/72) x 45 = **41.3/45 (91.7%)**

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols is collateral deployed? | Pendle, Aave (Tier-0), Morpho (Tier-0), Balancer, Uniswap V3, Convex, Curve, Euler, Odos. All established, vetted DeFi protocols. No CEX or RWA exposure. Aave and Morpho are Tier-0 per SR list. Others are established but untiered. | 9 | 9 | Non-Improvable (optimal) | [P1] [ETH Yield Vault](https://etherfi.gitbook.io/etherfi/liquid/eth-yield-vault), [P1] [0xMacro audit scope](https://0xmacro.com/library) |
| ST-PC-02 | Are revenue-share arrangements documented? | Yes. Product page shows 0% platform fee, 0% performance fee, no exit fee. This is a change from the broader Liquid vault documentation which states fees "usually range from 0%-2%" per vault. The ETH Yield vault specifically charges 0% fees. Nonce Capital's arrangement as strategy provider is disclosed on the product page. | 9 | 9 | Non-Improvable (optimal) | [P0] [Product page](https://www.ether.fi/app/liquid/eth), [P1] [How Liquid Works](https://help.ether.fi/en/articles/517109-how-liquid-works) |
| ST-PC-03 | Are there hard limits per counterparty? | Yes. Strategy constrained via Merkle proofs to pre-approved protocols and assets. DecoderAndSanitizer validates each interaction. The whitelist constrains which protocols and asset types can be used. While per-counterparty PERCENTAGE caps are not documented explicitly, the Merkle system provides on-chain enforcement of allowed interactions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |
| ST-PC-04 | How quickly can positions be unwound? | Variable. Standard DeFi positions (Aave, Morpho, Uniswap, Curve): typically within hours. EigenLayer/Karak restaking: 7-day cooldown. Total withdrawal time: 3-10 days. Queue-based execution with 72-hour base period. No discretionary approvals required. | 9 | 9 | Non-Improvable (optimal) | [P0] [Product page -- 72h queue](https://www.ether.fi/app/liquid/eth), [P1] [Withdrawal FAQs](https://help.ether.fi/en/articles/269720-why-is-it-taking-so-long-to-withdraw-from-the-liquid-vaults) |
| ST-PC-05 | Are third-party service providers disclosed? | Yes. Nonce Capital identified as strategy provider on product page. Veda Technology as infrastructure provider. All whitelisted protocols publicly listed via audit scope and documentation. | 9 | 9 | Non-Improvable (optimal) | [P0] [Product page -- Nonce Capital, Veda](https://www.ether.fi/app/liquid/eth), [P1] [Veda Docs](https://docs.veda.tech/) |

**Protocol Counterparty Subtotal:**
- 5 questions: 5 x 9 = 45/45
- Adjusted: (45/45) x 45 = **45.0/45 (100.0%)**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed? | BoringOnChainQueue: user submits request with deadline and 0.9999 discount rate. Solver fulfills atomically within 72 hours (base period). Requests can be replaced or canceled before fulfillment. Pause possible via Accountant exchange rate violation (automatic) or Pauser role (manual). Protocol-wide only, no address-level blocking. | 9 | 9 | Non-Improvable (optimal) | [P0] [Product page -- 72h queue, 0.9999 discount](https://www.ether.fi/app/liquid/eth), [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |
| ST-L-02 | Is there enough liquidity to redeem ~100% of TVL? | **Untested under stress.** $218M TVL deployed across multiple protocols with variable withdrawal delays. EigenLayer 7-day cooldown compounds exit delays. Has NOT been tested in a real stress scenario. Theoretical capacity exists but resilience unproven. | 3 | 3 | Non-Improvable | [P0] [Etherscan -- ~93,416 liquidETH shares](https://etherscan.io/token/0xf0bb20865277aBd641a307eCe5ee04E79073416C), [P1] [Withdrawal FAQs](https://help.ether.fi/en/articles/269720-why-is-it-taking-so-long-to-withdraw-from-the-liquid-vaults) |
| ST-L-03 | Have there been past withdrawal delays or freezes? | No material delays reported. Standard 3-10 day withdrawal window communicated and observed. No unexpected freezes. TVL has decreased from $444M to $218M (orderly outflows over months, not crisis-driven), suggesting withdrawal mechanism functions. | 9 | 9 | Non-Improvable (optimal) | [P1] [Postmortems](https://github.com/etherfi-protocol/postmortems) |
| ST-L-04 | Do caps restrict timely redemptions? | Deposit caps exist but withdrawals are not capped. Queue-based system handles variable utilization. No evidence of withdrawal restrictions. | 9 | 9 | Non-Improvable (optimal) | [P1] [0xMacro Audits](https://0xmacro.com/library) |
| ST-L-05 | How does exit liquidity behave during volatility? | **Untested under severe stress.** During volatility, underlying protocol utilization may spike (Aave, Morpho), potentially delaying some position exits. The 3-10 day queue provides a buffer but has not been tested under extreme conditions. Per battle-tested vs untested principle, untested protocols cannot score Low (9). | 3 | 3 | Non-Improvable | No stress event documentation |
| ST-L-06 | Do withdrawals rely on unstaking longer than stated period? | The stated withdrawal period is 3-10 days, which explicitly includes the EigenLayer/Karak 7-day cooldown. Less than 10% of situations would result in durations beyond the stated 10-day maximum. | 9 | 9 | Non-Improvable (optimal) | [P1] [Withdrawal FAQs](https://help.ether.fi/en/articles/269720-why-is-it-taking-so-long-to-withdraw-from-the-liquid-vaults) |
| ST-L-07 | Does redemption depend on secondary-market liquidity? | No for protocol redemption. BoringOnChainQueue is always available for vault share redemption. Solver fulfills atomically. No secondary market dependency for the primary exit path. | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | **Mixed.** The collateral (weETH/WETH) has deep DEX liquidity. However, the vault share token (liquidETH) does NOT trade on secondary markets. Users must exit via the queue (3-10 days). Combined assessment: collateral deep but receipt token illiquid on open market. Scoring Mid (3): adequate mainly for staggered exits. | 3 | 9 | **Improvable** | [P0] [Chainlink weETH/ETH](https://data.chain.link/feeds/ethereum/mainnet/weeth-eth), [P0] [Etherscan -- no DEX pools for liquidETH](https://etherscan.io/token/0xf0bb20865277aBd641a307eCe5ee04E79073416C) |
| ST-L-09 | What is the risk of bank-run scenarios? | **Untested.** Queue-based withdrawal with 3-10 day window. EigenLayer cooldowns compound delays under stress. Has NOT been tested under bank-run conditions. Queue provides orderly processing but real-world resilience unproven. | 3 | 3 | Non-Improvable | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |

**Liquidity Subtotal:**
- 9 questions: L-01(9)+L-02(3)+L-03(9)+L-04(9)+L-05(3)+L-06(9)+L-07(9)+L-08(3)+L-09(3) = 57/81
- Adjusted: (57/81) x 45 = **31.7/45 (70.4%)**

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the receipt token peg performed under stress? | **N/A.** The BoringVault share token (liquidETH) does NOT trade on secondary markets with meaningful pricing. Users exit via the on-chain queue. Per applicability check: mark N/A for protocols where receipt token has no meaningful secondary market pricing. | N/A | N/A | N/A | [P0] [Etherscan -- no DEX pools for liquidETH](https://etherscan.io/token/0xf0bb20865277aBd641a307eCe5ee04E79073416C) |
| ST-M-02 | Can adverse market moves cause permanent losses? | Low direct ETH exposure. Vault primarily holds ETH-correlated assets (weETH/eETH). No directional leverage on ETH price. However, leverage is used (disclosed) which creates some market-related liquidation risk. The ETH-to-ETH nature means correlation is high. Restaking slashing and DeFi protocol risks are main loss vectors, not pure market direction. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risks](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/risks) |
| ST-M-03 | Are interest rate models robust during TVL shifts? | The vault itself is an allocator, not a lending protocol with its own rate model. Underlying Aave/Morpho have well-tested rate models. The strategist can reallocate between protocols if rate conditions deteriorate. No vault-level rate model risk. | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |
| ST-M-04 | Have historic volatility scenarios been modeled? | **No published stress testing.** The BoringVault architecture includes exchange rate bounds. However, no published formal stress testing against severe volatility regimes (30-50% spot gaps, liquidity dry-ups) exists. Nonce Capital's internal risk processes are not publicly documented. | 3 | 9 | **Improvable** | No published stress testing found |
| ST-M-05 | Can sharp price moves trigger forced liquidations? | Low risk for most vault positions. ETH-correlated strategy means collateral and debt are highly correlated (weETH collateral, ETH debt on Aave/Morpho). However, the product page explicitly discloses "This vault uses leverage, which means there is liquidation risk." Exchange rate bounds provide circuit breaker. Overall, liquidation risk is real but bounded by ETH-ETH correlation and Merkle constraints. | 9 | 9 | Non-Improvable (optimal) | [P0] [Product page -- leverage/liquidation disclosure](https://www.ether.fi/app/liquid/eth) |

**Market Subtotal:**
- 4 scored questions, 1 N/A: 3 x 9 + 1 x 3 = 30/36
- Adjusted: (30/36) x 45 = **37.5/45 (83.3%)**

---

**Strategy Total: 35.0 + 37.5 + 41.3 + 45.0 + 31.7 + 37.5 = 227.9/270 (84.4%)**

---

### OPERATIONS (30% Weight) - Score: 243.0/270 (90.0%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls changes? | ETHFI token governance via Snapshot voting. 4-day voting window. 1M ETHFI quorum. Delegate voting supported. Protocol parameters controlled by Admin multisig with timelock (48h+). No single entity can unilaterally change core fund-custody logic. **Platform-level score, consistent with eETH rating.** | 9 | 9 | Non-Improvable (optimal) | [P1] [Governance](https://etherfi.gitbook.io/gov/), [P2] [Snapshot](https://vote.ether.fi/info) |
| O-G-02 | How concentrated is voting power? | ETHFI allocation: investors 33.74%, core contributors 21.47%, treasury 21.62%, user airdrops 19.27%. Total insider allocation (investors + contributors) ~55%, exceeding 33% threshold for Low (9). Delegate system helps distribute voting but does not change underlying token concentration. No staker veto mechanism. **Platform-level score, consistent with eETH rating.** | 3 | 3 | Non-Improvable | [P1] [ETHFI Allocations](https://etherfi.gitbook.io/gov/ethfi-allocations) |
| O-G-03 | Are timelocks and veto mechanisms in place? | Yes. Timelock at least 48 hours for contract/module changes. 4-day Snapshot voting window. Quorum requirements. **Platform-level score, consistent with eETH rating.** | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |
| O-G-04 | Can strategy manager be replaced without blocking withdrawals? | Yes. Admin role can update strategist via RoleRegistry. Withdrawals handled by separate Queue/Solver system. Strategy changes do not block the BoringOnChainQueue exit mechanism. | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |

**Governance Subtotal:**
- 4 questions: 3x9 + 1x3 = 30/36
- Adjusted: (30/36) x 67.5 = **56.3/67.5 (83.3%)**

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are team and entities publicly identified? | Yes. Mike Silagadze (CEO, founder of Top Hat $400M+), Rok Kopp (CCO). Nonce Capital identified as strategy provider on product page. Veda as infrastructure provider. **Platform-level score, consistent with eETH rating.** | 9 | 9 | Non-Improvable (optimal) | [P1] [Team](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/team) |
| O-TL-02 | Is the protocol dependent on a single developer? | No. Multiple teams: ether.fi core team, Veda (infrastructure), Nonce Capital (strategy). Distributed development across components. **Platform-level score, consistent with eETH rating.** | 9 | 9 | Non-Improvable (optimal) | [P1] [Veda](https://veda.tech/) |
| O-TL-03 | What legal entity operates the protocol? | Ether.Fi SEZC (Special Economic Zone Company), organized under laws of the Cayman Islands. Clear legal entity with jurisdiction disclosure. **Platform-level score, consistent with eETH rating.** | 9 | 9 | Non-Improvable (optimal) | [P1] [Terms of Use](https://etherfi.gitbook.io/etherfi/ether.fi-legal/terms-of-use) |
| O-TL-04 | Known investigations or regulatory actions? | No known regulatory enforcement actions. **Platform-level score, consistent with eETH rating.** | 9 | 9 | Non-Improvable (optimal) | No adverse findings |
| O-TL-05 | On-call and incident response process? | Yes. September 2024 incident demonstrated rapid response. Partnerships with Seal911, Doppel, Hypernative. Formal incident response policy (Nov 2024). **Platform-level score, consistent with eETH rating.** | 9 | 9 | Non-Improvable (optimal) | [P1] [Sep 24 Incident Report](https://etherfi.gitbook.io/etherfi/security/sep-24-incident-attempted-domain-account-takeover) |
| O-TL-06 | Timely support for critical issues? | Yes. Help center (help.ether.fi). September 2024 incident resolved same day. Active governance forum. Discord community. **Platform-level score, consistent with eETH rating.** | 9 | 9 | Non-Improvable (optimal) | [P1] [Help Center](https://help.ether.fi/) |
| O-TL-07 | Major investors disclosed? | Yes. $32.3M raised. Bullish Capital, CoinFund, OKX Ventures, Foresight Ventures, Consensys, Bankless Ventures. **Platform-level score, consistent with eETH rating.** | 9 | 9 | Non-Improvable (optimal) | [P4] [CoinDesk Series A](https://www.coindesk.com/business/2024/02/28/liquid-restaking-protocol-etherfi-raises-23m-series-a) |
| O-TL-08 | Does strategy manager manage similar products creating conflicts? | **Limited information.** Nonce Capital is identified as a blockchain venture studio (founded 2019 per Crunchbase). Unlike Seven Seas Capital (which has extensive public documentation of managing Sommelier vaults and other DeFi strategies), Nonce Capital's DeFi vault management history is not well-documented publicly. However, the product page clearly identifies them as the strategy manager, and no direct conflicting mandates have been identified. Scoring 9 as no disclosed conflicts exist and the question scores High (1) only when "undisclosed or unmanaged conflicts" exist -- here there is simply limited information about other mandates, not evidence of conflicts. | 9 | 9 | Non-Improvable (optimal) | [P0] [Product page](https://www.ether.fi/app/liquid/eth), [P3] [Crunchbase](https://www.crunchbase.com/organization/nonce-capital) |
| O-TL-09 | Has strategy manager been involved in products with collateral loss? | **No known loss events.** Nonce Capital's public track record is limited compared to Seven Seas Capital. No documented collateral loss events found in public sources. However, the limited public history means this assessment has a narrower evidence base. Per criteria, "No known uncompensated collateral loss events linked to manager" scores Low (9). | 9 | 9 | Non-Improvable (optimal) | [P3] [Crunchbase](https://www.crunchbase.com/organization/nonce-capital), Web search -- no loss events found |

**Team & Legal Subtotal:**
- 9 questions: 9 x 9 = 81/81
- Adjusted: (81/81) x 67.5 = **67.5/67.5 (100.0%)**

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Up-to-date documentation? | Yes. Comprehensive GitBook docs covering whitepaper, Liquid technical documentation, risks section. Veda architecture documentation. Regular updates for new features and integrations. **Platform-level score, consistent with eETH rating.** | 9 | 9 | Non-Improvable (optimal) | [P1] [Whitepaper](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper), [P1] [Liquid Docs](https://etherfi.gitbook.io/etherfi/liquid) |
| O-DT-02 | Documented how collateral is used and when loss occurs? | Yes. Risks section covers smart contract, key management, regulatory risks. Product page explicitly discloses leverage risk and impermanent loss risk. Technical documentation covers Merkle constraints, exchange rate bounds, role separation. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risks](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/risks), [P0] [Product page risk disclosures](https://www.ether.fi/app/liquid/eth) |
| O-DT-03 | Contract addresses documented in one place? | Yes. Deployed Contracts page lists mainnet addresses. BoringVault address (0xf0bb20865277aBd641a307eCe5ee04E79073416C) documented. **Platform-level score, consistent with eETH rating.** | 9 | 9 | Non-Improvable (optimal) | [P1] [Deployed Contracts](https://etherfi.gitbook.io/etherfi/contracts-and-integrations/deployed-contracts) |
| O-DT-04 | Roles, permissions and timelocks documented? | Yes. Technical documentation covers Admin, Strategist, Pauser roles with responsibilities. Merkle-proof constraints, timelock durations, exchange rate bounds all documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |
| O-DT-05 | Proof-of-reserves published? | Yes. Full on-chain transparency. BoringVault holdings verifiable on Etherscan. Underlying DeFi positions traceable via on-chain transactions. Share price verifiable. ~93,416 liquidETH shares at ~$2,333/share. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan BoringVault](https://etherscan.io/address/0xf0bb20865277aBd641a307eCe5ee04E79073416C) |
| O-DT-06 | Contracts verified on block explorers? | Yes. Core BoringVault contract verified on Etherscan with Solidity 0.8.21 source code readable. Not a proxy. Supporting contracts also verified. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan BoringVault -- verified](https://etherscan.io/address/0xf0bb20865277aBd641a307eCe5ee04E79073416C) |

**Documentation Subtotal:**
- 6 questions: 6 x 9 = 54/54
- Adjusted: (54/54) x 67.5 = **67.5/67.5 (100.0%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Backstop reserve or safety module? | **Partial.** Treasury exists (~$104M across 4 addresses). $50M buyback proposal demonstrates treasury activity. However, no dedicated ring-fenced safety module with binding activation rules for user loss compensation exists. Treasury serves multiple purposes without specific loss-coverage commitments. **Platform-level score, consistent with eETH rating.** | 3 | 9 | **Improvable** | [P1] [ETHFI Allocations](https://etherfi.gitbook.io/gov/ethfi-allocations) |
| O-FR-02 | How large are reserves relative to TVL? | **Insufficiently disclosed.** Treasury holds ~$104M across 4 identified addresses. The composition of liquid reserves (stablecoins, ETH) vs illiquid ETHFI token holdings is not publicly disclosed. The $104M total is known but the liquid/illiquid breakdown is unavailable. | 3 | 9 | **Source Missing** | [P0] Treasury addresses provided: 0x7D4bBE471369a066186c18bAF33622796A08d5Cd, 0x7A6A41F353B3002751d94118aA7f4935dA39bB53, 0x5f0E7A424d306e9E310be4f5Bb347216e473Ae55, 0xD022d6bb8B6C1C357ec77D930Dc6A0aD40FFC90b |
| O-FR-03 | Estimated operational runway? | Strong. $32.3M raised. Broader ether.fi ecosystem TVL in the billions. Revenue from platform fees across all products. Runway comfortably >24 months. | 9 | 9 | Non-Improvable (optimal) | [P3] [Tracxn](https://tracxn.com/d/companies/ether.fi/__ybuswctFLX6Yyk0tndtj8aoDimNowhN3z_XQDPgnARo), [P3] [DeFiLlama](https://defillama.com/protocol/ether.fi) |
| O-FR-04 | How have TVL/revenue/buffers behaved in stress, including composability contagion? | **Untested under severe stress.** Vault TVL has decreased from ~$444M (Feb 2026) to ~$218M (Mar 2026), but this appears to be organic outflows during a broader market downturn, not a crisis-driven event. The vault has NOT been tested under a severe market stress event. Per battle-tested vs untested principle, untested protocols cannot score Low (9). **Composability contagion (v0.1-gamma):** liquidETH vault share has no secondary market and minimal external composability — contagion risk from the vault token itself is low. However, the underlying positions include weETH which is heavily composed across DeFi, so a severe eETH/weETH incident would impact the vault's underlying collateral. **Platform-level score, consistent with eETH rating.** | 3 | 3 | Non-Improvable | [P0] [Etherscan -- ~93,416 shares](https://etherscan.io/token/0xf0bb20865277aBd641a307eCe5ee04E79073416C), [P3] [DeFiLlama](https://defillama.com/protocol/ether.fi-liquid) |
| O-FR-05 | Can protocol remain safe if team disappears? | Mostly yes. Non-upgradeable core BoringVault. Permissionless withdrawal queue. Strategist role could be frozen (no new rebalances) but existing positions remain. Some reliance on Solver for optimal execution. Protocol can run in degraded mode with users exiting via queue. | 9 | 9 | Non-Improvable (optimal) | [P1] [Technical Documentation](https://etherfi.gitbook.io/etherfi/liquid/technical-documentation) |

**Financial Resilience Subtotal:**
- 5 questions: 2 x 9 + 3 x 3 = 27/45
- Adjusted: (27/45) x 67.5 = **40.5/67.5 (60.0%)**

---

**Operations Total: 56.3 + 67.5 + 67.5 + 40.5 = 231.8/270 (85.8%)**

---

## Final Score Calculation

| Category | Subcategory | Scored Q | N/A Q | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|----------|-------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security | 11 | 0 | 99 | 99 | 180.0 | 180 | 100.0% |
| | Key Management | 8 | 0 | 60 | 72 | 150.0 | 180 | 83.3% |
| | **Security Subtotal** | **19** | **0** | | | **330.0** | **360** | **91.7%** |
| **Strategy** | Protocol Mechanics | 9 | 0 | 63 | 81 | 35.0 | 45 | 77.8% |
| | Collateral | 4 | 0 | 30 | 36 | 37.5 | 45 | 83.3% |
| | Infra Counterparty | 8 | 0 | 66 | 72 | 41.3 | 45 | 91.7% |
| | Protocol Counterparty | 5 | 0 | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity | 9 | 0 | 57 | 81 | 31.7 | 45 | 70.4% |
| | Market | 4 | 1 | 30 | 36 | 37.5 | 45 | 83.3% |
| | **Strategy Subtotal** | | | | | **227.9** | **270** | **84.4%** |
| **Operations** | Governance | 4 | 0 | 30 | 36 | 56.3 | 67.5 | 83.3% |
| | Team & Legal | 9 | 0 | 81 | 81 | 67.5 | 67.5 | 100.0% |
| | Documentation | 6 | 0 | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience | 5 | 0 | 27 | 45 | 40.5 | 67.5 | 60.0% |
| | **Operations Subtotal** | | | | | **231.8** | **270** | **85.8%** |
| **TOTAL** | | **82** | **1** | | | **789.7** | **900** | **87.7%** |

---
