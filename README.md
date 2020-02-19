# SQL

## Joins

* A join is a data retrival operation that combines rows from two or more tables, views, meterialized views. 

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
  Table1, Table2, TableN..
  WHERE <join condition>
  AND < filter condition> ;
  
  ##### Guidelines:
  
When writing a SELECT statement that join tables, precede the column name with table name or the table alias for faster access to avoid ambiguity.

###### Example:
Display empno,ename,deptno,dname,loc?
'''
SELECT e.empno, e.ename, d.deptno, d.dname, d.loc
FROM emp e, dept d
WHERE e.deptno = d.deptno;
'''
### NOTE:
* JOIN condition is specified by using ON clause or USING clause
* Use USING clause if commnon column name is same.

##### Using ON clause

###### Examples using ON caluse:

SELECT e.empno, e.ename, e.sal, d.dname, d.loc
FROM emp e dept d
ON (e.deptno = d.dept.no);

###### Examples Using Using clause:

SELECT e.empno, e.ename, e.sal, d.dname, d.loc
FROM emp e JOIN dept d
USING(deptno);

### NOTE: 
* In USING caluse common column name should not be prefixed with table alias.
