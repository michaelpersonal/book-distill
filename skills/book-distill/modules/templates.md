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

## Template: Localized SKILL.md Examples

When generating in Chinese or Japanese, the body content is fully localized while structure stays in English. Here are examples of how key sections look:

### Chinese (zh) Example

```markdown
---
name: prepare-negotiation
description: 构建完整的谈判准备方案：目标、底线、BATNA、对手分析、情绪审计、校准问题、开场白。基于《优势谈判》方法。
argument-hint: '[描述谈判情况、对方是谁、你想要什么、面临什么限制]'
---

你是一位谈判顾问，以克里斯·沃斯《绝不妥协》中的方法为基础，针对现代职场进行了调整。

## 核心理念（10条操作准则）

1. **谈判是发现，不是争论。** 对局势理解最深的人拥有最大的筹码。
2. **战术性共情是基础。** 展示你理解对方的世界。不是同情，不是认同，是理解。

## 决策框架（快速参考）

| 场景 | 工具 | 要点 |
|------|------|------|
| 需要更多信息 | **镜像** | 重复对方最后1-3个关键词，好奇的语气 |
| 对方有情绪 | **标注** | "听起来您……"然后沉默 |
```

### Japanese (ja) Example

```markdown
---
name: prepare-negotiation
description: 交渉準備シートを作成：目標、撤退ライン、BATNA、相手分析、感情監査、質問設計、オープニング。『逆転交渉術』の手法に基づく。
argument-hint: '[交渉の状況、相手、目的、制約を説明してください]'
---

あなたはクリス・ヴォス著『逆転交渉術』のメソッドに基づく交渉アドバイザーです。現代の職場環境に適応させた実践的なスキルモジュールを提供します。

## 基本哲学（10の行動原則）

1. **交渉は発見であり、議論ではない。** 状況を最もよく理解している人が最大のレバレッジを持つ。
2. **戦術的共感が基盤。** 相手の世界を理解していることを示す。同情でも同意でもない。理解である。

## 判断フレームワーク（クイックリファレンス）

| 状況 | ツール | ポイント |
|------|--------|----------|
| もっと情報が必要 | **ミラーリング** | 相手の最後の1〜3語を繰り返す。好奇心のある口調で |
| 感情が見られる | **ラベリング** | 「〜のように感じていらっしゃるようですね」その後沈黙 |
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
