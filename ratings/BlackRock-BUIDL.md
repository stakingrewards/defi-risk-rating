# BlackRock BUIDL - USD Institutional Digital Liquidity Fund Risk Rating

**Rating Date**: 2026-02-19
**Final Grade**: CCC+
**Total Score**: 630.4/900 points

---

## Detailed Analysis

### Security (40%) - Score: 170.4/360 (47.3%)

#### Smart Contract Security (20%) - 121.8/180

**[S-SC-01] Have all core contracts that hold or route funds been independently audited?**
- **Answer**: Yes. Securitize's DS Protocol (DSToken) has been audited by at least 2 independent firms: Halborn (Sep 2025, most recent) and CoinFabrik (earlier audit of DSToken/DS Protocol). The Halborn audit covered the full DSToken framework including TokenIssuer, ComplianceService, RegistryService, and transfer/swap/buy/redemption flows. CoinFabrik previously audited the DS Protocol contracts. The BUIDL token on Ethereum (0x7712c34205737192402172409a8f7ccef8aa2aec) is deployed using this audited framework.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Halborn audit: https://www.halborn.com/audits/securitize/dstoken-e07b34; [P1] CoinFabrik audit: https://www.coinfabrik.com/blog/securitize-smart-contract-audit/; [P0] Verified proxy on Etherscan: https://etherscan.io/address/0x7712c34205737192402172409a8f7ccef8aa2aec
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-SC-02] Who performed the most recent audit and what is their reputation tier?**
- **Answer**: The most recent audit (Sep 2025) was performed by Halborn, a Tier-1 auditor per the SR list. CoinFabrik is a smaller firm not on the SR tier list. Cyfrin has been referenced as working with Securitize per their 2024 wrap-up, but no specific public report was found. No Tier-0 auditor (Trail of Bits, OpenZeppelin, Sherlock, etc.) has audited the DS Protocol based on available evidence.
- **Current Score**: 3 (Mid Risk - most recent audit by Tier-1 only, no Tier-0)
- **Potential Score**: 9 (Low Risk - if Tier-0 audit commissioned)
- **Classification**: Improvable
- **Evidence**: [P1] Halborn audit page: https://www.halborn.com/audits/securitize/dstoken-e07b34; [P1] Halborn is Tier-1 per SR list; [P1] Cyfrin reference: https://www.cyfrin.io/blog/cyfrin-2024-wrapup-growth-education-security
- **Evidence Status**: Verified (Halborn Tier-1); Cyfrin claimed but unverified
- **Path to Potential**: Commission Tier-0 auditor (Trail of Bits, OpenZeppelin, or Sherlock)

**[S-SC-03] Have upgrades to core contracts been followed by new audits?**
- **Answer**: The Halborn audit was completed September 25, 2025, covering the current DSToken framework. The BUIDL proxy was deployed March 2024. No evidence of core contract upgrades since the September 2025 audit that would require additional audit coverage.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Halborn audit dates: Sep 1-25, 2025; [P0] Proxy deployment: Mar 2024 on Etherscan
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-SC-04] Have all critical and high-severity audit findings been fully remediated and re-verified?**
- **Answer**: The Halborn audit report states "Halborn identified several areas for improvement to reduce both the likelihood and impact of potential risks, which were successfully addressed by the Securitize team." Key findings (totalIssued burn logic, wallet validation in issueTokensCustom) were remediated. The earlier CoinFabrik audit found a storage collision issue (abi.encodePacked) that was acknowledged; remediation status for the current codebase is not explicitly confirmed but the Halborn re-audit provides current coverage.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Halborn report: https://www.halborn.com/audits/securitize/dstoken-e07b34; [P1] CoinFabrik: https://www.coinfabrik.com/blog/ds-token-security-audit-review/
- **Evidence Status**: Verified (Halborn confirms remediation)
- **Path to Potential**: N/A

**[S-SC-05] Are core contracts upgradeable and how tightly are upgrades constrained?**
- **Answer**: The BUIDL token (0x7712c34205737192402172409a8f7ccef8aa2aec) uses a custom proxy pattern with `setTarget()` and `setOwner()` functions restricted to `onlyOwner`. The owner can change the implementation at any time without timelock, governance vote, or multisig requirement on-chain. The proxy delegates all calls to an implementation contract (DSToken at 0x603Bb690...bE7fB83b2). While off-chain controls exist (Fireblocks MPC, operational procedures), on-chain there is no timelock and no public upgrade policy.
- **Current Score**: 1 (High Risk - upgradeable with no on-chain timelock, broad admin upgrade powers, constraints undocumented)
- **Potential Score**: 9 (Low Risk - if on-chain timelock >= 24h + multisig added)
- **Classification**: Improvable
- **Evidence**: [P0] Etherscan verified proxy code at 0x7712c34205737192402172409a8f7ccef8aa2aec: setTarget(onlyOwner), setOwner(onlyOwner); [P1] Fireblocks MPC: https://www.fireblocks.com/blog/securitize-integrates-fireblocks-to-improve-its-security-in-the-tokenization-of-real-world-assets
- **Evidence Status**: Verified on-chain
- **Path to Potential**: Add on-chain timelock (>=24h) and multisig for proxy upgrades

**[S-SC-06] Has any on-chain exploit or critical bug affecting user funds occurred?** (Deal Breaker)
- **Answer**: No confirmed exploit or critical bug affecting BUIDL user funds since launch in March 2024. No incidents reported across any of the nine chains where BUIDL is deployed.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P4] No exploit reports found in extensive searches; [P1] CertiK Skynet listing shows no incidents; [P0] No suspicious transactions on Etherscan token tracker
- **Evidence Status**: Verified (absence confirmed across multiple sources)
- **Path to Potential**: N/A

