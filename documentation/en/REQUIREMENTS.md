# Requirements Specification · PitShield Core System

> [🇪🇸 Español](../es/REQUERIMIENTOS.md) · 🇬🇧 English

| Field              | Value                                                   |
| ------------------ | ------------------------------------------------------- |
| **Product**        | PitShield Core System                                   |
| **Version**        | 1.0                                                     |
| **Status**         | Approved for design                                     |
| **Initial market** | Colombia (COP currency, DIAN electronic invoicing)      |
| **User stories**   | [`USER-STORY.md`](USER-STORY.md)                        |

> The Spanish version is the reference document, since development is done in Spanish. Requirement IDs are the same in both languages: **RF** (functional requirement), **RN** (business rule) and **RNF** (non-functional requirement).

---

## Contents

1. [Purpose and scope](#1-purpose-and-scope)
2. [Why PitShield? Market needs](#2-why-pitshield-market-needs)
3. [System roles](#3-system-roles)
4. [Functional requirements (RF)](#4-functional-requirements-rf)
5. [Business rules (RN)](#5-business-rules-rn)
6. [Non-functional requirements (RNF)](#6-non-functional-requirements-rnf)
7. [Constraints and assumptions](#7-constraints-and-assumptions)
8. [Release plan](#8-release-plan)
9. [Traceability matrix](#9-traceability-matrix)
10. [Glossary](#10-glossary)

---

## 1. Purpose and scope

This document defines **what** PitShield Core System must do and **under which conditions**. It is the basis for design, development, automated tests and manual tests.

**In scope:**

- Auto repair shops and detailing centers as customers of the platform (multi-workshop SaaS model).
- Customers, vehicles and the digital vehicle history.
- Scheduling, work orders, quotes, inventory and purchasing.
- Invoicing, in-person and online payments, credit notes and refunds.
- Extended warranties and microinsurance: eligibility, issuance, coverage, claims and commissions.
- Customer web portal, notifications, reports and AI support agents.

**Out of scope (version 1.0):**

- Native mobile apps (the customer portal is a responsive web app).
- Full accounting (payroll, balance sheets, tax returns). PitShield provides the reports an accountant needs.
- Issuing policies itself: the partner insurer carries the risk; PitShield is the sales and management channel.

---

## 2. Why PitShield? Market needs

Traditional auto repair shops and detailing centers face three major operational and financial problems. **PitShield** solves them with integrated Fintech features.

### 2.1 The trust deficit

* **The problem:** vehicle owners often doubt whether billed parts were actually installed, whether prices are fair or whether a diagnosis is genuine.
* **The solution:** an immutable, transparent **Digital Vehicle History**, with mileage, installed parts and photo or video evidence of every service.

### 2.2 Administrative chaos and lost margin

* **The problem:** many shops still rely on paper, spreadsheets or generic point-of-sale systems, with no electronic invoicing, digital payments or financial tracking.
* **The solution:** an integrated **billing and payments module**, with electronic invoicing, automatic job costing, payment gateways and real-time metrics.

### 2.3 Warranty risk and missed revenue

* **The problem:** when a part or repair fails after the service, the shop either pays for the rework or loses the customer. It also lacks recurring products that raise the average order value.
* **The solution:** **embedded extended warranties and microinsurance**, issued at checkout and backed by an insurer. Claims are handled digitally and the shop earns a commission on every product sold.

---

## 3. System roles

| Role                     | Description                                                                              |
| ------------------------ | ---------------------------------------------------------------------------------------- |
| **Platform Administrator** | PitShield staff. Onboards workshops and insurers, configures products and commissions. |
| **Workshop Administrator** | Owner or manager. Configures the workshop, manages users and reads reports.            |
| **Service Advisor**      | Receives vehicles, creates work orders and quotes, and serves the customer.              |
| **Technician**           | Diagnoses, records evidence, uses parts and does the work.                               |
| **Cashier**              | Issues invoices and records payments, credit notes and refunds.                          |
| **Inventory Manager**    | Manages parts, suppliers and purchases.                                                  |
| **Customer**             | Vehicle owner. Uses the portal to check, approve and pay.                                |
| **Insurer Auditor**      | Reviews and decides warranty and microinsurance claims.                                  |
| **System**               | Automated processes: scheduled jobs, webhooks and notifications.                         |

A user can hold more than one role within a workshop (for example, Administrator and Cashier in a small shop).

---

## 4. Functional requirements (RF)

### Module 1 · Authentication, users and security

| ID        | Requirement                                                                                                                    |
| --------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **RF-01** | The system must let users log in and out with email and password, and end the session automatically when it expires.         |
| **RF-02** | The system must let users recover their password by email and change it while logged in.                                      |
| **RF-03** | The system must let administrators create, edit, activate and deactivate users, and assign them one or more roles.            |
| **RF-04** | The system must keep an audit log of relevant actions (who, what, when and on which record) and let it be searched with filters. |
| **RF-05** | The system must record the customer's consent to personal data processing and handle requests to view, update or delete it.   |

### Module 2 · Workshops and configuration

| ID        | Requirement                                                                                                 |
| --------- | ----------------------------------------------------------------------------------------------------------- |
| **RF-06** | The system must let the workshop register and update its business and tax details (tax ID, legal name, logo). |
| **RF-07** | The system must let the workshop configure taxes, invoice numbering and its invoicing authorization.        |
| **RF-08** | The system must manage branches and their opening hours.                                                    |

### Module 3 · Customers, vehicles and digital history

| ID        | Requirement                                                                                                           |
| --------- | --------------------------------------------------------------------------------------------------------------------- |
| **RF-09** | The system must let users register, search and update customers, and link them to one or more vehicles.               |
| **RF-10** | The system must register vehicles by license plate and VIN, with make, model, year, engine, type of use and mileage.  |
| **RF-11** | The system must show the vehicle's digital history in chronological order: services, parts, evidence and coverage.    |
| **RF-12** | The system must allow transferring a vehicle to a new owner while keeping its history.                                |
| **RF-13** | The system must prevent deleting the history and keep the previous value of every correction.                        |

### Module 4 · Services, scheduling and technicians

| ID        | Requirement                                                                                          |
| --------- | ---------------------------------------------------------------------------------------------------- |
| **RF-14** | The system must manage the service catalog with price, estimated duration and status.                |
| **RF-15** | The system must let users create, confirm, reschedule and cancel appointments based on availability. |
| **RF-16** | The system must assign technicians to a work order and record labor time.                            |

### Module 5 · Work orders

| ID        | Requirement                                                                                                                       |
| --------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **RF-17** | The system must record the vehicle check-in: mileage, fuel level, visible damage, belongings left and check-in photos.            |
| **RF-18** | The system must create work orders with a unique code and control their life cycle according to the defined status flow (RN-10). |
| **RF-19** | The system must record symptoms, diagnosis, notes and media evidence.                                                             |
| **RF-20** | The system must generate versioned quotes with services, parts, labor, taxes and discounts.                                       |
| **RF-21** | The system must let the customer approve or reject the quote remotely.                                                            |
| **RF-22** | The system must record the vehicle hand-over with the exit mileage and the customer's acceptance.                                 |

### Module 6 · Inventory, suppliers and purchasing

| ID        | Requirement                                                                                                     |
| --------- | --------------------------------------------------------------------------------------------------------------- |
| **RF-23** | The system must manage parts with code, cost, sale price, and available, reserved and minimum stock.            |
| **RF-24** | The system must reserve, consume and return parts as the work order progresses, and record adjustments with a reason. |
| **RF-25** | The system must manage suppliers and purchase orders, and increase stock when goods are received.              |

### Module 7 · Invoicing and payments

| ID        | Requirement                                                                                                           |
| --------- | --------------------------------------------------------------------------------------------------------------------- |
| **RF-26** | The system must turn a finished work order into an invoice itemizing labor, parts, taxes and discounts.               |
| **RF-27** | The system must send the electronic invoice to the DIAN through an authorized provider and store its CUFE.            |
| **RF-28** | The system must record in-person payments (cash, card, bank transfer) and partial payments.                           |
| **RF-29** | The system must create online payment links and update the invoice when the gateway confirms the payment (webhook).   |
| **RF-30** | The system must issue credit notes and handle refunds without deleting the original invoice.                          |

### Module 8 · Warranties, microinsurance and claims

| ID        | Requirement                                                                                                                  |
| --------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **RF-31** | The system must let protection products be configured: type, insurer, coverage, term, price, commission and conditions.    |
| **RF-32** | The system must check the vehicle's eligibility and issue the warranty or microinsurance at checkout, with a digital certificate. |
| **RF-33** | The system must show coverage with its status and term, and handle its expiry and cancellation.                             |
| **RF-34** | The system must let users file claims with evidence, track them and record the auditor's decision.                          |
| **RF-35** | The system must calculate and settle platform and workshop commissions for every product sold and payment processed.        |

### Module 9 · Customer portal

| ID        | Requirement                                                                                                                  |
| --------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **RF-36** | The system must invite the customer to the portal and let them activate their account.                                       |
| **RF-37** | The portal must let customers view their vehicles, history, work orders, quotes, invoices, payments, coverage and claims.    |

### Module 10 · Notifications

| ID        | Requirement                                                                                               |
| --------- | --------------------------------------------------------------------------------------------------------- |
| **RF-38** | The system must send automatic email and WhatsApp notifications for service events.                       |
| **RF-39** | The system must create preventive maintenance reminders based on time or estimated mileage.               |
| **RF-40** | The system must let customers choose their notification channels and withdraw consent to messages.        |

### Module 11 · Reports and analytics

| ID        | Requirement                                                                                                     |
| --------- | --------------------------------------------------------------------------------------------------------------- |
| **RF-41** | The system must show a financial dashboard: revenue, outstanding balances, refunds and commissions by period.   |
| **RF-42** | The system must produce operational reports (work orders, times, services) and inventory reports (movements, critical stock). |
| **RF-43** | The system must export reports to CSV and PDF.                                                                  |

### Module 12 · Artificial intelligence agents

| ID        | Requirement                                                                                                                              |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **RF-44** | The system must offer AI support agents for diagnosis, preventive maintenance, customer service, inventory and claim pre-analysis.       |
| **RF-45** | The system must log every relevant interaction with the AI agents and whether their recommendation was accepted or dismissed.            |

### Module 13 · Platform administration

| ID        | Requirement                                                                                                  |
| --------- | ------------------------------------------------------------------------------------------------------------ |
| **RF-46** | The system must let platform administrators onboard, activate and suspend workshops, and create their first Workshop Administrator. |
| **RF-47** | The system must let platform administrators register partner insurers and their auditor users.               |

---

## 5. Business rules (RN)

| ID        | Rule                          | Description and constraints                                                                                                                                                     |
| --------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **RN-01** | Coverage eligibility          | By default, a protection product only applies to vehicles under 120,000 km, under 10 years old and for private use (no taxis or fleets). Each product can set its own limits.   |
| **RN-02** | Document immutability         | An issued invoice or an invoiced work order cannot be edited or deleted. Changes are made with auditable credit notes.                                                          |
| **RN-03** | Platform commission           | PitShield keeps a configurable percentage of every protection product issued and every online payment processed, before settling with the workshop.                           |
| **RN-04** | Mandatory inspection          | To activate coverage, the technician must upload at least 2 photos of the newly installed part and record the exact mileage.                                                    |
| **RN-05** | Stock validation              | A work order cannot move to "In Progress" if the required parts do not have enough available stock.                                                                             |
| **RN-06** | Workshop isolation            | Every operational record belongs to a workshop. Users only see their workshop's data, except Platform Administrators and Auditors on the claims assigned to them.               |
| **RN-07** | Lockout after failed logins   | After 5 failed logins within 15 minutes, the account is locked for 15 minutes. Password recovery links expire after 30 minutes and can be used once.                           |
| **RN-08** | Vehicle identity              | License plate and VIN are unique within a workshop. History recorded by another workshop is only visible if the owner allows it from the portal.                               |
| **RN-09** | Quote validity                | A quote expires after 15 days (configurable). Any additional work requires a new version approved by the customer.                                                             |
| **RN-10** | Work order status flow        | Draft → Pending Approval → Approved → In Progress ⇄ On Hold → Finished → Ready for Pickup → Delivered. "Cancelled" is only possible before "Finished".                        |
| **RN-11** | Invoice origin                | Only a work order in "Finished" status or later can be invoiced. A work order produces a single invoice.                                                                        |
| **RN-12** | Idempotent payments           | The gateway's transaction ID is unique. The same event received twice does not record two payments.                                                                             |
| **RN-13** | Partial payments              | An invoice is "Paid" when the sum of its payments equals the total. The balance can never be negative or exceed the total.                                                     |
| **RN-14** | Claim conditions              | A claim can only be filed with active coverage, within 30 days of the failure and with at least one piece of evidence of the failure.                                           |
| **RN-15** | Human decision                | AI agents only recommend. No final status (diagnosis, coverage, claim, payment) changes without an action by an authorized user.                                               |
| **RN-16** | Reminder limit                | At most one reminder per vehicle and condition every 30 days, and never to a customer who withdrew consent.                                                                     |
| **RN-17** | No negative stock             | No movement can take a part's available stock below zero.                                                                                                                       |
| **RN-18** | Currency and taxes            | Amounts are in Colombian pesos (COP). Default VAT is 19 %, and each service or part can have its own rate (including exempt).                                                  |
| **RN-19** | Personal data                 | Customer data is only processed with explicit consent, under Colombian Law 1581 of 2012. Data owner requests are answered within 15 business days.                            |
| **RN-20** | Cancellation after consumption | If a work order already consumed parts, cancelling it requires invoicing what was used or a justification approved by the Workshop Administrator.                             |

---

## 6. Non-functional requirements (RNF)

| ID         | Category              | Acceptance criteria / metric                                                                                                                                       |
| ---------- | --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **RNF-01** | Security              | Role-based access control (RBAC) with short-lived JWTs and refresh tokens, BCrypt passwords, HTTPS (TLS 1.2 or later) and mitigation of the OWASP Top 10.        |
| **RNF-02** | Availability          | In production, at least 99.5 % monthly uptime.                                                                                                                     |
| **RNF-03** | Multi-tenancy         | Strict logical isolation: Workshop A can never see or query Workshop B's data. Checked by automated tests on every endpoint.                                        |
| **RNF-04** | Performance           | With 50 concurrent users per workshop, the 95th percentile of queries (history, inventory, invoices) is under 1.5 s and generating an invoice takes under 3 s.    |
| **RNF-05** | Tax compliance        | Electronic invoicing according to current DIAN rules, through an authorized technology provider.                                                                  |
| **RNF-06** | Privacy               | Compliance with Law 1581 of 2012 (habeas data). Sensitive data is encrypted at rest and never written to logs.                                                    |
| **RNF-07** | Usability             | Responsive interface (customers use the portal on their phones) and accessible according to WCAG 2.1 level AA.                                                     |
| **RNF-08** | Localization          | Interface in Spanish (es-CO), COP currency, America/Bogota time zone and dd/mm/yyyy dates.                                                                         |
| **RNF-09** | Maintainability       | Modular monolith with one module per domain. Code in Spanish, mandatory pull request review and static analysis in CI.                                           |
| **RNF-10** | Quality and testing   | At least 80 % coverage in services and domain. CI blocks the merge when a test fails. Critical flows have end-to-end tests.                                        |
| **RNF-11** | Observability         | Structured logs with a correlation ID, health checks and exposed metrics.                                                                                          |
| **RNF-12** | Backup                | Daily database backups kept for at least 7 days (maximum data loss: 24 hours).                                                                                     |
| **RNF-13** | Media files           | JPG/PNG photos up to 10 MB and MP4 videos up to 100 MB, stored in object storage and served through temporary links.                                              |
| **RNF-14** | API                   | Versioned REST API (`/api/v1`) documented with OpenAPI.                                                                                                             |
| **RNF-15** | Portability           | Backend, frontend and database run in Docker containers. The local environment starts with a single command.                                                       |

---

## 7. Constraints and assumptions

**Constraints**

- Backend in Java with Spring Boot, frontend in React with TypeScript, and a PostgreSQL database.
- Development (code, database, commits and issues) is done in Spanish. Documentation is published in Spanish and English.
- A team of 3 developers, managed with GitHub Projects.

**Assumptions**

- External integrations (payment gateway, electronic invoicing, insurer and WhatsApp) are first built against their sandbox environments or simulators.
- The partner insurer defines the real coverage. The values in this document are configurable references.
- The customer portal and the workshop system share the same frontend, with views based on the user's role.

---

## 8. Release plan

| Release       | Content                                                                                                              | Modules        |
| ------------- | -------------------------------------------------------------------------------------------------------------------- | -------------- |
| **MVP**       | Access and roles, workshops, customers, vehicles and history, scheduling, work orders, inventory, invoicing and in-person payments | 1 – 7, 13 (workshop onboarding) |
| **Release 2** | Online payments, electronic invoicing, warranties and microinsurance, claims, customer portal and notifications     | 7 – 10, 13     |
| **Release 3** | Reports, exports and artificial intelligence agents                                                                  | 11, 12         |

The priority and release of each user story are listed in [`USER-STORY.md`](USER-STORY.md).

---

## 9. Traceability matrix

| Requirement | User stories              | Requirement | User stories              |
| ----------- | ------------------------- | ----------- | ------------------------- |
| RF-01       | HU-001, HU-049            | RF-25       | HU-024                    |
| RF-02       | HU-002                    | RF-26       | HU-025                    |
| RF-03       | HU-003                    | RF-27       | HU-057                    |
| RF-04       | HU-004                    | RF-28       | HU-056                    |
| RF-05       | HU-050                    | RF-29       | HU-026, HU-027            |
| RF-06       | HU-005                    | RF-30       | HU-028                    |
| RF-07       | HU-051                    | RF-31       | HU-065                    |
| RF-08       | HU-006                    | RF-32       | HU-029, HU-030            |
| RF-09       | HU-007, HU-052            | RF-33       | HU-031, HU-058            |
| RF-10       | HU-008                    | RF-34       | HU-032, HU-033            |
| RF-11       | HU-009                    | RF-35       | HU-059                    |
| RF-12       | HU-010                    | RF-36       | HU-060                    |
| RF-13       | HU-011                    | RF-37       | HU-034 – HU-037           |
| RF-14       | HU-012                    | RF-38       | HU-038                    |
| RF-15       | HU-013                    | RF-39       | HU-039                    |
| RF-16       | HU-014, HU-053            | RF-40       | HU-061                    |
| RF-17       | HU-054                    | RF-41       | HU-040                    |
| RF-18       | HU-015, HU-019, HU-020    | RF-42       | HU-041, HU-042            |
| RF-19       | HU-016                    | RF-43       | HU-062                    |
| RF-20       | HU-017                    | RF-44       | HU-043 – HU-047           |
| RF-21       | HU-018                    | RF-45       | HU-048                    |
| RF-22       | HU-055                    | RF-46       | HU-063                    |
| RF-23       | HU-021                    | RF-47       | HU-064                    |
| RF-24       | HU-022, HU-023            |             |                           |

---

## 10. Glossary

| Term                    | Meaning                                                                                                   |
| ----------------------- | --------------------------------------------------------------------------------------------------------- |
| **Work order (OT)**     | The record of everything done to a vehicle during one visit to the workshop.                              |
| **VIN**                 | Vehicle Identification Number, unique worldwide (17 characters).                                          |
| **Workshop (tenant)**   | Each company that uses PitShield. Its data is isolated from other workshops.                              |
| **Extended warranty**   | A commitment to repair a part or job if it fails within a period beyond the legal warranty.               |
| **Microinsurance**      | A low-cost policy backed by an insurer that covers defined mechanical failures.                          |
| **Coverage**            | A warranty or microinsurance issued for a vehicle, with its term and conditions.                         |
| **Claim**               | A request for the coverage to pay for a failure.                                                          |
| **Credit note**         | A document that cancels or reduces an invoice without deleting it.                                        |
| **CUFE**                | The unique code the DIAN assigns to every electronic invoice.                                             |
| **Webhook**             | An automatic message an external service (for example, the payment gateway) sends to PitShield when something happens. |
| **Idempotency**         | A property of an operation that gives the same result when repeated (it prevents duplicate payments).     |
| **RBAC**                | Role-based access control.                                                                                |
