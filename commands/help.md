---
description: "Display help documentation for the ralph-planner plugin"
---

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

### From File
- `/ralph-planner:from-file "<path>" [--type <type>] [--output <path>]` - Create plan from existing .md file

### From GitHub Issue
- `/ralph-planner:from-issue "#123" [--type <type>] [--output <path>] [--include-comments]` - Create plan from GitHub issue
- Auto-detects work type from issue labels (bug → bugfix, enhancement → feature, etc.)
- Supports `#123` (current repo) or `owner/repo#123` (external repo)

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
