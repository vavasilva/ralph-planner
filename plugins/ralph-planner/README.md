# ralph-planner

Companion plugin for [ralph-wiggum](https://github.com/anthropics/claude-code/tree/main/plugins/ralph-wiggum) that creates structured execution plans in Ralph format.

## Installation

```bash
claude plugins:add vavasilva/ralph-planner
```

## Requirements

Requires the [ralph-wiggum](https://github.com/anthropics/claude-code/tree/main/plugins/ralph-wiggum) plugin:

```bash
claude plugins:add anthropics/claude-code/plugins/ralph-wiggum
```

## Commands

| Command | Description |
|---------|-------------|
| `/ralph-planner:plan-loop "<task>"` | Generic plan for any task |
| `/ralph-planner:feature "<desc>"` | New feature implementation |
| `/ralph-planner:bugfix "<desc>"` | Bug fix with regression test |
| `/ralph-planner:refactor "<desc>"` | Code refactoring |
| `/ralph-planner:migration "<desc>"` | Data/code migration |
| `/ralph-planner:performance "<desc>"` | Performance optimization |
| `/ralph-planner:help` | Show help documentation |

## Work Type Templates

Each template has **pre-defined phases** and **verifiable promises** optimized for the work type:

### Feature
```
/ralph-planner:feature "Add user authentication with JWT"
```
**Phases:** Discovery → Implementation → Testing → Documentation

**Promises:** All new tests pass, Feature works as specified, No regressions

### Bugfix
```
/ralph-planner:bugfix "Users can't login after password reset"
```
**Phases:** Reproduction → Root Cause → Fix → Verification

**Promises:** Bug no longer reproducible, Regression test added, No new issues

### Refactor
```
/ralph-planner:refactor "Extract payment logic into separate service"
```
**Phases:** Analysis → Preparation → Refactor → Validation

**Promises:** All existing tests pass, No behavior changes, Goals met

### Migration
```
/ralph-planner:migration "Move user data from MySQL to PostgreSQL"
```
**Phases:** Assessment → Preparation → Migration → Verification

**Promises:** All data migrated, Application functional, Rollback tested

### Performance
```
/ralph-planner:performance "Reduce API response time for /users endpoint"
```
**Phases:** Baseline → Analysis → Optimization → Validation

**Promises:** Metrics improved by X%, No regressions, Results documented

## How It Works

1. Choose a template matching your work type (or use generic `plan-loop`)
2. The plugin generates phases with clear completion criteria
3. It calculates iterations estimate (`tasks × 3`)
4. It outputs the ready-to-run `/ralph-wiggum:ralph-loop` command

## Why Templates?

Generic promises like *"I will complete all phases systematically"* are not verifiable. Templates provide:

- **Specific phases** for each work type
- **Verifiable promises** ("All tests pass" vs "I'll do my best")
- **Consistent structure** for repeatable planning

## License

MIT
