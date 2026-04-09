---
title: Credit Score Selection (Representative Credit Score)
type: topic
tags: [credit, credit-score, eligibility, fico]
sources: [source-fnma-selling-guide-2026-04, source-loandepot-conventional-guide-2026-03]
related: [credit-score-requirements, credit-bureau-report-requirements, frozen-credit-bureaus, no-credit-score-borrowers]
confidence: verified
status: active
last_updated: 2026-04-08
---

## Overview

The representative credit score is determined by selecting a single score for each borrower, then taking the lowest score across all borrowers. It is used for loan eligibility (manually underwritten loans) and for pricing (LLPAs on all loans). A separate "average median credit score" calculation applies only to manually underwritten multi-borrower loans for determining eligibility. (Source: [[source-fnma-selling-guide-2026-04]], B3-5.1-02)

---

## Key Rules

### Step 1 — Select Individual Score Per Borrower

Fannie Mae recommends obtaining at least **two credit scores per borrower**:

| Scores Available | Score to Select |
|---|---|
| Three scores | **Middle score** |
| Two of three identical | Middle of the three (e.g., 700/680/680 → 680; 700/700/680 → 700) |
| Two scores | **Lower score** |
| One score | That score is used |

(Source: [[source-fnma-selling-guide-2026-04]], B3-5.1-02)

### Step 2 — Determine Representative Credit Score for the Loan

| Borrowers on Loan | Representative Credit Score |
|---|---|
| One borrower | The single borrower's selected score |
| Multiple borrowers | **Lowest** applicable score from across all borrowers |
| Borrower without a credit score | Based on the credit scores of the other borrowers |

(Source: [[source-fnma-selling-guide-2026-04]], B3-5.1-02)

### Average Median Credit Score — Manual Underwriting Only

For certain manually underwritten transactions with multiple borrowers, the **average median credit score** is used **in place of** the representative credit score to determine if the minimum credit score requirement is met:

- Step 1: Determine each borrower's median score
- Step 2: Average all borrowers' median scores → this is the average median credit score

**Example**:
- Borrower 1 scores: 590 / 605 / 648 → median = 605
- Borrower 2 scores: 661 / 693 / 693 → median = 693
- Average median = (605 + 693) / 2 = **649**
- Representative credit score = **605** (lowest median, still used for LLPAs)

The average median is used for eligibility; the representative (lowest median) is always used for pricing. (Source: [[source-fnma-selling-guide-2026-04]], B3-5.1-02)

### When Data Is Missing from Repositories

- **One or two repositories have no data**: Report is acceptable if credit data is available from at least one repository AND a three in-file merged report was requested
- **One repository is frozen**: Report is acceptable if credit data is available from two repositories AND a three in-file merged report was requested
- **Two or more repositories frozen**: Loan is **not eligible** for delivery to Fannie Mae, whether manually or DU underwritten

(Source: [[source-fnma-selling-guide-2026-04]], B3-5.1-01)

### Foreign Credit Reports and Scores

Fannie Mae permits the use of a foreign country credit report to document credit history (except for DU loan casefiles). However, foreign credit scores **cannot** be used to establish eligibility or delivered to Fannie Mae unless the score is a classic FICO score meeting B3-5.1-01 requirements.

Foreign credit reports must meet the standards for domestic reports and must be in English or include an English translation. Borrowers relying on foreign credit reports for credit history must be manually underwritten. (Source: [[source-fnma-selling-guide-2026-04]], B3-5.1-02)

---

## Exceptions & Nuances

### DU Risk Assessment vs. Representative Credit Score

DU does not use the representative credit score as an eligibility threshold — DU performs its own holistic analysis. The representative credit score is delivered at Loan Delivery and is used for LLPA pricing. (Source: [[source-fnma-selling-guide-2026-04]], B3-5.1-01)

### FHLMC — Credit Score Selection

(Lender note: FHLMC uses the same middle/lower score selection logic. Single borrower: the single applicable score. Multiple borrowers: lowest applicable score from the group. Non-credit-score borrower: based on other borrowers' scores.) (Source: [[source-loandepot-conventional-guide-2026-03]], p.316–317)

---

## Interpretation Notes

⚠️ The two-step process (per-borrower then across borrowers) can trip up underwriters. Each borrower's individual score must be determined first (using middle/lower rules), and THEN the lowest of all borrowers' individual scores is selected as the loan's representative credit score.

⚠️ The average median credit score is only relevant to manually underwritten loans for eligibility determination. It does not apply to DU loans, and it does not affect LLPA pricing.

⚠️ Foreign credit scores on foreign report formats cannot be used even if the score number happens to match the FICO scale. Only actual classic FICO scores from qualifying bureaus are acceptable.
