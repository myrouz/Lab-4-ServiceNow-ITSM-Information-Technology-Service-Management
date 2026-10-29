
# Lab 4: ServiceNow Information Technology Service Management

![ServiceNow](https://img.shields.io/badge/ServiceNow-ITSM-00C7D4?style=for-the-badge&logo=servicenow&logoColor=white)
![Incident Management](https://img.shields.io/badge/Incident-Management-blue?style=for-the-badge)
![Change Management](https://img.shields.io/badge/Change-Management-orange?style=for-the-badge)
![Service Catalog](https://img.shields.io/badge/Service-Catalog-green?style=for-the-badge)


## 🎥 Walkthrough

Watch the full lab walkthrough here! 

[Loom Video: ServiceNow ITSM Lab](https://www.loom.com/share/9a49364d46e84af4890f325823619b21)

## 📋 Overview

IT Service Management (ITSM) platforms, such as ServiceNow, serve as structured enterprise systems used to track, route, prioritize, and resolve IT requests while enforcing standardized operational processes across an organization. 

This project demonstrates the deployment and configuration of an IT service management environment using a free ServiceNow Personal Developer Instance (PDI). The lab simulates a professional enterprise support environment where IT administrators manage service delivery, handle break/fix incidents, maintain infrastructure stability through change control, and streamline user self-service requests.  

Implementation includes provisioning the PDI, creating and resolving IT incidents, configuring priority levels and Service Level Agreements (SLAs), assigning tickets to appropriate queues, building customized service catalog items with user variables, and implementing structured approval workflows and change management controls for infrastructure modifications.  

I also leveraged ServiceNow's workflow and automation engine to manage approval routing, assignment rules, and SLA timers, while building analytical dashboard reports to track incident volume, resolution metrics, and operational performance.   

The project highlights core ITIL framework and service management principles, including incident lifecycle management, problem tracking, change risk mitigation, asset configuration management, and knowledge documentation. These skills provide a practical foundation for professional IT support, help desk administration, and enterprise ITSM operations.  

---

## 🎯 Business Context

Organizations often struggle with fragmented IT operations where incidents slip through the cracks, requests face delays, and infrastructure changes occur without proper authorization or oversight. Without a centralized ITSM platform, IT teams lack visibility into operational performance, leading to inconsistent issue resolution and diminished accountability.  

This lab simulates addressing these challenges by deploying an enterprise ITSM environment from the ground up using a ServiceNow Personal Developer Instance (PDI). By leveraging centralized incident tracking, structured service request catalogs, change control governance, and automated approval workflows, the platform eliminates manual bottlenecks and streamlines ticket routing. Implementing these practices empowers organizations to standardize ITIL-aligned operations, reduce resolution times, enhance cross-team visibility, and maintain a fully auditable record of IT service delivery.

| Role | How this lab applies |
|---|---|
| IT Support / Help Desk | Creating and resolving incidents — the core daily task |
| Sysadmin | Change management — logging, approving, and documenting infrastructure changes |
| IT Service Manager | Building service catalogues, defining workflows, reporting on SLA compliance |
| Cloud Engineer | Change requests, incident management, and service requests for cloud resources |

---

## 🧩 Architecture

<img width="1024" height="533" alt="servicenow-itsm-architecture" src="https://github.com/user-attachments/assets/88fdfdc3-c878-4b48-ad3b-5df4a78215ab" />


## 📚 Key Concepts

These terms come up in every IT support interview and are tested in ITIL Foundation. Understanding how they map to ServiceNow makes them concrete.

| ITIL Term | Definition | ServiceNow Module |
|---|---|---|
| **Incident** | An unplanned interruption to a service. Goal: restore service as quickly as possible. | Service Desk → Incidents |
| **Problem** | The root cause of one or more incidents. Goal: eliminate the root cause permanently. | Service Desk → Problems |
| **Change** | A planned modification to infrastructure or applications. Goal: implement with minimal risk. | Change → Changes |
| **Service Request** | A user request for something new (access, hardware, information). Not a break/fix. | Service Catalog |
| **SLA** | Service Level Agreement: the committed response and resolution time for each priority level. | SLA → SLA Definitions |
| **CMDB** | Configuration Management Database: the record of every IT asset and its relationships. | Configuration → CIs |
| **Knowledge Base** | Articles documenting known issues and their solutions, which reduces repeat incident volume. | Knowledge → Articles |
---

## ✅ Prerequisites

<details>
<summary><b>1. Provision Your Free ServiceNow PDI</b></summary>

<br>

1. Go to [developer.servicenow.com](https://developer.servicenow.com) and sign up with email and password. No credit card is required.
2. Click **Request Instance**, select the latest stable release (Washington or newer), and click **Request**.
3. Wait 10–15 minutes for provisioning, then log in at your instance URL (`devXXXXX.service-now.com`).

> ⚠️ **Keep your instance active**
> ServiceNow hibernates Personal Developer Instances that haven't been accessed in 10 days and reclaims instances inactive for more than 30 days. Log in at least once a week to keep it active. If it gets reclaimed, you can request a new one for free, but you lose your work.

</details>

---
## 🛠️ Steps
<details>
<summary><b>2. Create and Work an Incident</b></summary>

<br>

Simulate a common IT support issue: a user cannot access Outlook. Create and document the incident, work through the troubleshooting process, and close the ticket with resolution notes.

**Navigate:** Service Desk → Incidents → New

| Field | Value |
|---|---|
| Caller | Abel Tuter |
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

</details>

<details>
<summary><b>3. Build a Service Catalogue Item</b></summary>

<br>

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

</details>

<details>
<summary><b>4. Create a Change Request with CAB Approval</b></summary>

<br>

Change requests require approval before work begins on production infrastructure—a core ITIL control that helps ensure changes are reviewed, authorized, and coordinated before implementation.

**Navigate:** Change isn't in the **All** menu on this PDI. Use global search instead:

1. Click the global search icon (top nav) and type **change request**
2. Select **Change Requests** → click **Go to list view**
3. Click **New** in the upper right
4. On the "Create a change request" template picker, click **Normal** — not Standard

</details>

<details>
<summary><b>5. Build a Report</b></summary>

<br>

**Navigate:** Reports → Create New

Build **Incident Volume by Priority — Last 30 Days** as a bar chart (Data: Incident, Group by: Priority, Condition: Created in the last 30 days). For the portfolio, also build **Mean Time to Resolution (MTTR)** by Assignment Group and **Open Incidents by Assigned Agent**.

</details>

---

## ✅ Validation & Troubleshooting

---

## 📖 Key Terms

| Term | Definition | 
| --- | --- | 
| **ITSM (IT Service Management)** | A structured framework and set of policies used to design, deliver, manage, and improve how IT services are provided to end users across an organization.|
| **ITIL (Information Technology Infrastructure Library)** |The world's most widely adopted set of best practices and standard processes for delivering high-quality IT service management.|
| **Incident** | An unplanned interruption to an IT service or a reduction in service quality; the primary goal is to restore service as quickly as possible. |
| **Problem** | The underlying root cause of one or more recurring incidents, aimed at identifying permanent fixes to prevent future occurrences. |
| **Change** | A planned modification to IT infrastructure, software, or applications designed to be implemented with minimal risk and proper review. |
| **Service Catalog** | A user-facing self-service portal where employees can browse, submit, and request standard IT services (like new hardware or software access). |
| **Service Request** | A formal user request for something new—such as hardware, software access, or information—rather than an unplanned break/fix issue. |
| **SLA (Service Level Agreement)** | The committed response and resolution timeframes mandated for each priority level to ensure operational accountability. | 
| **CMDB (Configuration Management Database)** | A centralized repository and record tracking every IT asset, hardware component, and their logical relationships. |
| **Knowledge Base** | A collection of articles documenting known issues, troubleshooting steps, and approved solutions to reduce repeat incident volumes. | Knowledge $\rightarrow$ Articles |
| **CAB (Change Advisory Board)** | A group that review, evaluate, assess risk, and approve or reject high-impact or major planned changes to IT infrastructure. |

---

## 💡 Lessons Learned 

- **Good documentation is the real product of a ticket.** Work notes show what was tried and why, and resolution notes record the fix. The activity log turns one incident into an audit trail that the next technician can learn from.
- **Priority reflects impact and workaround, not how urgent it feels.** The Outlook incident was Priority 3 because one user was affected and webmail was available. Setting priority honestly keeps response times meaningful for the tickets that really are urgent.
- **Reports turn tickets into decisions.** Incident volume by priority, MTTR by assignment group, and open incidents by agent answer different questions: where demand is, how fast it gets resolved, and who is overloaded.
- **Incident, problem, change, and service request are different things.** Restoring Outlook was an incident. If the same failure kept recurring, it would become a problem needing root cause analysis. Patching production is a change, and requesting a laptop is a service request. Using the right record type keeps work routed and measured correctly.
- **A catalogue item moves routine work out of the help desk queue.** A form with mandatory variables (requester, business justification, required-by date) captures what fulfilment needs up front, so there is less back-and-forth than with an emailed request.
- **Change control exists to prevent uncoordinated outages.** A Normal change needs a test plan, a backout plan, and approval before it is scheduled. I used Normal instead of Standard because Standard changes are pre-approved, low-risk templates that skip that review.

