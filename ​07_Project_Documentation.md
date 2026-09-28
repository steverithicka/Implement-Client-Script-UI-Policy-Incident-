# Phase 7 – Project Documentation

## 7.1 Project Overview

The project **“Implement Client Script & UI Policy (Incident)”** demonstrates the use of ServiceNow UI Policies, UI Policy Actions, and Client Scripts to control and automate Incident form behavior.

The implementation focuses on improving data consistency and providing dynamic validation during Incident creation and modification. The configured controls respond to specific Incident field conditions and user actions.

The project demonstrates how client-side configurations can be used to:

* Apply conditional field behavior.
* Make required fields mandatory under specific conditions.
* Automatically update field values.
* Validate information before Incident submission.
* Restrict direct field changes through list editing.
* Allow normal updates through the Incident form.

The implementation is focused on the **Incident table** and the specific requirements defined for the project.

---

## 7.2 Problem Statement

Incident records contain important information that must be entered consistently and accurately.

When Incident information is entered manually without appropriate validation or field controls, incomplete or inconsistent records may be created. Such records can affect reporting, SLA compliance, and the overall quality of Incident management.

The project addresses this problem by introducing client-side controls that respond dynamically to Incident field values.

For example, when an Incident has **Impact = High**, specific field behaviors are applied. Similarly, when users attempt to submit an Incident without the required information, the configured Client Script validates the form before allowing submission.

The project therefore provides a controlled approach to Incident data entry within the defined requirements.

---

## 7.3 Project Objectives

The main objectives of the project are:

1. To implement a UI Policy for High Impact Incidents.
2. To make Assignment Group mandatory when Impact is High.
3. To make Urgency read-only under the defined High Impact condition.
4. To automatically set Urgency to High when Impact changes to High.
5. To validate Assigned To before submitting a High Impact Incident.
6. To prevent State changes through direct list editing.
7. To allow State updates through the normal Incident form.
8. To verify the implemented functionality through functional testing.

These objectives are implemented using ServiceNow configuration and client-side scripting.

---

## 7.4 Implemented Solution

The project combines UI Policies, UI Policy Actions, and three types of Client Scripts.

### 7.4.1 UI Policy – High Impact Control

A UI Policy named **High Impact Control** is configured on the Incident table.

The policy is triggered when:

**Impact = 1 – High**

When this condition is true, the associated UI Policy Actions are applied.

The policy includes reverse behavior so that the conditional field settings can be restored when the Impact condition is no longer true.


---

### 7.4.2 UI Policy Action – Assignment Group

An associated UI Policy Action is configured for the **Assignment Group** field.

When Impact is High:

**Assignment Group becomes mandatory.**

This ensures that the required assignment information is provided for the defined High Impact condition.

---

### 7.4.3 UI Policy Action – Urgency

Another UI Policy Action is configured for the **Urgency** field.

When Impact is High:

**Urgency becomes read-only.**

This prevents direct modification of the Urgency field while the specified UI Policy condition is active.

---

### 7.4.4 OnChange Client Script

The project includes an onChange Client Script named:

**Auto set urgency for high impact**

The script is associated with the **Impact** field.

When the user changes Impact to High, the script automatically sets:

**Urgency = High**

An informational message is also displayed to inform the user that the Urgency value has been updated.

This reduces manual data entry and provides immediate feedback on the Incident form.

---

### 7.4.5 OnSubmit Client Script

The project includes an onSubmit Client Script named:

**Prevent save if Assigned To missing**

The script executes when the user attempts to submit an Incident.

It checks whether:

* Impact is High, and
* Assigned To is empty.

If both conditions are true, the Incident submission is prevented and an error message is displayed.

This provides an additional validation layer before the Incident is saved.

---

### 7.4.6 OnCellEdit Client Script

The project includes an onCellEdit Client Script named:

**Prevent state change via list edit**

The script is associated with the **State** field.

When a user attempts to change State directly from the Incident list, an alert message is displayed and the list-edit operation is rejected.

The user is instructed to open the Incident instead.

This restriction applies specifically to list editing and does not prevent normal State updates through the Incident form.

---

## 7.5 Implementation Summary

| Component                | Configuration                       | Purpose                                            |
| ------------------------ | ----------------------------------- | -------------------------------------------------- |
| UI Policy                | High Impact Control                 | Applies conditional behavior when Impact is High   |
| UI Policy Action         | Assignment Group                    | Makes Assignment Group mandatory                   |
| UI Policy Action         | Urgency                             | Makes Urgency read-only                            |
| OnChange Client Script   | Auto set urgency for high impact    | Automatically sets Urgency to High                 |
| OnSubmit Client Script   | Prevent save if Assigned To missing | Validates Assigned To before submission            |
| OnCellEdit Client Script | Prevent state change via list edit  | Prevents direct State changes through list editing |

The components work together to provide conditional behavior, automatic field updates, form validation, and controlled list editing.

---

## 7.6 Project Workflow

The implemented functionality can be summarized through the following workflow:

**Create/Open Incident**

↓

**Set Impact**

↓

**If Impact = High**

↓

**Assignment Group becomes mandatory**

↓

**Urgency is automatically set to High**

↓

**Urgency becomes read-only**

↓

**OnSubmit validation checks Assigned To**

↓

**If validation succeeds → Incident is saved**

**If validation fails → Error message is displayed**

For State management:

**Incident List**

→ Direct State editing is blocked.

**Incident Form**

→ State can be changed and saved normally.

