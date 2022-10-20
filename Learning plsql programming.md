## loops
- EXAMPLE 1 -> print natural numbers from 1 to 5
	
```
declare
	i number;
begin 
	i :=1;
	loop
	dbms_output.put_line(i);
	i:=i+1;
	exit when i>5;
	end loop;
end;
```
## procedures
- named block of a statement
- may or maynot return a value
	### syntax
	```
CREATE [OR REPLACE] PROCEDURE procedure_name 
[ (parameter_name [IN | OUT | IN OUT] type [, ...])] 
{IS | AS} 
BEGIN
	<procedure body> 
END procedure_name;
```
	- IN -> input
	- out -> to return the values
	- IN OUT -> variable can be used for both in and out
	- if not specified , default is in
```
create or replace procedure getTopperStudent
as
topperName student.name%type; 
begin
select name into topperName from student where marks=(select max(marks) from student)
dbms_output.put_line(topperName);
end;
```
		- **topperName student.name%type;** -> topperName variable will have the same type as that of the type of name column of student table
		- storing procedure without parameters
		```
create or replace procedure getTopperStudent
as
topperName number:=1; 
begin
dbms_output.put_line(topperName);
end;
```
		- running a stored procedure
		```
begin 
getTopperStudent;
end;
```

## Cursor
- A cursor is a temporary area created in the main memory
when a SQL statement is executed that contains information on a select statement and the rows of data
accessed by it.
- This temporary work area is used to store the data
retrieved from the database, and manipulate this data. 
- A cursor can hold more than one row, but can process
only one row at a time. The set of rows the cursor holds is called the active set. 
- There are two types of cursors in PL/SQL: 
	- Implicit 
		- Implicit cursors get created when you execute DMA queries like Select, insert, delete, update.
		- Oracle gives some useful attributes on this implicit cursors to help us check the status of DML operations
| Attribute | Usage |
|---|---|
|%found|if DML statement affects atleast one row returns True else returns False|
|%notfound|if DML statement affects atleast one row returns False else returns True|
|%rowcount| return the number of rows affected by the DML operations INSERT,DELETE,UPDATED,SELECT |	
		- change the fees to 4500 to all the students 
```
create or replace procedure updateFees(newfee int)
as
var_rows number;
 begin 
update student set fees=newFee; 
if SQL%FOUND then
	var_rows :=SQL%ROWCOUNT;
 	dbms output.put_line('The fees of '|| var_rows Il' students was
updated'); 
else
dbms_output.put_line("Some issue in updating'); 
end if;
 end;
```
		- call the function
```
begin
updateFees(4500);
end;
```

	- Explicit
		- They must be created when you are executing a SELECT statement that returns more than one row in a PL/SQL procedure or a function.
		- Even though the cursor stores multiple records, only one record can be processed at a time, which is called as current row. When you fetch a row the current row position moves to next row. 
		- Both implicit and explicit cursors have the same functionality, but they differ in the way they are accessed.
	- Show the average fees paid by students of each
department.
	```
	declare cursor c1
	is
select deptName as Department.avg(fees) as Average Fees from
	student natural join department group by deptName;
 	rec1 c1%rowtype;
 begin
 for reci in c1 loop
 dbms_output.put_line(rec1.Department ||''|| rec1.Average_Fees);
 end loop;
 end;
	```
	
- https://youtu.be/xofpqdU3cD4?t=655

















