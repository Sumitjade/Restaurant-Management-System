# Restaurant-Management-System
Scenario:

Based in Pune, Little Italy is a family-owned Mediterranean restaurant, focused on traditional recipes served with a modern twist. The chefs draw inspiration from Italian, Greek, and Turkish culture and have a menu of 12–15 items that they rotate seasonally. The restaurant has a rustic and relaxed atmosphere with moderate prices, making it a popular place for a meal any time of the day.

Little Italy is owned by two Italian brothers, Mario and Adrian, who moved to the India to pursue their shared dream of owning a restaurant. To craft the menu, Mario relies on family recipes and his experience as a chef in Italy. Adrian does all the marketing for the restaurant and led the effort to expand the menu beyond classic Italian to incorporate additional cuisines from the Mediterranean region.

Prerequisites:
You must first create the_Little Italy database in MySQL  . You must also have the Customers, Bookings, and Courses tables created and populated with relevant data as shown below:

1. Create the Database:
CREATE DATABASE IF NOT EXISTS Little_Italy;

2. Use the Database:
USE Little_Italy;

3. Create the Customers Table:
CREATE TABLE Customers (
    CustomerID INT NOT NULL PRIMARY KEY, 
    FullName VARCHAR(100) NOT NULL, 
    PhoneNumber INT NOT NULL UNIQUE
);

Populate the Customers Table:
   
   
INSERT INTO Customers (CustomerID, FullName, PhoneNumber) VALUES
(1, "Sumit Jade", 0757536378), 
(2, "Yogesh Ganar", 0757536379), 
(3, "Ashish Donode", 0757536376), 
(4, "Gaurav Dotonade", 0757536375), 
(5, "Chandan Majumdar", 0757536374),     
(6, "Karanjeet Patel", 0757636378),      
(7, "Sakshi Sarode", 0753536379),      
(8, "Chetan Ingole", 0754536376),      
(9, "Vishal Bais", 0757236375),     
(10, "Sajit Pathan", 0757936374);


4. Create the Bookings Table:
CREATE TABLE Bookings (
    BookingID INT, 
    BookingDate DATE, 
    TableNumber INT, 
    NumberOfGuests INT,
    CustomerID INT
);

Populate the Bookings Table:   
INSERT INTO Bookings (BookingID, BookingDate, TableNumber, NumberOfGuests, CustomerID) VALUES
(10, '2024-11-10', 7, 5, 1),  
(11, '2024-11-10', 5, 2, 2),  
(12, '2024-11-10', 3, 2, 4), 
(13, '2024-11-11', 2, 5, 5),  
(14, '2024-11-11', 5, 2, 6),  
(15, '2024-11-11', 3, 2, 7), 
(16, '2024-11-11', 3, 5, 1),  
(17, '2024-11-12', 5, 2, 2),  
(18, '2024-11-12', 3, 2, 4), 
(19, '2024-11-13', 7, 5, 6),  
(20, '2024-11-14', 5, 2, 3),  
(21, '2024-11-14', 3, 2, 4);


5. Create the Courses Table:
CREATE TABLE Courses (
    CourseName VARCHAR(255) PRIMARY KEY, 
    Cost DECIMAL(4,2)
);

Populate the Courses Table:
INSERT INTO Courses (CourseName, Cost) VALUES
("Greek Salad", 15.50), 
("Bean Soup", 12.25), 
("Pizza", 15.00), 
("Carbonara", 12.50), 
("Kabsa", 17.00), 
("Shwarma", 11.30);




Task Instructions:

Task 1: Filter Data with WHERE Clause:
Retrieve records from the Bookings table for booking dates between 2024-11-11 and 2024-11-13.
 
SELECT * 
FROM Bookings 
WHERE BookingDate BETWEEN '2024-11-11' AND '2024-11-13';


Task 2: Create a JOIN Query:
Retrieve the full names of customers and their booking IDs for bookings on 2024-11-11.

SELECT Customers.FullName, Bookings.BookingID 
FROM Customers 
JOIN Bookings ON Customers.CustomerID = Bookings.CustomerID 
WHERE BookingDate = '2024-11-11';


Task 3: Create a GROUP BY Query:
Show booking dates and the total number of bookings for each date.

SELECT BookingDate, COUNT(*) AS TotalBookings 
FROM Bookings 
GROUP BY BookingDate;


Task 4: Update with REPLACE:
Update the cost of Kabsa from $17.00 to $20.00.

REPLACE INTO Courses (CourseName, Cost) VALUES
("Kabsa", 20.00);


Task 5: Create a New Table with Constraints:
Create a DeliveryAddress table with specific constraints.

CREATE TABLE DeliveryAddress (
    ID INT PRIMARY KEY,
    Address VARCHAR(255) NOT NULL,
    Type VARCHAR(50) NOT NULL DEFAULT "Private",
    CustomerID INT NOT NULL,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);


Task 6: Alter Table Structure:

Add a new column Ingredients to the Courses table.
   
ALTER TABLE Courses 
ADD Ingredients VARCHAR(255);


Task 7: Create a Subquery:
Retrieve the full names of customers who made bookings on 2024-11-11.
   
SELECT FullName 
FROM Customers 
WHERE CustomerID IN (
    SELECT CustomerID 
    FROM Bookings 
    WHERE BookingDate = '2024-11-11'
);


Task 8: Create a Virtual Table:
Create a view BookingsView for bookings before 2024-11-13 with more than 3 guests.
   
CREATE VIEW BookingsView AS
SELECT BookingID, BookingDate, NumberOfGuests 
FROM Bookings 
WHERE BookingDate < '2024-11-13' AND NumberOfGuests > 3;


Task 9: Create a Stored Procedure:
Create a stored procedure to retrieve bookings data based on an input date.

CREATE PROCEDURE GetBookingsData (IN InputDate DATE)
BEGIN
    SELECT * 
    FROM Bookings 
    WHERE BookingDate = InputDate;


CALL GetBookingsData('2024-11-13');


Task 10: Use a String Function:
List booking details in a formatted string.

SELECT 
    CONCAT("ID: ", BookingID, ", Date: ", BookingDate, ", Number of guests: ", NumberOfGuests) AS BookingDetails 
FROM Bookings;

