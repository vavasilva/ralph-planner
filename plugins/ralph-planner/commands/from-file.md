---
description: "Create a structured execution plan based on an existing markdown file"
---

# from-file

Create a structured execution plan based on an existing markdown file.

## Arguments

- `file_path` (required): Path to the markdown file containing the task/feature description
- `--type` (optional): Work type template to use (feature, bugfix, refactor, migration, performance)
- `--output` (optional): Path to save the generated plan (e.g., `./plans/my-plan.md`)

## Instructions

You are a planning assistant. Create a structured plan based on the content of a file.

### Step 1: Read the File

Read the file at the specified path: `$ARGUMENTS`

Extract parameters from arguments:
- `file_path`: The path to the source file
- `--type <type>`: (optional) Use specific template
- `--output <path>`: (optional) Save plan to this file

If no type specified, analyze the content to determine the best template.

### Step 2: Analyze Content

Read and understand the file content. Look for:
- What is being requested/described?
- What is the scope and complexity?
- Are there acceptance criteria or requirements listed?
- What type of work is this? (feature, bugfix, refactor, migration, performance)

### Step 3: Select Template

If `--type` was specified, use that template. Otherwise, auto-detect:

| Content indicators | Template |
|-------------------|----------|
| "add", "implement", "create", "new feature" | feature |
| "fix", "bug", "issue", "broken", "error" | bugfix |
| "refactor", "restructure", "clean up", "improve code" | refactor |
| "migrate", "move", "upgrade", "convert" | migration |
| "performance", "optimize", "slow", "speed", "latency" | performance |

### Step 4: Generate Plan

Using the selected template, generate a structured plan that:
1. Uses the **phases** from the template
2. Creates **specific tasks** based on the file content
3. Includes **verifiable promises** from the template
4. Incorporates any requirements/criteria from the file

Output format:
```
## Plan: [Title derived from file content]

**Source:** [file path]
**Template:** [selected template type]

### Phase 1: [Phase Name from template]
**Tasks:**
- [ ] [Task derived from file content]
- [ ] ...

**Completion Criteria:** [From template + file specifics]

[Continue for all phases...]

---

**Total Tasks:** [count]
**Estimated Iterations:** [count × 3]

🏷️ **Promise Tag:** [Verifiable promises from template]
```

### Step 5: Generate Loop Command

**IMPORTANT:**
1. Always include the DONE condition with verifiable promises
2. If `--output` was used, include the **plan file path** so ralph-loop knows where to find it

**Format (with --output):**
```
/ralph-wiggum:ralph-loop [iterations] "Implement [summary] from [plan-path]. DONE when: [criteria]"
```

**Format (without --output):**
```
/ralph-wiggum:ralph-loop [iterations] "[summary]. DONE when: [criteria]"
```

**Examples:**
```
# With --output (includes plan path):
/ralph-wiggum:ralph-loop 42 "Implement auth features from ./plans/auth-plan.md. DONE when: login works, tests pass"

# Without --output:
/ralph-wiggum:ralph-loop 42 "Implement auth features. DONE when: login works, tests pass"
```

If the plan has multiple phases, generate a command for each:
```
# Phase 1 (recommended start):
/ralph-wiggum:ralph-loop [phase1 iterations] "Implement Phase 1 from [plan-path]. DONE when: [phase1 criteria]"

# All phases:
/ralph-wiggum:ralph-loop [total iterations] "Implement all from [plan-path]. DONE when: [all key criteria]"
```

### Step 6: Save Plan (if --output specified)

If `--output <path>` was provided:
1. Create the directory if it doesn't exist
2. Save **ONLY the plan from Step 4** to the file (phases, tasks, criteria, promise tag)
3. **DO NOT save the execution commands (Step 5) to the file** — they go only in chat
4. Confirm: "Plan saved to [path]"

**Why?** The execution commands are for the USER to copy/run. If saved in the plan file, ralph-loop might misinterpret them as tasks to execute.

After saving, **display the execution commands in the chat** so the user can copy them.

### Step 7: STOP - Do Not Execute

**CRITICAL:** After completing steps 1-6, you are DONE.

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
/ralph-planner:from-file "./docs/auth-feature.md"
/ralph-planner:from-file "./issues/bug-123.md" --type bugfix
/ralph-planner:from-file "./specs/api-migration.md" --type migration
/ralph-planner:from-file "./docs/feature.md" --output "./plans/feature-plan.md"
/ralph-planner:from-file ".serena/memory/tasks.md" --type feature --output "./plans/tasks-plan.md"
```

## Guidelines

- Preserve important details from the source file
- Map file requirements to specific tasks
- If file has acceptance criteria, incorporate into completion criteria
- Auto-detection is best-effort; use `--type` when certain
