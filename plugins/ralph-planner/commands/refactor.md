# refactor

Create a structured execution plan for refactoring code.

## Arguments

- `description` (required): Description of the refactoring goal

## Instructions

You are a planning assistant. Create a structured plan for refactoring: "$ARGUMENTS"

### Plan Structure

Generate a plan with these specific phases:

```
## Plan: Refactor [Component/area from description]

### Phase 1: Analysis
**Tasks:**
- [ ] Map current code structure and dependencies
- [ ] Identify specific improvements to make
- [ ] Document current behavior (what must NOT change)
- [ ] Identify risks and potential breaking changes

**Completion Criteria:** Current state documented, target state defined, risks identified

### Phase 2: Preparation
**Tasks:**
- [ ] Ensure adequate test coverage exists for affected code
- [ ] Add missing tests if coverage is insufficient
- [ ] Create backup/branch for safety
- [ ] Run all tests to establish baseline (all must pass)

**Completion Criteria:** Test coverage sufficient, all tests passing before changes

### Phase 3: Refactor
**Tasks:**
- [ ] Apply changes incrementally (small commits)
- [ ] [Specific refactoring tasks based on goal...]
- [ ] Run tests after each significant change
- [ ] Keep behavior identical - only structure changes

**Completion Criteria:** Refactoring complete, code matches target structure

### Phase 4: Validation
**Tasks:**
- [ ] Run full test suite
- [ ] Verify no functional behavior changes
- [ ] Review code meets stated goals
- [ ] Check performance hasn't degraded

**Completion Criteria:** All tests pass, behavior unchanged, goals met

---

**Total Tasks:** [count]
**Estimated Iterations:** [count × 3]

🏷️ **Promise Tag:** I will complete this refactoring when:
- All existing tests still pass
- No functional behavior has changed
- Code structure meets the stated goals
- No performance degradation
```

### Generate Loop Command

```
Ready to execute? Run:
/ralph-wiggum:ralph-loop [estimated iterations] "Refactor: [component]"
```

### Guidelines

- Tests first - never refactor without coverage
- Incremental changes, run tests frequently
- Behavior must remain identical
- If tests are missing, adding them is part of the work
