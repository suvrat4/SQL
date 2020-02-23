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

*Syntax: 
  SELECT <collist> FROM 
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

#### Non Equi Join:
When the join condition is based on equality operator, the join is said to be an equi join. When the join condition is based on other than equality operator, the join is said be a non equi join.

### NOTE:
* In Non Equi Join JOIN condition is not based on = operator. It is based on other than = operator usually BETWEEN or > or < opeartors.

*Syntax:
    SELECT <collist> 
    FROM TABLE1, TABLE2..
    WHERE <join condition>[AND <join condition>]
    AND <condition>;

###### Examples:

SELECT e.empno, e.ename, e.sal, s.grade
FROM emp e, salgrade s
WHERE e.sal BETWEEN s.losal AND s.hisal;


SELECT e.empno,e.name,e.sal,d.name,d.loc,s.grade
FROM emp e, dept d, salgrade s
WHERE e.deptno = d.deptno
AND
e.sal BETWEEN g.losal AND g.hisal;


#### Self Join:
* Joining a table to itself is called Self Join.
* Self Join is performed when tables having self referential integrity.
* To perform self join same table must be listed twice with different alias.
* Self join is equi join within the table.

*Syntax:
  SELECT<collist>
  FROM table1 T1, table2 T2
  where T1.column1=T2.column2;
  
###### Exapmles:
Display empno,ename,sal,mgrname?

SELECT e.empno, e.ename, e.sal, m.ename
FROM emp e, emp m
WHERE e.mgr=m.empno;
  
 SQL>  SELECT e.empno, e.ename, e.sal, m.ename
 FROM emp e, emp m
 WHERE e.mgr=m.empno;

     EMPNO ENAME             SAL ENAME
---------- ---------- ---------- ----------
      7902 FORD             3000 JONES
      7788 SCOTT            3000 JONES
      7844 TURNER           1500 BLAKE
      7499 ALLEN            1600 BLAKE
      7521 WARD             1250 BLAKE
      7900 JAMES             950 BLAKE
      7654 MARTIN           1250 BLAKE
      7934 MILLER           1300 CLARK
      7876 ADAMS            1100 SCOTT
      7698 BLAKE            2850 KING
      7566 JONES            2975 KING
      7782 CLARK            2450 KING
      7369 SMITH             800 FORD

13 rows selected.

*Ansi Style

Display EMPNO,ENAME,SAL,MGRNAME?

SQL>  SELECT e.empno, e.ename, e.sal, m.ename
FROM emp e JOIN emp m  
ON (e.mgr=m.empno);

     EMPNO ENAME             SAL ENAME
---------- ---------- ---------- ----------
      7902 FORD             3000 JONES
      7788 SCOTT            3000 JONES
      7844 TURNER           1500 BLAKE
      7499 ALLEN            1600 BLAKE
      7521 WARD             1250 BLAKE
      7900 JAMES             950 BLAKE
      7654 MARTIN           1250 BLAKE
      7934 MILLER           1300 CLARK
      7876 ADAMS            1100 SCOTT
      7698 BLAKE            2850 KING
      7566 JONES            2975 KING
      7782 CLARK            2450 KING
      7369 SMITH             800 FORD

13 rows selected.

Display ENAME,SAL,DNAME,LOC,GRADE,MGRNAME?

SQL>SELECT e.ename,e.sal as salary,d.dname,d.loc as location ,s.grade,m.ename as manager
  2  FROM emp e join dept d
  3  USING(deptno)
  4  JOIN salgrade s
  5  ON(e.sal between s.losal and s.hisal)
  6  JOIN emp m
  7  ON(e.mgr=m.empno);

