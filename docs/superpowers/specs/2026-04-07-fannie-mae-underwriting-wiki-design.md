# Fannie Mae Underwriting Knowledge System — Design Spec

**Date**: 2026-04-07
**Status**: Approved
**Purpose**: Build a markdown-based, Obsidian-friendly, Claude Code-queryable underwriting knowledge system for Fannie Mae guidelines using the Karpathy-style LLM wiki approach.

---

## 1. Architecture Overview

**Approach**: Domain-organized wiki with flat pages inside functional folders. Hybrid WAT integration — the wiki is the product, `workflows/` holds operational SOPs.

**Dual-use design**:
- Human browsing via Obsidian (wikilinks, graph view, tag filtering)
- Machine querying via Claude Code (structured frontmatter, hot cache, taxonomy index)

**Key constraints**:
- Never invent guidelines
- Always cite sources with trust-level labels
- Flag conflicts instead of resolving silently
- Prefer accuracy over completeness
- Separate sourced facts from interpretation

---

## 2. Folder Structure

```
Mortgage Knowledge/
├── CLAUDE.md                    # Operating instructions for Claude Code
├── raw/                         # Drop zone for source PDFs, notes, screenshots
├── wiki/
│   ├── index.md                 # Master entry point with taxonomy + navigation
│   ├── hot.md                   # Active memory / hot cache (~100 lines max)
│   ├── change-log.md            # Running log of all ingestion + edits
│   ├── open-questions.md        # Unresolved gray areas needing confirmation
│   ├── taxonomy.md              # Full domain → subtopic map
│   ├── topics/                  # Core guideline pages (primary growth area)
│   ├── scenarios/               # Real-world underwriting situation pages
│   ├── sources/                 # Source attribution pages
│   ├── definitions/             # Term definitions (brief, linkable)
│   ├── checklists/              # Documentation requirement checklists
│   └── decision-trees/          # Decision logic for ambiguous situations
├── workflows/                   # Operational SOPs (WAT-style)
│   ├── ingest.md                # How to process new raw materials
│   ├── query.md                 # How to answer underwriting questions
│   ├── lint.md                  # Health check / quality control
│   └── scenario-build.md        # How to create scenario pages
└── .tmp/                        # Disposable processing artifacts
```

### Folder Details

| Folder | Purpose | Expected Growth |
|--------|---------|-----------------|
| `raw/` | Drop zone. Unprocessed source material. Files stay after ingestion as reference. | Grows as sources are added |
| `wiki/topics/` | One page per underwriting concept. The core of the system. | **Primary** — 100-300+ pages |
| `wiki/scenarios/` | One page per real-world borrower situation. Links to topics and sources. | Steady growth with experience |
| `wiki/sources/` | Attribution pages. One per Selling Guide section, FAQ, or bulletin. | Grows with each ingestion |
| `wiki/definitions/` | Short, linkable definitions. Keeps topic pages cleaner. | ~50-100 pages, slow growth |
| `wiki/checklists/` | Documentation requirement lists by loan/income type. | ~20-40 pages |
| `wiki/decision-trees/` | Step-by-step logic for ambiguous decisions. | ~10-30 pages |
| `workflows/` | SOPs for Claude Code operations. Rarely changes. | 4-6 files, stable |
| `.tmp/` | Intermediate processing files. Disposable. | Ephemeral |

### Design Decisions
- No `comparisons/` subfolder — comparison content lives in topic pages or decision-tree pages
- No nested domains within `topics/` — domain hierarchy lives in `taxonomy.md` and frontmatter tags
- `hot.md` at wiki root for fast access

---

## 3. File Naming Conventions

- All lowercase, kebab-case
- Topics: descriptive name → `self-employed-income.md`, `gift-funds.md`
- Scenarios: `scenario-` prefix → `scenario-declining-se-income.md`
- Sources: `source-` prefix → `source-selling-guide-b3-3.1-09.md`
- Definitions: `def-` prefix → `def-stable-monthly-income.md`
- Checklists: `checklist-` prefix → `checklist-self-employed-docs.md`
- Decision trees: `decision-` prefix → `decision-rental-income-method.md`

---

## 4. Frontmatter Standard

Every page requires this YAML frontmatter (with exceptions noted below):

```yaml
---
title: Page Title
type: topic | scenario | source | definition | checklist | decision-tree
tags: [domain, subtopic]
sources: [source-page-names]
related: [related-page-names]
confidence: verified | interpreted | needs-review
status: active | draft | stale
last_updated: YYYY-MM-DD
---
```

