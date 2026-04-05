# Evaluation Module

## Purpose

Assess whether a book is a good candidate for conversion into a Claude Code skill pack. Score its "skillability" and give the user a clear go/no-go recommendation.

---

## Process

### Step 1: AI Knowledge Check

For the given book, state:

1. **Title and Author**
2. **Core Thesis** — What is this book fundamentally about? One sentence.
3. **Key Frameworks/Models** — The named models, matrices, processes the author introduces (e.g., "the 2x2 Care/Challenge matrix" or "the Ackerman bargaining model")
4. **Main Techniques** — Specific repeatable methods the book teaches (e.g., "mirroring," "labeling," "calibrated questions")
5. **Target Domain** — What situations does the book address? (e.g., negotiation, leadership, sales, productivity)
6. **Confidence Level**:
   - **High** — "I know this book well. The above should be accurate — please correct anything I got wrong."
   - **Medium** — "I have partial knowledge. I may be missing key concepts — please fill in gaps."
   - **Low** — "I don't know this book well enough to draft from memory. I'll need you to describe the key frameworks."

If the user provided notes/highlights, read them first and incorporate before presenting.

### Step 2: User Validation

Ask the user:
- "Does this look accurate? Anything I'm missing or getting wrong?"
- Wait for corrections before proceeding to scoring.

### Step 3: Skillability Scoring

Score each dimension 1-5:

#### Actionability (weight: high)
How much of the book teaches repeatable methods vs. tells stories?

| Score | Description | Examples |
|-------|-------------|----------|
| 1 | Pure narrative or memoir | *Shoe Dog*, *Educated* |
| 2 | Mostly narrative with some principles | *The Hard Thing About Hard Things* |
| 3 | Mix of story and principles with some methods | *Thinking, Fast and Slow* |
| 4 | Principles with clear methods and examples | *Crucial Conversations* |
| 5 | Step-by-step methods throughout | *Never Split the Difference* |

#### Modularity (weight: high)
Can the content break into distinct, independent skills?

| Score | Description | Examples |
|-------|-------------|----------|
| 1 | One big interconnected idea | *Sapiens* |
| 2 | 2-3 concepts, heavily interdependent | *Atomic Habits* |
| 3 | Several distinct concepts, some dependencies | *The 7 Habits of Highly Effective People* |
| 4 | Many separable techniques, light dependencies | *Radical Candor* |
| 5 | Toolkit of independent techniques | *Never Split the Difference* |

#### Situational Triggers (weight: high)
Are there clear "use this when X" moments?

| Score | Description | Examples |
|-------|-------------|----------|
| 1 | General life wisdom, no clear triggers | *Man's Search for Meaning* |
| 2 | Broad themes, vague applicability | *Mindset* |
| 3 | Some clear use cases, some general advice | *How to Win Friends and Influence People* |
| 4 | Most techniques map to specific situations | *Crucial Conversations* |
| 5 | Every technique has an obvious trigger | *Never Split the Difference* |

#### Concreteness (weight: medium)
Does the book provide specific scripts, templates, and checklists?

| Score | Description | Examples |
|-------|-------------|----------|
| 1 | Abstract philosophy only | *Meditations* |
| 2 | Principles with occasional examples | *Good to Great* |
| 3 | Principles with worked examples | *Thinking, Fast and Slow* |
| 4 | Methods with example scripts/outputs | *Radical Candor* |
| 5 | Ready-to-use scripts, templates, checklists | *Never Split the Difference* |

#### Scope Clarity (weight: medium)
Is the domain well-defined?

| Score | Description | Examples |
|-------|-------------|----------|
| 1 | Covers everything — life, work, philosophy | *Principles* (Dalio) |
| 2 | Broad domain with some focus | *The 7 Habits* |
| 3 | Themed but wide | *How to Win Friends and Influence People* |
| 4 | Clear domain, some adjacent topics | *Radical Candor* |
| 5 | Tight, well-defined domain | *Never Split the Difference* |

### Step 4: Calculate and Present

**Total Score** = sum of all five dimensions (max 25)

| Range | Verdict | Recommendation |
|-------|---------|----------------|
| **20-25** | Excellent | Full skill pack — expect strong, deep modules across the board |
| **14-19** | Good | Solid skill pack — some modules will be strong, flag areas that may be thin |
| **8-13** | Marginal | Extract only the most actionable parts — skip narrative/philosophical sections |
| **5-7** | Poor fit | Better as a reference document or cheat sheet than a skill pack |

Present the scorecard as a table:

```
Book: "Never Split the Difference" by Chris Voss

| Dimension           | Score | Notes                                    |
|---------------------|-------|------------------------------------------|
| Actionability       | 5/5   | Every chapter teaches a repeatable method |
| Modularity          | 5/5   | Techniques are independent and composable |
| Situational Triggers| 5/5   | Clear "use mirror when..." triggers       |
| Concreteness        | 5/5   | Specific scripts and example dialogues    |
| Scope Clarity       | 5/5   | Tightly focused on negotiation            |
|---------------------|-------|------------------------------------------|
| TOTAL               | 25/25 | Verdict: EXCELLENT                        |

Recommendation: Full skill pack. This book is ideal for conversion.
```

### Step 5: Go/No-Go

Ask the user:
- For scores 14+: "Ready to proceed with generation?"
- For scores 8-13: "This book has some strong parts but will be thin in places. Want to proceed with just the strongest sections, or skip?"
- For scores 5-7: "This book isn't a great fit for a skill pack. Would you prefer a reference doc or cheat sheet instead?"

---

## Handling Low-Confidence Books

When your confidence is Low, switch to structured Q&A before scoring:

1. "What are the 3-5 core frameworks or models in this book?"
2. "For each framework, is there a step-by-step method or is it more of a mindset/principle?"
3. "What specific situations does the book address? (e.g., 'when someone gives you negative feedback')"
4. "Does the book provide scripts, templates, or checklists you could use directly?"
5. "What's the book's domain — is it tightly focused or does it cover many areas?"

Use the answers to score. Be transparent: "Based on your description, here's how I'd score it — adjust if I'm off."
