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

**Skill names**: lowercase, hyphenated, verb-first when possible — always in English regardless of output language
- Good: `give-tough-feedback`, `prepare-negotiation`, `respond-to-bad-offer`
- Bad: `tough-feedback-skill`, `negotiation-preparation`, `bad-offer-response`

**Module names**: match the primary action — always in English regardless of output language
- Good: `prepare.md`, `tactics.md`, `closing.md`
- Bad: `chapter-3.md`, `part-two.md`, `miscellaneous.md`

**Template names**: describe the scenario, not the technique — in the output language
- English: "Vendor Over Budget", "Peer Overreach", "Unrealistic Timeline"
- Chinese: "供应商超预算", "同事越权", "不合理的时间线"
- Japanese: "ベンダー予算超過", "同僚の越権", "非現実的な期限"

---

## Multilingual Generation Rules

When generating in a non-English language, follow these rules:

### What stays in English
- **File names** — `SKILL.md`, `prepare.md`, `templates.md`, etc.
- **Frontmatter keys** — `name`, `description`, `argument-hint`
- **Frontmatter `name` value** — skill names are always English (for CLI invocation)
- **Markdown structure** — headings like `## Module:`, `**Purpose**:`, `**Method**:` stay in English for parsing consistency

### What gets localized
- **Frontmatter `description` value** — written in the output language
- **All body content** — role statements, methods, examples, guardrails, templates
- **Example outputs** — must feel native, not translated. Use culturally appropriate workplace scenarios
- **Decision framework entries** — situations and instructions in the output language
- **README body text** — descriptions, quick start, skill flow
- **Template scripts** — the actual language people would say/write

### Cultural adaptation
Don't just translate — adapt:

**Chinese (zh):**
- Use 您 vs. 你 appropriately in formal workplace contexts
- Workplace examples should reflect Chinese business norms (e.g., 面子 dynamics, hierarchical communication, 饭局 contexts)
- Templates should include both spoken (口语) and written (书面语) registers where relevant
- Use 「」for quotes in templates if the user's notes suggest traditional formatting

**Japanese (ja):**
- Use appropriate keigo (敬語) levels — most workplace skills need 丁寧語 at minimum, some need 尊敬語/謙譲語
- Workplace examples should reflect Japanese norms (e.g., 根回し, 報連相, 空気を読む)
- Templates should distinguish between email (メール), meeting (会議), and 1-on-1 (面談) registers
- Include both the concept in Japanese and the book's original term if the book is translated

### Cross-language books
When the book is in one language but output is in another:
- Preserve the book's original key terms alongside translations: e.g., "tactical empathy（戦術的共感）"
- The first mention uses both; subsequent mentions can use just the output language term
- Attribution always includes the original title: *Never Split the Difference*（『決して「イエス」と言うな』）
