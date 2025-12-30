# jwhite-claude-plugin

## Plugin Overview

This plugin provides a complete planning workflow for Claude Code, including codebase research, implementation planning, execution, and validation commands with specialized analysis agents.

## Commands

### /create-issue

Creates issues through Socratic questioning to expose gaps in thinking. Never writes an issue after just one exchange - pushes for 2-3 rounds of clarification.

Key behaviors:
- Challenges vague statements
- Exposes hidden assumptions
- Probes for edge cases
- Questions scope
- Verifies understanding through playback

Issues are saved to `thoughts/shared/issues/YYYY-MM-DD-kebab-case-title.md`.

### /research_codebase

Documents codebase as-is with thoughts directory for historical context. Uses parallel sub-agents to comprehensively research and synthesize findings.

Key behaviors:
- Documents what exists without suggesting improvements
- Uses specialized agents (codebase-locator, codebase-analyzer, codebase-pattern-finder)
- Integrates thoughts directory for historical context
- Produces research documents with YAML frontmatter

Research documents are saved to `thoughts/shared/research/YYYY-MM-DD-description.md`.

### /create_plan

Creates detailed implementation plans through interactive research and iteration.

Key behaviors:
- Reads all context files completely before planning
- Spawns parallel research agents to gather context
- Iterates with user on plan structure before writing details
- Separates automated and manual success criteria
- Produces comprehensive plans with phases and verification steps

Plans are saved to `thoughts/shared/plans/YYYY-MM-DD-description.md`.

### /implement_plan

Implements approved technical plans from `thoughts/shared/plans/`.

Key behaviors:
- Reads plan and all referenced files fully
- Implements each phase before moving to next
- Runs success criteria checks after each phase
- Pauses for human verification of manual steps
- Updates checkboxes in plan as work completes

### /validate_plan

Validates that an implementation plan was correctly executed.

Key behaviors:
- Discovers what was implemented through git and codebase analysis
- Runs all automated verification commands
- Documents pass/fail status
- Generates comprehensive validation report
- Lists remaining manual testing required

## Agents

The plugin includes 6 specialized agents for research tasks:

### codebase-locator
Finds WHERE files and components live. A "Super Grep/Glob/LS tool" for locating code.

### codebase-analyzer
Analyzes HOW specific code works with precise file:line references.

### codebase-pattern-finder
Finds similar implementations and existing patterns that can be modeled after.

### thoughts-locator
Discovers relevant documents in the thoughts/ directory.

### thoughts-analyzer
Extracts high-value insights from thoughts documents.

### web-search-researcher
Researches external documentation and resources when explicitly requested.

## Skills

### humanlayer-thoughts-setup

Guides users through HumanLayer setup using npm (not Python):

```bash
npm install -g hlyr
export HUMANLAYER_API_KEY=your_key
humanlayer thoughts sync
```

## Scripts

### spec_metadata.sh

Collects metadata for research and planning documents:
- Current date/time with timezone
- Git commit hash and branch
- Repository name
- HumanLayer thoughts status

Usage: `${CLAUDE_PLUGIN_ROOT}/scripts/spec_metadata.sh`

## Integration Notes

- The `/create-issue` command expects `thoughts/shared/issues/` directory to exist
- The `/create_plan` command expects `thoughts/shared/plans/` directory to exist
- The `/research_codebase` command expects `thoughts/shared/research/` directory to exist
- Run `humanlayer thoughts sync` after creating documents to share with team
- HumanLayer can run as MCP server: `humanlayer mcp serve`

## Workflow

The recommended workflow is:
1. `/create-issue` - Define the problem clearly
2. `/research_codebase` - Understand the current state
3. `/create_plan` - Design the implementation approach
4. `/implement_plan` - Execute the plan
5. `/validate_plan` - Verify correctness
