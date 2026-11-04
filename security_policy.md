# Security Policy & Practices

**Vendor:** TheOpsLabs  
**Product:** Gatekeeper for Jira (Cloud)  
**Effective Date:** October 16, 2026  
**Last Updated:** November 4, 2026  
**Support & Security Contact:** support@theopslabs.com  
**Documentation & Repository:** https://github.com/MohanRajS-Tech/gatekeeper-jira  

---

## 1. Architectural Security & Data Handling

Gatekeeper for Jira is engineered exclusively as a native **Atlassian Forge Cloud application**. The application executes directly within Atlassian's isolated, multi-tenant runtime environment.

### Data Flow & Storage
* **Zero External Egress:** The application manifest (`manifest.yml`) declares zero external egress network domains. No issue data, user metadata, or system telemetry ever leaves the Atlassian Cloud perimeter.
* **Ephemeral In-Memory Processing:** Workflow validation is performed synchronously in-memory using native Jira Expressions (`issue.description`). Once validation completes, all references are immediately garbage-collected.
* **Zero Persistent Storage:** The app provisions no SQL/NoSQL databases, provisions no Forge key-value storage (`@forge/api` storage), and retains no logs containing issue text or customer personally identifiable information (PII).
* **Least Privilege Scopes:** The app requests strictly one read-only OAuth permission:
  * `read:jira-work` — Restricted strictly to reading the issue description field during workflow transition validation.

---

## 2. Encryption Standards

Because Gatekeeper operates 100% serverless within Atlassian Forge:
* **Encryption in Transit:** All communication between Jira Cloud and the Forge execution container is enforced via TLS 1.2 / TLS 1.3 with industry-standard cryptographic cipher suites.
* **Encryption at Rest:** Although Gatekeeper persists zero customer data, any underlying Atlassian Cloud infrastructure environment configurations are encrypted at rest using AES-256.

---

## 3. Vulnerability Management & Code Quality

TheOpsLabs maintains continuous security verification across all codebases and dependencies:

### Automated Security Testing (SAST & SCA)
* **Static Application Security Testing (SAST):** All repository code, including the staged ADF parser module (`src/parser.js`), is analyzed via automated static analyzers and ESLint security rulesets. Code audits verify zero usage of dynamic evaluation (`eval()`, `Function()`, `setTimeout(string)`) and deterministic regex execution to prevent ReDoS (Regular Expression Denial of Service).
* **Software Composition Analysis (SCA):** Production runtime dependencies are scanned via `npm audit --omit=dev`. Gatekeeper maintains strictly 1 direct dependency (`@forge/api`) and operates with **0 known vulnerabilities**.
* **Audit Cadence:** Automated dependency scans run bi-weekly. Security patches from Atlassian Forge SDK are incorporated within 7 calendar days of release.

---

## 4. Vulnerability Remediation SLOs (Atlassian Marketplace Security Alignment)

TheOpsLabs adheres strictly to the **Atlassian Marketplace Security Bug Fix Policy** and tracks reported vulnerabilities through Atlassian Marketplace Security (AMS):

| Severity Level | Definition | Mandatory Resolution Window |
| :--- | :--- | :--- |
| **Critical** | Remote Code Execution, Privilege Escalation, or critical data exposure | **$\le$ 10 Calendar Days** |
| **High** | Significant security bypass or unauthorized authenticated action | **$\le$ 28 Calendar Days** |
| **Medium** | Minor security defect or non-critical parameter manipulation | **$\le$ 84 Calendar Days** |
| **Low** | Cosmetic or low-impact security hardening observation | **$\le$ 175 Calendar Days** |

* **Vulnerability Reporting Alignment:** Security vulnerability reports received via Atlassian Marketplace Security (AMS/ECOHELP) or direct disclosure are triaged and acknowledged within 24 business hours.

---

## 5. Security Incident Management & Disclosure Protocol

In the event of a confirmed security incident or critical vulnerability (evaluated on 24/7 calendar availability):

1. **Containment & Hotfix (< 12 Calendar Hours):** Isolate affected module and prepare immediate Forge serverless hotfix.
2. **Atlassian Notification (< 48 Hours):** Submit comprehensive incident dispatch to Atlassian Ecosystem Security via the official security ticket portal (`ECOHELP` / `AMS`), detailing affected tenants and root cause.
3. **Deployment (< 24 Hours):** Deploy verified patch directly to Atlassian Forge production environment with zero customer downtime.
4. **Customer Transparency (< 48 Hours):** Publish a security advisory with CVE/GHSA attribution and detailed version release notes on the Atlassian Marketplace listing.

---

## 6. Infrastructure & Platform Certifications

The host environment for Gatekeeper is provided and maintained by Atlassian Cloud Infrastructure, which maintains independent enterprise certifications:
* **SOC 2 Type II**
* **ISO/IEC 27001, 27018**
* **GDPR & CCPA Compliance**
* **Cloud Data Residency:** Inherits the host Jira instance's configured data residency boundary automatically.

---

## 7. Reporting a Vulnerability

We welcome responsible security disclosures. If you discover a vulnerability, please contact:
* **Email:** `support@theopslabs.com`
* **Secure Transmission:** Include complete reproduction steps, proof of concept (PoC), and target version.
* **Response Commitment:** Initial acknowledgement within 24 business hours.

