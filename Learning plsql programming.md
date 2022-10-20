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
	- 





















