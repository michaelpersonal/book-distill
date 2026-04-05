# book-distill

Distill any book into an executable Claude Code skill pack. Evaluates skillability, generates structured skills with modules/templates/examples, and supports multi-book synthesis.

## What This Is

A meta-skill — it doesn't teach you a book's content, it converts a book's methods into Claude Code skills you can actually use. Feed it a title, it scores the book's "skillability," then generates a complete skill pack: SKILL.md files, modules, templates, decision frameworks, and guardrails.

## Installation

In Claude Code:

```
/install gh:michaelpersonal/book-distill
```

## Usage

```
/book-distill "Never Split the Difference"
/book-distill "Radical Candor" "Crucial Conversations"
/book-distill "The Manager's Path" --notes ~/highlights/managers-path.md
```

**Arguments:**
- One or more book titles (required)
- `--notes` — path to highlights/excerpts/notes file (optional)
- `--output` — output directory (optional, defaults to cwd)

## How It Works

```
┌─────────────────────────────────────────────────────────┐
│  1. EVALUATE                                            │
│     AI states what it knows → scores skillability       │
│     → user validates → go/no-go                         │
├─────────────────────────────────────────────────────────┤
│  2. MULTI-BOOK (if 2+ books)                            │
│     Overlap analysis → unique / complementary / redundant│
│     → synthesis recommendations → user confirms         │
├─────────────────────────────────────────────────────────┤
│  3. STRUCTURE                                           │
│     Router+modules vs. standalone skills                │
│     → based on book's nature → user can override        │
├─────────────────────────────────────────────────────────┤
│  4. GENERATE                                            │
│     Skill files produced → incremental review           │
│     → user validates each section                       │
├─────────────────────────────────────────────────────────┤
│  5. FINALIZE                                            │
│     Write files → README → git init → commit            │
└─────────────────────────────────────────────────────────┘
```

## Skillability Score

Books are scored on 5 dimensions (1-5 each, max 25):

| Dimension | What it measures |
|-----------|-----------------|
| **Actionability** | Methods vs. narrative |
| **Modularity** | Separable techniques vs. one big idea |
| **Situational Triggers** | Clear "use when X" vs. general wisdom |
| **Concreteness** | Scripts/templates vs. abstract principles |
| **Scope Clarity** | Tight domain vs. covers everything |

| Score | Verdict |
|-------|---------|
| 20-25 | Excellent — full skill pack |
| 14-19 | Good — solid with some thin areas |
| 8-13  | Marginal — extract strongest parts only |
| 5-7   | Poor fit — better as reference doc |

## Multi-Book Synthesis

When given multiple books, the skill analyzes overlap:

- **Unique** concepts stay in each book's pack
- **Complementary** concepts get synthesized into unified modules (stronger than either source)
- **Redundant** concepts use the stronger treatment

The output includes a shared router that maps situations to the right skill regardless of source book.

## Skill Structure

```
book-distill/
├── skills/
│   └── book-distill/
│       ├── SKILL.md              # The meta-skill
│       └── modules/
│           ├── evaluate.md       # Skillability scoring
│           ├── generate.md       # Skill pack generation
│           ├── synthesize.md     # Multi-book overlap & merging
│           └── templates.md      # Output format templates
└── README.md
```

## Examples Built With This Pattern

- [negotiate-skills](https://github.com/michaelpersonal/negotiate-skills) — *Never Split the Difference* (router+modules)
- [radical-candor-skills](https://github.com/michaelpersonal/radical-candor-skills) — *Radical Candor* (standalone skills)
