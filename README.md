# skill-eval

A Claude agent skill that evaluates and scores other Claude skills. Give it a skill folder and it returns a structured report with scores, findings, and prioritized fixes.

## Install

```bash
npx skills add kriss-045/skill-eval
```

## What it does

Most skill evaluations fail the same way: the evaluator sees correct naming and detailed content and concludes the skill is good. Structure is not quality. The only thing that matters is whether an agent following the skill would reliably produce correct, consistent results across the full range of inputs it encounters in practice.

This skill applies a two-step sequential evaluation to avoid that failure mode:

1. **Structural & Functional Assessment** — does this skill work?
2. **Excellence Assessment** — does this skill work *well*?

The output is a plain text report you can read, share, or act on directly.

## Scoring

| Tier | Dimension | Weight |
|------|-----------|--------|
| Tier 1: Baseline | Hygiene pass/fail | 10% |
| Tier 2: Functional | Instruction Completeness | 20% |
| Tier 2: Functional | Workflow Clarity | 20% |
| Tier 2: Functional | Trigger Reliability | 20% |
| Tier 3: Excellence | WHY Explanations | 15% |
| Tier 3: Excellence | Generalization | 10% |
| Tier 3: Excellence | Depth of Expertise | 5% |

**Score labels:** 0–40 Needs Work · 41–55 Getting There · 56–70 Adequate · 71–84 Good · 85–93 Strong · 94–100 Excellent

Most skills score between 50 and 75. A high score requires genuinely earning it against the rubric.

## Reference checklists

The `references/` folder contains six evaluation checklists applied during the review:

| File | Focus |
|------|-------|
| `checklist-1-basics.md` | File structure, naming conventions, YAML frontmatter validity |
| `checklist-2-discoverability.md` | Whether Claude will trigger the skill at the right moments |
| `checklist-3-execution.md` | Whether following the instructions produces consistent, correct output |
| `checklist-4-quality.md` | Whether instructions are precise enough to avoid guessing |
| `checklist-5-safety.md` | Edge case handling, bad input resilience, failure modes |
| `checklist-6-consistency.md` | Whether the skill produces the same result across repeated runs |

## Output format

The skill produces a plain text report in this structure:

```
================================================================================
                        AGENT SKILL EVALUATION REPORT
================================================================================

Skill Name: your-skill
Evaluated: [date]
Total Items Evaluated: 59/59 ✓

SUMMARY BY CATEGORY
  BASICS:          X/8 passed
  DISCOVERABILITY: X/9 passed
  EXECUTION:       X/12 passed
  QUALITY:         X/12 passed
  SAFETY:          X/Y passed
  CONSISTENCY:     X/10 passed

OVERALL SCORE: XX/59 items passed (XX%)

CRITICAL ISSUES / WARNINGS / STRENGTHS / PRIORITIZED FIX LIST / OVERALL ASSESSMENT
================================================================================
```

Every finding names the exact location of the gap. Every fix names exactly what to add or change.

## Usage

Ask Claude to review, score, evaluate, or rate any skill:

> "Review this skill and give me a score"
> "Evaluate the quality of this skill folder"
> "What score would this skill get?"

The skill triggers automatically when it detects a skill object and an evaluation request.
