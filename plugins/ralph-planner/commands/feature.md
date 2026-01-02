# feature

Create a structured execution plan for implementing a new feature.

## Arguments

- `description` (required): Description of the feature to implement

## Instructions

You are a planning assistant. Create a structured plan for implementing: "$ARGUMENTS"

### Plan Structure

Generate a plan with these specific phases:

```
## Plan: [Feature name derived from description]

### Phase 1: Discovery
**Tasks:**
- [ ] Understand requirements and acceptance criteria
- [ ] Identify affected files and components
- [ ] Check for existing patterns to follow
- [ ] Identify potential edge cases

**Completion Criteria:** Requirements are clear, affected areas mapped, approach decided

### Phase 2: Implementation
**Tasks:**
- [ ] [Core implementation tasks based on feature]
- [ ] [Additional implementation tasks...]
- [ ] Handle edge cases identified in discovery

**Completion Criteria:** Core feature logic implemented and functional

### Phase 3: Testing
**Tasks:**
- [ ] Write unit tests for new functionality
- [ ] Write integration tests if applicable
- [ ] Test edge cases
- [ ] Run existing test suite to check for regressions

**Completion Criteria:** All new tests pass, no regressions in existing tests

### Phase 4: Documentation
**Tasks:**
- [ ] Update relevant documentation if needed
- [ ] Add code comments for complex logic
- [ ] Update changelog/release notes if applicable

**Completion Criteria:** Documentation reflects new feature

---

**Total Tasks:** [count]
**Estimated Iterations:** [count × 3]

🏷️ **Promise Tag:** I will complete this feature when:
- All new tests pass
- Feature works as specified in requirements
- No regressions in existing tests
- Code follows project patterns
```

### Generate Loop Command

```
Ready to execute? Run:
/ralph-wiggum:ralph-loop [estimated iterations] "[feature name]"
```

### Guidelines

- Break implementation into small, testable chunks
- Each task should be completable in one iteration
- Completion criteria must be verifiable (not subjective)
- Include specific file paths when known
