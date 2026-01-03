---
description: "Create a structured execution plan for performance optimization"
---

# performance

Create a structured execution plan for performance optimization.

## Arguments

- `description` (required): Description of the performance issue or optimization goal

## Instructions

You are a planning assistant. Create a structured plan for optimizing: "$ARGUMENTS"

### Plan Structure

Generate a plan with these specific phases:

```
## Plan: Optimize [Area from description]

### Phase 1: Baseline
**Tasks:**
- [ ] Define metrics to measure (latency, throughput, memory, etc.)
- [ ] Measure current performance with consistent methodology
- [ ] Document baseline numbers
- [ ] Set target improvement goal (specific %)

**Completion Criteria:** Baseline metrics documented, target defined

### Phase 2: Analysis
**Tasks:**
- [ ] Profile the system to identify bottlenecks
- [ ] Rank bottlenecks by impact
- [ ] Research optimization approaches for top bottlenecks
- [ ] Estimate effort vs impact for each approach

**Completion Criteria:** Bottlenecks identified and prioritized, approaches selected

### Phase 3: Optimization
**Tasks:**
- [ ] Implement highest-impact optimization first
- [ ] [Specific optimization tasks...]
- [ ] Measure after each change to verify improvement
- [ ] Ensure no functional regressions

**Completion Criteria:** Optimizations implemented, each verified to improve metrics

### Phase 4: Validation
**Tasks:**
- [ ] Run full performance measurement suite
- [ ] Compare to baseline (document improvement %)
- [ ] Run functional test suite (no regressions)
- [ ] Document changes and results for future reference

**Completion Criteria:** Target improvement achieved, no regressions, results documented

---

**Total Tasks:** [count]
**Estimated Iterations:** [count × 3]

🏷️ **Promise Tag:** I will complete this optimization when:
- Performance improved by [X]% vs baseline
- No functional regressions
- All benchmarks documented
- Changes are sustainable (not hacks)

⚠️ **Completion Signal:** When ALL criteria above are met, output:
<promise>COMPLETE</promise>
```

### Generate Loop Command

**IMPORTANT:** Always include DONE condition with verifiable promises!

```
Ready to execute? Run:
/ralph-wiggum:ralph-loop [estimated iterations] "Optimize: [area]. DONE when: performance improved vs baseline, no functional regressions, benchmarks documented"
```

### Guidelines

- Measure before optimizing - no guessing
- One change at a time, measure each
- Premature optimization is the root of all evil
- Document results for future reference
