# Assignment 2 - SQL Mini Project

## Student Details
- Name: Insha Shahnawaz
- Enrollment No: LNCDBTC21007
- Email ID: inshashahnawaz444@gmail.com
- PBLApp ID: DB_261370065

## About
This assignment covers creating tables, inserting data, updating/deleting records,
and writing queries/views/synonyms/indexes as part of the Wipro TalentNext DBMS program.

## 1. Create Tables

\`\`\`sql
CREATE TABLE LEDGE_Details (
    Ledge_Name     VARCHAR2(20) PRIMARY KEY,
    Ledge_Manager  VARCHAR2(30),
    Ledge_Address  VARCHAR2(30) NOT NULL
);

CREATE TABLE EMP_Details (
    Empno       NUMBER PRIMARY KEY,
    First_Name  VARCHAR2(30) NOT NULL,
    Last_Name   VARCHAR2(30) NOT NULL,
    Ledge_Name  VARCHAR2(20),
    CONSTRAINT fk_emp_ledge FOREIGN KEY (Ledge_Name)
        REFERENCES LEDGE_Details(Ledge_Name)
);

CREATE TABLE BILL_Details (
    Bill        VARCHAR2(20) PRIMARY KEY,
    Bill_Class  VARCHAR2(20)
);

CREATE TABLE EMP_Bill (
    Empno   NUMBER,
    Bill    VARCHAR2(20),
    Grade   VARCHAR2(2),
    CONSTRAINT pk_emp_bill PRIMARY KEY (Empno, Bill),
    CONSTRAINT fk_eb_emp  FOREIGN KEY (Empno) REFERENCES EMP_Details(Empno),
    CONSTRAINT fk_eb_bill FOREIGN KEY (Bill)  REFERENCES BILL_Details(Bill)
);
\`\`\`

## 2. Insert Data

\`\`\`sql
INSERT INTO LEDGE_Details VALUES ('Jaasy Ledge',   'Rajen', 'Rajesh Nagar');
INSERT INTO LEDGE_Details VALUES ('Rajesh Ledge',  'Rajen', 'Silver Nagar');
INSERT INTO LEDGE_Details VALUES ('Basaley Ledge', 'John',  'Sea Road');

INSERT INTO EMP_Details VALUES (101, 'James',   'Jackson', 'Jaasy Ledge');
INSERT INTO EMP_Details VALUES (102, 'Gojesh',  'Raj',     'Rajesh Ledge');
INSERT INTO EMP_Details VALUES (103, 'Jasmine', 'Jay',     'Basaley Ledge');

INSERT INTO BILL_Details VALUES ('ClassSQL',  'Oracle Corporation');
INSERT INTO BILL_Details VALUES ('SQLClass',  'VII');
INSERT INTO BILL_Details VALUES ('SClass',    'EDP Corporation');

INSERT INTO EMP_Bill VALUES (101, 'ClassSQL', 'A');
INSERT INTO EMP_Bill VALUES (102, 'SQLClass', 'A');
INSERT INTO EMP_Bill VALUES (103, 'SClass',   'A');
\`\`\`

## 3. Updates / Deletes

\`\`\`sql
-- Employee 101 moved to Basaley Ledge
UPDATE EMP_Details SET Ledge_Name = 'Basaley Ledge' WHERE Empno = 101;

-- Employee 102 left the company
DELETE FROM EMP_Bill    WHERE Empno = 102;
DELETE FROM EMP_Details WHERE Empno = 102;
DELETE FROM LEDGE_Details WHERE Ledge_Name = 'Rajesh Ledge';
\`\`\`

## 4. HR Reports

\`\`\`sql
-- Empno, First_Name, Ledge_Name for every employee
SELECT Empno, First_Name, Ledge_Name FROM EMP_Details;

-- Empno, Grade, Ledge Manager
SELECT e.Empno, b.Grade, l.Ledge_Manager
FROM EMP_Details e
JOIN EMP_Bill b       ON e.Empno = b.Empno
JOIN LEDGE_Details l  ON e.Ledge_Name = l.Ledge_Name;

-- View: Employee_Ledge_Name
CREATE VIEW Employee_Ledge_Name AS
SELECT e.Empno, e.First_Name, e.Last_Name, e.Ledge_Name,
       l.Ledge_Manager, l.Ledge_Address
FROM EMP_Details e
JOIN LEDGE_Details l ON e.Ledge_Name = l.Ledge_Name;

-- Synonym EMP for
