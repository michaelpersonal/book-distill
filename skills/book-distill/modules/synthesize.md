# Multi-Book Synthesis Module

## Purpose

When the user provides 2+ books, analyze overlap between them and recommend which modules to synthesize into unified skills vs. keep separate.

---

## Process

### Step 1: Concept Mapping

For each book, list its key concepts and techniques in a flat list:

```
"Radical Candor":
- 2x2 Care/Challenge framework
- SBI feedback model (Situation-Behavior-Impact)
- Praise specifically
- Give tough feedback
- Push back on authority
- Repair after being too harsh
- Repair after being too vague
- Coach underperformers

"Never Split the Difference":
- Tactical empathy
- Mirroring
- Labeling
- Calibrated questions
- Accusation audit
- Ackerman model
- Black swan hunting
- Rule of Three
```

### Step 2: Overlap Detection

Compare concepts across books and categorize each into one of three buckets:

#### Unique
Concept exists meaningfully in only one book. It stays in that book's skill pack.

**Criteria:**
- The technique is distinctive to that author's methodology
- No other book covers the same situation with a comparable method
- Removing it would leave a gap in that book's system

#### Complementary
Different books address the same situation from different angles. These are candidates for **deep synthesis** — merging into a unified module that's stronger than either source.

**Criteria:**
- Both books address the same real-world situation (e.g., "delivering hard feedback")
- The approaches are different but compatible (not contradictory)
- Combining them produces a more complete method than either alone
- A practitioner would naturally use both approaches together

**How to synthesize:**
- Create a unified module with clear phases that draw from each source
- Attribute each element: "From [Book]: [technique]"
- The synthesized skill should feel like one coherent method, not a collage
- Write new example outputs that demonstrate both books' techniques working together
- Add a "Sources" section at the bottom listing which book each element comes from

#### Redundant
Books teach essentially the same technique. Pick the stronger treatment.

**Criteria:**
- Both books cover the same concept with similar depth
- The methods are interchangeable, not complementary
- Using both would be repetitive, not additive

**How to handle:**
- Use the deeper/more actionable treatment as the primary source
- Cite the other book as "also covers this"
- If the weaker treatment adds one useful nuance, incorporate it as a note

### Step 3: Present the Analysis

Format as:

```
═══════════════════════════════════════════════════════
OVERLAP ANALYSIS: "Book A" × "Book B"
═══════════════════════════════════════════════════════

UNIQUE — stays in each book's pack:
  Book A:
    • [concept] — [one-line description]
    • [concept] — [one-line description]
  Book B:
    • [concept] — [one-line description]
    • [concept] — [one-line description]

COMPLEMENTARY — recommend synthesis:
  "[Situation name]"
    Book A brings: [technique and what it contributes]
    Book B brings: [technique and what it contributes]
    Synthesized: [what the combined module would look like]
    Why combine: [why the combination is stronger]

  "[Situation name]"
    Book A brings: ...
    Book B brings: ...
    Synthesized: ...
    Why combine: ...

REDUNDANT — use stronger treatment:
  "[Concept]"
    Book A: [brief assessment]
    Book B: [brief assessment]
    Recommendation: Use [Book X]'s treatment (deeper/more actionable)

═══════════════════════════════════════════════════════
```

### Step 4: User Confirmation

Ask:
- "Does this overlap analysis look right?"
- "Any concepts I miscategorized?"
- "For the complementary items — do you want me to synthesize all of them, or keep any separate?"

Wait for confirmation before proceeding to generation.

### Step 5: Output Structure for Multi-Book Packs

```
[output-dir]/
├── SKILL.md                    # Shared router — routes by situation to the right skill
├── [book-a-slug]/              # Book A's unique skills
│   ├── SKILL.md or modules/
│   └── ...
├── [book-b-slug]/              # Book B's unique skills
│   ├── SKILL.md or modules/
│   └── ...
├── synthesized/                # Merged modules from complementary concepts
│   ├── [situation-slug].md
│   └── ...
└── README.md
```

The top-level `SKILL.md` acts as a router:
- Maps situations to the right skill/module
- Indicates source book(s) for each skill
- Provides a decision framework spanning all books

---

## Handling Contradictions

When books give conflicting advice for the same situation:

1. **Name the contradiction explicitly** — don't paper over it
2. **Present both approaches** with the context where each works better
3. **Let the user decide** which framing they prefer, or whether to include both with guidance on when to use each
4. Example: "Book A says do X in this situation, Book B says do Y. Book A's approach works better when [context], Book B's when [context]. Which framing do you prefer, or should I include both with situational guidance?"

---

## Scaling Beyond Two Books

For 3+ books:
- Run pairwise overlap analysis for each combination
- Group complementary concepts that span 3+ books into single synthesized modules
- The router SKILL.md becomes more important — it should clearly map "I'm facing X" → "use this skill from [Book(s)]"
- Consider grouping books by domain if they diverge significantly (e.g., two leadership books + one sales book → separate sections in the router)
