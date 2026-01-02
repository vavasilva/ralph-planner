# help

Display help documentation for the ralph-planner plugin.

## Instructions

Output the following help information:

```
# Ralph Planner

Companion plugin for ralph-wiggum that creates structured execution plans.

## Commands

### Generic Planning
- `/ralph-planner:plan-loop "<task>"` - Create a plan for any task

### Work Type Templates
Specialized templates with pre-defined phases and **verifiable promises**:

- `/ralph-planner:feature "<description>"` - New feature implementation
- `/ralph-planner:bugfix "<description>"` - Bug fix with regression test
- `/ralph-planner:refactor "<description>"` - Code refactoring
- `/ralph-planner:migration "<description>"` - Data/code migration
- `/ralph-planner:performance "<description>"` - Performance optimization

### Help
- `/ralph-planner:help` - Show this help message

## Template Benefits

Each template includes:
- **Pre-defined phases** optimized for the work type
- **Verifiable promises** (not generic statements)
- **Specific completion criteria** for each phase

Example promises by type:
- **feature**: "All new tests pass", "No regressions"
- **bugfix**: "Bug no longer reproducible", "Regression test added"
- **refactor**: "All existing tests still pass", "No behavior changes"
- **migration**: "All data migrated correctly", "Rollback tested"
- **performance**: "Metrics improved by X%", "Benchmarks documented"

## Example

```
/ralph-planner:bugfix "Users can't login after password reset"
```

Generates a plan with Reproduction → Root Cause → Fix → Verification phases.

## Requirements

Requires ralph-wiggum plugin for executing generated loop commands.
```
