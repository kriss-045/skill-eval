# Checklist 6: CONSISTENCY (10 items)

Focus: What causes execution variance and unreliability across runs?

---

### C1: SKILL.md length is reasonable (<500 lines ideal)
Check: SKILL.md is under 500 lines. If it exceeds this, assess whether the additional length is justified by genuine complexity, or whether content should be moved to reference files.
- ✅ SKILL.md is focused and self-contained; long content is in reference files
- ❌ SKILL.md is 600+ lines with content that should be in references/
Evidence: State the line count and whether excess length is justified or a structural problem.
**Severity: Important** — Long SKILL.md files cause the agent to lose track of instructions. Key workflow steps buried deep in the document are more frequently skipped or misread. This is one of the primary causes of inconsistent skill execution.

---

### C2: Reference files are used appropriately
Check: Reference files contain reference material (checklists, lookup tables, detailed guides) — not workflow instructions. Workflow logic lives in SKILL.md; content lives in reference files.
- ✅ SKILL.md has the workflow; references/ has detailed content the workflow points to
- ❌ Reference file contains "Step 1: Do X, Step 2: Do Y" workflow logic that belongs in SKILL.md
Evidence: Assess whether the split between SKILL.md and reference files respects the workflow/content boundary.
**Severity: Important** — When workflow logic is scattered across SKILL.md and reference files, the agent loses the thread of execution. Consistent skill behavior requires a single authoritative workflow location.

---

### C3: Not too many rigid rules (<5–7 ALWAYS/NEVER commands)
Check: Count the total number of ALWAYS, NEVER, MUST, and DO NOT commands across SKILL.md. More than 5–7 suggests over-constraining.
- ✅ Fewer than 7 capitalized directives; most instructions allow for appropriate judgment
- ❌ 15+ ALWAYS/NEVER commands — the agent must memorize and apply too many rigid constraints simultaneously
Evidence: Count and list the capitalized directives found.
**Severity: Important** — Too many rigid rules create instruction conflicts. When constraints clash on a real input, the agent cannot resolve them consistently. The result is unpredictable behavior across runs.

---

### C4: Instructions are generalizable (not overfitted to examples)
Check: Instructions describe general patterns, not specific instances. If the skill's instructions would only work correctly for the exact examples used during development, they are overfitted.
- ✅ "For each checklist item, record PASS, FAIL, or N/A based on whether the condition is met."
- ❌ "For item B1, check if the folder is named 'pdf-processor' — if so, mark PASS."
Evidence: Identify any instructions that appear to describe specific test cases rather than general rules.
**Severity: Critical** — Overfitted instructions produce correct results only for the examples they were written around. All other inputs produce inconsistent or incorrect output. This is the most common source of poor skill generalization.

---

### C5: Examples match the generalized instructions
Check: Any examples in the skill accurately illustrate what the instructions say — they are not edge cases, exceptions, or the only cases where the instructions happen to work.
- ✅ Example shows the standard case; the instructions clearly generalize from it
- ❌ Example is an unusual case that required special handling; typical inputs would not be handled by the same logic
Evidence: For each example, assess whether a typical input would be handled correctly by the same instructions.
**Severity: Important** — Mismatched examples and instructions cause the agent to follow the example rather than the instruction, since concrete examples often outweigh abstract rules in agent interpretation.

---

### C6: Output format is consistently specified
Check: If the skill produces structured output, the output format is defined once and applied consistently. The skill does not describe one format in the instructions and show a different format in examples.
- ✅ Output template is defined clearly and examples follow it exactly
- ❌ Instructions say "produce a numbered list" but examples show a bulleted list; or instructions show one template and the example shows a different one
Evidence: Compare the specified output format against any examples to confirm they match.
**Severity: Important** — Output format inconsistency causes the agent to alternate between formats across runs. Downstream consumers of the skill's output cannot rely on consistent structure.

---

### C7: Description length is balanced (200–600 characters sweet spot)
Check: The description is in the 200–600 character range — same check as D2, evaluated here for its impact on consistency. Descriptions outside this range cause over-triggering or under-triggering, both of which produce inconsistent skill invocation.
- ✅ Description is 200–600 characters
- ❌ Under 200: skill is missed on variant trigger phrases. Over 600: key trigger signals are diluted by noise.
Evidence: State the character count. Reference D2 if already evaluated — no need to re-analyze, just note whether the consistency impact was identified.
**Severity: Important** — Inconsistent triggering means the skill runs on some inputs that should trigger it but not others, making it unreliable from the user's perspective even when the instructions themselves are correct.
Note: This item references D2 — the description balance check from Discoverability. Both matter, for different reasons.

---

### C8: No contradictory instructions
Check: No two instructions in the skill contradict each other. If a later instruction overrides an earlier one, the override is explicit and clear.
- ✅ Instructions are internally coherent; no two rules require opposite actions in the same situation
- ❌ "Always include an executive summary" in section 2, "Do not include a summary if the report is short" in section 4, with no definition of "short"
Evidence: Identify any contradictions found, or confirm internal consistency.
**Severity: Critical** — Contradictory instructions cause the agent to pick whichever it encountered last (or most recently in context), producing different behavior across runs depending on which instruction is more salient.

---

### C9: Error handling is defined (not left to agent judgment)
Check: When errors or unexpected conditions occur, the instructions tell the agent exactly what to do — not "handle appropriately" or "use your judgment." Consistent error handling requires explicit instructions.
- ✅ "If the input file is missing, output: 'No skill files found to evaluate.' and stop."
- ❌ "Handle any errors that come up gracefully." (agent defines 'graceful' differently each time)
Evidence: Describe the error handling instructions present, and assess their specificity.
**Severity: Important** — Vague error handling is one of the primary sources of inconsistency. Two runs that hit the same error will produce different output if the agent is left to decide what "handle it" means.

---

### C10: Terminology is consistent throughout
Check: Same check as Q7, evaluated here for its impact on consistency. Key terms are used identically across SKILL.md and all reference files. No alternation between synonyms for the same concept.
- ✅ "checklist item" is always "checklist item" — never "check", "criterion", "rule", or "evaluation point"
- ❌ "checklist item" in SKILL.md becomes "criterion" in one reference file and "check" in another
Evidence: Identify any terminology inconsistencies across files, or confirm consistency.
**Severity: Quality** — Terminology drift across files causes the agent to treat the same concept as distinct, leading to missed coverage, duplication, or gaps in execution that appear randomly across runs.
