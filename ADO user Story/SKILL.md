---
name: ado-user-stories
description: Create, update, and improve Azure DevOps user stories. Use when asked to create user story, write user story, update user story, improve user story, refine user story, or work with ADO items. Handles Description field (HTML) and Acceptance Criteria field separately.
---

# ADO User Stories

## Workflow

1. **Fetch**: When given an ADO number (e.g., 1234), fetch via MCP server using work item ID
2. **Edit**: Create/modify content following templates below
3. **Update**: Push changes via MCP server (default) unless user requests output only

## ADO Links

- Work item URL: `https://dev.azure.com/NationalEducationUnion/Membership%20System%20Replacement/_workitems/edit/{ADO-number}`
- Internal link format (for referencing other stories):
  ```html
  <a href="https://dev.azure.com/NationalEducationUnion/Membership%20System%20Replacement/_workitems/edit/{number}/" data-vss-mention="version:1.0">#{number}</a>
  ```

## Description Field Template (HTML)

Use this structure. Remove irrelevant sections during refinement but start complete:

```html
<div>
<p style="box-sizing:border-box;font:18px &quot;Segoe UI&quot;;margin:0px 0px 14.9px;"><b>Client Requirement</b></p>
<p style="box-sizing:border-box;font:14px &quot;Segoe UI&quot;;margin:0px;">[Requirement text here]</p>

<p style="box-sizing:border-box;font:14px &quot;Segoe UI&quot;;margin:0px;"><br></p>
<p style="box-sizing:border-box;margin:0px;font-family:&quot;Segoe UI&quot;;"><b>Data Migration</b> (optional)</p>
<p style="box-sizing:border-box;font:14px &quot;Segoe UI&quot;;margin:0px;">[Consider: treating "existing/old" data/records differently]</p>

<p style="box-sizing:border-box;font:14px &quot;Segoe UI&quot;;margin:0px;"><br></p>
<p style="box-sizing:border-box;font:14px &quot;Segoe UI&quot;;margin:0px;"><b>Process diagrams</b></p>
<p style="box-sizing:border-box;font:14px &quot;Segoe UI&quot;;margin:0px;">Figjam link: [link]</p>

<p style="box-sizing:border-box;font:14px &quot;Segoe UI&quot;;margin:0px;"><br></p>
<p style="box-sizing:border-box;margin:0px;font-family:&quot;Segoe UI&quot;;"><b>Assumptions</b> (optional)</p>
<p style="box-sizing:border-box;font:14px &quot;Segoe UI&quot;;margin:0px;">[Assumptions list]</p>

<p style="box-sizing:border-box;font:14px &quot;Segoe UI&quot;;margin:0px;"><br></p>
<p style="box-sizing:border-box;font:18px &quot;Segoe UI&quot;;margin:0px 0px 14.9px;"><b>Proposed Technical Approach</b></p>
<p style="box-sizing:border-box;font:14px &quot;Segoe UI&quot;;margin:0px;">[Technical approach details]</p>

<p style="box-sizing:border-box;font:14px &quot;Segoe UI&quot;;margin:0px;"><br></p>
<p style="box-sizing:border-box;margin:0px;font-family:&quot;Segoe UI&quot;;"><b>Prerequisites</b> (optional)</p>
<p style="box-sizing:border-box;font:14px &quot;Segoe UI&quot;;margin:0px;">[e.g.: SPO set up, Customer Insights configured, outgoing mailboxes defined & available]</p>
</div>
```

## Acceptance Criteria Field

**Always use the dedicated AC field, not the Description field.**

### Format (strict)

```
**Feature: [Feature Title]**

**AC1: [Scenario Name]**
**Given** [precondition]
**When** [action]
**Then** [expected outcome]
**And** [additional outcome if needed]

**AC2: [Scenario Name]**
**Given** [precondition]
**When** [action]
**Then** [expected outcome]
```

### Rules

- Number ACs sequentially (AC1, AC2, AC3...)
- Bold all keywords: **Given**, **When**, **Then**, **And**
- Bold AC headers: **AC1: Name**
- Each AC tests one scenario
- Label assumptions needing verification when scenarios aren't explicitly described

## Client Review Highlighting

Items requiring client sign-off/review: <span style="background-color:yellow;">[client review]</span>

## Parent Linking

When parent item provided, set the parent work item link in ADO.