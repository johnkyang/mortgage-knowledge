# Change Log

_Running log of all ingestion, edits, lint runs, and scenario builds._

---

## 2026-04-08 — Ingestion: FNMA Selling Guide (April 1, 2026) — Credit Section (pp. 469–527)

- **Source**: Selling-Guide_04-01-2026_Highlighted.pdf (trust level: official — FNMA)
- **Pages created**: [[credit-score-requirements]], [[dti-limits]], [[minimum-tradelines]], [[bankruptcy]], [[foreclosure]], [[short-sale-deed-in-lieu]]
- **Pages updated**: [[derogatory-credit-event-seasoning]] (upgraded lender notes to official citations; added DU override codes, timeshare exception, multiple BK clarification), [[credit-score-selection]] (upgraded to official; added average median score calculation, foreign credit report rules), [[past-due-collections-chargeoffs]] (upgraded to official; added DU vs. manual UW distinction, B3-5.3-09 vs. B3-6-07 separation), [[authorized-user-accounts]] (upgraded FNMA DU and manual UW sections to official citations per B3-5.3-06 and B3-5.3-09), [[nontraditional-credit-history]] (full upgrade with B3-5.4-01/02/03 content: eligibility, reference counts, reference types, documentation standards, quality standards), [[no-credit-score-borrowers]] (added official FNMA eligibility rules; clarified loanDepot overlays), [[student-loan-payments]] (upgraded FNMA section to official citation from B3-6-05)
- **Open questions added**: 0
- **Notes**: Credit section (pp. 469–527, B3-5.1 through B3-6-08) fully ingested from the FNMA Selling Guide (April 1, 2026 edition). Key FNMA rules confirmed as official: no minimum credit score for DU loans (DU performs holistic assessment); manual UW minimum 620 fixed / 640 ARM; maximum DTI 36%/45% manual, 50% DU; nontraditional credit requires 3 references manual (2 for DU), 4 for HomeReady; $0 IDR student loan payment allowed with documentation (FNMA only); collections on 1-unit primary need not be paid regardless of amount (DU); authorized user tradelines excluded in manual UW unless borrower documented as sole payer for 12+ months. All lender notes from loanDepot guide for these pages are now confirmed/corrected against official source. Ingested sections B3-5.1-01, B3-5.1-02, B3-5.2-01 through B3-5.2-03, B3-5.3-01 through B3-5.3-09, B3-5.4-01 through B3-5.4-03, B3-6-01 through B3-6-08.

---

## 2026-04-08 — Ingestion: loanDepot Conventional Guide — Military Income (pp. 195–196)

- **Source**: Guide_Conventional.pdf (trust level: lender)
- **Pages updated**: [[military-income]] (stub replaced with full content)
- **Notes**: Eligible types = flight/hazard pay, BAS, BAH, clothing allowance, proficiency pay. FNMA: verify via LES; DU validation ineligible. FHLMC: active-duty needs no employment history; reserve/NG needs 1 year; docs = YTD LES + W-2 (or written VOE + 10-day PCV); AIM ineligible.

---

## 2026-04-08 — Ingestion: loanDepot Conventional Guide — Alimony/Child Support Income (p. 156)

- **Source**: Guide_Conventional.pdf (trust level: lender)
- **Pages updated**: [[alimony-child-support-received]] (stub replaced with full content)
- **Notes**: 6-month receipt history + 3-year continuance both required; sporadic/partial payments disqualify; child support ages must support 3-year continuance; court order/decree required. Applies to FNMA B3-3.1-09 and FHLMC 5305.2.

---

## 2026-04-07 — Ingestion: loanDepot Conventional Guide — Borrower Eligibility (pp. 119–121)

- **Source**: Guide_Conventional.pdf (trust level: lender — loanDepot Conventional Lending Guide, March 2026)
- **Pages updated**: [[borrower-eligibility]] (stub replaced with full content)
- **Notes**: Covers general eligibility (natural persons, no max age), inter vivos / land trust exceptions, blind trust ineligibility, SSN/ITIN requirements, SSA validation process, SSA-89 form, FNMA SFC 162 requirement, ineligibility triggers for invalid SSNs, ownership interest requirements, life estate provisions, and FNMA homebuyer education triggers.

---

## 2026-04-07 — Ingestion: loanDepot Conventional Guide — Assets Section (pp. 275–312)

- **Source**: Guide_Conventional.pdf (trust level: lender — loanDepot Conventional Lending Guide, March 2026)
- **Pages created**: [[asset-verification-documentation]], [[business-assets]], [[credit-card-financing-reward-points]], [[cryptocurrency]], [[earnest-money-deposit]], [[funds-required-to-close]], [[gift-of-equity]], [[ineligible-assets]], [[interested-party-contributions]], [[large-deposits]], [[minimum-borrower-contribution]], [[stocks-bonds-mutual-funds]], [[reserves]], [[retirement-accounts]], [[sale-of-personal-assets]], [[trade-equity]]
- **Pages updated**: [[gift-funds]] (added FHLMC donor eligibility, second-home rule, transfer method requirements), [[source-loandepot-conventional-guide-2026-03]], [[hot]], [[index]], [[taxonomy]], [[change-log]]
- **Open questions added**: 0 (2 existing remain; removed stale large-deposit entry now resolved by ingestion)
- **Notes**: Assets section fully processed (38 pages, pp. 275–312). 16 new topic pages created. Notable rules: Large deposit threshold is 50% of monthly qualifying income (FNMA) or 50% of qualifying income plus asset-depletion income (FHLMC); purchase deposits need sourcing only if needed to qualify (FNMA); FHLMC requires sourcing if used to pay down debt regardless of amount; IPC limits by occupancy/LTV (3%/6%/9% primary+2nd home, 2% investment); gift of equity exempt from IPC limits if requirements met; 20% buffer rule means no liquidation evidence required for stocks/bonds/retirement if combined value ≥ 120% of closing need (FNMA and FHLMC); cryptocurrency ineligible in raw form — must convert to USD. Income (pp. 155–249), Liabilities (pp. 250–274), and Credit (pp. 313–325) sections previously ingested. loanDepot conventional guide now fully ingested.

