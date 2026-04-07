# Lint Workflow

**Trigger**: After major ingestions, on request, or monthly
**Purpose**: Quality control — catch structural problems, stale content, and broken links
**Output**: Lint report appended to `wiki/change-log.md`

---

## Checks

Run each check in order. Log all findings. Do not auto-fix without user confirmation on anything that could change content.

### Check 1 — Orphan Pages
**What**: Pages with no inbound wikilinks from other pages
**How**: For each page in wiki/, search all other pages for `[[filename]]` references
**Flag**: Pages with zero inbound links

### Check 2 — Missing Backlinks
**What**: Page A links to Page B, but Page B doesn't reference Page A in `related:` or body
**How**: For each wikilink found, verify the target page has a reciprocal link
**Flag**: One-way links that should be bidirectional

### Check 3 — Unsourced Claims
**What**: Topic pages with `confidence: needs-review` that are older than 30 days
**How**: Check frontmatter `confidence` and `last_updated` fields
**Flag**: List page name and date it was created/last updated

### Check 4 — Stale Pages
**What**: Pages with `status: active` but `last_updated` older than 6 months
**How**: Compare `last_updated` to current date
**Flag**: Pages that may need review for guideline changes

### Check 5 — Duplicate Coverage
**What**: Multiple topic pages covering the same underwriting concept
**How**: Scan titles and tags for near-identical coverage; look for redundant content in Key Rules sections
**Flag**: Pairs of pages that may need merging

### Check 6 — Orphan Scenarios
**What**: Scenario pages not linked from any topic page
**How**: For each `wiki/scenarios/` page, check if any topic page links to it in `## Related Scenarios`
**Flag**: Unlinked scenario pages

### Check 7 — Unsupported Scenarios
**What**: Scenario pages making rule claims not backed by a linked source page
**How**: For each rule in `## Applicable Rules`, verify the cited source page exists
**Flag**: Missing source citations or broken source wikilinks

### Check 8 — Dangling Open Questions
**What**: Entries in `open-questions.md` with `status: open` older than 30 days
**How**: Check date raised and status fields
**Flag**: List with dates — these need resolution or escalation

### Check 9 — Missing Definitions
**What**: Technical terms used frequently across pages without a `def-` page
**How**: Scan for repeated terms across topic pages; check if a def- page exists
**Flag**: Top candidates for definition pages

### Check 10 — Inconsistent Naming
**What**: Files not following naming conventions
**How**: Verify prefixes (scenario-, source-, def-, checklist-, decision-) and kebab-case
**Flag**: Non-conforming filenames

### Check 11 — Empty Sections
**What**: Template sections that were never filled in (still contain HTML comments or placeholder text)
**How**: Scan pages for `<!--` comments or lines matching template placeholder patterns
**Flag**: Page name and empty section name

### Check 12 — Taxonomy Gaps
**What**: Topic pages not referenced in `wiki/taxonomy.md`
**How**: For each file in `wiki/topics/`, verify it appears in taxonomy.md
**Flag**: Missing entries with suggested placement in the taxonomy

---

## Output Format

Append to `wiki/change-log.md`:

```markdown
## YYYY-MM-DD — Lint

### Results Summary
- Orphan pages: [count]
- Missing backlinks: [count]
- Unsourced claims (>30 days): [count]
- Stale pages (>6 months): [count]
- Duplicate coverage: [count]
- Orphan scenarios: [count]
- Unsupported scenarios: [count]
- Dangling open questions: [count]
- Missing definitions: [count]
- Naming inconsistencies: [count]
- Empty sections: [count]
- Taxonomy gaps: [count]

### Issues Requiring Action
[List each flagged item with page name and recommended action]

### No Action Needed
[List checks that passed cleanly]
```

---

## Remediation Rules

After running lint, remediation requires user confirmation for:
- Merging pages (duplicate coverage)
- Setting pages to `status: stale`
- Creating new definition pages from the missing definitions list

Claude Code can fix independently without confirmation:
- Adding missing backlinks (wikilinks in `related:` frontmatter)
- Fixing naming conventions (rename files to match convention)
- Filling in empty template sections with "Not yet documented" placeholders
- Updating taxonomy.md to include missing topic pages

---

## Frequency

- After every major ingestion (5+ pages created)
- On explicit user request
- Monthly recommended for active vaults
