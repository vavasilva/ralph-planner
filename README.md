# Ralph Planner

**Planning-first workflows for Ralph Wiggum loops**

> Turn a vague task into a clear execution plan — then run it in a loop.

## The Problem

Ralph Wiggum loops are powerful, but they often fail because of **bad prompts**:

- Unclear scope
- No definition of done
- Infinite or wasteful iterations

**Ralph Planner fixes this by adding a planning layer before the loop runs.**

## What It Does

Given a task description, Ralph Planner:

1. Breaks it into **phases** based on work type
2. Generates **concrete tasks** per phase
3. Adds **completion criteria** (Definition of Done)
4. Estimates **iterations** (`tasks × 3`)
5. Outputs a **ready-to-run loop command** with DONE condition

## Demo

### Input

```
/ralph-planner:feature "Implement JWT authentication for the API"
```

### Output

```markdown
## Phase 1: Discovery
- [ ] Analyze authentication requirements
- [ ] Identify affected endpoints
- [ ] Research JWT best practices

## Phase 2: Implementation
- [ ] Create JWT generation on login
- [ ] Add validation middleware
- [ ] Secure protected routes

## Phase 3: Testing
- [ ] Write unit tests for auth logic
- [ ] Write integration tests for endpoints

## Phase 4: Documentation
- [ ] Update API documentation

Estimated iterations: 30
```

### Ready-to-run command

```
/ralph-wiggum:ralph-loop 30 "Implement JWT authentication. DONE when: feature works as specified, all new tests pass, no regressions"
```

**Plan → Execute → Converge**

## Installation

```bash
claude plugin marketplace add vavasilva/ralph-planner
claude plugin install ralph-planner@ralph-planner
```

### Requirement

Requires [ralph-wiggum](https://github.com/anthropics/claude-code/tree/main/plugins/ralph-wiggum):

```bash
claude plugin install ralph-wiggum@claude-plugins-official
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
| `/ralph-planner:from-file "<path>"` | Create plan from existing .md file |
| `/ralph-planner:help` | Show help documentation |

## Work Type Templates

Each template has **pre-defined phases** and **verifiable promises** optimized for the work type:

### Feature

```
/ralph-planner:feature "Add user authentication with JWT"
```

| Phases | Discovery → Implementation → Testing → Documentation |
|--------|-------------------------------------------------------|
| Promises | All new tests pass, Feature works as specified, No regressions |

### Bugfix

```
/ralph-planner:bugfix "Users can't login after password reset"
```

| Phases | Reproduction → Root Cause → Fix → Verification |
|--------|------------------------------------------------|
| Promises | Bug no longer reproducible, Regression test added, No new issues |

### Refactor

```
/ralph-planner:refactor "Extract payment logic into separate service"
```

| Phases | Analysis → Preparation → Refactor → Validation |
|--------|------------------------------------------------|
| Promises | All existing tests pass, No behavior changes, Goals met |

### Migration

```
/ralph-planner:migration "Move user data from MySQL to PostgreSQL"
```

| Phases | Assessment → Preparation → Migration → Verification |
|--------|-----------------------------------------------------|
| Promises | All data migrated, Application functional, Rollback tested |

### Performance

```
/ralph-planner:performance "Reduce API response time for /users endpoint"
```

| Phases | Baseline → Analysis → Optimization → Validation |
|--------|--------------------------------------------------|
| Promises | Metrics improved, No regressions, Results documented |

### From File

Already have a feature spec or issue documented? Generate a plan from it:

```
/ralph-planner:from-file "./docs/my-feature.md"
/ralph-planner:from-file "./issues/bug-123.md" --type bugfix
/ralph-planner:from-file "./docs/feature.md" --output "./plans/feature-plan.md"
```

**Options:**
- `--type <type>`: Force a specific template (feature, bugfix, refactor, migration, performance)
- `--output <path>`: Save the plan to a file instead of just displaying it

## Why Templates?

Generic promises like *"I will complete all phases systematically"* are **not verifiable**.

Templates provide:

- **Specific phases** for each work type
- **Verifiable promises** ("All tests pass" vs "I'll do my best")
- **DONE conditions** that tell the loop when to stop

## How It Fits the Ralph Ecosystem

| Tool | Role |
|------|------|
| ralph-wiggum | Execution loop |
| ralph-planner | Planning & scope definition |
| You | Decide when to run |

Ralph Planner does **not** compete with ralph-wiggum — it **makes it better**.

## Roadmap

- [ ] Configurable iteration multiplier (`--multiplier`)
- [ ] Risk & dependency section in plans
- [ ] Machine-readable plan format (YAML/JSON)
- [ ] Custom template creation

## Troubleshooting

### Loop runs infinitely / "No completion promise set"

If you see this message repeatedly:
```
Ralph iteration X | No completion promise set - loop runs infinitely
```

The ralph-wiggum plugin saves state in `.claude/ralph-loop.local.md`. If a loop wasn't properly cancelled, it persists.

**Solution:**

1. Cancel the active loop:
   ```
   /ralph-wiggum:cancel-ralph
   ```

2. Or delete the state file manually:
   ```bash
   rm .claude/ralph-loop.local.md
   ```

3. Start a fresh Claude session

### Plan generates but loop starts automatically

If planning triggers automatic execution, there's likely an active loop from a previous session. Cancel it first using the steps above.

## License

MIT