---

## 2026-04-07 — Ingestion: loanDepot Conventional Guide — Liabilities Section (pp. 250–274)

- **Source**: Guide_Conventional.pdf (trust level: lender — loanDepot Conventional Lending Guide, March 2026)
- **Pages created**: [[liabilities-overview]], [[alimony-child-support-paid]], [[authorized-user-accounts]], [[business-debt-in-borrower-name]], [[contingent-liabilities-debts-paid-by-others]], [[departure-residence-pending-sale]], [[property-tax-qualification]], [[irs-installment-agreements]], [[loans-secured-by-financial-asset]], [[monthly-housing-expense]], [[open-30-day-accounts]], [[revolving-accounts]], [[secondary-subordinate-financing]], [[student-loan-payments]], [[timeshares]], [[total-monthly-debt-obligations]]
- **Pages updated**: [[source-loandepot-conventional-guide-2026-03]], [[hot]], [[index]], [[taxonomy]], [[change-log]]
- **Open questions added**: 0 (existing 2 remain open)
- **Notes**: Liabilities section (25 pages, pp. 250–274) fully processed. 15 topic pages created. Notable rules: FHLMC requires alimony to reduce qualifying income (FNMA permits but does not require); FHLMC uses 0.5% of outstanding balance for $0 student loans vs. FNMA allows true $0 on IDR plans; FHLMC HELOC default payment is 1.5% of outstanding balance when not documented; timeshare foreclosures exempt from standard derogatory seasoning (FHLMC); crypto-secured installment loans must always be in DTI. Assets section (pp. 275–312) remains to be ingested.

---

## 2026-04-07 — Ingestion: loanDepot Conventional Guide — Credit Section (pp. 313–325)

- **Source**: Guide_Conventional.pdf (trust level: lender — loanDepot Conventional Lending Guide, March 2026)
- **Pages created**: [[no-credit-score-borrowers]], [[credit-bureau-report-requirements]], [[credit-report-inquiries]], [[credit-score-selection]], [[derogatory-credit-event-seasoning]], [[disputed-tradelines]], [[frozen-credit-bureaus]], [[mortgage-history]], [[nontraditional-credit-history]], [[past-due-collections-chargeoffs]]
- **Pages updated**: [[source-loandepot-conventional-guide-2026-03]], [[hot]], [[index]], [[taxonomy]], [[change-log]]
- **Open questions added**: 0 (existing 2 remain open)
- **Notes**: Credit section (13 pages) processed. 10 topic pages created covering all credit subtopics listed in the source guide. All pages are trust level lender — loanDepot overlays; underlying GSE references noted but not independently verified. FHLMC guidance consistently defers to LPA Accept findings rather than publishing independent waiting period tables. Notable rules: FNMA 1-unit primary residence collections require no payoff regardless of amount; single 60-day late in prior 12 months bars FNMA eligibility under loanDepot guidelines. Assets and Liabilities sections remain to be ingested.

---

## 2026-04-07 — Ingestion: loanDepot Conventional Guide — Income Section (pp. 155–249)

- **Source**: Guide_Conventional.pdf (trust level: lender — loanDepot Conventional Lending Guide, March 2026)
- **Pages created**: [[source-loandepot-conventional-guide-2026-03]], [[self-employed-income]], [[rental-income]], [[bonus-overtime-commission-income]], [[temporary-leave-income]], [[social-security-retirement-income]], [[asset-depletion-income]], [[continuity-of-income]]
- **Pages updated**: [[hot]], [[index]], [[change-log]]
- **Open questions added**: 0 (existing 2 remain open)
- **Notes**: Income section (95 pages) processed. Covers FNMA and FHLMC requirements side by side. All pages are trust level lender — represent loanDepot overlays, not raw GSE guidelines. Assets, Liabilities, and Credit sections remain to be ingested. Additional income subtopics (alimony/child support, restricted stock, employment offers/contracts, boarder income) captured in continuity-of-income and referenced but not built as standalone pages yet.

---

## 2026-04-07 — Vault Initialization

- **Type**: Setup
- **Source**: N/A
- **Pages created**: [[index]], [[taxonomy]], [[hot]], [[open-questions]], [[gift-funds]], [[source-selling-guide-b3-4.3-04]], [[scenario-gift-large-deposit]], [[def-interested-party-contribution]], [[checklist-gift-funds-docs]], [[decision-gift-eligibility]]
- **Pages updated**: N/A
- **Open questions added**: 0
- **Notes**: Initial vault setup from design spec. Sample pages created with realistic Fannie Mae content. Awaiting first real ingestion from Selling Guide PDF.
