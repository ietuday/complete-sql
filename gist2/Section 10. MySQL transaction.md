- [``MySQL transaction``](http://www.mysqltutorial.org/mysql-transaction.aspx) – learn about MySQL transactions, and how to use ``COMMIT`` and ``ROLLBACK`` to manage transactions in MySQL.
- [``MySQL table locking``](http://www.mysqltutorial.org/mysql-table-locking/) – learn how to use MySQL locking for cooperating table access between sessions.

## Introducing to MySQL Transaction
To understand what a transaction in MySQL is, let’s take a look at an example of adding a new sales order in our sample database. The steps of adding a sales order are as described as follows:

- Query the latest sales order number from the ``orders`` table, and use the next sales order number as the new sales order number.
- Insert a new sales order into the ``orders`` table for a given customer.
- Insert new sales order items into the ``orderdetails`` table.
- Get data from both table ``orders`` and ``orderdetails`` tables to confirm the changes

Now imagine what would happen to your data if one or more steps above fail because of database failure such as table lock security? If the step of adding order items into ``orderdetails`` table failed, you would have an empty sales order in your system without knowing it. Your data may not be integrity and the effort you have to spend to fix it is tremendous.

How do you solve this problem? That’s why the transaction processing comes to the rescue. MySQL transaction enables you to execute a set of MySQL operations to ensure that the database never contains the result of partial operations. In a set of operations, if one of them fails, the rollback occurs to restore the database. If no error occurred, the entire set of statements is committed to the database.