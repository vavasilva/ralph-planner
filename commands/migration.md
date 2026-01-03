---
description: "Create a structured execution plan for a migration task"
---

# migration

Create a structured execution plan for a migration task.

## Arguments

- `description` (required): Description of what needs to be migrated

## Instructions

You are a planning assistant. Create a structured plan for migrating: "$ARGUMENTS"

### Plan Structure

Generate a plan with these specific phases:

```
## Plan: Migrate [Subject from description]

### Phase 1: Assessment
**Tasks:**
- [ ] Inventory everything that needs migration
- [ ] Document current state and dependencies
- [ ] Identify migration order (dependencies first)
- [ ] Estimate scope and complexity

**Completion Criteria:** Complete inventory, dependencies mapped, migration order defined

### Phase 2: Preparation
**Tasks:**
- [ ] Create backup of current state
- [ ] Document rollback procedure
- [ ] Test rollback procedure works
- [ ] Set up target environment/structure
- [ ] Create migration scripts if needed

**Completion Criteria:** Backup exists, rollback tested, target ready

### Phase 3: Migration
**Tasks:**
- [ ] Execute migration in defined order
- [ ] [Specific migration steps based on task...]
- [ ] Validate each step before proceeding
- [ ] Document any issues encountered

**Completion Criteria:** All items migrated to target

### Phase 4: Verification
**Tasks:**
- [ ] Verify all data/functionality in new location
- [ ] Run application tests against migrated state
- [ ] Compare old vs new (spot check critical items)
- [ ] Confirm rollback still possible if needed

**Completion Criteria:** Migration verified correct, application functional

---

**Total Tasks:** [count]
**Estimated Iterations:** [count × 3]

🏷️ **Promise Tag:** I will complete this migration when:
- All items successfully migrated
- Application functions normally with migrated state
- Data integrity verified
- Rollback procedure documented and tested

⚠️ **Completion Signal:** When ALL criteria above are met, output:
<promise>COMPLETE</promise>
```

### Generate Loop Command

**IMPORTANT:** Always include DONE condition with verifiable promises!

```
Ready to execute? Run:
/ralph-wiggum:ralph-loop [estimated iterations] "Migrate: [subject]. DONE when: all items migrated, application functional, data integrity verified, rollback tested"
```

### Guidelines

- Always have a tested rollback plan
- Migrate in small batches when possible
- Verify after each batch, not just at the end
- Keep old system available until migration confirmed
