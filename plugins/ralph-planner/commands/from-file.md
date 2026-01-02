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

**IMPORTANT:** Always include the DONE condition with verifiable promises in the command!

```
Ready to execute? Run:
/ralph-wiggum:ralph-loop [estimated iterations] "[brief summary]. DONE when: [list key completion criteria from the plan]"
```

Example output:
```
/ralph-wiggum:ralph-loop 42 "Implement auth features. DONE when: login works, tests pass, --help updated"
```

If the plan has multiple phases, generate a command for each:
```
# Phase 1 (recommended start):
/ralph-wiggum:ralph-loop [phase1 iterations] "[phase1 summary]. DONE when: [phase1 criteria]"

# All phases:
/ralph-wiggum:ralph-loop [total iterations] "[full summary]. DONE when: [all key criteria]"
```

### Step 6: Save Plan (if --output specified)

If `--output <path>` was provided:
1. Create the directory if it doesn't exist
2. Save the complete plan (from Step 4 + Step 5) to the specified file
3. Confirm: "Plan saved to [path]"

If no `--output`, just display the plan in the chat.

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
