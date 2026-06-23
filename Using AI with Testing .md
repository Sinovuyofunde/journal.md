Exercise: Using AI to Help with Testing

Part 1: Understanding What to Test
Exercise 1.1: Behavior Analysis

Test cases:calculateTaskScore:

High priority task will get a higher score than low priority task
Completed task has reduced or zero priority score
Overdue task increases score compared to non-overdue task
Tasks that are assigned to the current user get a score boost (+12)
The score for the task will be higher if it is updated recently than if it is outdated.
Note that task without due date does not crash the function (an edge case)

Exercise 1.2: Test Planning

Testing Plan

Unit Tests:

Calculate Task Score individual scoring rules
sortTasksByImportance – sorting by importance
If the number of tasks in the task list is correct, getTopPriorityTasks returns the correct number of tasks.

Integration Tests:

Complete workflow, from scoring, sorting to filtering.

Test Priority:

calculateTaskScore (core logic)
Sorts the tasks by their importance (based on the score).
The getTopPriorityTasks function is used to get the top priority tasks and requires both.

Test Dependencies:

Correct scoring is key to sorting
Sorting output is fundamental to top tasks.

Expected Outcomes:

There must be a perfect match between scores and rules.
The sorting should be done by score and should be in descending order.
only return correct highest scores for top tasks

Part 2: Improving a Single Test

This is an improved version of Basic Test (Exercise 2.1).

Improved Test Focus:

Takes a look at what happens at the output rather than at the internal logic.
Clearly validates score difference

Example improvement:

Make sure that two tasks that have different priority values return different scores
Make sure function returns the number.Make sure that function returns number.
Assign higher priority to get higher score.
The results of this exercise are due on the date of the exercise.

Good Test Principles:

Evaluate a logic based on fixed dates.Evaluate a logic that is based on a fixed date.
Avoid real-time dependency
Cover overdue cases vs not overdue cases

Better Test Example:

Task due date in past: Higher Score
Task due date in future → normal score

Edge Cases:

Due date = today
Missing due date
Very old task dates

Part 3: Test Driven Development (TDD)

This is a new feature exercise (+12 User Boost):This is a NEW FEATURE Exercise (+12 User Boost):

TDD Steps:

Write failing test:
Task assigned to current user should have score +12 higher

Minimal implementation:
This covers adding a condition check for an assigned user.

Refactor:
Reorganize the scoring rules.Organize the scoring rules.

Next test:
Prevent the other tasks from being affected by boost.

Bug Fix – Days Calculation – Exercise 3.2

Bug Test:

Create a task that has a known update date
Avoid being surprised by different number of days if any.

Fix Approach:

Correct use of .days or proper date difference function

Regression Tests:

Same-day update → 0 days
Correct positive value → past update

Part 4: Integration Testing

Conduct the Full Workflow Test.Run the Full Workflow Test (Exercise 4.1).

Scenario:

Numerous tasks that have varying priorities, dates and users

Test Data:

Task C: very high priority, assigned to user.
Task B: low priority, not assigned
Task C: task that is overdue.

Assertions:

Scores calculated correctly
Correct order on sorting.
Top tasks is not a function.Top tasks is no function.

Structure:

Arrange test data
Perform Action (Run Full Workflow)
Make a final ordered output:

Reflection
What I learned:
The focus for testing is on behaviour, not structure of code.
Edge cases are the same type of cases as normal cases.
The key to preventing bugs is through TDD.
Integration testing checks that all functions are integrated and functioning properly.
AI is useful in finding missing test cases that I didn't think of.