ENAME          SALARY DNAME          LOCATION           GRADE MANAGER
---------- ---------- -------------- ------------- ---------- ----------
FORD             3000 RESEARCH       DALLAS                 4 JONES
SCOTT            3000 RESEARCH       DALLAS                 4 JONES
JONES            2975 RESEARCH       DALLAS                 4 KING
BLAKE            2850 SALES          CHICAGO                4 KING
CLARK            2450 ACCOUNTING     NEW YORK               4 KING
ALLEN            1600 SALES          CHICAGO                3 BLAKE
TURNER           1500 SALES          CHICAGO                3 BLAKE
MILLER           1300 ACCOUNTING     NEW YORK               2 CLARK
WARD             1250 SALES          CHICAGO                2 BLAKE
MARTIN           1250 SALES          CHICAGO                2 BLAKE
ADAMS            1100 RESEARCH       DALLAS                 1 SCOTT
JAMES             950 SALES          CHICAGO                1 BLAKE
SMITH             800 RESEARCH       DALLAS                 1 FORD

13 rows selected.

#### Outer Join:
Equi join returns only matching records from both the tables but not unmatched record, an outer join retrives a row even when one of the column in the join contains a null value. For example there are two tables one is customer thet stores customer information and another orders table that stores orders placed by customer, INNER JOIN returns only the list of customer who placed orders, but OUTER JOIN also returns customer who did not placed any order. Outer join is 3 types.

* LEFT OUTER JOIN
* RIGHT OUTER JOIN
* FULL OUTER JOIN

##### LEFT OUTER JOIN:

LEFT OUTER JOIN returns all rows(matched and unmatched) from LEFT SIDE table and matching records from RIGHT SIDE table.

*Syntax:
  SELECT table1.column, table2.column
  FROM table1
  LEFT OUTER JOIN table2
  ON (table1.column = table2.column)
  [WHERE CONDITON];

###### EXAMPLES:

SQL> SELECT e.empno,e.ename,d.dname,d.loc
  2  FROM emp e LEFT OUTER JOIN dept d
  3  ON(e.deptno= d.deptno);

     EMPNO ENAME      DNAME          LOC
---------- ---------- -------------- -------------
      7934 MILLER     ACCOUNTING     NEW YORK
      7839 KING       ACCOUNTING     NEW YORK
      7782 CLARK      ACCOUNTING     NEW YORK
      7902 FORD       RESEARCH       DALLAS
      7876 ADAMS      RESEARCH       DALLAS
      7788 SCOTT      RESEARCH       DALLAS
      7566 JONES      RESEARCH       DALLAS
      7369 SMITH      RESEARCH       DALLAS
      7900 JAMES      SALES          CHICAGO
      7844 TURNER     SALES          CHICAGO
      7698 BLAKE      SALES          CHICAGO
      7654 MARTIN     SALES          CHICAGO
      7521 WARD       SALES          CHICAGO
      7499 ALLEN      SALES          CHICAGO

14 rows selected.

##### RIGHT OUTER JOIN:
RIGHT OUTER JOIN returns all rows(matched and unmatched) from right side table and matching records from left side table.

*Syntax:
  SELECT table1.column, table2.column
  FROM table1
  RIGHT OUTER JOIN table2
  ON (table1.column = table2.column);
  
##### FULL OUTER JOIN:
* Returns all rows(matched and unmatched) from both the tables.
* Prior to oracle9i doesn't support FULL OUTER JOIN.
* To perform FULL OUTER JOIN in prior to ORACLE 9i.

*Syntax:
  SELECT table1.column, table2.column
  FROM table1
  FULL OUTER JOIN table2
  ON (table1.column = table2.column);
  
  ##### CROSS JOIN:
  * CROSS JOIN returns cross product of two tables.
  * Each record of one table is joined to each and every record of another table.
  * If table1 contains 10 records and table2 contains 5 records then CROSS JOIN between table1 and table2 returns 50 records.
  * ORACLE performs CROSS JOIN when we submit query without JOIN CONDITION.
  
  *Syntax:
      SELECT  col1,col2 FROM tab1,tab2;
   
   #### Frequently asked questions:
   
   Display various dnames along with total salary for each of the job where total salary is greater than 8000?
   
SQL> SELECT dname,sum(sal)
2    FROM emp JOIN dept
3    USING(deptno)
4    GROUP BY dname HAVING sum(sal)>8000;

DNAME            SUM(SAL)
-------------- ----------
ACCOUNTING           8750
RESEARCH            10875
SALES                9400
   
   
