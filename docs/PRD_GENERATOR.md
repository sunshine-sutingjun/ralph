# Ralph PRD Generator - Guide for AI Systems

This guide helps AI systems automatically analyze projects and generate PRDs (Project Requirements Documents) for Ralph.

**Note**: This is the technical guide for AI systems. Users don't need to read this - they just tell their AI "use Ralph" and the AI handles PRD generation automatically.

## PRD Generation Workflow

### Step 1: Understand the Task

Ask or infer:
- **What is the goal?** (e.g., "write paper", "implement feature", "analyze data")
- **What task type?** (code, research, content, data, devops, testing, orchestrator)
- **What's the scope?** (single item or multi-part project)
- **Is git involved?** (for code PRDs)

### Step 2: Analyze Project Structure

Scan the project directory to find:

```
Key elements to identify:
├── Source code
│   └── What files, what languages?
├── Documentation
│   ├── README.md, docs/, etc.
│   └── Existing guides or explanations
├── Data/Results
│   ├── Input data files
│   ├── Output/result files
│   └── Visualizations
├── References
│   ├── BibTeX files (.bib)
│   ├── Papers (PDFs, markdown)
│   └── External links
└── Configuration
    ├── package.json, setup.py, Cargo.toml, etc.
    └── Environment or build files
```

### Step 3: Check Available Skills

Identify which skills are installed/available:
```
Commands to check:
- List available skills
- Understand what each skill does
- Note their capabilities
```

Examples:
- "web-automation" → can interact with browsers
- "database-tools" → can query databases
- "qmd-writing" → can format QMD documents
- "git" → can version control
- "visualization" → can create charts

### Step 4: Map Task to User Stories

Break the task into user stories based on the project structure.

**For a paper writing project:**
- US001: Write Introduction
- US002: Write Literature Review
- US003: Write Methodology
- US004: Write Results
- US005: Write Discussion
- US006: Write Conclusion

**For a code project:**
- US001: Set up database
- US002: Create API endpoints
- US003: Add authentication
- US004: Write tests
- US005: Deploy

### Step 5: Build contextMap

For each user story, identify what resources it needs:

```json
"contextMap": {
  "write_results": {
    "references": [
      "refs/methodology.bib",
      "docs/experiment_guide.md"
    ],
    "code_files": [
      "src/experiment1.py",
      "src/experiment2.py"
    ],
    "explanation": "docs/results_interpretation.md",
    "experiments": [
      {
        "name": "exp1",
        "code": "src/exp1.py",
        "output": "results/exp1.json",
        "visualization": "results/exp1.png"
      }
    ]
  }
}
```

**What to look for:**
- Referenced files in the project
- Code files that need to be understood
- Data/results files that will be used
- Documentation explaining the context
- Dependencies between files

### Step 6: Identify requiredSkills

Match project needs to available skills:

```
Project needs:          Your AI has:          Map to:
---------              ----------            -------
QMD formatting    →    qmd-writing       →   "QMD formatting support"
Figure rendering  →    qmd-rendering     →   "Figure and chart rendering"
Code analysis     →    code-analysis     →   "Code understanding and refactoring"
Git operations    →    git-cli           →   "Version control"
Data processing   →    pandas-tools      →   "Data manipulation and analysis"
```

Describe capabilities, not exact skill names:
```json
"requiredSkills": [
  "Document formatting with mathematical notation",
  "Code repository management",
  "Dependency resolution",
  "Unit test framework"
]
```

### Step 7: Build the Complete PRD

Assemble everything:

```json
{
  "description": "Write MCM competition paper",
  "taskType": "content",
  "branchName": "paper/mcm-2026",
  "requiredSkills": [
    "Document formatting with mathematical notation",
    "Figure and visualization support",
    "Citation and bibliography management"
  ],
  "contextMap": {
    // ... (from Step 5)
  },
  "userStories": [
    {
      "id": "US001",
      "title": "Write Introduction",
      "section": "intro",
      "acceptanceCriteria": [
        "Read problem statement",
        "Read background references",
        "Write 300-500 word introduction",
        "Include problem overview and motivation"
      ],
      "priority": 1,
      "passes": false
    }
    // ... more stories
  ]
}
```

## Example: Paper Writing PRD Generation

User says: "Write my MCM paper. Code in src/, results in results/, refs in refs/."

Your AI analyzes:

```
Detected structure:
├── src/
│   ├── model.py
│   ├── experiment1.py
│   ├── experiment2.py
│   └── algorithms.py
├── results/
│   ├── exp1_output.json
│   ├── exp1_plot.png
│   ├── exp2_output.json
│   └── exp2_plot.png
├── refs/
│   ├── methodology.bib
│   ├── background.bib
│   └── papers/
└── docs/
    ├── problem_statement.md
    └── experiment_guide.md

Available skills: qmd-writing, qmd-rendering, citation-manager

Generated PRD:
- taskType: "content"
- writingFormat: "qmd"
- outline: [intro, literature, methodology, results, discussion, conclusion]
- contextMap: Maps each section to relevant code, results, references
- requiredSkills: [
    "QMD document formatting",
    "Mathematical notation support",
    "Figure insertion and rendering"
  ]
- userStories: One per section + one for final assembly
```

## Before Running Ralph

**Important**: After generating a PRD, show it to the user for confirmation before executing Ralph.

The user should see:
- **Description**: What will Ralph do?
- **Task Type**: What category of work?
- **Outline**: What are the steps?
- **Resources**: What files will be read?
- **Skills**: What capabilities will be used?
- **Stories**: What will be accomplished?

Ask: "Does this plan look good? Approve to proceed, or tell me what to adjust."

This prevents Ralph from executing a poorly-generated plan.

## Validation Checklist

Before showing the PRD to user, verify:

- [ ] All files referenced in contextMap exist
- [ ] File paths are correct
- [ ] User stories cover all outlined sections
- [ ] Acceptance criteria are specific and testable
- [ ] requiredSkills match available capabilities
- [ ] taskType matches the work (code vs content vs data, etc.)
- [ ] Priority ordering makes sense
- [ ] All stories have `passes: false` (starting state)

## Handling Edge Cases

### No Obvious Structure
If the project is unstructured:
- Ask the user for clarification
- Suggest a structure based on the task type
- Let user confirm before proceeding

### Missing Documentation
If some context is missing:
- Note it in the PRD
- Add placeholder contextMap entries
- Tell Ralph to create those docs if needed

### Complex Dependencies
If stories have complex dependencies:
- Use `priority` field to sequence them
- Add notes about dependencies in `acceptanceCriteria`
- Consider breaking into smaller user stories

### Multiple Skill Matches
If multiple skills could do the same job:
- Describe what's needed in `requiredSkills`
- Let your AI choose the best available skill
- Ralph doesn't assume specific skill names

## Tips for Better PRD Generation

1. **Be thorough in file scanning** - Ralph needs to know about all relevant files
2. **Create detailed contextMap** - Better context = better writing
3. **Make user stories atomic** - Each story should be completable independently
4. **Prioritize correctly** - Order matters for multi-part projects
5. **Don't hardcode skill names** - Describe capabilities instead
6. **Validate before running** - Check the generated PRD makes sense
7. **Ask when uncertain** - Better to confirm than to guess

## Feedback Loop

If Ralph has issues:
1. Review the generated PRD
2. Check if contextMap is complete
3. Verify all referenced files exist
4. Confirm requiredSkills match your capabilities
5. Adjust and regenerate if needed
