# book-distill — Design Document

**Date:** 2026-04-05
**Status:** Approved
**Purpose:** Meta-skill that distills any book into an executable Claude Code skill pack.

---

## Overview

`book-distill` is a Claude Code skill that takes one or more book titles, evaluates their "skillability," and generates structured skill packs — complete with modules, templates, examples, decision frameworks, and guardrails. Supports multi-book synthesis for overlapping or complementary content.

## Invocation

```
/book-distill "Never Split the Difference"
/book-distill "Radical Candor" "Crucial Conversations"
/book-distill "The Manager's Path" --notes ~/highlights/managers-path.md
```

**Arguments:**
- One or more book titles (required)
- `--notes` — path to highlights/excerpts/notes file (optional)
- `--output` — output directory (optional, defaults to current directory)

---

## End-to-End Flow

1. **Input** — User names book(s), optionally provides notes/highlights
2. **Evaluate** — AI drafts what it knows, scores skillability, presents results
3. **User validates** — Corrects/adds to AI's understanding, decides go/no-go per book
4. **Multi-book decision** (if >1 book) — Overlap analysis, synthesis recommendations
5. **Structure recommendation** — Router+modules vs. standalone skills
6. **Skill generation** — Produces full skill pack with incremental review
7. **Finalize** — Writes files, initializes git repo, generates README

---

## Phase 1: Evaluation

### AI Knowledge Check

For each book, the AI states:
- Author, core thesis, key frameworks, main techniques
- Confidence level: "I know this book well" / "Partial knowledge" / "I'll need your input"

### Skillability Scoring

| Dimension | 1 (Poor) | 3 (Moderate) | 5 (Excellent) |
|-----------|----------|--------------|---------------|
| **Actionability** | Pure narrative/memoir | Mix of story + principles | Step-by-step methods |
| **Modularity** | One big idea | A few distinct concepts | Many separable techniques |
| **Situational triggers** | General life wisdom | Some clear use cases | Obvious "use when X" moments |
| **Concreteness** | Abstract philosophy | Principles with examples | Scripts, templates, checklists |
| **Scope clarity** | Covers everything | Broad but themed | Tight domain |

### Verdict

- **20-25:** Excellent fit — proceed with full skill pack
- **14-19:** Good fit — some modules will be strong, flag thin areas
- **8-13:** Marginal — recommend extracting only the strongest parts
- **5-7:** Poor fit — suggest alternative formats (reference doc, cheat sheet)

### User Validation

User corrects AI's understanding, adds missing frameworks, adjusts scores. Decides go/no-go.

---

## Phase 2: Multi-Book Flow

When 2+ books are provided:

### Overlap Analysis

Map each book's concepts into three categories:

- **Unique** — exists only in one book, stays in that book's pack
- **Complementary** — different books cover the same situation from different angles; candidates for deep synthesis into unified modules stronger than either source alone
- **Redundant** — books say essentially the same thing; pick stronger treatment, cite both

### Synthesis Recommendation

Present analysis like:
```
Overlap Analysis: "Radical Candor" x "Never Split the Difference"

UNIQUE (keep separate):
  RC: Praise frameworks, quadrant diagnosis, repair skills
  NSTD: Ackerman model, black swan hunting

COMPLEMENTARY (synthesize):
  "Delivering hard feedback" — RC's Care+Challenge framing
    + NSTD's accusation audit & calibrated questions
    -> Synthesized module: stronger than either alone

REDUNDANT:
  Active listening — both cover it, NSTD deeper -> use NSTD's
```

### Output Structure

- Shared router `SKILL.md` at the top level routes by situation
- Each book gets its own subfolder for unique skills
- Synthesized modules live in a `synthesized/` folder with attribution to both sources

---

## Phase 3: Generation

### Structure Decision

AI recommends based on book's nature:
- **Single deep framework** -> router `SKILL.md` + `modules/` subfolder (negotiate-skills pattern)
- **Collection of distinct situations** -> standalone `SKILL.md` per skill (radical-candor pattern)

User can override.

### Per Skill/Module Output

Each generated skill includes:
- **SKILL.md** — frontmatter (name, description, argument-hint), purpose, when to use, philosophy/operating rules
- **Modules** — step-by-step methods, inputs needed, example outputs, failure modes
- **Templates** — reusable fill-in-the-blank templates for common scenarios
- **Decision framework** — quick-reference table mapping situations to techniques
- **Quick-start mode** — 30-second version for live situations
- **Guardrails** — explicit "when NOT to use this" and misuse warnings

### Incremental Review

Each file presented in 200-300 word sections. User validates before moving on. Critical review points:
- Example outputs — are they realistic?
- Guardrails — are they sufficient?
- Templates — are they practical?

### Finalize

- Write all files to disk
- Generate README.md with install instructions, skill table, flow diagram
- Initialize git repo, create initial commit
- Report stats: X skills, Y modules, Z templates

---

## Repo Structure

```
book-distill/
├── skills/
│   └── book-distill/
│       ├── SKILL.md              # The meta-skill itself
│       └── modules/
│           ├── evaluate.md       # Skillability scoring rubric & process
│           ├── generate.md       # Skill pack generation logic
│           ├── synthesize.md     # Multi-book overlap detection & merging
│           └── templates.md      # Output templates for generated skills
└── README.md
```

---

## Content Strategy

The skill uses a **combination approach** for book knowledge:
- AI proposes what it knows from training data (works well for popular books)
- User fills gaps, corrects, adds missing frameworks
- For obscure books, gracefully degrades to structured Q&A
- Optional `--notes` flag lets users feed in highlights/excerpts

---

## Precedents

Two existing book-to-skill packs inform the output quality:
- **negotiate-skills** — *Never Split the Difference* — router+modules pattern
- **radical-candor** — *Radical Candor* — standalone skills pattern

The generated output should match the quality and depth of these examples.