### Field Definitions

| Field | Purpose |
|-------|---------|
| `title` | Human-readable page title |
| `type` | Page type — drives how Claude processes and retrieves it |
| `tags` | Domain/subtopic tags for Obsidian filtering and Claude retrieval |
| `sources` | Links to source pages (official material backing this page) |
| `related` | Links to other wiki pages (cross-references) |
| `confidence` | How well-sourced the content is |
| `status` | Page lifecycle state |
| `last_updated` | Date of last meaningful edit |

### Confidence Levels
- `verified` — Directly from official Selling Guide or FAQ
- `interpreted` — Requires professional judgment or combines multiple rules
- `needs-review` — Uncertain, incomplete, or newly created

### Exceptions by Page Type
- **Source pages**: Use `trust_level` instead of `confidence`. Do not include `sources` field (a source page IS a source).
```yaml
trust_level: official | faq | du-official | lender | personal
```
- **Definition pages**: Include `confidence` and `status` fields.
- **Checklist and decision-tree pages**: Include `confidence` and `status` fields.

### Tagging Convention
Tags use lowercase kebab-case matching taxonomy domains and subtopics: `[income, self-employment, schedule-c]`. Use 3-5 tags per page.

### Cross-Domain Topics
When a topic spans multiple taxonomy domains (e.g., "Departure Residence" appears under both Income and Occupancy), create one topic page tagged with all relevant domains. The taxonomy lists it under each domain; the page itself is the single source of truth.

### Page Length Guideline
If a topic page exceeds ~200 lines, consider splitting into sub-topic pages matching the taxonomy subtopic entries (e.g., `self-employed-income.md` → separate pages for `schedule-c-income.md`, `k1-income.md`, etc.).

---

## 5. Linking Conventions

- Obsidian wikilinks: `[[page-name]]`
- Aliased links for definitions: `[[def-stable-monthly-income|stable monthly income]]`
- Source citations at end of rule statements: `(Source: [[source-page]])`

---

## 6. Page Templates

### 6.1 Topic Page

```markdown
---
title:
type: topic
tags: []
sources: []
related: []
confidence: needs-review
status: draft
last_updated:
---

## Summary
<!-- 2-3 sentence plain-language overview of this guideline area -->

## Key Rules
<!-- Bulleted rules directly from source material. Each rule ends with source citation. -->
- Rule statement (Source: [[source-page]])

## Documentation Requirements
<!-- What paperwork is needed -->

## Exceptions & Nuances
<!-- Conditions where the standard rule doesn't apply -->

## Common Pitfalls
<!-- Mistakes underwriters make in this area -->

## Related Scenarios
<!-- Links to scenario pages that apply this topic -->

## Related Topics
<!-- Links to other topic pages -->

## Interpretation Notes
> ⚠️ **Interpretation**: Content below is not directly sourced. It reflects practical application or professional judgment.

## Sources
<!-- Full list of source pages backing this content -->
```

### 6.2 Scenario Page

```markdown
---
title: "Scenario: "
type: scenario
tags: []
sources: []
related: []
confidence: needs-review
status: draft
last_updated:
---

## Borrower Profile
<!-- Brief description of the borrower situation -->

## Underwriting Issue
<!-- What makes this scenario tricky or notable -->

## Applicable Rules
<!-- Key rules that govern this situation, with source links -->
- [[topic-page]] — rule summary (Source: [[source-page]])

## Documentation Needed
<!-- Specific docs required for this scenario -->

## Analysis Approach
<!-- Step-by-step how to underwrite this -->

## Common Pitfalls
<!-- What goes wrong in this type of scenario -->

## Compensating Factors
<!-- If applicable — what strengthens the file -->

## Likely Conditions
<!-- Conditions an underwriter would typically issue -->

## Open Issues
<!-- Anything unresolved or requiring lender-specific guidance -->
```

### 6.3 Source Page

```markdown
---
title: "Source: "
type: source
tags: []
related: []
trust_level: official
status: active
last_updated:
---

## Reference
- **Document**:
- **Section**:
- **Effective Date**:
- **URL**: <!-- if available -->

## Summary
<!-- What this source section covers -->

## Topics Covered
<!-- Links to topic pages derived from this source -->

## Key Excerpts
<!-- Important verbatim or near-verbatim passages -->
> Quoted guideline text here

## Notes
<!-- Anything notable about this source -->
```

