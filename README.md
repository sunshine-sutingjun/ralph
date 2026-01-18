# Ralph - Autonomous Agent Framework

[中文版本](README.zh.md) | **English**

An intelligent autonomous agent framework that breaks down complex projects into manageable user stories and executes them step by step. Ralph is designed to work with command-line AI systems that have access to various skills and tools.

## 🎯 Quick Overview

Ralph enables AI systems to:

1. **Analyze** your project structure and available resources
2. **Generate** an intelligent Project Requirements Document (PRD)
3. **Present** the plan to you for confirmation
4. **Execute** all tasks automatically with human oversight

```
User Request → AI Analyzes → PRD Generated → User Confirms → Ralph Executes
```

## ✨ Key Features

### 🤖 AI-Driven PRD Generation
No manual PRD writing. Your AI system:
- Scans your project structure
- Identifies available skills
- Automatically generates a smart PRD
- Shows it to you for approval

### 📋 Context-Aware Execution
- **contextMap**: Maps resources to each user story
- **requiredSkills**: Declares what capabilities are needed
- **userStories**: Breaks work into atomic, executable pieces

### ⏸️ Pause & Resume Control
- Pause execution anytime
- Review progress at any point
- Resume with corrections or new guidance
- Full session persistence

### 🔍 Turn-by-Turn Execution
- Each iteration runs in fresh context
- Checkpoint after every turn
- Progress logged and maintained
- Sensitive operations flagged for approval

### 🌳 Multi-Task Support
Ralph handles different project types:
- **code**: Software development and refactoring
- **content**: Documentation, papers, blog posts, guides
- **research**: Data analysis and research projects
- **data**: Data processing and analysis
- **devops**: Infrastructure and deployment
- **testing**: Test suite creation and validation
- **orchestrator**: Complex multi-step workflows

## 🚀 Getting Started

### Basic Usage

```bash
# Create and start a session
ralph.mjs create --prd path/to/prd.json --start

# Monitor progress with live logs
ralph.mjs logs <session-id> --follow

# Pause if needed
ralph.mjs pause <session-id> --reason "Waiting for review"

# Resume with corrections
ralph.mjs resume <session-id> --guidance "Try this approach instead"

# Check session status
ralph.mjs status <session-id>
```

### Full CLI Reference

```bash
ralph.mjs --help
```

## 📚 Documentation

### For AI Systems
- **[SKILL.md](SKILL.md)** - What Ralph does and how to use it
- **[docs/AI_WORKFLOW.md](docs/AI_WORKFLOW.md)** - 13-phase workflow for AI systems
- **[docs/PRD_GENERATOR.md](docs/PRD_GENERATOR.md)** - How to generate smart PRDs

### Examples
- **[examples/MCM_PAPER_GUIDE.md](examples/MCM_PAPER_GUIDE.md)** - Complete paper writing example
- **[examples/mcm-paper-prd.json](examples/mcm-paper-prd.json)** - Sample PRD structure

### Task-Specific Guides
- **[prompts/base.md](prompts/base.md)** - Base instructions for all tasks
- **[prompts/content.md](prompts/content.md)** - Content/writing PRDs
- **[prompts/code.md](prompts/code.md)** - Code development PRDs
- **[prompts/research.md](prompts/research.md)** - Research projects
- **[prompts/data.md](prompts/data.md)** - Data analysis
- **[prompts/devops.md](prompts/devops.md)** - Infrastructure tasks
- **[prompts/testing.md](prompts/testing.md)** - Testing PRDs
- **[prompts/orchestrator.md](prompts/orchestrator.md)** - Complex workflows

## 🏗️ Architecture

Ralph consists of:

### CLI Layer
**ralph.mjs** - Command-line interface for creating and managing sessions

### Daemon Layer
- **daemon/server.mjs** - HTTP API server
- **daemon/session-manager.mjs** - Session lifecycle management
- **daemon/turn-engine.mjs** - Controlled turn-by-turn execution
- **daemon/storage.mjs** - SQLite persistence layer
- **daemon/ui.html** - Optional web UI for monitoring

### Prompt Templates
- **prompts/base.md** - Universal instructions for Ralph
- **prompts/{taskType}.md** - Task-specific guidance

## 📖 PRD Structure

A typical PRD looks like:

```json
{
  "description": "Write my research paper",
  "taskType": "content",
  "requiredSkills": [
    "Document formatting with mathematical notation",
    "Figure rendering and validation",
    "Bibliography management"
  ],
  "contextMap": {
    "US001": {
      "references": ["docs/problem_statement.md"],
      "code_files": ["src/experiment.py"],
      "experiments": ["results/exp1_output.json"]
    }
  },
  "userStories": [
    {
      "id": "US001",
      "title": "Write Introduction",
      "acceptanceCriteria": [
        "Read problem statement",
        "Write 300-500 words",
        "Include motivation and scope"
      ],
      "priority": 1,
      "passes": false
    }
  ]
}
```

## 🔄 The Workflow

### Phase 1-8: AI Prepares
AI system analyzes your project and generates a smart PRD

