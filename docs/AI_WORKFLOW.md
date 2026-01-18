# Ralph AI Workflow - Step-by-Step

This document describes the exact workflow an AI should follow when using Ralph.

## When User Invokes Ralph

User says something like:
```
"Use Ralph to write my paper"
"Use Ralph to implement this feature"
"Use Ralph to analyze this dataset"
```

## AI Workflow

### Phase 1: Understand the Request

**AI Actions:**
1. Read the user's request
2. Understand the goal and scope
3. Ask clarifying questions if needed:
   - "What format should the paper be in?"
   - "What's the main goal of this implementation?"
   - "What's the dataset structure?"

**Output:** Clear understanding of what to do

### Phase 2: Analyze Project/Resources

**AI Actions:**
1. List files in the project directory (recursively)
2. Identify different categories:
   - Source code files (by language)
   - Data/Results files
   - Documentation files
   - Configuration files
   - Reference materials

3. Understand the structure by looking at:
   - File names and extensions
   - Directory organization
   - README or setup files
   - Existing documentation

**Example Output:**
```
Project Analysis:
- Language: Python
- Code: src/model.py, src/exp1.py, src/exp2.py
- Results: results/exp1.json, results/exp1.png, results/exp2.json
- References: refs/methodology.bib, refs/papers/
- Docs: docs/experiment_guide.md, README.md
- Config: requirements.txt, setup.py
```

### Phase 3: Identify Available Skills

**AI Actions:**
1. List all installed/available skills
2. For each skill, understand its capabilities
3. Note what it can do

**Example:**
```
Available Skills:
- qmd-writing: Can format QMD, handle equations, code blocks
- qmd-rendering: Can compile QMD, preview output, generate PDFs
- git: Can manage version control
- citation-manager: Can manage BibTeX, format citations
```

### Phase 4: Determine Task Type

**AI Decides:**
- Is this code development? → `taskType: "code"`
- Is this content/writing? → `taskType: "content"`
- Is this data analysis? → `taskType: "data"`
- Is this research? → `taskType: "research"`
- Is this infrastructure? → `taskType: "devops"`
- Is this testing? → `taskType: "testing"`
- Multiple coordinated tasks? → `taskType: "orchestrator"`

### Phase 5: Define User Stories

**AI Creates:**
1. List of work items to complete
2. Each story represents a logical unit of work
3. Ordered by priority/dependency

**For paper writing:**
```
- US001: Write Introduction (priority 1)
- US002: Write Literature Review (priority 1)
- US003: Write Methodology (priority 2)
- US004: Write Results (priority 2)
- US005: Write Discussion (priority 3)
- US006: Write Conclusion (priority 3)
```

**For code:**
```
- US001: Set up database schema (priority 1)
- US002: Create API endpoints (priority 1)
- US003: Add error handling (priority 2)
- US004: Write tests (priority 2)
```

### Phase 6: Build Context Map

**AI Maps each story to resources:**

For each user story:
1. What files/code does it need to understand?
2. What references or documentation applies?
3. What data or results will it use?
4. What explanations are relevant?

