/*
# Topic : Library Management System 
You are going to build a project based on Library Management System. It keeps track of all information about books in the library, their cost, status and total number of books available in the library.
Create a database named library and following TABLES in the database: 1. Branch 2. Employee 3. Books 4. Customer 5. IssueStatus 6. ReturnStatus
*/
--  Create the Database
DROP DATABASE IF EXISTS library;
CREATE DATABASE library;
USE library;

-- Branch Table:
CREATE TABLE Branch (
    Branch_no INT PRIMARY KEY,
    Manager_Id INT,
    Branch_address VARCHAR(255),
    Contact_no VARCHAR(15)
);

-- Insert records into Branch
INSERT INTO Branch (Branch_no, Manager_Id, Branch_address, Contact_no) 
VALUES 
(1, 101, 'Kannur', '1234567890'),
(2, 102, 'Thrissur', '2345678901'),
(3, 103, 'Kochi', '3456789012'),
(4, 104, 'Kozhikode', '4567890123'),
(5, 105, 'Kottayam', '7890123456'),
(6, 106, 'Palakkad', '5678901234'),
(7, 107, 'Alappuzha', '6789012345'),  
(8, 108, 'Kochi', '9876543210');

-- View all records from Branch
SELECT * FROM Branch;

-- Employee Table:
CREATE TABLE Employee (
    Emp_Id INT PRIMARY KEY,
    Emp_name VARCHAR(100),
    Position VARCHAR(100),
    Salary DECIMAL(10, 2),
    Branch_no INT,
    FOREIGN KEY (Branch_no) REFERENCES Branch(Branch_no)
);

-- Insert records into Employee
INSERT INTO Employee (Emp_Id, Emp_name, Position, Salary, Branch_no)  
VALUES 
(109, 'Annie', 'Manager', 55000, 4),  
(110, 'Suriys', 'Assistant Manager', 45000, 6), 
(111, 'Riya', 'PRO', 60000, 3),   
(112, 'Farsan', 'Assistant', 30000, 6),   
(113, 'Shahid', 'Manager', 67000, 4),   
(114, 'Mary', 'Staff', 34000, 3),   
(116, 'Rizan', 'Manager', 60000, 6),
(117, 'Kevin', 'Staff', 32000, 6),
(118, 'Alina', 'Assistant', 35000, 6),
(119, 'James', 'Clerk', 28000, 6);   

-- View all records from Employee
SELECT * FROM Employee;

-- Books Table
CREATE TABLE Books (
    ISBN VARCHAR(17) PRIMARY KEY,
    Book_title VARCHAR(255),
    Category VARCHAR(100),
    Rental_Price DECIMAL(10, 2),
    Status VARCHAR(3),  -- 'yes' for available, 'no' for not available
    Author VARCHAR(100),
    Publisher VARCHAR(100)
); 

-- Inserting Data into Books Table
INSERT INTO Books (ISBN, Book_title, Category, Rental_Price, Status, Author, Publisher)
VALUES
('978-3-16-148410-0', 'The Great Gatsby', 'Fiction', 25.99, 'yes', 'F. Scott Fitzgerald', 'Scribner'),
('978-0-14-103614-4', '1984', 'Dystopian', 6.50, 'no', 'George Orwell', 'Penguin Books'),
('978-0-06-112008-4', 'To Kill a Mockingbird', 'Fiction', 14.75, 'yes', 'Harper Lee', 'J.B. Lippincott & Co.'),
('978-0-19-953556-9', 'Pride and Prejudice', 'Classic', 35.25, 'no', 'Jane Austen', 'Oxford University Press'),
('978-0-14-243724-7', 'Moby Dick', 'Adventure', 17.00, 'yes', 'Herman Melville', 'Penguin Classics'),
('978-0-19-923276-5', 'War and Peace', 'History', 19.50, 'no', 'Leo Tolstoy', 'Oxford University Press'),
('978-0-345-39169-6', 'Sapiens: A Brief History of Humankind', 'History', 8.99, 'yes', 'Yuval Noah Harari', 'Harper');

-- Retrieve all records from Books Table
SELECT * FROM Books;

-- Customer Table
CREATE TABLE Customer (
    Customer_Id INT PRIMARY KEY,
    Customer_name VARCHAR(100),
    Customer_address VARCHAR(255),
    Reg_date DATE
);

-- Inserting Data into Customer Table
INSERT INTO Customer (Customer_Id, Customer_name, Customer_address, Reg_date)
VALUES 
(1, 'Johny Tom', '123 Main St', '2021-01-15'),
(2, 'Smitha Raju', '456 Oak St', '2022-06-20'),
(3, 'Femi Wilson', '789 Pine St', '2021-04-12'),
(4, 'Lissy Mathew', '101 Maple St', '2023-06-01'),
(5, 'Teena Thomas', '202 Elm St', '2023-01-08'),  
(6, 'Emily Francis', '303 Birch St', '2023-06-19'),
(7, 'Leena Michael', '404 Cedar St', '2020-06-10'),
(8, 'Sema Manuel', '505 Pine St', '2021-12-15');


-- Retrieve all records from Customer Table
SELECT * FROM Customer;

-- IssueStatus Table:
CREATE TABLE IssueStatus (
    Issue_Id INT PRIMARY KEY,
    Issued_cust INT,
    Issued_book_name VARCHAR(255),
    Issue_date DATE,
    Isbn_book VARCHAR(17),
    FOREIGN KEY (Issued_cust) REFERENCES Customer(Customer_Id),
    FOREIGN KEY (Isbn_book) REFERENCES Books(ISBN)
);

