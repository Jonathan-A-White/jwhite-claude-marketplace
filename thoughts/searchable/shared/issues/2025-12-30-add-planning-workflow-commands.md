# Add Planning Workflow Commands to jwhite-claude-plugin

## Status
Open

## Priority
Medium

## Type
Feature

## Problem Statement

The jwhite-claude-plugin currently only has the `/create-issue` command. To enable a complete planning workflow, we need to add the research, planning, implementation, and validation commands that exist in the HumanLayer repo.

### Context
These commands form a cohesive workflow:
1. `/research_codebase` - Document codebase as-is with thoughts directory for historical context
2. `/create_plan` - Create detailed implementation plans through interactive research
3. `/implement_plan` - Execute approved plans from `thoughts/shared/plans/`
4. `/validate_plan` - Verify implementation against plan and success criteria

### Impact
Without these commands, users of the plugin cannot leverage the full planning workflow. Adding them makes the plugin self-contained and shareable via the marketplace.

## Current Behavior
The plugin has:
- `commands/create-issue.md`
- `skills/humanlayer-thoughts-setup/SKILL.md`

## Expected Behavior
The plugin will have:
- `commands/create-issue.md` (existing)
- `commands/research_codebase.md` (new)
- `commands/create_plan.md` (new)
- `commands/implement_plan.md` (new)
- `commands/validate_plan.md` (new)
- `agents/codebase-analyzer.md` (new)
- `agents/codebase-locator.md` (new)
- `agents/codebase-pattern-finder.md` (new)
- `agents/thoughts-analyzer.md` (new)
- `agents/thoughts-locator.md` (new)
- `agents/web-search-researcher.md` (new)
- `scripts/spec_metadata.sh` (new)

## Scope

### In Scope
- Copy 4 command files from HumanLayer repo
- Copy 6 agent files from HumanLayer repo
- Copy `spec_metadata.sh` script from HumanLayer repo
- Update script path references: `hack/spec_metadata.sh` → `${CLAUDE_PLUGIN_ROOT}/scripts/spec_metadata.sh`
- Remove Linear agent references (linear-ticket-reader, linear-searcher)
- Update plugin.json to reflect new capabilities
- Update CLAUDE.md with command documentation
- Update README.md

### Out of Scope
- Linear integration (explicitly excluded)
- The `_nt` and `_generic` variants of commands
- Other HumanLayer commands (commit, describe_pr, etc.)
- Modifying the command logic beyond path/reference fixes

## Success Criteria
- [ ] All 4 commands copied and functional
- [ ] All 6 agents copied and available
- [ ] `spec_metadata.sh` script works via `${CLAUDE_PLUGIN_ROOT}/scripts/`
- [ ] No references to Linear agents remain
- [ ] Plugin installs cleanly from marketplace
- [ ] `/research_codebase` runs successfully
- [ ] `/create_plan` runs successfully
- [ ] `/implement_plan` runs successfully
- [ ] `/validate_plan` runs successfully

## Technical Notes

### Source Files (from HumanLayer GitHub)
**Commands** - https://github.com/humanlayer/humanlayer/tree/main/.claude/commands
- `research_codebase.md`
- `create_plan.md`
- `implement_plan.md`
- `validate_plan.md`

**Agents** - https://github.com/humanlayer/humanlayer/tree/main/.claude/agents
- `codebase-analyzer.md`
- `codebase-locator.md`
- `codebase-pattern-finder.md`
- `thoughts-analyzer.md`
- `thoughts-locator.md`
- `web-search-researcher.md`

**Scripts** - https://github.com/humanlayer/humanlayer/tree/main/hack
- `spec_metadata.sh`

### Path Reference Updates
The `research_codebase.md` command references `hack/spec_metadata.sh`. This must be updated to use the plugin-relative path pattern established by compound-engineering:

```bash
# Before (HumanLayer repo context)
hack/spec_metadata.sh

# After (plugin context)
${CLAUDE_PLUGIN_ROOT}/scripts/spec_metadata.sh
```

### Linear References to Remove
The following agent references should be removed from command files:
- `linear-ticket-reader`
- `linear-searcher`

These appear in `research_codebase.md` and `create_plan.md`.

### Plugin Structure After Implementation
```
plugins/jwhite-claude-plugin/
├── .claude-plugin/
│   └── plugin.json
├── agents/
│   ├── codebase-analyzer.md
│   ├── codebase-locator.md
│   ├── codebase-pattern-finder.md
│   ├── thoughts-analyzer.md
│   ├── thoughts-locator.md
│   └── web-search-researcher.md
├── commands/
│   ├── create-issue.md
│   ├── create_plan.md
│   ├── implement_plan.md
│   ├── research_codebase.md
│   └── validate_plan.md
├── scripts/
│   └── spec_metadata.sh
├── skills/
│   └── humanlayer-thoughts-setup/
│       └── SKILL.md
├── CLAUDE.md
├── LICENSE
└── README.md
```

## Open Questions
None - all decisions made during issue creation.

## References
- HumanLayer repo: https://github.com/humanlayer/humanlayer
- Existing plugin: `plugins/jwhite-claude-plugin/`
- Path pattern reference: compound-engineering plugin uses `${CLAUDE_PLUGIN_ROOT}`