**[S-SC-07] Has any confirmed rug-pull event occurred?** (Deal Breaker)
- **Answer**: No confirmed rug-pull. BlackRock is the world's largest asset manager ($10T+ AUM), a publicly traded company (NYSE: BLK). The reputational and legal risk is effectively zero.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P2] SEC Form D filing; [P1] BlackRock NYSE-listed public company
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-SC-08] Were there reductions to the timelock delay that weaken governance protections?**
- **Answer**: No on-chain timelock exists for the BUIDL token contract. Since there was never a timelock to reduce, no reduction has occurred. The absence of a timelock is penalized separately in S-SC-05.
- **Current Score**: 9 (Low Risk - no reductions occurred)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already meets criteria)
- **Evidence**: [P0] No timelock contract found associated with BUIDL proxy on Etherscan
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-SC-09] Does the protocol run an active bug-bounty via a reputable platform?**
- **Answer**: BlackRock operates a Vulnerability Disclosure Program (VDP) on HackerOne (https://hackerone.com/blackrock). This is a disclosure program rather than a formal bounty with guaranteed payouts >= $100K. It covers BlackRock's technology infrastructure broadly. No smart-contract-specific bounty on Immunefi, Sherlock, or Code4rena for BUIDL/Securitize contracts was found.
- **Current Score**: 3 (Mid Risk - VDP exists on HackerOne but no documented payout >= $100K, narrow smart contract scope)
- **Potential Score**: 9 (Low Risk - if formal bounty with >= $100K max launched)
- **Classification**: Improvable
- **Evidence**: [P1] BlackRock HackerOne: https://hackerone.com/blackrock; [P1] https://www.blackrock.com/us/individual/compliance/responsible-disclosure
- **Evidence Status**: Verified (VDP exists; payout unclear; no Immunefi listing)
- **Path to Potential**: Launch dedicated smart contract bounty on Immunefi or equivalent with >= $100K max

**[S-SC-10] Are real-time security monitoring and alerting systems in place?**
- **Answer**: No public evidence of specific real-time on-chain monitoring for BUIDL smart contracts (e.g., Hypernative, Blockaid). BlackRock and Securitize almost certainly have operational monitoring given their institutional nature, but specifics about 24/7 on-chain invariant monitoring are not publicly documented. Fireblocks provides transaction monitoring at the wallet level.
- **Current Score**: 3 (Mid Risk - institutional monitoring likely but unverified for on-chain specifics)
- **Potential Score**: 9 (Low Risk - if documented monitoring system disclosed)
- **Classification**: Source Missing
- **Evidence**: [P1] Fireblocks wallet-level monitoring; no public docs on BUIDL-specific on-chain monitoring
- **Evidence Status**: Claimed but unverified
- **Path to Potential**: Publish monitoring setup details or confirm on-chain security monitoring provider

**[S-SC-11] Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts?**
- **Answer**: The DS Protocol includes compliance-level transfer restrictions and the ability to pause transfers via the ComplianceService. However, these are manual admin controls, not automatic invariant-triggered circuit breakers.
- **Current Score**: 3 (Mid Risk - manual triggers exist via compliance module but no automatic protections)
- **Potential Score**: 9 (Low Risk - if automatic monitoring-triggered pause implemented)
- **Classification**: Improvable
- **Evidence**: [P1] DS Protocol architecture: ComplianceService enforces restrictions; [P1] Halborn audit scope covers ComplianceService
- **Evidence Status**: Verified (manual controls exist)
- **Path to Potential**: Implement automatic invariant-breach triggered pause

**SC Subtotal: 9+3+9+9+1+9+9+9+3+3+3 = 67/99 -> (67/99) x 180 = 121.8**

#### Key Management & Permissions (20%) - 48.6/180

**[S-KM-01] Who controls admin and upgrade keys for contracts holding user funds?**
- **Answer**: The BUIDL proxy contract has a single `owner` address that controls both `setTarget()` (implementation upgrades) and `setOwner()` (ownership transfer). This owner is Securitize, operating via Fireblocks MPC wallet infrastructure. On-chain it presents as a single address. The MPC quorum and key share distribution for BUIDL are not publicly documented. No change history is publicly available.
- **Current Score**: 1 (High Risk - admin rights held by single entity on-chain; MPC details undocumented)
- **Potential Score**: 9 (Low Risk - if on-chain multisig with public documentation)
- **Classification**: Improvable
- **Evidence**: [P0] Etherscan proxy contract: single owner address; [P1] Fireblocks MPC: https://www.fireblocks.com/blog/securitize-integrates-fireblocks-to-improve-its-security-in-the-tokenization-of-real-world-assets
- **Evidence Status**: Verified (single address on-chain; off-chain MPC unverifiable)
- **Path to Potential**: Deploy on-chain multisig (e.g., Safe) with publicly documented signers

**[S-KM-02] Can any single key move user funds or upgrade custody contracts?** (Deal Breaker)
- **Answer**: Yes. The proxy owner can call `setTarget()` to point the proxy at any new implementation, which could include functions to drain all token balances. On-chain this is a single address. While Fireblocks MPC distributes key shares off-chain, there is no on-chain multisig or timelock requirement. No threshold >= 3 AND signers >= 5 on-chain.
- **Current Score**: 1 (High Risk - Deal Breaker triggered)
- **Potential Score**: 9 (Low Risk - if >= 3-of-5 multisig + >= 24h timelock on-chain)
- **Classification**: Improvable
- **Evidence**: [P0] Etherscan: setTarget(onlyOwner); single address control; [P1] Fireblocks MPC off-chain
- **Evidence Status**: Verified on-chain
- **Path to Potential**: Implement on-chain multisig >= 3-of-5 + timelock >= 24h

**[S-KM-03] How decentralized and robust is the multisig for critical actions?**
- **Answer**: No on-chain multisig exists. Critical actions controlled by single owner address backed by Fireblocks MPC (key shares distributed, Intel SGX hardware). Specific quorum, key share count, and identity of holders not publicly disclosed. On-chain: effectively single-entity control.
- **Current Score**: 1 (High Risk - no on-chain multisig; MPC not publicly verifiable)
- **Potential Score**: 9 (Low Risk - if on-chain multisig with verified independent signers)
- **Classification**: Improvable
- **Evidence**: [P0] No multisig contract on-chain; [P1] Fireblocks MPC: https://www.fireblocks.com/what-is-mpc
- **Evidence Status**: Verified (absence confirmed)
- **Path to Potential**: Deploy on-chain multisig >= 3-of-5 with public signer disclosure

**[S-KM-04] How constrained are pause, blocklist and withdrawal-control permissions?**
- **Answer**: The DS Protocol includes comprehensive compliance controls: ComplianceService enforces transfer restrictions, lockups, and jurisdictional investor limits. Admin can pause transfers globally and block specific addresses (whitelist management is core to the token's regulatory compliance model). Controls are broad by design for securities regulation -- only KYC-approved addresses can hold tokens. The scope is partially documented through DS Protocol architecture but detailed rules are not fully public.
- **Current Score**: 3 (Mid Risk - broad controls exist with Fireblocks MPC and are partially documented; serve regulatory purpose)
- **Potential Score**: 3 (Mid Risk - regulatory requirements mean broad controls remain necessary)
- **Classification**: Non-Improvable (regulatory requirement for securities transfer agent control)
- **Evidence**: [P0] DS Protocol compliance module on-chain; [P1] DS Protocol: https://medium.com/securitize/introducing-ds-digital-securities-protocol-securitizes-digital-ownership-architecture-for-4bcb6a9c4a16
- **Evidence Status**: Verified
- **Path to Potential**: N/A - broad controls inherent to regulated securities model

**[S-KM-05] Are all user assets held in non-custodial smart contracts?**
- **Answer**: No. BUIDL tokens on-chain represent shares in the fund, but the underlying assets (US T-bills, repos, cash) are held off-chain by BNY Mellon as custodian. 100% of the actual assets are in traditional custody. BNY Mellon is a systemically important financial institution and one of the most regulated custodians globally.
- **Current Score**: 1 (High Risk - 100% of underlying assets held off-chain)
- **Potential Score**: 1 (Non-Improvable - inherent to RWA tokenized fund model)
- **Classification**: Non-Improvable (structural feature)
- **Evidence**: [P1] BNY Mellon as custodian per SEC filing and press releases; [P2] SEC Form D
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-KM-06] Are user funds fully segregated from treasury and operational wallets?**
- **Answer**: Yes. The fund is a separate BVI legal entity (BlackRock USD Institutional Digital Liquidity Fund Ltd.) with BNY Mellon as dedicated custodian. Fund assets are legally and operationally segregated from BlackRock's proprietary assets and Securitize's operational funds by traditional fund structures and regulatory requirements.
- **Current Score**: 9 (Low Risk - clear legal and operational segregation)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P2] SEC Form D: BVI entity; [P1] BNY Mellon custody
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-KM-07] What are the whitelisted protocols the vault strategy can interact with?**
- **Answer**: N/A. BUIDL is not a vault deploying funds into DeFi protocols. The underlying assets are US Treasuries and repos held at BNY Mellon.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A
- **Evidence**: Fund invests 100% in cash, T-bills, and repos
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[S-KM-08] Is there a tested incident playbook for admin-key compromise or signer loss?**
- **Answer**: No public evidence of a documented incident playbook specific to BUIDL/Securitize operations. BlackRock has enterprise incident response procedures and Fireblocks provides key recovery/rotation mechanisms (MPC key share rotation). However, no BUIDL-specific playbook or tabletop exercise has been publicly disclosed.
- **Current Score**: 1 (High Risk - no documented playbook publicly available)
- **Potential Score**: 9 (Low Risk - if documented and tested playbook published)
- **Classification**: Source Missing
- **Evidence**: No public documentation found; [P1] Fireblocks key rotation: https://www.fireblocks.com/what-is-mpc
- **Evidence Status**: Missing
- **Path to Potential**: Publish incident response playbook with key rotation procedures and testing cadence