### 6.4 Definition Page

```markdown
---
title: "Def: "
type: definition
tags: []
sources: []
related: []
confidence: verified
status: active
last_updated:
---

## Definition
<!-- Clear, concise definition -->

## Context
<!-- Where this term appears and why it matters -->

## Source
<!-- Official source for this definition -->
```

### 6.5 Checklist Page

```markdown
---
title: "Checklist: "
type: checklist
tags: []
sources: []
related: []
confidence: verified
status: active
last_updated:
---

## When to Use
<!-- What loan type / income type / situation this checklist applies to -->

## Required Documentation
- [ ] Item
- [ ] Item

## Conditional Documentation
- [ ] If [condition], then [document needed]

## Sources
```

### 6.6 Decision Tree Page

```markdown
---
title: "Decision: "
type: decision-tree
tags: []
sources: []
related: []
confidence: interpreted
status: active
last_updated:
---

## Question
<!-- The underwriting question this tree answers -->

## Decision Logic
1. **Is [condition]?**
   - Yes → [outcome or next question]
   - No → [outcome or next question]

## Key Rules Applied
<!-- Source-linked rules driving this logic -->

## Edge Cases
<!-- Situations where this tree may not apply cleanly -->
```

### 6.7 Open Questions (single running file)

Each entry follows this format:
```markdown
### [Topic or question title]
- **Date raised**: YYYY-MM-DD
- **Context**: Why this came up
- **Related pages**: [[links]]
- **Status**: open | researching | resolved
- **Resolution**: (filled in when resolved)
```

### 6.8 Change Log Entry Format

Each entry appended to `wiki/change-log.md`:
```markdown
## YYYY-MM-DD — [Ingestion | Edit | Lint | Scenario Build]
- **Source**: (if ingestion — raw file name and trust level)
- **Pages created**: [[list]]
- **Pages updated**: [[list]]
- **Open questions added**: (count)
- **Notes**: (anything notable)
```

### 6.9 Index Page Structure (`wiki/index.md`)

```markdown
# Fannie Mae Underwriting Wiki

## Quick Links
- [[hot]] — Active memory / recent activity
- [[taxonomy]] — Full topic map
- [[open-questions]] — Unresolved gray areas
- [[change-log]] — Change history

## Browse by Domain
<!-- Links to the top-level taxonomy domains, each linking to key topic pages -->
- **Income**: [[self-employed-income]], [[rental-income]], ...
- **Assets**: [[gift-funds]], [[large-deposits]], ...
- (etc.)

## Recent Additions
<!-- Last 5-10 pages added — updated during ingestion -->
```

---

## 7. Source of Truth Hierarchy

| Level | Label | What it means | Example |
|-------|-------|---------------|---------|
| 1 | `official` | Direct Fannie Mae Selling Guide language | B3-3.1-09 rental income rules |
| 2 | `faq` | Official Fannie Mae FAQ or Lender Letter | LL-2024-07 |
| 3 | `du-official` | DU-specific official material | DU messaging on asset depletion |
| 4 | `lender` | Lender training notes, bulletins, overlays | Company guideline summary |
| 5 | `personal` | Interpretation, experience, notes | "In practice, most UWs require..." |

### Rules
- Level 1-3: State as fact with source citation
- Level 4: Label as `(Lender note: ...)`
- Level 5: Must go in Interpretation Notes section with ⚠️ warning
- Conflicts between sources: Flag in `open-questions.md`, never silently pick one
- Never synthesize a rule that doesn't exist. If combining rules, show reasoning and label as interpretation

---

## 8. Master Taxonomy

Top-level domains and subtopics for `wiki/taxonomy.md`:

