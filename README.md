## **1} Banking System Project Using MySQL:**

A simple MySQL-based banking system that manages accounts, deposits, withdrawals, and transaction history. Built without triggers, it updates balances manually to help beginners understand core SQL operations and how basic banking processes work behind the scenes.

### **2} Purpose of the Project:**

The purpose of this project is to design a simple and well-structured database system that can handle the basic operations of a banking environment. It focuses on managing customer accounts and financial transactions in an organized and reliable way using MySQL.
This project helps students and beginners understand how real-world banking systems store, manage, and retrieve data. It demonstrates important database concepts such as relational table design, data integrity, constraints, and query-based reporting, making it a strong foundation for learning SQL and database development.

### **3} Key Objectives:**

3.1} Customer Account Management
Store and manage customer account details efficiently.

3.2} Transaction Handling
Record deposits and withdrawals accurately for each account.

3.3} Data Integrity and Consistency
Maintain correct and reliable data using primary keys, foreign keys, and constraints.

3.4} Account Summary and Query Support
Enable easy retrieval of account details, transaction history, and summaries using SQL queries.

### **4} Advantages:**

4.1} Efficient management of customer accounts and transactions

4.2} Accurate tracking of deposits and withdrawals

4.3} Maintains data consistency and integrity

4.4} Supports reporting and basic financial analysis

4.5} Scalable for adding more customers and transactions

4.6} Helps in understanding SQL queries and database design concepts

### **5} Disadvantages:**

5.1} Works mainly through MySQL CLI or MySQL Workbench (no user interface)

5.2} Not suitable for large-scale or real-time banking systems

5.3} Lacks advanced security features like authentication and encryption

5.4} Some operations require manual execution of SQL scripts

### **6} Working Flow:**

6.1} Database Initialization
Create the banking database and required tables (Accounts and Transactions).
Apply constraints such as primary keys, foreign keys, and NOT NULL to ensure data accuracy.

6.2️} Data Insertion
Insert sample customer account records into the Accounts table.
Insert sample deposit and withdrawal records into the Transactions table.

6.3️} Transaction Handling
Users or bank staff add new transactions.
Each transaction is linked to a valid account using a foreign key.

6.4} Information Retrieval
Execute SQL queries to view account details and transaction history.
Use views to display summarized account information such as balance and totals.

6.5️} Analysis and Reporting
Run aggregate queries to calculate totals, averages, and summaries.
Use JOIN queries to combine account and transaction data for reports.

6.6️} Maintenance and Updates
Add new accounts or transactions when required.
Update account details if needed.
Perform regular database backups to prevent data loss.

## STEP 1: Create and Use Database
```sql
Create Database Bank;
use Bank;
```

## STEP 2: Create Table Accounts
```sql
CREATE TABLE accounts (account_num INT PRIMARY KEY, cust_name VARCHAR(50), gender CHAR(1),account_type VARCHAR(20),current_balance DECIMAL(10,2));
```

## STEP 3: Insert Values in Accounts Table
```sql
INSERT INTO accounts (account_num, cust_name, gender, account_type, current_balance) VALUES
(1001, 'Priya Patel', 'F', 'Savings', 75000.00),(1002, 'Amit Sharma', 'M', 'Current', 30000.00),(1003, 'Rohan Deshpande', 'M', 'Savings', 12000.00),(1004, 'Sneha Joshi', 'F', 'Savings', 52000.00),(1005, 'Vikas Singh', 'M', 'Current', 85000.00),(1006, 'Pooja Shetty', 'F', 'Savings', 60000.00),(1007, 'Nitin Verma', 'M', 'Current', 15000.00),(1008, 'Ananya Rao', 'F', 'Savings', 40000.00),(1009, 'Amit Sharma', 'M', 'Savings', 20000.00), (1010, 'Kavita Shah', 'F', 'Current', 90000.00);
```