**KM Subtotal (7 scored, 1 N/A): 1+1+1+3+1+9+1 = 17/63 -> (17/63) x 180 = 48.6**

**Security Total: 121.8 + 48.6 = 170.4/360 (47.3%)**

---

### Strategy (30%) - Score: 250.0/270 (92.6%)

#### Protocol Mechanics (5%) - 45.0/45

**[ST-PM-01] What are the sources of yield and is it aligned with the mandate?**
- **Answer**: 100% of yield comes from US Treasury bill interest, repurchase agreement returns, and cash interest -- fully aligned with the stated mandate of "current income consistent with liquidity and stability of principal." Yield is approximately 4% (tracking federal funds rate minus 0.20-0.50% management fee). All yield is organic from underlying government securities.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Fund description: https://securitize.io/blackrock/buidl; [P2] SEC filing; [P3] RWA.xyz: https://app.rwa.xyz/assets/BUIDL
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-02] Under which conditions does net yield become negative or cause loss?**
- **Answer**: Negative yield limited to extreme tail scenarios: (1) federal funds rate dropping below management fee (~0.20-0.50%), requiring near-zero rate policy; (2) US Treasury default (unprecedented). Short-duration T-bill portfolio has minimal interest rate risk.
- **Current Score**: 9 (Low Risk - limited to rare tail shocks)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Fund invests in T-bills and overnight repos; [P3] Current yield ~4%
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-03] Is leverage or rehypothecation used and up to what effective level?**
- **Answer**: No leverage or rehypothecation. 100% direct investment in T-bills, repos, and cash. Effective leverage is 1.0x.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Fund description: 100% T-bills, repos, cash
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-04] Are there automated mechanics to prevent Liquidation Events?**
- **Answer**: N/A. Not a lending protocol; no LTV ratios, collateral, or liquidation mechanics.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A
- **Path to Potential**: N/A

**[ST-PM-05] Has this strategy or a close variant ever experienced negative yield?** (Deal Breaker)
- **Answer**: N/A. Not a DeFi lending/vault strategy. Traditional T-bill money market funds have decades of track record.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A
- **Path to Potential**: N/A

