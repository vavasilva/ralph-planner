# ralph-planner

## Overview
Companion plugin for [ralph-wiggum](https://github.com/anthropics/claude-code/tree/main/plugins/ralph-wiggum) that creates structured plans in Ralph format and auto-generates loop commands.

## Location
`~/Code/ralph-planner`

## Structure
```
ralph-planner/
├── .claude-plugin/
│   └── plugin.json       # Plugin metadata
├── commands/
│   ├── plan-loop.md      # Main command: /plan-loop "task"
│   └── help.md           # Help documentation
└── README.md             # GitHub README with install instructions
```

## Key Features
- `/plan-loop "task description"` - Creates plan in Ralph format
- Auto-generates `/ralph-wiggum:ralph-loop` command ready to execute
- Estimates iterations based on task count (tasks × 3)
- Forces structure: Phases → Completion Criteria → Promise Tag

## Dependencies
- Requires [ralph-wiggum](https://github.com/anthropics/claude-code/tree/main/plugins/ralph-wiggum) plugin installed

## Commands to Create
1. `commands/plan-loop.md` - Main command that creates plans
2. `commands/help.md` - Explains the plugin

## GitHub
Public repo: https://github.com/vavasilva/ralph-planner
