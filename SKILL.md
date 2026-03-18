---
name: skill-reviewer-eval
description: Evaluates the quality of an Agent Skill and returns a structured plain text report with scores, findings, and prioritized fixes. Use when given a parsed skill object (frontmatter, body, reference files, script files, folder structure) and asked to review, score, grade, evaluate, or rate it. Also triggers when a user uploads a skill folder or zip file and asks for feedback, thoughts, impressions, or whether the skill is good — regardless of whether they use the words evaluate, score, or review. Does not evaluate prompt quality, system prompts, or non-skill AI configurations.
---

# Agent Skill Evaluator

Evaluates Agent Skills across 59 items in 6 categories, producing a structured plain text report with scores, findings, and prioritized fixes.

Every item must be evaluated. Every finding must reference a specific location in the skill — file name, field name, or line reference. Vague findings ("the skill lacks X") are not acceptable ("Field `description` in frontmatter is 847 characters — exceeds the 600-character sweet spot defined in D2" is the standard).

---

## Step 0 — Initialize

Before evaluating anything:

1. Confirm with the user that 59 items across 6 categories will be evaluated.
2. Identify what skill material has been provided: folder structure, SKILL.md content, reference files, scripts, assets.
3. Note any missing material explicitly — do not fabricate content to evaluate.
4. State: "Beginning evaluation. 59 items across 6 categories."

Do not proceed to Step 1 until initialization is complete.

---

## Step 1 — BASICS (8 items)

Read `references/checklist-1-basics.md` in full.

Evaluate every item (B1 through B8) against the skill. For each item:
- State the item ID
- State PASS, FAIL, or N/A
- Provide specific evidence — quote the relevant content or state the specific finding

After evaluating all 8 items, output:

```
Items evaluated: B1, B2, B3, B4, B5, B6, B7, B8
BASICS: 8/8 items checked ✓
Category Score: X/Y passed (where Y = applicable items, excluding N/A)
```

**Checkpoint:** Confirm that all 8 item IDs (B1–B8) appear in your output before proceeding. If any are missing, re-evaluate that item before continuing.

---

## Step 2 — DISCOVERABILITY (9 items)

Read `references/checklist-2-discoverability.md` in full.

Evaluate every item (D1 through D9) against the skill. For each item:
- State the item ID
- State PASS, FAIL, or N/A
- Provide specific evidence — quote the relevant content or state the specific finding

After evaluating all 9 items, output:

```
Items evaluated: D1, D2, D3, D4, D5, D6, D7, D8, D9
DISCOVERABILITY: 9/9 items checked ✓
Category Score: X/Y passed (where Y = applicable items, excluding N/A)
```

**Checkpoint:** Confirm that all 9 item IDs (D1–D9) appear in your output before proceeding. If any are missing, re-evaluate that item before continuing.

---

## Step 3 — EXECUTION (12 items)

Read `references/checklist-3-execution.md` in full.

Evaluate every item (E1 through E12) against the skill. For each item:
- State the item ID
- State PASS, FAIL, or N/A
- Provide specific evidence — quote the relevant content or state the specific finding

After evaluating all 12 items, output:

```
Items evaluated: E1, E2, E3, E4, E5, E6, E7, E8, E9, E10, E11, E12
EXECUTION: 12/12 items checked ✓
Category Score: X/Y passed (where Y = applicable items, excluding N/A)
```

**Checkpoint:** Confirm that all 12 item IDs (E1–E12) appear in your output before proceeding. If any are missing, re-evaluate that item before continuing.

---

## Step 4 — QUALITY (12 items)

Read `references/checklist-4-quality.md` in full.

Evaluate every item (Q1 through Q12) against the skill. For each item:
- State the item ID
- State PASS, FAIL, or N/A
- Provide specific evidence — quote the relevant content or state the specific finding

After evaluating all 12 items, output:

```
Items evaluated: Q1, Q2, Q3, Q4, Q5, Q6, Q7, Q8, Q9, Q10, Q11, Q12
QUALITY: 12/12 items checked ✓
Category Score: X/Y passed (where Y = applicable items, excluding N/A)
```

**Checkpoint:** Confirm that all 12 item IDs (Q1–Q12) appear in your output before proceeding. If any are missing, re-evaluate that item before continuing.

---

## Step 5 — SAFETY (8 items)

Read `references/checklist-5-safety.md` in full.

S1 and S2 are universal — always evaluate them. S3 through S8 are optional — mark N/A if the condition does not apply (no scripts, no network activity, no data access, no file manipulation, no destructive operations, no defined error messages).

Evaluate every item (S1 through S8) against the skill. For each item:
- State the item ID
- State PASS, FAIL, or N/A
- Provide specific evidence — quote the relevant content or state the specific finding

After evaluating all 8 items, output:

```
Items evaluated: S1, S2, S3, S4, S5, S6, S7, S8
SAFETY: 8/8 items checked ✓
Category Score: X/Y passed (where Y = applicable items, excluding N/A)
```

**Scoring note:** If only S1 and S2 are applicable (all others are N/A), report "Category Score: 2/2 passed" — N/A items are excluded from the denominator.

**Checkpoint:** Confirm that all 8 item IDs (S1–S8) appear in your output before proceeding. If any are missing, re-evaluate that item before continuing.

---

## Step 6 — CONSISTENCY (10 items)

Read `references/checklist-6-consistency.md` in full.

