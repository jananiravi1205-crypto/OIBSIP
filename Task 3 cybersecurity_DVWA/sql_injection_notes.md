SQL Injection — Testing Notes

1. Introduction

This document records the SQL Injection tests performed on Damn Vulnerable Web Application (DVWA).

The testing was performed only on DVWA running locally on my own computer. DVWA is intentionally designed to contain security vulnerabilities for educational and security-testing purposes.

DVWA Security Level: Low
Testing Environment: Localhost
Module: SQL Injection

---

2. Purpose of the Testing

The purpose of this exercise was to:

- Understand how SQL Injection works.
- Test how unsafe user input can affect an SQL query.
- Observe the information returned by the vulnerable application.
- Test different SQL Injection inputs.
- Understand why the vulnerability occurs.
- Learn how developers can prevent SQL Injection.

---

3. Testing Environment

Item| Details
Application| DVWA
Security Level| Low
Server| XAMPP / Local Server
Database| MySQL/MariaDB
Browser| Web Browser
Testing Location| Localhost
Module| SQL Injection

---

4. Test Case 1

Input Used

' OR '1'='1

Purpose

The purpose of this test was to determine whether the application directly inserts user input into an SQL query without properly separating the input from the SQL statement.

Observation

The application returned multiple user records instead of restricting the result to one particular user ID.

The condition:

'1'='1'

is logically true.

Because the application is intentionally vulnerable at the Low security level, the supplied input changes the logic of the database query.

Result

Vulnerable — Multiple records were returned.

Screenshot

![SQL Injection Test 1](screenshots/sql-injection-test1.png)

---

5. Test Case 2

Input Used

' OR 1=1 #

Purpose

This test was performed to verify the SQL Injection behavior using a different input.

Observation

The "OR 1=1" condition evaluates to true.

The "#" character is treated as a comment in MySQL/MariaDB, so the remaining part of the SQL statement can be ignored.

As a result, the application returned multiple records from the database.

Result

Vulnerable — Multiple records were returned.

Screenshot

![SQL Injection Test 2](screenshots/sql-injection-test2.png)

---

6. Test Results Summary

Test| Input| Result| Status
1| "' OR '1'='1"| Multiple records displayed| Vulnerable
2| "' OR 1=1 #"| Multiple records displayed| Vulnerable

---

7. What Data Was Exposed?

The SQL Injection tests caused the application to return information from the local DVWA users database.

The displayed information can include fields such as:

- User ID
- First name
- Last name
- Username or other fields displayed by DVWA

The exact output depends on the records stored in the local DVWA database.

The important finding is that the application allowed the database query to be manipulated through user input.

---

8. Why Did the Injection Work?

The vulnerability exists because the application does not properly separate SQL code from user input when the security level is set to Low.

A simplified vulnerable query can be represented as:

SELECT first_name, last_name
FROM users
WHERE user_id = '$id';

Normally, "$id" should contain only a user ID.

However, when specially crafted input is inserted directly into the query, it can change the SQL condition.

For example, a condition such as:

1 = 1

is always true.

Therefore, the database may return records that were not intended by the original query.

---

9. Root Cause

The main causes of the vulnerability are:

1. User input is directly included in an SQL query.
2. The application does not use parameterized queries.
3. The input is not properly separated from SQL commands.
4. The application is intentionally configured as vulnerable for educational purposes.

---

10. How to Prevent SQL Injection

The most important defense is to use parameterized queries / prepared statements.

Instead of constructing SQL using string concatenation, the application should use a parameter placeholder.

Example:

SELECT first_name, last_name
FROM users
WHERE user_id = ?;

The user input is then supplied separately as a parameter.


