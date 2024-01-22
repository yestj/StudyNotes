##  **Stored Procedure**

\- A set of SQL statements that are stored on the server and can be executed as a single unit

\- Precompiled and stored in the database, allowing for improved performance and code reusability

#### **Procedure Declaration**

\- A stored procedure is defined using the 'CREATE PROCEURE' statement

\- Includes the procedure name, parameters(if any), and the body of the procedure

```
/* Basic sysntax */
CREATE PROCEDURE procedure_name (parameter1 datatype, parameter2 datatype)
BEGIN
	-- SQL statements to perform the task
END;
```

#### **Parameters**

\- IN Parameters : Pass values into the stored procedure

```
CREATE PROCEDURE example_procedure(IN param1 INT, IN param2 VARCHAR(255))
BEGIN
    -- SQL statements using param1 and param2 as input
END;
```

  
\- OUT Parameters : Return values from the stored procedure to the calling environment

```
CREATE PROCEDURE example_procedure(OUT result INT)
BEGIN
    -- SQL statements to calculate result
    SET result = some_calculation_result;
END;
```

```
CALL example_procedure(@output_result);
SELECT @output_result AS Result;
```

\- INOUT Parameters : Pass values into the procedure and also return modified values to the calling environment

```
CREATE PROCEDURE example_procedure(INOUT inout_param INT)
BEGIN
    -- SQL statements using inout_param as both input and output
    SET inout_param = inout_param * 2;
END;
```

```
CALL example_procedure(@input_output_param);
SELECT @input_output_param AS ModifiedResult;
```

#### **Procedure Body**

\- SQL statements that perform the desired task (between 'BEGIN' and 'END' keywords

#### **Executing the Procedure**

\- Execute using the 'CALL' statement

```
CALL procedure_name(parameter1_value, parameter2_value);
```

### **Stored Procedure VS Stored Function**

| Feature | Stored Procedure | Stored Function |
| --- | --- | --- |
| CREATE Syntax | CREATE PROCEDURE... | CREATE FUNCTION... |
| Parameters | Can have IN, OUT, INOUT parameters | Can have IN parameters |
| Return Type | Does not require a return type | Must have a return type(e.g., INT, etc.) |
| RETURN Statement | Does not use the 'RETURN' of values | Uses the 'RETURN' to return a value |
| Call from   SQL statement | Typically called using the CALL statement | Can be used in SQL statements(SELECT, etc.) |
| Transaction   Control | Support | Does not support |
| Common   Use Cases | Business logic   (transaction control, complex operations) | Computation   (calculation, data transformation) |
