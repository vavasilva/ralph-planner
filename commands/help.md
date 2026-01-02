# help

Display help documentation for the ralph-planner plugin.

## Instructions

Output the following help information:

```
# Ralph Planner

Companion plugin for ralph-wiggum that creates structured execution plans.

## Commands

### /ralph-planner:plan-loop "<task>"
Creates a structured plan in Ralph format with:
- **Phases**: Logical groupings of related tasks
- **Completion Criteria**: Clear definition of done for each phase
- **Promise Tag**: Commitment marker for systematic execution
- **Iteration Estimate**: Calculated as tasks × 3

Auto-generates the `/ralph-wiggum:ralph-loop` command ready to execute.

### /ralph-planner:help
Shows this help message.

## Example

```
/ralph-planner:plan-loop "Implement user authentication with JWT"
```

This will generate a phased plan and output:
```
Ready to execute? Run:
/ralph-wiggum:ralph-loop 15 "Implement JWT authentication"
```

## Requirements

Requires the ralph-wiggum plugin to be installed for executing the generated loop commands.

Install: https://github.com/anthropics/claude-code/tree/main/plugins/ralph-wiggum
```
