### intro to oracle PL/SQL
  * give list of employees for deptno 30
    ```
    Select * from employees where deptno=30;
    ```
  * update salary of employees for 
    * dept 20 => hike=5%, 
    * dept 30 => hike=10%
    * if any error print error message
  * requirements :
    * conditional update 
    * error handling
  * why PL/SQL?
    * supports error handling 
    * oops
    * composite data types
    * programming constructs like variable declarations,conditional statements,loop
  * PL/SQL block
    *  basic programming structure wth 3 sections
      * declarations ( optional section)
        * declare variables,cursors 
      * executable sections(Mandatory)
        * write programming logic
      * exception section(optional)
        * handle error at runtime -> write exceptions
  * Basic structure of PL/SQL Block
    ```
    Declare
    -- variables
    BEGIN
    -- program logic
    EXCEPTION
    -- Write Exceptions
    END;
    ```
    
