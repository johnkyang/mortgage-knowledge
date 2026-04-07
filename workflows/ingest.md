# Ingestion Workflow

**Trigger**: New source material dropped into `raw/`
**Purpose**: Extract knowledge from raw sources and populate the wiki accurately
**Output**: Source pages, topic pages, definition pages, updated indexes, change log entry

---

## Prerequisites

Before starting:
- Confirm the file exists in `raw/`
- Identify the source type: Selling Guide section, Lender Letter, FAQ, lender overlay, personal notes
- Assign a trust level: `official` | `faq` | `du-official` | `lender` | `personal`

---

## Steps

### Step 1 — Classify

Read the raw file. Determine:
- **Trust level** (see CLAUDE.md hierarchy)
- **Selling Guide section(s)** covered (e.g., B3-4.3-04, B3-3.1-09)
- **Underwriting domains** touched (Income, Assets, Credit, etc.)
- **Scope**: Is this one section or multiple? If multiple, plan to create one source page per section.

For large PDFs: process section by section. Confirm with user between major sections before continuing.

### Step 2 — Create Source Page

For each distinct section or document, create one page in `wiki/sources/`.

Naming: `source-selling-guide-b3-4.3-04.md` (use the guide section ID as the slug)

Populate:
- Reference block (document name, section, effective date, URL if available)
- Summary of what the section covers
- Key verbatim or near-verbatim excerpts (use blockquotes)
- Topics Covered (links to topic pages — fill in after Step 3)

### Step 3 — Extract Concepts

Read through the source and identify:
- Distinct rules and requirements (each gets a bullet in the relevant topic page)
- Numerical thresholds (LTV limits, waiting periods, percentage requirements)
- Term definitions (new `def-` pages)
- Exceptions and nuances to existing rules
- Examples or borrower situations (potential scenario pages)

Map each concept to:
- An existing topic page (update it) or
- A new topic page needed (create it)

### Step 4 — Create or Update Topic Pages

**Creating new pages:**
- Use the topic page template from CLAUDE.md
- Set `confidence: needs-review` initially; upgrade to `verified` after source review is complete
- Set `status: draft` until content is complete
- Every rule bullet ends with `(Source: [[source-page]])`

**Updating existing pages:**
- Never overwrite or delete existing sourced content
- Append new rules with their own source citations
- If the new source conflicts with existing content: add both, note the conflict explicitly, flag in open-questions.md
- Update `last_updated` date

**Key Rules section discipline:**
- Only direct source language here (or close paraphrase with citation)
- No synthesis, inference, or practitioner knowledge in this section
- Interpretation goes in `## Interpretation Notes` with ⚠️ warning

### Step 5 — Create Definition Pages

For any term that:
- Is defined by the source
- Appears frequently across multiple pages
- Would benefit from a single linkable definition

Create a page in `wiki/definitions/` with the `def-` prefix.

### Step 6 — Identify Scenarios

If the source describes:
- Specific borrower situations or examples
- Edge cases or exceptions
- Common problem patterns

Flag these as potential scenario pages. Create them if the situation is:
- Complex enough to warrant step-by-step analysis
- A common real-world underwriting challenge
- An intersection of 2+ guideline areas

Use `workflows/scenario-build.md` for scenario creation.

### Step 7 — Cross-Reference

After all pages are created/updated:
- Add `sources: [source-page]` to topic page frontmatter
- Add `related: [page-names]` to link related topic, scenario, and definition pages
- Add wikilinks within body text where natural (not every mention — just meaningful cross-references)
- In the source page, fill in `## Topics Covered` with links to all derived topic pages
- Update `taxonomy.md` if new topic areas were added

### Step 8 — Update Indexes

- **`wiki/index.md`**: Add new pages to the Browse by Domain section and Recent Additions
- **`wiki/hot.md`**: Add source to Recently Ingested (roll off oldest), add active topics to Active Topics list

### Step 9 — Log Open Questions

For any:
- Ambiguous guideline language
- Rules that seem to conflict across sections
- Topics requiring lender-specific interpretation
- Gaps in the source material

Add an entry to `open-questions.md` using the standard format.

### Step 10 — Write Change Log

Append an entry to `wiki/change-log.md`:

```markdown
## YYYY-MM-DD — Ingestion
- **Source**: [filename] (trust level: [level])
- **Pages created**: [[list]]
- **Pages updated**: [[list]]
- **Open questions added**: [count]
- **Notes**: [anything notable — conflicts found, sections skipped, etc.]
```

---

## Constraints

- **Accuracy over completeness.** If you can't confidently extract a rule, flag it rather than guessing.
- **Large PDFs:** Process one major section at a time. Pause for user confirmation before moving to the next section.
- **Ambiguous pages:** Set `confidence: needs-review` and add to `open-questions.md`.
- **Paid API calls:** If the ingestion tool involves API costs, confirm scope with user before running.
- **Never delete raw files** after ingestion. They stay in `raw/` as reference.
