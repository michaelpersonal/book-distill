# Generation Module

## Purpose

Generate a complete, high-quality skill pack from evaluated book content. Produces SKILL.md files, modules, templates, decision frameworks, and guardrails.

---

## Process

### Step 1: Determine Output Structure

Based on the book's nature (decided in Phase 3 of the main flow):

**Router + Modules** (single deep framework):
```
skills/[skill-name]/
├── SKILL.md                      # Router — overview, philosophy, decision framework, quick-start
└── modules/
    ├── [phase-1].md              # First phase/category of techniques
    ├── [phase-2].md              # Second phase/category
    ├── [phase-3].md              # ...
    ├── templates.md              # Reusable templates for common scenarios
    └── [additional].md           # Guardrails, agent prompts, etc. as needed
```

**Standalone Skills** (collection of distinct situations):
```
skills/
├── [skill-1]/SKILL.md            # Each skill is self-contained
├── [skill-2]/SKILL.md
├── [skill-3]/SKILL.md
└── ...
```

### Step 2: Generate the Router SKILL.md

Every skill pack needs a main SKILL.md. Follow this structure:

```markdown
---
name: [skill-name]
description: [One sentence. Start with a verb. Say what it does, not what the book is about.]
argument-hint: [describe what the user should provide as input]
---

[Role statement — who the AI becomes when this skill is active. 2-3 sentences max.]

## What This Skill Is For
[2-3 sentences describing the real-world situations this skill addresses.]

## Good Use vs. Misuse
**Good**: [3-4 examples of appropriate use]
**Misuse**: [3-4 examples of what NOT to do with this skill]

---

## Core Philosophy ([N] Operating Rules)
[Numbered list of the book's key principles, distilled to one line each.
Each rule should be actionable, not philosophical.
Bad: "Communication is important"
Good: "Label emotions before addressing content — the feeling must be acknowledged before the logic can land"]

---

## Available Modules / Skills
[List each module/skill with:
- File path
- Command name
- One-line description of what it does and when to use it]

---

## Decision Framework (Quick Reference)
[Table mapping situations → which tool/technique to use]

| Situation | Tool | Key |
|-----------|------|-----|
| [specific trigger] | **[technique name]** | [one-line how-to] |

---

## Quick-Start Mode (30 Seconds)
[For live situations without time for full prep.
3-4 numbered steps, each one sentence.
Plus a "what to avoid" list.]

### Mid-Conversation Reframe
[Table of "If you're... → Switch to..." for real-time course correction]
```

### Step 3: Generate Modules

For router+modules structure, each module file follows this pattern:

```markdown
# [Module Category Name]

## Module: [module-name]

**Purpose**: [One sentence — what this module produces]

**When to use**: [Specific situational triggers]

**Inputs needed**:
- [What information the user must provide]
- [Each input on its own line]

**Method**:
1. [Numbered steps — each step is one concrete action]
2. [Steps should produce visible output, not just "think about X"]
3. [Include specific language patterns where the book provides them]
4. [End with a deliverable — something the user walks away with]

**Example output**:
[A complete, realistic example showing what following the method produces.
Use a workplace scenario. Make it specific enough to be useful as a template.
Format it the way the user would actually use it.]

**Failure modes**:
- [What it looks like when this technique is used poorly]
- [Common mistakes and how to recognize them]
- [When this technique makes things worse]

---

[Repeat for each module in this category]
```

For standalone skills, each SKILL.md follows the same structure as the `give-tough-feedback` example — self-contained with the full method, examples, and failure checks.

### Step 4: Generate Templates

Create a `templates.md` (or include templates in each standalone skill) with:

```markdown
# Templates

## Template: [Scenario Name]

**Situation**: [When to use this template]

**Setup**:
- [Context the user needs to fill in]

**Script**:
> "[Fill-in-the-blank script using the book's techniques]"

**What makes this work**: [1-2 sentences explaining which principles are at play]

**Watch out for**: [Common way this template gets misused]

---

[At least 3-6 templates covering the most common scenarios]
```

### Step 5: Generate Guardrails

Every skill pack needs explicit guardrails. Include either as a section in SKILL.md or as a separate `guardrails.md` / `workplace.md`:

- **When to use the full toolkit vs. lighter touch** — not every situation needs the heavy machinery
- **Channel-specific guidance** — email vs. meeting vs. Slack vs. 1:1 (if applicable)
- **Power dynamics** — how to adjust when you have more/less power
- **Cultural considerations** — techniques that may not translate across contexts
- **Signs of misuse** — mechanical application, manipulation, over-engineering low-stakes situations

### Step 6: Incremental Review

Present each generated file to the user in sections of 200-300 words. After each section:
- "Does this look right?"
- "Anything to add or change?"

**Priority review points:**
- Example outputs — "Is this realistic? Would someone actually say this?"
- Guardrails — "Anything missing? Any scenario where this could go wrong?"
- Templates — "Would you actually use this? Is the language natural?"
- Decision framework — "Does this mapping make sense? Any situations missing?"

Revise before moving to the next file.

---

## Quality Checklist

Before finalizing any generated skill, verify:

- [ ] Every technique has a clear situational trigger ("use when...")
- [ ] Every method has numbered steps that produce visible output
- [ ] Every module has at least one realistic example
- [ ] Failure modes are specific, not generic ("don't use it wrong")
- [ ] Guardrails address power dynamics and misuse
- [ ] Language patterns from the book are preserved where they exist
- [ ] The skill is executable — a user can follow the steps cold and produce useful output
- [ ] Attribution is clear — the user knows which book each technique comes from
- [ ] The decision framework covers the most common situations (at least 6-8 rows)
- [ ] Quick-start mode actually works in 30 seconds

---

## Naming Conventions

**Skill names**: lowercase, hyphenated, verb-first when possible
- Good: `give-tough-feedback`, `prepare-negotiation`, `respond-to-bad-offer`
- Bad: `tough-feedback-skill`, `negotiation-preparation`, `bad-offer-response`

**Module names**: match the primary action
- Good: `prepare.md`, `tactics.md`, `closing.md`
- Bad: `chapter-3.md`, `part-two.md`, `miscellaneous.md`

**Template names**: describe the scenario, not the technique
- Good: "Vendor Over Budget", "Peer Overreach", "Unrealistic Timeline"
- Bad: "Mirror Template", "Label Template", "Accusation Audit Template"