Evaluate every item (C1 through C10) against the skill. For each item:
- State the item ID
- State PASS, FAIL, or N/A
- Provide specific evidence — quote the relevant content or state the specific finding

Note: C7 references the same description length check as D2. If D2 was already evaluated, note the finding here without re-analyzing — state whether the consistency impact was identified.

After evaluating all 10 items, output:

```
Items evaluated: C1, C2, C3, C4, C5, C6, C7, C8, C9, C10
CONSISTENCY: 10/10 items checked ✓
Category Score: X/Y passed (where Y = applicable items, excluding N/A)
```

**Checkpoint:** Confirm that all 10 item IDs (C1–C10) appear in your output before proceeding. If any are missing, re-evaluate that item before continuing.

---

## Step 7 — Final Verification and Report

Before producing the final report:

1. Confirm all 6 completion markers are present:
   - BASICS: 8/8 items checked ✓
   - DISCOVERABILITY: 9/9 items checked ✓
   - EXECUTION: 12/12 items checked ✓
   - QUALITY: 12/12 items checked ✓
   - SAFETY: 8/8 items checked ✓
   - CONSISTENCY: 10/10 items checked ✓

2. Confirm total items evaluated: 59/59.

3. If any category marker is missing, stop and re-evaluate that category before proceeding.

4. Produce the final report using the template below.

---

## Output Format

Use this exact template. Output must be plain text — no markdown formatting (no #, **, __, >, or backticks). Use only the structural elements shown below.

```
================================================================================
                        AGENT SKILL EVALUATION REPORT
================================================================================

Skill Name: [name from frontmatter, or "Unknown" if missing]
Evaluated: [today's date]
Total Items Evaluated: 59/59 ✓

--------------------------------------------------------------------------------
SUMMARY BY CATEGORY
--------------------------------------------------------------------------------

  BASICS:          X/8 passed    [8/8 items checked]
  DISCOVERABILITY: X/9 passed    [9/9 items checked]
  EXECUTION:       X/12 passed   [12/12 items checked]
  QUALITY:         X/12 passed   [12/12 items checked]
  SAFETY:          X/Y passed    [8/8 items checked]  (Y = applicable items only)
  CONSISTENCY:     X/10 passed   [10/10 items checked]

OVERALL SCORE: XX/59 items passed (XX%)

--------------------------------------------------------------------------------
CRITICAL ISSUES (Must Fix)
--------------------------------------------------------------------------------

[List every FAIL item marked Critical severity, with specific location and finding.
If none, write: No critical issues found.]

--------------------------------------------------------------------------------
WARNINGS (Should Fix)
--------------------------------------------------------------------------------

[List every FAIL item marked Important severity, with specific location and finding.
If none, write: No warnings.]

--------------------------------------------------------------------------------
STRENGTHS
--------------------------------------------------------------------------------

[List notable things this skill does well — specific, not generic.
"Instructions are clear" is not acceptable. "The progressive disclosure structure in Steps 1–3 prevents SKILL.md bloat by routing all checklist content to reference files" is the standard.
If nothing notable, write: No notable strengths identified.]

--------------------------------------------------------------------------------
PRIORITIZED FIX LIST
--------------------------------------------------------------------------------

Priority 1 (Critical — Fix First):
[List all Critical FAIL items with specific fix instructions]

Priority 2 (Important — Fix Soon):
[List all Important FAIL items with specific fix instructions]

Priority 3 (Nice to Have):
[List all Quality FAIL items with specific fix instructions]

--------------------------------------------------------------------------------
OVERALL ASSESSMENT
--------------------------------------------------------------------------------

[PASS / PASS WITH WARNINGS / FAIL]

Reasoning: [1–2 sentences. Name the specific mechanism that makes this skill pass or fail — not "the skill has some issues" but "the overfitted instructions in E12 and the contradictory rules in C8 mean the skill will produce inconsistent output on any input that is not the exact test case used during development."]

Recommendation: [Choose one: Deploy as-is / Fix warnings then deploy / Critical fixes required before deployment]

================================================================================
```

---

## Assessment Thresholds

PASS: All Critical items pass, and fewer than 3 Important items fail.
PASS WITH WARNINGS: All Critical items pass, but 3 or more Important items fail.
FAIL: Any Critical item fails.

---

## Anti-Skip Protocol

This evaluation contains 59 items. Skipping items is a failure of the evaluation — a skipped item is an undetected problem.

If at any point a category checkpoint fails (item IDs are missing from output), stop immediately. Re-read the checklist for that category and re-evaluate. Do not proceed to the next category until the checkpoint passes.

The final verification in Step 7 is mandatory. Produce the final report only after all 6 category markers are confirmed.

---

## Evidence Standard

Every PASS, FAIL, and N/A must be supported by specific evidence:

UNACCEPTABLE: [B1] FAIL — The folder name is wrong.
REQUIRED: [B1] FAIL — Folder name is `PDF_Processor` — contains uppercase letters and an underscore. Must be fully lowercase kebab-case (e.g., `pdf-processor`).

UNACCEPTABLE: [D2] PASS — The description is a good length.
REQUIRED: [D2] PASS — Description is 347 characters, within the 200–600 character sweet spot.

UNACCEPTABLE: [S3] N/A — No scripts.
REQUIRED: [S3] N/A — No scripts/ directory found. No script files present at any level of the skill folder.

Generic findings are not acceptable. Every finding must answer: where exactly is the issue, and what is the specific observation?
