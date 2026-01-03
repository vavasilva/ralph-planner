---
description: "Create a structured execution plan based on a GitHub issue"
---

# from-issue

Create a structured execution plan based on a GitHub issue.

## Arguments

- `issue` (required): Issue reference - can be `#123` (current repo) or `owner/repo#123`
- `--type` (optional): Work type template to use (feature, bugfix, refactor, migration, performance)
- `--output` (optional): Path to save the generated plan (e.g., `./plans/my-plan.md`)
- `--include-comments` (optional): Include issue comments in the context

## Instructions

You are a planning assistant. Create a structured plan based on a GitHub issue.

### Step 1: Parse Arguments

Extract from `$ARGUMENTS`:
- `issue`: The issue reference (#123 or owner/repo#123)
- `--type <type>`: (optional) Force specific template
- `--output <path>`: (optional) Save plan to this file
- `--include-comments`: (optional) Include comments

### Step 2: Fetch Issue Data

Use the GitHub CLI to fetch the issue:

**For current repo (#123):**
```bash
gh issue view 123 --json title,body,labels,state,url
```

**For external repo (owner/repo#123):**
```bash
gh issue view 123 --repo owner/repo --json title,body,labels,state,url
```

**If --include-comments:**
```bash
gh issue view 123 --json title,body,labels,state,url,comments
```

If the issue doesn't exist or can't be accessed, inform the user and stop.

### Step 3: Analyze Issue Content

From the issue data, extract:
- **Title**: What is being requested?
- **Body**: Detailed description, requirements, context
- **Labels**: Use for auto-detecting work type
- **Comments**: Additional context (if --include-comments)

### Step 4: Select Template

If `--type` was specified, use that template. Otherwise, auto-detect from labels:

| GitHub Labels | Template |
|---------------|----------|
| `bug`, `bugfix`, `fix`, `defect` | bugfix |
| `enhancement`, `feature`, `new` | feature |
| `refactor`, `tech-debt`, `cleanup`, `improvement` | refactor |
| `migration`, `upgrade`, `database` | migration |
| `performance`, `perf`, `optimization`, `slow` | performance |

If no matching labels, analyze the title and body:

| Content indicators | Template |
|-------------------|----------|
| "add", "implement", "create", "new feature" | feature |
| "fix", "bug", "issue", "broken", "error", "doesn't work" | bugfix |
| "refactor", "restructure", "clean up", "improve code" | refactor |
| "migrate", "move", "upgrade", "convert" | migration |
| "performance", "optimize", "slow", "speed", "latency" | performance |

Default to `feature` if still uncertain.

### Step 5: Generate Plan

Using the selected template, generate a structured plan:

```
## Plan: [Issue Title]

**Source:** [Issue URL]
**Issue:** #[number]
**Template:** [selected template type]
**Labels:** [list of labels]

### Phase 1: [Phase Name from template]
**Tasks:**
- [ ] [Task derived from issue content]
- [ ] ...

**Completion Criteria:** [From template + issue specifics]

[Continue for all phases...]

---

**Total Tasks:** [count]
**Estimated Iterations:** [count × 3]

🏷️ **Promise Tag:** [Verifiable promises from template]

⚠️ **Completion Signal:** When ALL criteria above are met, output:
<promise>COMPLETE</promise>
```

### Step 6: Generate Loop Command

**IMPORTANT:**
1. Always include the DONE condition with verifiable promises
2. Reference the issue number in the summary
3. If `--output` was used, include the **plan file path**

**Format (with --output):**
```
/ralph-wiggum:ralph-loop [iterations] "Implement #[issue] from [plan-path]. DONE when: [criteria]"
```

**Format (without --output):**
```
/ralph-wiggum:ralph-loop [iterations] "Implement #[issue]: [summary]. DONE when: [criteria]"
```

**Examples:**
```
# With --output:
/ralph-wiggum:ralph-loop 42 "Implement #123 from ./plans/issue-123.md. DONE when: all tests pass, feature works"

# Without --output:
/ralph-wiggum:ralph-loop 42 "Implement #123: Add dark mode. DONE when: dark mode toggle works, theme persists"
```

### Step 7: Save Plan (if --output specified)

If `--output <path>` was provided:
1. Create the directory if it doesn't exist
2. Save **ONLY the plan from Step 5** to the file (phases, tasks, criteria, promise tag)
3. **DO NOT save the execution commands to the file** — they go only in chat
4. Confirm: "Plan saved to [path]"

After saving, **display the execution commands in the chat** so the user can copy them.

### Step 8: STOP - Do Not Execute

**CRITICAL:** After completing steps 1-7, you are DONE.

⛔ **DO NOT:**
- Start implementing any tasks
- Run any ralph-loop commands
- Begin coding or making changes
- Execute anything from the plan

✅ **DO:**
- Display the plan summary
- Show the execution commands for the user to copy
- Wait for the user to manually run the commands

The user will copy and run the ralph-loop command themselves when ready.

## Examples

```
# Issue in current repo
/ralph-planner:from-issue "#42"

# Issue in external repo
/ralph-planner:from-issue "vavasilva/my-app#15"

# Force template type
/ralph-planner:from-issue "#42" --type bugfix

# Save plan to file
/ralph-planner:from-issue "#42" --output "./plans/issue-42.md"

# Include comments for more context
/ralph-planner:from-issue "#42" --include-comments

# Full example
/ralph-planner:from-issue "#42" --type feature --output "./plans/feature.md" --include-comments
```

## Label Mapping Reference

| Label Category | Possible Values | Template |
|----------------|-----------------|----------|
| Bugs | bug, bugfix, fix, defect, broken | bugfix |
| Features | enhancement, feature, new, feat | feature |
| Refactoring | refactor, tech-debt, cleanup, code-quality | refactor |
| Migration | migration, upgrade, database, data | migration |
| Performance | performance, perf, optimization, speed | performance |

## Guidelines

- Preserve important details from the issue body
- Map issue requirements to specific tasks
- If issue has acceptance criteria or checkboxes, incorporate them
- Use comments to understand additional context and decisions
- Reference the issue number throughout for traceability
