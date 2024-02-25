## **Concurrency Control**

When multiple transactions are processed simultaneously in a single DBMS, the utilization of processors and disks increases, leading to an increase in throughput (the number of transactions processed per unit time), and there is a benefit of reduced response time as shorter transactions do not need to wait for other transactions. However, because multiple transactions are executed concurrently, there may be unexpected results depending on the order in which operations within each transaction are performed. To prevent this, the DBMS must establish methods to **control concurrency** to ensure the independence and accuracy of each transaction, with **transaction scheduling** being a prominent method.

### **Schedule**

A series of operations from one or more transactions

#### **1\. Serial Schedule**

\- Transactions are executed sequentially, with no overlap in their execution  
\- Each transaction completes before the next one begins

#### **2\. Concurrent Schedule**

\- Multiple transactions are active and executing simultaneously, with their operaions interleaved

\- Allows for increased throughput and reduced response time  

### **Serializability**

When two or more transactions are performed, the simplest way to achieve correct results is to adopt a Serial schedule. However, to improve the efficiency of transaction processing, DBMS adopts Concurrent schedule. Among Concurrent schedules, DBMS selects **Serializable schedules** to ensure consistency in the database. Serializability refers to the property of a schedule being convertible into a serial schedule, meaning it is serializable when there exists a serial schedule with the same results.

Serializability is based on the assumption that all transactions and Serial schedules guarantee database consistency. Therefore, Serializable schedules also ensure database consistency, making it acceptable for DBMS to select these schedules.

| **Aspect** | **Serial Schedule** | **Serializable Schedule** |
| --- | --- | --- |
| Execution | Executed sequentially, one after another | May be executed concurrently |
| Overlap | No overlap in transaction execution | May overlap in time |
| Consistency | Simple, but may lead to reduced performance | Ensures consistency and prevents anomalies |
| Performance | May have reduced performance due to   sequential execution | Allows for concurrent execution,   enhancing performance |
| Properties | No concurrency, easy to understand | Maintains illusion of sequential execution, prevents anomalies |
| ACID compliance | Executed one after another | Allows for concurrency while ensuring ACID properties |

#### **Conflict**

To determine whether a schedule is serializable, we check if there are any conflicts (collisions) in the current schedule. A conflict occurs when the order of operations between two different transactions affects the outcome of the entire schedule. In other words, if the order of operations between the conflicting transactions changes, the outcome of the entire schedule changes as well. Conflicts typically arise when different transactions access the same data simultaneously.

#### **Conflict Equivalent**

Two schedules are considered conflict equivalent if they generate the same set of conflicts between transactions. In other words, if the same transactions are involved in conflicts, and the conflicts occur in the same order in both schedules, then they are conflict equivalent.

Formally, two schedules S1 and S2 are conflict equivalent if:

1.  They involve the same set of transactions
2.  The conflicts between transactions (read-write and write-write conflicts) occur in the same order in both schedules

#### **Conflict Serializable**

A schedule is conflict serializable if it is equivalent to a serial schedule regarding its conflict order. In other words, a schedule is conflict serializable if its execution order can be rearranged into a serial order without changing the conflicts between transactions.

Formally, a schedule S is conflict serializable if there exists a serial schedule S' (i.e., a schedule where transactions are executed one after another without overlap) such that:

1.  The set of transactions in S' is the same as the set of transactions in S.
2.  The order of conflicts (read-write and write-write conflicts) between transactions in S' is the same as the order of conflicts in S.

### **Recoverability**

In actual database environments, transactions may fail for various reasons. In such cases, the DBMS needs to recover the database to its state before the transaction began. When multiple transactions are executed concurrently, ensuring successful recovery may not be straightforward. Therefore, to address this, the DBMS needs to schedule transactions to be recoverable.

#### **Recoverable Schedule**

**A recoverable schedule** ensures that if a transaction reads data that has been written by another transaction, the writing transaction must commit before the reading transaction does. This prevents the possibility of "dirty reads," where a transaction reads uncommitted data from another transaction.

#### **Cascadeless Schedule**

**Cascading rollback**  
A phenomenon in database systems where the rollback of one transaction results in the rollback of other transactions that have read uncommitted data modified by the first transaction. This cascade effect occurs because the uncommitted data read by subsequent transactions becomes invalid or inconsistent once the originating transaction is rolled back. Cascading rollback can lead to data inconsistency and performance issues, making it essential for database systems to employ concurrency control mechanisms to prevent this phenomenon.

**A cascadeless schedule** ensures that if one transaction writes data that another transaction reads, the writing transaction must commit before the reading transaction does. This prevents the propagation of undesired effects caused by the cascading rollback of transactions.

#### **Strict Schedule**

**A strict schedule** ensures that a transaction can only read a data item after all preceding write operations on that item have been committed. This prevents non-repeatable reads and phantom reads by enforcing a strict ordering between read and write operations.
