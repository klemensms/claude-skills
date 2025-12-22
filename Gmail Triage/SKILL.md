---
name: gmail-triage
description: Systematically categorize unlabelled emails in Gmail inbox by reading content and applying priority labels. Use when the user asks to triage emails, categorize inbox, process emails, achieve inbox zero, or sort their Gmail. Integrates with Todoist for action items with deadlines.
---

# Gmail Triage

Categorize inbox emails with priority labels and create Todoist tasks for action items.

## Workflow

Process each email individually before moving to the next:

1. **Search** for unlabelled inbox emails (no `ai_*` labels)
2. **Read** the full email content
3. **Categorize** using rules below → apply category + confidence label
4. **Create Todoist task** if `ai_01_ActionRequired` AND has a deadline
5. **Archive** if category 3+ (remove INBOX label)
6. **Repeat** for next email

## Category Rules

**ai_01_ActionRequired** — Requires action:
- Emails from user or spouse (klemens@stelk.co.uk, klemens.stelk@smartimpact.co.uk, prakritigupta1988@gmail.com) → ALWAYS action required
- Money/payments involved
- Failures, closures, automation errors
- Meeting RSVPs, assigned tasks, approval requests, deadlines

**ai_02_NeedsReading** — Important, no immediate action:
- Manager/leadership updates
- Project status updates
- Company announcements
- Children routine/schedule changes

**ai_03_read_if_time_permits** — Optional reading:
- School newsletters (routine info)
- Industry newsletters: AI, IT, photography, philosophy, stoicism, health, entrepreneurship, food
- Blog posts, optional webinars

**ai_04_Notification** — Automated system alerts:
- Calendar reminders, build notifications
- Password confirmations, shipping updates

**ai_05_LowPriority** — Archive/delete:
- OTPs, verification links (already used)
- Outdated invitations, auto-updated events
- Marketing emails, unread newsletters

**ai_Unsure** — When uncertain (review later with user)

## Confidence Labels

Apply ONE alongside the category:
- `ai_c_h` — High confidence: clear match, established pattern
- `ai_c_m` — Medium confidence: reasonable match
- `ai_c_l` — Low confidence: borderline decision

## Todoist Integration

Create task only for `ai_01_ActionRequired` with identifiable deadline:

```json
{
  "tasks": [{
    "content": "Gmail-mcp | [action description]",
    "projectId": "inbox",
    "description": "Email link: https://mail.google.com/mail/u/0/#inbox/[messageId]",
    "deadlineDate": "YYYY-MM-DD"
  }]
}
```

Skip Todoist for: calendar invites, webinar invitations.

## Label IDs

See [references/labels.md](references/labels.md) for complete label ID mappings.

Quick reference:
- ai_01_ActionRequired: `Label_26`
- ai_02_NeedsReading: `Label_29`  
- ai_03_read_if_time_permits: `Label_22`
- ai_04_Notification: `Label_24`
- ai_05_LowPriority: `Label_25`
- ai_Unsure: `Label_20`
- ai_c_h: `Label_23` | ai_c_m: `Label_27` | ai_c_l: `Label_28`

## Summary Report

After processing, provide:
- Number of emails processed
- Label applied to each with brief reasoning
- Any "Unsure" items needing manual review
