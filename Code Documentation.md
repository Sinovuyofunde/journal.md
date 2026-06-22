# Code Documentation Exercise

## Selected Code
Task Priority Sorting Algorithm – `calculateTaskScore(Task task)`

---

# 1. Documentation (Prompt 1 Output)

## Function: calculateTaskScore

### Description
Calculates a numeric score for a task based on multiple factors including priority, due date, status, tags, and recent updates.  
This score is used to rank tasks by importance.

---

### Parameters

- `task` (Task)  
  The task object containing priority, due date, status, tags, and timestamps used for scoring.

---

### Returns

- `int`  
  A calculated importance score. Higher values indicate higher priority.

---

### Edge Cases / Errors

- If `priority` is missing, it defaults to 0.
- If `dueDate` is null, no due date scoring is applied.
- If `tags` are empty, no tag bonus is added.
- Completed tasks get a strong score reduction.

---

### Example Usage

```java
int score = calculateTaskScore(task);
