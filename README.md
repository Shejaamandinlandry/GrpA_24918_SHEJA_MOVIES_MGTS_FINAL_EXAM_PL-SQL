# GrpA_24918_SHEJA_MOVIES_MGTS_FINAL_EXAM_PL-SQL


Phase I: Problem Statement and Presentation
Project Title:
Movies Management System

Problem Definition:
In the contemporary entertainment landscape, cinema operators often face critical challenges in managing core operations such as movie scheduling, ticket bookings, and customer engagement. Traditional or semi-automated systems are prone to human error, inefficiencies, and data fragmentation, which adversely impact customer satisfaction and operational efficiency. These systems lack integration, making it difficult to track show performance, monitor sales, or manage customer records in real-time.
The proposed Movies Management System seeks to eliminate these inefficiencies by offering an integrated, PL/SQL-powered Oracle database solution that automates and streamlines theater operations.

Context:
This system is designed for deployment in modern cinema theaters—both single-screen and multiplex environments. It will be used by administrative staff for scheduling and operations management, by sales clerks for real-time ticket booking, and by customers for querying movie availability. The system is applicable in commercial cinema venues, educational institutions with film clubs, and even community screening hubs.

Target Users:
Cinema Administrators: Manage showtimes, theaters, pricing, and staff access.
Ticketing Staff: Perform bookings, issue tickets, and track attendance.
Customers: View movies, showtimes, and book seats online or at the counter.
Distributors/Film Agents: Manage the lifecycle of movies available for screening.
Project Goals:
Design a robust, normalized database model to manage complex cinema operations.
Automate core functionalities such as movie scheduling, ticket booking, and seat assignment.
Ensure data integrity, security, and real-time access through PL/SQL procedures and packages.
Enable the generation of comprehensive reports for decision-making (e.g., movie performance, peak hours).
Implement auditing and access control to monitor staff activity and ensure operational compliance
Presentation Slide Summary
Slide 1: Project Overview
Problem: Existing systems are fragmented, inefficient, and prone to errors.
Objectives:
Automate and streamline ticket sales and scheduling
Centralize data management
Improve decision-making with real-time analytics
Slide 2: Main Database Entities
Movie: ID, title, duration, genre, language, rating
Theater: ID, name, location, capacity
Show: ID, movie ID, theater ID, show datetime
Customer: ID, name, contact info, booking history
Ticket: ID, show ID, customer ID, seat number, price
Staff: ID, name, role, login credentials
Payment: ID, booking ID, amount, payment method, timestamp
Slide 3: Anticipated Benefits
Enhanced data accuracy and traceability
Real-time analytics for show optimization and pricing strategy

Improved user experience and reduced wait times
Scalable for future integration with mobile apps or third-party platforms

References
Oracle 21c XE Documentation: https://docs.oracle.com/en/database/oracle
AUCA Capstone Guidelines 2024–2025
INSY 8311 Lecture Slides and Practical Labs

=========================================================================

Phase II: Business Process Modeling (MIS Perspective)
 Objective
To model a core business process within the system that supports decision-making and automation from a Management Information System (MIS) perspective. We'll use UML/BPMN with swimlanes to clearly show the roles and responsibilities of different entities.

 Selected Business Process: Ticket Booking and Confirmation Workflow
This process captures how a customer interacts with the system to view available shows and book a ticket, and how the system verifies availability, reserves the seat, records payment, and confirms booking.

📌Scope
This process begins when a customer views showtimes and ends when a booking confirmation is issued. It supports MIS goals by enabling:
Real-time decision-making (e.g., seat availability, pricing)
Automation of manual ticketing
Audit and reporting for sales tracking

👥Key Entities (Actors & Systems)
Actor/System	Role
Customer	Initiates ticket booking
Ticketing System	Validates availability, stores booking
Payment Processor	Handles payment validation
Theater Admin	Reviews booking logs, schedules shows

 Steps in the Process
1 .Customer
  
                        Selects movie, location, showtime
