- 👋 Hi, I’m @flex997
- 👀 I’m interested in learning and develop my skills & knowledge.
- 🌱 I’m currently learning MySQL, PL/SQL, Database management, Python, PyCharm.
- 💞️ I’m looking to collaborate on creating/managing a database.
- 📫 How to reach me: LinkedIn Profile: https://www.linkedin.com/in/gabriel-avram-97aig29/
                     : G-Mail Address: avramioangabriel@gmail.com

<!---
flex997/flex997 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
- Below i have pasted a workbook of mine done in MySQL.
- Please note that the below lines of code represent a fictive database, just to demonstrate my knowledge on creating/managing a database.






DROP TABLE student;

CREATE TABLE student (
     student_id INT AUTO_INCREMENT,
	 name VARCHAR (20),
     major VARCHAR (20),
     PRIMARY KEY (student_id)
     );
    
    describe student;
INSERT INTO student VALUES(5, 'Mike', 'Computer Science');
INSERT INTO student VALUES(4, 'Jack', 'Biology');
INSERT INTO student VALUES(3, 'Claire', 'Chemistry');
INSERT INTO student VALUES(2, 'Kate', 'Sociology');
INSERT INTO student(student_id, name) VALUES(1, 'Jack');
INSERT INTO student(name, major) VALUES('Stan', 'Computer Science');

 
ALTER TABLE student add gpa DECIMAL(3, 2);
ALTER TABLE student DROP COLUMN gpa; 
   
  
  
  UPDATE student
  SET major = 'Bio'
  WHERE student_id = 4;
   
   
   UPDATE student
  SET major = 'Comp Sci'
  WHERE student_id = 5;

  
UPDATE student
 SET major = 'Biochemistry'
  WHERE major = 'Bio' OR major = 'Chemistry';


SELECT student.name, student.major
 FROM student
  ORDER BY name;
  
  SELECT student.name, student.major
 FROM student
  ORDER BY name DESC;
  
  SELECT *
 FROM student
  ORDER BY major, student_id;
  
   SELECT *
 FROM student
  ORDER BY major, student_id DESC;
  
     SELECT name, major
  FROM student
   WHERE major <> 'Chemistry';
   
   
   --  <, >, <=, >=, =, <>, AND, OR
   
    SELECT *
  FROM student
   WHERE student_id <= 3 AND name <> 'Jack';
   
   SELECT *
  FROM student
   WHERE name IN ('Claire', 'Kate', 'Mike');
   
   SELECT *
  FROM student
   WHERE major IN ('Biology', 'Chemistry') AND student_id > 2;
   
 
 -- In order to keep the working db more organised, please drop the above table and refer to the below for further queries. --
 

CREATE TABLE employee (
  emp_id INT PRIMARY KEY,
  first_name VARCHAR(40),
  last_name VARCHAR(40),
  birth_day DATE,
  sex VARCHAR(1),
  salary INT,
  super_id INT,
  branch_id INT
);
CREATE TABLE branch (
  branch_id INT PRIMARY KEY,
  branch_name VARCHAR(40),
  mgr_id INT,
  mgr_start_date DATE,
  FOREIGN KEY(mgr_id) REFERENCES employee(emp_id) ON DELETE SET NULL
);
ALTER TABLE employee
ADD FOREIGN KEY(branch_id)
REFERENCES branch(branch_id)
ON DELETE SET NULL;

ALTER TABLE employee
ADD FOREIGN KEY(super_id)
REFERENCES employee(emp_id)
ON DELETE SET NULL;
CREATE TABLE client (
  client_id INT PRIMARY KEY,
  client_name VARCHAR(40),
  branch_id INT,
  FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE SET NULL
);
CREATE TABLE works_with (
  emp_id INT,
  client_id INT,
  total_sales INT,
  PRIMARY KEY(emp_id, client_id),
  FOREIGN KEY(emp_id) REFERENCES employee(emp_id) ON DELETE CASCADE,
  FOREIGN KEY(client_id) REFERENCES client(client_id) ON DELETE CASCADE
);
CREATE TABLE branch_supplier (
  branch_id INT,
  supplier_name VARCHAR(40),
  supply_type VARCHAR(40),
  PRIMARY KEY(branch_id, supplier_name),
  FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE CASCADE
);
-- Corporate
INSERT INTO employee VALUES(100, 'David', 'Wallace', '1967-11-17', 'M', 250000, NULL, NULL);

INSERT INTO branch VALUES(1, 'Corporate', 100, '2006-02-09');

UPDATE employee
SET branch_id = 1
WHERE emp_id = 100;

INSERT INTO employee VALUES(101, 'Jan', 'Levinson', '1961-05-11', 'F', 110000, 100, 1);
-- Scranton
INSERT INTO employee VALUES(102, 'Michael', 'Scott', '1964-03-15', 'M', 75000, 100, NULL);

INSERT INTO branch VALUES(2, 'Scranton', 102, '1992-04-06');

UPDATE employee
SET branch_id = 2
WHERE emp_id = 102;

