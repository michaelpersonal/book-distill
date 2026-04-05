# Output Templates

## Purpose

Reference templates that define the exact output format for each type of generated file. The generation module uses these templates to ensure consistent, high-quality output across all book-to-skill conversions.

---

## Template: SKILL.md (Router Style)

Use for books with a single deep framework.

```markdown
---
name: {{skill-name}}
description: {{One sentence starting with a verb. What the skill does, not what the book is about. Include the book title for attribution.}}
argument-hint: {{[describe what the user should provide as context]}}
---

You are a {{role}} grounded in the methods of {{Author}}'s *{{Book Title}}*, adapted for {{domain}} use. You help users {{primary action}} — not by summarizing theory, but by running practical skill modules that produce usable output.

## What This Skill Is For

{{2-3 sentences describing real-world situations. Be specific about the kinds of problems this solves.}}

## Good Use vs. Misuse

**Good**: {{3-4 specific examples of appropriate use}}

**Misuse**: {{3-4 specific examples of what NOT to do}}

---

## Core Philosophy ({{N}} Operating Rules)

{{Numbered list. Each rule is one bolded sentence followed by a one-line explanation.
Format: **Rule.** Explanation.}}

---

## Available Modules

{{For each module:}}
### {{Phase/Category Name}}
**File: `modules/{{filename}}.md`**
- **{{module-name}}** — {{one-line description of what it does and when to use it}}

---

## Decision Framework (Quick Reference)

| Situation | Tool | Key |
|-----------|------|-----|
| {{specific trigger}} | **{{technique}}** | {{one-line instruction}} |

---

## Quick-Start Mode (30 Seconds)

{{3-4 numbered steps, each one sentence}}

{{A "what to avoid" bullet list}}

### Mid-Conversation Reframe

| If you're... | Switch to... |
|-------------|-------------|
| {{bad state}} | {{specific correction with example language}} |
```

---

## Template: SKILL.md (Standalone Style)

Use for individual situational skills.

```markdown
---
name: {{skill-name}}
description: {{One sentence. Verb-first. Describe the action, not the concept.}}
argument-hint: {{[what the user should describe]}}
---

You are a {{role}} grounded in {{framework name}} from {{Author}}'s *{{Book Title}}*. Help the user {{primary action}}.

## Core Principle

**{{One-sentence principle.}}** {{2-3 sentence explanation of why this matters.}}

## The Method

### Step 1: {{Action Name}}
{{What to do. Include the specific question to ask the user.}}

- Bad: {{example of wrong approach}}
- Good: {{example of right approach}}

Ask the user: **{{specific question}}**

### Step 2: {{Action Name}}
{{Continue the pattern...}}

### Step N: {{Final Step}}
{{End with a deliverable — something concrete the user walks away with.}}

## Drafting the Output

Combine the steps into a {{format — spoken version, written doc, email, etc.}}:

**Template**:
> "{{Fill-in-the-blank template with placeholders}}"

## Failure Mode Check

Before delivering, check:

| Check | If yes, fix |
|-------|------------|
| {{failure condition}} | {{specific correction}} |

## Output

Provide:
1. {{Deliverable 1}}
2. {{Deliverable 2}}
3. {{Deliverable N}}
```

---

## Template: Module File

```markdown
# {{Category Name}} Modules

## Module: {{module-name}}

**Purpose**: {{One sentence — what this module produces}}

**When to use**: {{Specific situational triggers — "before X", "when Y happens", "after Z"}}

**Inputs needed**:
- {{Input 1 — what information the user must provide}}
- {{Input 2}}

**Method**:
1. {{Concrete action that produces visible output}}
2. {{Next step — reference specific language patterns from the book where they exist}}
3. {{Continue...}}
4. {{End with a clear deliverable}}

**Example output**:
```
{{Complete, realistic workplace example.
Show what following the method actually produces.
Use a specific scenario, not a generic one.
Make it detailed enough to serve as a template.}}
```

**Failure modes**:
- {{What bad usage looks like — be specific}}
- {{Common mistake and how to recognize it}}
- {{When this technique makes things worse, not better}}

---
```

---

## Template: Templates File

```markdown
# Templates

## Template: {{Scenario Name}}

**Situation**: {{One sentence describing when to use this}}

**Setup**:
- {{Context the user fills in — who, what, where}}
- {{Any prerequisites}}

**Script**:
> "{{Ready-to-use or fill-in-the-blank language.
Use [BRACKETS] for parts the user customizes.
Keep it natural — this should sound like something a real person would say.}}"

**What makes this work**: {{1-2 sentences naming which principles from the book are operating}}

**Watch out for**: {{The most common way this template gets misused}}

---
```

---

## Template: README.md

```markdown
# {{Skill Pack Name}}

{{One sentence description.}} Built from *{{Book Title}}* by {{Author}}.

## Installation

In Claude Code:

\```
/install {{repo-path}}
\```

## Skills

| Skill | Command | When to use |
|-------|---------|-------------|
| {{Skill Name}} | `/{{command}}` | {{One sentence trigger}} |

## {{Framework Name — optional}}

{{If the book has a core visual framework (like the 2x2 matrix), include it here as ASCII art or a brief explanation.}}

## Quick Start

{{The single most useful entry point — one sentence telling the user what to try first.}}

## Skill Flow

\```
{{ASCII flow diagram showing: situation → which skill to use}}
\```
```

---

## Template: Synthesized Module (Multi-Book)

```markdown
# {{Situation Name}} — Synthesized Module

**Sources**: *{{Book A}}* by {{Author A}} + *{{Book B}}* by {{Author B}}

**Purpose**: {{What this combined module does — should be stronger than either source alone}}

**When to use**: {{Situational trigger}}

---

## Combined Method

### Phase 1: {{Phase from Book A or B}}
*From {{Book A}}:*
{{Steps from the first book's approach}}

### Phase 2: {{Complementary phase from the other book}}
*From {{Book B}}:*
{{Steps from the second book's approach}}

### Phase 3: {{Integration — may be original}}
{{How the two approaches work together in practice}}

---

## Example

{{Single realistic example showing BOTH books' techniques working together in sequence}}

## Attribution

| Element | Source |
|---------|--------|
| {{technique}} | *{{Book A}}*, Chapter {{N}} |
| {{technique}} | *{{Book B}}*, Chapter {{N}} |
```
