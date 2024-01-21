## **Stored Function**

\- A set of SQL statements that perform a specific task and return a single value

\- Allow to encapsulate a series of SQL statements into a reusable and modular unit

```
DELIMITER // -- change DELIMITER ";" to "//" temporarily

CREATE FUNCTION calculate_area(length DOUBLE, width DOUBLE) RETURNS DOUBLE
BEGIN
    DECLARE area DOUBLE;
    SET area = length * width;
    RETURN area;
END
//

DELIMITER ; -- back to original delimiter
```

#### **DELIMITER**

\- Statement used to change the statement terminator temporarily  
\- Helps defining stored functions or procedures without interference from the default statement terminator(;) used by the MySQL command-line client

#### **CREATE FUNCTION**

\- Statement used to define a new stored function  
\- function\_name : name of function that you are creating (calculate\_area is function name in above example)

\- parameters : Variables that can use within the function and each parameter has a name and a data type

#### **RETURNS return\_datatype**

\- The data type of the value that the function will return

\- If function doesnt' return a value, use 'RETURNS VOID' or omit the 'RETURNS' clause

#### **BEGIN...END**

\- The body of the function

\- SQL statements that perform the desired task between these keywords

#### **RETURN expression**

\- Statement used to return a value from the function

#### **DECLARE**

\- Statement used to declare variables within a stored function  
\- Variables can be used to store and manipulate data within the scope of the stored function

\- The '@' symbol is used to denote declared variable
