# Content PRD - Documentation and Writing

This PRD involves creating content: documentation, blogs, articles, guides, or other written materials.

## Key Differences

**You do NOT:**
- Commit code changes (you're writing, not implementing)
- Run typecheck or tests (no code changes)
- Work on a git branch (unless specifically asked)

**You DO:**
- Write or edit documentation
- Create guides, tutorials, or blog posts
- Edit existing content for clarity and completeness
- Create markdown files with polished, publication-ready content

## Content Types

- **Documentation**: API docs, guides, tutorials, handbooks
- **Blog Posts**: Articles, technical deep-dives, announcements
- **User Guides**: How-to guides, FAQs, troubleshooting
- **Release Notes**: Changelog entries, upgrade guides
- **Marketing Copy**: Product descriptions, landing page content

## Writing Workflow

1. **Review guidelines** - Check for style guides or documentation standards in the project
2. **Research context** - Understand what you're documenting
3. **Create outline** - Plan the structure and flow
4. **Write first draft** - Get the content down
5. **Edit and refine** - Polish for clarity, grammar, and completeness
6. **Review checklist** - Verify all acceptance criteria are met
7. **Save/commit** - Save content files (commit to git if specified)

## Quality Requirements

- **Clear and concise** - Use simple language, short sentences
- **Well-structured** - Logical flow with good headings
- **Complete** - Cover all aspects mentioned in acceptance criteria
- **Accurate** - Verify technical facts and code examples
- **Consistent** - Match existing documentation style if updating existing content

## Markdown Best Practices

- Use proper heading hierarchy (H1 for title, H2 for sections, etc.)
- Code snippets in proper fenced blocks with language specification
- Links properly formatted: `[text](url)`
- Tables for tabular data
- Bullet points and numbered lists as appropriate
- Bold for emphasis on key concepts

## Common Content Patterns

### API Documentation
```markdown
### `methodName(params)`

**Parameters:**
- `param1` (type) - Description

**Returns:** Return type description

**Example:**
\`\`\`js
// Code example
\`\`\`
```

### Tutorial/Guide
```markdown
## Step 1: [Title]
Description and context

\`\`\`
code or commands
\`\`\`

## Step 2: [Title]
...
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
- Update progress with patterns about documentation style/structure
