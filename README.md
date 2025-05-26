Got it! Here’s a full practical write-up in a nice format, suitable for your exam notebook:


---

Aim

To perform various operations on the Employee table using MySQL, including group by, lowest paid employee, order by, altering columns, and triggers.


---

Procedures

1. Create the Employee table.


2. Insert some sample data (if needed).


3. Use GROUP BY to display employee names and salary for department ‘xxx’.


4. Display the lowest paid employee in each department.


5. List employee names in descending order.


6. Rename a column using ALTER TABLE.


7. Create a trigger to insert a row in the log table whenever a new row is inserted in Employee table.




---

Queries

1. Create the Employee table



CREATE TABLE Employee (
    Emp_no INT PRIMARY KEY,
    Emp_name VARCHAR(50),
    Emp_dept VARCHAR(50),
    Job VARCHAR(50),
    Mgr INT,
    Sal DECIMAL(10,2)
);


---

2. Insert sample data (optional for testing)



INSERT INTO Employee (Emp_no, Emp_name, Emp_dept, Job, Mgr, Sal) VALUES
(1, 'John', 'Sales', 'Manager', 101, 5000),
(2, 'Alice', 'Sales', 'Executive', 101, 3000),
(3, 'Bob', 'HR', 'Executive', 102, 4000),
(4, 'Charlie', 'HR', 'Manager', 102, 6000),
(5, 'David', 'IT', 'Executive', 103, 2000);


---

3. a) Use GROUP BY to display Emp_name and salary for Emp_dept='Sales'



SELECT Emp_name, Sal
FROM Employee
WHERE Emp_dept = 'Sales'
GROUP BY Emp_name, Sal;


---

4. b) Display lowest paid employee details under each department



SELECT Emp_dept, Emp_name, Sal
FROM Employee e
WHERE Sal = (
    SELECT MIN(Sal)
    FROM Employee
    WHERE Emp_dept = e.Emp_dept
);


---

5. c) List the employee names in descending order



SELECT Emp_name
FROM Employee
ORDER BY Emp_name DESC;


---

6. d) Rename the column Emp_name to Employee_Name



ALTER TABLE Employee
CHANGE COLUMN Emp_name Employee_Name VARCHAR(50);


---

7. e) Insert row in Employee table using a trigger



i. Create log table for demonstration:

CREATE TABLE Employee_log (
    Emp_no INT,
    Emp_name VARCHAR(50),
    Action_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

ii. Create the trigger:

DELIMITER $$

CREATE TRIGGER before_employee_insert
BEFORE INSERT ON Employee
FOR EACH ROW
BEGIN
    INSERT INTO Employee_log (Emp_no, Emp_name)
    VALUES (NEW.Emp_no, NEW.Emp_name);
END $$

DELIMITER ;

iii. Insert a row to test trigger:

INSERT INTO Employee (Emp_no, Emp_name, Emp_dept, Job, Mgr, Sal)
VALUES (6, 'Eve', 'Finance', 'Analyst', 104, 3500);


---

Output & Result

1. GROUP BY Output

Displays employee names and salaries from Sales department.



2. Lowest Paid Employee

Displays the employee(s) with the lowest salary in each department.



3. Descending Order List

Lists employee names from Z to A.



4. Renamed Column

Emp_name column changed to Employee_Name.



5. Trigger Output

When you insert a new employee, a log entry is added automatically in Employee_log table.





---

Result:
Successfully performed the MySQL queries: created table, inserted data, used GROUP BY, found lowest paid employee, sorted data, renamed column, and created trigger.


---

Let me know if you’d like this in a formatted document or if you need to modify it for your school/college’s template!

