# IFest Event Management System

## Project Overview
The IFest Event Management System is a database-driven application designed to manage technical festival events efficiently. It handles participants, teams, registrations, payments, certificates, feedback, and event coordination.

The system is built using PostgreSQL for database management and Java (JDBC) for backend connectivity.

---

## Features
- Participant and Team Management
- Event Creation and Scheduling
- Registration System
- Payment Tracking
- Certificate and Prize Management
- Feedback System
- Inventory and Milestone Tracking
- Judge and Sponsor Management
- 40+ SQL Queries for data analysis

---

## Technologies Used
- PostgreSQL (Database)
- Java (JDBC)
- SQL (DDL, DML, Queries)
- Java Swing (Frontend)
- VS Code (IDE)

---

## Database Design
The database is designed using:
- Entity Relationship Diagram (ERD)
- Relational Model
- Normalization up to 3NF/BCNF

### Main Entities
- Participants
- Teams
- Events
- Registration
- Payment
- Certificates
- Prizes
- Judges
- Sponsors
- Coordinators
- Inventory
- Milestones
- Feedback

---

## Normalization
- First Normal Form (1NF): Ensured atomic attributes
- Second Normal Form (2NF): Removed partial dependencies
- Third Normal Form (3NF): Removed transitive dependencies

---

## Database Schema
The system includes tables such as:
- Participants
- Teams
- Events
- Registration
- Payment
- Certificates
- Certificate_Type
- Prizes
- Judges
- Event_Judges
- Sponsors
- Coordinators
- Inventory
- Milestones
- Feedback
- Address

---

## Setup Instructions

### 1. Clone Repository
```bash
git clone https://github.com/your-username/ifest-event-management.git
cd ifest-event-management
```

### 2. Setup PostgreSQL Database
- Install PostgreSQL
- Create a database:
```sql
CREATE DATABASE IFest_Event_Management;
```

- Run the DDL scripts provided in the project to create tables

---

### 3. Configure Database Connection
Update the database credentials in `DBConnection.java`:

```java
private static final String URL = "jdbc:postgresql://localhost:5432/IFest_Event_Management";
private static final String USER = "postgres";
private static final String PASSWORD = "your_password";
```

---

### 4. Run the Application
Compile and run Java files:

```bash
javac DBConnection.java
javac TeamCRUD.java
java TeamCRUD
```

---

## CRUD Operations
The system supports:
- Insert Team
- View Teams
- Update Team
- Delete Team

Implemented using:
- PreparedStatement
- JDBC Connection

---

## Sample Queries
Examples:
```sql
-- List all participants
SELECT * FROM Participants;

-- Show all events
SELECT Event_Name, Date, Time FROM Events;

-- Find pending payments
SELECT * FROM Payment WHERE Payment_Status = 'Pending';
```

---

## Trigger Example
Automatically updates payment status when proof is uploaded:

```sql
CREATE OR REPLACE FUNCTION update_payment_status()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.Payment_Proof IS NOT NULL THEN
        NEW.Payment_Status := 'Completed';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_update_payment_status
BEFORE INSERT OR UPDATE ON Payment
FOR EACH ROW
EXECUTE FUNCTION update_payment_status();
```

---

## Challenges Faced
- JDBC driver configuration issues
- Database connection errors
- Handling SQL exceptions

---

## Learning Outcomes
- Understanding ERD and relational modeling
- Database normalization (1NF to 3NF)
- Writing complex SQL queries
- JDBC connectivity with PostgreSQL
- CRUD operations using Java

---

## References
- PostgreSQL Official Documentation
- Java JDBC Documentation
- GeeksforGeeks JDBC Tutorials
- Oracle Java Swing Tutorials
- IFest DA-IICT Website

---

## Author
Developed as part of a Database Management System project.
