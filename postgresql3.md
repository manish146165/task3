
<center>

<h1><u> PostgreSQL Assignment-3</u></h1>

</center>


## 1. Create a new PostgreSQL database named "keenable".

<h4>postgres=# create database keenable;</h4>

<p>Here's a short explanation of the command:

    create database: This is the SQL command for creating a new database.
    keenable: This is the name of the database being created. You can replace "keenable" with the desired name for your database.

This command is essential for initializing a new database within your PostgreSQL server.</p>

![Alt text](<Screenshot from 2023-10-12 10-41-55.png>)


## 2. Define three schemas within the database: "hr", "technical", and "management".

#### postgres=# \c keenable 

![Alt text](connectingdb.png)
<p>It's a way to change  current database context to "keenable" for running SQL queries and operations within that database.</p>


<h4>A. keenable=# create schema hr; <br>B. keenable=# create schema technical;<br>C. keenable=# create schema management;
</h4>

![Alt text](sch.png)
<p>This query creates a schema named "hr","technical","management" in the "keenable" database.</p>

#### keenable=# \dn
![Alt text](schlist.png)

<p>The command \dn in PostgreSQL is used to list all the schemas in the current database. </p>

<p><h4>2.1 HR Schema:</h4>

![Alt text](hrtable.png)
![Alt text](<vc table.png>)

Create the following tables in the "hr" schema:<br>
<h4>2.1.1.</h4> 

![Alt text](<insert data.png>)

"employees" to store employee information (employee_id, first_name,last_name, email, hire_date).<br>
<h4>2.1.2.</h4> 

![Alt text](insertingvc.png)
![Alt text](vstablelist.png)
"vacation_requests" to track employee vacation requests (request_id,employee_id, start_date, end_date, status).</p>


<p> <h4>2.2. Technical Schema:</h4> <br>

![Alt text](pj.png)
Create the following tables in the "technical" schema:

<h4>2.2.1.</h4> 

![Alt text](pj1.png)
![Alt text](tc.png)
"projects" to store project details (project_id, project_name, start_date,end_date).<br>


<h4>2.2.2. </h4>

![Alt text](pj2.png)
![Alt text](pc.png)
"project_assignments" to associate employees with projects
(assignment_id, project_id, employee_id, assignment_date).
</p>


<p><h4>2.3. Management Schema:</h4><br>

![Alt text](dep1.png)
![Alt text](dep2.png)
Create the following tables in the "management" schema:<br>

<h4>2.3.1.</h4>

![Alt text](man1.png)
![Alt text](mg2.png)

 "departments" to manage department information (department_id,department_name, location).<br>

<h4>2.3.2.</h4> 

![Alt text](cc.png)
![Alt text](12.png)
"department_employees" to track employee department assignments
(assignment_id, employee_id, department_id, start_date, end_date).</p>

## 3. Relationships:
<p>
Establish appropriate foreign key relationships between tables to maintain
referential integrity. For example, link "project_assignments" to "projects" and
"employees."<br><br>

##### For that I had used the following command:
1. keenable=#-- In the "technical" schema
ALTER TABLE technical.project_assignments
ADD CONSTRAINT fk_project_assignment_project
FOREIGN KEY (project_id) REFERENCES technical.projects(project_id);
ALTER TABLE <br><br>

2. keenable=# -- In the "technical" schema
ALTER TABLE technical.project_assignments
ADD CONSTRAINT fk_project_assignment_employee
FOREIGN KEY (employee_id) REFERENCES hr.employees(employee_id);
ALTER TABLE




![Alt text](re.png)
![Alt text](re1.png)
</p>

## 4. Queries and Reporting:
<p>

Write SQL queries to retrieve information such as:
4.1. Employees in a specific department
4.2. Projects assigned to an employee.
4.3. Vacation requests for an employee.

<h4>4.1.</h4> 

##### For that I had used the following command:

keenable=# SELECT e.first_name, e.last_name
FROM hr.employees e
JOIN management.departments_employees de ON e.employee_id = de.employee_id
JOIN management.departments d ON de.department_id = d.department_id
WHERE d.department_name = 'HR Department';


![Alt text](yy.png)

Employees in a specific department
<h4>4.2.</h4>

##### For that I had used the following command:

keenable=# SELECT p.project_name
FROM technical.project_assignments pa
INNER JOIN technical.projects p ON pa.project_id = p.project_id
WHERE pa.employee_id = 1;  -- Replace with the desired employee ID


![Alt text](yy1.png)

Projects assigned to an employee.

<h4>4.3.</h4> 

##### For that I had used the following command:

keenable=# SELECT vr.request_id, vr.start_date, vr.end_date, vr.status
FROM hr.vacation_requests vr
WHERE vr.employee_id = 4;  -- Replace with the desired employee ID


![Alt text](yy2.png)
Vacation requests for an employee.</p>
