# sql6
1. Joins using School and College tables
Create School Table
CREATE TABLE School (
    School_Name VARCHAR(100),
    Student_Name VARCHAR(100),
    Enrollment_ID INT PRIMARY KEY
);

Create College Table
CREATE TABLE College (
    College_Name VARCHAR(100),
    Student_Name VARCHAR(100),
    Enrollment_ID INT PRIMARY KEY
);

Insert Values into School
INSERT INTO School VALUES
('Green Valley School', 'Arun', 101),
('Sunrise School', 'Bala', 102),
('Hill View School', 'Charan', 103),
('Riverdale School', 'Divya', 104);

Insert Values into College
INSERT INTO College VALUES
('ABC Engineering College', 'Arun', 101),
('XYZ Arts College', 'Bala', 102),
('National College', 'Ezhil', 105);

INNER JOIN

(Displays students present in both School and College)

SELECT 
    s.Student_Name,
    s.School_Name,
    c.College_Name,
    s.Enrollment_ID
FROM School s
INNER JOIN College c
ON s.Enrollment_ID = c.Enrollment_ID;

LEFT JOIN

(All School students + matched College data)

SELECT 
    s.Student_Name,
    s.School_Name,
    c.College_Name,
    s.Enrollment_ID
FROM School s
LEFT JOIN College c
ON s.Enrollment_ID = c.Enrollment_ID;

RIGHT JOIN

(All College students + matched School data)

SELECT 
    c.Student_Name,
    s.School_Name,
    c.College_Name,
    c.Enrollment_ID
FROM School s
RIGHT JOIN College c
ON s.Enrollment_ID = c.Enrollment_ID;

FULL OUTER JOIN

(All records from both tables)

SELECT 
    s.Student_Name,
    s.School_Name,
    c.College_Name,
    COALESCE(s.Enrollment_ID, c.Enrollment_ID) AS Enrollment_ID
FROM School s
FULL OUTER JOIN College c
ON s.Enrollment_ID = c.Enrollment_ID;


🔹 Note:
If using MySQL, FULL JOIN is written as:

SELECT s.Student_Name, s.School_Name, c.College_Name, s.Enrollment_ID
FROM School s
LEFT JOIN College c ON s.Enrollment_ID = c.Enrollment_ID
UNION
SELECT s.Student_Name, s.School_Name, c.College_Name, c.Enrollment_ID
FROM School s
RIGHT JOIN College c ON s.Enrollment_ID = c.Enrollment_ID;

2. Self Join – Products Table
Create Products Table
CREATE TABLE Products (
    Product_ID INT,
    Product_Name VARCHAR(100),
    Order_ID INT
);

Insert Values
INSERT INTO Products VALUES
(1, 'Medimix', 1001),
(2, 'Lux', 1002),
(3, 'Soap', 1003),
(4, 'Vim liquid', 1004),
(5, 'Washing Liquid', 1005),
(6, 'Surf Excel', 1006),
(7, 'Powder', 1007);

Self Join Query

(Map product with its related category using common names)

SELECT 
    p1.Product_Name AS Product_Name,
    p2.Product_Name AS Category
FROM Products p1
JOIN Products p2
ON (
    (p1.Product_Name LIKE '%Medimix%' OR p1.Product_Name LIKE '%Lux%')
    AND p2.Product_Name = 'Soap'
)
OR (
    p1.Product_Name LIKE '%Vim%'
    AND p2.Product_Name = 'Washing Liquid'
);

Result
Product Name      Category
----------------  ----------------
Medimix           Soap
Lux               Soap
Vim liquid        Washing Liquid
