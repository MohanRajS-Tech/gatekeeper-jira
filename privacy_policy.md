# Privacy Policy for Gatekeeper for Jira

**Effective Date:** October 16, 2026  
**Last Updated:** October 16, 2026

## 1. Overview
Gatekeeper for Jira ("the App") is developed as an Atlassian Forge application designed to validate Definition of Done and checklist items in Jira issue descriptions. 

This Privacy Policy explains how the App handles data when installed on your Atlassian Cloud site.

## 2. Zero Data Collection & Zero Egress Architecture
Gatekeeper for Jira is built strictly on the **Atlassian Forge** platform and operates entirely within Atlassian's Cloud infrastructure:

* **Zero External Data Egress:** The App does not transmit, forward, or send any issue data, metadata, or user information to any third-party server, cloud provider, or external database.
* **In-Memory Expression Execution:** Checklist validation is evaluated synchronously in-memory using native Jira Expressions (`issue.description`). No text or checklist content is stored or cached.
* **No Database Storage:** The App does not provision or utilize any persistent Forge Storage, SQL/NoSQL databases, or cookies.
* **No Personal Data Processing:** The App does not log, collect, track, or profile personal data, user identities, IP addresses, or browsing activities.

## 3. Scopes & Permissions Requested
The App requests only the minimum required scope:
* `read:jira-work`: Required exclusively to read the `description` field of Jira issues to determine whether unchecked items (`[ ]`) exist during workflow transition validation.

## 4. Third-Party Sharing
We do not sell, rent, trade, or share any data with third parties. No data leaves your Atlassian Cloud tenant.

## 5. Security & Compliance
* **Atlassian Forge Sandbox:** All code runs inside Atlassian-managed multi-tenant sandboxes compliant with SOC2, ISO 27001, and GDPR standards.
* **Data Residency:** All data remains strictly within the data residency boundary configured on your Atlassian Cloud organization.

## 6. Contact & Data Protection Inquiries
For questions regarding this policy or technical inquiries:
* **Developer Contact:** mohanrajs (Atlassian Developer Space)
* **Email:** support@gatekeeperjira.com (or via Marketplace vendor support portal)
