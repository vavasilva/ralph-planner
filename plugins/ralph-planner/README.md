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
| `/ralph-planner:from-file "<path>" [--type] [--output]` | Create plan from existing .md file |
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

### From File

Already have a feature spec or issue documented? Use `from-file` to generate a plan:

```
/ralph-planner:from-file "./docs/my-feature.md"
/ralph-planner:from-file "./issues/bug-123.md" --type bugfix
/ralph-planner:from-file "./docs/feature.md" --output "./plans/feature-plan.md"
```

**Options:**
- `--type <type>`: Force a specific template (feature, bugfix, refactor, migration, performance)
- `--output <path>`: Save the plan to a file instead of just displaying it

The command reads your file, auto-detects the work type (or uses `--type`), and generates a structured plan based on the content.

## How It Works

1. Choose a template matching your work type (or use generic `plan-loop`)
2. The plugin generates phases with clear completion criteria
3. It calculates iterations estimate (`tasks × 3`)
4. It outputs ready-to-run commands **with DONE conditions included**

### Generated Command Example

```
Ready to execute? Run:
/ralph-wiggum:ralph-loop 42 "Implement auth feature. DONE when: feature works as specified, all new tests pass, no regressions, documentation updated"
```

The **DONE condition** tells ralph-wiggum when to stop the loop, preventing infinite execution.

## Why Templates?

Generic promises like *"I will complete all phases systematically"* are not verifiable. Templates provide:

- **Specific phases** for each work type
- **Verifiable promises** ("All tests pass" vs "I'll do my best")
- **Consistent structure** for repeatable planning

## License

MIT
