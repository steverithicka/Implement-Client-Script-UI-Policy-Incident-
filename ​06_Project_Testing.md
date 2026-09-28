# Phase 6 – Project Testing

## 6.1 Testing Objective

Testing is performed to verify that the configured **UI Policies, UI Policy Actions, and Client Scripts** behave according to the defined project requirements.

The testing focuses on validating:

* Mandatory field enforcement.
* Automatic field updates.
* Conditional field behavior.
* Reversal of conditional behavior.
* Form submission validation.
* List-edit restrictions.
* Normal form-based Incident updates.

The objective is to ensure that the configured client-side controls provide the expected behavior during different Incident management scenarios.

---

## 6.2 Testing Environment

The testing is performed within the **ServiceNow Incident Management** environment.

The following configurations are included in the testing:

| Component                | Configuration Being Tested          |
| ------------------------ | ----------------------------------- |
| UI Policy                | High Impact Control                 |
| UI Policy Action         | Assignment Group mandatory behavior |
| UI Policy Action         | Urgency read-only behavior          |
| OnChange Client Script   | Automatic Urgency update            |
| OnSubmit Client Script   | Assigned To validation              |
| OnCellEdit Client Script | State list-edit restriction         |

The testing is performed using Incident records and different values of the **Impact, Assignment Group, Assigned To, Urgency, and State** fields.

---

## 6.3 Testing Approach

The project uses **scenario-based functional testing**.

Each test case follows the following structure:

1. Identify the required Incident condition.
2. Perform the specified action.
3. Observe the behavior of the Incident form.
4. Compare the observed behavior with the expected result.
5. Record the actual result.
6. Capture a screenshot as evidence where applicable.

The test cases are designed to cover both valid and invalid user actions.

---

# 6.4 Test Case 1 – Mandatory Validation for High Impact Incident

## Test ID

**TC-01**

## Test Scenario

Verify that the Incident cannot be submitted when **Impact is High** and **Assigned To is empty**.

## Objective

To verify that the OnSubmit Client Script correctly validates the Assigned To field before allowing the Incident to be submitted.

## Preconditions

* ServiceNow Incident form is accessible.
* The OnSubmit Client Script is active.
* A new Incident record can be created.

## Test Steps

1. Navigate to the **Incident** module.
2. Open the Incident creation form.
3. Select or create a new Incident.
4. Set the **Impact** field to **1 – High**.
5. Leave the **Assigned To** field empty.
6. Attempt to submit/save the Incident.
7. Observe the response displayed by the system.

## Expected Result

The Incident should **not be submitted**.

An error message should be displayed indicating that **Assigned To is mandatory for High Impact incidents**.

The validation is implemented using the OnSubmit Client Script, which checks whether:

```javascript
g_form.getValue('impact') == '1'
```

and:

```javascript
g_form.getValue('assigned_to') == ''
```

When both conditions are true, the script displays an error and returns `false`, preventing submission.

<img width="1365" height="561" alt="tc1 mandatory" src="https://github.com/user-attachments/assets/45f27722-47a1-41fa-8d46-ba388f0614f6" />


# 6.5 Test Case 2 – Successful Submission with Assigned To

## Test ID

**TC-02**

## Test Scenario

Verify that a High Impact Incident can be submitted successfully when the required Assigned To value is provided.

## Objective

To verify that the submission validation allows a valid Incident to be saved.

## Preconditions

* Incident form is available.
* Impact can be set to High.
* Assigned To contains a valid user.

## Test Steps

1. Open the Incident form.
2. Set **Impact** to **1 – High**.
3. Provide a valid value in **Assigned To**.
4. Verify the Incident form.
5. Submit the Incident.
6. Observe whether the record is successfully saved.

## Expected Result

The Incident should be successfully submitted because the Assigned To field contains a value.

The test should also verify the other High Impact behaviors:

* Urgency should be automatically set to High.
* Urgency should follow the configured read-only behavior.
* The Incident should be saved successfully.

The project document specifically identifies successful saving after providing Assigned To as one of the testing scenarios.
<img width="1365" height="606" alt="tc2" src="https://github.com/user-attachments/assets/38a7720b-6df5-48cf-a754-d573be21a2d1" />


# 6.6 Test Case 3 – Automatic Urgency Update

## Test ID

**TC-03A**

## Test Scenario

Verify that Urgency is automatically updated when Impact is changed to High.

## Objective

To verify the functionality of the **onChange Client Script**.

## Preconditions

* OnChange Client Script is active.
* Incident form is open.

## Test Steps

