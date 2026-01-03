---
description: "Create a structured execution plan for fixing a bug"
---

# bugfix

Create a structured execution plan for fixing a bug.

## Arguments

- `description` (required): Description of the bug to fix

## Instructions

You are a planning assistant. Create a structured plan for fixing: "$ARGUMENTS"

### Plan Structure

Generate a plan with these specific phases:

```
## Plan: Fix [Bug summary derived from description]

### Phase 1: Reproduction
**Tasks:**
- [ ] Reproduce the bug consistently
- [ ] Document exact steps to reproduce
- [ ] Identify the expected vs actual behavior
- [ ] Note any error messages or logs

**Completion Criteria:** Bug is reproducible with documented steps

### Phase 2: Root Cause Analysis
**Tasks:**
- [ ] Trace the code path involved
- [ ] Identify the root cause (not just symptoms)
- [ ] Understand why the bug wasn't caught before
- [ ] Check if the bug exists elsewhere (similar patterns)

**Completion Criteria:** Root cause identified and documented

### Phase 3: Fix Implementation
**Tasks:**
- [ ] Implement the fix for root cause
- [ ] Address any related occurrences found
- [ ] Ensure fix doesn't introduce new issues

**Completion Criteria:** Fix implemented, code compiles/runs

### Phase 4: Verification
**Tasks:**
- [ ] Write regression test that would have caught this bug
- [ ] Verify bug no longer occurs with original reproduction steps
- [ ] Run existing test suite
- [ ] Test related functionality for side effects

**Completion Criteria:** Regression test passes, bug no longer reproducible, no new issues

---

**Total Tasks:** [count]
**Estimated Iterations:** [count × 3]

🏷️ **Promise Tag:** I will complete this bugfix when:
- Bug is no longer reproducible
- Regression test is added and passes
- All existing tests still pass
- No new issues introduced

⚠️ **Completion Signal:** When ALL criteria above are met, output:
<promise>COMPLETE</promise>
```

### Generate Loop Command

**IMPORTANT:** Always include DONE condition with verifiable promises!

```
Ready to execute? Run:
/ralph-wiggum:ralph-loop [estimated iterations] "Fix: [bug summary]. DONE when: bug no longer reproducible, regression test added and passes, all existing tests pass"
```

### Guidelines

- Never skip reproduction - understand before fixing
- Root cause > symptom treatment
- Regression test is mandatory, not optional
- Check for similar bugs in related code
