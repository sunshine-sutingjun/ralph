---
name: ralph
description: Autonomous agent for tackling big projects. Create PRDs with user stories, then run them via the CLI. Sessions persist across restarts with pause/resume and real-time monitoring.
---

---
name: ralph
description: Autonomous agent for tackling big projects. Create PRDs with user stories, then run them via the CLI. Sessions persist across restarts with pause/resume and real-time monitoring.
---

# Ralph - Autonomous Agent Skill

Ralph is an autonomous agent skill that breaks complex projects into user stories and executes them step by step. It's designed to work with command-line AI systems that have skills installed.

## How Ralph Works with Your AI

When you tell your AI "use Ralph" or "use the Ralph skill":

1. Your AI reads this SKILL.md to understand what Ralph does
2. Your AI creates a PRD (project requirements document)
3. Your AI runs Ralph to execute the project automatically
4. Ralph breaks the work into user stories and completes them one by one

## Installation

Ralph is installed as a skill in your AI system. Once installed, you can use it anytime by saying "use Ralph" or referencing it in your request.

## Creating Work for Ralph

1. **Create a PRD** - Define user stories with acceptance criteria
2. **Run it** - `ralph.mjs create --prd path/to/prd.json --start`
3. **Monitor** - `ralph.mjs logs <session-id> --follow`

## Creating Work for Ralph

### Basic Workflow

1. **Define a PRD** - Create a JSON file describing your project
2. **Run Ralph** - `ralph.mjs create --prd path/to/prd.json --start`
3. **Monitor** - `ralph.mjs logs <session-id> --follow`

### PRD Structure

```json
{
  "description": "Brief description of the project",
  "taskType": "code",
  "branchName": "feature/my-feature",
  "requiredSkills": [
    "description of capability needed"
  ],
  "contextMap": {
    "storyId": {
      "references": ["file1", "file2"],
      "code_files": ["src/file.py"],
      "explanation": "path/to/notes.md"
    }
  },
  "userStories": [
    {
      "id": "US001",
      "title": "Short descriptive title",
      "description": "As a [user], I want [feature] so that [benefit]",
      "acceptanceCriteria": [
        "Specific testable criterion"
      ],
      "priority": 1,
      "passes": false
    }
  ]
}
```

### PRD Fields

- **description** - What the project is about
- **taskType** - Type of work (code, research, content, data, devops, testing, orchestrator)
- **branchName** - Git branch for code projects (optional)
- **requiredSkills** - Capabilities needed (e.g., "QMD formatting and compilation", "web automation")
  - Ralph declares what it needs
  - Your AI identifies which of its installed skills can help
  - Your AI calls those skills at appropriate moments
- **contextMap** - Maps story IDs to resources they need to read
  - `references` - Documents to read (markdown, BibTeX, etc.)
  - `code_files` - Source code to understand
  - `explanation` - Implementation notes or guides
  - `experiments` - Data and visualizations for results sections
- **userStories** - List of tasks to complete

### Task Types

Ralph supports multiple task types via the `taskType` field in PRD:

- **code** - Software development (web, backend, CLI, etc.)
- **research** - Research, analysis, data collection
- **content** - Documentation, blogs, writing, papers
- **data** - Data processing, ETL, analytics, reports
- **devops** - Infrastructure, deployment, configuration
- **testing** - Automated testing and QA
- **orchestrator** - Coordinate multiple sub-tasks

## Working with Resources and Skills

### Resource Mapping (contextMap)

When your project has lots of resources (code, documentation, experimental results), use `contextMap` to tell Ralph what to read for each story:

```json
"contextMap": {
  "write_results": {
    "references": ["refs/methodology.bib"],
    "explanation": "docs/results_guide.md",
    "experiments": [
      {
        "name": "exp1",
        "code": "src/experiment1.py",
        "output": "results/exp1.json",
        "visualization": "results/exp1.png"
      }
    ]
  }
}
```

Ralph will read all these resources before writing that section.

### Required Skills

The `requiredSkills` field tells Ralph what capabilities it needs. Your AI system will:

1. **Read the skill declarations** - e.g., "needs QMD formatting and compilation"
2. **Identify matching skills** - Your AI knows what skills it has
3. **Call appropriate skills** - At the right moments during execution

Example:

```json
"requiredSkills": [
  "QMD formatting and mathematical notation",
  "Figure rendering and validation",
  "Citation and bibliography management"
]
```

Your AI might say to itself: "I have qmd-writing skill for formatting, qmd-rendering for figures, and bibutils for citations. Those match perfectly."

## Example: MCM Paper Writing

A complete example is in `examples/mcm-paper-prd.json` showing:
- Multi-section document structure
- Resource mapping for each section  
- Referenced skills for formatting and visualization
- Experimental results tied to specific sections

### Story Guidelines

- **Priority 1**: Foundation - migrations, types, base components
- **Priority 2-3**: Core functionality
- **Priority 4+**: Secondary features, polish
- Each story should touch 1-3 files, not 10-file refactors
- Include "Typecheck passes" in acceptance criteria

## CLI Commands

The daemon starts automatically when you run any command.

### Running Sessions

```bash
# Create and start a session
ralph.mjs create --prd path/to/prd.json --start

# List all sessions
ralph.mjs list

# Check session status
ralph.mjs status <session-id>

# Follow logs in real-time
ralph.mjs logs <session-id> --follow
```

### Session Control

```bash
# Pause a session
ralph.mjs pause <session-id> --reason "Waiting for API"

# Resume with guidance
ralph.mjs resume <session-id> --guidance "API is ready on port 3000"

# Inject guidance into running session
ralph.mjs inject <session-id> --message "Try using the helper in utils.ts"

# Abort a session
ralph.mjs abort <session-id>
```

### Orchestration (Multi-Level)

For orchestrator PRDs that spawn child sessions:

```bash
# Spawn a child session
ralph.mjs spawn <parent-id> --prd child/prd.json --start

# List children of a session
ralph.mjs children <session-id>

# Wait for all children to complete
ralph.mjs wait <session-id>

# View session tree
ralph.mjs tree <session-id>

# Abort parent and all children
ralph.mjs abort <session-id> --cascade
```

## PRD Types

| Type | Use Case |
|------|----------|
| `code` (default) | Implement features, commit code |
| `orchestrator` | Coordinate multiple sub-Ralphs |
| `testing` | Browser automation testing |

Set via `"type": "orchestrator"` in prd.json.

## Full CLI Reference

Run `ralph.mjs --help` for complete documentation.
