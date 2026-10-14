# PeryaPH — Real-Money Launch Readiness Plan

**Current release:** Virtual-credit demo only  
**Real-money status:** DISABLED — do not accept deposits, wagers, or withdrawals  
**Repository:** https://github.com/annamabanlag-wq/Casino-Games

This plan is an engineering and compliance checklist, not a legal opinion or evidence of licensing. PeryaPH must not represent itself as PAGCOR-licensed unless that status has been formally granted and verified.

## Why the current build cannot handle cash

The current game frontend is a static HTML page. Its demo credits are maintained in browser JavaScript/local storage and its game outcomes are generated client-side. A player can change browser state and inspect or alter front-end code. Therefore those balances and outcomes cannot be treated as real money, authoritative game results, or a financial ledger.

GitHub Pages is a static hosting service; it is not a secure gaming-wallet backend. Do not connect a payment button directly to the current client-side credits.

## Recommended route

Before building cash wagering, ask PAGCOR's Electronic Gaming Licensing Department to confirm in writing which licensing and approval route applies to PeryaPH's proposed business model. PAGCOR's published description says it regulates local electronic gaming operations, handles gaming-platform/system and game-content evaluation, and describes online operations in connection with PAGCOR-licensed gaming venues. Read the current requirements directly:

- PAGCOR Electronic Gaming Licensing: https://www.pagcor.ph/regulatory/cegs.php
- PAGCOR regulatory announcements and application kits: https://www.pagcor.ph/regulatory/announcements-ebld.php
- PAGCOR responsible gaming: https://www.pagcor.ph/responsible-gaming/
- PAGCOR security-seal and platform verification entry point: https://www.pagcor.ph/

**Likely first commercial path to investigate:** a written partnership with a currently licensed operator and the appropriate PAGCOR-accredited gaming-system/service provider, rather than independently launching an unlicensed casino. Verify the operator's exact legal entity, license scope, registered brand/domain and the provider's accreditation directly with PAGCOR. Do not rely on screenshots, sales messages, or a broker's promises.

## Launch gates — every gate must be completed before cash play

### 1. Legal, licensing, and contracts
- Obtain Philippine gaming counsel's written advice on whether PeryaPH is acting as an operator, service provider, game supplier, or another regulated role.
- Obtain written PAGCOR guidance and the required license/accreditation/approval for that role, domain/brand, platform and each game.
- Sign agreements with the appropriate licensed operator and accredited system provider, including responsibility for player accounts, compliance, game approval, support, disputes, reports, funds and withdrawals.
- Confirm the permitted player locations, excluded locations, advertising and affiliate rules, and any requirements for hosting or venue operations.
- Do not claim the app is licensed before approval is granted and independently verified.

### 2. Game fairness and server-side game engine
- Move all outcomes and wager settlement to a trusted server. Never trust JavaScript, local storage, a client-supplied outcome, or client-supplied balance.
- Document each game rule, exact payout table, probability/math model, maximum exposure and edge cases.
- Use an approved cryptographically secure random-number implementation, with the independent game/RNG testing or certification required by the regulator and contracted operator.
- Use unique server-issued round IDs; make settlement idempotent; record outcomes and settlement decisions in tamper-evident audit logs.
- Add automated tests for edge cases, concurrency, replay attempts, insufficient funds, disconnects, duplicate callbacks and recovery after outages.

### 3. Player account, KYC and responsible gaming
- Do not rely on a checkbox or a self-declared birth date. Integrate the operator's approved identity and age-verification workflow; PAGCOR's public responsible-gaming page says people under 21 are prohibited from gambling.
- Implement restricted-player checks and the operator's approved Know Your Customer and anti-money-laundering controls.
- Implement self-exclusion, cooling-off/time-out, deposit/wager/loss limits where required, session reminders, account closure and complaint/dispute handling.
- Minimize personal information, encrypt it in transit and at rest, restrict staff access, define retention/deletion policies and complete a privacy impact assessment under Philippine data-protection requirements.
- Provide visible responsible-gaming messages and customer-support/escalation procedures.

### 4. Real-money wallet and payment operations
- Use only payment and withdrawal channels explicitly approved for the licensed operator and the planned gaming activity.
- Do not assume GCash QR, manual receipt review, ordinary payment links, or any particular e-wallet flow is permitted for gambling. Obtain written approval from the operator, regulator as applicable, and payment provider first.
- Never store card credentials or payment secrets in the frontend or repository. Use provider-hosted or tokenized payment methods and signed server-to-server callbacks where the approved provider supports them.
- Implement an append-only double-entry ledger in the backend, with balances calculated/reconciled server-side; unique transaction IDs; idempotency keys; deposit holds; wager debits; outcome credits; reversals; withdrawal review; reconciliation; and an auditable admin action log.
- Separate player funds and operating funds as required by the legal/contractual arrangement. Define refund, chargeback, failed-payment and withdrawal-dispute procedures before launch.

### 5. Security, hosting, and operations
- Build the backend and database in a controlled environment with secrets stored only in the hosting provider's secret manager, never in source code or browser JavaScript.
- Require multi-factor authentication and least privilege for administrators; add rate limits, bot/abuse controls, session security, monitoring, backups, alerting and incident response.
- Obtain independent penetration testing and complete applicable regulator/provider security assessments before production.
- Maintain separate demo, test/staging and production environments. Real-money credentials and routes must be absent from demo builds.
- Use an allowlist-based production feature flag enforced by the backend. If licenses/approvals, provider credentials, KYC controls, or payment configuration are missing or invalid, the backend must reject cash wagers and all deposit/withdrawal requests.

## Implementation sequence

1. **Pre-application:** confirm legal route with PAGCOR and Philippine gaming counsel.
2. **Partnership:** identify and verify an appropriate licensed operator/accredited system provider; secure written interest and responsibility split.
3. **Game pack:** document PeryaPH Color Game, Beto-Beto Dice, Number Ball, Video Karera and the remaining game rules/math for regulator/provider evaluation.
4. **Engineering:** develop the backend wallet, identity/compliance integrations, server-side RNG/game engine, audit logs and security controls in a test environment.
5. **Certification and acceptance:** complete the required tests, approvals, security reviews and contract acceptance.
6. **Controlled launch:** enable production only after written authorization and a formal go-live checklist signed by the responsible legal/compliance and technical owners.

## Current repository state

- index.html: mobile-friendly game lobby and browser-side virtual-credit gameplay.
- Cash deposits, cash wagers, and withdrawals are not implemented and must remain off.
- No live payment credentials, production gaming wallet, certified RNG, operator integration or proof of license is configured.
- The "Real-Money Launch Gate" in the UI is a status reminder, not a regulator approval or technical authorization switch.

## Acceptance checklist

- [ ] Written PAGCOR/legal route confirmed
- [ ] Licensed operator and required accredited provider verified
- [ ] PeryaPH brand/domain/platform and games approved as required
- [ ] Game rules, mathematics and RNG independently tested as required
- [ ] 21+ identity verification and restricted-player checks tested
- [ ] Responsible-gaming and self-exclusion flows tested
- [ ] Approved payment/withdrawal contract and callbacks verified
- [ ] Server wallet ledger reconciles correctly and has audit trails
- [ ] Independent security assessment completed
- [ ] Incident, dispute, privacy and customer-support procedures ready
- [ ] Written go-live approval recorded; only then consider enabling real-money mode
