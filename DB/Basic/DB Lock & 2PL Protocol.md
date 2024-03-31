## **DB Lock**

: Machanisms used in database management systems to control concurrent access to shared resources such as database tables, rows, or even specific data items.

\- Ensure data consistency and integrity by preventing conflicts between concurrent transactions

### **Types**

#### **1\. Shared Lock (S-Lock)**

\- Allows multiple transactions to read a resource simultaneously

\- Prevents write operations by other transactions while allowing concurrent read operations

#### **2\. Exclusive Lock (X-Lock)**

\- Grants exclusive access to a resource, allowing modification while preventing other transactions from accessing it

\- Ensrues only one transaction can modify a resource at a time, preventing data inconsistency

#### **3\. Intent Lock**

\- Higher-level locks indicating the intention of a transaction to acquire a specific type of lock on a resource.

\- Helps manage lock compatibility and avoid deadlocks

#### **4\. Schema Lock**

\- Prevents concurrent transactions from modifying the structure of the database

\- Ensures schema consistency during concurrent operaions

#### **5\. Record Lock**

\- Locks placed on individual database records or rows

\- Prevents simultaneous modification of the same record, ensuring data integrity

### **Two-Phase Locking (2PL) Protocol**

: Concurrency control mechanism used in database systems to ensure serializability of transactions and prevent issues such as data inconsistency and deadlock

\- Ensure that transactions acquire all necessary locks before modifying data and release them once finished, preventing inconsistent reads or writes and avoiding deadlocks

#### **Execution Process**

1\. At the start of the transaction's execution, it acquires all necessary DB Locks

2\. The transaction holds onto these locks until it completes its operations, at which point it releases all the acquired DB Locks.

#### **Phase**

**1\. Growing Phase (Lock Acquisition)**

: Transactions acquire all necessary locks without releasing any

**2\. Shirinking Phase (Lock Release)**

: Transactions release all locks they hold, allowing other transactions to access locked resources

#### **Types**

| **Aspect** | **Conservative 2PL** | **Strict 2PL** |
| --- | --- | --- |
| **Lock Acquisition** | Acquires all locks at the beginning |  |
| **Lock Release** | Releases all locks at the end | Releases locks after commiting or aborting |
| **Deadlock Handling** | Deadlocks are resolved by aborting one of the transactions involved | Deadlocks are resolved similarly, but may involve distributed coordination |
| **Atomicity and Durability** | Ensures atomicity and durability within a single database | Extends atomicity and durability across distributed databases or nodes |
| **Consistency Across Databases** | N/A | Ensures global consistency across distributed databases |
| **Performance** | May suffer from lock contention and deadlocks due to long-held locks | Holding locks until commit time can reduce lock contention but may introduce delays |
