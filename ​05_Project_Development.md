# Phase 5 – Project Development

## 5.1 Development Environment

The project is implemented using the **ServiceNow Incident** table and focuses on client-side configuration.

The development consists of one UI Policy, a UI Policy Action for Urgency, and three Client Scripts.

## 5.2 UI Policy Configuration

### High Impact Control

**Configuration:**

* Name: High Impact Control
* Table: Incident
* Active: True
* Condition: Impact is 1 – High

### UI Policy Action

The Assignment Group field is configured as mandatory when the High Impact condition is satisfied.

The reverse behavior is enabled so that the mandatory setting can be removed when the condition becomes false.

## 5.3 Urgency UI Policy Action

The Urgency field is configured as read-only under the High Impact condition.

This ensures that the field cannot be manually modified while the specified condition is active.

## 5.4 OnChange Client Script

**Name:** Auto set urgency for high impact
**Table:** Incident
**Type:** onChange
**Field:** Impact
**Active:** True

```javascript
function onChange(control, oldValue, newValue, isLoading) {
    if (isLoading || newValue == '') {
        return;
    }

    if (newValue == '1') {
        g_form.setValue('urgency', '1');
        g_form.addInfoMessage('Urgency set to High for High impact incident.');
    }
}
```

This script monitors changes to Impact. When the new value represents High Impact, Urgency is automatically set to High and an informational message is displayed.

## 5.5 OnSubmit Client Script

**Name:** Prevent save if Assigned To missing
**Table:** Incident
**Type:** onSubmit
**Active:** True

```javascript
function onSubmit() {
    if (g_form.getValue('impact') == '1' &&
        g_form.getValue('assigned_to') == '') {
        g_form.showErrorBox(
            'assigned_to',
            'Assigned To is mandatory for High impact incidents.'
        );
        return false;
    }
    return true;
}
```

The script checks the Impact and Assigned To values during submission. If Impact is High and Assigned To is empty, submission is stopped and an error is displayed. Otherwise, the form is allowed to proceed.

## 5.6 OnCellEdit Client Script

**Name:** Prevent state change via list edit
**Table:** Incident
**Type:** onCellEdit
**Field:** State
**Active:** True

```javascript
function onCellEdit(sysIDs, table, oldValues, newValue, callback) {
    alert('State cannot be updated using list editing. Please open the Incident.');
    callback(false);
}
```

This script prevents users from changing the Incident State directly through list editing. The user is instructed to open the Incident and make the change through the form.

## 5.7 Development Evidence

The following screenshots should be added to the GitHub repository after implementation:

1. High Impact Control UI Policy.
2. Assignment Group UI Policy Action.
3. Urgency UI Policy Action.
4. OnChange Client Script.
5. OnSubmit Client Script.
6. OnCellEdit Client Script.
7. Incident form showing High Impact behavior.
8. Automatic Urgency update.
9. Submission validation.
10. List-edit restriction.
