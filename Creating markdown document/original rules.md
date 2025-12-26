
# 1
Always start a page with a table of content: [[_TOC_]]
Followed by the version (this is a link to the final section fo the document) and author (not you, the agent, but the human who instructed you)

# 2
Start with a very brief statement about **what** this document is about / helps the reader to do
Where applicable, the **what** above is followed by a section on **why** this is required - again, keep this short. 
This section is for my CTO / CEO. 

# 3 (optional - applies to wiki documentation only)
The next section is called 'Quick Start Checklist'
this is the most important section, it lists all the 'actions' that have to be taken (and who is responsible), current right through the fluff. 
each action links to antoher part of the wiki document, where the action is explained in greater details (what ever level is required for someone who has never done this) . 

# 4-n
All further sections the contain the details and background info etc for the actions above. 

# n+1
The final seciton: version history table: when, who & a brief what

# Markdown Formatting Rules


## Markdown Table Formatting 

**Tables must have aligned columns for readability in raw markdown.**

When creating tables in documentation, pad columns so they align when viewing the raw `.md` file:

**✅ CORRECT - Columns aligned with padding:**
```markdown
| Option                     | Monthly Cost          | Uptime            |
|----------------------------|-----------------------|-------------------|
| **A. Client-Hosted VM**    | $0 (existing infra)   | 24/7              |
| **B. Container Apps**      | ~$1-5                 | On-demand         |
```

**❌ WRONG - Columns not aligned:**
```markdown
| Option | Monthly Cost | Uptime |
|--------|-------------|--------|
| **A. Client-Hosted VM** | $0 (existing infra) | 24/7 |
| **B. Container Apps** | ~$1-5 | On-demand |
```

**Why this matters:**
- Documentation is read in raw form (GitHub, editors, diffs)
- Aligned tables are scannable without rendering
- Professional appearance signals quality

**Tips:**
- Use consistent padding within each column
- Header separator (`|---|`) should match column width
- Longest cell content determines column width