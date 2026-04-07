# Query Workflow

**Trigger**: User asks an underwriting question
**Purpose**: Answer accurately using only wiki-sourced content; flag gaps
**Output**: Structured answer with source citations, wiki page links, and flagged gray areas

---

## Steps

### Step 1 — Parse the Question

Before reading any file, identify:
- **Domains involved**: Income? Assets? Credit? Property? (see taxonomy)
- **Borrower profile elements**: Loan type, occupancy, income type, credit situation
- **Question type**:
  - Hard rule (yes/no, specific threshold)
  - Judgment call (how to handle, what's reasonable)
  - Documentation requirement (what docs are needed)
  - Eligibility question (can this borrower qualify)

### Step 2 — Consult the Hot Cache First

Read `wiki/hot.md`. Check:
- Active Topics: Is this question related to pages already being worked on?
- Recent Questions: Has a similar question been answered recently?
- Pages Needing Review: Is a relevant page flagged as uncertain?

### Step 3 — Identify Relevant Pages

Read `wiki/index.md` and `wiki/taxonomy.md` to identify relevant topic pages by domain.

Do NOT scan entire folders. Use taxonomy and tags to target specific pages.

Prioritize:
1. `confidence: verified` topic pages — highest reliability
2. `confidence: interpreted` pages — usable with labeling
3. `confidence: needs-review` pages — use with explicit caution disclaimer

### Step 4 — Read Topic Pages

Read the relevant topic pages. Focus on:
- `## Key Rules` section — sourced facts
- `## Documentation Requirements` — for doc questions
- `## Exceptions & Nuances` — for edge cases
- `## Common Pitfalls` — for risk flagging

Note which source pages back the rules being used.

### Step 5 — Check Scenarios

Search `wiki/scenarios/` for pages that match the borrower situation. If found, read:
- `## Applicable Rules` — already synthesized rule set
- `## Analysis Approach` — step-by-step logic
- `## Compensating Factors` — if relevant

### Step 6 — Check Definitions

If the question involves terms that have `def-` pages, read them. Use aliased wikilinks in your answer: `[[def-interested-party-contribution|interested party contribution]]`.

### Step 7 — Assemble the Answer

Structure every answer in this order:

```
## Answer
[Direct answer — yes/no or clear conclusion]

## Rules (Sourced)
- Rule statement (Source: [[source-page]])
- Rule statement (Source: [[source-page]])

## Documentation Required
- [List specific docs]

## Nuances & Exceptions
- [Any conditions that change the answer]

## Interpretation
⚠️ The following reflects professional judgment, not direct Selling Guide language:
- [Interpretation notes]

## Gray Areas / Open Questions
- [Anything unresolved, flagged in open-questions.md]

## Related Pages
- [[topic-page]] — [why it's relevant]
- [[scenario-page]] — [if a matching scenario exists]
```

### Step 8 — Flag Gaps

If the wiki lacks coverage for this question:
- Say explicitly: "This topic hasn't been ingested yet."
- Name the likely source section that would cover it (e.g., "B3-3.1-09 covers rental income")
- Recommend dropping the source PDF in `raw/` for ingestion
- If the gap is significant, add an entry to `open-questions.md`

### Step 9 — Update Hot Cache

After answering:
- Add the question and key page links to `## Recent Questions` in `hot.md`
- Update `## Active Topics` if new pages were consulted
- Roll off oldest entries to keep hot.md under ~100 lines

---

## Constraints

- **Never invent a guideline.** Not in the wiki = not in the answer.
- **When combining rules**, show the reasoning explicitly and label the conclusion as an inference.
- **Confidence transparency**: If answering from a `needs-review` page, say so in the answer.
- **Cite wiki pages** in answers — not just source docs — so users can drill into Obsidian.
- **Do not paraphrase source pages from memory.** Read the actual page before citing it.
