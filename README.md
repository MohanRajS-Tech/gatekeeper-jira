# Gatekeeper: DoD & Checklist Validator for Jira

> **Enforce Definition of Done and Acceptance Criteria on native Jira issue descriptions with zero bloat and zero custom scripts.**

---

## Overview

**Gatekeeper for Jira** adds an automated Quality Gate to any Jira Cloud workflow. It parses native markdown checkboxes (`- [ ]`, `• [ ]`, `* [ ]`) and rich-text checklists in the issue description and blocks status transitions (e.g., moving to *Done* or *Ready for QA*) until all required items are marked complete (`[x]`).

### Why Gatekeeper?
* **Zero UI Clutter:** Works directly with Jira's native description editor. No heavy third-party panels, custom tables, or extra database fields.
* **Serverless Execution:** Runs 100% inside the **Atlassian Forge** hosted runtime with zero cold-start latency.
* **Enterprise Security Ready:** Zero data egress, zero database storage, and strictly read-only permissions (`read:jira-work`).

---

## How to Configure in Jira (30-Second Setup)

To enforce Definition of Done validation on any Jira workflow transition:

1. **Open Workflow Settings:**
   * Go to **Project Settings** → **Workflows** (or **Jira Settings** ⚙️ → **Issues** → **Workflows**).
   * Click the **Pencil (Edit)** icon on the workflow you want to protect.

2. **Add Gatekeeper Validator:**
   * Click on the transition arrow entering your completion status (e.g., **Done**, **Resolved**, or **Ready for QA**).
   * In the right-hand panel, click **Validators** → **Add validator**.
   * Select **Gatekeeper Definition of Done Validator** and click **Add**.

3. **Publish Workflow Draft:**
   * Click **Publish Draft** at the top of the workflow editor.
   * Confirm **Publish**.

---

## How to Use: Section Scoping

To prevent arbitrary notes or backlog ideas from blocking your ticket, group your release checks under an explicit heading:

```markdown
## Definition of Done
- [x] Unit tests passing (>85% coverage)
- [x] Code reviewed and approved
- [ ] Staging verification complete
```

* **Inside the DoD Section:** Incomplete items (`- [ ]`) block the transition and alert the user with the exact pending item names.
* **Outside the DoD Section:** Checkboxes under other headings (e.g., `## Notes` or `## Out of Scope`) are **completely ignored**.
* **Flexible Syntax:** Works with `## Definition of Done`, `**Definition of Done:**`, `## Acceptance Criteria`, or `## DoD`.

---

## Supported Checklist Syntax

| Format | Unchecked (Blocked) | Checked (Allowed) |
| :--- | :--- | :--- |
| **Standard Dash Markdown** | `- [ ] Pending task` | `- [x] Completed task` |
| **Jira Bullet Checkbox** | `• [ ] Pending task` | `• [x] Completed task` |
| **Asterisk Markdown** | `* [ ] Pending task` | `* [x] Completed task` |
| **Numbered Checkbox** | `1. [ ] Pending task` | `1. [x] Completed task` |
| **Native Jira Checkbox** | Native ADF interactive checkbox | Native ADF checked box |

---

## Smart Guardrails Built-In

* **Code Block Immunity:** Fenced code snippets (```` ```...``` ````), inline code (`` `[ ]` ``), and JSON arrays in bug reports are ignored.
* **Sub-task Exemption:** Informal sub-tasks without a `## Definition of Done` heading pass automatically to prevent daily workflow friction.
* **Terminal Resolution Bypass:** Transitions to *Cancelled*, *Won't Do*, *Duplicate*, or *Rejected* bypass validation so tickets never become trapped.

---

## Security & Architecture

* **Zero Data Egress:** Gatekeeper does not send or forward any Jira data to external servers or third-party cloud infrastructure.
* **No Database Storage:** No issue data, user information, or checklist items are stored or logged. Validation occurs in-memory during transition evaluation.
* **Least Privilege:** Requests only `read:jira-work` strictly necessary to inspect `issue.description`.

---

## Support & Bug Reports

* **Issue Tracker:** [GitHub Issues](https://github.com/MohanRajS-Tech/gatekeeper-jira/issues)
* **Privacy Policy:** [Privacy Policy](https://github.com/MohanRajS-Tech/gatekeeper-jira/blob/main/privacy_policy.md)
* **Terms of Service:** [Terms of Service](https://github.com/MohanRajS-Tech/gatekeeper-jira/blob/main/terms_of_service.md)
