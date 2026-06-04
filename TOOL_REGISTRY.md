# Three Flows Solutions — Tool Registry

## Templates (never shown in free-tools.html)
| File | Type | Purpose |
|---|---|---|
| tool-ck000-template.html | Checklist | Master template for all CK tools |
| tool-ca000-template.html | Calculator | Master template for all CA tools |

## Active Tools
| ID    | Type       | Tool Name                         | File             | Last Revised |
|-------|------------|-----------------------------------|------------------|--------------|
| CK001 | Checklist  | Pre-Launch Planning Checklist     | tool-ck001.html  | May 8, 2026  |
| CK002 | Checklist  | Sample Sourcing Checklist         | tool-ck002.html  | May 8, 2026  |
| CK003 | Checklist  | Voice of Customer Checklist       | tool-ck003.html  | May 8, 2026  |
| CK004 | Checklist  | Company and Brand Setup Checklist | tool-ck004.html  | May 8, 2026  |
| CA001 | Calculator | Unit Economics & Cashflow Model   | tool-ca001.html  | May 29, 2026 |
| CA002 | Calculator | Last-Mile Rate Calculator         | tool-ca002.html  | June 3, 2026 |

## Retired / Superseded Tools
| Former ID / File | Superseded by | Note |
|---|---|---|
| UE001 / tool-ue001.html | CA001 / tool-ca001.html | "UE" (unit economics) calculator naming was used briefly in handoff v0529; the series was consolidated under "CA" (Calculator). Files and IDs renamed June 3, 2026. |
| UE002 / tool-ue002.html | CA002 / tool-ca002.html | Same consolidation as above. |

## ID Reference
- Two tool types: CK = Checklist, CA = Calculator
- Base format: CK001, CK002 ... CK999 and CA001, CA002 ... CA999
- Revision format: CK001A through CK001Z, then CK002 for the 27th revision
  (same rule applies to CA series)
- Filename convention: tool-ck001.html, tool-ca001.html, tool-ck001a.html etc.
- Cookie name convention: tf_tool_ck001, tf_tool_ca001, tf_tool_ck001a etc.
- Display: tool name + last revised date only — ID never shown to users
- Revision rule: logic change = new letter suffix
- Deactivation: when a revision goes live, previous version card must be
  removed from free-tools.html
- Sort order in free-tools.html: checklists group first (CK ascending),
  calculators group second (CA ascending), manually overridden per deploy
- Next available checklist ID: CK005
- Next available calculator ID: CA003

## Backlog — Calculator Ideas (not reserved, not yet built)
These were sketched during early planning. They are concepts only — no ID is
reserved until a tool is built and renumbered sequentially per the rule above.
- Landed Cost
- Storage Fee
- Inventory Turns

## Pre-Assigned IDs (Checklists)
| ID    | Type       | Tool Name                     |
|-------|------------|-------------------------------|
| CK001 | Checklist  | Pre-Launch Planning           |
| CK002 | Checklist  | Sample Sourcing               |
| CK003 | Checklist  | Voice of Customer             |
| CK004 | Checklist  | Company and Brand Setup       |
| CK005 | Checklist  | Set Up Your Back Office       |
| CK006 | Checklist  | Launch Playbook               |
| CK007 | Checklist  | Vendor Scorecard              |