```
Borrower
├── Borrower Eligibility
├── Citizenship / Residency Status
├── First-Time Homebuyer
├── Non-Occupant Co-Borrower
├── Inter Vivos Trust
├── Power of Attorney
├── Age of Documents

Income
├── Base / Salary / Hourly
├── Bonus Income
├── Overtime Income
├── Commission Income
├── Self-Employment
│   ├── Schedule C
│   ├── K-1 / Partnership (1065)
│   ├── S-Corp (1120S)
│   ├── C-Corp (1120)
│   ├── Cash Flow Analysis
├── Rental Income
│   ├── Schedule E
│   ├── Departure Residence
│   ├── Conversion of Primary to Rental
│   ├── Subject Property Rental
├── Boarder Income
├── Retirement / Pension / Social Security
├── Trust Income
├── Asset Depletion / Asset Dissipation
├── Temporary Leave Income
├── Variable Income
├── RSU / Stock Options
├── Notes Receivable
├── Alimony / Child Support (received)
├── Foreign Income
├── Military Income (BAH, BAS)
├── Trailing Co-Borrower Income
├── Employment Gaps
├── Verbal VOE Requirements

Assets
├── Checking / Savings
├── Gift Funds
├── Gift of Equity
├── Grants / DPA
├── Retirement Accounts (401k, IRA)
├── Stocks / Bonds / Mutual Funds
├── Business Funds
├── Sale of Assets
├── Large Deposits
├── Earnest Money Deposit
├── Cash to Close
├── Proceeds from Sale of Home
├── Borrowed Funds (secured/unsecured)
├── Cash Value Life Insurance
├── Trade Equity

Credit
├── Credit Score Requirements
├── Minimum Tradelines
├── Non-Traditional Credit
├── Authorized User Accounts
├── Disputed Accounts
├── Collections / Charge-Offs
├── Judgments / Liens
├── Significant Derogatory Events
│   ├── Bankruptcy (Ch 7, Ch 13)
│   ├── Foreclosure
│   ├── Short Sale / Deed-in-Lieu
│   ├── Pre-Foreclosure
├── Housing Payment History
├── Mortgage Delinquency

Liabilities
├── Revolving Debt
├── Installment Debt (10-month rule)
├── Student Loans (IBR, deferred)
├── Alimony / Child Support (paid)
├── Business Debt in Borrower Name
├── Contingent Liabilities
├── HELOC
├── DTI Limits / Thresholds

Property
├── Property Types (SFR, Condo, PUD, Co-op, MH)
├── 2-4 Unit Properties
├── Manufactured Housing
├── Condo Eligibility
│   ├── Full Review
│   ├── Limited Review
│   ├── PERS
│   ├── Condo Project Standards
├── Co-op Requirements
├── Mixed-Use Properties
├── Non-Warrantable Condo
├── Ineligible Properties
├── Leasehold
├── Rural Properties
├── Unique / Non-Traditional Properties

Occupancy
├── Primary Residence
├── Second Home
├── Investment Property
├── Departure Residence
├── Conversion of Primary to Rental
├── Multiple Financed Properties

Collateral / Appraisal
├── Appraisal Requirements
├── Desktop Appraisal
├── Appraisal Waivers
├── Comparable Selection
├── Condition / Quality Ratings
├── Repairs / Completion Requirements
├── Value Reconciliation
├── Reconsideration of Value
├── Property Inspection Alternatives

Eligibility / Product
├── Loan Limits (conforming, high-balance)
├── LTV / CLTV / HCLTV
├── ARM Qualifying Rate
├── Temporary Buydowns
├── HomeReady
├── HomeStyle Renovation
├── High-Balance
├── Texas Section 50(a)(6)
├── Construction-to-Permanent

Reserves
├── Reserve Requirements by Property Type
├── Multiple Financed Properties Reserves
├── Acceptable Reserve Sources
├── Gift Funds for Reserves
├── Retirement Funds as Reserves

DU / Desktop Underwriter
├── DU Findings Interpretation
├── DU Approve/Eligible
├── DU Refer
├── DU Overrides
├── Manual Underwrite Requirements

Documentation
├── Age of Documents
├── Verbal VOE Timing
├── Tax Return Requirements
├── Pay Stub Requirements
├── Bank Statement Requirements

Compliance / Regulatory
├── Interested Party Contributions
├── TRID Considerations
├── QM / ATR
├── Anti-Steering

Special Scenarios
├── Non-Arm's Length Transactions
├── Identity of Interest
├── Relocation Benefits
├── Properties with Solar Panels
├── PACE Loans
├── Accessory Dwelling Units
```

Each leaf in the taxonomy links to its topic page via wikilink. Pages are created as needed, not all up front.

---

## 9. Workflows

### 9.1 Ingestion Workflow (`workflows/ingest.md`)

Triggered when new source material is dropped into `raw/`.