**[ST-PM-06] Is a risk framework for vault curation or protocol mechanics documented?**
- **Answer**: N/A. Not a vault with curation. Investment guidelines governed by offering memorandum and BlackRock's framework.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A
- **Path to Potential**: N/A

**[ST-PM-07] Is current yield sustainable relative to underlying economics?**
- **Answer**: 100% organic from US Treasury interest and repo rates. Zero dependence on incentives, emissions, or token rewards. Sustainable economic model functioning for decades in traditional finance.
- **Current Score**: 9 (Low Risk - 100% organic yield)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Fund description; [P3] Yield data on RWA.xyz
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-08] Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative?**
- **Answer**: Yes. Underlying T-bills and overnight repos are the most liquid instruments globally. Entire portfolio can unwind within days with near-zero price impact. Circle USDC instant facility (up to $20M) provides immediate on-chain off-ramp.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Circle facility: https://www.circle.com/pressroom/circle-announces-usdc-smart-contract-for-transfers-by-blackrocks-buidl-fund-investors
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PM-09] Does the strategy rely on a spread, peg, or funding rate that can invert?**
- **Answer**: No. Yield comes directly from US Treasury interest rates. No carry trade, peg dependency, or funding rate arbitrage.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Fund structure: direct T-bill ownership
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**PM Subtotal (6 scored, 3 N/A): 9+9+9+9+9+9 = 54/54 -> (54/54) x 45 = 45.0**

#### Collateral (5%) - 45.0/45

**[ST-C-01] Which assets are accepted as collateral and how are they risk rated?**
- **Answer**: Fund holds US Treasury bills, repurchase agreements (collateralized by US Treasuries), and cash. Highest-quality assets globally, rated AAA by all major agencies.
- **Current Score**: 9 (Low Risk - exclusively US Treasuries and cash)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Fund mandate; [P2] SEC filing
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-C-02] How did each collateral behave versus its underlying during past stress or depegs?**
- **Answer**: US T-bills are the ultimate safe-haven asset; they appreciate during crises. BUIDL has maintained $1.00 peg since March 2024 through multiple market events including August 2025 stress.
- **Current Score**: 9 (Low Risk - no depeg; T-bills are global safe haven)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P3] CoinGecko price data; [P1] T-bill behavior during stress is well-documented
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-C-03] How is validator or slashing risk handled for staking-based collaterals?**
- **Answer**: N/A. No staking-based collateral.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A
- **Path to Potential**: N/A

**[ST-C-04] What share of TVL relies on bridged or wrapped assets?**
- **Answer**: On Ethereum (primary chain), BUIDL is a native token. Cross-chain deployments are separate share classes via Wormhole, not wrapped versions. Underlying T-bill assets are not bridged. 0% bridged assets on the primary chain.
- **Current Score**: 9 (Low Risk - native on primary chain)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P0] Etherscan: native ERC-20; [P1] Wormhole provides interoperability for separate share classes
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**C Subtotal (3 scored, 1 N/A): 9+9+9 = 27/27 -> (27/27) x 45 = 45.0**

#### Infra Counterparty Exposures (5%) - 30.0/45

**[ST-IC-01] Which chains, bridges, oracles, wallets and CEXs does the strategy depend on?**
- **Answer**: Primary chain: Ethereum (Tier-0). Bridge: Wormhole (Tier-2) for cross-chain share classes. Oracle: BNY Mellon on-chain NAV feed (institutional-grade). Wallet: Fireblocks MPC. Custodian: BNY Mellon. All dependencies known but Wormhole is Tier-2 per SR list.
- **Current Score**: 3 (Mid Risk - Wormhole is Tier-2)
- **Potential Score**: 9 (if Wormhole upgraded or replaced)
- **Classification**: Improvable
- **Evidence**: [P1] Wormhole integration: https://wormhole.com/blog/securitize-announces-the-live-deployment-of-wormhole-enabling-tokenized; [P0] Ethereum Tier-0
- **Evidence Status**: Verified
- **Path to Potential**: Migrate cross-chain interoperability to Tier-0 bridge (Chainlink CCIP or Across)

**[ST-IC-02] How redundant and battle-tested are the oracle and bridge setups?**
- **Answer**: BNY Mellon NAV feed launched April 2025 (novel, limited battle-testing but world's largest custodian). Wormhole is sole cross-chain bridge (Tier-2, $320M exploit Feb 2022 -- Jump Trading compensated all users). No fallback bridge. For Ethereum-only use, bridge is not critical.
- **Current Score**: 3 (Mid Risk - single Tier-2 bridge; novel NAV feed)
- **Potential Score**: 9
- **Classification**: Improvable
- **Evidence**: [P1] Wormhole exploit: https://techcrunch.com/2023/07/27/wormhole-new-security-320m-hack/; [P1] BNY NAV feed: https://www.bny.com/corporate/global/en/about-us/newsroom/press-release/bny-expands-digital-asset-platform-with-launch-of-innovative-on-chain-offering.html
- **Evidence Status**: Verified
- **Path to Potential**: Add bridge redundancy or upgrade to Tier-0 bridge (Chainlink CCIP or Across)

**[ST-IC-03] Are off-chain infrastructure providers certified by standard IT security audits?**
- **Answer**: Yes. Fireblocks: SOC 2 Type II (EY) + ISO 27001. BNY Mellon: SIFI-regulated (OCC, Fed, FDIC). BlackRock: SEC-registered. PwC: Big Four. Securitize: SEC-registered transfer agent + FINRA broker-dealer.
- **Current Score**: 9 (Low Risk - all critical providers certified/regulated)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Fireblocks SOC 2: https://www.fireblocks.com/press/ernst-and-young-grants-soc-2-type-ii-certification-to-fireblocks/; [P1] Securitize SEC: https://www.finextra.com/pressarticle/79561/securitize-becomes-an-sec-registered-transfer-agent
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-IC-04] How did these infra components behave in past outages or chain incidents?**
- **Answer**: BUIDL operational since March 2024 (nearly 2 years). No reported infrastructure failures. Ethereum no significant halt. Wormhole no exploit since 2022 (pre-BUIDL). Fund operated through multiple market conditions including October 2025 stress. Deployed >= 6 months with no incidents.
- **Current Score**: 9 (Low Risk - >= 6 months with no incidents)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P0] Continuous operations on Etherscan since March 2024; [P1] No incidents found
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-IC-05] Has the base chain recently halted block production or experienced consensus failure?**
- **Answer**: Ethereum has not experienced a chain halt > 30 minutes in the last 12 months.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P0] Ethereum continuous block production; [P3] No halt reported
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-IC-06] Has the validator set experienced slashing events that could impact staked collateral?**
- **Answer**: N/A. No staking-based collateral or proprietary validator dependency.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A
- **Path to Potential**: N/A

