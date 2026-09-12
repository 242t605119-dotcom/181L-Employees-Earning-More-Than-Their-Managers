# LeetCode 181 - Employees Earning More Than Their Managers

## Problem

The `Employee` table contains information about employees, including their salary and the ID of their manager.

The task is to find the employees who **earn more than their managers**.

The result should contain the employee's name in a column named `Employee`.

## Table Structure

The `Employee` table contains:

* `id` - Unique ID of the employee
* `name` - Name of the employee
* `salary` - Salary of the employee
* `managerId` - ID of the employee's manager

## Approach

This problem can be solved using a **Self Join**.

Since both employees and managers are stored in the same `Employee` table, we use the table twice:

* `e1` represents the employee.
* `e2` represents the employee's manager.

The relationship is established using:

`e1.managerId = e2.id`

After connecting each employee with their manager, we compare their salaries.

If:

`e1.salary > e2.salary`

then the employee earns more than their manager, so we include their name in the result.

## SQL Query

```sql
SELECT e1.name AS Employee
FROM Employee e1
JOIN Employee e2
ON e1.managerId = e2.id
WHERE e1.salary > e2.salary;
```

## Example

### Input

| id | name  | salary | managerId |
| -- | ----- | ------ | --------- |
| 1  | Joe   | 70000  | 3         |
| 2  | Henry | 80000  | 4         |
| 3  | Sam   | 60000  | NULL      |
| 4  | Max   | 90000  | NULL      |

### Output

| Employee |
| -------- |
| Joe      |

Joe earns `70000`, while his manager Sam earns `60000`.

Therefore, Joe is included in the result.

## Key Concept

**Self Join**

A self join is used when we need to compare rows within the same table.

Here:

* `e1` → Employee
* `e2` → Manager

The important relationship is:

`Employee.managerId = Manager.id`

Then we compare:

`Employee.salary > Manager.salary`

## Time Complexity

The exact execution cost depends on the database engine and indexes. Since `id` is the primary key, the manager lookup can be performed efficiently.

For the logical SQL operation, we can consider the comparison as approximately **O(n)** with an indexed employee ID lookup.

## Space Complexity

The query uses a self join and does not require an additional data structure proportional to the input.

**Auxiliary Space: O(1)**

## Difficulty

**Easy**

## Topic

* SQL
* Self Join
* JOIN
* WHERE condition
* Table aliases
* Comparing rows from the same table

## What I Learned

This problem helped me understand how a table can be joined with itself to compare related records. It also improved my understanding of table aliases and how `JOIN` conditions can connect an employee with their manager.

## Author

T.Nandhini
