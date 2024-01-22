## **3-Tier Architecture**

### **1\. Presentation Layer (User Interface)**

\- Topmost layer that is responsible for interacting with end-users (e.g. web pages, mobile apps, etc.)

\- To present information to users and gather user input(forwards user requests to the next layer)

### **2\. Business Logic Layer (Application Layer)**

\- Processes the user input received from the presentation layer and coordinates the application's functionality

\- Contains the application's logic, workflows, and business rules  
\- Interacts with the data layer to retrieve or store data but does not directly manage the data storage details  
\- e.g. sign-up, product list-up alogorithm, product information upload feature, etc.

### **3\. Data Storage Layer (Database Layer)**

\- Manage and store data used by the application (includes databases, file systems, or any data storage)

\- Handles data retrieval, storage, and management

\- e.g. member information, product information, history of sales information, etc.

If I use stored procedure, it implies that the data storage layer contains business logic

## **Advantages of Using Stored Procedure**

### **1\. Transparent to Application**

\- If you need to modify the business logic, and the business logic resides in the application layer, you have to turn off and on the instance to apply the changed logic  
\- However, when using stored procedure, as the business logic  is stored within the stored procedure, you can immediately use the modified business logic by simply changing the stored procedure

\- In other words, you can avoid cumbersome process of replacing or updating application server instances, and efficiently manage the business logic within the database

### **2\. Improve Performance**

\- By executing logic on the server side, stored procedures can minimize the amount of data transferred between the database and the appllication, reducing network traffic  
\- Stored procedures are precompiled, which can result in optimized execution plans and faster query execution compared to dynamically generated SQL statements

### **3\. Higher Code Reusability**

\- Stored procedures promote modular design by encapsulating logic within the database  
\- This makes it easier to reuse the same logic across multiple parts of the application

### **4\. Security Enhancements**

\- Stored procedures allow for fine-grained access control, so can control who has permission to execute specific procedures, providing an additional layer of security  
\- By using parameterized queries, the risk of SQL injection attacks is reduced, as user inputs are treated as parameters rather than concatenated directly into SQL statements

## **Chanllenges of Using Stored Procedure**

### **1\. Difficulties in Versioning and Maintenance**

\- Managing version control can be challenging, and changes may not be easily tracked or synchronized  
\- Changes to stored procedures may impact dependent parts of the application, making it essential to manage dependencies effectively

### **2. Complexity in Adding New DB Server**

\- When implementing business logic using stored procedures, if the traffic passes through the presentation tier and moves to the logic tier, most of the traffic is forwarded to the DB server  
\- As a result, there is a possibility that the CPU usage on the DB server may increase more than on the web application server  
In the event of a sudden surge in traffic, considering the scaling of the RDBMS server is an option, but responding urgently is difficult as it involves replicating data to a new server for server expansion  
\- However, if business logic is managed through source code in the logic tier, without directly holding the data, adding application servers is relatively easier  
In other words, managing business logic in the logic tier allows for a quicker response even in urgent situations

### **3\. Concerns about Transparency**

\- Stored procedure is not completely transparent. If you have to change stored procedure name or parameters, you have to modify all application codes  
\- Also, it's not always advantageous to have everything transparent. For instance, if unexpected bugs arise after applying changes, all web applications using the problematic procedure will be using incorrect logic during that time  
\- On the other hand, when managing business logic through source code in the logic tier, if an issue occurs, it is possible to roll back and restart only the affected server, minimizing the impact during problem occurrences
