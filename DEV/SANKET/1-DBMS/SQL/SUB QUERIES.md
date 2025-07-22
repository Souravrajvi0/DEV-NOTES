---
view-count: 4
---
A **subquery** is a query nested inside another SQL query. It is used to retrieve data that will be used by the main (or outer) query. Subqueries can be used in various SQL statements such as `SELECT`, `INSERT`, `UPDATE`, or `DELETE`.

### **Types of Subqueries**

## 1. **Single-Row Subquery**:
    
    - Returns a single value (one row and one column).
    - It is often used in conjunction with comparison operators like =,<,>
    - This allows the outer query to filter results based on the single value returned by the inner query.

     EXAMPLE:
```SQL
SELECT name
FROM employees
WHERE department_id = (
    SELECT department_id
    FROM departments
    WHERE department_name = 'Sales'
);

```
#### Components:

1. **Outer Query**:
    
    - `SELECT name FROM employees`
    - This part selects the `name` of employees from the `employees` table.
2. **Comparison Operator**:
    
    - `WHERE department_id = (...)`
    - The outer query uses the   =  operator to compare the `department_id` of each employee with the result of the inner query.
```SQL
SELECT department_id
FROM departments
WHERE department_name = 'Sales'

```

- This subquery retrieves the `department_id` of the department named 'Sales' from the `departments` table.
### How It Works

1. **Execution of Inner Query**:
    
    - The inner query is executed first. It searches the `departments` table for a row where the `department_name` is 'Sales'.
    - If there is a department with that name, it returns the corresponding `department_id`.
    - Since this is a single-row subquery, it should return only one value (the `department_id` of the 'Sales' department).
2. **Execution of Outer Query**:
    
    - After the inner query returns the `department_id`, the outer query retrieves the names of employees from the `employees` table.
    - It filters these employees by checking if their `department_id` matches the value returned by the inner query.

- If the inner query in a single-row subquery returns a column of data containing multiple `department_id` values instead of a single value, it will result in an error
- To handle situations where the inner query might return multiple rows, you can use one of the following approaches:
####  Use `IN` Instead of =
If you expect multiple `department_id` values, you can use the `IN` operator:

```SQL
SELECT name
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
);
```




## 2. **Multi-Row Subquery**:

A **Multiple-Row Subquery** is a type of subquery that returns multiple rows (but typically only one column). This is useful when you want to compare a value against a list of values returned by the subquery. Common operators used with multiple-row subqueries include `IN`, `ANY`, and `ALL`



```SQL
SELECT name
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location_id = 100
);

```

We can use the `IN` operator on a resultant table (or set of rows) returned by a subquery. The `IN` operator checks if a specified value matches any value in a list or a result set


#### Components:

1. **Outer Query**:
    
    - `SELECT name FROM employees`
    - This part selects the `name` of employees from the `employees` table.
2. **Comparison Operator**:
    
    - `WHERE department_id IN (...)`
    - The outer query uses the `IN` operator to check if the `department_id` of each employee is present in the list of department IDs returned by the inner query.

![SUB QUERIES-20250101154655831.webp](../../../Images/SUB%20QUERIES-20250101154655831.webp)

### How It Works

1. **Execution of Inner Query**:
    
    - The inner query is executed first. It searches the `departments` table for all rows where `location_id` equals `100`.
    - It returns a list of `department_id` values that meet this condition. For example, it might return:
        - `1`
        - `2`
        - `3`

2. **Execution of Outer Query**:
    
    - After the inner query returns the list of `department_id` values, the outer query retrieves the names of employees from the `employees` table.
    - It filters these employees by checking if their `department_id` is in the list returned by the inner query.

- A **Multiple-Row Subquery** returns multiple rows (but typically only one column).
- The outer query can use operators like `IN` to filter results based on the list of values returned by the inner query.
- This approach is useful for retrieving data based on a set of criteria



## 3. **Multi-Column Subquery**:

- Returns multiple columns (one or more rows).
- Used in situations like comparisons or joins.

**Example**: Find employees whose department and job match those of a specific employee


```SQL
SELECT employee_id, name
FROM employees
WHERE (department_id, job_id) = (
    SELECT department_id, job_id
    FROM employees
    WHERE name = 'John Doe'
);

```


## 4. **Correlated Subquery**:

A **Correlated Subquery** is a subquery that references columns from the outer query. 
Unlike regular subqueries, which are executed independently, a correlated subquery is executed once for each row processed by the outer query. 
This means that the inner query depends on the outer query for its values.


```SQL
SELECT employee_id, name, salary
FROM employees e1
WHERE salary > (
    SELECT AVG(salary)
    FROM employees e2
    WHERE e1.department_id = e2.department_id
);

```

#### Components:

1. **Outer Query**:
    
    - `SELECT name FROM employees e`
    - This part selects the `name` of employees from the `employees` table. The alias `e` is used to refer to the `employees` table.
2. **Comparison Operator**:
- `WHERE salary > (...)`
- The outer query checks if the `salary` of each employee is greater than the result of the inner query.

**Inner Query**:

```SQL
SELECT AVG(salary)
FROM employees
WHERE department_id = e.department_id
```

- This subquery calculates the average salary of employees in the same department as the current employee being processed by the outer query.
- It uses `e.department_id`, which refers to the `department_id` of the current employee in the outer query.


