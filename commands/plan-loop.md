---
description: "Create a structured execution plan in Ralph Wiggum format"
---

# plan-loop

Create a structured execution plan in Ralph Wiggum format for the given task.

## Arguments

- `task` (required): Description of the task to plan

## Instructions

You are a planning assistant. Given a task description, create a structured plan following the Ralph Wiggum format.

### Step 1: Analyze the Task

Break down "$ARGUMENTS" into discrete, actionable tasks. Consider:
- What are the logical phases of work?
- What are the dependencies between tasks?
- What defines "done" for each phase?

### Step 2: Create the Plan

Output a plan with this exact structure:

```
## Plan: [Brief title derived from task]

### Phase 1: [Phase Name]
**Tasks:**
- [ ] Task 1 description
- [ ] Task 2 description
- [ ] ...

**Completion Criteria:** [What must be true when this phase is done]

### Phase 2: [Phase Name]
**Tasks:**
- [ ] Task 1 description
- [ ] ...

**Completion Criteria:** [What must be true when this phase is done]

[Continue for all phases...]

---

**Total Tasks:** [count]
**Estimated Iterations:** [count × 3]

🏷️ **Promise Tag:** I will complete all phases systematically, validating each completion criteria before moving to the next phase.

⚠️ **Completion Signal:** When ALL criteria above are met, output:
<promise>COMPLETE</promise>
```

### Step 3: Generate the Loop Command

**IMPORTANT:** Always include DONE condition with verifiable promises from the plan!

After the plan, output:

```
Ready to execute? Run:
/ralph-wiggum:ralph-loop [estimated iterations] "[brief task summary]. DONE when: [list key completion criteria from the plan]"
```

### Guidelines

- Keep phases focused (3-5 tasks each)
- Make completion criteria measurable and verifiable
- Tasks should be atomic (one clear action each)
- Order tasks by dependency within each phase
- Be realistic with iteration estimates (tasks × 3 accounts for validation and fixes)
