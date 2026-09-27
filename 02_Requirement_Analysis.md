# Phase 2 – Requirement Analysis

## 2.1 Functional Requirements

The system should provide the following functionality within the ServiceNow Incident form.

### FR-01: High Impact Control

When the Incident **Impact** is set to **1 – High**, the **Assignment Group** field should become mandatory.

### FR-02: Urgency Field Control

When the Incident Impact is High, the **Urgency** field should become read-only.

### FR-03: Automatic Urgency Update

When the Impact field is changed to High, the system should automatically set the Urgency field to High.

### FR-04: Assigned To Validation

When an Incident has High Impact and the **Assigned To** field is empty, the system should prevent the record from being submitted.

### FR-05: List Edit Restriction

The system should prevent users from changing the Incident **State** directly through list editing.

### FR-06: Form-Based State Update

Users should still be able to change the Incident State through the Incident form.

### FR-07: Reverse Conditional Behavior

When the Impact condition changes from High to another value, the applicable UI Policy behavior should be reversed so that the affected fields return to their normal state.

These requirements are derived from the five implementation tasks and testing scenarios defined in the project document.

## 2.2 Non-Functional Requirements

The implementation should:

* Be simple to configure and maintain.
* Provide clear validation messages.
* Respond dynamically to user actions.
* Minimize unnecessary manual data entry.
* Maintain consistent Incident information.
* Be suitable for demonstration within a ServiceNow development environment.

## 2.3 Input and Output

### Inputs

The primary input is the Incident form data, particularly:

* Impact
* Assignment Group
* Assigned To
* Urgency
* State

### Outputs

Depending on the user's actions and the selected Impact value, the system should:

* Change field mandatory status.
* Change field read-only status.
* Automatically update Urgency.
* Display validation messages.
* Prevent unauthorized list editing.
* Allow valid Incident submissions.

## 2.4 Scope

The project is limited to client-side behavior and validation associated with the ServiceNow Incident table. It demonstrates UI Policies, UI Policy Actions, and Client Scripts rather than implementing a complete Incident Management application.