### How It Works

1. **Execution of Outer Query**:
    
    - The outer query processes each employee one at a time.
    - For each employee, it retrieves their `salary` and `department_id`.
2. **Execution of Inner Query**:
    
    - For each employee, the inner query is executed to calculate the average salary of employees in that employee's department.
    - This means that the inner query runs once for each employee, making it "correlated" to the outer query.
3. **Comparison**:
    
    - The outer query then checks if the employee's `salary` is greater than the average salary returned by the inner query.
    - If it is, that employee's name is included in the final result set.


### Example Scenario

Assume the following data in the `employees` table:

|employee_id|name|salary|department_id|
|---|---|---|---|
|101|Alice|60000|1|
|102|Bob|50000|1|
|103|Charlie|70000|2|
|104|David|80000|2|

### Step-by-Step Execution

1. **For Alice** (department_id = 1):
    
    - Inner query: `SELECT AVG(salary) FROM employees WHERE department_id = 1`
    - Calculates average salary: (60000 + 50000) / 2 = 55000.
    - Outer query checks: `60000 > 55000` (True, include Alice).
2. **For Bob** (department_id = 1):
    
    - Inner query: Same as above, average = 55000.
    - Outer query checks: `50000 > 55000` (False, do not include Bob).
3. **For Charlie** (department_id = 2):
    
    - Inner query: `SELECT AVG(salary) FROM employees WHERE department_id = 2`
    - Calculates average salary: (70000 + 80000) / 2 = 75000.
    - Outer query checks: `70000 > 75000` (False, do not include Charlie).
4. **For David** (department_id = 2):
    
    - Inner query: Same as above, average = 75000.
    - Outer query checks: `80000 > 75000` (True, include David).

### Final Output

The final output of the query will be:

| name  |
| ----- |
| Alice |
| David |







## 5. **Scalar Subquery**:

A **Scalar Subquery** is a type of subquery that returns exactly one value (one row and one column). It is commonly used in `SELECT` or `WHERE` clauses to provide a single value that can be used in the main query. This type of subquery is particularly useful for calculations or aggregations that need to be performed for each row in the outer query.



```SQL
SELECT department_id, 
       (SELECT COUNT(*) FROM employees e WHERE e.department_id = d.department_id) AS total_employees
FROM departments d;


```

#### Components:

1. **Outer Query**:
    
    - `SELECT department_id, ... FROM departments d`
    - This part selects the `department_id` from the `departments` table. The alias `d` is used to refer to the `departments` table.

**Scalar Subquery**:


```SQL
(SELECT COUNT(*) FROM employees e WHERE e.department_id = d.department_id) AS total_employees
```
- This subquery counts the number of employees in each department.
- It references `d.department_id`, which corresponds to the `department_id` of the current department being processed by the outer query.
- The result of this subquery will be a single value representing the total number of employees in that specific department


### How It Works

1. **Execution of Outer Query**:
    
    - The outer query retrieves each `department_id` from the `departments` table.
2. **Execution of Scalar Subquery**:
    
    - For each department, the scalar subquery is executed to count the employees in that department.
    - Since it is a scalar subquery, it will always return one value (the count of employees).
3. **Result Compilation**:
    
    - The outer query combines the `department_id` with the result of the scalar subquery, producing a result set that shows each department and the total number of employees in it.

### Example Scenario

Assume the following data in the `departments` and `employees` tables:

**Departments Table**:

|department_id|department_name|
|---|---|
|1|Sales|
|2|Marketing|
|3|IT|

**Employees Table**:

|employee_id|name|department_id|
|---|---|---|
|101|Alice|1|
|102|Bob|1|
|103|Charlie|2|
|104|David|2|
|105|Eve|1|

### Step-by-Step Execution

1. **For department_id = 1 (Sales)**:
    
    - Scalar subquery: `SELECT COUNT(*) FROM employees e WHERE e.department_id = 1`
    - Count = 3 (Alice, Bob, Eve).
2. **For department_id = 2 (Marketing)**:
    
    - Scalar subquery: `SELECT COUNT(*) FROM employees e WHERE e.department_id = 2`
    - Count = 2 (Charlie, David).
3. **For department_id = 3 (IT)**:
    
    - Scalar subquery: `SELECT COUNT(*) FROM employees e WHERE e.department_id = 3`
    - Count = 0 (no employees).

### Final Output

The final output of the query will be:

|department_id|total_employees|
|---|---|
|1|3|
|2|2|
|3|0|

### Summary

- A **Scalar Subquery** returns exactly one value and is often used in `SELECT` or `WHERE` clauses.
- In this example, the scalar subquery counts the total number of employees in each department and returns it alongside the `department_id`.
- This allows for efficient aggregation of data related to each department.



### **Key Characteristics**

- Subqueries are enclosed in parentheses `()`.
- They can appear in:
    - **`WHERE` Clause**: Used for filtering.
    - **`FROM` Clause**: Acts like a virtual table (inline views).
    - **`SELECT` Clause**: To include derived values in the result.
- Subqueries must return data in the format expected by the outer query:
    - **Single value** for comparisons.
    - **Multiple values** for `IN`, `ANY`, or `ALL`.