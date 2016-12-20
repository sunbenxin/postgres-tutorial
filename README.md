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



-- schema fast restore



## sql syntax

- sql input consists of a sequence of commands. a command is composed of sequence of tokens,terminated by a semicolon(;)
    which tokens are valid depends on the syntax of the particular command

- a token can be a key word, and identifier, a quoted identifier, aliteral or a special character symbol.

- a string constant in SQL is an arbitrary sequence of characters bounded by single quotes. to include a single-quote character within
    a string constant, write two adjacent single quotes.

- bit-string constants looks like regular string constants with a B(upper or lower case)

- value expressions are used in variety of contexts,a value expression is one of following:
    a constant or literal value
    a column reference
    a positional parameter reference , in the body of a function definition or prepared statement
    a subscripted expression
    a filed selectioin expression
    an operator invocation
    a function call
    an aggregate expression
    a window function call
    a type cast
    a collation expression
    a scalar subquery
    an array constructor
    a row constructor
    another value expression in parentheses
