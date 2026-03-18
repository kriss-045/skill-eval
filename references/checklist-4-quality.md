# Checklist 4: QUALITY (12 items)

Focus: Is this GOOD, not just working?

---

### Q1: Built for real, repeated need
Check: The skill addresses a task that will genuinely recur — not a one-off task that should have been a direct prompt or a task so narrow it applies to one project.
- ✅ Task happens regularly across different users, contexts, or inputs
- ❌ Skill was built for a single project's specific setup and is unlikely to be reused
Evidence: Assess whether the skill's purpose suggests repeated, varied use or a one-time task.
**Severity: Important** — Skills built for one-time tasks create maintenance burden and catalog noise without delivering recurring value.

---

### Q2: Instructions are clear and unambiguous
Check: Every instruction has one obvious interpretation. There are no phrases that a reasonable person could interpret in two different ways.
- ✅ "If the description exceeds 600 characters, mark D2 as FAIL" — one interpretation
- ❌ "Make sure the description is a good length" — completely ambiguous
Evidence: Identify any ambiguous instructions, or confirm clarity.
**Severity: Important** — Ambiguous instructions produce inconsistent results across runs. The agent will interpret them differently each time, defeating the purpose of a skill.

---

### Q3: Professional tone (not chatty or verbose)
Check: The instructions are written in a direct, professional style. No filler phrases, no conversational asides, no unnecessary encouragement.
- ✅ "Evaluate each item against the skill content. Record failures with specific location references."
- ❌ "Great! Now let's move on to the next step, which is really important — you'll want to make sure you carefully..."
Evidence: Note any instances of chatty or verbose language, or confirm professional tone.
**Severity: Quality** — Verbose instructions increase token consumption and dilute the signal. Chatty language causes agents to treat style as substance.

---

### Q4: No unnecessary human-facing documentation in skill folder
Check: The skill folder does not contain files intended for human readers that serve no function for the agent — changelogs, contribution guides, development notes, roadmap files.
- ✅ Only SKILL.md, reference files, scripts, and assets that the agent uses are present
- ❌ `CHANGELOG.md`, `CONTRIBUTING.md`, `dev-notes.txt`, or `TODO.md` present in skill folder
Evidence: List all files in the skill folder and flag any that appear human-facing.
**Severity: Quality** — Human-facing files add noise to the skill folder. The agent may attempt to read them as instructions, producing unexpected behavior.

---

### Q5: SKILL.md length is appropriate (<500 lines ideal)
Check: SKILL.md is under 500 lines. Longer files are a signal that content should be moved to reference files or the skill scope is too broad.
- ✅ SKILL.md is focused and under 500 lines
- ❌ SKILL.md is 800+ lines, suggesting monolithic structure or scope creep
Evidence: State the line count of SKILL.md.
**Severity: Important** — Excessively long SKILL.md files degrade agent attention. The agent is more likely to skip or misread instructions that appear deep in a long document.

---

### Q6: Instructions match actual capability
Check: The skill does not instruct the agent to do things that are impossible or unreliable — such as accessing URLs that weren't provided, calling APIs without credentials, or performing real-time lookups from memory.
- ✅ All instructions are within the agent's actual capability given the context and tools available
- ❌ "Search the web for the latest version" (if web search is not enabled); "Remember what the user said last session" (impossible)
Evidence: Identify any instructions that exceed the agent's realistic capability, or confirm alignment.
**Severity: Important** — Instructions that exceed capability will either be silently skipped or result in hallucinated output as the agent improvises.

---

### Q7: Terminology is consistent throughout
Check: The skill uses the same term for the same concept throughout — it does not alternate between "skill", "agent skill", and "plugin" to mean the same thing, or use "evaluate" and "assess" interchangeably without defining a distinction.
- ✅ Key terms are used consistently from first mention to last
- ❌ "Document" in section 1 becomes "file" in section 2 and "artifact" in section 3, referring to the same thing
Evidence: Note any terminology inconsistencies found, or confirm consistency.
**Severity: Quality** — Inconsistent terminology causes the agent to treat the same concept as distinct, leading to gaps in coverage or duplication of effort.

---

### Q8: Instructions are appropriately detailed
Check: Instructions provide enough detail to execute correctly without requiring the agent to make significant judgment calls — but not so detailed that they become rigid scripts that break on variation.
- ✅ Enough detail to produce consistent output; enough flexibility to handle input variation
- ❌ Too sparse: "Evaluate the skill and produce a report." Too rigid: Every micro-decision is prescribed, leaving no room for the input to vary.
Evidence: Assess the level of detail and whether it strikes the right balance.
**Severity: Important** — Under-detailed skills produce wildly inconsistent output. Over-detailed skills fail on any input that differs from the exact scenario they describe.

---

### Q9: Reference files are well-organized **(optional — if reference files exist)**
Check: Reference files use clear headings, consistent formatting, and logical section order. A reader can navigate them without reading every word.
- ✅ Clear headings, logical flow, consistent formatting across files
- ❌ Reference file is a wall of text, or uses inconsistent heading levels and formatting
**Mark N/A if no reference files exist.**
Evidence: Describe the organization of reference files, or state N/A.
**Severity: Quality (if applicable)** — Poorly organized reference files slow down the agent and increase the chance that relevant content is missed.

---

### Q10: Skill solves one clear problem (not multiple unrelated tasks)
Check: The skill has a single, clearly defined purpose. If the skill description requires "and also" to explain its scope, it may be doing too much.
- ✅ Skill evaluates agent skills — one clear function
- ❌ Skill evaluates agent skills AND generates new skills AND updates existing ones AND tracks versions
Evidence: Assess whether the skill's purpose is singular and coherent.
**Severity: Important** — Skills with multiple unrelated functions are harder to trigger correctly, harder to maintain, and produce less consistent output because the agent must decide which function applies.

---

### Q11: No obvious copy-paste errors or inconsistencies
Check: The skill does not contain leftover placeholder text, instructions from a different skill, mismatched examples, or references to concepts not defined in this skill.
- ✅ All content is coherent and relevant to this skill's purpose
- ❌ "Replace this with your checklist items", outdated item IDs, examples referencing a different skill's domain
Evidence: Note any copy-paste artifacts or inconsistencies found, or confirm clean.
**Severity: Quality** — Copy-paste errors undermine trust in the skill's instructions and confuse the agent about what the actual requirements are.

---

### Q12: Context is provided where needed
Check: Instructions provide sufficient background for the agent to understand the domain — especially for specialized or technical topics where assumptions about agent knowledge should not be made.
- ✅ Key concepts, acronyms, and domain terms are defined or explained on first use
- ❌ Instructions assume the agent knows specialized terms or domain conventions without introducing them
Evidence: Identify any concepts that are used without context, or confirm adequate setup.
**Severity: Quality** — Missing context forces the agent to rely on training data assumptions, which may be incorrect or inconsistent with the skill's intended domain-specific behavior.
