---
title: "Decision: Gift Fund Eligibility by Property and Loan Type"
type: decision-tree
tags: [assets, gift-funds, occupancy, eligibility]
sources: [source-selling-guide-b3-4.3-04]
related: [gift-funds, checklist-gift-funds-docs, scenario-gift-large-deposit, def-interested-party-contribution]
confidence: interpreted
status: active
last_updated: 2026-04-07
---

## Question

Can this borrower use gift funds toward their down payment, and are there any minimum borrower contribution requirements?

---

## Decision Logic

**1. Is the property an investment property?**
- **Yes** → Gift funds are **NOT permitted**. Stop. Funds must be sourced entirely from the borrower's own assets.
- **No** → Continue to Step 2.

---

**2. Is the donor an eligible party?**
- Check: Is the donor a relative (spouse, child, parent, sibling, grandparent), domestic partner, fiancé/fiancée, or other eligible Fannie Mae-defined donor?
- **No** → Gift funds are **NOT permitted** from this donor. Reclassify if the donor has a financial interest in the transaction (see [[def-interested-party-contribution|IPC rules]]). Stop.
- **Yes** → Continue to Step 3.

---

**3. Does the gift letter include all required elements?**
- Dollar amount, transfer date, donor info, relationship, no-repayment statement
- **No** → Gift is not yet documented. Obtain complete gift letter before proceeding.
- **Yes** → Continue to Step 4.

---

**4. What is the occupancy type?**

**A. Principal Residence:**
- Continue to Step 5 for LTV analysis.

**B. Second Home:**
- Gift funds are permitted.
- **LTV ≤ 80%**: Check DU findings — DU may impose a minimum borrower contribution. If DU does not require reserves and no minimum contribution is flagged, gift funds may cover the full down payment. Follow DU findings.
- **LTV > 80%**: Gift funds may cover the full down payment. Follow DU findings.
- Document per [[checklist-gift-funds-docs]].

---

**5. Principal Residence — What is the LTV?**

**A. LTV > 80% (less than 20% down):**
- Gift funds may cover the **entire** down payment. No minimum borrower contribution required.
- Document per [[checklist-gift-funds-docs]].

**B. LTV ≤ 80% (20% or more down):**
- Check DU findings for minimum borrower contribution requirements.
- If DU requires minimum borrower contribution: at least the specified percentage must come from borrower's own funds.
- If DU does not require minimum contribution: gift funds may cover the entire down payment.
- **Note**: DU is the governing source for contribution requirements at LTV ≤ 80%. Do not assume gift funds are unrestricted — always check findings.

---

## Key Rules Applied

- Gift funds prohibited for investment properties. (Source: [[source-selling-guide-b3-4.3-04]])
- Eligible donors defined as relatives, domestic partners, and fiancés/fiancées. (Source: [[source-selling-guide-b3-4.3-04]])
- No minimum borrower contribution for primary residence at LTV > 80%. (Source: [[source-selling-guide-b3-4.3-04]])
- At LTV ≤ 80%, DU findings govern minimum contribution requirements. (Source: [[source-selling-guide-b3-4.3-04]])
- Donors may not be interested parties (builder, agent, seller, etc.). (Source: [[source-selling-guide-b3-4.3-04]])

---

## Edge Cases

- **Gift from employer**: Employer gifts may be IPCs if the employer has any financial interest in the transaction. Run through IPC analysis — see [[def-interested-party-contribution]].
- **Gift of equity**: If the "gift" is equity from a family member seller, this is a gift of equity — not a cash gift. Governed by different rules. See [[gift-of-equity]].
- **Gift used for reserves only**: Gift funds from family members may be used for reserves. Gift funds from non-family donors are not acceptable as reserves.
- **Gift with large deposit**: If the gift appears as a large deposit on bank statements, large deposit sourcing requirements are triggered in addition to gift documentation. See [[scenario-gift-large-deposit]].
- **Down payment assistance programs**: DPA grants from government entities or non-profits are not gifts. Analyze under [[grants-dpa]].
