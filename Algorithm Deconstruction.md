# Algorithm Deconstruction Challenge

## Selected Algorithm
Task Priority Sorting and Filtering Algorithm

---

# 1. Recognize the Algorithm

This algorithm calculates a score for each task and then sorts tasks based on that score.

The score is influenced by several factors:

- Priority level (LOW → URGENT)
- Due date urgency
- Completion status
- Tags (such as blocker or critical)
- Recent updates

Each task is assigned a final numeric score. A higher score means higher importance.

---

# 2. How the Algorithm Works

## Step 1: Calculate Task Score

For each task:

- Priority is converted into a weight and multiplied
- Due date increases the score if the task is urgent or overdue
- Completed tasks reduce the score
- Important tags increase the score
- Recently updated tasks get a small boost

---

## Step 2: Sorting

All tasks are sorted based on their calculated score:

- Higher score = higher priority
- Lower score = lower priority

---

## Step 3: Top Tasks Selection

A limit is applied to return only the top N tasks (e.g., top 5).

---

# 3. Data Flow Diagram

```text
Tasks List
   ↓
calculate_task_score(task)
   ↓
Assign numeric score to each task
   ↓
Sort tasks by score (descending)
   ↓
Return sorted / top N tasks
```

---

# 4. Key Insights

- Priority alone does not determine ordering
- The system uses a weighted scoring model
- Multiple factors affect task importance
- Sorting happens after scoring, not before

---

# 5. Difficult Parts

- Understanding how multiple scoring factors combine into one value
- Realising that priority is only one part of the score
- Understanding how due dates significantly affect ranking

---

# 6. Explanation for Another Student

This algorithm gives each task a score based on different factors like priority, urgency, due date, and status.  
It then sorts all tasks from highest score to lowest score so the most important tasks appear first.

---

# 7. Reflection

The AI explanation helped break the scoring system into smaller parts.

At first, it looked like simple priority sorting, but it is actually a multi-factor scoring system.

This showed me that sorting algorithms can be based on weighted conditions, not just simple ordering.