1. Open an Incident record.
2. Locate the **Impact** field.
3. Change Impact to **1 – High**.
4. Observe the **Urgency** field.
5. Observe any informational message displayed on the form.

## Expected Result

When Impact is changed to High:

* Urgency should automatically be set to **1 – High**.
* An informational message should be displayed.

The configured Client Script uses:

```javascript
g_form.setValue('urgency', '1');
```

and displays:

```text
Urgency set to High for High impact incident.
```

The source document specifies this behavior for the OnChange Client Script.

<img width="1365" height="611" alt="tc3" src="https://github.com/user-attachments/assets/8ae011db-a6c3-4c7d-b3f6-5f30cb86fd9e" />

---

# 6.7 Test Case 4 – Reverse Conditional Behavior

## Test ID

**TC-04**

## Test Scenario

Verify that the conditional field behavior is reversed when Impact changes from High to Medium.

## Objective

To verify the **Reverse if false** behavior configured in the UI Policy.

## Preconditions

* An Incident is available.
* Impact is currently High.
* High Impact UI Policy is active.

## Test Steps

1. Open a High Impact Incident.
2. Verify the current field behavior.
3. Change **Impact** from **High** to **Medium**.
4. Observe Assignment Group.
5. Observe Urgency.
6. Attempt to interact with the affected fields.
7. Save the Incident.

## Expected Result

When Impact is changed from High to Medium:

* The High Impact condition should no longer apply.
* The mandatory behavior should be reversed where configured.
* Urgency should return to its normal editable behavior where applicable.
* The Incident should be allowed to save if other requirements are satisfied.

The source document specifically defines this reverse-condition scenario.

23
<img width="1365" height="603" alt="tc4" src="https://github.com/user-attachments/assets/c2e7b320-1a9d-4f59-8cc1-25952067e19b" />

---

# 6.8 Test Case 5 – State List-Edit Restriction

## Test ID

**TC-05**

## Test Scenario

Verify that the Incident State cannot be changed directly using list editing.

## Objective

To verify the functionality of the **onCellEdit Client Script**.

## Preconditions

* Incident records are available.
* The OnCellEdit Client Script is active.
* State is displayed in the Incident list.

## Test Steps

1. Navigate to the Incident list.
2. Locate an Incident.
3. Double-click the **State** field or use the available list-edit functionality.
4. Attempt to change the State value.
5. Observe the system response.

## Expected Result

An alert should be displayed:

```text
State cannot be updated using list editing. Please open the Incident.
```

The State change should be rejected.

The Client Script uses:

```javascript
callback(false);
```

to prevent the list-edit operation.

<img width="1365" height="675" alt="tc5" src="https://github.com/user-attachments/assets/2472fa25-0b19-42d4-9b60-14f5a26e167c" />


# 6.9 Test Case 6 – Form-Based State Update

## Test ID

**TC-06**

## Test Scenario

Verify that the Incident State can still be changed through the normal Incident form.

## Objective

To ensure that the list-edit restriction does not prevent legitimate State updates performed through the Incident form.

## Preconditions

* Incident record exists.
* Incident form can be opened.

## Test Steps

1. Open an existing Incident.
2. Locate the **State** field.
3. Change State to another valid value.
4. Select **Update**.
5. Reopen or refresh the Incident if required.
6. Verify the State value.

## Expected Result

The State should be successfully updated through the Incident form.

The list-edit restriction should apply specifically to direct list editing and should not prevent a normal form-based update.

Incident form before the State change
<img width="1365" height="623" alt="tc6 1" src="https://github.com/user-attachments/assets/7a420bbd-8b85-43fd-b2cd-bcd4830774dc" />


State changed on the form
<img width="1365" height="606" alt="tc2" src="https://github.com/user-attachments/assets/b06ddc74-46b3-4940-8577-a2257270d7a9" />

<img width="1365" height="601" alt="tc6 3" src="https://github.com/user-attachments/assets/b6a0f79f-9df5-49f3-9892-14e0e714a279" />

---



# 6.10 Testing Conclusion

The testing phase is intended to confirm that the ServiceNow UI Policies and Client Scripts operate according to the defined project requirements.

The test scenarios cover both valid and invalid user actions, including mandatory field validation, automatic field updates, conditional reversal, list-edit restrictions, and normal form-based updates.

After executing the test cases, the **Actual Result** and **Status** columns should be updated based on the observed ServiceNow behavior. The corresponding screenshots should be added as supporting evidence in the GitHub repository.

This testing process provides documented evidence that the implemented Incident form controls have been evaluated against their intended requirements.
