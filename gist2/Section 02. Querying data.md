This section helps you learn how to query data from the MySQL database server. We will start with a simple ``SELECT`` statement that allows you to query data from a single table.

- [SELECT](http://www.mysqltutorial.org/mysql-select-statement-query-data.aspx) – show you how to use simple ``SELECT`` statement to query the data from a single table.
- [SELECT  DISTINCT](http://www.mysqltutorial.org/mysql-distinct.aspx)  – learn how to use the ``DISTINCT`` operator in the ``SELECT`` statement to eliminate duplicate rows in a result set.

## ``SELECT``
### Introduction to MySQL SELECT statement
The ``SELECT`` statement allows you to get the data from tables or views. A table consists of rows and columns like a spreadsheet. Often, you want to see a subset rows, a subset of columns, or a combination of two. The result of the ``SELECT`` statement is called a result set that is a list of rows, each consisting of the same number of columns.

See the following ``employees`` table in the sample database.  It has eight columns: **employee number, last name, first name, extension, email, office code, reports to, job title** and many rows.
![](http://www.mysqltutorial.org/wp-content/uploads/2009/12/MySQL-employees-table.png)

### syntax of the SELECT statement:
```
SELECT 
    column_1, column_2, ...
FROM
    table_1
[INNER | LEFT |RIGHT] JOIN table_2 ON conditions
WHERE
    conditions
GROUP BY column_1
HAVING group_conditions
ORDER BY column_1
LIMIT offset, length;
```
The ``SELECT`` statement consists of several clauses as explained in the following list:
- ``SELECT`` followed by a list of comma-separated columns or an asterisk (*) to indicate that you want to return all columns.
- ``FROM`` specifies the table or view where you want to query the data.
- [``JOIN``](http://www.mysqltutorial.org/mysql-join/) gets related data from other tables based on specific join conditions.
- [``WHERE``](http://www.mysqltutorial.org/mysql-where/) clause filters row in the result set.
- **[``GROUP BY``](http://www.mysqltutorial.org/mysql-group-by.aspx) clause groups a set of rows into groups and applies [aggregate functions](http://www.mysqltutorial.org/mysql-aggregate-functions.aspx) on each group.**
- [``HAVING``](http://www.mysqltutorial.org/mysql-having.aspx) clause filters group based on groups defined by GROUP BY clause.
- [``ORDER BY``](http://www.mysqltutorial.org/mysql-order-by/) clause specifies a list of columns for sorting.
- [``LIMIT``](http://www.mysqltutorial.org/mysql-limit.aspx) constrains the number of returned rows.

The ``SELECT`` and ``FROM`` clauses are required in the statement. Other parts are optional.

### MySQL SELECT statement examples
The ``SELECT`` statement allows you to query partial data of a table by specifying a list of comma-separated columns in the ``SELECT`` clause. For instance, if you want to view only  first name, last name, and job title  of the employees, you use the following query:
```
SELECT 
    lastname, firstname, jobtitle
FROM
    employees;
```
Even though the ``employees`` table has many columns, the ``SELECT`` statement just returns data of three columns of all rows in the table as highlighted in the picture below:
![](http://www.mysqltutorial.org/wp-content/uploads/2009/12/MySQL-employees-table-columns.png)
![](http://www.mysqltutorial.org/wp-content/uploads/2009/12/MySQL-SELECT-columns-example.png)

If you want to get data for all columns in the ``employees`` table, you can list all column names in the ``SELECT`` clause. Or you just use the asterisk (*) to indicate that you want to get data from all columns of the table like the following query:
```
SELECT * FROM employees;
```
It returns all columns and rows in the ``employees`` table.

You should use the asterisk (*) for testing only. In practical, you  should list the columns that you want to get data explicitly because of the following reasons:

- The asterisk (*) returns data from the columns that you may not use. It produces unnecessary I/O disk and network traffic between the MySQL database server and application.
- If you explicit specify the columns, the result set is more predictable and easier to manage. Imagine when you use the asterisk(*) and someone changes the table by adding more columns, you will end up with a result set that is different from what you expected.
- Using asterisk (*) may expose sensitive information to unauthorized users.

In this tutorial, you’ve learned about the basic MySQL SELECT statement to query data from a table in MySQL.

## ``SELECT DISTINCT``
### Introduction to MySQL DISTINCT clause
When querying data from a table, you may get duplicate rows. In order to remove these duplicate rows, you use the ``DISTINCT`` clause in the SELECT statement.

The syntax of using the ``DISTINCT`` clause is as follows:
```
SELECT DISTINCT
    columns
FROM
    table_name
WHERE
    where_conditions;
```

### MySQL DISTINCT example
Let’s take a look a simple example of using the ``DISTINCT`` clause to select the unique last names of employees from the ``employees`` table.

First, we query the last names of employees from the ``employees`` table using the ``SELECT`` statement as follows:
![](http://www.mysqltutorial.org/wp-content/uploads/2011/02/mysql-duplicate-last-name.png)

Some employees have the same last name  ``Bondur``,``Firrelli`` etc.

To remove the duplicate last names, you add the ``DISTINCT`` clause to the ``SELECT`` statement as follows:
```
SELECT DISTINCT
    lastname
FROM
    employees
ORDER BY lastname;
```
![](http://www.mysqltutorial.org/wp-content/uploads/2011/02/MySQL-DISTINCT-last-name.png)
The duplicate last names are eliminated in the result set when we used the ``DISTINCT`` clause.

### MySQL ``DISTINCT`` and ``NULL`` values
