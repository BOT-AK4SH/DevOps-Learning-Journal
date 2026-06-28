# Roles in an Organization, SDLC & Jira

---

**As a DevOps Engineer:**

* You do **not directly interact with customers**.
* You usually **do not receive requirements directly from clients**.
* Requirements flow through several roles before reaching you.
* Your work is usually assigned through tools like **Jira**.

---

# 1. Requirement Flow (Important)

```text
Customer
   ↓
Business Analyst (BA)
   ↓
Product Manager (PM)
   ↓
Product Owner (PO)
   ↓
Solution Architect (SA)
   ↓
Development Team
   ↓
DevOps / QA / DBA
   ↓
SRE
```

---

# 2. Customer

Customers are the most important part of any business.

Example requirements:

* Deliver groceries within 15 minutes.
* Add UPI payment gateway.
* Add Stripe payment gateway.

Without customers, a product may be discontinued.

---

# 3. Business Analyst (BA)

### Responsibilities

* Interacts with customers.
* Collects requirements.
* Understands customer feedback.
* Creates BRD (Business Requirement Document).

---

# 4. Product Manager (PM)

### Responsibilities

* Defines product vision.
* Prioritizes requirements.
* Decides what should be built first.
* Looks at competitors and market trends.

### Example

PM decides:

| Requirement         | Priority |
| ------------------- | -------- |
| 15-Min Delivery     | High     |
| New Payment Gateway | Medium   |

PM may schedule implementation for:

* Q1 (Jan-Feb-Mar)
* Q2
* Future releases

---

# 5. Product Owner (PO)

### Responsibilities

* Converts product vision into actionable work.
* Manages backlog.
* Creates Epics and Stories.
* Defines "Definition of Done."

### Example

Requirement:

> 15-Minute Delivery Service

PO breaks it into:

* Mobile app support
* Desktop app support
* Backend implementation
* Database changes

These become **Epics/Features**.

---

# 6. Solution Architect (SA)

### Responsibilities

* Creates technical design.
* Creates HLD and LLD.

### HLD

**High-Level Design**

Explains:

* System architecture
* Components
* Communication flow

### LLD

**Low-Level Design**

Explains:

* APIs
* Database tables
* Services
* Implementation details

SA decides:

* Is the feature technically feasible?
* Do we have required skills?
* What technologies should be used?

---

# 7. Development Team

The actual implementation starts here.

Developers analyze requirements and identify needs such as:

* Kubernetes Cluster
* Docker
* Git repositories
* Databases
* AWS resources

This is where DevOps Engineers start receiving tasks.

---

# 8. DevOps Engineer Role

### Main Responsibilities

Provide infrastructure required by developers.

Examples:

* Create Kubernetes clusters
* Create AWS infrastructure
* Configure Docker
* Manage CI/CD pipelines
* Create Git repositories
* Automate deployments

### Important

DevOps engineers generally receive requirements from:

* Developers
* Solution Architects

Not from customers.

---

# 9. QA Engineer

### Responsibilities

* Test applications.
* Validate requirements.
* Perform automation testing.
* Perform manual testing.

Works closely with developers and DevOps engineers.

---

# 10. Database Administrator (DBA)

### Responsibilities

* Database administration.
* Monitoring databases.
* Performance tuning.
* Backup and recovery.

Sometimes DevOps creates databases, while DBA manages them.

---

# 11. SRE (Site Reliability Engineer)

After the application goes live:

### Responsibilities

* Reliability
* Availability
* Monitoring
* Alerting
* Dashboards
* Incident management

Tools often used:

* Prometheus
* Grafana
* ELK Stack

---

# 12. Technical Writer

### Responsibilities

* Creates documentation.
* Writes release notes.
* Documents features.

Example:

When Android releases a new feature, technical writers document:

* What changed
* How it works
* How users can use it

---

# 13. Scrum Team

A Scrum Team usually contains:

* Developers
* DevOps Engineers
* QA Engineers
* DBA
* Sometimes Technical Writers

