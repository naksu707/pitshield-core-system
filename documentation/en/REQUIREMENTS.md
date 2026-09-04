## Why PitShield? Market Needs & Value Proposition

Traditional auto repair shops and detailing centers face three major operational and financial pain points. **PitShield** directly solves these challenges through integrated Fintech solutions.

---

### 1. The Trust Deficit in Auto Repair
* **The Problem:** The automotive service sector suffers from a widespread lack of customer trust. Vehicle owners often feel uncertain about whether billed replacement parts were actually installed, if prices are fair, or if the diagnoses are genuine.
* **The PitShield Solution:** An immutable, transparent **Digital Vehicle History**. PitShield generates a verifiable digital service log featuring exact mileage tracking, logged replacement parts, and attached photo/video evidence for every service session.

---

### 2. Administrative Chaos & Margin Leaks
* **The Problem:** Many shop managers still rely on paper records, spreadsheets, or generic point-of-sale systems. These tools lack integration with fiscal regulations, digital payment flows, and automated financial tracking, resulting in lost revenue and administrative fatigue.
* **The PitShield Solution:** An integrated **Fintech Billing & Payment Module**. PitShield streamlines electronic invoicing, automates job-costing, connects seamlessly with digital payment gateways, and provides real-time shop performance analytics.

---

### 3. Uncovered Warranty Risks & Missed Upsell Revenue
* **The Problem:** When a part or repair fails post-service, the shop must either absorb the costly rework out-of-pocket or risk alienating the customer. Furthermore, traditional shops lack recurring financial products to increase average order value (AOV).
* **The PitShield Solution:** **Embedded Microinsurance & Extended Warranties**. PitShield enables workshops to issue insurance-backed extended protection plans directly at checkout. If a covered component fails within the coverage window, the claim is handled digitally—protecting shop margins while creating a new commission-based revenue stream.

---

## Comprehensive System Requirements & Business Rules

### A. Functional Requirements (FR)

| ID | Module | Description |
| :--- | :--- | :--- |
| **FR-01** | **Vehicle Management** | System must register and lookup vehicle history by License Plate or VIN, including make, model, year, and engine specifications. |
| **FR-02** | **Work Order Management** | System must manage job status lifecycle (Draft, Pending Approval, In Progress, Ready for Delivery, Invoiced). |
| **FR-03** | **Fintech Billing** | System must convert work orders into digital invoices with itemized labor, parts, taxes, and applied discounts. |
| **FR-04** | **Integrated Payments** | System must integrate payment gateways to process credit cards, bank transfers, and automated payment links via SMS/WhatsApp. |
| **FR-05** | **Warranty Issuance** | System must automatically evaluate warranty eligibility and offer one-click issuance for embedded microinsurance during checkout. |
| **FR-06** | **Claims Management** | System must provide a dedicated workflow to submit, review, and settle parts/service failure claims with photo/video evidence. |
| **FR-07** | **Inventory & Spare Parts** | System must track spare parts stock, unit costs, retail prices, and auto-deduct inventory upon work order completion. |
| **FR-08** | **Client Portal / Web App** | System must allow vehicle owners to access their digital maintenance record, view photos, and approve quotes remotely. |
| **FR-09** | **Commission & Financial Reports** | System must calculate workshop revenue, commission payouts from insurance providers, and sales tax summaries. |

---

### B. Business Rules (BR)

| ID | Rule Name | Description & Constraints |
| :--- | :--- | :--- |
| **BR-01** | **Warranty Eligibility** | Microinsurance can only be issued for vehicles with <120,000 km mileage, <10 years of age, and no commercial use (e.g., taxi/fleet). |
| **BR-02** | **Record Immutability** | Once an order or invoice is marked "Paid", record details cannot be edited/deleted. Adjustments require an auditable credit note. |
| **BR-03** | **Platform Revenue Share** | PitShield automatically deducts a platform service fee (%) per warranty issued and payment processed before settling to the workshop. |
| **BR-04** | **Mandatory Pre-Inspection** | To activate extended warranty coverage, the technician must upload at least two photos of the newly installed part and record initial mileage. |
| **BR-05** | **Stock Validation** | A work order cannot be set to "In Progress" if required replacement parts are out of stock in the workshop inventory module. |

---

### C. Non-Functional Requirements (NFR)

| ID | Category | Metric / Acceptance Criteria |
| :--- | :--- | :--- |
| **NFR-01** | **Security** | Role-Based Access Control (RBAC) with JWT auth, HTTPS/TLS 1.3 encryption, and OWASP Top 10 compliance. |
| **NFR-02** | **Availability** | Cloud-native deployment ensuring a minimum system uptime of 99.5% monthly. |
| **NFR-03** | **Multi-Tenancy** | Strict logical data isolation ensuring Workshop A can never access or query Workshop B's data. |
| **NFR-04** | **Performance** | Vehicle history and invoice search API queries must respond within <1.5 seconds under standard load. |
| **NFR-05** | **Fiscal Compliance** | System must support local electronic invoicing standards (e.g., DIAN, SAT, IRS equivalent) for invoice signing. |