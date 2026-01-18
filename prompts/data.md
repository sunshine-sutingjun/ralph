# Data PRD - Data Processing and Analysis

This PRD involves data tasks: ETL (Extract-Transform-Load), data cleaning, analysis, reports, or data pipeline work.

## Key Differences

**You do NOT:**
- Commit code changes (data processing, not software development)
- Run typecheck (no code PRD quality requirements)
- Work on a git branch (unless specifically for data pipeline code)

**You DO:**
- Write data processing scripts (Python, SQL, etc.)
- Clean and transform datasets
- Perform data analysis and generate insights
- Create data visualizations and reports
- Save processed data as CSV, JSON, or database formats
- Update shared state files or data repositories

## Data Task Types

### ETL Tasks
Extract data from sources → Transform it → Load to destination

### Data Cleaning
- Remove duplicates
- Handle missing values
- Standardize formats
- Fix data inconsistencies

### Analysis Tasks
- Descriptive statistics
- Trend analysis
- Correlation analysis
- Aggregations and grouping

### Report Generation
- Create visual reports
- Generate summary statistics
- Produce charts and graphs
- Create data-driven dashboards

## Workflow

1. **Understand the data** - Read source files, understand schema
2. **Define transformations** - Write scripts to process data
3. **Test on sample** - Run on small subset first
4. **Process full dataset** - Execute on complete data
5. **Validate output** - Check for quality and completeness
6. **Generate report** - Create summary and visualizations
7. **Save artifacts** - Store processed data and reports

## Common Tools

- **Python**: pandas, numpy, scipy, matplotlib
- **SQL**: data warehouses, transformations
- **Shell scripts**: simple data pipelines
- **Data formats**: CSV, JSON, Parquet, SQL databases

## Quality Checklist

- Data validation: Check record counts before/after
- Error handling: Log any skipped or problematic records
- Documentation: Explain transformations in comments
- Reproducibility: Scripts should be runnable multiple times
- Performance: Optimize for large datasets if needed

## Report Format

```markdown
# [Dataset Name] - Data Analysis Report

**Date**: [date]
**Data Source**: [file or system]
**Records Processed**: X
**Time Range**: [if applicable]

## Summary
[Key findings at a glance]

## Dataset Overview
- Total Records: X
- Fields: X
- Time Period: [if applicable]

## Key Metrics
| Metric | Value |
|--------|-------|
| Count | X |
| Average | Y |

## Findings
[Insights and patterns discovered]

## Data Quality
- Missing values: X%
- Duplicates: X
- Anomalies: [describe]

## Recommendations
- [Action item 1]
- [Action item 2]

## Output Files
- `processed_data.csv` - Cleaned dataset
- `analysis_results.json` - Computed metrics
```

## Important for Data PRDs

- Document data transformations clearly
- Keep raw data as backup
- Version processed datasets
- Log all transformations
- Update progress with data patterns discovered
