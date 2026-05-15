# Tabby - tmux sidebar plugin

Fork: `GergelyH/tabby` (upstream: `brendandebeasi/tabby`)
Branch: `feat/work-dashboard-todos`

## Current focus: TODO-driven work dashboard

TODOs are the organizing principle. Active TODOs become their own sidebar groups.
Backlog TODOs appear in the Work widget at the bottom. Haiku manages TODO lifecycle
via Claude Code stop hooks.

### Architecture

- **State**: `~/.claude/work-state.json` managed by `~/.claude/hooks/work-state.sh`
- **Start hook**: `work-dashboard-start.sh` renames tmux window on session start
- **Stop hook**: `work-dashboard-stop.sh` calls Haiku for summarization, TODO classification, completion detection
- **Sidebar**: `coordinator.go` renders Work widget, handles TODO clicks
- **Grouping**: `grouper.go` auto-creates dynamic groups for TODO-tagged windows
- **Window tagging**: `@todo_id`, `@tabby_group`, `@tabby_name_locked` tmux user options
- **Refresh**: SIGUSR1 to tabby-daemon PID (at `/tmp/tabby-daemon-$SESSION.pid`)

### Tasks

| Task | Status | Owner | Blocked-by | Notes |
|------|--------|-------|------------|-------|
| Test Haiku stop hook end-to-end | open | - | - | Verify classification, completion detection, and new TODO discovery with real sessions |
| Fix screenshot-terminal.sh permissions | open | - | - | Needs Screen Recording permission granted to terminal app for visual verification |
| Dynamic group theming for TODO groups | open | - | - | Currently empty theme with palette defaults; may want per-project colors |
| TODO completion action from sidebar | open | - | - | Clicking an active TODO group header could offer a "mark done" action |
| Handle stale daemon processes | open | - | - | Daemons for detached sessions linger; need cleanup on session destroy |
| Sidebar scroll for many TODOs | open | - | - | Work widget has up/down arrows but needs testing with 10+ items |
| Upstream PR preparation | open | - | Test Haiku stop hook end-to-end | Clean up, write tests, separate generic work-widget from opinionated Haiku integration |
