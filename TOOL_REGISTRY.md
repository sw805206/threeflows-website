# Three Flows Solutions — Tool Registry

## Templates (never shown in free-tools.html)
| File | Type | Purpose |
|---|---|---|
| tool-ck000-template.html | Checklist | Master template for all CK tools |
| tool-ca000-template.html | Calculator | Master template for all CA tools |

## Active Tools
| ID    | Type      | Tool Name                     | File             | Last Revised |
|-------|-----------|-------------------------------|------------------|--------------|
| CK001 | Checklist | Pre-Launch Planning Checklist | tool-ck001.html  | May 8, 2026  |
| CK002 | Checklist | Sample Sourcing Checklist     | tool-ck002.html  | May 8, 2026  |
| CK003 | Checklist | Voice of Customer Checklist   | tool-ck003.html  | May 8, 2026  |
| CK004 | Checklist | Company and Brand Setup Checklist | tool-ck004.html | May 8, 2026 |

## Retired / Superseded Tools
(none yet)

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
- Sort order in free-tools.html: checklists group first (CK001 ascending),
  calculators group second (CA001 ascending), manually overridden per deploy
- Next available checklist ID: CK005
- Next available calculator ID: CA001

## Pre-Assigned IDs
| ID    | Type       | Tool Name                     |
|-------|------------|-------------------------------|
| CK001 | Checklist  | Pre-Launch Planning           |
| CK002 | Checklist  | Sample Sourcing               |
| CK003 | Checklist  | Voice of Customer             |
| CK004 | Checklist  | Company and Brand Setup       |
| CK005 | Checklist  | Set Up Your Back Office       |
| CK006 | Checklist  | Launch Playbook               |
| CK007 | Checklist  | Vendor Scorecard              |
| CA001 | Calculator | Landed Cost                   |
| CA002 | Calculator | Storage Fee                   |
| CA003 | Calculator | Last Mile Cost                |
| CA004 | Calculator | Unit Economics                |
| CA005 | Calculator | Inventory Turns               |
