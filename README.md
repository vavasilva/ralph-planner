# Ralph Planner

**Planning-first workflows for Ralph Wiggum loops**

> Turn a vague task into a clear execution plan — then run it in a loop.

## The Problem

Ralph Wiggum loops are powerful, but they often fail because of **bad prompts**:

- Unclear scope
- No definition of done
- Infinite or wasteful iterations

**Ralph Planner fixes this by adding a planning layer before the loop runs.**

## Quick Start

```
/ralph-planner:plan-loop "Add user authentication with JWT"
```

That's it. You get a structured plan + a ready-to-run loop command.

## The DONE Condition (Why This Matters)

The #1 reason loops run forever: **no verifiable exit criteria**.

Ralph Planner generates commands with **specific DONE conditions**:

```
# Bad (runs forever)
/ralph-wiggum:ralph-loop 30 "Implement auth"

# Good (knows when to stop)
/ralph-wiggum:ralph-loop 30 "Implement auth. DONE when: POST /login returns 200 with valid JWT, all tests pass, invalid credentials return 401"
```

Every template includes verifiable promises like:
- `"All tests pass"` (not "tests look good")
- `"Endpoint returns 200"` (not "endpoint works")
- `"Bug no longer reproducible"` (not "bug seems fixed")

## Installation

### In-app (recommended)

```
/plugin marketplace add vavasilva/ralph-planner
/plugin install ralph-planner@ralph-planner
```

### CLI

```bash
claude plugin marketplace add vavasilva/ralph-planner
claude plugin install ralph-planner@ralph-planner
```

### Requirement

Requires [ralph-wiggum](https://github.com/anthropics/claude-code/tree/main/plugins/ralph-wiggum):

```
/plugin install ralph-wiggum@claude-plugins-official
```

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
/ralph-wiggum:ralph-loop 30 "Implement JWT auth. DONE when: POST /login returns JWT, protected routes reject invalid tokens, all tests pass"
```

**Plan → Execute → Converge**

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
| `/ralph-planner:from-issue "#123"` | Create plan from GitHub issue |
| `/ralph-planner:help` | Show help documentation |

## Specialized Templates

Each template has **pre-defined phases** and **verifiable promises**:

### Feature

```
/ralph-planner:feature "Add user authentication with JWT"
```

| Phases | Discovery → Implementation → Testing → Documentation |
|--------|-------------------------------------------------------|
| DONE when | All new tests pass, Feature works as specified, No regressions |

### Bugfix

```
/ralph-planner:bugfix "Users can't login after password reset"
```

| Phases | Reproduction → Root Cause → Fix → Verification |
|--------|------------------------------------------------|
| DONE when | Bug no longer reproducible, Regression test added, No new issues |

### Refactor

```
/ralph-planner:refactor "Extract payment logic into separate service"
```

| Phases | Analysis → Preparation → Refactor → Validation |
|--------|------------------------------------------------|
| DONE when | All existing tests pass, No behavior changes, Goals met |

### Migration

```
/ralph-planner:migration "Move user data from MySQL to PostgreSQL"
```

| Phases | Assessment → Preparation → Migration → Verification |
|--------|-----------------------------------------------------|
| DONE when | All data migrated, Application functional, Rollback tested |

### Performance

```
/ralph-planner:performance "Reduce API response time for /users endpoint"
```

| Phases | Baseline → Analysis → Optimization → Validation |
|--------|--------------------------------------------------|
| DONE when | Response time < target, No regressions, Benchmarks documented |

### From File

Already have a feature spec documented? Generate a plan from it:

```
/ralph-planner:from-file "./docs/my-feature.md"
/ralph-planner:from-file "./issues/bug-123.md" --type bugfix
/ralph-planner:from-file "./docs/feature.md" --output "./plans/feature-plan.md"
```

### From Issue

Create plans directly from GitHub issues. Labels auto-detect the work type:

```
/ralph-planner:from-issue "#42"
/ralph-planner:from-issue "owner/repo#123"
/ralph-planner:from-issue "#42" --include-comments
```

**Auto-detection from labels:**

| GitHub Labels | Template |
|---------------|----------|
| `bug`, `bugfix`, `fix` | bugfix |
| `enhancement`, `feature` | feature |
| `refactor`, `tech-debt` | refactor |
| `migration`, `upgrade` | migration |
| `performance`, `perf` | performance |

## Why Templates?

Generic promises like *"I will complete all phases systematically"* are **not verifiable**.

Templates provide:

- **Specific phases** for each work type
- **Verifiable DONE conditions** ("All tests pass" vs "I'll do my best")
- **Exit criteria** that tell the loop when to stop

## How It Fits the Ralph Ecosystem

| Tool | Role |
|------|------|
| ralph-wiggum | Execution loop |
| ralph-planner | Planning & scope definition |
| You | Decide when to run |

Ralph Planner does **not** compete with ralph-wiggum — it **makes it better**.

## Running Unattended Loops

For long-running loops without permission prompts:

```bash
claude --dangerously-skip-permissions
```

> **Warning:** This skips ALL permission checks. Only use in:
> - Isolated/sandboxed environments
> - Projects where you trust the plan completely
> - When you've reviewed the generated plan first

**Recommended workflow:**

1. Generate plan with ralph-planner (review it carefully)
2. Start Claude with `--dangerously-skip-permissions`
3. Run the ralph-loop command

## Roadmap

- [ ] Configurable iteration multiplier (`--multiplier`) [#2](https://github.com/vavasilva/ralph-planner/issues/2)
- [ ] Risk & dependency section in plans [#3](https://github.com/vavasilva/ralph-planner/issues/3)
- [ ] Machine-readable plan format (YAML/JSON) [#4](https://github.com/vavasilva/ralph-planner/issues/4)
- [ ] Custom template creation [#5](https://github.com/vavasilva/ralph-planner/issues/5)

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
