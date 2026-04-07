# Fannie Mae Underwriting Knowledge System — Claude Code Operating Instructions

## What This Vault Is

A markdown-based, Obsidian-compatible knowledge system for Fannie Mae conventional loan underwriting guidelines. It is built for two audiences simultaneously:

- **Humans** — browsing via Obsidian (wikilinks, graph view, tag filtering)
- **Claude Code** — structured querying via frontmatter, hot cache, and taxonomy index

This vault is the product. The `workflows/` folder holds operational SOPs that govern how Claude Code interacts with it.

---

## Core Principles (Non-Negotiable)

1. **Never invent guidelines.** If a rule isn't in the wiki backed by a sourced page, it does not exist here.
2. **Always cite sources.** Every factual claim in a topic page ends with `(Source: [[source-page]])`.
3. **Label all interpretation.** Content that reflects professional judgment — not direct source language — goes in the `## Interpretation Notes` section with a ⚠️ warning.
4. **Flag conflicts, never resolve silently.** If two sources disagree, log both in `open-questions.md` and show both in the topic page.
5. **Prefer accuracy over completeness.** A shorter, verified page is better than a longer, uncertain one.
6. **Separate fact from interpretation.** Keep the `## Key Rules` section sourced-only.

---

## Source Trust Hierarchy

| Level | Label | What it means | How to cite |
|-------|-------|---------------|-------------|
| 1 | `official` | Direct Fannie Mae Selling Guide text | State as fact with source citation |
| 2 | `faq` | Official Fannie Mae FAQ or Lender Letter | State as fact with source citation |
| 3 | `du-official` | DU-specific official material | State as fact with source citation |
| 4 | `lender` | Lender training notes, bulletins, overlays | Label as `(Lender note: ...)` |
| 5 | `personal` | Interpretation, experience, practitioner notes | Must go in Interpretation Notes section with ⚠️ |

When sources conflict: add both to the topic page and flag in `open-questions.md`. Never pick one silently.

---

## Folder Structure

```
Mortgage Knowledge/
├── CLAUDE.md                    ← You are here
├── raw/                         ← Drop zone for source PDFs, notes, screenshots
├── wiki/
│   ├── index.md                 ← Master entry point — start here for navigation
│   ├── hot.md                   ← Hot cache (~100 lines max) — read FIRST on every query
│   ├── change-log.md            ← Running log of all ingestion + edits
│   ├── open-questions.md        ← Unresolved gray areas needing confirmation
│   ├── taxonomy.md              ← Full domain → subtopic map with wikilinks
│   ├── topics/                  ← Core guideline pages (primary growth area)
│   ├── scenarios/               ← Real-world underwriting situation pages
│   ├── sources/                 ← Source attribution pages
│   ├── definitions/             ← Term definitions (brief, linkable)
│   ├── checklists/              ← Documentation requirement checklists
│   └── decision-trees/          ← Decision logic for ambiguous situations
├── workflows/                   ← Operational SOPs
│   ├── ingest.md                ← How to process new raw materials
│   ├── query.md                 ← How to answer underwriting questions
│   ├── lint.md                  ← Health check / quality control
│   └── scenario-build.md        ← How to create scenario pages
└── .tmp/                        ← Disposable processing artifacts
```

---

## File Naming Conventions

- All lowercase, kebab-case
- Topics: descriptive name → `self-employed-income.md`, `gift-funds.md`
- Scenarios: `scenario-` prefix → `scenario-declining-se-income.md`
- Sources: `source-` prefix → `source-selling-guide-b3-3.1-09.md`
- Definitions: `def-` prefix → `def-stable-monthly-income.md`
- Checklists: `checklist-` prefix → `checklist-self-employed-docs.md`
- Decision trees: `decision-` prefix → `decision-rental-income-method.md`

---

## Frontmatter Standard

Every page requires YAML frontmatter:

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

**Confidence levels:**
- `verified` — Directly from official Selling Guide or FAQ
- `interpreted` — Requires professional judgment or combines multiple rules
- `needs-review` — Uncertain, incomplete, or newly created

**Source page exception:** Use `trust_level` instead of `confidence`. No `sources` field (the source page IS the source).

**Tagging:** Use 3–5 lowercase kebab-case tags matching taxonomy domains and subtopics.

---

## Linking Conventions

- Wikilinks: `[[page-name]]`
- Aliased links: `[[def-stable-monthly-income|stable monthly income]]`
- Source citations inline: `(Source: [[source-page]])`

---

## Token Efficiency: Query Order

When answering a question, read files in this order to avoid unnecessary context loading:

1. `wiki/hot.md` — always first
2. `wiki/index.md` — for navigation
3. `wiki/taxonomy.md` — to identify relevant topic pages
4. Specific topic / scenario / definition pages as needed
5. Source pages only if excerpt verification is needed

Do NOT scan all files in a folder. Use taxonomy and frontmatter tags to identify what's relevant.

---

## Workflow References

| Task | Workflow |
|------|----------|
| New source material in `raw/` | `workflows/ingest.md` |
| Answering an underwriting question | `workflows/query.md` |
| Quality check / health check | `workflows/lint.md` |
| Building a scenario page | `workflows/scenario-build.md` |

---

## How to Handle Conflicts

1. Identify both sources and their trust levels
2. State both in the topic page under ## Exceptions & Nuances or ## Key Rules (clearly labeled)
3. Add an entry to `open-questions.md` with both source links and a clear description of the conflict
4. Set `confidence: needs-review` on the affected topic page
5. Never pick the higher-trust source and drop the other without logging the conflict

---

## Hallucination Prevention

- If you are uncertain whether a rule exists in the wiki, say so. Do not guess.
- "This topic hasn't been ingested yet" is a valid and correct answer.
- If a rule seems familiar from training data but isn't in the wiki, do not include it in the answer. Flag it as a potential ingestion candidate.
- Interpretation notes are acceptable — but must be labeled ⚠️ and kept separate from sourced facts.
- When combining two sourced rules to reach a conclusion, show the reasoning step explicitly and label it as an inference.
