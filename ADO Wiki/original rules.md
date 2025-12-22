Working with ADO Wiki articles - skill


# 1
Always start a page with a table of content: [[_TOC_]]
Followed by the version (this is a link to the final section fo the document) and author (not you, the agent, but the human who instructed you)

# 2
Start with a very breif statement about what this documents help the rader to do
The what above is followed by a section on why this is required - again, keep this short. 

# 3
The next section is called 'Quick Start Checklist'
this is the most important section, it lists all the 'actions' that have to be taken (and who is responsible), current right through the fluff. 
each action links to antoher part of the wiki document, where the action is explained in greater details (what ever level is required for someone who has never done this) . 

# 4-n
All further sections the contain the details and background info etc for the actions above. 

# n+1
The final seciton: version history table: when, who & a brief what


# General instructions
## Usage of '#' for headers
The table of content needs to show the most important headers only. 
Therefore, to avoid showing too many items in the TOC, use '#' (and all smaller headings) sparingly, preferably in a way where only the main actions with max 1-3 sub-headers show in the TOC - but try to avoid sub-headers alltogether and use ** ** instead

## header formatting
Add this to the line above every header: <!--⭐️Header⭐️-->
It makes the md file more readable for humans, that way they can identify the relevant header easily. 

## Shorter is better
To update a wiki page you (the agent) have to re-write the full document each time - therefore, to make this more effiecient, do nto shy away from moving 'longer' steps/actions/section into sub-pages in the wiki - in that case clearly link and back link betweem them. 

## Links
Include all links like this: <a href="placeholder.com" target="_blank">Open in new tab: </a>

## Colour
Dont be shy to use colour to make important information stand out - use this syntax: <span style="color:red">Pending - WIP</span> 

## Additional / Background information
To allow the user to focus on the important aspects of the document, 'hide' all 'explanatory' bit using this syntax: 

```
<details>
  <summary style="color: darkgrey; text-decoration: underline;">Explanation/Reasoning/Screenshots</summary>

<br>

{add content here}

<br>

</details>
<br>
```

# Azure DevOps Wiki Update Instructions

## The Problem

When using `RTPI-ADO-beta:update-wiki-page` to update an **existing** wiki page, the API returns a 500 error with message:
```
"The page '/Page Name' specified in the add operation already exists in the wiki. Please specify a new page path."
```

This error is misleading - the actual issue is a **missing version parameter**.

## The Solution

**Always include the `version` parameter** when updating an existing wiki page.

### Correct Workflow

1. **Get the current page content AND version (ETag)**
```json
RTPI-ADO-beta:get-wiki-page
{
  "pagePath": "/SPO%2DSetup%2DGuide",
  "project": "RTPI",
  "wikiId": "5a23b2eb-0059-44f9-a233-24bc57dd6627",
  "includeContent": true
}
```

2. **Extract the version from the response**
```json
{
  "version": "\"990948f603ba55253206f2e0f525b9c8d5fb4fb4\"",
  ...
}
```

3. **Include version in the update call**
```json
RTPI-ADO-beta:update-wiki-page
{
  "content": "new content here",
  "pagePath": "/SPO%2DSetup%2DGuide",
  "project": "RTPI",
  "wikiId": "5a23b2eb-0059-44f9-a233-24bc57dd6627",
  "version": "\"990948f603ba55253206f2e0f525b9c8d5fb4fb4\""
}
```

## Key Points

| Scenario | Version Required? |
|----------|-------------------|
| `create-wiki-page` (new page) | No |
| `update-wiki-page` (existing page) | **YES** |
| `azuredevops-str-replace-wiki-page` | No (handled internally) |

## Why This Happens

The `version` parameter is the **ETag** for optimistic concurrency control. Azure DevOps uses it to:
- Prevent conflicting updates from multiple users
- Ensure you're updating the version you think you're updating

Without it, the API doesn't know if this is an update or a create, and fails with the confusing "already exists" error.

## Best Practice

When doing a full page rewrite:
1. Always call `get-wiki-page` first
2. Save the `version` value from the response
3. Pass it to `update-wiki-page`

For small edits, prefer `azuredevops-str-replace-wiki-page` - it handles versioning internally and is less error-prone.