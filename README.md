# SQL

## Joins

* A join is a data retrival operation that combines rows from two or more tables, views, mererialized views. 

* Oracle performs a join operation whenever multiple table appear in the from clause of the query.

### Types of Joins
* Inner join or Equi join
* Non-Equi join
* Self join
* Outer join
* Cross join

#### Inner Join

* In Inner Join operation is performed based on common columns.
* To perform INNER JOIN there should be a common column in joining tables and name of the common column need not to be same.
* To perform INNER JOIN parent/child relatioship between the tables is not mandatory.
* INNER JOIN is most commonly used join in real time.

--Syntax: SELECT <collist> FROM 
  Table1, Table2, Tablen..
  WHERE <join condition>
  AND < filter condition> ;
  
  ##### Guidelines:
  
When writing a SELECT statement that join tables, precede the column name with table name or the table alias for faster access to avoid ambiguity.
  
  
