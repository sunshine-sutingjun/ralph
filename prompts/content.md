# Content PRD - Documentation and Writing

This PRD involves creating content: documentation, blogs, articles, guides, papers, or other written materials.

## Key Differences

**You do NOT:**
- Commit code changes (you're writing, not implementing)
- Run typecheck or tests (no code changes)
- Work on a git branch (unless specifically asked)

**You DO:**
- Write or edit documentation
- Create guides, tutorials, blog posts, or papers
- Edit existing content for clarity and completeness
- Create markdown/QMD files with polished, publication-ready content
- Use required skills when formatting or inserting media

## Content Types

- **Documentation**: API docs, guides, tutorials, handbooks
- **Papers/Theses**: Research papers, academic writing, dissertations
- **Blog Posts**: Articles, technical deep-dives, announcements
- **User Guides**: How-to guides, FAQs, troubleshooting
- **Release Notes**: Changelog entries, upgrade guides
- **Marketing Copy**: Product descriptions, landing page content

## Reading Referenced Resources First

**IMPORTANT**: Before writing any section, always read all provided context:

1. **Check for contextMap** - If PRD has `contextMap[sectionId]`:
   - Read `problem_statement` files
   - Read all referenced documents in `references` array
   - Read code files listed in `code_files`
   - Read experiment outputs and explanations
   - Read the `result_map` document to understand which results apply where

2. **Review style and format** - Check for style guides or documentation standards
3. **Understand scope** - Read acceptance criteria completely
4. **Identify required skills** - If PRD lists `requiredSkills`, understand what they do

## Writing Workflow

1. **Read all context** - Problem statement, references, code, results (see above)
2. **Make notes** - Document key information to include
3. **Create outline** - Plan the structure for this section
4. **Write first draft** - Get the content down
5. **Format and insert media** - Use skills as needed
6. **Edit and refine** - Polish for clarity and completeness
7. **Verify output** - Use skills to check formatting if needed
8. **Save** - Commit to git if specified in acceptance criteria

## Using Required Skills

If the PRD specifies `requiredSkills`:

1. **Read skill documentation** before using
2. **Call skill appropriately** when:
   - Implementing special formatting (QMD, LaTeX, etc.)
   - Inserting figures, tables, or cross-references
   - Testing compilation or rendering
   - Debugging format issues

3. **Example skill usage**:
   ```
   Use the qmd-writing skill to format this code block correctly
   Use the qmd-rendering skill to verify the figure renders properly
   ```

## Quality Requirements

- **Clear and concise** - Use appropriate language for the audience
- **Well-structured** - Logical flow with proper headings
- **Complete** - Cover all aspects in acceptance criteria
- **Accurate** - Cite references, verify technical facts
- **Consistent** - Match existing style if updating existing content
- **Properly formatted** - Use correct markup for special formatting
- **Media properly inserted** - Figures, tables, code blocks formatted correctly

## Markdown and QMD Best Practices

- Use proper heading hierarchy (H1 for title, H2 for sections, etc.)
- Code snippets in proper fenced blocks with language specification
- Links properly formatted: `[text](url)`
- Tables for tabular data
- Bullet points and numbered lists as appropriate
- Bold for emphasis on key concepts
- **For QMD files**: Follow QMD syntax for executable code, figures, cross-references

## Common Content Patterns

### Academic/Research Paper Section
```markdown
## Methodology

[Opening paragraph introducing the approach]

### Mathematical Model
[Equations and notation, explained]

### Implementation
[How the model was implemented]
\`\`\`python
# Code example
\`\`\`
```

### Data/Results Section with Figures
```markdown
## Results

[Interpretation of results]

![Figure 1: Description](path/to/figure.png)

[Discussion of figure and what it shows]

[Next result discussion...]
```

### Section with Citations
```markdown
## Background

[Topic explanation with citations] [1][2].

[More detailed discussion referencing literature] [3].

### References
[1] Author et al. "Title". Journal, Year.
[2] ...
```
```

### FAQ Section
```markdown
## Q: Question here?
Answer with clear explanation and examples if needed.
```

## Important for Content PRDs

- Make content scannable - use headers and lists
- Include examples when helpful
- Proofread carefully
- Keep audience in mind
- Read all context before writing
- Use required skills to ensure proper formatting
- Cite sources appropriately
- Update progress with patterns about writing and content structure