**Steps:**
1. **Classify** — Read the raw file. Determine trust level (official/faq/lender/personal). Identify underwriting domains covered.
2. **Create source page** — One page in `wiki/sources/` per distinct guide section or document. Record reference info and key excerpts.
3. **Extract concepts** — Identify distinct rules, requirements, thresholds. Map each to existing topic page or flag new page needed.
4. **Create/update topic pages** — Add rules with source citations. Never overwrite existing sourced content. If conflict, add both and flag.
5. **Create definition pages** — For any terms introduced or defined by the source.
6. **Identify scenarios** — If examples or borrower situations are described, create scenario pages.
7. **Cross-reference** — Add `related` links in frontmatter. Add wikilinks in body. Update `taxonomy.md` for new topics.
8. **Update indexes** — Add new pages to `index.md`. Update `hot.md`.
9. **Log open questions** — Ambiguities, conflicts, gaps → `open-questions.md`.
10. **Write change log** — Append entry to `change-log.md`.

**Constraints:**
- For large PDFs, process section by section. Pause between sections for user confirmation.
- Prioritize accuracy over completeness.
- Ambiguous pages get `confidence: needs-review`.

### 9.2 Query Workflow (`workflows/query.md`)

Triggered when the user asks an underwriting question.

**Steps:**
1. **Parse** — Identify domains, borrower profile elements, whether it's a hard rule vs. judgment call.
2. **Consult index** — Read `hot.md` first, then `index.md` and `taxonomy.md` for relevant pages.
3. **Read source-backed pages** — Prioritize `confidence: verified` pages. Read Key Rules sections.
4. **Check scenarios** — Search `wiki/scenarios/` for matching situations.
5. **Check definitions** — Read relevant `def-` pages.
6. **Assemble answer** — Structure as: Answer → Rules (with sources) → Documentation needed → Nuances → Interpretation (labeled) → Gray areas → Related pages.
7. **Flag gaps** — If wiki lacks coverage, say so. Recommend what source material to ingest. Add to `open-questions.md` if warranted.
8. **Update hot cache** — Add the question to Recent Questions in `hot.md`. Update Active Topics if new pages were consulted.

**Constraints:**
- Never invent a guideline. If not in wiki, say "this topic hasn't been ingested yet."
- When combining multiple rules, show reasoning and label as interpretation.
- Cite wiki pages for Obsidian drill-down.

### 9.3 Lint Workflow (`workflows/lint.md`)

Run periodically for quality control.

**Checks:**

| Check | What it catches |
|-------|----------------|
| Orphan pages | Pages with no inbound links |
| Missing backlinks | A links to B but B doesn't reference A |
| Unsourced claims | `confidence: needs-review` pages older than 30 days |
| Stale pages | `status: active` with `last_updated` older than 6 months |
| Duplicate coverage | Multiple pages covering the same guideline |
| Orphan scenarios | Scenario pages not linked to any topic |
| Unsupported scenarios | Scenario claims not backed by linked sources |
| Dangling open questions | Open questions with status `open` older than 30 days |
| Missing definitions | Terms used across pages without a `def-` page |
| Inconsistent naming | Files not following naming conventions |
| Empty sections | Template sections never filled in |
| Taxonomy gaps | Topic pages not listed in `taxonomy.md` |

**Output:** Summary appended to `change-log.md`.

**Frequency:** After major ingestions, on request, monthly recommended.

### 9.4 Scenario Build Workflow (`workflows/scenario-build.md`)

Triggered when creating scenario pages.

**When to create:**
- Intersection of 2+ guideline areas
- Recurring question requiring combined rules
- Edge case or gray area deserving documented analysis
- Notable real-world underwriting situation

**Steps:**
1. Define borrower profile (2-3 sentences)
2. Identify governing rules from topic pages with source citations
3. Map the analysis — how rules combine for this situation
4. Document specific paperwork needed
5. Flag pitfalls a less experienced underwriter would miss
6. Note compensating factors
7. Identify open issues requiring lender judgment
8. Cross-link to all touched topic pages

**Naming:** Focus on the issue, not the borrower → `scenario-declining-se-income.md`

---

## 10. Hot Cache Design (`wiki/hot.md`)

Token-efficiency layer. Claude Code reads this before scanning the full wiki.

**Contents:**
- Recently Ingested (last 5 sources)
- Active Topics (max 10 pages being built/refined)
- Recent Questions (last 5 queries with page links)
- Open Issues — High Priority (top 5 from open-questions.md)
- Pages Needing Review (max 10 flagged pages)

