# Gatekeeper: DoD & Checklist Validator for Jira
# Gatekeeper: Definition of Done & Checklist Validator for Jira

> **Enforce Definition of Done and acceptance criteria on native Jira issue descriptions with zero bloat and zero custom scripts.**

---

## Overview

**Gatekeeper for Jira** adds an automated Quality Gate to any Jira Cloud workflow. It parses native markdown checkboxes (`- [ ]`, `• [ ]`, `* [ ]`) in the issue description and synchronously blocks status transitions (e.g., moving to *Done* or *Resolved*) until every single checklist item is marked complete (`[x]`).

### Why Gatekeeper?
* **Zero UI Clutter:** Works directly with Jira's native description editor. No heavy third-party panels, custom tables, or extra fields.
* **0ms Latency:** Evaluates in-memory directly within Jira Cloud using native Jira Expressions. Zero cold-start latency.
* **Enterprise Security Ready:** Built 100% on the **Atlassian Forge** platform. Zero data egress, zero database storage, and strictly read-only permissions (`read:jira-work`).

---

## How to Configure in Jira (30-Second Setup)

To enforce Definition of Done validation on any Jira workflow transition:

1. **Open Workflow Settings:**
   * Go to **Jira Settings** (cog icon) $\rightarrow$ **Issues** $\rightarrow$ **Workflows**.
   * Locate the workflow you want to protect (e.g., *Software Development Workflow* or *Service Request Workflow*) and click **Edit**.

2. **Add Gatekeeper Validator:**
   * Click on the transition arrow entering your final status (e.g., transition to **Done** or **Resolved**).
   * In the properties panel on the right, click **Validators**.
   * Click **Add validator**.
   * Select **Gatekeeper Definition of Done Validator** from the list and click **Add**.

3. **Publish Workflow Draft:**
   * Click **Publish Draft** at the top of the workflow editor.
   * Select whether to save a backup of the previous workflow, then confirm **Publish**.

> [!TIP]
> **Working in your sprint?**  
> If Gatekeeper helped your team enforce Definition of Done, support this free, zero-egress utility with a 10-second review on [Atlassian Marketplace](https://marketplace.atlassian.com/apps/415931997?tab=reviews&hosting=cloud).

---

## Supported Checklist Syntax

Gatekeeper natively recognizes standard markdown and Jira rich-text checkbox formats:

| Format | Unchecked (Blocked) | Checked (Allowed) |
| :--- | :--- | :--- |
| **Standard Dash Markdown** | `- [ ] Pending task` | `- [x] Completed task` |
| **Jira Bullet Checkbox** | `• [ ] Pending task` | `• [x] Completed task` |
| **Asterisk Markdown** | `* [ ] Pending task` | `* [x] Completed task` |
| **Numbered Checkbox** | `1. [ ] Pending task` | `1. [x] Completed task` |
| **Tight Markdown** | `-[ ] Pending task` | `-[x] Completed task` |

---

## Security & Architecture

* **Zero External Data Egress:** Gatekeeper does not send or forward any Jira data to external servers or third-party cloud infrastructure.
* **No Database Storage:** No issue data, user information, or checklist items are stored or logged. Validation occurs in-memory during workflow transition evaluation.
* **Least Privilege:** Requests only `read:jira-work` scope strictly necessary to read `issue.description`.

---

## Support & Bug Reports

* **Issue Tracker:** [GitHub Issues](https://github.com/MohanRajS-Tech/gatekeeper-jira/issues)
* **Privacy Policy:** [Privacy Policy](https://github.com/MohanRajS-Tech/gatekeeper-jira/blob/main/privacy_policy.md)
* **Terms of Service:** [Terms of Service](https://github.com/MohanRajS-Tech/gatekeeper-jira/blob/main/terms_of_service.md)
