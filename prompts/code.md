# Code PRD - Software Implementation

This PRD involves implementing code. Adapt these guidelines to your specific project type.

## Before Starting

### 1. Detect Project Type
Check the project structure to understand what you're working with:
- **JavaScript/TypeScript**: Look for `package.json`
- **Python**: Look for `setup.py`, `pyproject.toml`, or `requirements.txt`
- **Go**: Look for `go.mod`
- **Rust**: Look for `Cargo.toml`
- **Java**: Look for `pom.xml` or `build.gradle`
- **C#/.NET**: Look for `.sln` or `project.csproj`

### 2. Check for Git Workflow
If PRD has `branchName`:
1. Ensure you're on the correct branch
2. If not, check it out or create from main

## Quality Requirements

**General:**
- Keep changes focused and minimal
- Follow existing code patterns in the codebase
- Only commit working code

**Language/Framework Specific:**
- **JavaScript/TypeScript**: `npm run typecheck` (or equivalent type checking)
- **Python**: Type checking with `mypy` or `pyright` if configured
- **Go**: `go vet`, `gofmt`
- **Rust**: `cargo check`, `cargo fmt`

If the project has quality check scripts, run them before committing.

## After Completing Work (between base steps 6 and 7)

After executing the acceptance criteria but before marking the story as passing:

1. **Run available quality checks** (whatever applies to the project):
   - Type checking if available
   - Linting if available
   - Tests if available

2. **Commit changes** with message: `feat: [Story ID] - [Story Title]`

## Git Commit Rules

- **NEVER use `git add -f` or `--force`** - If a file is gitignored, it should NOT be committed
- The PRD and progress log are gitignored intentionally - do not force-add them
- Only commit source code changes, not Ralph project tracking files
- If `git add` silently skips files, that's correct behavior - they're gitignored for a reason

## Update Documentation

Before committing, check if any edited files have learnings worth preserving:

Look for these documentation files in the project root:
- `CLAUDE.md` - Agent-specific patterns and gotchas
- `DEVELOPMENT.md` - Developer guide
- `README.md` - Project overview

If you discover **reusable patterns** that future developers/agents should know:
- API patterns or conventions specific to that module
- Gotchas or non-obvious requirements
- Dependencies between files
- Testing approaches for that area
- Setup or environment requirements

**Examples of good additions:**
- "When modifying X, also update Y to keep them in sync"
- "This module uses pattern Z for all operations"
- "Tests require the dev server running on PORT 3000"

**Do NOT add:**
- Story-specific implementation details
- Temporary debugging notes
- Information already in progress log

## Important for Code PRDs

- Commit frequently - one logical change per commit
- Keep the main branch working
- Test before committing when possible