INSERT INTO employee VALUES(103, 'Angela', 'Martin', '1971-06-25', 'F', 63000, 102, 2);
INSERT INTO employee VALUES(104, 'Kelly', 'Kapoor', '1980-02-05', 'F', 55000, 102, 2);
INSERT INTO employee VALUES(105, 'Stanley', 'Hudson', '1958-02-19', 'M', 69000, 102, 2);
-- Stamford
INSERT INTO employee VALUES(106, 'Josh', 'Porter', '1969-09-05', 'M', 78000, 100, NULL);

INSERT INTO branch VALUES(3, 'Stamford', 106, '1998-02-13');

UPDATE employee
SET branch_id = 3
WHERE emp_id = 106;

INSERT INTO employee VALUES(107, 'Andy', 'Bernard', '1973-07-22', 'M', 65000, 106, 3);
INSERT INTO employee VALUES(108, 'Jim', 'Halpert', '1978-10-01', 'M', 71000, 106, 3);
-- BRANCH SUPPLIER
INSERT INTO branch_supplier VALUES(2, 'Hammer Mill', 'Paper');
INSERT INTO branch_supplier VALUES(2, 'Uni-ball', 'Writing Utensils');
INSERT INTO branch_supplier VALUES(3, 'Patriot Paper', 'Paper');
INSERT INTO branch_supplier VALUES(2, 'J.T. Forms & Labels', 'Custom Forms');
INSERT INTO branch_supplier VALUES(3, 'Uni-ball', 'Writing Utensils');
INSERT INTO branch_supplier VALUES(3, 'Hammer Mill', 'Paper');
INSERT INTO branch_supplier VALUES(3, 'Stamford Lables', 'Custom Forms');
-- CLIENT
INSERT INTO client VALUES(400, 'Dunmore Highschool', 2);
INSERT INTO client VALUES(401, 'Lackawana Country', 2);
INSERT INTO client VALUES(402, 'FedEx', 3);
INSERT INTO client VALUES(403, 'John Daly Law, LLC', 3);
INSERT INTO client VALUES(404, 'Scranton Whitepages', 2);
INSERT INTO client VALUES(405, 'Times Newspaper', 3);
INSERT INTO client VALUES(406, 'FedEx', 2);
-- WORKS_WITH
INSERT INTO works_with VALUES(105, 400, 55000);
INSERT INTO works_with VALUES(102, 401, 267000);
INSERT INTO works_with VALUES(108, 402, 22500);
INSERT INTO works_with VALUES(107, 403, 5000);
INSERT INTO works_with VALUES(108, 403, 12000);
INSERT INTO works_with VALUES(105, 404, 33000);
INSERT INTO works_with VALUES(107, 405, 26000);
INSERT INTO works_with VALUES(102, 406, 15000);
INSERT INTO works_with VALUES(105, 406, 130000);

select * from employee;
select * from works_with;

-- SELECT --
-- Find all employees
SELECT *
FROM employee;

-- Find all clients
SELECT *
FROM client;

-- Find all employees ordered by salary
SELECT *
FROM employee
ORDER BY salary;

-- Find all employees ordered by sex then name
SELECT *
FROM employee
ORDER BY sex, first_name, last_name;

-- Find the first 5 employees in the table
SELECT *
FROM employee
LIMIT 5;

-- Find the first and last names of all employees
SELECT first_name, last_name
FROM employee;

-- Find the forename an the surenames of all employees
SELECT first_name AS forename, last_name AS surename
FROM employee;

-- Find out all the different genders
SELECT distinct sex
FROM employee;

-- Find the number of employees
SELECT count(emp_id)
FROM employee;

SELECT count(super_id)
FROM employee;

-- Find the number of female employees born after 1970
SELECT COUNT(emp_id)
FROM employee
WHERE sex = 'F' AND birth_date > '1970-01-01';

-- Find the average(AVG) of all employee's salaries
SELECT AVG(salary)
FROM employee
WHERE sex = 'M';

-- Find the sum(SUM) of all employee's salaries
SELECT SUM(salary)
FROM employee;

-- Find out how many males and how many females there are
SELECT COUNT(sex), sex
FROM employee
GROUP BY sex;

-- Find the total sales of each salesman
SELECT SUM(total_sales), emp_id
FROM works_with
GROUP BY emp_id;
-- Client case
SELECT SUM(total_sales), client_id
FROM works_with
GROUP BY client_id;

-- WILDCARDS -- 

--	%	=	any # characters,	_	=	one character

-- Find any clients who are an LLC (Limited Liability Company)
SELECT *
FROM client
WHERE client_name LIKE '%LLC';

-- Find any branch supplier who are in the label business
SELECT *
FROM branch_supplier
WHERE supplier_name LIKE '% Label%';

-- Find an employee born in October
SELECT *
FROM employee
WHERE birth_day LIKE '____-10%';

-- Find any clients who are schools
SELECT * 
FROM client
WHERE client_name LIKE '%school%';

-- UNION --

