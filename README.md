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

## Usage

### Create a Plan

```
/ralph-planner:plan-loop "Implement user authentication with JWT"
```

This generates a structured plan with:
- **Phases** - Logical groupings of related tasks
- **Completion Criteria** - Clear definition of done for each phase
- **Promise Tag** - Commitment marker for tracking
- **Iteration Estimate** - Calculated as `tasks × 3`

### Example Output

```
## Plan: JWT Authentication Implementation

### Phase 1: Setup
**Tasks:**
- [ ] Install JWT dependencies
- [ ] Create auth configuration file
- [ ] Set up environment variables

**Completion Criteria:** Dependencies installed and configuration in place

### Phase 2: Core Implementation
**Tasks:**
- [ ] Create JWT utility functions
- [ ] Implement login endpoint
- [ ] Implement token refresh endpoint

**Completion Criteria:** All endpoints functional with valid JWT generation

---

**Total Tasks:** 6
**Estimated Iterations:** 18

🏷️ **Promise Tag:** I will complete all phases systematically...

Ready to execute? Run:
/ralph-wiggum:ralph-loop 18 "Implement JWT authentication"
```

## Commands

| Command | Description |
|---------|-------------|
| `/ralph-planner:plan-loop "<task>"` | Create a structured plan for the given task |
| `/ralph-planner:help` | Show help documentation |

## How It Works

1. You describe a task
2. The plugin breaks it into phases with clear completion criteria
3. It estimates iterations (tasks × 3) for the Ralph loop
4. It generates the ready-to-run `/ralph-wiggum:ralph-loop` command

## License

MIT