**[ST-IC-07] Are validators diverse geographically and by operator?**
- **Answer**: N/A. No proprietary validator set. Uses public blockchain infrastructure.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A
- **Path to Potential**: N/A

**[ST-IC-08] Can any single infra component failure alone block withdrawals or cause losses?**
- **Answer**: Securitize (transfer agent) is a critical dependency for token operations. Securitize outage would delay transfers and redemptions. However, underlying fund assets at BNY Mellon are independent. BlackRock could appoint a new transfer agent. Legal fund structure provides recourse beyond on-chain mechanics. Single failure can delay but not permanently block.
- **Current Score**: 3 (Mid Risk - Securitize failure could delay 24-48h but not permanently block)
- **Potential Score**: 3 (Non-Improvable - transfer agent model inherent)
- **Classification**: Non-Improvable (inherent to regulated fund structure)
- **Evidence**: [P1] Securitize as sole transfer agent; [P1] BNY Mellon as custodian; [P2] Legal fund structure
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**IC Subtotal (6 scored, 2 N/A): 3+3+9+9+9+3 = 36/54 -> (36/54) x 45 = 30.0**

#### Protocol Counterparty Exposures (5%) - 45.0/45

**[ST-PC-01] Into which external protocols, CEXs or RWA platforms is collateral deployed?**
- **Answer**: Assets deployed into US T-bills (via primary dealers/secondary market) and overnight repos -- standard institutional finance infrastructure. No DeFi protocol deployment. All venues are highest-tier global financial infrastructure.
- **Current Score**: 9 (Low Risk - exclusively Tier-0 traditional finance venues)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Fund mandate: T-bills, repos, cash; [P2] SEC filing
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PC-02] Are revenue-share or incentive arrangements documented and do they create conflicts?**
- **Answer**: Management fee (0.20-0.50% depending on share class) is standard and disclosed. BlackRock earns management fee; Securitize earns tokenization fees. Standard institutional fund economics with aligned incentives.
- **Current Score**: 9 (Low Risk - standard disclosed fee structure)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Fee range confirmed by multiple sources; [P2] SEC filing
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PC-03] Are there hard limits and rebalancing rules per counterparty?**
- **Answer**: Fund invests in US Treasuries, repos, and cash. Concentration governed by SEC money market fund regulations and BlackRock's institutional guidelines. Primary "counterparty" is the US government.
- **Current Score**: 9 (Low Risk - governed by SEC regulations and institutional framework)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Fund structure; [P2] SEC regulatory framework
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PC-04] How quickly and safely can positions be unwound from each counterparty?**
- **Answer**: US T-bills trade in a $25+ trillion market. Overnight repos mature daily. Fund can unwind virtually 100% of positions within 1-2 business days with zero material slippage. Circle USDC facility provides immediate on-chain off-ramp.
- **Current Score**: 9 (Low Risk - near-instant unwind capability)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] T-bill market depth; [P1] Circle facility
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-PC-05] Are third-party validators, custody providers or asset managers disclosed?** (Deal Breaker)
- **Answer**: All fully disclosed: BNY Mellon (custodian/admin), BlackRock Financial Management (investment manager), Securitize LLC (transfer agent), Securitize Markets LLC (placement agent), PwC (auditor), Fireblocks (wallet/MPC), Wormhole (cross-chain). Subscriber custodians: Anchorage Digital, BitGo, Copper, Fireblocks.
- **Current Score**: 9 (Low Risk - all third parties fully disclosed with roles)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] https://securitize.io/blackrock/buidl; [P2] SEC Form D; [P1] Multiple press releases
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**PC Subtotal (5 scored): 9+9+9+9+9 = 45/45 -> (45/45) x 45 = 45.0**

#### Liquidity (5%) - 40.0/45

**[ST-L-01] How are withdrawals executed and can they be paused, blocked or delayed?**
- **Answer**: Redemptions processed through Securitize (transfer agent). Token transfers require whitelist compliance and can be paused/blocked by admin for regulatory reasons. Withdrawals rely on Securitize's off-chain processing. Admin can selectively block addresses and pause transfers as required by securities regulations.
- **Current Score**: 1 (High Risk - can be selectively blocked; rely on off-chain approval)
- **Potential Score**: 1 (Non-Improvable - regulatory requirement)
- **Classification**: Non-Improvable (transfer agent control legally required for registered securities)
- **Evidence**: [P1] Securitize as transfer agent; [P1] DS Protocol compliance module
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-02] Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time?**
- **Answer**: Yes. T-bills and repos are the most liquid instruments globally. Circle USDC instant facility ($20M). Uniswap/UniswapX integration (Feb 2026) with market makers (Flowdesk, Tokka Labs, Wintermute).
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Circle facility; [P1] Uniswap: https://blog.uniswap.org/unlocking-defi-liquidity-for-buidl
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-03] Have there been past withdrawal delays, queues or freezes?**
- **Answer**: No reported delays, queues, or freezes in nearly 2 years of operation. $447M net outflows in August 2025 processed without incident.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P4] Aug 2025 outflow reports; [P3] RWA.xyz data
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-04] Do caps or limits restrict timely redemptions during high utilization?**
- **Answer**: Minimum redemption $250K. No redemption caps or gates beyond this. Circle facility has a $20M cap but formal redemptions through Securitize are not capped.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] $250K minimum; no reported caps
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-05] How does exit liquidity behave during volatility and network congestion?**
- **Answer**: BUIDL processed $447M in August 2025 outflows during market volatility without disruption. T-bill market deepens during volatility (flight to safety). Off-chain redemptions independent of blockchain congestion.
- **Current Score**: 9 (Low Risk - demonstrated resilience)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P4] Aug 2025 outflows reported; [P1] T-bill flight-to-safety dynamics
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-06] Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period?**
- **Answer**: No. T-bills mature within days-to-weeks; repos are overnight. No unstaking, vesting, or bridge delays for underlying assets.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] T-bill maturities; overnight repos
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-07] Does redemption depend on secondary-market liquidity and is it sufficient?**
- **Answer**: No. Primary redemption through Securitize with direct fund asset liquidation. Circle USDC facility and Uniswap integration provide supplementary options. Secondary markets optional.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Direct redemption through Securitize; [P1] Uniswap integration
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-08] What is the liquidity depth of collateral and receipt tokens?**
- **Answer**: Underlying collateral (US T-bills) has effectively unlimited depth. BUIDL token secondary market is KYC-gated but growing (Circle facility, Uniswap market makers). Constraint is access restriction, not asset liquidity.
- **Current Score**: 9 (Low Risk - underlying liquidity unlimited)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] US Treasury market; [P1] Market makers on Uniswap
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-L-09] What is the risk of bank-run scenarios under full utilization?**
- **Answer**: N/A. Not a lending protocol; no utilization rate. All assets are liquid T-bills and repos with no leverage.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A
- **Path to Potential**: N/A

