# Phase 4 – Project Planning

## 4.1 Development Plan

The project will be implemented in the following sequence.

| Phase | Activity                        | Expected Output                    |
| ----- | ------------------------------- | ---------------------------------- |
| 1     | Understand the problem          | Defined project objective          |
| 2     | Analyze requirements            | Functional requirements            |
| 3     | Design solution                 | UI Policy and Client Script design |
| 4     | Configure UI Policy             | High Impact Control                |
| 5     | Configure UI Policy Action      | Urgency field restriction          |
| 6     | Create OnChange Client Script   | Automatic Urgency update           |
| 7     | Create OnSubmit Client Script   | Submission validation              |
| 8     | Create OnCellEdit Client Script | State list-edit restriction        |
| 9     | Execute test cases              | Test evidence                      |
| 10    | Prepare documentation           | GitHub project documentation       |
| 11    | Prepare demonstration           | Demo video                         |

## 4.2 Implementation Sequence

### Step 1 – Configure UI Policy

Create the **High Impact Control** UI Policy on the Incident table with the condition:

**Impact is 1 – High**

### Step 2 – Configure UI Policy Action

Configure Assignment Group as mandatory and configure Urgency as read-only under the appropriate policy behavior.

### Step 3 – Create OnChange Client Script

Create a Client Script that responds to changes in the Impact field and sets Urgency to High when required.

### Step 4 – Create OnSubmit Client Script

Implement validation that checks whether Assigned To is populated before allowing a High Impact Incident to be submitted.

### Step 5 – Create OnCellEdit Client Script

Prevent direct State changes through list editing and instruct the user to open the Incident form.

### Step 6 – Test the Configuration

Execute the defined test cases and record the actual results with screenshots.

## 4.3 Documentation Plan

The GitHub repository will contain:

* Project overview.
* Phase-wise documentation.
* Configuration details.
* Client Script details.
* Test cases.
* Screenshots.
* Final project report.
* Demonstration information.

The repository should be maintained throughout the project rather than being populated only at the end.
