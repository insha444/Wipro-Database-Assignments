# Assignment 1 – Database Normalization

**Name:** Insha Shahnawaz  
**Enrollment No:** LNCDBTC21007  
**PBLApp ID:** DB_261370065

---


# Question 1: Normalize the following table into First Normal Form (1NF)

## Original Table

| Member_ID | First_Name | Last_Name | Hobbies |
|------------|------------|-----------|----------|
| 101 | Jayson | Mark | Cricket, Swimming, Football |
| 102 | Ram | Ganesh | Swimming, Running, Music |
| 103 | Raj | Kishore | Dancing, Singing, Running |

## Explanation

The **Hobbies** column contains multiple values in a single attribute. According to 1NF, each field should contain only one value.

## 1NF Table

| Member_ID | First_Name | Last_Name | Hobby |
|------------|------------|-----------|--------|
| 101 | Jayson | Mark | Cricket |
| 101 | Jayson | Mark | Swimming |
| 101 | Jayson | Mark | Football |
| 102 | Ram | Ganesh | Swimming |
| 102 | Ram | Ganesh | Running |
| 102 | Ram | Ganesh | Music |
| 103 | Raj | Kishore | Dancing |
| 103 | Raj | Kishore | Singing |
| 103 | Raj | Kishore | Running |

---

# Question 2: Normalize the following table into Second Normal Form (2NF)

## Original Table

| Empno | Training | Training_Date | Dept |
|--------|-----------|---------------|------|
| 101 | Oracle SQL | 12-Aug-2015 | TT |
| 101 | Java | 21-Aug-2015 | BU |
| 102 | Oracle SQL | 18-Sep-2014 | TT |

## Explanation

Assume the composite key is:

**(Empno, Training)**

Functional Dependencies:

- (Empno, Training) → Training_Date
- Empno → Dept

Since **Dept** depends only on **Empno** and not on the entire composite key, a partial dependency exists.

To achieve 2NF, we decompose the table.

## Employee Table

| Empno | Dept |
|--------|------|
| 101 | TT |
| 102 | TT |

## Training Table

| Empno | Training |
|--------|-----------|
| 101 | Oracle SQL |
| 101 | Java |
| 102 | Oracle SQL |

## Training Details Table

| Empno | Training | Training_Date |
|--------|-----------|---------------|
| 101 | Oracle SQL | 12-Aug-2015 |
| 101 | Java | 21-Aug-2015 |
| 102 | Oracle SQL | 18-Sep-2014 |

---

# Question 3: Normalize the following table into Third Normal Form (3NF)

## Original Table

| Member_ID | First_Name | Last_Name | Sports | Fees |
|------------|------------|-----------|--------|------|
| 101 | Rajesh | Chand | Cricket | 100 |
| 102 | Jayesh | Raj | Hockey | 80 |
| 103 | Mark | Dorson | Football | 90 |

## Explanation

Functional Dependencies:

- Member_ID → First_Name, Last_Name, Sports
- Sports → Fees

Therefore:

Member_ID → Sports → Fees

This creates a **transitive dependency**.

To achieve 3NF, separate the Sports and Fees information into another table.

## Member Table

| Member_ID | First_Name | Last_Name | Sports |
|------------|------------|-----------|---------|
| 101 | Rajesh | Chand | Cricket |
| 102 | Jayesh | Raj | Hockey |
| 103 | Mark | Dorson | Football |

## Sports Fees Table

| Sports | Fees |
|---------|------|
| Cricket | 100 |
| Hockey | 80 |
| Football | 90 |

---