**L Subtotal (8 scored, 1 N/A): 1+9+9+9+9+9+9+9 = 64/72 -> (64/72) x 45 = 40.0**

#### Market (5%) - 45.0/45

**[ST-M-01] How has the LST or receipt token peg performed under market stress?**
- **Answer**: BUIDL has maintained $1.00 per token since March 2024 without any depeg. During August 2025 stress ($447M outflows), token maintained value without disruption. Peg maintained by direct asset backing.
- **Current Score**: 9 (Low Risk - maintained through all conditions)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P3] CoinGecko: https://www.coingecko.com/en/coins/blackrock-usd-institutional-digital-liquidity-fund
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-M-02] How likely can adverse crypto market moves cause permanent losses due to directional exposure?**
- **Answer**: Zero crypto-directional exposure. 100% US Treasuries, repos, and cash. Crypto drawdowns have no direct impact on NAV.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Fund mandate: 100% T-bills, repos, cash
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-M-03] Are interest rate/incentive models robust during TVL shifts or volatility spikes?**
- **Answer**: Yield tracks federal funds rate minus management fee. No utilization curve, no incentive model, no reflexive dynamics. During $447M August 2025 outflows, yield remained stable.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Fixed-rate T-bill portfolio
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-M-04] Have historic scenarios with high market volatility been explicitly modeled?**
- **Answer**: BlackRock uses Aladdin (proprietary risk analytics) and SEC-mandated money market fund stress testing. Real-world resilience demonstrated in August 2025. Institutional risk management exceeds typical DeFi protocol analysis.
- **Current Score**: 9 (Low Risk - institutional risk management + regulatory requirements + demonstrated resilience)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] BlackRock Aladdin; [P2] SEC stress testing requirements; [P4] Aug 2025 demonstrated resilience
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[ST-M-05] Can sharp price moves trigger forced liquidations that crystallize losses?**
- **Answer**: No. No leverage, no liquidation mechanics. US T-bills cannot be "liquidated." 1.0x effective leverage.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] 100% T-bills/repos/cash; zero leverage
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**M Subtotal (5 scored): 9+9+9+9+9 = 45/45 -> (45/45) x 45 = 45.0**

**Strategy Total: 45.0 + 45.0 + 30.0 + 45.0 + 40.0 + 45.0 = 250.0/270 (92.6%)**

---

### Operations (30%) - Score: 210.0/270 (77.8%)

#### Governance (7.5%) - 22.5/67.5

