# Lombard Finance - LBTC Risk Rating

**Rating Date**: 2026-03-13
**Final Grade**: CCC+
**Total Score**: 643.7/900 points
**Framework**: Staking Rewards DeFi Protocol Rating Framework v1.0-alpha

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 292.0/360 (81.1%)

#### Smart Contract Security (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. LBTC smart contracts audited by 6+ independent parties: OpenZeppelin (Dec 2024), Halborn (Jul-Aug 2024, Oct 2024, Dec 2024), Veridise (May-Jun 2024, Aug 2024), Cantina, Sherlock, and Ackee Blockchain (Mar 2025 for Solana). Immunefi audit competition (Dec 2024-Jan 2025). All reports available on GitHub. Double audits before every major release. | 9 | 9 | Non-Improvable (optimal) | [P1] [GitHub Audits](https://github.com/lombard-finance/evm-smart-contracts/tree/main/docs/audit), [P1] [Halborn Report](https://www.halborn.com/audits/lombard/lbtc), [P1] [Veridise Report](https://veridise.com/audits-archive/company/lombard-finance/lbtc-2024-08-21/), [P1] [OpenZeppelin Audit](https://www.openzeppelin.com/news/lombard-audit) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | Sherlock (Tier-0) and Cantina (Tier-1) conducted audits. Halborn (Tier-1) performed the most recent EVM audit (Dec 2024). OpenZeppelin performed V2 review (Dec 2024). Multiple Tier-0/1 auditors in the most recent cycle. | 9 | 9 | Non-Improvable (optimal) | [P1] Sherlock, Cantina, Halborn, OpenZeppelin audit reports |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. V2 release (Dec 2024) audited by Halborn and OpenZeppelin. BTC.b integration (Oct 2024) audited by Halborn. Solana deployment (Mar 2025) audited by Ackee Blockchain. All production code double-audited before release per stated policy. | 9 | 9 | Non-Improvable (optimal) | [P1] Halborn V2 (Dec 2024), [P1] OZ V2 (Dec 2024), [P1] Ackee Solana (Mar 2025) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Halborn identified issues (burn function validation, burnCommission initialization) that were successfully addressed. All published reports are final versions indicating remediation was verified. Immunefi competition findings resolved. No evidence of unresolved critical/high findings. | 9 | 9 | Non-Improvable (optimal) | [P1] Halborn final report, [P1] GitHub audit directory |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | Yes, TransparentUpgradeableProxy (OpenZeppelin). Upgrades via Proxy Upgrade Timelock contract (0x055E84e7...77e59) with 1-hour delay. The 1-hour timelock is below the 24-hour best practice threshold. Consortium governance requires 2/3 consensus, adding an additional layer, but the on-chain timelock itself is only 1 hour. Docs mention 24-hour cooling-off for key policy changes, but proxy upgrades use only the 1-hour timelock. | 3 | 9 | **Improvable** | [P0] [Timelock Contract](https://etherscan.io/address/0x055E84e7FE8955E2781010B866f10Ef6E1E77e59), [P1] [Smart Contracts Docs](https://docs.lombard.finance/technical-documentation/smart-contracts) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploits affecting Lombard user funds. The Ionic Money hack (Feb 2025, $8.6M) involved a fake LBTC token impersonation on a third-party platform, not an exploit of Lombard itself. No direct security incidents in ~18 months of operation. | 9 | 9 | Non-Improvable (optimal) | [P4] [Halborn Ionic Analysis](https://www.halborn.com/blog/post/explained-the-ionic-money-hack-february-2025), [P1] Lombard docs state zero incidents |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No. Institutional backing from Polychain Capital, Franklin Templeton, BabylonChain. 15-member Security Consortium of named institutions. ~18-month track record with $1B+ TVL. | 9 | 9 | Non-Improvable (optimal) | [P1] [Lombard docs](https://docs.lombard.finance), [P4] Fundraising reports |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No evidence of timelock reductions. The 1-hour proxy upgrade timelock has been consistent since deployment. No governance proposals or on-chain evidence of timelock parameter changes. | 9 | 9 | Non-Improvable (optimal) | [P0] Etherscan timelock contract history |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Active bug bounty on Immunefi with up to $250,000 maximum payout for critical vulnerabilities. Program live since September 2024. Payments in USDC. Requires PoC for submissions. Additionally, Immunefi audit competition conducted Dec 2024-Jan 2025. Meaningful scope and payout well above $100K threshold. | 9 | 9 | Non-Improvable (optimal) | [P1] [Immunefi Bounty](https://immunefi.com/bug-bounty/lombard-finance/), [P1] [Bug Bounty Docs](https://docs.lombard.finance/learn/lombard-security-model/bug-bounty-program) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Yes. Hexagate provides 24/7 real-time monitoring with automated pausing capabilities detecting anomalies, exploits, oracle deviations, and 3rd party dependencies. Cubist Bascule provides independent invariant checks (cross-chain reserve consistency). PagerDuty for incident response and on-call management. Multiple independent monitoring layers. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Blog](https://www.lombard.finance/blog/lbtc-security-and-transparency/), [P1] [Hexagate Integration](https://www.lombard.finance/blog/how-top-security-experts-safeguard-the-lbtc-ecosystem/) |
| S-SC-11 | Are automatic safety controls (e.g. pause, circuit breakers) triggered by monitoring alerts? | LBTC uses ERC-20 Pausable for automated incident response. Hexagate triggers automated pauses upon detection of anomalies and potential attacks. Cubist Bascule halts bridge operations if reserve discrepancy detected. Designated Pauser role can pause critical functions. Multiple automated triggers from independent systems (Hexagate + Bascule). Clear rules documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [LBTC Design](https://docs.lombard.finance/technical-documentation/protocol-architecture/lbtc-design), [P1] Security blog |

**Smart Contract Security Subtotal:**
- Raw scores: 9+9+9+9+3+9+9+9+9+9+9 = 93/99
- Adjusted: (93/99) x 180 = **169.1/180 (93.9%)**

---

#### Key Management & Permissions (20% weight, 180 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Admin/upgrade rights held by Security Consortium, a custom multi-sig contract (0xed6D647E...0348Eea) requiring 2/3 consensus from ~15 institutional members (Galaxy, OKX, DCG, Wintermute, Figment, Kiln, P2P, Kraken, Chorus.one, Amber, Antpool, F2Pool, and others). Upgrades go through 1-hour timelock. BTC keys managed via Cubist CubeSigner HSM. Changes documented via blog posts and consortium announcements. Diversified institutional multisig with publicly documented membership. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Consortium](https://docs.lombard.finance/lombards-partners/security-consortium), [P0] [Consortium Contract](https://etherscan.io/address/0xed6D647E2F81E5262101aFf72c4A7bcDcfd780e0) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. Minting/burning LBTC requires valid signatures from both the Consortium (2/3 of ~15 members, approximately 10-of-15 threshold) AND the Bascule Drawbridge (independent Cubist verification). Proxy upgrades require Consortium consensus through the timelock. BTC keys in CubeSigner HSM with hardware-enforced policies. Dual-signature requirement (Consortium + Bascule) with threshold of ~10-of-15 significantly exceeds the 3-of-5 minimum. | 9 | 9 | Non-Improvable (optimal) | [P1] [Consortium Design](https://docs.lombard.finance/technical-documentation/protocol-architecture/consortium-design), [P1] [Bascule Drawbridge](https://docs.lombard.finance/technical-documentation/protocol-architecture/bascule-drawbridge) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Consortium requires 2/3 of ~15 members (~10-of-15 threshold). Members are named institutions (Galaxy, OKX, DCG, Wintermute, etc.) strongly suggesting independence. However, individual signer wallet addresses are not publicly disclosed. On-chain verification of independence is not possible since this is a custom multi-sig contract, not a Gnosis Safe. Institutional names strongly suggest independence but cannot be cryptographically confirmed. Per the scoring criteria: "If signer identities are fully unknown, independence cannot be confirmed -- score Mid (3) at best." | 3 | 9 | **Source Missing** | [P1] [Consortium Members](https://docs.lombard.finance/lombards-partners/lombards-security-consortium), [P0] Custom consortium contract |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | Pause is protocol-wide via ERC-20 Pausable, triggered by designated Pauser role or automated via Hexagate. No evidence of address-level arbitrary withdrawal censorship. TRM sanctions screening exists for compliance. Pause scope and rules publicly documented. No address-level blocking capability identified beyond sanctions. | 9 | 9 | Non-Improvable (optimal) | [P1] [LBTC Design](https://docs.lombard.finance/technical-documentation/protocol-architecture/lbtc-design), [P1] Security blog |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | BTC is held in Bitcoin addresses managed by CubeSigner HSM infrastructure. Keys in FIPS 140 HSMs and Nitro enclaves -- no one (not Cubist, not Lombard) can access raw private keys. However, this is not a standard non-custodial on-chain smart contract model. BTC sits in Bitcoin UTXO addresses controlled by HSM-managed keys. Consortium consensus provides distributed control. This is functionally "fully disclosed MPC wallets" which maps to Mid (3) per criteria. 100% of BTC backing is in this custody model. | 3 | 3 | Non-Improvable | [P1] [CubeSigner Key Management](https://docs.lombard.finance/technical-documentation/protocol-architecture/cubesigner-key-management), [P1] [Cubist Blog](https://cubist.dev/blog/cubist-lombard-connecting-bitcoin-to-defi) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | BTC deposits held in dedicated Babylon staking addresses, separate from Lombard operational wallets. LBTC is a separate ERC-20 contract. Dual Proof of Reserves oracles (Chainlink, RedStone) verify BTC reserves match LBTC supply, confirming segregation. No evidence of co-mingling. | 9 | 9 | Non-Improvable (optimal) | [P1] [PoR Oracle Docs](https://docs.lombard.finance/technical-documentation/oracles), [P0] [RedStone PoR](https://etherscan.io/address/0xb415eAA355D8440ac7eCB602D3fb67ccC1f0bc81) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | N/A -- LST product, not a managed vault strategy. LBTC is staked on Babylon via designated Finality Providers. Users independently choose DeFi activities with their LBTC. | N/A | N/A | N/A | - |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Lombard has PagerDuty-based incident response and Hexagate automated pausing. Blog mentions "proactive security response frameworks enabling swift remediation." However, no publicly documented incident playbook with specific steps for key rotation, signer replacement, or tabletop exercises has been found. Infrastructure suggests a process exists but documentation is not public. | 1 | 9 | **Source Missing** | [P1] Security blog mentions incident response, [P1] PagerDuty + Hexagate confirmed |

**Key Management Subtotal:**
- Scored questions: 7 (S-KM-07 is N/A)
- Raw scores: 9+9+3+9+3+9+1 = 43/63
- Adjusted: (43/63) x 180 = **122.9/180 (68.3%)**

**Security Total: 169.1 + 122.9 = 292.0/360 (81.1%)**

---

### STRATEGY (30% Weight) -- Score: 212.0/270 (78.5%)

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | LBTC yield comes from Babylon Bitcoin staking via 4 institutional Finality Providers, generating BABY token rewards. Base staking rate ~0.4% APY. 8% performance fee charged. Yield source (Babylon staking) is aligned with mandate (Bitcoin liquid staking). However, approximate percent contributions not explicitly broken down in docs, and much of user value proposition relies on Lux points and ecosystem incentives beyond the base staking yield. | 3 | 9 | **Improvable** | [P3] [StakingRewards](https://www.stakingrewards.com/asset/lombard-staked-bitcoin), [P1] [FAQ](https://docs.lombard.finance/frequently-asked-questions/faqs) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Net yield becomes negative in plausible but severe scenarios: (1) Finality Provider slashing on Babylon, (2) LBTC depeg on secondary markets during 9-day unstaking period, (3) Smart contract exploit, (4) Babylon protocol failure. The 0.4% base APY is thin, meaning even small fee increases or slashing events could push net yield negative. No leverage. | 3 | 3 | Non-Improvable | [P1] Unstaking docs, [P1] Risk disclosures |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No leverage or rehypothecation. BTC staked 1:1 on Babylon. LBTC is a receipt token backed 1:1 by staked BTC. | 9 | 9 | Non-Improvable (optimal) | [P1] [Protocol Architecture](https://docs.lombard.finance/technical-documentation/protocol-architecture) |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- LST product with no leverage. No liquidation risk within the protocol. | N/A | N/A | N/A | - |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss events for LBTC holders in ~18 months. No comparable BTC LST on Babylon has experienced permanent losses. | 9 | 9 | Non-Improvable (optimal) | [P1] Lombard docs, [P3] DeFiLlama data |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | N/A -- LST product, not a vault. | N/A | N/A | N/A | - |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Base Babylon staking yield ~0.4% APY (organic, from BABY token rewards). Much of user-facing value relies on Lombard Lux points, BARD incentives, and DeFi farming. Base staking rate is sustainable but very low. Incentive-driven yield likely >70% of the value proposition, raising sustainability concerns. Protocol yield would be near zero (but not negative) without incentives. | 1 | 3 | **Improvable** | [P3] StakingRewards ~0% LBTC APY, [P1] FAQ on staking rewards |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Direct unstaking at 1:1 BTC ratio through Lombard's mechanism -- no slippage on redemption itself. 9-day wait is a delay, not a penalty. Under conservative assumptions, the strategy can unwind most of position within stated 9-day horizon with effectively 0% slippage via direct redemption. Secondary market exit would have some slippage for large sizes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Unstaking Guide](https://docs.lombard.finance/lbtc-liquid-bitcoin/lbtc-yield-bearing-btc/user-guides/unstaking-lbtc) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | Yield from Babylon staking rewards, not from a spread or funding rate. LBTC/BTC peg is structurally 1:1 backed by PoR-verified reserves. Secondary market pricing can deviate temporarily but this does not drive yield. Peg reliance <30% of expected yield. | 9 | 9 | Non-Improvable (optimal) | [P1] PoR oracle docs, [P3] Price data |

**Protocol Mechanics Subtotal:**
- Scored questions: 7 (ST-PM-04, ST-PM-06 are N/A)
- Raw scores: 3+3+9+9+1+9+9 = 43/63
- Adjusted: (43/63) x 45 = **30.7/45 (68.2%)**

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | LBTC accepts only native BTC as deposits. BTC is the premier digital asset with the highest market cap (~$1.7T). It is an established large-cap asset at the lowest risk tier. No other collateral types accepted. Pure single-asset, highest-quality collateral. | 9 | 9 | Non-Improvable (optimal) | [P1] Protocol docs, [P3] CoinGecko BTC data |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | LBTC/BTC peg maintained by 1:1 PoR backing. No documented depeg >2% in ~24 months of operation. LBTC survived multiple BTC drawdowns and the October 2025 global crypto market liquidation ($19B in leveraged positions liquidated, BTC dropped ~14%) without losing peg. No depeg reports during any stress event. Battle-tested: peg held through real market stress, Low (9). | 9 | 9 | Non-Improvable (optimal) | [P3] CoinGecko LBTC/BTC, [P1] FAQ depeg risk, [P4] October 2025 crypto crash data |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | 4 institutional Finality Providers: Galaxy ($4.2B AUS), Kiln, P2P (explicit slashing protection), Figment (700+ institutional clients). Diversified across independent operators. Institutional-grade monitoring and infrastructure. No slashing incidents in operational history. | 9 | 9 | Non-Improvable (optimal) | [P1] [Staking Partners](https://docs.lombard.finance/lombards-partners/bitcoin-staking-partners), [P1] [Kiln](https://www.kiln.fi/protocols/lombard) |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | ~98% of TVL is native BTC staked on Babylon (not bridged/wrapped). LBTC ERC-20 on Ethereum and other chains is the liquid token, but underlying BTC backing is native. Cross-chain LBTC uses Chainlink CCIP (Tier-0). Less than 2% in bridged form. | 9 | 9 | Non-Improvable (optimal) | [P3] DeFiLlama TVL, [P1] CCIP docs |

**Collateral Subtotal:**
- Raw scores: 9+9+9+9 = 36/36
- Adjusted: (36/36) x 45 = **45.0/45 (100.0%)**

---

#### Infra Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | Critical dependencies explicitly listed: Bitcoin (Tier-0), Ethereum (Tier-0), Babylon (novel, institutional-backed), Chainlink CCIP (Tier-0 bridge), Chainlink PoR (Tier-0 oracle), RedStone (Tier-1 oracle), CubeSigner/Cubist (SOC 2 Type II certified HSM). 5 of 7 dependencies are Tier-0/1. Babylon and Cubist are untiered but have strong institutional backing and security certifications. Majority Tier-0/1 warrants Low (9). | 9 | 9 | Non-Improvable (optimal) | [P1] [Protocol Architecture](https://docs.lombard.finance/technical-documentation/protocol-architecture), [P1] [Oracles](https://docs.lombard.finance/technical-documentation/oracles) |
| ST-IC-02 | How redundant and battle-tested are the oracle and bridge setups? | Dual PoR oracles: Chainlink (Tier-0) and RedStone (Tier-1) -- independent providers. Cross-chain via Chainlink CCIP (Tier-0) with dual-layer validation (CCIP + Consortium). Battle-tested providers. Independent fallbacks exist for both oracle and bridge. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracles Docs](https://docs.lombard.finance/technical-documentation/oracles), [P0] [RedStone PoR](https://etherscan.io/address/0xb415eAA355D8440ac7eCB602D3fb67ccC1f0bc81) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | Cubist (CubeSigner) holds SOC 2 Type II certification and uses FIPS 140-certified HSMs with AWS Nitro enclaves. Hexagate's parent company Chainalysis holds SOC 2 Type II certification and FedRAMP Moderate (In Process) status. Both key off-chain providers have industry-standard IT security certifications. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cubist Information Security](https://cubist.dev/information-security), [P1] [Chainalysis Trust Center](https://trust.chainalysis.com/), [P1] CubeSigner FIPS 140 docs |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | ~18 months operational with no infrastructure failures causing user impact. Navigated Babylon Finality Provider transition (April 2025) smoothly. No Bitcoin or Ethereum chain outages impacted operations. Protocol operating >6 months without incidents scores Low (9). | 9 | 9 | Non-Improvable (optimal) | [P2] [Twitter FP Transition](https://x.com/Lombard_Finance/status/1912713537249488903), [P1] FAQ |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | Bitcoin: No chain halts in history. Ethereum: No halts >30 minutes in last 12 months. Both Tier-0 chains with excellent uptime. | 9 | 9 | Non-Improvable (optimal) | [P3] Chain monitoring data |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | No slashing events for Lombard's Finality Providers (Galaxy, Kiln, P2P, Figment) on Babylon. Babylon slashing is new but all providers have institutional track records. No incidents in ~18 months. | 9 | 9 | Non-Improvable (optimal) | [P1] Staking Partners docs |
| ST-IC-07 | Are validators diverse geographically and by operator? | 4 independent Finality Providers: Galaxy (US), Kiln (France/EU), P2P (distributed), Figment (Canada). Separate ownership and infrastructure. No single operator >25% (4 operators at ~25% each). Geographic diversity across US, EU, Canada. | 9 | 9 | Non-Improvable (optimal) | [P1] [Staking Partners Blog](https://www.lombard.finance/blog/lombard-partners-with-institutional-staking-providers-to-scale-bitcoin-staking-infrastructure/) |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | CubeSigner HSM is a critical dependency for BTC key operations. Sustained Cubist outage could delay BTC withdrawals beyond 48 hours. Consortium distributes control across ~15 members but all rely on CubeSigner infrastructure. CCIP failure blocks cross-chain but not in-protocol unstaking. Cubist HSM platform is a plausible single point of failure for BTC operations. | 3 | 9 | **Improvable** | [P1] CubeSigner architecture, [P1] Protocol architecture |

**Infra Counterparty Subtotal:**
- Raw scores: 9+9+9+9+9+9+9+3 = 66/72
- Adjusted: (66/72) x 45 = **41.25/45 (91.7%)**

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | BTC deployed exclusively to Babylon Protocol via 4 Finality Providers. No CEX or RWA deployment. Babylon is novel and untiered by SR but has significant institutional backing and dedicated audit coverage. Given untiered status despite strong profile, scores Mid (3). | 3 | 9 | **Improvable** | [P1] Protocol Architecture, [P3] DeFiLlama Babylon |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | 8% performance fee on staking rewards (Finality Provider commission) publicly disclosed. Revenue-share with FPs is standard institutional staking. No undisclosed arrangements found. | 9 | 9 | Non-Improvable (optimal) | [P1] [FAQ](https://docs.lombard.finance/frequently-asked-questions/faqs) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | BTC staked across 4 Finality Providers. April 2025 transition from single FP to 4 institutional partners suggests active management. However, specific per-provider allocation limits or rebalancing rules not publicly documented. No on-chain caps. | 3 | 9 | **Improvable** | [P2] [Twitter FP Transition](https://x.com/Lombard_Finance/status/1912713537249488903) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Unwinding from Babylon requires 7-day unbonding (protocol design). Deterministic and non-discretionary. Within stated 9-day withdrawal horizon. No discretionary approvals beyond Consortium validation. | 9 | 9 | Non-Improvable (optimal) | [P1] [Unstaking Docs](https://docs.lombard.finance/lbtc-liquid-bitcoin/lbtc-yield-bearing-btc/user-guides/unstaking-lbtc) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | All 4 Finality Providers (Galaxy, Kiln, P2P, Figment) publicly named with roles. Cubist disclosed as HSM provider. All 15 Consortium members named. Hexagate, RedStone, Chainlink disclosed. Comprehensive third-party disclosure. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Consortium](https://docs.lombard.finance/lombards-partners/security-consortium), [P1] [Staking Partners](https://docs.lombard.finance/lombards-partners/bitcoin-staking-partners) |

**Protocol Counterparty Subtotal:**
- Raw scores: 3+9+3+9+9 = 33/45
- Adjusted: (33/45) x 45 = **33.0/45 (73.3%)**

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Unstaking via Lombard WebApp -- LBTC burned, BTC undelegated from FPs, returned to user BTC address after 9 days. Pause is protocol-wide (ERC-20 Pausable), not address-level selective. Controlled by Pauser role, visible on-chain. TRM sanctions screening for compliance. Permissionless on-chain path exists. | 9 | 9 | Non-Improvable (optimal) | [P1] [Unstaking Guide](https://docs.lombard.finance/lbtc-liquid-bitcoin/lbtc-yield-bearing-btc/user-guides/unstaking-lbtc) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | In-protocol redemption is 1:1 BTC backed (PoR verified). However, Babylon unbonding queue creates bottlenecks in mass unstaking. 9-day period is per-request but system-wide queue congestion possible. Secondary market LBTC depth limited relative to $1B+ TVL. Large-scale redemption feasible via unstaking path but would require extended queuing. | 3 | 3 | Non-Improvable | [P1] Unstaking docs, [P3] DeFiLlama TVL |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | No reported delays or freezes in ~24 months. No user complaints found. FP transition (Apr 2025) was protocol-level, not user withdrawal disruption. However, limited on-chain time-series data to verify specific withdrawal completion rates. Publishing withdrawal completion data would confirm performance. | 3 | 9 | **Source Missing** | [P1] FAQ, [P2] Twitter history |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Minimum unstake 0.00013300 LBTC. No maximum cap documented. No daily redemption limits. Unstaking fee applies but is not punitive. No history of caps blocking exits. | 9 | 9 | Non-Improvable (optimal) | [P1] Unstaking docs |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | LBTC not tested through major volatility event. 9-day unstaking means no quick exit to BTC during stress. Secondary market DEX liquidity could thin under stress. Battle-tested framework: untested, max score 3. | 3 | 3 | Non-Improvable | [P3] Price data, [P1] Depeg risk disclosure |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | Stated withdrawal period is 9 days. All BTC staked on Babylon with 7-day unbonding + 2 days processing. No portion locked longer than stated 9 days. | 9 | 9 | Non-Improvable (optimal) | [P1] Unstaking docs |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | Most users can exit via in-protocol 1:1 BTC redemption (9-day wait). Secondary markets (Uniswap, Curve, CEXs) optional for faster exits but required for instant liquidity. In-protocol path reliable but slow. Deeper secondary market liquidity could improve instant exit options. | 3 | 9 | **Improvable** | [P1] Docs, [P3] DEX data |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | LBTC trades on Uniswap V3, Curve, multiple CEXs. Market cap ~$732M. Veda manages DEX liquidity for peg stability. 100+ DeFi integrations. Without specific depth metrics, estimated ~3-10% of TVL absorb-able without major impact. Publishing detailed liquidity depth data would confirm. | 3 | 9 | **Source Missing** | [P3] CoinGecko, [P1] Veda blog |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | In bank-run, 9-day queue creates orderly process. LBTC is 1:1 BTC-backed (PoR verified) so no permanent haircuts expected. Queue congestion and secondary market discount likely. Protocol untested in this scenario. Battle-tested framework: untested, max 3. | 3 | 3 | Non-Improvable | [P1] PoR design, [P3] TVL data |

**Liquidity Subtotal:**
- Raw scores: 9+3+3+9+3+9+3+3+3 = 45/81
- Adjusted: (45/81) x 45 = **25.0/45 (55.6%)**

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | LBTC is an LST that trades on secondary markets. No documented depeg >2% in ~24 months. LBTC survived the October 2025 global crypto liquidation event ($19B liquidated, BTC dropped ~14%) and multiple BTC drawdowns without significant peg deviation. Current LBTC/BTC ratio fluctuates within ~0.5% band. Battle-tested: peg held through real market stress, Low (9). | 9 | 9 | Non-Improvable (optimal) | [P3] CoinGecko LBTC/BTC, [P1] FAQ |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | LBTC is effectively 1x long BTC. No leverage, no shorting. BTC drawdowns affect USD value but not BTC-denominated backing. Low-beta, no liquidation risk from price moves. | 9 | 9 | Non-Improvable (optimal) | [P1] Protocol architecture |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Babylon staking yield is organic (~0.4% APY from BABY rewards), set by Babylon network mechanics not utilization curves. No reflexive incentive loops. TVL shifts don't directly affect staking rate. | 9 | 9 | Non-Improvable (optimal) | [P1] Docs, [P3] StakingRewards |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | No publicly available stress testing or scenario analysis documentation. Risk disclosures are qualitative only (depeg risk, slashing risk, smart contract risk). No quantitative tail-risk modeling published. Given institutional backing, internal models may exist but are not public. | 1 | 9 | **Source Missing** | [P1] FAQ qualitative risk disclosures only |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | No leverage in LBTC protocol. No liquidation risk from price moves. 1:1 BTC backing with no borrowing. External DeFi protocol usage of LBTC as collateral is outside Lombard's control. | 9 | 9 | Non-Improvable (optimal) | [P1] Protocol architecture |

**Market Subtotal:**
- Raw scores: 9+9+9+1+9 = 37/45
- Adjusted: (37/45) x 45 = **37.0/45 (82.2%)**

**Strategy Total: 30.7 + 45.0 + 41.25 + 33.0 + 25.0 + 37.0 = 211.95/270 (78.5%)**

---

### OPERATIONS (30% Weight) -- Score: 139.7/270 (51.7%)

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Protocol changes controlled by Security Consortium (15 institutional members, 2/3 consensus). BARD governance token launched recently with on-chain governance planned via Liquid Bitcoin Foundation (LBF). Current model is hybrid: Consortium controls upgrades, BARD governance nascent/not yet binding. No single entity can unilaterally change core logic. | 3 | 9 | **Improvable** | [P1] [Token Economics](https://docs.lombard.finance/learn/token-economics), [P1] [Consortium](https://docs.lombard.finance/lombards-partners/security-consortium) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | BARD: 1B total supply. At TGE ~22.5% circulating. Allocation ~35% Treasury/Foundation, ~25% Contributors (48-mo vesting), ~20% Investors (vesting), ~20% Ecosystem. Early stage means concentration expected. Without specific voting data, top 10 likely control >33% given team + investor allocations. | 3 | 9 | **Improvable** | [P1] [BARD Tokenomics](https://www.lombard.finance/blog/bard-tokenomics/), [P3] CoinGecko BARD |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Proxy upgrade timelock of 1 hour (on-chain). Key policy changes have 24-hour cooling-off period (per docs). Consortium 2/3 consensus required. Bascule provides independent verification layer. The on-chain proxy timelock (1h) is below 24h threshold. Key policy changes have 24h cooling-off but this is a separate mechanism. Partial coverage. | 3 | 9 | **Improvable** | [P0] [Timelock](https://etherscan.io/address/0x055E84e7FE8955E2781010B866f10Ef6E1E77e59), [P1] Consortium design |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | N/A -- LST product. The April 2025 Finality Provider transition was executed without blocking user withdrawals, demonstrating operational flexibility. | N/A | N/A | N/A | - |

**Governance Subtotal:**
- Scored questions: 3 (O-G-04 is N/A)
- Raw scores: 3+3+3 = 9/27
- Adjusted: (9/27) x 67.5 = **22.5/67.5 (33.3%)**

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Core team publicly identified: Jacob Phillips (Co-founder, ex-Polychain Capital), Olivia Thet (Engineering Director, UC Berkeley), Matthew Donovan (Head of BD). LinkedIn profiles verified. Backgrounds from Argent, Coinbase, Maple. 15 employees. Verifiable track records. | 9 | 9 | Non-Improvable (optimal) | [P1] [IQ.wiki Jacob Phillips](https://iq.wiki/wiki/jacob-phillips), [P2] LinkedIn profiles |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | 15 employees with dedicated engineering, BD, marketing. Multiple GitHub contributors. Security Consortium provides operational redundancy. FPs operate independently. Not single-person dependent. | 9 | 9 | Non-Improvable (optimal) | [P1] Team disclosures, [P1] GitHub |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Headquartered in Cayman Islands. Liquid Bitcoin Foundation (LBF) established as governance entity. Specific entity registration details not fully disclosed beyond headquarters. Entity and jurisdiction mentioned but legal roles partially clear. | 3 | 9 | **Improvable** | [P4] Tracxn, [P1] LBF in tokenomics blog |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known regulatory investigations or enforcement actions. Clean record for ~18-month operational history. | 9 | 9 | Non-Improvable (optimal) | [P4] SEC search negative, [P4] No news reports |
| O-TL-05 | Is there an on-call and incident response process for core teams? | PagerDuty integration for incident response. Hexagate 24/7 monitoring with automated alerting. "Proactive security response frameworks." Multiple monitoring layers suggest structured on-call. Specific SLAs and runbook details not public. | 3 | 9 | **Improvable** | [P1] Security blog, [P1] PagerDuty confirmed |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Active Discord, Twitter, documentation. SDK for integrators. Regular blog posts. No specific evidence of structured support SLAs or ticket systems. General social media presence suggests responsive team. | 3 | 9 | **Improvable** | [P1] Docs, [P2] Social media |
| O-TL-07 | Are major investors or strategic partners disclosed? | Fully disclosed: Polychain Capital (lead), Franklin Templeton, BabylonChain, dao5, Foresight Ventures, Mirana, Mantle EcoFund, Nomad Capital. Strategic: Bitget, Bybit, OKX. $16M seed publicly announced. | 9 | 9 | Non-Improvable (optimal) | [P4] The Block, [P1] Lombard blog |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | N/A -- LST product, not a managed vault. | N/A | N/A | N/A | - |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | N/A -- LST product, not a managed vault. | N/A | N/A | N/A | - |

**Team & Legal Subtotal:**
- Scored questions: 7 (O-TL-08, O-TL-09 are N/A)
- Raw scores: 9+9+3+9+3+3+9 = 45/63
- Adjusted: (45/63) x 67.5 = **48.2/67.5 (71.4%)**

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Comprehensive docs at docs.lombard.finance: Protocol Architecture, LBTC Design, Consortium Design, CubeSigner, Bascule, Oracles, Smart Contracts, Supported Blockchains. Risk disclosures in FAQ. Current and regularly updated. | 9 | 9 | Non-Improvable (optimal) | [P1] [docs.lombard.finance](https://docs.lombard.finance) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | BTC flow documented: deposit -> Babylon staking via FPs -> LBTC minting. Loss scenarios qualitatively described (slashing, depeg, smart contract risk). End-to-end flow documented but no systematic scenario mapping with quantitative thresholds. | 3 | 9 | **Improvable** | [P1] Architecture docs, [P1] FAQ |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | docs.lombard.finance/technical-documentation/smart-contracts lists LBTC token, Consortium governance, Proxy Upgrade Timelock for Ethereum. Registry limited to 3 core Ethereum contracts. Cross-chain deployments (15+ chains) not comprehensively listed in one place. | 3 | 9 | **Improvable** | [P1] [Smart Contracts](https://docs.lombard.finance/technical-documentation/smart-contracts) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | LBTC Design docs comprehensively describe roles: Consortium, Minters, Claimers, Operator, Pauser, Owner. Permissions documented for each role with clear scope. Timelock documented (1h). Consortium member changes announced via blog posts. Core role and permission documentation is thorough and accessible. | 9 | 9 | Non-Improvable (optimal) | [P1] [LBTC Design](https://docs.lombard.finance/technical-documentation/protocol-architecture/lbtc-design) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Dual PoR oracles: Chainlink PoR and RedStone PoR (0xb415eAA...0bc81). Verifies BTC reserves match LBTC supply across all chains. Algorithm runs every 20 min, on-chain update within 24h or 1% deviation. First BTC LST with dual PoR. No liabilities (1:1 backing, no borrowing) so PoL N/A. | 9 | 9 | Non-Improvable (optimal) | [P0] [RedStone PoR](https://etherscan.io/address/0xb415eAA355D8440ac7eCB602D3fb67ccC1f0bc81), [P1] [Oracle Docs](https://docs.lombard.finance/technical-documentation/oracles) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | LBTC token, Consortium governance, Proxy Upgrade Timelock all verified on Etherscan. Source code on GitHub. Cross-chain deployments appear verified on respective explorers. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan LBTC](https://etherscan.io/address/0x8236a87084f8b84306f72007f36f2618a5634494), [P0] [Etherscan Timelock](https://etherscan.io/address/0x055E84e7FE8955E2781010B866f10Ef6E1E77e59) |

**Documentation Subtotal:**
- Raw scores: 9+3+3+9+9+9 = 42/54
- Adjusted: (42/54) x 67.5 = **52.5/67.5 (77.8%)**

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | No dedicated safety module or backstop reserve. BARD staking secures cross-chain transfers, not user loss backstop. No ring-fenced reserve for edge case losses. 1:1 BTC backing (PoR) provides structural assurance but no explicit reserve for slashing beyond validator protection. | 1 | 9 | **Improvable** | [P1] Token economics, [P1] No safety module in docs |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | No DeFiLlama treasury data (API returns "not found"). No treasury wallet addresses disclosed. BARD market cap ~$264M. Tokenomics mention ~35% to Treasury/Foundation but no wallet addresses or balances disclosed. Cannot verify reserves. | 1 | 9 | **Source Missing** | [P3] DeFiLlama treasury "not found", [P1] Tokenomics 35% allocation |
| O-FR-03 | What is the estimated operational runway at current burn? | $16M seed (Jul 2024) plus BARD community sale proceeds. 8% fee on staking rewards (~$320K/year at current TVL and yield). 15 employees. Runway likely 12-24+ months with seed + sale proceeds but exact figures not disclosed. Reasonable but partly assumption-dependent. | 3 | 9 | **Improvable** | [P4] Fundraising reports, [P1] Fee structure |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events? | TVL grew to ~$2.2B peak then declined to ~$1B (organic, not exploit-related). No major stress event tested resilience. No depositor haircuts. TVL halved from peak is notable but not stress-related. Battle-tested: untested, max 3. | 3 | 3 | Non-Improvable | [P3] DeFiLlama TVL history |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Consortium (15 independent institutions) could theoretically continue validation. BTC in Babylon continues earning. However, CubeSigner HSM depends on Cubist operating. Withdrawals depend on Consortium processing unstaking. Distributed Consortium provides resilience but Cubist dependency is a concern. Users can hold/trade LBTC but unstaking requires Consortium. | 3 | 3 | Non-Improvable | [P1] Consortium design, [P1] CubeSigner dependency |

**Financial Resilience Subtotal:**
- Raw scores: 1+1+3+3+3 = 11/45
- Adjusted: (11/45) x 67.5 = **16.5/67.5 (24.4%)**

**Operations Total: 22.5 + 48.2 + 52.5 + 16.5 = 139.7/270 (51.7%)**

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 93 | 99 | 169.1 | 180 | 93.9% |
| | Key Management (7 of 8 Q scored) | 43 | 63 | 122.9 | 180 | 68.3% |
| | **Security Subtotal** | | | **292.0** | **360** | **81.1%** |
| **Strategy** | Protocol Mechanics (7 of 9 Q scored) | 43 | 63 | 30.7 | 45 | 68.2% |
| | Collateral (4 Q) | 36 | 36 | 45.0 | 45 | 100.0% |
| | Infra Counterparty (8 Q) | 66 | 72 | 41.25 | 45 | 91.7% |
| | Protocol Counterparty (5 Q) | 33 | 45 | 33.0 | 45 | 73.3% |
| | Liquidity (9 Q) | 45 | 81 | 25.0 | 45 | 55.6% |
| | Market (5 Q) | 37 | 45 | 37.0 | 45 | 82.2% |
| | **Strategy Subtotal** | | | **211.95** | **270** | **78.5%** |
| **Operations** | Governance (3 of 4 Q scored) | 9 | 27 | 22.5 | 67.5 | 33.3% |
| | Team & Legal (7 of 9 Q scored) | 45 | 63 | 48.2 | 67.5 | 71.4% |
| | Documentation (6 Q) | 42 | 54 | 52.5 | 67.5 | 77.8% |
| | Financial Resilience (5 Q) | 11 | 45 | 16.5 | 67.5 | 24.4% |
| | **Operations Subtotal** | | | **139.7** | **270** | **51.7%** |
| **TOTAL** | | | | **643.65** | **900** | **71.5%** |

---