**Example for "Write Results":**
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
      },
      {
        "name": "exp2",
        "code": "src/exp2.py",
        "output": "results/exp2.json",
        "visualization": "results/exp2.png"
      }
    ]
  }
}
```

### Phase 7: Identify Required Skills

**AI Maps needs to skills:**

For the project, identify what capabilities are needed:
- "Document formatting" → AI has qmd-writing skill
- "Math notation" → AI has qmd-writing skill
- "Figure rendering" → AI has qmd-rendering skill
- "Bibliography management" → AI has citation-manager skill

**Create requiredSkills list** (describe needs, not names):
```json
"requiredSkills": [
  "Document formatting with mathematical notation",
  "Figure and chart rendering",
  "Bibliography and citation management",
  "Equation support"
]
```

### Phase 8: Generate Complete PRD

**AI Creates full PRD JSON:**
```json
{
  "description": "Write MCM competition paper",
  "taskType": "content",
  "branchName": "paper/mcm-2026",
  "requiredSkills": [ ... ],
  "contextMap": { ... },
  "userStories": [
    {
      "id": "US001",
      "title": "Write Introduction",
      "description": "Create compelling introduction",
      "section": "intro",
      "acceptanceCriteria": [
        "Read problem statement",
        "Read background.bib",
        "Write 300-500 words",
        "Include problem overview"
      ],
      "priority": 1,
      "passes": false
    }
    // ... more stories
  ]
}
```

### Phase 9: Validate PRD

**AI Checks:**
- [ ] All referenced files exist
- [ ] File paths are correct
- [ ] All stories have clear acceptance criteria
- [ ] Priorities make sense
- [ ] No circular dependencies
- [ ] All stories have `passes: false`

### Phase 10: Run Ralph

**AI Executes:**
```bash
ralph.mjs create --prd generated_prd.json --start
ralph.mjs logs <session-id> --follow
```

### Phase 11: Monitor Progress

**AI Watches:**
- Check logs periodically
- If Ralph gets stuck, inject guidance
- If issues arise, adjust contextMap or user stories

### Phase 12: On Completion

**AI Handles:**
- Verify all stories are complete
- Check output quality
- Provide summary to user
- Help with next steps

## Key Principles

### 1. Smart Analysis
Don't assume - actually scan and analyze:
- Real file structure
- Real available skills
- Real project dependencies

### 2. Contextual Mapping
Make contextMap as complete as possible:
- Better context = better work
- Include all relevant references
- Map data to where it's used

### 3. Capability Description
In requiredSkills, describe what's needed:
- NOT: `["qmd-writing"]`
- YES: `["Document formatting with mathematical notation"]`

### 4. Atomic Stories
Make user stories independent:
- Each can be done in one iteration
- Clear entry and exit criteria
- Minimal dependencies

### 5. Prioritization
Order by dependency and importance:
- Foundation first (databases, setup)
- Core features next
- Polish and testing last

### 6. Error Handling
If anything is missing:
- Ask the user
- Make reasonable assumptions
- Document what you assumed
- Be ready to regenerate PRD

## Example: Complete Workflow

**User:** "Write my MCM paper. Code in src/, results in results/, references in refs/."

**AI Step 1:** Understand → Paper writing in QMD format

**AI Step 2:** Analyze project
```
Found:
- src/: model.py, exp1.py, exp2.py
- results/: exp1.json, exp1.png, exp2.json, exp2.png
- refs/: methodology.bib, background.bib
- docs/: experiment_guide.md, README.md
```

**AI Step 3:** Check skills
```
Available: qmd-writing, qmd-rendering, citation-manager
```

**AI Step 4:** taskType → "content"

**AI Step 5:** Create stories
```
- US001: Intro
- US002: Literature
- US003: Methodology
- US004: Results
- US005: Discussion
- US006: Conclusion
```

**AI Step 6-8:** Build full PRD with contextMap

**AI Step 9:** Validate ✓

**AI Step 10:** Run Ralph
```bash
ralph.mjs create --prd mcm_paper.json --start
```

**AI Step 11:** Monitor and provide feedback

**User gets:** Complete paper! 🎉

## Common Issues and Solutions

### Issue: File not found in contextMap
- **Check:** Does file actually exist?
- **Fix:** Scan project again, correct paths
- **Regenerate:** PRD with correct paths

### Issue: Ralph can't find a reference
- **Check:** Is the reference listed in contextMap?
- **Fix:** Add missing reference
- **Regenerate:** PRD with complete contextMap

### Issue: Skill capability mismatch
- **Check:** Does your AI have the needed skill?
- **Fix:** Install the missing skill OR change approach
- **Regenerate:** PRD with different requiredSkills

### Issue: Stories are too big
- **Check:** Can each story be done in one iteration?
- **Fix:** Break into smaller stories
- **Regenerate:** PRD with more, smaller stories