All work together to complete a feature.

No single role completes the feature alone.

---

# 14. SDLC (Software Development Life Cycle)

The complete flow:

```text
Planning
   ↓
Analysis
   ↓
Design
   ↓
Implementation
   ↓
Testing & Integration
   ↓
Maintenance
```

---

## Phase 1: Planning

Handled mainly by:

* BA
* PM

Activities:

* Gather requirements
* Discuss customer needs

---

## Phase 2: Analysis

Activities:

* Feasibility study
* Requirement analysis
* Priority evaluation

---

## Phase 3: Design

Handled by:

* Solution Architect

Activities:

* HLD
* LLD

---

## Phase 4: Implementation

Handled by:

* Developers
* DevOps
* QA

Activities:

* Coding
* Infrastructure creation
* Automation

---

## Phase 5: Testing & Integration

Handled by:

* QA
* Developers
* DevOps

Activities:

* Testing
* Bug fixes
* Integration

---

## Phase 6: Maintenance

Handled by:

* SRE
* Operations teams

Activities:

* Monitoring
* Reliability
* Incident response

---

# 15. Additional Responsibility of DevOps

DevOps does not only create infrastructure.

DevOps also improves SDLC efficiency.

Goal:

```text
Reduce delivery time
Increase automation
Improve reliability
```

Examples:

### CI/CD

Automate:

```text
Code Commit
     ↓
Build
     ↓
Test
     ↓
Deploy
```

### Security

Integrate:

* SAST
* DAST
* Vulnerability scanning

### Automation

Reduce manual work wherever possible.

---

# 16. Why Jira is Needed

Problem:

Many teams are involved.

Management needs to know:

* Who is working on what?
* What is blocked?
* What is completed?
* What is delayed?

Solution:

**Jira**

A project management tool.

---

# 19. Important Jira Concepts

## Epic

Large business requirement.

Example:

```text
15-Minute Grocery Delivery
```

---

## Story

Small task under an Epic.

Examples:

```text
Create Mobile UI
Create Desktop UI
Create Kubernetes Cluster
Create AWS RDS Database
```

---

## Backlog

Collection of pending work.

All upcoming work is stored here.

---

## Sprint

Fixed duration work cycle.

Usually:

* 2 weeks
* 3 weeks

Example:

```text
Sprint 1
Day 1 → Day 14
```

Team commits to completing selected tasks.

---

## Sprint Planning

Meeting where team decides:

* Which backlog items will be worked on.

---

## Sprint Retrospective

Meeting after sprint completion.

Questions:

* What went well?
* What went wrong?
* What can be improved?

---

# 17. Example DevOps Story in Jira

Epic:

```text
15-Minute Delivery Service
```

Developer says:

> We need a Kubernetes cluster.

Story created:

```text
Create Kubernetes Cluster
```

Assigned to:

```text
DevOps Engineer
```

Another developer says:

> We need a database.

Story created:

```text
Create AWS RDS Database
```

Assigned to:

```text
DevOps Engineer
```

This is how DevOps receives day-to-day tasks.

---

# Interview Notes (Very Important)

### Who gathers customer requirements?

**Business Analyst (BA)**

### Who prioritizes requirements?

**Product Manager (PM)**

### Who converts requirements into actionable work?

**Product Owner (PO)**

### Who creates HLD and LLD?

**Solution Architect**

### Who creates infrastructure?

**DevOps Engineer**

### Who tests applications?

**QA Engineer**

### Who manages reliability after deployment?

**SRE**

### What is an Epic?

Large business requirement.

### What is a Story?

Small task under an Epic.

### What is a Sprint?

2–3 week work cycle.

### What is Jira?

Project management and work tracking tool.

---

# One-Line Summary

**Customer requirements flow through BA → PM → PO → Solution Architect → Developers → DevOps/QA/DBA, and all work is tracked through Jira using Epics, Stories, Backlogs, and Sprints while DevOps focuses on infrastructure, automation, CI/CD, and improving the SDLC process.**
