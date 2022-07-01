##  SQL

## Introduction
In this paper, we will learn about SQL and Acid Properties, Joins, Normalizations etc.

# Table of Contents
1. [ACID ](#example)
2. [CAP Theorem](#example2)
3. [Joins](#third-example)
4. [Aggregations](#fourth-examplehttpwwwfourthexamplecom)
5. [Filters in queries](#example)
6. [Normalization](#example2)
7. [Indexes](#third-example)
8. [Locking mechanism](#fourth-examplehttpwwwfourthexamplecom)
9. [Database Isolation Levels](#example2)
10. [Triggers](#third-example)
 



## 1.ACID Properties
The Term ACID stands for Atomicity, Consistency ,Isolation,Durability.

These 4 properties play a very important role in maintaining the data-integrity.

### Why ACID properties ?
This properties ensures that the database transaction is completed entirely. It never leaves in the transcations in the half-completed state.

### Atomicity

It means **All or Nothing**. If any operation is performed on a data it should be executed completely or not executed at all (There is no partial execution on the data).

**Eg:-** Let us assume a person is transfering some amount from account A to account B. Let's say he started the transaction and the amount is debited from account A but not credited into the account B (operation failed). Then we use rollback transaction to go back to the previous state. If the transaction is completed only then we commit out database.

### Consistency

It simply states that any changes to a values in an instance are consistent with the values in other instance. At the end of transaction all the data must be left in the consistent state.

**Eg:-** If an amount is debited from a account. The same amount will be credited to the other account not more or less.

This ensures data consistency in the database.

### Isolation

Isolation occures when there is a concurrent transactions. It states that we can convert a parallel schedule into serial schedule.

When two or more transactions occur simultaneously. The data from one transaction should not effect the other transaction untill it is commited.

**Eg:-**  Let's say there are 2 transactions T1 and T2 which is performed
on the database concurrently. What isolation says is first perform one operation T1 and then go to T2.(T1->T2)
or (T2->T1). Let's say a person is transfering an amount 20 Rs to one account B and 30 Rs to another account C. First the amount of 20 Rs will be debited from his account and later balance is updated in his account after that from the remaining balance the 30 Rs will be debited.

When two or more events is happening parallely the consistency of the data is remained.

### Durability

Durability says that all the updates and modifications performed on the database are committed permanently. Once a cycle of Transcation is completed.



### 2.CAP Theorem
CAP theorem, also known as Brewer’s theorem, stands for Consistency, Availability and Partition Tolerance.
 
 
 **Availability**
 
 
Imagine there is a very popular mobile operator in your city and you are its customer because of the amazing plans it offers. Besides that, they also provide an amazing customer care service where you can call anytime and get your queries and concerns answered quickly and efficiently. Whenever a customer calls them, the mobile operator is able to connect them to one of their customer care operators.

The customer is able to elicit any information required by her/him about his accounts like balance, usage, or other information. We call this Availability because every customer is able to connect to the operator and get the information about the user/customer.

**Consistency**

Now, you have recently shifted to a new house in the city and you want to update your address registered with the mobile operator. You decide to call the customer care operator and update it with them. When you call, you connect with an operator. This operator makes the relevant changes in the system. But once you have put down the phone, you realize you told them the correct street name but the old house number (old habits die hard!).

So you frantically call the customer care again. This time when you call, you connect with a different customer care operator but they are able to access your records as well and know that you have recently updated your address. They make the relevant changes in the house number and the rest of the address is the same as the one you told the last operator.

We call this as Consistency because even though you connect to a different customer care operator, they were able to retrieve the same information.

**Partition tolerance**

Recently you have noticed that your current mobile plan does not suit you. You do not access that much mobile data any longer because you have good wi-fi facilities at home and at the office, and you hardly step outside anywhere. Therefore, you want to update your mobile plan. So you decide to call the customer care once again.

On connecting with the operator this time, they tell you that they have not been able to update their records due to some issues. So the information lying with the operator might not be up to date, therefore they cannot update the information. We can say here that the service is broken or there is no Partition tolerance.

## 3.Joins in SQL

A **JOIN** clause is used to combine rows from two or more tables, Based on the common column present in both the tables.

Types of Joins
* Inner Join
* Right Join
* Left Join
* Full Join

![Joins](https://www.thecrazyprogrammer.com/wp-content/uploads/2019/05/Joins-in-SQL-Inner-Outer-Left-and-Right-Join.jpg?ezimgfmt=ng:webp/ngcb1)

### Inner Join
It only returns the data from which it has a common matches for that column.

```
SELECT table.column1 FROM table1
  INNER JOIN table2 ON table1.       common_column = table2.common_column;
```
In the above example it only retrives the data from common_column which has common values in both the tables.

### Left Join

It returns all the records from the left table and only the matched data from the right table.

```
SELECT column FROM table1
  LEFT JOIN table2 ON table1.comm_colum = table2.comm_colum;
```

### Right Join

It returns all the records from the right table and only the matched data from the left table.
```
SELECT column FROM table1
  RIGHT JOIN table2 ON table1.comm_colum = table2.comm_colum;
```

### Outer Join
 It returns all the data from left and right tables

 ```
SELECT column FROM table1
  FULL OUTER JOIN table2 ON table1.comm_colum = table2.comm_colum;
  
  
```

## 4.Aggregate Function's in Databases
Aggregate functions are used to perform calculations on multiple rows of a specific column of the data.

These are used to summarize the data.
* SUM()
* COUNT()
* AVG()
* MIN()
* MAX()
#### SUM()
This function is used to calculate the sum of all the values in a specific column.
```
SELECT SUM(marks) FROM student;
```
#### COUNT()
This function is used to total number of records are present in the table.
```
SELECT COUNT(marks) FROM Students
WHERE marks>50;
```
The above Example gives the total count of students who marks is greater than 50.

#### AVG()

This function is used to compute the average of values for a specified column

```
SELECT AVG(marks) FROM Students;
```
This gives the average marks of the class.

#### MIN()

This function is used to find the minimun value in a specific column which is mentioned.

```
SELECT MIN(marks) FROM students;
```
The above command give the least marks obtained in the students table.

#### MAX()
This function is used to find the maximum value in a specific column which is mentioned.

```
SELECT MAX(marks) FROM students;
```
The above commands gives the marks of student who scored highest.

[For More Aggregate function](https://www.postgresql.org/docs/current/functions-aggregate.html)

## 5.Filters in Databases
### How to retrive data with specified condition ?
In DBMS we have key word to filter the data based on a specific condition.

There are many way's to filter the data from the table.

We use **WHERE** clause in DBMS to get the specific data which satisifies that condition in the table.

```
SELECT * FROM students WHERE marks>60;
```
The above commands retrives only the records of student table who scored more than 60.

### LIMIT
It is used to read only the first 5 records of the data from the table
```
SELECT * FROM students
LIMIT 5
```
It only reads the first 5 records from the students table.

With the help of OFFSET we can specify where our data should start reading from.
```
SELECT * FROM students
LIMIT 5 OFFSET 2;
```
It display's  5 records of the data starting from 2nd record.

### GROUP BY
GROUP BY clause is used to group the data based on categorical column data.

```
SELECT class,AVG(Marks) FROM students
GROUP BY class;
```
The above command gives the average marks of each class.

### ORDER BY

ORDER BY clause is used to sort the data based upon the specific column.

```
SELECT marks FROM students
ORDER BY marks ASC| DESC;
```
ASC stands for Ascending order. It display's the marks in the ascending order.

DESC stands for descending order. It display's the marks in the descending order.



## 6.Normalization



### Consistency

It simply states that any changes to a values in an instance are consistent with the values in other instance. At the end of transaction all the data must be left in the consistent state.

**Eg:-** If an amount is debited from a account. The same amount will be credited to the other account not more or less.

This ensures data consistency in the database.

### Isolation

Isolation occures when there is a concurrent transactions. It states that we can convert a parallel schedule into serial schedule.

When two or more transactions occur simultaneously. The data from one transaction should not effect the other transaction untill it is commited.

**Eg:-**  Let's say there are 2 transactions T1 and T2 which is performed
on the database concurrently. What isolation says is first perform one operation T1 and then go to T2.(T1->T2)
or (T2->T1). Let's say a person is transfering an amount 20 Rs to one account B and 30 Rs to another account C. First the amount of 20 Rs will be debited from his account and later balance is updated in his account after that from the remaining balance the 30 Rs will be debited.

When two or more events is happening parallely the consistency of the data is remained.

### Durability

Durability says that all the updates and modifications performed on the database are committed permanently. Once a cycle of Transcation is completed.



Normalization is a technique of organizing databases into multiple related tables, in order to reduce data redundency.

If there is duplicate data it takes lots of space and also reduces the performance when performing operations.
so,we use Normalizations techniques to overcome this problem.

<img src="https://aksakalli.github.io/images/db-norm/levels-of-normalization.svg" width="200" height="200"/>

#### **1NF**

It states that each single cell must have a single value. All the records must be unique. It should follow the rule of Atomicity.

#### **2NF**
Database should be in 1 NF and necessarily consist of a single column primary key.

#### **3NF**

The database should be in 2 NF and must not have any transitive functional dependencies. (For suppose you had a table which has name and gender as the attributes if you change the name of the person to female person then you should also change the gender of that specific person. This dependency is called Transitive functional dependency.)

In **3 NF** when there is a transitive dependency column we remove that column and make a another table with unique-keys .

#### **BCNF** (Boyce-codd Normal Form)

It is also known as 3.5 Normal Form, Where you divide your tables further so that there would only one candidate key is present.

[Normaliztion Example](https://aksakalli.github.io/2012/03/12/database-normalization-and-normal-forms-with-an-example.html)



## 7.Indexes
Index is a database object that helps in quick retrivel of data from the table. It helps in navigating the data faster.

* Indexes are created on the columns, The columns on which the index is created is called index key.

Syntax to create a index
```
CREATE INDEX index_name ON table_name;
```
#### Unique Indexes
A unique index does **not allow any duplicate values** to be inserted into the table.
```
CREATE UNIQUE INDEX index_name
on table_name (column_name);
```
#### Composite Indexes
A composite index is an index on two or more columns of a table.
```
CREATE INDEX index_name
on table_name (column1, column2);
```
### When do we use indexes
  * when a column contains a wide range of values.
  * A column does not contain a large number of null values.
  * When we need a faster retrival of data from the table.



## 8.Locking

Locking is a mechanism in DBMS which is used to over the problems which are caused by the concurrent access.

There are 2 types of locking modes

* Share lock mode (Read Lock Mode)
* Exclusive lock mode (Write Lock Mode)
  
### Share Lock Mode:
It allows the associated resources to be shared,depending on the operations involved. Several transactions can acquire share locks in the same resource.

### Exclusive lock Mode:-
It  prevents the associates resources from being shared. This lock mode is obtained to modify the data. The first transaction to lock a resource exclusively is the only transaction that can alter the resource until the exclusive lock is released.

* Share-Share is allowed (Two users can simultaneously read the data)
* Share-Exclusive is allowed (While one is reading the data the other can modify it is allowed)
* Exclusive- Share is allowed (While one is updating the other one can read the data.)
* Exclusive-Exclusive is not allowed (While one is updating the data the other one can't update the data which is prohibited.)

Locks are placed at 2 Levels
* Row level
* Tabel level

### Row- Level

In this only the rows which you are updaing are locked not the whole Table.

It is used to prevent 2 transactions from modifying the same row.While 1 transaction is performing a task the other transaction is waiting for that to complete that transaction only then this transaction will execute.

Row-level locking leads to a problem called **dead-lock.**
Dead-Lock:- It occurs when both are waiting for each other.

### Table-Level Locking
Here the entire table is locked.
Table-level locking prevents all the operations on the table.(we can't modify,perform any operation on that table.) 

## 9.Transaction Isolation Levels.

When there is a concurrent transactions on the database we need to isolate the data for each transaction.

To avoid the problems which are caused by the concurrent transactions we use Transaction Isolation Levels

There are 4 types of transaction levels
* Read uncommitted
* Read committed
* Repeatable read
* Serializable
  
![Transaction Isolation Table](https://media.geeksforgeeks.org/wp-content/cdn-uploads/transactnLevel.png)

The above table explains with the use of specific level of transaction we can avoid the anomalies faced by concurrent Transaction.


## 10.Triggers

Triggers are sql commands that are automatically executed in response to certain events on a particular table. This helps in maintaining the integrity of the data. In simple terms it helps to automate the tasks.

### Why do we use Triggers.

Let's say there is a task which needs to performed frequently like Good Morning mail to all the employees daily. It consumes lot of time to do this task repeatedly. In order to automate this we use triggers. 

#### How to create a trigger

```
create trigger [trigger_name] 
[before | after]  
{insert | update | delete}  
on [table_name]  
[for each row]  
[trigger_body]
```
Before or After statement tells us when to perform the Triggers. 
* BEFORE:- It runs the triggers before the trigger statement is run.
*  AFTER:- It runs the triggers after the trigger statemnts are run.

#### HOW To Drop the Trigger

```
DROP TRIGGER <Trigger Name>;
```

BEFORE INSERT Triggers are used to update or modify records before saving in the database.

AFTER INSERT Triggers are used to access the field values that are set by the system and to effect changes in other records.

### Advantages of the Triggers

* It helps in maintaining the integrity of the data.
* Automating the tasks.
* It helps in catching the errors.
* Triggers are useful for inspecting the data.
  
### Disadvantages of the Triggers

* Triggers imposes load on servers.
* Triggers can be very hard to troubleshoot because they execute automatically in the database.
* Triggers can't provide all  kind validations.





## References
* https://www.sqlshack.com/locking-sql-server/
* https://www.tutorialspoint.com/What-are-the-advantages-disadvantages-and-restrictions-of-using-MySQL-triggers
* https://sqlbolt.com/lesson/select_queries_with_joins
* https://www.geeksforgeeks.org/concurrency-control-in-dbms/
* https://www.javatpoint.com/acid-properties-in-dbms
* https://www.geeksforgeeks.org/transaction-isolation-levels-dbms/
* https://www.tutorialspoint.com/sql/sql-indexes.html
* https://www.postgresql.org/docs/9.5/transaction-iso.html