This workflow demonstrates how the different ServiceNow configurations interact during Incident management.

---

## 7.7 Project Outcome

The completed implementation demonstrates the practical use of ServiceNow client-side controls for Incident management.

The project successfully demonstrates:

### Conditional Field Behavior

The UI Policy applies specific behavior when Impact is High.

### Mandatory Field Control

Assignment Group becomes mandatory when the High Impact condition is active.

### Automatic Field Update

Urgency is automatically set to High when Impact changes to High.

### Read-Only Behavior

Urgency is made read-only while the defined High Impact condition is active.

### Form Validation

The OnSubmit Client Script prevents submission when Impact is High and Assigned To is empty.

### List-Edit Restriction

The OnCellEdit Client Script prevents direct State changes from the Incident list.

### Form-Based Update

State can still be changed through the normal Incident form.

Together, these functions demonstrate a controlled approach to Incident data entry and user interaction.

---

## 7.8 Client Script Types Demonstrated

The project demonstrates three Client Script execution types.

| Script Type    | Field/Operation     | Function                      |
| -------------- | ------------------- | ----------------------------- |
| **onChange**   | Impact              | Automatically updates Urgency |
| **onSubmit**   | Incident submission | Validates Assigned To         |
| **onCellEdit** | State               | Restricts direct list editing |

### onChange

The onChange Client Script runs when the value of the Impact field changes.

When Impact becomes High, Urgency is automatically set to High.

### onSubmit

The onSubmit Client Script runs when the user attempts to submit the Incident.

It checks the defined condition and prevents submission when Assigned To is empty for a High Impact Incident.

### onCellEdit

The onCellEdit Client Script controls direct editing from the Incident list.

It prevents State from being changed through list editing and directs the user to the Incident form instead.

---

## 7.9 Testing and Validation

The implemented configurations are validated through scenario-based functional testing.

The testing covers:

* High Impact Incident with Assigned To empty.
* High Impact Incident with Assigned To populated.
* Automatic Urgency update.
* Reversal of conditional behavior.
* State list-edit restriction.
* Form-based State update.

For each scenario, the expected behavior is compared with the actual behavior observed in ServiceNow.

Testing screenshots are maintained separately as part of **Phase 6 – Project Testing**.

The testing evidence provides support for confirming that the configured UI Policies and Client Scripts behave according to the defined requirements.

---

## 7.10 Project Benefits

The implementation provides the following benefits within the defined project scope:

### Improved Data Consistency

Conditional field behavior helps ensure that related Incident information follows the defined requirements.

### Reduced Manual Data Entry

The automatic Urgency update reduces the need for users to manually enter the related value.

### Immediate User Feedback

Validation and informational messages provide immediate feedback when user action is required.

### Controlled State Updates

The project prevents direct State changes through list editing while allowing normal updates through the Incident form.

### Dynamic Form Behavior

The Incident form responds to changes in Impact and applies the configured behavior dynamically.

### Simple and Focused Implementation

The project demonstrates important ServiceNow concepts within a limited and clearly defined Incident Management scope.

---

## 7.11 Project Limitations

The implementation is limited to the requirements defined for this project.

### Incident Table Scope

The configurations are implemented specifically for the Incident table and the selected fields.

### Client-Side Focus

The project primarily demonstrates UI Policies and Client Scripts. It does not implement a complete server-side validation framework.

### Defined Conditions

The configured behavior applies only to the conditions specified in the project, particularly the High Impact condition.

### Limited Workflow Coverage

The project does not attempt to implement a complete Incident Management workflow. It focuses on field behavior, validation, automation, and list-edit control.

These limitations define the scope of the current implementation.

---

## 7.12 Documentation and Evidence

The project documentation provides a record of the configuration, implementation, and testing activities.

The GitHub repository should contain the relevant project materials, including:

* Project documentation.
* UI Policy configuration details.
* UI Policy Action details.
* Client Script configuration details.
* Test cases.
* Testing screenshots.
* Implementation screenshots where applicable.
* Demonstration video information.

Screenshots should clearly show the relevant ServiceNow configuration or result being documented.

The testing screenshots are maintained under the testing phase, while selected implementation screenshots may be included in this documentation phase to explain the configured solution.

---

## 7.13 Final Project Review

Before completing the documentation phase, the following points should be verified:

* High Impact UI Policy is configured.
* Assignment Group mandatory behavior is configured.
* Urgency read-only behavior is configured.
* OnChange Client Script is active.
* OnSubmit Client Script is active.
* OnCellEdit Client Script is active.
* Automatic Urgency update has been tested.
* Submission validation has been tested.
* State list-edit restriction has been tested.
* Form-based State update has been tested.
* Testing screenshots have been captured.
* Actual test results have been documented.
* Relevant project documentation has been added to the GitHub repository.

---

## 7.14 Conclusion

The project demonstrates the practical application of **ServiceNow UI Policies, UI Policy Actions, and Client Scripts** to control Incident form behavior.

The implemented solution uses conditional field behavior, automatic value updates, form submission validation, and list-edit restrictions to provide controlled Incident data entry.

The project also demonstrates three Client Script execution types:

* **onChange** for automatic field updates.
* **onSubmit** for submission validation.
* **onCellEdit** for controlling list-based changes.

The implementation remains focused on the defined Incident requirements and demonstrates how ServiceNow client-side configuration can be used to improve data consistency and user interaction.

The completed documentation, testing evidence, and implementation details provide a structured record of the project from configuration through validation and final review.