Chooses number of seats
Proceeds to payment
2. System (Booking Module)
Checks seat availability
Locks selected seats temporarily
Generates booking ID
3.Payment Gateway
Collects payment info
Confirms transaction
Sends confirmation or failure
4.System (Confirmation Module)
Finalizes booking
Updates seat status
Sends ticket with QR code/email

5.Theater Admin
Can access real-time reports
Uses data for daily analytics


 How It Supports MIS
Improves decision-making: Enables theater managers to adjust show timings or pricing based on booking trends.
Streamlines operations: Eliminates double-bookings and manual logs.
Enables reporting: Generates real-time dashboards for management (total tickets sold, revenue per show, etc.).
MIS Relevance:
This process improves the quality of information by integrating booking, payments, and reporting. It provides timely insights for theater managers and streamlines the ticketing workflow, thus improving operational efficiency and customer satisfaction.
IMAGE THAT SHOW IT CLEARY
===============================================================================================================================================================================

Phase III: Logical Model Design
This phase is about building a well-normalized, relational database structure with appropriate entities, attributes, relationships, and constraints, aligned with the business process you modeled in Phase II.

 Objectives:
Create an Entity-Relationship (ER) Model
Define relationships and constraints
Normalize the schema (up to 3NF)
Ensure data integrity and realistic data scenarios

 Step1:Identify Entities and Attributes
Entity	Attributes (with data types)
Movie	movie_id (PK), title, genre, duration, language, rating
Theater	theater_id (PK), name, location, total_seats
Show	show_id (PK), movie_id (FK), theater_id (FK), show_time
Customer	customer_id (PK), full_name, email, phone
Ticket	ticket_id (PK), show_id (FK), customer_id (FK), seat_number, price
Staff	staff_id (PK), name, role, username, password
Payment	payment_id (PK), ticket_id (FK), amount, payment_method, payment_date

 Step2:Define Relationships and Constraints
Movie ↔ Show: One-to-Many (A movie can have many shows)
Theater ↔ Show: One-to-Many (A theater can host many shows)
Show ↔ Ticket: One-to-Many (Each show has multiple tickets)
Customer ↔ Ticket: One-to-Many (A customer can buy multiple tickets)
Ticket ↔ Payment: One-to-One (Each ticket has a payment)
Staff is standalone for admin purposes (used in auditing, Phase VII)
Constraints:
Primary Keys: Defined for all tables
Foreign Keys: Enforce referential integrity
NOT NULL: On essential fields (e.g., movie title, seat number)
UNIQUE: On seat_number within the same show
CHECK: On ticket price (> 0)
DEFAULT: payment_method defaults to 'cash' if not provided

 Step 3: Normalization (up to 3NF)
