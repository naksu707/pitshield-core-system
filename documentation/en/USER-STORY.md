# User Stories - PitShield Core System

> [🇪🇸 Español](../es/HISTORIAS-USUARIO.md) · 🇬🇧 English

> **Production Backlog Document:** User Stories (HU) with acceptance criteria in BDD (Behavior-Driven Development / Gherkin) format for the development of the PitShield Core System platform.

| Field             | Value                                                                                |
| ----------------- | ------------------------------------------------------------------------------------ |
| **Total stories** | 65 stories in 13 modules                                                             |
| **Requirements**  | [`REQUIREMENTS.md`](REQUIREMENTS.md) (the RF, RN and RNF cited in each story)        |
| **Priority**      | High (essential for its release) · Medium (important) · Low (nice to have)           |
| **Releases**      | MVP · Release 2 · Release 3 (see the release plan in the requirements)               |

> The Spanish version is the reference document, since development is done in Spanish. Story IDs (HU) and requirement IDs are the same in both languages. The roles are described in section 3 of the requirements. Stories inside a module are not always in numerical order: new stories took the next available number so existing IDs never change.

---

## Modules

1. [Module 1: Authentication, Users and Security](#1-module-1-authentication-users-and-security)
2. [Module 2: Workshops and Configuration](#2-module-2-workshops-and-configuration)
3. [Module 3: Customers, Vehicles and Digital History](#3-module-3-customers-vehicles-and-digital-history)
4. [Module 4: Services, Scheduling and Technicians](#4-module-4-services-scheduling-and-technicians)
5. [Module 5: Work Orders](#5-module-5-work-orders)
6. [Module 6: Inventory, Suppliers and Purchasing](#6-module-6-inventory-suppliers-and-purchasing)
7. [Module 7: Invoicing and Payments](#7-module-7-invoicing-and-payments)
8. [Module 8: Warranties, Microinsurance and Claims](#8-module-8-warranties-microinsurance-and-claims)
9. [Module 9: Customer Portal](#9-module-9-customer-portal)
10. [Module 10: Automated Notifications](#10-module-10-automated-notifications)
11. [Module 11: Reports and Analytics](#11-module-11-reports-and-analytics)
12. [Module 12: Artificial Intelligence Agents](#12-module-12-artificial-intelligence-agents)
13. [Module 13: Platform Administration](#13-module-13-platform-administration)
14. [Cross-cutting acceptance rules](#cross-cutting-acceptance-rules)
15. [Definition of done](#definition-of-done)

---

# 1. Module 1: Authentication, Users and Security

### HU-001: Login and Role-Based Access Control (RBAC)
* **As a:** System User
* **I want to:** Log in with my credentials
* **So that:** I can only reach the features my role allows.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-01, RN-06, RN-07

```gherkin
Scenario: Successful login
  GIVEN the user exists and is active
  WHEN they enter valid credentials
  THEN the system grants access
  AND shows only the modules allowed for their role.

Scenario: Invalid credentials
  GIVEN the user exists
  WHEN they enter a wrong password
  THEN the system denies access
  AND shows an invalid credentials message.

Scenario: Inactive user
  GIVEN the user is deactivated
  WHEN they try to log in with valid credentials
  THEN the system denies access
  AND shows a message saying the account is not active.
```

### HU-002: Password Recovery and Change
* **As a:** System User
* **I want to:** Recover or change my password
* **So that:** I keep secure access to my account.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-02, RN-07

```gherkin
Scenario: Password recovery
  GIVEN the user has a registered email
  WHEN they request password recovery
  THEN the system sends a temporary link to that email
  AND lets them set a new password.

Scenario: Password change while logged in
  GIVEN the user is logged in
  WHEN they enter their current password and a valid new password
  THEN the system updates the password
  AND confirms the change.
```

### HU-003: User and Role Management
* **As a:** Workshop Administrator
* **I want to:** Create, edit, activate and deactivate users and assign roles
* **So that:** I control who can use each feature of the system.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-03

```gherkin
Scenario: User creation
  GIVEN the administrator is in User Management
  WHEN they register a user with valid data and assign a role
  THEN the system creates the account
  AND makes it available according to the configured status.

Scenario: User deactivation
  GIVEN an active user exists
  WHEN the administrator deactivates them
  THEN the system blocks new logins
  AND keeps their action history.
```

### HU-004: Action and Access Auditing
* **As a:** Workshop Administrator
* **I want to:** Review the relevant actions performed in the system
* **So that:** I keep traceability and detect unauthorized changes.
* **Priority:** Medium · **Release:** MVP · **Requirements:** RF-04

```gherkin
Scenario: Auditable action recorded
  GIVEN a user modifies a critical record
  WHEN the operation is completed
  THEN the system records the user, date, time, action and affected record
  AND keeps the audit information.

Scenario: Audit search
  GIVEN audit events exist
  WHEN the administrator searches the audit log
  THEN the system allows filtering by user, date, module and action type.
```

### HU-049: Logout and Session Expiry
* **As a:** System User
* **I want to:** Log out and have my session close by itself when idle
* **So that:** Nobody else can use my account on a shared computer.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-01

```gherkin
Scenario: Logout
  GIVEN the user has an active session
  WHEN they click "Log Out"
  THEN the system invalidates the session
  AND redirects them to the login screen.

Scenario: Expired session
  GIVEN the user's session expired due to inactivity
  WHEN they try to perform an operation
  THEN the system rejects the operation
  AND asks them to log in again without losing the screen they were on.

Scenario: Lockout after failed attempts
  GIVEN the user entered a wrong password 5 times within 15 minutes
  WHEN they try to log in again
  THEN the system locks the account for 15 minutes
  AND records the lockout in the audit log.
```

### HU-050: Personal Data Consent and Rights
* **As a:** Customer
* **I want to:** Consent to the processing of my data and be able to view, update or request deletion of it
* **So that:** I stay in control of my personal information (Colombian Law 1581 of 2012).
* **Priority:** High · **Release:** MVP · **Requirements:** RF-05, RN-19

```gherkin
Scenario: Consent recorded
  GIVEN the advisor registers a new customer
  WHEN the customer accepts the data processing policy
  THEN the system stores the date, channel and version of the accepted policy.

Scenario: Customer without consent
  GIVEN the customer has not accepted the data processing policy
  WHEN the advisor tries to send them communications
  THEN the system blocks the message
  AND shows that consent is missing.

Scenario: Deletion request
  GIVEN the customer asks to delete their personal data
  WHEN the administrator approves the request
  THEN the system anonymizes the customer's personal data
  AND keeps the tax documents the law requires to be stored.
```

---

# 2. Module 2: Workshops and Configuration

### HU-005: Workshop Data Configuration
* **As a:** Workshop Administrator
* **I want to:** Register and update the workshop's business and tax details
* **So that:** They are used on invoices, receipts and communications.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-06

```gherkin
Scenario: Successful update
  GIVEN the administrator is in Settings
  WHEN they change the allowed fields and save
  THEN the system updates the workshop profile
  AND uses the new data in future documents.
```

### HU-006: Branch and Opening Hours Management
* **As a:** Workshop Administrator
* **I want to:** Configure branches, opening hours and availability
* **So that:** I can organize the workshop's operation and schedule.
* **Priority:** Medium · **Release:** MVP · **Requirements:** RF-08

```gherkin
Scenario: Branch creation
  GIVEN the administrator has configuration permissions
  WHEN they register a branch with valid data
  THEN the system creates the branch
  AND allows setting its opening hours.

Scenario: Opening hours update
  GIVEN a branch exists
  WHEN the administrator changes its opening hours
  THEN the system updates availability for future appointments.
```

### HU-051: Tax and Invoice Numbering Configuration
* **As a:** Workshop Administrator
* **I want to:** Configure tax rates, the invoicing authorization and its numbering
* **So that:** Invoices are valid and use the authorized sequence.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-07, RN-18

```gherkin
Scenario: Invoicing authorization recorded
  GIVEN the administrator is in Settings
  WHEN they register the authorization number, prefix, authorized range and validity
  THEN the system stores the authorization
  AND uses it to number the next invoices.

Scenario: Numbering range used up
  GIVEN the last invoice of the authorized range was issued
  WHEN the cashier tries to issue another invoice
  THEN the system blocks it
  AND warns the administrator to register a new authorization.

Scenario: Tax rate per item
  GIVEN a service or part has a VAT rate configured
  WHEN it is included in a quote or invoice
  THEN the system calculates the tax with that rate.
```

---

# 3. Module 3: Customers, Vehicles and Digital History

### HU-007: Customer Registration and Vehicle Linking
* **As a:** Service Advisor
* **I want to:** Register a customer and link them to one or more vehicles
* **So that:** I keep the owner's information and make communication easier.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-09

```gherkin
Scenario: Successful registration and linking
  GIVEN the customer does not exist
  WHEN the advisor fills in the required data and links a vehicle
  THEN the system creates the profile
  AND links the customer to the vehicle.

Scenario: Existing customer
  GIVEN the customer already exists
  WHEN the advisor enters a registered ID
  THEN the system shows the existing customer
  AND allows linking a new vehicle without duplicating the profile.
```

### HU-008: Vehicle Registration and Initial History
* **As a:** Service Advisor
* **I want to:** Register a vehicle with plate, VIN, make, model, year and mileage
* **So that:** Its digital service record is created.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-10, RN-08

```gherkin
Scenario: Successful registration
  GIVEN the plate and VIN are not registered
  WHEN the advisor fills in the required fields
  AND clicks "Save Vehicle"
  THEN the system creates the profile
  AND starts the vehicle timeline.

Scenario: Duplicate plate or VIN
  GIVEN the plate or VIN already exists
  WHEN the user tries to register the vehicle
  THEN the system blocks the duplicate
  AND shows the existing record.
```

### HU-009: Digital History Lookup
* **As a:** Technician
* **I want to:** Search a vehicle by plate or VIN
* **So that:** I can see its services, parts, evidence and coverage.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-11, RN-08

```gherkin
Scenario: Successful lookup
  GIVEN the vehicle has recorded history
  WHEN the technician searches it by plate or VIN
  THEN the system shows the history in chronological order
  AND allows viewing the authorized evidence.

Scenario: Vehicle not found
  GIVEN the vehicle does not exist
  WHEN the technician searches for it
  THEN the system says it was not found
  AND offers to register it if the user has permission.
```

### HU-010: Vehicle Ownership Transfer
* **As a:** Administrator / Service Advisor
* **I want to:** Change the owner linked to a vehicle
* **So that:** The history continues without deleting earlier information.
* **Priority:** Medium · **Release:** MVP · **Requirements:** RF-12

```gherkin
Scenario: Successful transfer
  GIVEN the vehicle has a current owner
  WHEN an authorized user registers the new owner and confirms the transfer
  THEN the system updates the current owner
  AND keeps the vehicle's previous history.

Scenario: Transfer traceability
  GIVEN a transfer was made
  WHEN the audit log is reviewed
  THEN the system shows who made the change, when, and which owners were linked.
```

### HU-011: History Immutability and Auditing
* **As a:** Workshop Administrator
* **I want to:** Guarantee traceability of critical events in the vehicle history
* **So that:** Historical information cannot be deleted or changed without control.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-13

```gherkin
Scenario: Attempt to delete a history record
  GIVEN a history record is linked to a finished work order
  WHEN a user tries to delete it
  THEN the system blocks the deletion
  AND records the attempt in the audit log.

Scenario: Correcting information
  GIVEN some information needs a correction
  WHEN an authorized user makes an allowed change
  THEN the system keeps the previous value
  AND records the new value, user, date and reason.
```

### HU-052: Customer Search and Update
* **As a:** Service Advisor
* **I want to:** Search customers by ID, name, phone or plate and update their data
* **So that:** I serve them quickly and keep their contact details up to date.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-09

```gherkin
Scenario: Customer search
  GIVEN customers are registered in the workshop
  WHEN the advisor types at least 3 characters of the ID, name, phone or plate
  THEN the system shows the matching customers
  AND their linked vehicles.

Scenario: Contact details update
  GIVEN the customer changed their phone or email
  WHEN the advisor updates the data and saves
  THEN the system stores the new data
  AND records the previous value in the audit log.

Scenario: Duplicate ID
  GIVEN a customer with the same ID type and number already exists
  WHEN the advisor tries to assign that ID to another customer
  THEN the system blocks the change
  AND shows the existing customer.
```

---

# 4. Module 4: Services, Scheduling and Technicians

### HU-012: Service Catalog Management
* **As a:** Workshop Administrator
* **I want to:** Create, edit, activate or deactivate services
* **So that:** The catalog the workshop offers stays up to date.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-14

```gherkin
Scenario: Create a service
  GIVEN the administrator has permission
  WHEN they enter a valid name, description, price and estimated duration
  THEN the system creates the service
  AND makes it available for quotes and appointments.

Scenario: Deactivate a service
  GIVEN an active service exists
  WHEN the administrator deactivates it
  THEN it is no longer available for new appointments
  AND it stays in historical records.
```

### HU-013: Appointment and Schedule Management
* **As a:** Customer / Service Advisor
* **I want to:** Create, view, confirm, reschedule and cancel appointments
* **So that:** The workshop's work is organized.
* **Priority:** Medium · **Release:** MVP · **Requirements:** RF-15

```gherkin
Scenario: Appointment created
  GIVEN there is availability for the requested service
  WHEN the user selects the vehicle, service, date and time
  THEN the system creates the appointment
  AND sets its status to "Pending" or "Confirmed" according to the configured flow.

Scenario: Time slot not available
  GIVEN the time slot is already taken
  WHEN the user tries to book it
  THEN the system blocks the booking
  AND shows available time slots.

Scenario: Rescheduling
  GIVEN an active appointment exists
  WHEN an authorized user selects a new available time slot
  THEN the system updates the appointment
  AND keeps a history of the change.
```

### HU-014: Technician Assignment to a Work Order
* **As a:** Service Advisor / Administrator
* **I want to:** Assign one or more technicians to a work order
* **So that:** It is clear who is responsible for the work.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-16

```gherkin
Scenario: Successful assignment
  GIVEN a work order is pending execution
  WHEN the advisor selects an available technician
  THEN the system assigns them to the work order
  AND records the date and the user who made the assignment.

Scenario: Technician not available
  GIVEN the technician has no availability for the required period
  WHEN the advisor tries to assign them
  THEN the system warns that they are not available
  AND asks to choose another technician or period.
```

### HU-053: Labor Time Tracking
* **As a:** Technician
* **I want to:** Start, pause and finish time tracking on the tasks of a work order
* **So that:** The workshop knows the real time of each job and invoices it correctly.
* **Priority:** Medium · **Release:** MVP · **Requirements:** RF-16

```gherkin
Scenario: Time recorded
  GIVEN the technician is assigned to a work order in "In Progress"
  WHEN they start and then finish a task
  THEN the system records the duration
  AND adds it to the work order's labor.

Scenario: Task without assignment
  GIVEN the technician is not assigned to the work order
  WHEN they try to record time on it
  THEN the system blocks the entry.

Scenario: Time above the estimate
  GIVEN the recorded time exceeds the service's estimated duration
  WHEN the technician finishes the task
  THEN the system alerts the advisor
  AND asks the technician for a note.
```

---

# 5. Module 5: Work Orders

### HU-015: Work Order Creation
* **As a:** Service Advisor
* **I want to:** Create a work order linked to a customer, a vehicle and the requested services
* **So that:** The vehicle's service formally begins.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-18

```gherkin
Scenario: Work order created
  GIVEN the customer and vehicle are registered
  WHEN the advisor selects the requested services
  AND saves the order
  THEN the system generates a unique work order code
  AND creates it in "Draft" status.
```

### HU-016: Vehicle Diagnosis and Evidence
* **As a:** Technician
* **I want to:** Record symptoms, diagnosis, notes and evidence
* **So that:** The vehicle's condition is technically documented.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-19

```gherkin
Scenario: Diagnosis recorded
  GIVEN a work order is in an editable status
  WHEN the technician records the diagnosis and uploads the required evidence
  THEN the system stores the information
  AND links it to the work order and the vehicle history.

Scenario: Mandatory evidence
  GIVEN a service requires check-in evidence
  WHEN the technician tries to move forward without uploading it
  THEN the system blocks the progress
  AND asks for the missing evidence.
```

### HU-017: Quote Generation
* **As a:** Service Advisor
* **I want to:** Generate a quote with services, parts, labor, taxes and discounts
* **So that:** The customer knows the estimated cost before additional work is done.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-20, RN-09, RN-18

```gherkin
Scenario: Quote generated
  GIVEN the work order has valid services and costs
  WHEN the advisor generates the quote
  THEN the system calculates subtotals, taxes, discounts and total
  AND records the quote version.

Scenario: Quote changed
  GIVEN the quote has not been approved yet
  WHEN the advisor changes its items
  THEN the system recalculates the total
  AND keeps the previous version for traceability.
```

### HU-018: Remote Quote Approval
* **As a:** Vehicle Owner
* **I want to:** Review and approve or reject the quote from my phone
* **So that:** I can authorize the work without going to the workshop.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-21, RN-09

```gherkin
Scenario: Approval
  GIVEN the customer received a valid quote
  WHEN they review the details and click "Approve Work"
  THEN the system records the approval
  AND moves the work order to the corresponding status.

Scenario: Rejection
  GIVEN the customer received a valid quote
  WHEN they click "Reject Work" and give a reason
  THEN the system records the rejection
  AND notifies the workshop.
```

### HU-019: Work Order Life Cycle Management
* **As a:** Administrator / Service Advisor
* **I want to:** Control the statuses of a work order
* **So that:** Operations happen in the right order.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-18, RN-05, RN-10

```gherkin
Scenario: Valid status change
  GIVEN the work order meets the conditions of its current status
  WHEN an authorized user asks to move it forward
  THEN the system changes it to the next allowed status
  AND records the transition in the audit log.

Scenario: Status change not allowed
  GIVEN the work order does not meet the required conditions
  WHEN the user tries to move it forward
  THEN the system blocks the transition
  AND shows the pending conditions.
```

> **Status flow (RN-10):** Draft → Pending Approval → Approved → In Progress ⇄ On Hold → Finished → Ready for Pickup → Delivered. "Cancelled" is only possible before "Finished".

### HU-020: Controlled Work Order Cancellation and Changes
* **As a:** Service Advisor / Administrator
* **I want to:** Cancel or change a work order depending on its status
* **So that:** Changes requested by the customer or unexpected events are reflected.
* **Priority:** Medium · **Release:** MVP · **Requirements:** RF-18, RN-10, RN-20

```gherkin
Scenario: Work order cancelled
  GIVEN the work order is in a status that allows cancellation
  WHEN an authorized user gives a reason and confirms
  THEN the system changes the work order to "Cancelled"
  AND runs the corresponding inventory and invoicing operations.

Scenario: Change not allowed
  GIVEN the work order is in a closed status
  WHEN the user tries to change it
  THEN the system blocks the edit
  AND records the attempt when applicable.
```

### HU-054: Vehicle Check-in
* **As a:** Service Advisor
* **I want to:** Record the vehicle's condition when it is received
* **So that:** There is proof of how it arrived and disputes with the customer are avoided.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-17

```gherkin
Scenario: Check-in recorded
  GIVEN the vehicle arrives at the workshop
  WHEN the advisor records mileage, fuel level, visible damage, belongings left and check-in photos
  THEN the system stores the check-in
  AND links it to the work order and the vehicle history.

Scenario: Mileage lower than the last recorded
  GIVEN the history has a higher mileage than the one entered
  WHEN the advisor saves the check-in
  THEN the system shows an alert
  AND requires a note explaining the difference.

Scenario: Receipt for the customer
  GIVEN the check-in was recorded
  WHEN the advisor confirms it
  THEN the system generates a check-in receipt
  AND sends it to the customer through the configured channel.
```

### HU-055: Vehicle Hand-over to the Customer
* **As a:** Service Advisor
* **I want to:** Record the vehicle hand-over with the customer's acceptance
* **So that:** The visit is closed with proof of the exit condition.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-22

```gherkin
Scenario: Successful hand-over
  GIVEN the work order is "Ready for Pickup"
  WHEN the advisor records the exit mileage and the customer's acceptance
  THEN the system changes the work order to "Delivered"
  AND adds the hand-over to the vehicle history.

Scenario: Hand-over with an outstanding balance
  GIVEN the work order's invoice has an outstanding balance
  WHEN the advisor tries to record the hand-over
  THEN the system warns about the outstanding balance
  AND only continues with the Workshop Administrator's authorization.

Scenario: Customer not satisfied
  GIVEN the customer is not satisfied with the work
  WHEN the advisor records the complaint and its reason
  THEN the system stores it in the work order
  AND notifies the Workshop Administrator.
```

---

# 6. Module 6: Inventory, Suppliers and Purchasing

### HU-021: Parts and Stock Management
* **As a:** Inventory Manager
* **I want to:** View and manage spare parts stock
* **So that:** I keep control of the available inventory.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-23, RN-17

```gherkin
Scenario: Stock lookup
  GIVEN spare parts are registered
  WHEN the manager views the inventory
  THEN the system shows available, reserved and used quantities.

Scenario: Minimum stock
  GIVEN a part reaches or falls below its configured minimum stock
  WHEN the system updates the inventory
  THEN it creates a restocking alert.
```

### HU-022: Parts Reservation and Consumption
* **As a:** System / Inventory Manager
* **I want to:** Reserve and deduct parts as a work order progresses
* **So that:** Available stock always matches the parts actually used.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-24, RN-05, RN-17

```gherkin
Scenario: Stock reservation
  GIVEN an approved work order requires 2 units of a part
  WHEN the system confirms the work
  THEN it reserves the 2 units
  AND lowers the available stock without marking them as consumed yet.

Scenario: Consumption
  GIVEN the parts were used
  WHEN the technician records the consumption
  THEN the system marks them as consumed
  AND updates the inventory.
```

### HU-023: Inventory Returns and Adjustments
* **As a:** Inventory Manager
* **I want to:** Record returns and adjustments for damage, shrinkage or corrections
* **So that:** Physical and digital inventory stay in sync.
* **Priority:** Medium · **Release:** MVP · **Requirements:** RF-24, RN-17

```gherkin
Scenario: Unused part returned
  GIVEN a part is reserved but was not used
  WHEN the manager records its return
  THEN the system releases the reservation
  AND adds the quantity back to available stock.

Scenario: Shrinkage adjustment
  GIVEN there is a justified physical difference
  WHEN the manager records the adjustment with a reason
  THEN the system updates the stock
  AND records the movement in the audit log.
```

### HU-024: Supplier and Purchase Order Management
* **As a:** Inventory Manager
* **I want to:** Register suppliers and purchase orders
* **So that:** I control the supply of spare parts.
* **Priority:** Medium · **Release:** MVP · **Requirements:** RF-25

```gherkin
Scenario: Supplier registered
  GIVEN the supplier does not exist
  WHEN the manager registers its data
  THEN the system creates the supplier.

Scenario: Purchase received
  GIVEN a pending purchase order exists
  WHEN the manager records the receipt of 10 units
  THEN the system increases the stock
  AND records the purchase unit cost.
```

---

# 7. Module 7: Invoicing and Payments

### HU-025: Work Order to Invoice Conversion
* **As a:** Administrator / Cashier
* **I want to:** Generate an invoice from a finished work order
* **So that:** The service charge is formalized.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-26, RN-02, RN-11

```gherkin
Scenario: Invoice generated
  GIVEN the work order is finished and has a valid total
  WHEN the cashier generates the invoice
  THEN the system creates a unique document
  AND keeps its link to the work order.
```

### HU-026: Remote Payment and Payment Link
* **As a:** Administrator / Cashier
* **I want to:** Send a payment link to the customer
* **So that:** They can pay remotely.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-29

```gherkin
Scenario: Link sent
  GIVEN a pending invoice exists
  WHEN the cashier requests a payment link
  THEN the system generates a link tied to the invoice
  AND sends it through the configured channel.

Scenario: Payment declined
  GIVEN the customer tries to pay an invoice
  WHEN the gateway declines the transaction
  THEN the invoice stays pending
  AND the system records the result of the attempt.
```

### HU-027: Payment Confirmation via Webhook
* **As a:** System
* **I want to:** Update the invoice status when the gateway confirms a payment
* **So that:** Payments and invoices stay in sync.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-29, RN-12, RN-13

```gherkin
Scenario: Successful payment
  GIVEN a pending invoice exists
  WHEN a valid webhook confirms the payment
  THEN the system records the transaction
  AND marks the invoice as "Paid".

Scenario: Duplicate webhook
  GIVEN a payment was already recorded
  WHEN the gateway sends the same event again
  THEN the system does not duplicate the payment
  AND keeps a single record of the transaction.
```

### HU-028: Credit Notes and Refunds
* **As a:** Administrator / Cashier
* **I want to:** Cancel or adjust invoices and handle refunds
* **So that:** Accounting traceability is kept without deleting documents.
* **Priority:** Medium · **Release:** MVP · **Requirements:** RF-30, RN-02

```gherkin
Scenario: Credit note
  GIVEN an issued invoice needs an adjustment
  WHEN the administrator records the reason
  THEN the system generates the corresponding credit note
  AND keeps the original invoice.

Scenario: Refund
  GIVEN a payment can be refunded
  WHEN an authorized user requests a refund
  THEN the system records the request
  AND updates its status according to the gateway's response.
```

### HU-056: In-Person and Partial Payments
* **As a:** Cashier
* **I want to:** Record cash, card or bank transfer payments, in full or in part
* **So that:** I know exactly what each customer has paid.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-28, RN-13

```gherkin
Scenario: Full payment
  GIVEN a pending invoice for $500,000 exists
  WHEN the cashier records a cash payment of $500,000
  THEN the system marks the invoice as "Paid"
  AND generates the payment receipt.

Scenario: Partial payment
  GIVEN a pending invoice for $500,000 exists
  WHEN the cashier records a payment of $200,000
  THEN the system sets the invoice to "Partially Paid"
  AND shows an outstanding balance of $300,000.

Scenario: Payment above the balance
  GIVEN the invoice has a balance of $300,000
  WHEN the cashier tries to record a payment of $350,000
  THEN the system blocks it
  AND shows the maximum amount allowed.
```

### HU-057: Electronic Invoice Issuance
* **As a:** System
* **I want to:** Send each invoice to the electronic invoicing provider
* **So that:** The invoice is valid before the DIAN.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-27, RNF-05

```gherkin
Scenario: Invoice validated
  GIVEN the cashier issued an invoice
  WHEN the provider validates it with the DIAN
  THEN the system stores the CUFE and the "Validated" status
  AND sends the invoice PDF and XML to the customer.

Scenario: Invoice rejected
  GIVEN the provider rejects the invoice because of a data error
  WHEN the system receives the response
  THEN it marks the invoice as "Rejected by the DIAN"
  AND shows the reason to the cashier so it can be fixed.

Scenario: Provider unavailable
  GIVEN the provider does not respond
  WHEN the system tries to send the invoice
  THEN it retries automatically
  AND alerts the administrator if it cannot send it within 24 hours.
```

---

# 8. Module 8: Warranties, Microinsurance and Claims

> **Functional note:** the product must clearly define whether PitShield sells extended warranties, microinsurance or both. The stories below cover both concepts without assuming they are legally equivalent.

### HU-029: Eligibility Check
* **As a:** Service Advisor
* **I want to:** Check whether a vehicle and service meet the coverage conditions
* **So that:** I only offer products the customer is eligible for.
* **Priority:** High · **Release:** Release 2 · **Requirements:** RF-32, RN-01

```gherkin
Scenario: Eligible vehicle
  GIVEN the vehicle meets the configured conditions
  WHEN the advisor checks eligibility
  THEN the system shows the available product
  AND displays its price, coverage and term.

Scenario: Vehicle not eligible
  GIVEN the vehicle fails a condition
  WHEN the advisor checks eligibility
  THEN the system says it is not eligible
  AND shows the reason.
```

### HU-030: Warranty or Microinsurance Issuance
* **As a:** Service Advisor
* **I want to:** Issue the protection product the customer chose
* **So that:** Their coverage is activated and the certificate is generated.
* **Priority:** High · **Release:** Release 2 · **Requirements:** RF-32, RN-03, RN-04

```gherkin
Scenario: Successful issuance
  GIVEN the customer accepts the product and is eligible
  WHEN the purchase is completed
  THEN the system records the coverage
  AND generates a digital certificate or policy with its status and term.

Scenario: Failed issuance
  GIVEN the issuer does not confirm the issuance
  WHEN the system processes the request
  THEN it does not activate the coverage
  AND records the result for follow-up.
```

### HU-031: Coverage Lookup and Tracking
* **As a:** Customer / Advisor
* **I want to:** See active coverage and its term
* **So that:** I know which services or components are protected.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-33

```gherkin
Scenario: Coverage lookup
  GIVEN an active coverage exists
  WHEN the user views the vehicle
  THEN the system shows the term, coverage, status and main conditions.
```

### HU-032: Claim Filing and Tracking
* **As a:** Workshop Administrator
* **I want to:** File a claim with evidence and check its status
* **So that:** The coverage request is followed until it is resolved.
* **Priority:** High · **Release:** Release 2 · **Requirements:** RF-34, RN-14

```gherkin
Scenario: Claim filed
  GIVEN the coverage is active
  WHEN the administrator uploads the required evidence and describes the failure
  THEN the system creates the claim
  AND sets it to "Under Review".

Scenario: Information requested
  GIVEN the auditor needs additional evidence
  WHEN they request information
  THEN the claim moves to "Information Required"
  AND the workshop receives the request.

Scenario: Tracking
  GIVEN an active claim exists
  WHEN the user checks its status
  THEN the system shows the current status and the recorded actions.
```

### HU-033: Claim Audit and Decision
* **As a:** Insurer Auditor
* **I want to:** Review evidence and approve, reject or request more information
* **So that:** I decide whether the claim meets the coverage conditions.
* **Priority:** High · **Release:** Release 2 · **Requirements:** RF-34, RN-15

```gherkin
Scenario: Approval
  GIVEN the claim has enough evidence
  WHEN the auditor approves it
  THEN the system changes the status to "Approved"
  AND records the decision and the auditor.

Scenario: Rejection
  GIVEN the claim does not meet the conditions
  WHEN the auditor rejects it and gives a reason
  THEN the system changes the status to "Rejected"
  AND notifies the workshop.

Scenario: Information request
  GIVEN evidence is missing
  WHEN the auditor requests more information
  THEN the system changes the status to "Information Required"
  AND records exactly what information is missing.
```

### HU-058: Coverage Expiry and Cancellation
* **As a:** System / Workshop Administrator
* **I want to:** Expire coverage when its term ends and cancel it when appropriate
* **So that:** Only active coverage allows claims to be filed.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-33

```gherkin
Scenario: Automatic expiry
  GIVEN a coverage reached its end date
  WHEN the daily job runs
  THEN the system changes the coverage to "Expired"
  AND shows it that way in the vehicle history.

Scenario: Upcoming expiry notice
  GIVEN a coverage expires in 30 days
  WHEN the daily job runs
  THEN the system notifies the customer
  AND offers a renewal if the product allows it.

Scenario: Cancellation
  GIVEN the customer asks to cancel an active coverage
  WHEN the administrator records the cancellation and its reason
  THEN the system changes the coverage to "Cancelled"
  AND calculates the refund according to the product's conditions.
```

### HU-059: Commission Settlement
* **As a:** Platform Administrator / Workshop Administrator
* **I want to:** View and settle commissions from protection products and online payments
* **So that:** We know how much belongs to PitShield and to the workshop each period.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-35, RN-03

```gherkin
Scenario: Commission calculated
  GIVEN a coverage for $200,000 was issued with a 10 % platform commission
  WHEN the system records the issuance
  THEN it calculates $20,000 for the platform
  AND assigns the rest according to the product's conditions.

Scenario: Monthly settlement
  GIVEN the settlement period ended
  WHEN the Platform Administrator generates a workshop's settlement
  THEN the system shows the detail per coverage and transaction
  AND marks those commissions as settled so they are not included again.
```

---

# 9. Module 9: Customer Portal

### HU-034: Vehicle and History Lookup
* **As a:** Customer
* **I want to:** See my vehicles and their authorized history
* **So that:** I know the services performed and the condition of my vehicles.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-37, RN-08

```gherkin
Scenario: History lookup
  GIVEN the customer has a linked vehicle
  WHEN they open the portal
  THEN they can see the records they are allowed to view
  AND review the available evidence.
```

### HU-035: Work Order Tracking
* **As a:** Customer
* **I want to:** Check the status of my work order
* **So that:** I know how the service is progressing.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-37

```gherkin
Scenario: Status lookup
  GIVEN a work order is linked to the customer
  WHEN they open the portal
  THEN the system shows its current status
  AND the relevant information the workshop allows.
```

### HU-036: Invoice and Payment Lookup
* **As a:** Customer
* **I want to:** See my invoices and payment status
* **So that:** I keep track of what I owe and what I paid.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-37

```gherkin
Scenario: Invoice lookup
  GIVEN an invoice is linked to the customer
  WHEN they open the portal
  THEN they can view the document and its payment status.

Scenario: Pending invoice
  GIVEN the invoice is pending
  WHEN the customer views it
  THEN the system shows a payment option when available.
```

### HU-037: Warranty and Claim Lookup
* **As a:** Customer
* **I want to:** See my warranties and claims
* **So that:** I know my coverage and how my requests are going.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-37

```gherkin
Scenario: Warranty lookup
  GIVEN a coverage is linked to the vehicle
  WHEN the customer views it
  THEN the system shows its term, status and coverage.

Scenario: Claim lookup
  GIVEN a claim is linked to the customer
  WHEN they open the portal
  THEN they can see its status and the allowed updates.
```

### HU-060: Customer Portal Invitation and Activation
* **As a:** Customer
* **I want to:** Receive an invitation to activate my portal account
* **So that:** I can check my vehicles and services without calling the workshop.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-36

```gherkin
Scenario: Successful activation
  GIVEN the advisor registered the customer with a valid email
  WHEN the customer opens the invitation link and creates a password
  THEN the system activates their account
  AND shows only their vehicles.

Scenario: Expired invitation
  GIVEN the invitation link is more than 7 days old
  WHEN the customer tries to use it
  THEN the system says it expired
  AND lets them request a new one.

Scenario: Customer of several workshops
  GIVEN the customer already has an account through another workshop
  WHEN a new workshop invites them
  THEN the system links the new workshop to the same account
  AND does not create a duplicate account.
```

---

# 10. Module 10: Automated Notifications

### HU-038: Service Event Notifications
* **As a:** System
* **I want to:** Send automatic notifications about important events
* **So that:** The customer and staff stay informed.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-38, RN-16

```gherkin
Scenario: Approval notification
  GIVEN the customer approves a quote
  WHEN the system records the approval
  THEN it notifies the corresponding staff.

Scenario: Vehicle ready for pickup
  GIVEN the work order changes to "Ready for Pickup"
  WHEN the change is recorded
  THEN the system notifies the customer through the configured channel.
```

### HU-039: Automated Maintenance Reminders
* **As a:** System (Scheduled Job)
* **I want to:** Detect vehicles due for maintenance by time or mileage
* **So that:** Preventive maintenance is encouraged.
* **Priority:** Low · **Release:** Release 2 · **Requirements:** RF-39, RN-16

```gherkin
Scenario: Maintenance due soon
  GIVEN a vehicle meets the configured time or estimated mileage condition
  WHEN the scheduled job runs
  THEN the system creates a reminder
  AND offers an option to book an appointment.

Scenario: No duplicate notifications
  GIVEN a reminder was already sent for the same condition
  WHEN the job runs again
  THEN the system does not send a duplicate within the configured period.
```

### HU-061: Notification Preferences and Consent
* **As a:** Customer
* **I want to:** Choose the channels I receive messages on and stop receiving them if I want
* **So that:** I only get the information I care about.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-40, RN-16, RN-19

```gherkin
Scenario: Channel change
  GIVEN the customer has email and WhatsApp enabled
  WHEN they disable WhatsApp in the portal
  THEN the system stops sending them WhatsApp messages
  AND keeps using email.

Scenario: Consent withdrawn for reminders
  GIVEN the customer withdrew consent for marketing messages and reminders
  WHEN the reminder job runs
  THEN the system sends them no reminders
  AND only sends messages required by an ongoing service.
```

---

# 11. Module 11: Reports and Analytics

### HU-040: Financial Dashboard
* **As a:** Workshop Owner / Manager
* **I want to:** See financial indicators
* **So that:** I can evaluate revenue, collections, pending payments and profitability.
* **Priority:** Medium · **Release:** Release 3 · **Requirements:** RF-41

```gherkin
Scenario: Monthly view
  GIVEN transactions are recorded
  WHEN the manager selects a period
  THEN the system shows revenue, invoicing, pending payments, refunds and applicable commissions.
```

### HU-041: Operational Reports
* **As a:** Workshop Owner / Manager
* **I want to:** See operational indicators
* **So that:** I can evaluate the workshop's performance.
* **Priority:** Medium · **Release:** Release 3 · **Requirements:** RF-42

```gherkin
Scenario: Operational view
  GIVEN work orders and services are recorded
  WHEN the manager selects a period
  THEN the system shows open, finished and cancelled work orders, service times and services performed.
```

### HU-042: Inventory Reports
* **As a:** Inventory Manager / Manager
* **I want to:** See inventory movements and levels
* **So that:** I can make purchasing decisions.
* **Priority:** Low · **Release:** Release 3 · **Requirements:** RF-42

```gherkin
Scenario: Inventory report
  GIVEN inventory movements are recorded
  WHEN the user selects a period
  THEN the system shows receipts, consumption, returns, adjustments and parts with critical stock.
```

### HU-062: Report Export
* **As a:** Workshop Owner / Manager
* **I want to:** Export reports to CSV and PDF
* **So that:** I can share them with my accountant or analyze them in other tools.
* **Priority:** Low · **Release:** Release 3 · **Requirements:** RF-43

```gherkin
Scenario: CSV export
  GIVEN the manager is viewing a filtered report
  WHEN they click "Export CSV"
  THEN the system downloads a file with the same data and filters as the report.

Scenario: PDF export
  GIVEN the manager is viewing a report
  WHEN they click "Export PDF"
  THEN the system generates a PDF with the workshop logo, the period and the generation date.

Scenario: Report without data
  GIVEN the selected period has no records
  WHEN the manager tries to export
  THEN the system says there is no data to export.
```

---

# 12. Module 12: Artificial Intelligence Agents

> AI agents must work as **support assistants**. Technical, financial, coverage and claim decisions with real impact must stay under the control of authorized users.

### HU-043: AI-Assisted Diagnosis Agent
* **As a:** Technician
* **I want to:** Ask an AI agent using the symptoms, history and vehicle data
* **So that:** I get recommendations that support the technical diagnosis.
* **Priority:** Low · **Release:** Release 3 · **Requirements:** RF-44, RN-15

```gherkin
Scenario: Diagnosis recommendation
  GIVEN a work order has enough information
  WHEN the technician asks the AI agent for help
  THEN the agent analyzes the available information
  AND presents possible causes, suggested checks and a confidence level.

Scenario: Not enough information
  GIVEN the available information is not enough
  WHEN the technician asks the agent
  THEN the agent says which additional data it needs
  AND does not present any conclusion as a final diagnosis.
```

### HU-044: AI Preventive Maintenance Agent
* **As a:** System / Workshop Manager
* **I want to:** Analyze the vehicle's history and behavior
* **So that:** Preventive maintenance recommendations are generated.
* **Priority:** Low · **Release:** Release 3 · **Requirements:** RF-44, RN-15

```gherkin
Scenario: Preventive recommendation
  GIVEN the vehicle has enough history
  WHEN the agent analyzes its data
  THEN it generates maintenance recommendations
  AND relates them to the mileage, time or available history.
```

### HU-045: AI Customer Service Agent
* **As a:** Customer
* **I want to:** Ask an AI assistant about my service
* **So that:** I get quick answers about my vehicles, work orders, appointments and warranties.
* **Priority:** Low · **Release:** Release 3 · **Requirements:** RF-44, RN-15

```gherkin
Scenario: Authorized question
  GIVEN the customer is logged in
  WHEN they ask the agent about their vehicle or service
  THEN the agent answers only with information the customer can access.

Scenario: Information not available
  GIVEN the question needs information the agent cannot verify
  WHEN the customer asks it
  THEN the agent says it cannot confirm it
  AND does not make up information.
```

### HU-046: AI Inventory Agent
* **As a:** Inventory Manager
* **I want to:** Get recommendations based on consumption and stock
* **So that:** I can anticipate purchasing needs.
* **Priority:** Low · **Release:** Release 3 · **Requirements:** RF-44, RN-15

```gherkin
Scenario: Restocking recommendation
  GIVEN historical inventory movements exist
  WHEN the manager requests an analysis
  THEN the agent identifies parts at risk of running out
  AND presents an explainable recommendation based on the available data.
```

### HU-047: AI Claim Pre-Analysis Agent
* **As a:** Insurer Auditor
* **I want to:** Receive an automatic pre-analysis of a claim's evidence
* **So that:** Human review is prioritized and faster.
* **Priority:** Low · **Release:** Release 3 · **Requirements:** RF-44, RN-15

```gherkin
Scenario: Successful pre-analysis
  GIVEN a claim has enough information and evidence
  WHEN the agent processes the case
  THEN it generates a summary of the evidence, possible inconsistencies and relevant criteria
  AND presents the result as a recommendation for human review.

Scenario: Human decision required
  GIVEN the agent generates a recommendation
  WHEN the auditor views the result
  THEN the system does not change the claim's final status automatically
  AND requires the auditor to make the decision.
```

### HU-048: AI Interaction Traceability
* **As a:** Administrator
* **I want to:** Log the relevant interactions and recommendations of the AI agents
* **So that:** Their use is traceable and supervised.
* **Priority:** Medium · **Release:** Release 3 · **Requirements:** RF-45, RN-15

```gherkin
Scenario: Interaction logged
  GIVEN a user uses an AI agent in a critical process
  WHEN the agent generates a recommendation
  THEN the system records the user, date, agent, allowed context and result of the interaction
  AND shows whether the recommendation was accepted or dismissed.
```

---

# 13. Module 13: Platform Administration

### HU-063: Workshop Onboarding and Management
* **As a:** Platform Administrator
* **I want to:** Register, activate and suspend workshops, and create their first administrator
* **So that:** New workshops can join PitShield and their access is controlled.
* **Priority:** High · **Release:** MVP · **Requirements:** RF-46, RN-06

```gherkin
Scenario: Workshop onboarding
  GIVEN the workshop is not registered
  WHEN the Platform Administrator registers its tax ID, legal name and the administrator's email
  THEN the system creates the workshop with its data isolated from other workshops
  AND sends an invitation to the Workshop Administrator.

Scenario: Duplicate tax ID
  GIVEN a workshop with the same tax ID already exists
  WHEN the Platform Administrator tries to register it again
  THEN the system blocks the registration
  AND shows the existing workshop.

Scenario: Workshop suspension
  GIVEN a workshop is active
  WHEN the Platform Administrator suspends it with a reason
  THEN the workshop's users cannot operate
  AND the system keeps all its data.
```

### HU-064: Insurer and Auditor Management
* **As a:** Platform Administrator
* **I want to:** Register partner insurers and their auditor users
* **So that:** Each claim reaches the insurer that backs the coverage.
* **Priority:** Medium · **Release:** Release 2 · **Requirements:** RF-47

```gherkin
Scenario: Insurer registered
  GIVEN the insurer is not registered
  WHEN the Platform Administrator registers its data and contact
  THEN the system creates the insurer
  AND allows linking protection products to it.

Scenario: Auditor scope
  GIVEN an auditor belongs to Insurer A
  WHEN they view the claims
  THEN the system shows only claims for coverage backed by Insurer A.
```

### HU-065: Protection Product Configuration
* **As a:** Platform Administrator
* **I want to:** Create and configure extended warranties and microinsurance
* **So that:** Each product defines what it covers, what it costs and who can buy it.
* **Priority:** High · **Release:** Release 2 · **Requirements:** RF-31, RN-01, RN-03

```gherkin
Scenario: Product created
  GIVEN a registered insurer exists
  WHEN the Platform Administrator enters the type, coverage, term, price, commission and eligibility conditions
  THEN the system creates the product in "Draft" status
  AND only offers it to workshops once it is published.

Scenario: Conditions changed
  GIVEN a published product has issued coverage
  WHEN the Platform Administrator changes its price or conditions
  THEN the system creates a new version of the product
  AND coverage already issued keeps the conditions it was sold with.
```

---

## Cross-cutting acceptance rules

These rules apply to every story when relevant:

- The system must check permissions before running any operation.
- Critical records must never be physically deleted; their traceability must be kept.
- Financial operations must be idempotent to prevent duplicate payments or transactions.
- Status changes must follow the defined flow.
- Relevant operations must create audit records.
- Customer and vehicle information must only be visible to authorized users.
- Media evidence must stay linked to its vehicle, work order or claim.
- AI agents must present their results as assistance, not as a replacement for human decisions with technical, financial, contractual or coverage impact.
- Errors from external integrations must be logged and traceable.
- Notifications must avoid duplicate sends.
- Invoicing, payments, insurance and messaging features must follow the regulations and providers defined for the target market.
- Every operation must respect workshop isolation (RN-06): no user can see or change another workshop's data.

---

## Definition of done

A user story is done when:

1. It meets all its acceptance scenarios.
2. It has unit and integration tests, with at least 80 % coverage in services and domain (RNF-10).
3. Its main scenarios are automated (API or end-to-end) and the rest were tested manually with evidence.
4. It passed code review by at least one other team member.
5. Continuous integration is green.
6. The API documentation (OpenAPI) is up to date.
7. It was demonstrated and accepted in the sprint review.