### Phase 9: User Confirmation ⭐
AI shows you the plan:
```
STRUCTURE:
- 6 sections to write (Intro, Literature, Methods, Results, Discussion, Conclusion)

RESOURCES TO READ:
- Code: src/model.py, src/experiment.py
- Data: results/output.json, results/plots.png
- References: refs/methodology.bib

REQUIRED SKILLS:
✓ QMD formatting (using Quarto Authoring)
✓ Figure rendering (using Quarto)
✓ Bibliography management (using Citation Manager)

Confirm? (yes/no/adjust)
```

You approve or request changes. **No automation without your permission.**

### Phase 10-13: Ralph Executes
Ralph runs the PRD, monitoring progress and handling errors

## 💡 Why Ralph?

### ✅ Intelligent Automation
Your AI understands the actual project structure and generates a tailored plan

### ✅ Human Oversight
You review and approve the plan before automation begins

### ✅ Graceful Handling
Full pause/resume capability, progress persistence, and error handling

### ✅ Context Awareness
contextMap ensures Ralph has all needed context for each task

### ✅ Flexible & Extensible
Support for custom task types, skills, and workflows

## 📦 Project Structure

```
ralph/
├── ralph.mjs                 # CLI entry point
├── SKILL.md                  # Skill documentation
├── README.md                 # This file
├── daemon/
│   ├── server.mjs           # HTTP daemon
│   ├── session-manager.mjs  # Session management
│   ├── turn-engine.mjs      # Execution engine
│   ├── storage.mjs          # Data persistence
│   └── ui.html              # Web UI
├── prompts/
│   ├── base.md              # Base instructions
│   ├── content.md           # Content PRDs
│   ├── code.md              # Code PRDs
│   ├── research.md          # Research PRDs
│   ├── data.md              # Data PRDs
│   ├── devops.md            # DevOps PRDs
│   ├── testing.md           # Testing PRDs
│   └── orchestrator.md      # Complex workflows
├── docs/
│   ├── AI_WORKFLOW.md       # 13-phase workflow guide
│   ├── PRD_GENERATOR.md     # PRD generation guide
│   └── [other guides]
└── examples/
    ├── mcm-paper-prd.json   # Sample PRD
    └── MCM_PAPER_GUIDE.md   # Usage example
```

## 🔗 Integration

Ralph works seamlessly with:
- **Claude Agent SDK** - Turn-by-turn execution
- **Command-line AI systems** - Claude, other AI models
- **Custom skills** - Extend with your own tools
- **Version control** - Git integration for code PRDs
- **File systems** - Any project structure

## 📝 Example: Writing a Paper

```bash
# User: "Use Ralph to write my research paper"
# ↓
# AI analyzes: src/, data/, refs/ folders
# ↓
# AI checks: Quarto Authoring, Quarto Rendering skills available
# ↓
# AI generates PRD with:
#   - 6 user stories (sections)
#   - contextMap pointing to code, data, references
#   - requiredSkills: ["QMD formatting", "Figure rendering", ...]
# ↓
# AI shows PRD to user
# ↓
# User: "Looks good!"
# ↓
ralph.mjs create --prd generated_prd.json --start
# ↓
# Ralph executes all stories
# ↓
# You have a complete, polished research paper!
```

## 🛠️ Commands

### Session Management

```bash
# Create a new session
ralph.mjs create --prd <prd-file> [--start]

# List all sessions
ralph.mjs list

# Get session status
ralph.mjs status <session-id>

# Start a session
ralph.mjs start <session-id>

# Pause a session
ralph.mjs pause <session-id> --reason "..."

# Resume a session
ralph.mjs resume <session-id> --guidance "..."

# Inject guidance during execution
ralph.mjs inject <session-id> --message "..."

# Abort a session
ralph.mjs abort <session-id>

# Destroy a session (delete completely)
ralph.mjs destroy <session-id>
```

### Monitoring

```bash
# View session logs
ralph.mjs logs <session-id>

# Follow logs in real-time
ralph.mjs logs <session-id> --follow

# Show session tree (parent-child relationships)
ralph.mjs tree <session-id>

# List child sessions
ralph.mjs children <session-id>
```

## 🤝 Contributing

Ralph is designed to be extended. You can:

- Create custom task types (add new `prompts/{type}.md`)
- Develop new skills (integrate with your AI system)
- Extend the turn engine (add new command types)
- Customize the storage layer

## 📄 License

MIT

## 🤔 FAQ

**Q: Do I need to write PRDs manually?**
A: No! Your AI system generates them automatically. You just review and confirm.

**Q: Can I pause execution?**
A: Yes, anytime. Ralph persists all progress and can resume with corrections.

**Q: What if Ralph makes a mistake?**
A: Inject guidance with `ralph.mjs inject`, and Ralph adjusts on the next turn.

**Q: Can Ralph handle complex projects?**
A: Yes! Use the "orchestrator" task type or enable sensitive tool approvals.

**Q: What's a contextMap?**
A: A mapping of user story IDs to the files Ralph needs to read for that story. It ensures Ralph has all context.

**Q: Can I use Ralph with my own AI system?**
A: Yes! Ralph uses the Claude Agent SDK and can be adapted for other models.

---

**Ready to get started?** Check out [SKILL.md](SKILL.md) or [docs/AI_WORKFLOW.md](docs/AI_WORKFLOW.md).
