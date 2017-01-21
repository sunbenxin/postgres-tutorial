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



# new

## Sql Syntax

### Lexical structure

### Value expressions

### Calling functions


## Data Definition

## Data manipulation

### Insert
### Update
### Delete

## Queries

### overview
- the process of retrieving or the command to retrieve data from
a database called a query.In sql the SELECT command is used to specify queries.

- SELECT COMMAND syntax:

    [WITH with_queries] SELECT select_list FROM table_expression [ sort_specification]

### Table expressions

- a table expression computes a table. It can followed by where, group by and having clauses.
and this specify a pipeline of successive transformations performed on the table derived in the FROM clause.
all these transfromations produce a virtual table that provides the rows that are passed to the select list to compute the output rows of the query.

- The From clause derives a table from one or more other tables given in a comma-separated table reference list.

    FROM table_reference [, table_reference[, ...]]

- a table_reference can be a table name(possibly schma-qualified). 
or derived table such as a subquery, a join construct, or complex combinations of these.

- if more than one table reference is listed in the FROM clause,the tables are cross-joined.
the result of the FROM list is an intermediate virtual table that can then be subject to transformations by 
the WHERE, GROUP BY , and HAVING clauses and is finally the result of the overall table expression.

- When a table reference names a table that is the parent of a table inheritance hierarchy,the table reference produces rows of not only
that table but all of its descendata tables,unless the key word ONLY precedes the table name.
instead of writing ONLY before the table name, you can write * after the table name to explicitly specify that descendant tables are included.
writing * is not necessary since that behavior is the default.

- A joined table is a table derived from two other (real or derived) tables according to the rules of the particular join type. Inner,outer,and cross-joins.

    T1 join_type T2 [ join_condition ]

- join of all types can be chained together,or nested.

- cross join: will contain a row consisting of all columns in T1 followed by all columns in T2.

-  join binds more tightly than comma.

    T1 { [INNER] | {LEFT | RIGHT | FULL } [OUTER] } JOIN T2 ON boolean_expression

    T1 { [INNER] | {LEFT | RIGHT | FULL } [OUTER] } JOIN T2 USING ( join column list)

    T1 NATURAL { [INNER] | { LEFT | RIGHT | FULL } [ OUTER ]} JOIN T2

- the words INNER and OUTER are optional in all forms.INNER is the default,left ,right and full imply an outer join.

- INNER JOIN: for each row R1 of T1, the joined table has a row for each row in T2 that satifies the join condition with R1.

- LEFT OUTER JOIN:
- RIGHT OUTER JOIN:
- FULL OUTER JOIN:

- NATURAL is a shorthand form of USING: it forms a USING list consisting of all column names that appear in both input tables.

- a temporary name can be given to tables and complex table reference ss to be used for referceces to the derived table in the reset of query. this is called a table alias.

    FROM table_reference AS alias
    FROM table_reference alias

- talbe functions are function that produce a set of rows, made up of either base data types or composite data types.they are used like a table view or subquery in the FROM clause of a query.
Columns returned by table functions can be included in SELECT,JOIN OR WHERE clauses in the same manner as columns of a table,view,or subquery.

- talbe functions may also be combined using the ROWS FROM syntax with the results returned in parallel columns. the number of result rows in this case is that of the largest function result,with smaller results padded with null values to match.

    function_call [WITH ORDINALITY] [[AS] table_alias [(column_alias[,...])]]
    ROWS FROM (function_call[,...]) [WITH ORIDINALITY] [[AS] table_alias [(column_alias[,...])]]


### Select Lists
### Combining Queries
### Sorting Rows
### Limit and offset
### Values Lists
### With Queries


## Data types

## function and operator

## type conversion

## index

## full text search

## concurrency contorl

## performance tips

## parallel query

## Sever setup and operation

## Server configuration

## client configuration

## client authentication

## database roles

## trigger

## event trigger

## the rule system

## PL/pgSQL Procedural Language

### Overview

### Declarations

### Basic Statements

### control structure

### cursor

### Error and message


### trigger procedure


### PL/pgSQL under the hood


### tips for developing PL/pgSQL


### overview of PosgreSQL internal

### note

- table and query will cache, so when alter a table need fresh the function return setof the table in an transaction to low the influence during the cache restruct.

