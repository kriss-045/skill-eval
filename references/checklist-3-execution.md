# Checklist 3: EXECUTION (12 items)

Focus: Will it work correctly once triggered?

---

### E1: Instructions explain WHY, not just WHAT
Check: The skill body does not only list steps or rules — it explains the reasoning behind key decisions. An agent following this skill should understand why a step is taken, not just that it is required.
- ✅ "Check for missing fields before processing — if fields are absent, later steps will fail silently and produce incorrect output."
- ❌ "Check for missing fields. Then process the input. Then generate output." (no reasoning provided)
Evidence: Quote one rule or step that includes reasoning, and one (if any) that is bare instruction.
**Severity: Important** — Instructions without reasoning are brittle. When the agent encounters an edge case the instruction does not cover, it has no basis for judgment and will guess or fail.

---

### E2: Avoids excessive ALWAYS/NEVER caps
Check: The skill does not overuse capitalized directives (ALWAYS, NEVER, MUST, DO NOT). These add emphasis but reduce nuance. More than 5–7 uses across the entire SKILL.md suggests the skill is over-constrained.
- ✅ Rare use of caps for genuinely non-negotiable constraints
- ❌ Every other instruction is phrased as "ALWAYS do X" or "NEVER do Y" — the agent cannot prioritize or exercise judgment
Evidence: Count the number of ALWAYS/NEVER/MUST/DO NOT occurrences.
**Severity: Important** — Over-constrained skills make the agent rigid and prone to failure when instructions conflict with real inputs. Caps should be reserved for true showstoppers.

---

### E3: Includes examples (if instructions are non-trivial) **(optional — if instructions are complex)**
Check: If the skill performs a non-trivial task (judgment calls, structured output, multi-step workflows), it includes at least one worked example that shows input → process → output.
- ✅ Shows a sample input and the expected output format, or walks through a step with a concrete case
- ❌ Instructions describe a complex process but provide no examples of what correct output looks like
**Mark N/A if the skill is simple enough that examples would be redundant (e.g., a single-step lookup).**
Evidence: Describe any examples present, or state N/A.
**Severity: Important (if applicable)** — Without examples, agents interpret ambiguous instructions differently on each run, producing inconsistent output.

---

### E4: Examples match instructions (not overfitted)
Check: If examples are present, they accurately illustrate the instructions without being so specific that the agent treats only those exact cases as valid inputs.
- ✅ Example shows the pattern, not just one specific instance; other inputs would clearly be handled the same way
- ❌ Example is so narrow (one specific file name, one specific user name) that the agent treats only that case correctly
Evidence: Assess whether examples generalize to typical real inputs.
**Severity: Important** — Overfitted examples cause the agent to fail on inputs that differ even slightly from the example, which is most real inputs.

---

### E5: Clear output format specified **(optional — if structured output expected)**
Check: If the skill is expected to produce structured output (a report, a table, a JSON object, a specific document format), the output format is explicitly defined in the instructions.
- ✅ Provides a template or describes the exact fields, sections, and order of the output
- ❌ Instructions say "generate a report" but do not define what sections a report must contain
**Mark N/A if the skill's output is free-form prose where format is intentionally flexible.**
Evidence: Describe the output format specification, or state N/A.
**Severity: Important (if applicable)** — Undefined output format leads to inconsistent structure across runs, making output hard to use downstream.

---

### E6: Error handling guidance provided
Check: The instructions tell the agent what to do when something goes wrong — missing input, unexpected values, tool failures, ambiguous cases.
- ✅ "If the input file cannot be read, note the error in findings and continue with what is available."
- ❌ Instructions assume all inputs arrive correctly and provide no guidance on failures
Evidence: Describe the error handling instructions present, or note their absence.
**Severity: Important** — Skills without error handling silently fail, guess, or halt on edge cases that occur regularly in real use.

---

### E7: Edge cases addressed
Check: The instructions anticipate at least the most common edge cases for this skill's domain. These are inputs or conditions that differ from the happy path but are not rare.
- ✅ "If the skill has no reference files, assess whether the SKILL.md body is appropriately self-contained or bloated."
- ❌ Instructions only describe the ideal-case flow; no mention of what happens when inputs vary
Evidence: List edge cases addressed, or note their absence.
**Severity: Important** — Unaddressed edge cases are gaps the agent will fill with guesswork, producing inconsistent or incorrect results.

---

### E8: Progressive disclosure implemented **(optional — if reference files exist)**
Check: If the skill has reference files, SKILL.md does not reproduce their content inline. Instead, SKILL.md directs the agent to read specific reference files at the appropriate point in the workflow.
- ✅ "Read references/checklist-1-basics.md in full before evaluating basics."
- ❌ Reference file content is copy-pasted into SKILL.md, making the main file bloated
**Mark N/A if the skill has no reference files.**
Evidence: Confirm that reference files are referenced (not reproduced) in SKILL.md, or state N/A.
**Severity: Important (if applicable)** — Reproducing reference content in SKILL.md makes the file excessively long, which degrades agent attention and increases the chance of instructions being skipped.

---

### E9: Reference files have TOCs (if >100 lines) **(optional — if reference files exist and are long)**
Check: If any reference file exceeds 100 lines, it begins with a table of contents that allows the agent to navigate to relevant sections.
- ✅ Long reference file opens with a list of sections and their heading names
- ❌ 200-line reference file begins immediately with content, no navigation aid
**Mark N/A if no reference files exist, or if all reference files are under 100 lines.**
Evidence: Check length of each reference file and whether TOCs are present where needed.
**Severity: Quality (if applicable)** — Without a TOC, agents reading long reference files may miss later sections or lose track of structure, especially in complex multi-section documents.

---

### E10: Scripts are documented **(optional — if scripts exist)**
Check: If the skill includes scripts, each script has inline comments or an accompanying description explaining what it does, what inputs it expects, and what it outputs.
- ✅ Script opens with a comment block describing purpose, inputs, and outputs; key logic blocks are annotated
- ❌ Script file contains bare code with no comments
**Mark N/A if no scripts exist.**
Evidence: Describe the documentation level of scripts present, or state N/A.
**Severity: Important (if applicable)** — Undocumented scripts cannot be safely maintained, modified, or verified by the agent or human reviewers.

---

### E11: Not everything embedded in SKILL.md
Check: SKILL.md is not a monolithic file containing all content — long reference material, lookup tables, and detailed guides are in separate reference files, not inlined.
- ✅ SKILL.md is focused on orchestration and workflow; detailed content is in references/
- ❌ SKILL.md contains full lookup tables, multi-page guides, or content that would naturally belong in a reference file
Evidence: Assess whether SKILL.md length and content suggest inappropriate monolithic structure.
**Severity: Important** — An overstuffed SKILL.md degrades agent performance. The agent's attention window is finite; burying workflow instructions in long documents causes instructions to be missed or deprioritized.

---

### E12: Instructions are generalizable (not overfitted)
Check: The instructions work correctly for the full range of inputs the skill is intended to handle — not just the specific examples used during development.
- ✅ Instructions describe patterns and principles that apply across varied inputs
- ❌ Instructions reference specific file names, user names, or scenarios that only apply to test cases
Evidence: Identify any instructions that appear tied to specific test cases rather than general patterns.
**Severity: Critical** — Overfitted instructions produce correct results only for the examples they were written around. Real inputs will fail in non-obvious ways.
