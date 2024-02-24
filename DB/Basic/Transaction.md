## **Transaction**

: A logical unit of work in a database that consists of one or more operations performed on the database

### **ACID**

#### **1\. Atomicity**

\- Transactions are all-or-nothing

\- Ensures that all operations within a transaction are completed successfully, or none of them are

\- If any part fails, the entire transaction is rolled back

#### **2\. Consistency**

\- Maintains the database in a valid state before and after the transaction  
\- Integrity constraints must be enforced, ensuring that the database remains consistent with defined rules

\- If any constraints, triggers violate the rules of the database, the entire trasaction is rolled back

(ex. If a transaction results in a negative balance, violating the constraints that the account balance must be at least 0, the transaction must be rolled back)

#### **3\. Isolation**

\- Ensures that concurrent transactions do not interfere with each other  
\- Each transaction operates independently, preventing issues like dirty reads, non-repeatable reads, and phantom reads

#### **4\. Durability**

\- Guarantees that committed transactions are permanent and survive system failures  
\- Committed changes are stored in non-volatile storage and should not be lost, even in the event of crashes or restarts

### **A sequence of transaction**

\- Autocommit is a default option in many DBMS, every SQL statement is treated as a single transaction, and it is automatically committed immediately after execution

\- If you want to manipulate transactions: 

#### **in MYSQL**

```
-- BEGIN TRANSACTION
START TRANSACTION;

-- EXECUTE OPERATIONS 
UPDATE ~

-- COMMIT OR ROLLBACK
COMMIT; -- or ROLLBACK;

-- END TRANSACTION
```

#### **in JAVA**

```
public void function(String value) {
  try {
    Connection connection = ...;		// get DB connection 
    connection.setAutoCommit(false);	// START TRANSACTION
    ...
    ...
  } catch (Exception e) {
    ...
    connection.roolback();
    ...
  } finally {
    connection.setAutoCommit(true);		// back to autocommit
  }
}
```
