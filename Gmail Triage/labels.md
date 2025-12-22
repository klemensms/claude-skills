# Gmail Label IDs

Use these label IDs directly with Gmail modify operations. Do not retrieve from Gmail API.

## Category Labels

| Label | ID | Use When |
|-------|-----|----------|
| ai_01_ActionRequired | `Label_26` | Requires user action |
| ai_02_NeedsReading | `Label_29` | Important, needs attention |
| ai_03_read_if_time_permits | `Label_22` | Optional reading |
| ai_04_Notification | `Label_24` | System notifications |
| ai_05_LowPriority | `Label_25` | Archive/delete candidates |
| ai_Unsure | `Label_20` | Uncertain, needs review |

## Confidence Labels

| Label | ID | Use When |
|-------|-----|----------|
| ai_c_h | `Label_23` | Clear match, known pattern |
| ai_c_m | `Label_27` | Reasonable match |
| ai_c_l | `Label_28` | Borderline decision |

## Gmail Modify Examples

Apply labels:
```json
{
  "addLabelIds": ["Label_26", "Label_23"]
}
```

Archive (remove from inbox):
```json
{
  "removeLabelIds": ["INBOX"]
}
```

Combined (apply labels and archive):
```json
{
  "addLabelIds": ["Label_22", "Label_27"],
  "removeLabelIds": ["INBOX"]
}
```

## Search Query

Find unlabelled inbox emails:
```
in:inbox -label:ai_01_ActionRequired -label:ai_02_NeedsReading -label:ai_03_read_if_time_permits -label:ai_04_Notification -label:ai_05_LowPriority -label:ai_Unsure
```