## STEP 4: Create Table Transactions
```sql
CREATE TABLE transactions (tid INT PRIMARY KEY,account_num INT, transaction_type VARCHAR(20),amount DECIMAL(10,2), transaction_date DATE, FOREIGN KEY (account_num) REFERENCES accounts(account_num));
```


## STEP 5: Insert Values in Transactions Table
```sql
INSERT INTO transactions (tid, account_num, transaction_type, amount, transaction_date) VALUES (1, 1001, 'Deposit', 10000, '2025-11-01'),(2, 1002, 'Withdrawal', 5000, '2025-11-03'),(3, 1003, 'Deposit', 7000, '2025-11-05'),(4, 1004, 'Withdrawal', 6000, '2025-11-08'),(5, 1005, 'Deposit', 15000, '2025-11-10'),(6, 1006, 'Deposit', 20000, '2025-11-13'),(7, 1007, 'Withdrawal', 2500, '2025-10-28'),(8, 1008, 'Deposit', 5000, '2025-10-21'),(9, 1009, 'Deposit', 3000, '2025-09-10'),(10, 1010, 'Deposit', 25000, '2025-11-15'),(11, 1001, 'Withdrawal', 4500, '2025-11-17'),(12, 1005, 'Withdrawal', 12000, '2025-11-19'),(13, 1006, 'Deposit', 15000, '2025-11-20'),(14, 1008, 'Withdrawal', 5000, '2025-11-21'),(15, 1003, 'Withdrawal', 6500, '2025-11-22');
```

## STEP 6: Retrieve Table Accounts
```sql
select * from accounts;
```

## STEP 7: Retrieve Table Transactions
```sql
select * from transactions;
```

**Queries**

## 1. Retrieve all customer names who have a balance greater than 50,000.
```sql
mysql> select cust_name,current_balance from accounts where current_balance>50000;
```

## 2. Display account number, customer name, and account type of all customers having SAVINGS accounts.
```sql
mysql> select account_num,cust_name,account_type from accounts where account_type='Savings';
```

## 3. List all transactions made in the current month.
```sql
mysql> select * from transactions where month(transaction_date)=month(current_date);
```

## 4. Show customers who have not made any transactions yet.
```sql
mysql> select * from accounts where account_num not in (select account_num from transactions group by account_num);
```

## 5. Display the top 3 customers with the highest account balance.
```sql
mysql> select account_num,cust_name,current_balance from accounts order by current_balance desc limit 3;
```

## 6. Retrieve all transactions where the amount is greater than 10,000.
```sql
mysql> select * from transactions where amount>10000;
```

## 7. Show the total balance of all accounts combined.
```sql
mysql> select sum(current_balance) as total_balance from accounts;
```

## 8. List customers along with their total deposited amount.
```sql
mysql> select account_num,sum(amount) as Total_Deposit from transactions where transaction_type='Deposit' group by account_num ;
```

## 9. Find customers who made a withdrawal of more than 5,000.
```sql
mysql> select account_num,amount from transactions where transaction_type='Withdrawal' and amount>5000 ;
```

## 10. Display the most recent transaction date for each account.
```sql
mysql> select account_num,max(transaction_date) from transactions group by account_num;
```

## 11. Retrieve the number of transactions each customer has made.
```sql
mysql> select account_num,count(*) from transactions group by account_num;
```

## 12. List customers who have both SAVINGS and CURRENT accounts (if allowed).
```sql
mysql> select account_num,cust_name from accounts where account_type='Savings' and account_type='Current' group by account_num,cust_name;
```

## 13. Find all accounts created by customers whose name starts with 'P'.
```sql
mysql> select * from accounts where cust_name like'p%';
```

## 14. Retrieve customers sorted by their account balance in descending order.
```sql
mysql> select cust_name,current_balance from accounts order by current_balance desc ;
```

## 15. Display the average account balance per account type.
```sql
mysql> select account_type,round(avg(current_balance),2) as Avg_Balance from accounts group by account_type ;
```