**[O-G-01] What governance model controls protocol changes and upgrades?**
- **Answer**: BUIDL operates as a traditional regulated fund with corporate governance (Board of Directors: Ian Pilgrim, Jennifer Collins, W. William Woods, Noelle L'Heureux). BlackRock Financial Management acts as investment manager under board oversight. Securitize manages token operations as SEC-registered transfer agent. On the smart contract level, Securitize has unilateral control within extensive off-chain regulatory oversight.
- **Current Score**: 3 (Mid Risk - hybrid model where multisig/team can execute upgrades within documented bounds of regulatory framework)
- **Potential Score**: 9 (if on-chain governance constraints added)
- **Classification**: Improvable
- **Evidence**: [P2] SEC Form D: board members listed; [P1] Securitize as transfer agent
- **Evidence Status**: Verified
- **Path to Potential**: Add on-chain governance constraints (timelock, multisig)

**[O-G-02] How concentrated is voting power among top holders or delegates?**
- **Answer**: N/A. No governance token; no on-chain voting. BUIDL tokens are fund shares, not governance rights.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A
- **Path to Potential**: N/A

**[O-G-03] Are mechanisms in place to limit major changes like timelocks and veto?**
- **Answer**: On-chain: No timelock or veto. Off-chain: BVI corporate governance, SEC requirements, offering memorandum terms, Board oversight. Investors receive notices of material changes per fund documentation. However, no on-chain timelock exists.
- **Current Score**: 3 (Mid Risk - off-chain timelocks via regulatory framework; no on-chain mechanisms)
- **Potential Score**: 9 (if on-chain timelock >= 24h added)
- **Classification**: Improvable
- **Evidence**: [P0] No timelock on-chain; [P2] BVI governance + SEC oversight
- **Evidence Status**: Verified
- **Path to Potential**: Implement on-chain timelock (>= 24h) for contract changes

**[O-G-04] Can the protocol replace the strategy manager without blocking user withdrawals?**
- **Answer**: N/A. Not a vault with replaceable strategy manager. BlackRock is the investment manager; replacement would follow fund governance structure.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A
- **Path to Potential**: N/A

**G Subtotal (2 scored, 2 N/A): 3+3 = 6/18 -> (6/18) x 67.5 = 22.5**

#### Team & Legal & Compliance (7.5%) - 67.5/67.5

**[O-TL-01] Are core team and operating entities publicly identified and credible?**
- **Answer**: Yes. BlackRock, Inc. (NYSE: BLK, $10T+ AUM). CEO: Larry Fink. Securitize CEO: Carlos Domingo (PhD CS, ex-Telefonica). BNY Mellon (est. 1784, $46.5T under custody). Among the most credible entities globally.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] BlackRock NYSE-listed; [P1] Carlos Domingo LinkedIn; [P2] SEC Form D
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-02] Is the protocol dependent on a single developer or small team?**
- **Answer**: No. BlackRock: 19,000+ employees. Securitize: global team across Miami, NY, London, SF, Tel Aviv. BNY Mellon: 50,000+ employees. No key-person dependency. Securitize going public at $1.25B valuation.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] BlackRock; [P1] Securitize SPAC; [P1] BNY Mellon
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-03] What legal entity and jurisdiction operate the protocol and/or assets?**
- **Answer**: BlackRock USD Institutional Digital Liquidity Fund Ltd. (BVI). BlackRock Financial Management, Inc. (Delaware). Securitize, LLC (Delaware/Miami). Securitize Markets, LLC (FINRA-registered). BNY Mellon (New York). All recognized jurisdictions.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P2] SEC Form D; [P1] FINRA BrokerCheck: https://brokercheck.finra.org/firm/summary/283256
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-04] Are there known investigations or regulatory actions related to the entity?** (Deal Breaker)
- **Answer**: No known investigations or enforcement actions against BlackRock, Securitize, or BUIDL specifically. Securitize maintains active SEC registrations.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P2] No SEC enforcement filings found; [P1] Active SEC registrations
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-05] Is there an on-call and incident response process for core teams?**
- **Answer**: BlackRock and BNY Mellon are SIFIs with 24/7 operational capabilities. Securitize operates across multiple time zones. Fireblocks provides 24/7 operational support. Institutional infrastructure supports continuous operations.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Institutional 24/7 operations; [P1] Global office distribution
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-06] Does the team provide timely support for critical user or integrator issues?**
- **Answer**: Securitize provides dedicated support. SEC transfer agent requirements mandate investor communication. Uniswap integration demonstrated coordinated multi-party support. No reports of ignored critical issues.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] SEC transfer agent requirements; [P1] Uniswap integration coordination
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-07] Are major investors or strategic partners disclosed?**
- **Answer**: Yes. Securitize investors: BlackRock (led $47M round), Morgan Stanley, ARK Invest, Blockchain Capital, ParaFi Capital. Partners: Uniswap Labs, Wormhole, Circle, Binance, Crypto.com, Deribit, Ondo Finance, Ethena.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Securitize funding: https://www.prnewswire.com/news-releases/securitize-announces-47-million-strategic-funding-round-led-by-blackrock-302133075.html
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-TL-08] Does the strategy manager manage similar vaults creating conflict of interest?**
- **Answer**: N/A. Not a vault with a curator/strategy manager.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A
- **Path to Potential**: N/A

**[O-TL-09] Has the strategy manager previously been involved in products with collateral loss?**
- **Answer**: N/A. Not a vault with a strategy manager.
- **Current Score**: N/A
- **Potential Score**: N/A
- **Classification**: N/A
- **Path to Potential**: N/A

**TL Subtotal (7 scored, 2 N/A): 9+9+9+9+9+9+9 = 63/63 -> (63/63) x 67.5 = 67.5**

#### Documentation & Transparency (7.5%) - 52.5/67.5

**[O-DT-01] Is there up-to-date documentation explaining architecture, strategy mechanics, and risks?**
- **Answer**: Documentation exists across: Securitize BUIDL product page, SEC Form D, offering memorandum, Steakhouse Financial analysis, press releases, DS Protocol Medium posts, GitHub (interfaces), and Halborn audit report. Updated with each chain expansion. Comprehensive though distributed.
- **Current Score**: 9 (Low Risk - comprehensive documentation, updated regularly)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] https://securitize.io/blackrock/buidl; [P2] SEC Form D; [P1] Halborn audit; [P1] https://steakhouse.financial/projects/blackrock-buidl
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-DT-02] Is it clearly documented how collateral is used and when loss occurs?**
- **Answer**: Yes. Fund mandate clearly states 100% T-bills, repos, cash. Loss scenarios limited to US government default (unprecedented), repo counterparty failure (mitigated by collateralization), or smart contract exploit. Well-documented across multiple analyses.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] Fund mandate; [P1] Steakhouse analysis
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-DT-03] Are all contract, proxy and implementation addresses documented in one canonical place?**
- **Answer**: Token addresses available on Etherscan, RWA.xyz, and various block explorers across 9 chains. No single canonical registry page listing all contracts in one place.
- **Current Score**: 3 (Mid Risk - addresses documented but spread across multiple sources)
- **Potential Score**: 9 (if canonical registry created)
- **Classification**: Improvable
- **Evidence**: [P0] Etherscan: https://etherscan.io/token/0x7712c34205737192402172409a8f7ccef8aa2aec; [P3] RWA.xyz
- **Evidence Status**: Verified
- **Path to Potential**: Create single canonical page listing all contracts across all chains

**[O-DT-04] Are roles, permissions and timelocks documented with visible change history?**
- **Answer**: DS Protocol architecture describes roles (owner, compliance service, registry service, trust service). Proxy owner visible on Etherscan. No central registry of all role assignments across chains, no formal change log.
- **Current Score**: 3 (Mid Risk - role architecture documented; change history absent)
- **Potential Score**: 9 (if central registry with change log published)
- **Classification**: Improvable
- **Evidence**: [P1] DS Protocol on Medium; [P0] Owner visible on Etherscan; [P1] Halborn audit covers roles
- **Evidence Status**: Verified
- **Path to Potential**: Publish central role registry with change log

