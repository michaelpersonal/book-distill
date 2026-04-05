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

```mermaid
flowchart TD
    Start(["/book-distill 'Book Title'"]) --> Input{"How many\nbooks?"}

    Input -->|"1 book"| Eval
    Input -->|"2+ books"| EvalMulti

    subgraph Phase1 ["Phase 1: Evaluate"]
        Eval["AI drafts what it knows\nabout the book"]
        Eval --> Score["Score skillability\n(5 dimensions, max 25)"]
        Score --> Verdict{Score?}
        Verdict -->|"20-25\nExcellent"| Go["User validates\n→ Go"]
        Verdict -->|"14-19\nGood"| Go
        Verdict -->|"8-13\nMarginal"| Partial["Extract strongest\nparts only"]
        Verdict -->|"5-7\nPoor"| RefDoc["Suggest reference\ndoc instead"]
    end

    subgraph Phase1Multi ["Phase 1: Evaluate (each book)"]
        EvalMulti["Evaluate each book\nindependently"]
    end

    EvalMulti --> Synth

    subgraph Phase2 ["Phase 2: Multi-Book Synthesis"]
        Synth["Map concepts\nacross books"]
        Synth --> Categorize{"Categorize\neach concept"}
        Categorize -->|"Unique"| Keep["Keep in\nbook's pack"]
        Categorize -->|"Complementary"| Merge["Synthesize into\nunified module"]
        Categorize -->|"Redundant"| Pick["Use stronger\ntreatment"]
    end

    Go --> Structure
    Partial --> Structure
    Keep --> Structure
    Merge --> Structure
    Pick --> Structure

    subgraph Phase3 ["Phase 3: Structure"]
        Structure{"Book's\nnature?"}
        Structure -->|"Single deep\nframework"| Router["Router SKILL.md\n+ modules/"]
        Structure -->|"Distinct\nsituations"| Standalone["Standalone\nSKILL.md per skill"]
    end

    Router --> Generate
    Standalone --> Generate

    subgraph Phase4 ["Phase 4: Generate"]
        Generate["Generate skill files"]
        Generate --> Review["Present each section\n(200-300 words)"]
        Review --> Validate{"User\napproves?"}
        Validate -->|"Yes"| Next["Next section"]
        Validate -->|"Revise"| Generate
        Next --> Done["All files complete"]
    end

    subgraph Phase5 ["Phase 5: Finalize"]
        Done --> WriteFiles["Write files to disk"]
        WriteFiles --> GenREADME["Generate README\nwith install instructions"]
        GenREADME --> GitCommit["Git init + commit"]
        GitCommit --> Stats(["Report: X skills,\nY modules, Z templates"])
    end

    style Phase1 fill:#1a1a2e,stroke:#e94560,color:#fff
    style Phase1Multi fill:#1a1a2e,stroke:#e94560,color:#fff
    style Phase2 fill:#16213e,stroke:#0f3460,color:#fff
    style Phase3 fill:#1a1a2e,stroke:#e94560,color:#fff
    style Phase4 fill:#16213e,stroke:#0f3460,color:#fff
    style Phase5 fill:#1a1a2e,stroke:#e94560,color:#fff
    style Start fill:#e94560,stroke:#e94560,color:#fff
    style Stats fill:#0f3460,stroke:#0f3460,color:#fff
    style RefDoc fill:#533483,stroke:#533483,color:#fff
```

### Quick Reference

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