Example: Movie and Show
1NF: All attributes have atomic values
2NF: No partial dependencies (e.g., show_time is only in Show, not in Movie)
3NF: No transitive dependencies (e.g., theater location isn't dependent on movie ID)

🧾 Step 4: Data Scenarios
A customer books 2 tickets for 2 different shows.
A theater hosts 3 shows for different movies in one day.
Payment for each ticket is stored individually with method and timestamp.
Tickets can't be issued for the same seat in a show.
RELATED IMAGE

==============================================================================
Phase IV: Database Creation and Configuration
 Objective:
Create an Oracle Pluggable Database with the correct naming convention and set up Oracle Enterprise Manager (OEM) for monitoring.

 Step 1: Naming the Database
Follow the required format:
GrpName_StudentId_FirstName_ProjectName_DB
GrpA_24918_sheja_moviesMS_db
Password: 123

Step 2: Create the Database in Oracle (XE)
I use the following script( SQL Developer):

🧭 Step 3: Oracle Enterprise Manager (OEM)
Oracle XE comes with OEM (EM Express) which can be accessed at:
https://localhost:5500/em

=================================================================================

Phase V: Table Implementation and Data Insertion for your Movies Management System.
Objective
To convert the logical model into a physical Oracle database structure by creating tables, applying constraints, and inserting realistic sample data.

TABLES CREATION
-- MOVIE Table
CREATE TABLE movie (
    movie_id       NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    title          VARCHAR2(100) NOT NULL,
    genre          VARCHAR2(50),
    duration       NUMBER(3), -- in minutes
    language       VARCHAR2(30),
    rating         VARCHAR2(10)
);

-- THEATER Table
CREATE TABLE theater (
    theater_id     NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    name           VARCHAR2(100) NOT NULL,
    location       VARCHAR2(100),
    total_seats    NUMBER NOT NULL CHECK (total_seats > 0)
);

-- SHOW Table
CREATE TABLE showtime (
    show_id        NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    movie_id       NUMBER REFERENCES movie(movie_id),
    theater_id     NUMBER REFERENCES theater(theater_id),
    show_time      TIMESTAMP NOT NULL
);

-- CUSTOMER Table
CREATE TABLE customer (
    customer_id    NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    full_name      VARCHAR2(100) NOT NULL,
    email          VARCHAR2(100) UNIQUE,
    phone          VARCHAR2(15)
);

-- TICKET Table
CREATE TABLE ticket (
    ticket_id      NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    show_id        NUMBER REFERENCES showtime(show_id),
    customer_id    NUMBER REFERENCES customer(customer_id),
    seat_number    VARCHAR2(10) NOT NULL,
    price          NUMBER(6,2) NOT NULL CHECK (price > 0),
    UNIQUE (show_id, seat_number) -- Prevent double booking
);

-- PAYMENT Table
CREATE TABLE payment (
    payment_id     NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    ticket_id      NUMBER REFERENCES ticket(ticket_id),
    amount         NUMBER(6,2) NOT NULL,
    payment_method VARCHAR2(20) DEFAULT 'cash',
    payment_date   TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- STAFF Table
CREATE TABLE staff (
    staff_id       NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    name           VARCHAR2(100) NOT NULL,
    role           VARCHAR2(30),
    username       VARCHAR2(50) UNIQUE NOT NULL,
    password       VARCHAR2(100) NOT NULL
);


TABLE CREATED SUCCESSFULLY SCREENSHOTS





DATA INSERTION

-- Insert sample movies
INSERT INTO movie (title, genre, duration, language, rating) 
VALUES ('Inception', 'Sci-Fi', 148, 'English', 'PG-13');

INSERT INTO movie (title, genre, duration, language, rating) 
VALUES ('The Matrix', 'Action', 136, 'English', 'R');

-- Insert sample theaters
INSERT INTO theater (name, location, total_seats) 
VALUES ('Main Hall', 'Downtown', 120);

INSERT INTO theater (name, location, total_seats) 
VALUES ('Elite Screen', 'Uptown', 80);

-- Insert sample customers
INSERT INTO customer (full_name, email, phone) 
VALUES ('Alice Johnson', 'alice@gmail.com', '123456789');

INSERT INTO customer (full_name, email, phone) 
VALUES ('Bob Smith', 'bob@example.com', '987654321');

-- Insert sample shows
INSERT INTO showtime (movie_id, theater_id, show_time) 
VALUES (1, 1, TO_TIMESTAMP('2025-06-15 18:00', 'YYYY-MM-DD HH24:MI'));

INSERT INTO showtime (movie_id, theater_id, show_time) 
VALUES (2, 2, TO_TIMESTAMP('2025-06-15 20:30', 'YYYY-MM-DD HH24:MI'));

-- Insert sample tickets
INSERT INTO ticket (show_id, customer_id, seat_number, price) 
VALUES (1, 1, 'A10', 5000);

INSERT INTO ticket (show_id, customer_id, seat_number, price) 
VALUES (2, 2, 'B5', 5500);

-- Insert sample payments
INSERT INTO payment (ticket_id, amount, payment_method) 
VALUES (1, 5000, 'Mobile Money');

INSERT INTO payment (ticket_id, amount, payment_method) 
VALUES (2, 5500, 'Cash');





DATA INSERTED SUCCESSFULLY SCREENSHOTS



==========================================================================================

Phase VI: Database Interaction and Transactions for your Movies Management System.

Objective
You’ll write PL/SQL programs to interact with your database, focusing on:
DML/DDL operations
Cursors
Procedres and functions
Exception handling
Packages
Use of window functions for analytics

 1. Simple Problem Statement for Analytics
“Find out the top 3 most booked shows, based on the number of tickets sold.”

2. Create a Procedure to Fetch Booking Counts per Show

CREATE OR REPLACE PROCEDURE show_ticket_counts IS
BEGIN
    FOR rec IN (
        SELECT s.show_id, m.title, COUNT(*) AS tickets_sold
        FROM ticket t
        JOIN showtime s ON t.show_id = s.show_id
        JOIN movie m ON s.movie_id = m.movie_id
        GROUP BY s.show_id, m.title
        ORDER BY tickets_sold DESC
    ) LOOP
        DBMS_OUTPUT.PUT_LINE('Show: ' || rec.title || ' | Tickets Sold: ' || rec.tickets_sold);
    END LOOP;
END;
/


3. Function to Calculate Total Revenue for a Movie

CREATE OR REPLACE FUNCTION total_revenue_by_movie(p_movie_id NUMBER) RETURN NUMBER IS
    total NUMBER := 0;
BEGIN
    SELECT SUM(t.price)
    INTO total
    FROM ticket t
    JOIN showtime s ON t.show_id = s.show_id
    WHERE s.movie_id = p_movie_id;

    RETURN total;
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        RETURN 0;
    WHEN OTHERS THEN
        RETURN -1;
END;
/



4. Cursor Example: Loop Over Customers

DECLARE
    CURSOR c_customers IS
        SELECT full_name, email FROM customer;
BEGIN
    FOR rec IN c_customers LOOP
        DBMS_OUTPUT.PUT_LINE('Customer: ' || rec.full_name || ', Email: ' || rec.email);
    END LOOP;
END;
/


5. Error Handling Example

BEGIN
    INSERT INTO ticket (show_id, customer_id, seat_number, price)
    VALUES (999, 1, 'X1', 5000); -- 999 is a non-existent show_id
EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error inserting ticket: ' || SQLERRM);
END;
/

6. Create a Package for Show Analytics

CREATE OR REPLACE PACKAGE show_analytics AS
    PROCEDURE top_shows;
    FUNCTION revenue(movie_id NUMBER) RETURN NUMBER;
END show_analytics;
/



CREATE OR REPLACE PACKAGE BODY show_analytics AS
    PROCEDURE top_shows IS
    BEGIN
        FOR rec IN (
            SELECT s.show_id, m.title, COUNT(*) AS tickets_sold
            FROM ticket t
            JOIN showtime s ON t.show_id = s.show_id
            JOIN movie m ON s.movie_id = m.movie_id
            GROUP BY s.show_id, m.title
            ORDER BY tickets_sold DESC FETCH FIRST 3 ROWS ONLY
        ) LOOP
            DBMS_OUTPUT.PUT_LINE('Top Show: ' || rec.title || ' | Tickets Sold: ' || rec.tickets_sold);
        END LOOP;
    END;



    FUNCTION revenue(movie_id NUMBER) RETURN NUMBER IS
        total NUMBER;
    BEGIN
        SELECT SUM(price)
        INTO total
        FROM ticket t
        JOIN showtime s ON t.show_id = s.show_id
        WHERE s.movie_id = movie_id;

        RETURN total;
    EXCEPTION
        WHEN OTHERS THEN
            RETURN -1;
    END;
END show_analytics;
/

=================================================================================

Phase VII: Advanced Database Programming and Auditing
Project Name: Movies Management System
User Schema: GRPA_24918_SHEJA_MOVIESMS_DB

 Objective
The objective of Phase VII is to enhance security and auditing by restricting unauthorized changes to sensitive data (such as ticket records) and by recording all attempted changes. This includes:
Preventing ticket data changes during weekdays and blocked (holiday) dates
Logging every attempt (successful or denied) into an audit table

 Step 1: Create the Blocked Calendar Table
We define a list of dates when any ticket operations should be blocked. These represent public holidays or system-wide blocked days.
 SQL Query
sql
CopyEdit
CREATE TABLE blocked_calendar (
    block_date DATE PRIMARY KEY,
    reason     VARCHAR2(100)
);
 Sample Data
sql
CopyEdit
INSERT INTO blocked_calendar VALUES (TO_DATE('2025-06-17', 'YYYY-MM-DD'), 'Unity Day');INSERT INTO blocked_calendar VALUES (TO_DATE('2025-06-29', 'YYYY-MM-DD'), 'Independence Day');COMMIT;

 Step 2: Create the Audit Table
We log every INSERT, UPDATE, or DELETE attempt on the ticket table — whether it was allowed or blocked.
 SQL Query
sql
CopyEdit
CREATE TABLE ticket_audit (
    audit_id       NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    user_name      VARCHAR2(50),
    action_time    TIMESTAMP,
    operation_type VARCHAR2(10),
    status         VARCHAR2(10),
    message        VARCHAR2(200)
);




 Step 3: Create the Blocking and Logging Trigger
This trigger will:
Automatically run before any INSERT, UPDATE, or DELETE on ticket
Block operations on weekdays or blocked dates
Log the attempt with a message and user identity
 SQL Query
sql
CopyEdit
CREATE OR REPLACE TRIGGER trg_block_ticket_dml
BEFORE INSERT OR UPDATE OR DELETE ON ticketFOR EACH ROWDECLARE
    v_day_name    VARCHAR2(10);
    v_user        VARCHAR2(50);
    v_is_blocked  NUMBER := 0;
    v_operation   VARCHAR2(10);BEGIN
    SELECT TO_CHAR(SYSDATE, 'DAY'), USER
    INTO v_day_name, v_user
    FROM dual;

    SELECT COUNT(*) INTO v_is_blocked
    FROM blocked_calendar
    WHERE block_date = TRUNC(SYSDATE);

    IF INSERTING THEN
        v_operation := 'INSERT';
    ELSIF UPDATING THEN
        v_operation := 'UPDATE';
    ELSIF DELETING THEN
        v_operation := 'DELETE';
    END IF;

    IF v_day_name IN ('MONDAY   ', 'TUESDAY  ', 'WEDNESDAY', 'THURSDAY ', 'FRIDAY   ')
       OR v_is_blocked > 0 THEN

        INSERT INTO ticket_audit(user_name, action_time, operation_type, status, message)
        VALUES (
            v_user,
            CURRENT_TIMESTAMP,
            v_operation,
            'denied',
            'DML operation blocked due to weekday or blocked date.'
        );

        RAISE_APPLICATION_ERROR(-20001, 'DML operations are blocked on weekdays or blocked dates.');
    END IF;END;/



 Step 4: Testing and Validation
Positive Case
Test inserting a ticket on a non-blocked weekend:
sql
CopyEdit
INSERT INTO ticket (show_id, customer_id, seat_number, price)VALUES (1, 1, 'B1', 5000);


Expected Result: ✅ Success, and an entry is added in ticket_audit with status allowed.

 Negative Case
Test inserting a ticket on a blocked weekday or holiday:
sql
CopyEdit
-- This will fail if run on a blocked dateINSERT INTO ticket (show_id, customer_id, seat_number, price)VALUES (1, 2, 'B2', 5500);
Expected Result:  Error ORA-20001, and an entry is added to ticket_audit with status denied.

🔎 View Audit Log
To confirm the auditing works correctly:
sql
CopyEdit
SELECT * FROM ticket_audit ORDER BY action_time DESC;



 Summary
In this phase, we successfully:
Created a list of blocked operational dates
Implemented a trigger that blocks and logs any ticket data changes during those periods
Ensured that all changes are traceable by username, action, and status
Maintained all logic in the schema GRPA_24918_SHEJA_MOVIESMS_DB



