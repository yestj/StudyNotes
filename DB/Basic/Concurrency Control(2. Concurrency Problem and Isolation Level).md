## **Concurrency Problem and Isolation Level**

### **Concurrency Problem**

Concurrency problems occur when multiple transactions are being executed on the same database in unrestricted problems.

| **Concurrency Problem** | **Description** |
| --- | --- |
| **Lost Update** | Occurs when two transactions try to update the same data concurrently, pontentially resulting in one transaction's changes being overwritten by the other |
| **Dirty Read** | Happens when a transaction data that has been modified by another uncommitted transaction, leading to inconsistent or invalid data being read |
| **Non-Repeatable Read** | Arises when a transaction reads the same data multiple times, but the data values change between reads due to concurrent modifications by other transactions |
| **Phantom Read** | Occurs when a transaction reads a set of records that satisfy a certain condition, but other concurrent transactions insert or delete records, causing inconsistency |

### **Isolation Level (Standard SQL 92)**

Developers can choose the isolation level based on how much they want to tolerate such concurrency problems. Isolation levels are used to control concurrency issues that may arise when multiple transactions are executed simultaneously. There are various isolation levels, each providing different levels of data consistency and concurrency control.

| **Isolation Level** | **Description** |
| --- | --- |
| Read uncommitted | Allows transactions to read data that has been modified by other transactions but not yet committed. This level provides the lowest degree of isolation and offers minimal data consistency guarantees. |
| Read committed | Transactions can only read data that has been committed by other transactions. This level prevents dirty reads but still allows non-repeatable reads and phantom reads. It offers a moderate level of isolation and data consistency. |
| Repetable read | Guarantees that once a data item is read, it remains unchanged for the duration of the transaction. This level prevents dirty reads and non-repeatable reads but may still allow phantom reads. It offers a higher level of isolation. |
| Serializable | Provides the strictest isolation level, ensuring that transactions execute as if they were running sequentially, one after another. This level prevents all concurrency anomalies, including dirty reads, non-repeatable reads, and phantom reads. |

| **Isolation Level** | **Dirty Read** | **Non-repeatable Read** | **Phantom Read** |
| --- | --- | --- | --- |
| Read uncommitted | O | O | O |
| Read committed | X | O | O |
| Repeatable read | X | X | O |
| Serializable | X | X | X |

### **A Critique of ANSI SQL Isolation Level**

In addition to the concurrency problems mentioned earlier, such as lost updates, dirty reads, non-repeatable reads, and phantom reads, there are indeed more issues that can arise in concurrent database environments.

| **Concurrency Problem** | **Description** |
| --- | --- |
| **Dirty Write** | Occurs when two transactions concurrently attempt to modify the same data item, and both transactions commit their changes without being aware of each other's modifications. |
| **Write Skew** | Happens when two transactions concurrently modify related but distinct data items, leading to an inconsistent state that would not have occurred if the transactions had been executed serially. |
| **Read Skew** | Occurs when a transaction reads multiple data items within a single query, and the data items become inconsistent due to concurrent modifications by other transactions between the reads. |
| **Phantom Write** | Refers to a situation where two transactions concurrently insert new data records into a database, and both transactions commit their insertions without being aware of each other's additions. |

### **Snapshot Isolation**

Snapshot isolation is an isolation level used in database systems to provide a consistent and concurrent view of data to transactions. It ensures that each transaction sees a consistent snapshot of the database as of the beginning of the transaction, regardless of any changes made by other transactions during its execution.

#### **Mechanism**

1.  **Versioning**: The database system maintains multiple versions of data items to support snapshot isolation. When a transaction modifies a data item, instead of overwriting the existing value, the system creates a new version of the data item with the updated value. This version includes a timestamp or a transaction identifier to indicate when the modification occurred.
2.  **Read Consistency**: When a transaction begins, it is assigned a consistent snapshot of the database state. This snapshot includes all committed changes up to that point in time but excludes changes made by concurrent transactions after the transaction started. The transaction can read from this consistent snapshot without being affected by concurrent modifications made by other transactions.
3.  **Write Operations**: When a transaction performs a write operation, it updates data items as usual. However, instead of immediately overwriting the existing versions of the data items, the system creates new versions with the updated values. This ensures that other transactions can still access the previous versions of the data items according to their consistent snapshots.
4.  **Concurrency Control**: Snapshot isolation relies on concurrency control mechanisms to ensure that transactions can execute concurrently without interfering with each other's operations. Techniques such as multi-version concurrency control (MVCC) are commonly used to manage the visibility of data versions and prevent conflicts between transactions.
5.  **Visibility Rules**: Transactions executing under snapshot isolation adhere to specific visibility rules to ensure a consistent snapshot view of the database. These rules dictate that a transaction can only see changes made by other transactions if those changes were committed before the start of the current transaction. Changes made by concurrent transactions during the execution of the current transaction are not visible to it, preserving data consistency.
6.  **Commitment and Rollback**: Once a transaction completes its operations, it can either commit or rollback its changes. If the transaction commits, its modifications become visible to other transactions, and the database system marks the transaction as complete. If the transaction rolls back, its changes are discarded, and the database reverts to its previous state.
