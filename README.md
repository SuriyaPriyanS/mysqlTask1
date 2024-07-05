MySQL Group and Join Tables
Overview
This document provides a guide on how to create and use MySQL groups and joins, and how to create tables and implement functions to manage data.

Prerequisites
MySQL Server installed
MySQL Workbench or any other MySQL client
Setup
1. Create Tables
First, create the tables that will be used in the database.

students Table
sql
Copy code
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    major VARCHAR(100)
);
courses Table
sql
Copy code
CREATE TABLE courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(100),
    credits INT
);
enrollments Table
sql
Copy code
CREATE TABLE enrollments (
    enrollment_id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    course_id INT,
    enrollment_date DATE,
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
2. Insert Data
Insert sample data into the tables.

Insert Data into students
sql
Copy code
INSERT INTO students (name, age, major) VALUES
('John Doe', 20, 'Computer Science'),
('Jane Smith', 22, 'Mathematics'),
('Emily Johnson', 21, 'Physics');
Insert Data into courses
sql
Copy code
INSERT INTO courses (course_name, credits) VALUES
('Database Systems', 3),
('Algorithms', 4),
('Operating Systems', 4);
Insert Data into enrollments
sql
Copy code
INSERT INTO enrollments (student_id, course_id, enrollment_date) VALUES
(1, 1, '2023-01-10'),
(1, 2, '2023-01-15'),
(2, 1, '2023-02-10'),
(3, 3, '2023-03-10');
3. Group and Join Queries
Grouping Data
Use the GROUP BY clause to group data.

sql
Copy code
SELECT major, COUNT(*) AS num_students
FROM students
GROUP BY major;
Joining Tables
Use the JOIN clause to combine rows from two or more tables.

Inner Join
sql
Copy code
SELECT students.name, courses.course_name, enrollments.enrollment_date
FROM enrollments
INNER JOIN students ON enrollments.student_id = students.student_id
INNER JOIN courses ON enrollments.course_id = courses.course_id;
Left Join
sql
Copy code
SELECT students.name, courses.course_name
FROM students
LEFT JOIN enrollments ON students.student_id = enrollments.student_id
LEFT JOIN courses ON enrollments.course_id = courses.course_id;
4. Functions
Creating a Function
Create a function to calculate the average age of students.

sql
Copy code
CREATE FUNCTION average_student_age()
RETURNS FLOAT
DETERMINISTIC
BEGIN
    DECLARE avg_age FLOAT;
    SELECT AVG(age) INTO avg_age FROM students;
    RETURN avg_age;
END;
Using the Function
Call the function to get the average age.

sql
Copy code
SELECT average_student_age() AS avg_age;
Conclusion
This document covered the basics of creating MySQL tables, inserting data, using group and join queries, and creating a function. For more complex operations, refer to the MySQL documentation or other resources.

This README provides a foundational understanding of MySQL operations related to grouping, joining, and functions. Modify it according to your specific requirements and database schema.





