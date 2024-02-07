# Library_Management_System

# Library Management System Project

This project is a Library Management System that keeps track of information about books in the library, including their cost, status, and the total number of books available. The system includes a relational database named `library` with six tables: Branch, Employee, Customer, IssueStatus, ReturnStatus, and Books.

## Database Schema

1. **Branch**
    - `Branch_no` (Primary Key)
    - `Manager_Id`
    - `Branch_address`
    - `Contact_no`

2. **Employee**
    - `Emp_Id` (Primary Key)
    - `Emp_name`
    - `Position`
    - `Salary`
    - `Branch_no` (Foreign Key referencing `Branch`)

3. **Customer**
    - `Customer_Id` (Primary Key)
    - `Customer_name`
    - `Customer_address`
    - `Reg_date`

4. **IssueStatus**
    - `Issue_Id` (Primary Key)
    - `Issued_cust` (Foreign Key referencing `Customer`)
    - `Issued_book_name`
    - `Issue_date`
    - `Isbn_book` (Foreign Key referencing `Books`)

5. **ReturnStatus**
    - `Return_Id` (Primary Key)
    - `Return_cust`
    - `Return_book_name`
    - `Return_date`
    - `Isbn_book2` (Foreign Key referencing `Books`)

6. **Books**
    - `ISBN` (Primary Key)
    - `Book_title`
    - `Category`
    - `Rental_Price`
    - `Status` (Yes if book available, No if not available)
    - `Author`
    - `Publisher`

## Setup Instructions

1. **Create Database:**
   - Execute the SQL script to create the `library` database.

2. **Create Tables:**
   - Execute the SQL script to create the tables within the `library` database.

3. **Insert Sample Data (Optional):**
   - If desired, insert sample data into the tables to test the provided queries.
## SQL Queries

### 1. Retrieve the book title, category, and rental price of all available books.
SELECT Book_title, Category, Rental_Price
FROM Books
WHERE Status = 'yes';

##  List the employee names and their respective salaries in descending order of salary.
SELECT Emp_name, Salary
FROM Employee
ORDER BY Salary DESC;

## Retrieve the book titles and the corresponding customers who have issued those books.
SELECT b.Book_title, c.Customer_name
FROM Books b
JOIN IssueStatus i ON b.ISBN = i.Isbn_book
JOIN Customer c ON i.Issued_cust = c.Customer_Id;

## Display the total count of books in each category.
SELECT Category, COUNT(*) AS TotalBooks
FROM Books
GROUP BY Category;

## Retrieve the employee names and their positions for the employees whose salaries are above Rs.50,000.
SELECT Emp_name, Position
FROM Employee
WHERE Salary > 50000;

## List the customer names who registered before 2022-01-01 and have not issued any books yet.
SELECT c.Customer_name
FROM Customer c
LEFT JOIN IssueStatus i ON c.Customer_Id = i.Issued_cust
WHERE c.Reg_date < '2022-01-01' AND i.Issue_Id IS NULL;

## Display the branch numbers and the total count of employees in each branch
SELECT e.Branch_no, COUNT(*) AS TotalEmployees
FROM Employee e
GROUP BY e.Branch_no;

## Display the names of customers who have issued books in the month of June 2023.
SELECT c.Customer_name
FROM Customer c
JOIN IssueStatus i ON c.Customer_Id = i.Issued_cust
WHERE YEAR(i.Issue_date) = 2023 AND MONTH(i.Issue_date) = 6;

## Retrieve book_title from the Books table containing 'history'.
SELECT Book_title
FROM Books
WHERE Category = 'history';

## Retrieve the branch numbers along with the count of employees for branches having more than 5 employees.
SELECT e.Branch_no, COUNT(*) AS TotalEmployees
FROM Employee e
GROUP BY e.Branch_no
HAVING TotalEmployees > 5;


