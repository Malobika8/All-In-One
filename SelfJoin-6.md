Here’s the **employees table**:

| emp\_id | name    | manager\_id |
| ------- | ------- | ----------- |
| 1       | Alice   | NULL        |
| 2       | Bob     | 1           |
| 3       | Charlie | 1           |
| 4       | David   | 2           |
| 5       | Emma    | 2           |
| 6       | Frank   | 3           |

---

## Question 1

If we run this query:

```sql
select e.name as Employee, m.name as Manager
from employees e
join employees m on e.manager_id = m.emp_id;
```

👉 What rows do you expect in the result?

### Sol:

Since the condition is `e.manager_id = m.emp_id`, we’ll only get employees who actually have a manager (i.e. `manager_id` is not NULL).

Let’s list them from the table:

* Bob → Alice
* Charlie → Alice
* David → Bob
* Emma → Bob
* Frank → Charlie

So the result will be:

| Employee | Manager |
| -------- | ------- |
| Bob      | Alice   |
| Charlie  | Alice   |
| David    | Bob     |
| Emma     | Bob     |
| Frank    | Charlie |

💡 Notice: Alice (the top manager) doesn’t appear as an employee here because she has no manager.

---

## Question 2:
What do you think will happen if we flip the condition to

```sql
select e.name as Employee, m.name as Manager
from employees e
join employees m on e.emp_id = m.manager_id;
```

Who shows up now?

### Sol:

We now join on

```
e.emp_id = m.manager_id
```

That means:

* Take **e** as the “manager” side (since emp\_id uniquely identifies each employee).
* Match it with **m** where `m.manager_id = e.emp_id`.

So this query shows **all managers** (those whose emp\_id appears as someone’s manager\_id) along with their direct reports.

🔍 From our data:

* Alice (1) → Bob (2), Charlie (3)
* Bob (2) → David (4), Emma (5)
* Charlie (3) → Frank (6)

Result:

| Manager | Employee |
| ------- | -------- |
| Alice   | Bob      |
| Alice   | Charlie  |
| Bob     | David    |
| Bob     | Emma     |
| Charlie | Frank    |

---

💡 Difference:

* `e.manager_id = m.emp_id` → shows employees **with managers**.
* `e.emp_id = m.manager_id` → shows managers **with their employees**.

---