**[O-DT-05] Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities?** (Deal Breaker)
- **Answer**: Yes. BNY Mellon broadcasts fund accounting data (NAV) to Ethereum blockchain via Digital Asset Data Insights (launched April 2025). PwC provides financial audit. Combination of on-chain NAV feed + Big Four audit provides institutional-grade proof of reserves. Proof-of-liabilities N/A (no borrowing).
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] BNY Mellon: https://www.bny.com/corporate/global/en/about-us/newsroom/press-release/bny-expands-digital-asset-platform-with-launch-of-innovative-on-chain-offering.html; [P2] PwC as fund auditor
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-DT-06] Are all contracts verified on the leading block explorers?**
- **Answer**: Yes. BUIDL token proxy (0x7712c34205737192402172409a8f7ccef8aa2aec) verified on Etherscan with source code (Solidity v0.8.13). Implementation contract (DSToken) also verified. BUIDL-I variant verified. Contracts on other chains verified on respective explorers.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P0] Etherscan verified: https://etherscan.io/address/0x7712c34205737192402172409a8f7ccef8aa2aec
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**DT Subtotal (6 scored): 9+9+3+3+9+9 = 42/54 -> (42/54) x 67.5 = 52.5**

#### Financial Resilience (7.5%) - 67.5/67.5

**[O-FR-01] Is there a backstop reserve or safety module for user losses?**
- **Answer**: The institutional framework provides multiple layers: BNY Mellon custodial insurance, BlackRock's corporate balance sheet ($10T+ AUM), SEC regulatory protections, BVI legal entity structure. Fund assets (T-bills) are essentially risk-free. Institutional backstop is among the strongest possible.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] BlackRock: $10T+ AUM; [P1] BNY Mellon: SIFI; [P2] BVI legal entity
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-FR-02] How large and liquid are the backstop reserves and treasury relative to TVL?**
- **Answer**: BlackRock: $10.5T AUM, billions in corporate equity. BNY Mellon: $46.5T under custody. Backstop for a $2.4B fund is orders of magnitude larger than any DeFi treasury.
- **Current Score**: 9 (Low Risk)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] BlackRock financials; [P1] BNY Mellon
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-FR-03] What is the estimated operational runway at current burn?**
- **Answer**: BlackRock: 2024 revenue ~$20B, net income ~$6B. Securitize: $4B+ AUM, going public at $1.25B valuation with $225M PIPE. Runway effectively unlimited for both entities.
- **Current Score**: 9 (Low Risk - runway > 24 months by orders of magnitude)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P1] BlackRock NYSE-listed; [P1] Securitize SPAC
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-FR-04] How have TVL, revenue and buffers behaved in past stress events?**
- **Answer**: August 2025: $447M net outflows (-15% MoM). Orderly, no operational issues, NAV maintained, no gates/delays. Revenue decreased proportionally but fund remained fully operational. Demonstrated real-world stress resilience.
- **Current Score**: 9 (Low Risk - demonstrated resilience)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P4] Aug 2025 outflow reports; [P3] RWA.xyz data
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**[O-FR-05] Can the protocol remain safe in maintenance mode if team disappears?**
- **Answer**: If Securitize disappeared: token operations halt but fund assets at BNY Mellon unaffected. BlackRock could appoint new transfer agent. If BlackRock disappeared (implausible): BVI entity and BNY Mellon custody protect assets. Off-chain legal/custodial structure provides robust fallback.
- **Current Score**: 9 (Low Risk - off-chain structure ensures asset safety)
- **Potential Score**: 9
- **Classification**: Non-Improvable (already optimal)
- **Evidence**: [P2] BVI legal entity; [P1] BNY Mellon custody; [P1] BlackRock
- **Evidence Status**: Verified
- **Path to Potential**: N/A

**FR Subtotal (5 scored): 9+9+9+9+9 = 45/45 -> (45/45) x 67.5 = 67.5**

**Operations Total: 22.5 + 67.5 + 52.5 + 67.5 = 210.0/270 (77.8%)**

---

## Final Score Calculation

| Category | Subcategory | Questions | Scored | N/A | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|--------|-----|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security | 11 | 11 | 0 | 67 | 99 | 121.8 | 180 | 67.7% |
| | Key Management | 8 | 7 | 1 | 17 | 63 | 48.6 | 180 | 27.0% |
| | **Security Subtotal** | **19** | **18** | **1** | | | **170.4** | **360** | **47.3%** |
| **Strategy** | Protocol Mechanics | 9 | 6 | 3 | 54 | 54 | 45.0 | 45 | 100.0% |
| | Collateral | 4 | 3 | 1 | 27 | 27 | 45.0 | 45 | 100.0% |
| | Infra Counterparty | 8 | 6 | 2 | 36 | 54 | 30.0 | 45 | 66.7% |
| | Protocol Counterparty | 5 | 5 | 0 | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity | 9 | 8 | 1 | 64 | 72 | 40.0 | 45 | 88.9% |
| | Market | 5 | 5 | 0 | 45 | 45 | 45.0 | 45 | 100.0% |
| | **Strategy Subtotal** | **40** | **33** | **7** | | | **250.0** | **270** | **92.6%** |
| **Operations** | Governance | 4 | 2 | 2 | 6 | 18 | 22.5 | 67.5 | 33.3% |
| | Team & Legal | 9 | 7 | 2 | 63 | 63 | 67.5 | 67.5 | 100.0% |
| | Documentation | 6 | 6 | 0 | 42 | 54 | 52.5 | 67.5 | 77.8% |
| | Financial Resilience | 5 | 5 | 0 | 45 | 45 | 67.5 | 67.5 | 100.0% |
| | **Operations Subtotal** | **24** | **20** | **4** | | | **210.0** | **270** | **77.8%** |
| **TOTAL** | | **83** | **71** | **12** | | | **630.4** | **900** | **70.0%** |

---


---
