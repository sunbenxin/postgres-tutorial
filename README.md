# postgres-tutorial
## words
- integral decompose 
## data type
* asdf


## data def
* table
	- 

## Functions and Operators

- \df and \do can be used to list all available functions and operators.

- logical operators: AND OR NOT

- SQL uses a three-valued logic system with true,false,and null,which represents "unknown"

## PL/pgSQL - SQL Procedural Language

- functions written in PL/pgSQL can accept as arguments any scalar or array data type supported by the server,and they can return a result of any of these types. They can also accept or return any composite type (row type) specified by name. 
- PL/pgSQL function can handle errors and exceptions.
- Functions written in PL/pgSQL can invode other functions or contain sub-blocksi inside the main block
- PL/pgSQL is a block-structured and case-insensitive language. A block comprises statements inside the same set of the DECLARE/BEGIN and END statements.
- A block can be defined as follows:
    DECLARE
        declarations
    BEGIN
        statements
    END;

- CREATE OF REPLACE FUNCTION function_name (arguments)
    RETURN type AS
    (replace drops the function with same name if exists)

- the declaration section contains a variable name and its data type ends with a semicolon.
    any variable,row, or records used in a block or its sub-block should be declared here, with an exception to the FOR loop.
    DECLARE
        declaration;

- the statement section can further contain unlimited sub-blocks.
    BEGIN
        Statement;

- The END keyword ends the code block as shown in the following statement:
    END;
    LANGUAGE 'plpgsql';

- template
    CREATE OR REPLACE FUNCTION getRecords()
    RETURNS INTEGER AS $$
    DECLARE
        total INTEGER;
    BEGIN
        SELECT COUNT(*) INTO total FROM warehouse_tbl;
        RETURN total;
    END;
    $$ LANGUAGE plpgsql;

-- conmments --  or /* */

-- declaring variables 






- 
