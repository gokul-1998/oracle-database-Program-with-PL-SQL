## Chapter 1:  Overview of PL/SQL

### Advantages of PL/SQL
- Tight Integration with SQL
- High Performance
- High Productivity
- Portability
- Scalability
- Manageability
- Support for Object-Oriented Programming

#### 1) Tight Integration with SQL
- PL/SQL supports both static and dynamic SQL. 
	- Static SQL is SQL whose full text is known at compile time. 
	- Dynamic SQL is SQL whose full text is not known until run
time. Dynamic SQL lets you make your applications more flexible and versatile
- allows use of  all SQL data manipulation, cursor control, and transaction
control statements, and all SQL functions, operators, and pseudocolumns.
- You need not convert between PL/SQL and SQL data types.
-  PL/SQL lets you run a SQL query and process the rows of the result set one at a
time
-  PL/SQL functions can be declared and defined in the WITH clauses of SQL
SELECT statements
#### 2) High Performance
lets you send a block of statements to the database, significantly reducing
traffic between the application and the database
- Bind Variables
	- turns the variables in the WHERE
and VALUES clauses into bind variables.Can reuse these SQL statements each time the same
code runs, which improves performance.
	- does not create bind variables automatically when you use dynamic SQL, but
you can use them with dynamic SQL by specifying them explicitly
- Subprogram
	- subprograms are stored in executable form, which can be invoked repeatedly as they run in db server
	- are cached and shared among users,
which lowers memory requirements and invocation overhead.
	-  a single invocation over the network can start a large job.
	- This division of work reduces network traffic and
improves response times
- Optimizer
	- PL/SQL compiler has an optimizer that can rearrange code for better
performance.

#### 3) High Productivity
- has many features that save designing and debugging time, and it is the same
in all environments.
- lets you write compact code for manipulating data
-  Just as a scripting
language like PERL can read, transform, and write data in files, PL/SQL can query,
transform, and update data in a database.

#### 4) Portability
- portable and standard language for Oracle development.
- sypport any operating system and platform where
Oracle Database runs.

#### 5) Scalability
-  stored subprograms increase scalability by centralizing application
processing on the database server
- thousands of concurrent users on a single node, due to  shared memory facilities of the shared server 
- further scalability,  use Oracle Connection Manager to multiplex network
connections.

#### 6) Manageability
- stored subprograms increase manageability because you can maintain only
one copy of a subprogram, on the database server
- Any number of applications can use the subprograms, and you can change the
subprograms without affecting the applications that invoke them.

#### 7) Support for Object-Oriented Programming
- allows defining object types that can be used in object-oriented designs.
- supports object-oriented programming with "Abstract Data Types"

### Main Features of PL/SQL
- combines the data-manipulating power of SQL with the processing power of
procedural languages.
- When you can solve a problem with SQL, you can issue SQL statements from your
PL/SQL program, without learning new APIs
- lets you declare constants
and variables, control program flow, define subprograms, and trap runtime errors.
- break complex problems into easily understandable subprograms, which you
can reuse in multiple applications.

	### Topics
	- Error Handling
		- easy to detect and handle errors.
		- When an error occurs, PL/SQL raises an exception
		-  Normal execution stops and
control transfers to the exception-handling part of the PL/SQL block
		- u do not have
to check every operation to ensure that it succeeded, as in a C program.
	- Blocks
		- basic unit of a PL/SQL source program
		- defined by the keywords DECLARE, BEGIN, EXCEPTION, and END.
			- a declarative part, 
			- an executable part,
			-  an exception-handling part
		- Declarations are local to the block and cease to exist when the block completes
execution,
		- Blocks can be nested: Because a block is an executable statement, it can appear in
another block wherever an executable statement is allowed.
		-  can submit a block to an interactive tool. runs the block one time
		-  block is not stored in the database, called an anonymous block (even if it has a label)
		-  anonymous block is compiled each time it is loaded into memory, and its compilation has three stages:
			- 1) Syntax checking: PL/SQL syntax is checked, and a parse tree is generated
			- 2) Semantic checking: Type checking and further processing on the parse tree.
			- 3) Code generation
			- **NOTE** : An anonymous block is a SQL statement.
	- Example 1-1 PL/SQL Block Structure
```
<< label >> (optional)
DECLARE -- Declarative part (optional)
 ----- Declarations of local types, variables, & subprograms
BEGIN -- Executable part (required)
 ----- Statements (which can use items declared in declarative part)
[EXCEPTION -- Exception-handling part (optional)
 ------- Exception handlers for exceptions (errors) raised in executable part]
END;
```
	- Variables and Constants
		-  declare variables and constants, and then use them wherever you can
use an expression.
		- values of variables can change, but the values of constants
cannot
	- Subprograms
		-  PL/SQL subprogram is a named PL/SQL block that can be invoked repeatedly
		- if subprogram has parameters, their values can differ for each invocation
		-  two types of subprograms, 
			- procedures 
			- functions ( function returns a result.) 
		-  lets you invoke external programs written in other languages.
	- Packages
		- A package is a schema object that groups logically related PL/SQL types, variables,
constants, subprograms, cursors, and exceptions.
		- package is compiled and stored in the database, where many applications can share
its contents
		- use the many product-specific packages that Oracle Database supplies
	- Triggers
		- a named PL/SQL unit that is stored in the database and run in response to
an event that occurs in the database.
		- can specify the event, whether the trigger fires before or after the event, and
whether the trigger runs for each event or for each row affected by the event. 
			- For
example, you can create a trigger that runs every time an INSERT statement affects the
EMPLOYEES table
	- Input and Output
		- PL/SQL input and output (I/O) is done with SQL statements that store data in
database tables or query those tables.
| package | Description|
|---|---|
|DBMS_OUTPUT|Lets PL/SQL blocks, subprograms,packages, and triggers display output.Especially useful for displaying PL/SQLdebugging information.|
|HTF|Has hypertext functions that generate HTML tags (for example, the HTF.ANCHOR function generates the HTML anchor tag <A>)|
|HTP|Has hypertext procedures that generate HTML tags|
|DBMS_PIPE|Lets two or more sessions in the same instance communicate.|
|UTL_FILE|Lets PL/SQL programs read and write operating system files.|
|UTL_HTTP|make Hypertext Transfer Protocol (HTTP) callouts, and access data on the Internet over HTTP.|
|UTL_SMTP|Sends electronic mails (emails) over Simple Mail Transfer Protocol (SMTP) as specified by RFC821.|

- NOTE: 
	- To display output passed to DBMS_OUTPUT, you need another program, such as
SQL*Plus. To see DBMS_OUTPUT output with SQL*Plus, you must first issue the
SQL*Plus command SET SERVEROUTPUT ON.
	-  To accept data directly
from the keyboard, use the SQL*Plus commands PROMPT and ACCEPT.







