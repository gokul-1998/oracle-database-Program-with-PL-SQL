### intro to oracle PL/SQL

- give list of employees for deptno 30

  ```
  Select * from employees where deptno=30;
  ```

- update salary of employees for
  - dept 20 => hike=5%,
  - dept 30 => hike=10%
  - if any error print error message
- requirements :
  - conditional update
  - error handling
- why PL/SQL?
  - supports error handling
  - oops
  - composite data types
  - programming constructs like variable declarations,conditional statements,loop
- PL/SQL block
  - basic programming structure wth 3 sections
  - declarations ( optional section)
    - declare variables,cursors
  - executable sections(Mandatory)
    - write programming logic
  - exception section(optional)
    - handle error at runtime -> write exceptions
- Basic structure of PL/SQL Block

  ```
  Declare
  -- variables (declaration block)
  BEGIN
  -- program logic (execution block)
  EXCEPTION
  -- Write Exceptions ( exception block)
  END;
  ```

- SAMPLE 1 : print a message

```
BEGIN
  DBMS_OUTPUT.PUT_LINE('welcome to pl/sql training');
END;
```

- output

```
welcome to pl/sql training
```
- only single quote `'` should be used
- online compiler -> <https://livesql.oracle.com/>
- note : ``` set serveroutput on;``` -> to get the output on screen
	- we can also use lower case
- SAMPLE 2 : sum of two numbers

```
declare
x number :=5;
y number :=8;
z number;
begin
z := x+y;
DBMS_OUTPUT.PUT_LINE('sum is '|| z);
END;
```

- output

```
sum is 13
```
- SAMPLE 3 : bit complex

```
DECLARE 
  a number(2) := 20; 
  b number(2) := 10; 
  c number(2) := 15; 
  d number(2) := 5; 
  e number(2) ; 
BEGIN 
  e := (a + b) * c / d;      -- ( 30 * 15 ) / 5 
  dbms_output.put_line('Value of (a + b) * c / d is : '|| e );  
  e := ((a + b) * c) / d;   -- (30 * 15 ) / 5 
  dbms_output.put_line('Value of ((a + b) * c) / d is  : ' ||  e );  
  e := (a + b) * (c / d);   -- (30) * (15/5) 
  dbms_output.put_line('Value of (a + b) * (c / d) is  : '||  e );  
  e := a + (b * c) / d;     --  20 + (150/5) 
  dbms_output.put_line('Value of a + (b * c) / d is  : ' ||  e ); 
END; 
```

- output

```
Value of (a + b) * c / d is : 90
Value of ((a + b) * c) / d is  : 90
Value of (a + b) * (c / d) is  : 90
Value of a + (b * c) / d is  : 50
```
### exception section
* there are approximately 20 inbuilt exceptions present in PL/SQL
	- *OTHERS* -> handles any exception
	- *NO_DATA_FOUND*
	- *TOO_MANY_ROWS*
- SAMPLE 1 : sum of two numbers

```
declare
x number :=5;
y varchar2(100):= 'A';
z number;
begin
z := x+y;
DBMS_OUTPUT.PUT_LINE('sum is '|| z);
END;
```
- error
```
ORA-06502: PL/SQL: numeric or value error: character to number conversion error ORA-06512: at line 6
ORA-06512: at "SYS.DBMS_SQL", line 1721
```
	- HANDLING ERROR
```
declare
x number :=5;
y varchar2(100):= 'A';
z number;
begin
z := x+y;
DBMS_OUTPUT.PUT_LINE('sum is '|| z);
EXCEPTION
    WHEN OTHERS
        THEN 
        DBMS_OUTPUT.PUT_LINE('ERROR IS ENCOUNTERED');         
END;
```
	- output
```
ERROR IS ENCOUNTERED
```
- emp table

|slno |  emp_no  |  job  | ename | mgr | hiredate | sal |comm |  deptno  |
|---|---|---|---|---|---|---|---|---|
|1| 7499 | Salesman  | allen | 7698 | 20-feb-81 | 1600 | 300 | 30 |
|2| 7521| Salesman  | ward| 7698 | 22-feb-81 | 1250| 500| 30 |
|3| 7566 | manager| jones| 7839| 04-feb-81 | 2975| (null)| 20 |
|4| 7654 | Salesman  | martin| 7698 | 28-sep-81 | 1250| 1400 | 30 |
|5| 7369 | clerk| smith| 7902| 17-dec-80 | 800| (null) | 20 |

### example 1
- SQL
	```
	select ename from emp where emp_no=7499;
```
- PL/SQL
	```
DECLARE
lv_name VARCHAR2(100);
BEGIN
SELECT ename
INTO lv_name 
FROM emp 
WHERE emp_no=7499;
DBMS_OUTPUT.PUT_LINE('employee name is '|| lv_name);      
END;
```
- output
```
employee name is allen
```
### example 2 -> with no data, 
- SQL
	```
	select ename from emp where emp_no=787644;
```
- output
```
```
	```
DECLARE
lv_name VARCHAR2(100);
BEGIN
SELECT ename
INTO lv_name 
FROM emp 
WHERE emp_no=787644;
DBMS_OUTPUT.PUT_LINE('employee name is '|| lv_name);      
END;
```
- output
```
error message
```

- PL/SQL -> while handling exception
```
DECLARE
lv_name VARCHAR2(100);
BEGIN
SELECT ename
INTO lv_name 
FROM emp 
WHERE emp_no=787644;
DBMS_OUTPUT.PUT_LINE('employee name is '|| lv_name);  
EXCEPTION 
 WHEN NO_DATA_FOUND
 THEN
	DBMS_OUTPUT.PUT_LINE('No records fetched from the query');    
END;
```
- output
```
No records fetched from the query
```
### example 3 -> when query returns more than a single row
- SQL
	```
	select ename from emp where dept_no=20;
```
- output
| ename |
|---|
|jones|
|clerk|
- PL/SQL -> without handling exception
```
DECLARE
lv_name VARCHAR2(100);
BEGIN
SELECT ename
INTO lv_name 
FROM emp 
WHERE emp_no=787644;
DBMS_OUTPUT.PUT_LINE('employee name is '|| lv_name);  
EXCEPTION 
 WHEN NO_DATA_FOUND
 THEN
	DBMS_OUTPUT.PUT_LINE('No records fetched from the query');    
END;
```
- error
```
exact fetch returns more than the requested number of rows
```
#### note : any PL/SQL block can handle only one record/row

- PL/SQL -> while handling exception
```
DECLARE
lv_name VARCHAR2(100);
BEGIN
SELECT ename
INTO lv_name 
FROM emp 
WHERE emp_no=787644;
DBMS_OUTPUT.PUT_LINE('employee name is '|| lv_name);  
EXCEPTION 
 WHEN NO_DATA_FOUND
 THEN
	DBMS_OUTPUT.PUT_LINE('No records fetched from the query');
 WHEN TOO_MANY_ROWS
 THEN
	DBMS_OUTPUT.PUT_LINE('Multple records fetched from the query');
END;
```
- output
```
Multple records fetched from the query
```
## ADVANTAGE OF PL/SQL
- 1) Block Structure : has blocks of code which can be nested within each other, and can be stored in DB and reused
- 2) Consists of procedural language structure, if else and loops
- 3) better performance, by  processing multile statements as a single block, thereby reducing Network Traffic
- 4) handles error at runtime
- 5) composite data types - like %TYPE,%ROWTYPE,PL/SQL Records and Tables
- 6) Bulk collect -> to collect data which further enhances the performance of the program

SOURCE : https://www.youtube.com/watch?v=8yfEl0Yvxto 