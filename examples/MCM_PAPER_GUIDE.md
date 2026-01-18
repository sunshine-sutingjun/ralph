# MCM Paper Writing - Example Guide

This guide shows how to set up Ralph to write an academic paper (like MCM - Mathematical Contest in Modeling).

## Project Structure

```
mcm-paper/
├── prd.json                 # Main PRD with contextMap and requiredSkills
├── problems/
│   └── problem_statement.md # The competition problem description
├── references/
│   ├── introduction.bib
│   ├── literature_review.bib
│   ├── methods.bib
│   ├── discussion.bib
│   ├── conclusion.bib
│   ├── background.md        # Background reading materials
│   └── key_papers.md        # Summary of key papers
├── docs/
│   ├── literature_guide.md  # Notes on what to cover in lit review
│   ├── methodology_notes.md # Technical notes on your approach
│   ├── results_guide.md     # Overview of experiments
│   └── results_usage.md     # Maps each result to which paper section(s) should use it
├── src/
│   ├── model.py             # Mathematical model implementation
│   ├── algorithms.py        # Algorithms
│   ├── experiment1.py       # Experiment 1 code
│   ├── experiment2.py       # Experiment 2 code
│   └── experiment3.py       # Sensitivity analysis
├── results/
│   ├── exp1_output.json     # Experiment 1 results
│   ├── exp1_plot.png        # Experiment 1 visualization
│   ├── exp2_output.json     # Experiment 2 results
│   ├── exp2_plot.png        # Experiment 2 visualization
│   ├── exp3_sensitivity.json
│   └── exp3_heatmap.png
└── paper/
    ├── paper.qmd            # Main QMD file (generated/edited by Ralph)
    └── paper.pdf            # Final output
```

## Key Concepts

### requiredSkills - Declarative Capability Needs

The `requiredSkills` field describes what capabilities the project needs:

```json
"requiredSkills": [
  "QMD formatting and mathematical notation support",
  "Figure and visualization insertion",
  "Document compilation and rendering"
]
```

**How it works:**
- Ralph declares what it needs (e.g., "QMD formatting support")
- Your AI reads this and says "I have a qmd-writing skill that does that"
- Your AI automatically calls the right skill when needed
- Different AI systems can use different skill names - it's flexible

Ralph doesn't hardcode skill names. It describes what's needed, and your AI figures out what it has available.

The `contextMap` in the PRD tells Ralph what to read before writing each section:

```json
"contextMap": {
  "results": {
    "explanation": "docs/results_guide.md",
    "result_map": "docs/results_usage.md",
    "experiments": [
      {
        "name": "experiment_1",
        "code": "src/experiment1.py",
        "output": "results/exp1_output.json",
        "visualization": "results/exp1_plot.png"
      }
    ]
  }
}
```

Ralph will:
1. Read `results_guide.md` to understand the experiment context
2. Read `results_usage.md` to see which results go where
3. Read each experiment's code, output, and visualization
4. Incorporate them into the paper section

### requiredSkills

The `requiredSkills` field lists skills Ralph should use:

```json
"requiredSkills": ["qmd-writing", "qmd-rendering"]
```

Ralph will call these skills when:
- **qmd-writing**: Formatting equations, code blocks, cross-references
- **qmd-rendering**: Compiling QMD, previewing figures, debugging format issues

## Example: results_usage.md

This file maps experimental results to paper sections:

```markdown
# Results Usage Guide

## Experiment 1: Small-scale test case
- **File**: results/exp1_output.json
- **Visualization**: results/exp1_plot.png
- **Used in**: Results section, first subsection
- **Interpretation**: Shows that the model works correctly on simple cases
- **Key metrics to mention**: accuracy, runtime
- **How to present**: Include plot and table of metrics

## Experiment 2: Large-scale validation
- **File**: results/exp2_output.json
- **Visualization**: results/exp2_plot.png
- **Used in**: Results section, main results
- **Interpretation**: Validates model on real-world data
- **Key metrics to mention**: accuracy, precision, recall
- **How to present**: Multiple plots showing different aspects

## Experiment 3: Sensitivity analysis
- **File**: results/exp3_sensitivity.json
- **Visualization**: results/exp3_heatmap.png
- **Used in**: Discussion section
- **Interpretation**: Shows robustness to parameter variations
- **Key metrics to mention**: parameter ranges, sensitivity values
- **How to present**: Heatmap with annotations
```

## Running Ralph for Paper Writing

```bash
# Create and start the writing session
ralph.mjs create --prd path/to/mcm-paper/prd.json --start

# Monitor progress
ralph.mjs logs <session-id> --follow

# If Ralph gets stuck, inject guidance
ralph.mjs inject <session-id> --message "Focus on explaining the key results clearly"

# After all sections are written
ralph.mjs status <session-id>
```

## What Ralph Will Do

1. **Read the PRD** - Understand the paper structure and requirements
2. **For each section (US001-US006)**:
   - Read context from `contextMap[sectionId]`
   - Read referenced documents and code
   - Write the section
   - Use qmd-writing and qmd-rendering skills as needed
3. **For final section (US007)**:
   - Compile the entire QMD document
   - Verify all formatting
   - Generate final PDF

## Tips for Success

1. **Be specific in contextMap** - Include all files Ralph needs to understand each section
2. **Write clear result_map** - Ralph needs to know why each experiment matters
3. **Reference explanations** - Add notes in docs/ about your approach and models
4. **Include code comments** - Help Ralph understand your implementations
5. **Provide BibTeX files** - Make it easy for Ralph to cite sources

## Customization

You can adapt this approach for:
- Thesis chapters (change outline structure)
- Blog posts (shorter sections)
- Research papers (longer, more complex structure)
- Technical reports (mix of code, analysis, and narrative)