-- Find a list of employee and branch names
SELECT first_name
FROM employee
UNION
SELECT branch_name
FROM branch
UNION
SELECT client_name
FROM client;

-- Find a list of all clients & branch suppliers names
SELECT client_name, branch_id
FROM client
UNION
SELECT supplier_name, branch_id
FROM branch_supplier;

-- Because of similarities, another way of quering the above would be
SELECT client_name, client.branch_id
FROM client
UNION
SELECT supplier_name, branch_supplier.branch_id
FROM branch_supplier;

-- Find a list of all money spent or earned by the company
SELECT salary
FROM employee
UNION
SELECT total_sales
FROM works_with;


-- JOINS --
-- In order to enhance the learning experience, we will add the below line into our DB.
INSERT INTO branch VALUES(4, 'Buffalo', NULL, NULL);

-- Find all branches and the names of their managers
SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee
JOIN branch
ON employee.emp_id = branch.mgr_id;
-- LEFT JOIN --
SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee
LEFT JOIN branch
ON employee.emp_id = branch.mgr_id;
-- RIGHT JOIN --
SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee
RIGHT JOIN branch
ON employee.emp_id = branch.mgr_id;

-- Please note: As the lines of code continue, we're getting into more advanced query writing.
 --  Always refer to the basic symbols with which MySQL operates, in order to follow along with the syntax. 
 
 -- NESTED QUERIES --
 
-- Find names of all employees who have sold  over 30,000 to a single client
SELECT works_with.emp_id
FROM works_with
WHERE works_with.total_sales  > 30000;

SELECT employee.first_name, employee.last_name
FROM employee
WHERE employee.emp_id IN (
	SELECT works_with.emp_id
	FROM works_with
	WHERE works_with.total_sales  > 30000
);

-- Find all clients who are handled by the branch that Michael Scott manages. *assume you know Michael's ID*
SELECT branch.branch_id
FROM branch
WHERE branch.mgr_id = 102;

SELECT client.client_name
FROM client
WHERE client.branch_id = (
	SELECT branch.branch_id
	FROM branch
	WHERE branch.mgr_id = 102
	LIMIT 1
);

-- The above nested queries are recognized as embedded by the relational db management system.
-- Therefore, when RDMS sees an embedded SQL statement like this, it's going to execute the nested query first, and afterwards the outer query.

-- ON DELETE --

-- ON DELETE SET NULL --
	-- Orders to set any foreign keys as NULL, after deleting the table.
CREATE TABLE client (
  client_id INT PRIMARY KEY,
  client_name VARCHAR(40),
  branch_id INT,
  FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE SET NULL
);

-- ON DELETE CASCADE --
	-- Orders to delete the entire rows into the table, if you delete it.
CREATE TABLE works_with (
  emp_id INT,
  client_id INT,
  total_sales INT,
  PRIMARY KEY(emp_id, client_id),
  FOREIGN KEY(emp_id) REFERENCES employee(emp_id) ON DELETE CASCADE,
  FOREIGN KEY(client_id) REFERENCES client(client_id) ON DELETE CASCADE
);

-- Remember! These two functions are used in relation to what you have in your db.
	-- For situations where a foreign key is also a primary key, use ON DELETE CASCADE.
    
    
    
    
    -- TRIGGERS --
   
   CREATE TABLE trigger_test (
		message VARCHAR(100)
        );
  

DELIMITER $$
CREATE 
	TRIGGER my_trigger BEFORE INSERT 
    ON employee
    FOR EACH ROW BEGIN 
		INSERT INTO trigger_test VALUES('added new employee');
	END $$ 
DELIMITER ;

INSERT INTO employee 
VALUES(109, 'Oscar', 'Martinez', '1968-02-19', 'M', 69000, 106, 3);

select * from trigger_test;

DELIMITER $$
CREATE 
	TRIGGER my_trigger1 BEFORE INSERT 
    ON employee
    FOR EACH ROW BEGIN 
		INSERT INTO trigger_test VALUES(NEW.first_name);
	END $$ 
DELIMITER ;

INSERT INTO employee
VALUES (111, 'Kevin', 'Malone', '1978-02-19', 'M', 69000, 106, 3);



DELIMITER $$
CREATE 
	TRIGGER my_trigger2 BEFORE INSERT 
    ON employee
    FOR EACH ROW BEGIN 
		IF NEW.sex = 'M' THEN
				INSERT INTO trigger_test VALUES('added male employee');
		ELSEIF NEW.sex = 'F' THEN
				INSERT INTO trigger_test VALUES('added female employee');
		ELSE 
				INSERT INTO trigger_test VALUES('added other employee');
		END IF;
	END $$ 
DELIMITER ;

select * from trigger_test;

INSERT INTO employee
VALUES (118, 'Pam', 'Beesly', '1988-02-19', 'F', 69000, 106, 3);

-- You can create triggers for both BEFORE INSERT & AFTER DELETE.

drop trigger my_trigger;

--    ER	DIAGRAMS	--























  
  
    
    
    



    
