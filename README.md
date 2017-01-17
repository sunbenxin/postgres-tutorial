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
- Tokens are normally separeted by whitespace(space,tab,newline),but if there is no ambiguity(which is generally only the case if a 
    a special character is adjacent to some other tken type)

- conmments can occur in sql input. equivalent to whitespace.

- The sql syntax is not very consistent regarding what tokens identify commands and which 
    are operands or parameters.The first few tokens are generally the command name.

- sql identifiers and key words must begin with a letter(a-z,but also letters with diacritical marks and non-Latin letters) or an underscore.
    subsequent characters in an identifier or key workd can be letters,underscores,digits or dollar signs.(dollar signs are not allowed in sql standard)

- sql standard will not define a key word that constains digits or starts or ends with an underscore.

- The system uses no more than NAMEDATALEN-1 bytes of an identifier.

- key words and unquoted identifiers are case insensive.

- the delimited identifier or quoted identifier is formed by enclosing an arbitrary sequence fo characters in double-quotes. 
- quoted identifiers can contain any character,except the character with code zero.(to include a double quote ,write tow double quotes)

- there are three kinds of implicitly-typed constants in pg:strings,bit strings,and numbers.

- indeed no characters inside a dollar-quoted string are ever escaped.
- tag of dollar-quoted is case sensitive.

- A dollar-quoted string that follows a keyword or identifier must be separated from it by whitespace;otherwise the dollar quoting delimiter would be taken as part of the preceding identifier.

- Dollar quoting is not part of SQL standard.

- A constant of an arbitrary type can be entered using any one of the following notations:

    type 'string'
    'string' ::type
    CAST ('string' AS type)
    typename( 'string' ) // not all type names can be used in this way

    The ::,CAST() and function-call syntax can also be used to specify run-time type conversions of arbitrary expressions.
    to avoid syntactic ambiguity,the type 'string' syntax can only be used to specify the type of a simple literal constant. Another restriction on the type 'string' syntax is that 
    it does not work for array tpes;use :: or CAST() to specify the type of an array constant.

- The result of a value expression is sometimes called a scallar, to distinguish it from the result of a table expression.

- A positional parameter reference is used to indicate a value that is supplied externally to an sql statement.

- expression[subscript] or expression[lower_subscript:upper_subscript]
    each subscript is an expression,which must yield an integer value.

- (arrayfunction(a,b))[42] : the parentheses is required.

- If an expression yields a value of a composite type(row type),then a specific field of the row can be extracted by writing expression.fieldname

- Aggregate expression represents the application of an aggregate function across the rows selected by a query.

- most aggregate functions ignore null inputs.this can be assumed to be true, unless otherwise specified,for all built-in aggregates.

- oridinaril, the input rows are fed to the aggregate function in an unspecified order. order_by_clause can be used to specify the desired ordering.

- If filter is specified, then only the input rows for which the filter_clause evaluates to true are fed to the aggregate function.

- An aggregate expression can only apppear in the result list or HAVING clause of a SELECT command.
  it is forbidden in other causes,such as where,because those clauses are logically evaluated before the results of aggregates are formed

- When an aggregate expression appears in a subquery, the aggregate is normally evaluated over the rows of the subquery.But an exception occurs if the aggregate's 
    arguments contain only outer-level variables: the aggregate then belongs to the nearest such outer level,and is evaluated over t he rows of that query.
    the aggragtage expression as a whole is then an outer reference fro the subquery it appears in and act as a constant over any one evaluatioin of that subquery.

- A window function clal represents the application of an aggregate-like function over some portion of the rows selected by a query.Unlike regular aggregate function calls,this
    is not tied to grouping of the selected rows into a single output row- each row remains separate in the query output. 

- the window function is able to scan all the rows that would be part of the current rows group according to the grouping specification(PARTITION BY list) of the window function call.


### note

- table and query will cache, so when alter a table need fresh the function return setof the table in an transaction to low the influence during the cache restruct.

