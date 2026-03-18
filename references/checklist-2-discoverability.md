# Checklist 2: DISCOVERABILITY (9 items)

Focus: Will Claude actually find and trigger this skill at the right moments?

---

### D1: Description exists and is under 1,024 characters
Check: The `description:` field exists in frontmatter and its value is no longer than 1,024 characters (including spaces).
- ✅ Description is present and within character limit
- ❌ Description field is missing entirely, or exceeds 1,024 characters
Evidence: State the character count of the description.
**Severity: Critical** — A missing description means the skill is never triggered. An over-limit description may be truncated, destroying the trigger logic.

---

### D2: Description in "sweet spot" (200–600 characters)
Check: The description is long enough to convey purpose and triggers (at least 200 characters) but short enough to stay scannable and precise (no more than 600 characters).
- ✅ Description clearly states what the skill does and when to use it in 200–600 characters
- ❌ Under 200 chars: too vague to reliably trigger. Over 600 chars: bloated, dilutes key signals
Evidence: State the exact character count and whether it falls in range.
**Severity: Important** — This is a balance check. Both extremes cause problems: too short fails to trigger on edge cases; too long buries the trigger conditions in noise. Note: D1 and D2 work together — D1 is the hard limit, D2 is the quality target.

---

### D3: Description written in third person
Check: The description uses third-person language ("Processes...", "Creates...", "Evaluates...") and not first-person ("I process...", "I can help you...").
- ✅ "Processes PDF files and extracts tables into structured data"
- ❌ "I process PDF files and can extract tables for you"
Evidence: Quote the first sentence or two of the description and note the person used.
**Severity: Critical** — First-person descriptions break how the skill is injected into the system prompt. The agent reads first-person as its own statement, not as a skill descriptor, causing trigger failures.

---

### D4: Description states what the skill does
Check: A reader unfamiliar with the skill can understand its core function from the description alone — without needing to open SKILL.md.
- ✅ "Evaluates the quality of an Agent Skill and returns a structured plain text report with scores, findings, and prioritized fixes"
- ❌ "A skill for reviewing things and giving feedback"
Evidence: Quote the description and assess whether the core function is clear.
**Severity: Critical** — The description is the primary signal Claude uses to decide whether to load this skill. If the function is unclear, the skill is not loaded when it should be.

---

### D5: Description includes when to use it (trigger conditions)
Check: The description includes 2–4 specific conditions or user actions that should trigger the skill. These are phrases or situations that signal the skill is needed — not an exhaustive list, but enough to match the most common trigger cases.
- ✅ "Use when given a parsed skill object... and asked to review, score, grade, evaluate, or rate it."
- ❌ Description only says what the skill does, with no guidance on when to use it
Evidence: Identify the trigger phrases or conditions in the description, or note their absence.
**Severity: Critical** — Without explicit trigger conditions, the skill is under-triggered (missed when it should run) or over-triggered (runs when it shouldn't). Note: Include 2–4 key triggers, not an exhaustive list.

---

### D6: Description includes specific user phrases **(optional — if user-triggered)**
Check: If the skill is intended to be triggered by natural language requests from users, the description includes example phrases a user might say that should cause the skill to load.
- ✅ Description references phrases like "asked to review, score, grade, evaluate, or rate"
- ❌ Description describes the skill but gives no examples of how a user would request it
**Mark N/A if the skill is triggered programmatically or by system context rather than user language.**
Evidence: Quote example phrases if present, or state N/A.
**Severity: Important (if applicable)** — Without example phrases, Claude may fail to trigger the skill when users ask in natural, varied language.

---

### D7: Description mentions file types **(optional — if file-specific)**
Check: If the skill operates on or produces specific file types (.pdf, .docx, .xlsx, .zip, etc.), the description names those file types explicitly.
- ✅ "Generates Word documents (.docx) from user content"
- ❌ "Generates documents from user content" (file type unstated when skill is file-specific)
**Mark N/A if the skill is not file-specific.**
Evidence: Note which file types the skill uses, and whether they appear in the description.
**Severity: Important (if applicable)** — Omitting file types causes the skill to be missed when users mention specific file formats in their requests.

---

### D8: No security issues in frontmatter
Check: The frontmatter does not contain XML angle brackets (`<`, `>`) in any field value, and the `name` field does not contain "claude" or "anthropic" (case-insensitive).
- ✅ Frontmatter values are plain text; name is `pdf-processor` or similar
- ❌ Description contains `<skill>`, `<instructions>`, or similar tags; name is `claude-helper` or `anthropic-tool`
Evidence: Confirm both checks pass, or quote the offending content.
**Severity: Critical** — XML tags in frontmatter can cause prompt injection or parsing failures. Names referencing Claude or Anthropic can create impersonation or trust boundary violations.

---

### D9: No reliance on undocumented frontmatter fields
Check: The frontmatter uses only documented, supported fields. Common undocumented fields to watch for: `version`, `author`, `tags`, `priority`, `enabled`, `category`.
- ✅ Frontmatter contains only `name`, `description`, and other officially documented fields
- ❌ Frontmatter contains `version: 1.2`, `author: Jane`, `tags: [pdf, document]` — these are ignored silently
Evidence: List all frontmatter fields and flag any that are not officially documented.
**Severity: Important** — Undocumented fields are silently ignored. If the skill creator expects them to have an effect (e.g., `priority` affecting trigger order), the skill will not behave as intended.