**Rules:**
- Maximum ~100 lines
- Updated at the end of every ingestion and query session
- Older items roll off as new ones are added
- Pointer file only — links to detail, never contains detail

---

## 11. CLAUDE.md

Full operating instructions for Claude Code. Covers:
- What the vault is and isn't
- Core principles (never invent guidelines, always cite sources, label interpretation, flag conflicts)
- Source trust hierarchy (5 levels)
- Folder structure reference
- File naming conventions
- Frontmatter standard
- Linking conventions
- Workflow references (ingest, query, lint, scenario-build)
- How to handle conflicts
- How to avoid hallucination
- Token efficiency guidance

See Section 13 (Bootstrap Files) for the full CLAUDE.md content.

---

## 12. Implementation Plan

### Phase 1 — Vault Setup
- Create all directories
- Write CLAUDE.md
- Write all four workflow files

### Phase 2 — Starter Files
- Create `wiki/index.md`
- Create `wiki/taxonomy.md`
- Create `wiki/hot.md`
- Create `wiki/change-log.md`
- Create `wiki/open-questions.md`
- Create one sample of each page type with realistic Fannie Mae content

### Phase 3 — First Ingest
- User provides Fannie Mae Selling Guide PDF
- Process section by section following `workflows/ingest.md`
- Build out topic pages, source pages, definitions as extracted
- Log everything in change-log

### Phase 4 — Index Refinement
- Review taxonomy completeness against ingested content
- Fill in cross-references and backlinks
- Run first lint check
- Update hot cache

### Phase 5 — Scenario Library Creation
- Identify top 10-20 common underwriting scenarios from ingested material
- Build scenario pages following `workflows/scenario-build.md`
- Cross-link to topic pages

### Phase 6 — Linting and Maintenance
- Run full lint workflow
- Resolve open questions where possible
- Create missing definition pages
- Build decision trees for most common ambiguous areas

### Phase 7 — Query / Assistant Integration
- Test query workflow with real underwriting questions
- Refine answer format based on what's most useful
- Tune hot cache based on actual usage patterns

---

## 13. Bootstrap Files

The following starter files will be created during Phase 1-2:

1. `CLAUDE.md` — Full operating instructions
2. `wiki/index.md` — Master entry point
3. `wiki/taxonomy.md` — Full domain → subtopic map
4. `wiki/hot.md` — Empty hot cache template
5. `wiki/change-log.md` — Initialized with vault creation entry
6. `wiki/open-questions.md` — Empty template
7. `wiki/topics/gift-funds.md` — Sample topic page
8. `wiki/sources/source-selling-guide-b3-4.3-04.md` — Sample source page (gift funds)
9. `wiki/scenarios/scenario-gift-large-deposit.md` — Sample scenario page
10. `wiki/definitions/def-interested-party-contribution.md` — Sample definition
11. `wiki/checklists/checklist-gift-funds-docs.md` — Sample checklist
12. `wiki/decision-trees/decision-gift-eligibility.md` — Sample decision tree
13. `workflows/ingest.md` — Ingestion SOP
14. `workflows/query.md` — Query SOP
15. `workflows/lint.md` — Lint SOP
16. `workflows/scenario-build.md` — Scenario build SOP

---

## 14. Optimization Recommendations

**Token efficiency:**
- Hot cache (`hot.md`) prevents full-wiki scans on every query
- Taxonomy index allows targeted page retrieval by domain
- Moderate frontmatter balances queryability with maintenance cost
- Definition pages keep topic pages shorter and more focused

**Maintainability:**
- Flat pages within folders — no deep nesting to manage
- Single taxonomy file for reorganization without moving files
- Prefixed naming makes page type obvious at a glance
- Running change log provides full audit trail

**Expandability:**
- Same architecture works for Freddie Mac, FHA, VA, Non-QM vaults
- Each agency gets its own vault with identical structure
- Cross-vault comparison pages can be added later
- Lender overlays can be layered on top with `trust_level: lender`

**Practical use:**
- Scenario pages bridge the gap between static rules and real underwriting
- Open questions file prevents false confidence
- Confidence field makes it clear what's verified vs. interpreted
- Decision trees handle the most common ambiguous situations

**What to avoid:**
- Don't pre-create empty pages for every taxonomy entry — build as needed
- Don't over-tag — 3-5 tags per page is sufficient
- Don't duplicate content across pages — link instead
- Don't build tooling/scripts unless manual workflow becomes painful