-- Inserting Data into IssueStatus Table
INSERT INTO IssueStatus (Issue_Id, Issued_cust, Issued_book_name, Issue_date, Isbn_book)
VALUES
(101, 1, 'The Great Gatsby', '2023-06-10', '978-3-16-148410-0'),
(102, 2, '1984', '2024-09-10', '978-0-14-103614-4'),
(103, 3, 'To Kill a Mockingbird', '2023-06-15', '978-0-06-112008-4'),
(104, 4, 'Pride and Prejudice', '2024-07-22', '978-0-19-953556-9'),
(105, 5, 'Moby Dick', '2023-06-05', '978-0-14-243724-7'),
(106, 6, 'War and Peace', '2024-09-12', '978-0-19-923276-5'),
(107, 7, 'Sapiens: A Brief History of Humankind', '2024-10-01', '978-0-345-39169-6');

SELECT * FROM IssueStatus;

-- ReturnStatus Table:
CREATE TABLE ReturnStatus (
    Return_Id INT PRIMARY KEY,
    Return_cust INT,
    Return_book_name VARCHAR(255),
    Return_date DATE,
    Isbn_book2 VARCHAR(17),
    FOREIGN KEY (Return_cust) REFERENCES Customer(Customer_Id),
    FOREIGN KEY (Isbn_book2) REFERENCES Books(ISBN)
);

-- Inserting Data into ReturnStatus Table
INSERT INTO ReturnStatus (Return_Id, Return_cust, Return_book_name, Return_date, Isbn_book2)
VALUES
(201, 1, 'The Great Gatsby', '2024-09-01', '978-3-16-148410-0'),
(202, 2, '1984', '2024-09-15', '978-0-14-103614-4'),
(203, 3, 'To Kill a Mockingbird', '2024-08-05', '978-0-06-112008-4'),
(204, 4, 'Pride and Prejudice', '2024-08-12', '978-0-19-953556-9'),
(205, 5, 'Moby Dick', '2024-09-10', '978-0-14-243724-7'),
(206, 6, 'War and Peace', '2024-09-20', '978-0-19-923276-5'),
(207, 7, 'Sapiens: A Brief History of Humankind', '2024-10-05', '978-0-345-39169-6');

SELECT * FROM ReturnStatus;

SHOW TABLES;

-- Queries

-- 1. Retrieve the book title, category, and rental price of all available books:
SELECT Book_title, Category, Rental_Price 
FROM Books 
WHERE Status = 'yes';  -- Use 'yes' for available books

-- 2. List the employee names and their respective salaries in descending order of salary:
SELECT Emp_name, Salary 
FROM Employee 
ORDER BY Salary DESC;

-- 3. Retrieve the book titles and the corresponding customers who have issued those books:
SELECT B.Book_title, C.Customer_name 
FROM IssueStatus AS ISH
JOIN Books B ON ISH.Isbn_book = B.ISBN
JOIN Customer C ON ISH.Issued_cust = C.Customer_Id;

-- 4. Display the total count of books in each category:
SELECT Category, COUNT(*) AS Total_Books 
FROM Books 
GROUP BY Category;

-- 5. Retrieve the employee names and their positions for the employees whose salaries are above Rs. 50,000:
SELECT Emp_name, Position 
FROM Employee 
WHERE Salary > 50000;


-- 6. List the customer names who registered before 2022-01-01 and have not issued any books yet:
SELECT C.Customer_name 
FROM Customer C 
LEFT JOIN IssueStatus ISH ON C.Customer_Id = ISH.Issued_cust 
WHERE C.Reg_date < '2022-01-01' AND ISH.Issued_cust IS NULL;



-- 7. Display the branch numbers and the total count of employees in each branch
SELECT Branch_no, COUNT(E.Emp_Id) AS Total_Employees 
FROM Employee E
GROUP BY Branch_no;

-- 8. Display the names of customers who have issued books in the month of June 2023:
SELECT C.Customer_name 
FROM IssueStatus ISH 
JOIN Customer C ON ISH.Issued_cust = C.Customer_Id 
WHERE MONTH(ISH.Issue_date) = 6 AND YEAR(ISH.Issue_date) = 2023;

-- 9. Retrieve book titles from the Books table containing 'history':
SELECT Book_title 
FROM Books 
WHERE Category LIKE '%History%';

-- 10. Retrieve the branch numbers along with the count of employees for branches having more than 5 employees:
SELECT Branch_no, COUNT(E.Emp_Id) AS Employee_Count 
FROM Employee E 
GROUP BY Branch_no 
HAVING COUNT(E.Emp_Id) > 5;

-- 11. Retrieve the names of employees who manage branches and their respective branch addresses:
SELECT E.Emp_name, B.Branch_address 
FROM Employee E
JOIN Branch B ON E.Branch_no = B.Branch_no
WHERE E.Position = 'Manager';

-- 12. Display the names of customers who have issued books with a rental price higher than Rs. 25:
SELECT DISTINCT C.Customer_name 
FROM IssueStatus ISH 
JOIN Books B ON ISH.Isbn_book = B.ISBN 
JOIN Customer C ON ISH.Issued_cust = C.Customer_Id 
WHERE B.Rental_Price > 25.00;
