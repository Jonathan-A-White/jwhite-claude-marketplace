# jwhite-claude-plugin

Complete planning workflow for Claude Code with Socratic issue creation, codebase research, implementation planning, execution, and validation.

## Components

### Commands

- **`/create-issue`** - Create well-defined issues through Socratic questioning. Challenges assumptions, exposes gaps in thinking, and produces thorough issue documentation.

- **`/research_codebase`** - Document codebase as-is with thoughts directory for historical context. Uses parallel sub-agents to comprehensively research codebases.

- **`/create_plan`** - Create detailed implementation plans through interactive research and iteration. Produces phased plans with automated and manual success criteria.

- **`/implement_plan`** - Implement approved technical plans from `thoughts/shared/plans/`. Executes each phase with verification and pauses for human confirmation.

- **`/validate_plan`** - Validate that an implementation plan was correctly executed. Runs all automated checks and produces validation reports.

- **`/humanlayer_thoughts_setup`** - Guide for setting up HumanLayer thoughts using npm/Node.js for collaborative knowledge sharing.

### Agents

- **`codebase-locator`** - Find files and components by topic/feature
- **`codebase-analyzer`** - Analyze implementation details with file:line references
- **`codebase-pattern-finder`** - Find similar implementations and existing patterns
- **`thoughts-locator`** - Discover documents in thoughts/ directory
- **`thoughts-analyzer`** - Extract insights from thoughts documents
- **`web-search-researcher`** - Research external documentation and resources

## Installation

Install as a Claude Code plugin:

```bash
claude plugin install /path/to/jwhite-claude-plugin
```

Or add to your Claude Code configuration.

## Requirements

- Claude Code CLI
- Node.js v16+ (for HumanLayer)
- HumanLayer API key (get one at https://humanlayer.dev)

## Usage

### Complete Workflow

```
# 1. Define the problem
/create-issue The API is returning inconsistent errors

# 2. Research the codebase
/research_codebase How does error handling work in the API?

# 3. Create a plan
/create_plan thoughts/shared/issues/2025-01-08-api-error-handling.md

# 4. Implement the plan
/implement_plan thoughts/shared/plans/2025-01-08-fix-api-errors.md

# 5. Validate the implementation
/validate_plan thoughts/shared/plans/2025-01-08-fix-api-errors.md
```

### Create an Issue

```
/create-issue The API is returning inconsistent errors
```

The command will guide you through a Socratic questioning process to clarify:
- What exactly the problem is
- What assumptions you're making
- What the scope should be
- How to define success criteria

Issues are saved to `thoughts/shared/issues/`.

### Research the Codebase

```
/research_codebase How does authentication work?
```

The command spawns parallel agents to research and produces a comprehensive document.

### Set Up HumanLayer Thoughts

```
/humanlayer_thoughts_setup
```

This command provides guided installation instructions for HumanLayer using npm.

## Directory Structure

```
jwhite-claude-plugin/
├── .claude-plugin/
│   └── plugin.json           # Plugin configuration
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
│   ├── humanlayer_thoughts_setup.md
│   ├── implement_plan.md
│   ├── research_codebase.md
│   └── validate_plan.md
├── scripts/
│   └── spec_metadata.sh      # Metadata collection script
├── CLAUDE.md
├── LICENSE
└── README.md
```

## License

MIT
