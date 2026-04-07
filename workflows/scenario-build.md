# Scenario Build Workflow

**Trigger**: Creating a new scenario page
**Purpose**: Document real-world underwriting situations with analysis, rules, and docs
**Output**: A new page in `wiki/scenarios/` with full cross-linking

---

## When to Create a Scenario

Create a scenario page when the situation is:
- An intersection of 2+ guideline areas (e.g., gift funds + large deposits)
- A recurring question requiring combined rules each time
- An edge case or gray area deserving documented analysis
- A notable real-world underwriting challenge worth capturing

Do NOT create a scenario page for:
- Simple single-rule situations (answer lives in the topic page)
- Hypothetical situations with no real-world grounding
- Situations already well-covered by an existing scenario

---

## Naming

Focus the filename on the issue, not the borrower:

✅ `scenario-declining-se-income.md`
✅ `scenario-gift-large-deposit.md`
✅ `scenario-conversion-primary-to-rental.md`
❌ `scenario-john-smith-loan.md`
❌ `scenario-complicated-case.md`

---

## Steps

### Step 1 — Define the Borrower Profile

Write 2–3 sentences describing the borrower situation in concrete terms:
- Income type and structure
- Property type and occupancy
- Relevant assets, credit, or debt details
- What makes this situation non-standard

### Step 2 — Identify the Underwriting Issue

State clearly what makes this scenario tricky:
- Which guideline areas overlap
- What the primary risk or ambiguity is
- Why a less experienced underwriter might make an error

### Step 3 — Map Governing Rules

For each applicable rule:
- Link to the topic page: `[[topic-page]]`
- State the specific rule that applies
- Cite the source: `(Source: [[source-page]])`

Draw only from wiki-sourced rules. If a relevant rule isn't in the wiki yet, flag it as needing ingestion.

### Step 4 — Document Required Documentation

List every specific document needed for this scenario — not a generic checklist, but the specific items for this borrower situation. Cross-link to any relevant checklist pages.

### Step 5 — Map the Analysis Approach

Step-by-step how to underwrite this situation:
1. What to look for first
2. How to apply the rules in sequence
3. Where judgment calls arise
4. How to document the rationale

### Step 6 — Flag Common Pitfalls

What mistakes does an underwriter commonly make in this type of scenario?
- Misapplying a rule
- Missing a required document
- Failing to check a cross-domain interaction
- Confusing a similar-but-different situation

### Step 7 — Note Compensating Factors

If the scenario involves borderline eligibility or risk factors:
- What strengthens the file
- What DU typically weighs in these situations
- What an underwriter can document to support approval

### Step 8 — Identify Open Issues

What aspects of this scenario require:
- Lender-specific policy (overlays)
- Further Selling Guide research
- User confirmation before proceeding

Add these to `open-questions.md`.

### Step 9 — Cross-Link

In the scenario page frontmatter:
- `sources:` — list all source pages cited
- `related:` — list all topic pages referenced

In each referenced topic page, add this scenario under `## Related Scenarios`.

Update `wiki/index.md` if relevant.

---

## Quality Check Before Saving

Before marking the page `status: active`:
- [ ] Every rule in `## Applicable Rules` has a source citation
- [ ] Every topic page referenced is linked via wikilink
- [ ] All referenced topic pages have this scenario added to their `## Related Scenarios`
- [ ] `open-questions.md` has entries for any unresolved issues
- [ ] `confidence` level reflects actual certainty (usually `interpreted`)

---

## Change Log Entry

After creating the scenario, append to `wiki/change-log.md`:

```markdown
## YYYY-MM-DD — Scenario Build
- **Pages created**: [[scenario-name]]
- **Topics linked**: [[list]]
- **Open questions added**: [count]
- **Notes**: [anything notable]
```
