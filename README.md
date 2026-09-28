# Lab-4-ServiceNow-Information-Technology-Service-Management

![ServiceNow](https://img.shields.io/badge/ServiceNow-ITSM-00C7D4?style=for-the-badge&logo=servicenow&logoColor=white)
![Incident Management](https://img.shields.io/badge/Incident-Management-blue?style=for-the-badge)
![Change Management](https://img.shields.io/badge/Change-Management-orange?style=for-the-badge)
![Service Catalog](https://img.shields.io/badge/Service-Catalog-green?style=for-the-badge)

Watch the full lab walkthrough here! 
https://www.loom.com/share/9a49364d46e84af4890f325823619b21

## Overview

This lab demonstrates how ServiceNow can be used to manage common IT service management processes. It covers creating and resolving incidents, building a service catalogue item, implementing an approval workflow for changes, and generating reports to track IT operations. The lab provides hands-on experience with ITIL-based workflows commonly used in IT support, help desk, systems administration, and enterprise IT environments.

---

## Business Problem This Lab Solves

Organizations need a structured way to track, prioritize, route, approve, and resolve IT work consistently. Without a centralized process, incidents can be missed, requests can be delayed, changes can be made without proper approval, and IT teams have limited visibility into operational performance.

ServiceNow addresses these challenges by providing centralized incident management, service requests, change management, approvals, and reporting. These capabilities help IT teams standardize processes, improve accountability, reduce resolution times, and maintain an auditable record of IT operations.

| Role | How this lab applies |
|---|---|
| IT Support / Help Desk | Creating and resolving incidents — the core daily task |
| Sysadmin | Change management — logging, approving, and documenting infrastructure changes |
| IT Service Manager | Building service catalogues, defining workflows, reporting on SLA compliance |
| Cloud Engineer | Change requests, incident management, and service requests for cloud resources |

---

### 1. Provision Your Free ServiceNow PDI

Go to developer.servicenow.com and sign up with email and password — no credit card
Click Request Instance, select the latest stable release (Washington or newer), and click Request
Wait 10–15 minutes for provisioning, then log in at your instance URL (devXXXXX.service-now.com)

> ⚠️ **Keep your instance active**
> ServiceNow hibernates Personal Developer Instances that haven't been accessed in 10 days and reclaims instances inactive for more than 30 days. Log in at least once a week to keep it active. If it gets reclaimed, you can request a new one for free — but you lose your work.

---

## 2. Create and Work an Incident 

Simulate a common IT support issue: a user cannot access Outlook. Create and document the incident, work through the troubleshooting process, and close the ticket with resolution notes.

**Navigate:** Service Desk → Incidents → New

| Field | Value |
|---|---|
| Caller |  Abel Tuter|
| Category | Software |
| Subcategory | Email |
| Short description | User cannot access Outlook — error: Cannot connect to server |
| Description | User reports that Outlook stopped working this morning at approximately 9am. Error message: 'Cannot connect to the Exchange server. Verify your network settings.' Other users in the same building are not affected. User is on a laptop, connected via Wi-Fi. |
| Priority | 3 — Moderate (one user affected, workaround available — use webmail) |
| Assignment Group | Service Desk |

Work the ticket: set State to In Progress, assign it to yourself, add a work note, add resolution notes, then close it.

![Closed incident INC0010001 — Priority 3-Moderate, assigned to Beth Anglin](screenshots/incident-INC0010001-closed.png)

![Activity log — full incident lifecycle and work notes from New through Closed](screenshots/incident-activity-log.png)

![Resolution Information tab — resolution notes documenting the fix](screenshots/incident-resolution-notes.png)

---

## 3. Build a Service Catalogue Item

Service Catalog is a self-service portal where employees can request standard IT services or products.

**Navigate:** Service Catalog → Catalogs → Service Catalog → Maintain Items

Create a **New Laptop Request** item under the **Hardware** category, with fulfillment group **IT Hardware Team**, then add four variables: **Requester Name**, **Business Justification**, **Required By Date**, and **Laptop Model Preference**. Save and preview to confirm it appears in the portal.

| Field | Value |
|---|---|
| Name | New Laptop Request |
| Category | Hardware |
| Short description | Request a new or replacement laptop |
| Description | Use this form to request a new laptop for a new hire or to replace a failed or end-of-life device. Requests are reviewed within 2 business days. Delivery takes 5–7 business days after approval. |
| Fulfillment group | IT Hardware Team |
| Price | Leave blank — internal requests do not have a user-facing cost |



![New Laptop Request catalogue item — live order form with all four variables](screenshots/catalog-new-laptop-request-form.png)

![Catalog search results confirming the item is published under Hardware](screenshots/catalog-search-results.png)

--- 

## 4. Create a Change Request with CAB Approval

Change requests require approval before work begins on production infrastructure—a core ITIL control that helps ensure changes are reviewed, authorized, and coordinated before implementation.

**Navigate:** Change isn't in the **All** menu on this PDI. Use global search instead:

1. Click the global search icon (top nav) and type **change request**
2. Select **Change Requests** → click **Go to list view**
3. Click **New** in the upper right
4. On the "Create a change request" template picker, click **Normal** — not Standard



---

## 5. Build a Report 

**Navigate:** Reports → Create New

Build **Incident Volume by Priority — Last 30 Days** as a bar chart (Data: Incident, Group by: Priority, Condition: Created in the last 30 days). For the portfolio, also build **Mean Time to Resolution (MTTR)** by Assignment Group and **Open Incidents by Assigned Agent**.

---

### Key Skills Demonstrated 

Incident management — Creating, prioritizing, assigning, and resolving tickets through the full lifecycle.

SLA and prioritization — Setting priority based on impact and urgency.

Assignment and routing — Directing tickets to the appropriate team or individual.

Service catalogue design — Building self-service request items with custom fields.

Change management — Documenting, approving, and scheduling infrastructure changes.

Reporting and analytics — Creating reports for incident volume, MTTR, and workload.

ITIL process knowledge — Understanding incidents, problems, changes, and service requests.

---

