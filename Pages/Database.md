# Database

## Criteria for Acceptance:

- Simple to use
- Acceptable query speed


## Deciding for a data storage solution

While researching the possible database solutions for YAAC it became apparent that there are compromises with every solution.

### Why not full DBMS

Using a full Database Management System could make data management efficient and offers great performance and extensibility but such systems would need to be installed on the machine and initialized they can not easily be packaged. Requiring no additional setup and possibly only one executable should remain the focus.

### SQLite

SQLite is supported in GO and provides an minimal relational database which could be packaged together with the rest of YAAC. It is still performant and offers many functions and extensibility. It also supports saving binary data directly which can be used to store images up to 1GB per default.

---

## Important information for database security

For faster execution and security against SQL-Injection attacks it is crucial to use prepared statements wherever user input is parsed to an SQL statement. Prepared statements save resources and accept input variables only as values not as part of the sql statement. Usage is described here: Using prepared statements

## Database definition and model

The [Database ERM](/Diagrams/Database/DB-Entwurf.png) shows a high level overview planned out with everyone involved. It defines all tables and their relation needed for the basic program and leaves expandability.

Data dictionary

- Student:
    StudentId: INTEGER PRIMARY KEY
    LName: VARCHAR(50) NOT NULL
    FName: VARCHAR(50) NOT NULL
    StatusOfMatriculation: BOOLEAN Default=True NOT NULL
    Course: VARCHAR(12) NOT NULL

- AttendanceList:
    ListId: INTEGER PRIMARY KEY
    List: BLOB NOT NULL
    Date: TEXT Default=datetime() NOT NULL
    Course: VARCHAR(12) NOT NULL

Attendance:
    Date: DATE Default=date() PRIMARY KEY
    StudentId: INTEGER REFERENCES Student (StudentId) PRIMARY KEY
    Attending: BOOLEAN Default=False NOT NULL

Date is not a known type to sqlite but is can be represented as text in ISO8601 strings ("YYYY-MM-DD HH:MM:SS.SSS"). And build-in functions can produce such strings.