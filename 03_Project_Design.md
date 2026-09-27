# Phase 3 – Project Design

## 3.1 System Design Overview

The project uses a combination of **UI Policies** and **Client Scripts** to control the behavior of the ServiceNow Incident form.

The Impact field acts as a key condition. When its value is High, specific field-level controls and validation rules are applied.

## 3.2 UI Policy Design

### UI Policy: High Impact Control

| Property  | Configuration       |
| --------- | ------------------- |
| Name      | High Impact Control |
| Table     | Incident            |
| Active    | Yes                 |
| Condition | Impact is 1 – High  |

The UI Policy is designed to make the **Assignment Group** field mandatory when the Impact value is High.

The policy also supports reversing the mandatory behavior when the condition is no longer true.

### UI Policy Action: Urgency

The UI Policy Action is associated with the High Impact Control policy.

| Property  | Configuration       |
| --------- | ------------------- |
| UI Policy | High Impact Control |
| Field     | Urgency             |
| Read-only | Yes                 |
| Visible   | No change           |

When the High Impact condition is satisfied, the Urgency field becomes read-only. The behavior is reversed when the condition is no longer satisfied.

## 3.3 Client Script Design

The project contains three different types of Client Scripts.

### OnChange Client Script

**Purpose:** Automatically set Urgency to High when Impact changes to High.

**Trigger:** Impact field change.

### OnSubmit Client Script

**Purpose:** Prevent submission when the Incident has High Impact and Assigned To is empty.

**Trigger:** Incident form submission.

### OnCellEdit Client Script

**Purpose:** Prevent State from being changed through list editing.

**Trigger:** State field modification through list editing.

## 3.4 Functional Flow

```text
User opens Incident form
          |
          v
      Select Impact
          |
          v
   Is Impact = High?
       /       \
     Yes        No
      |          |
      v          v
Assignment     Normal
Group becomes  field behavior
mandatory
      |
      v
Urgency becomes read-only
      |
      v
Urgency automatically set to High
      |
      v
User submits Incident
      |
      v
Is Assigned To populated?
       /       \
     No         Yes
      |          |
      v          v
Display error   Allow submission
```

## 3.5 Design Principle

The design separates field behavior from submission validation:

* **UI Policies** manage dynamic form behavior.
* **Client Scripts** handle automation and validation.
* **OnCellEdit** controls a specific list-edit scenario.

This separation makes each configuration easier to understand and maintain.
