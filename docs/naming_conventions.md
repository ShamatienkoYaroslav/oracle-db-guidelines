# Naming Conventions

ToC:

[General Rules](#user-content-general-rules)

[Naming Conventions for PL/SQL](#user-content-naming-conventions-for-plsql)

## General Rules

1. Never use names with a leading numeric character.
1. Always choose meaningful and specific names.
1. Avoid using abbreviations unless the full name is excessively long.
1. Avoid long abbreviations. Abbreviations should be shorter than 5 characters.
1. Any abbreviations must be widely known and accepted.
1. Create a glossary with all accepted abbreviations.
1. Never use ORACLE keywords as names. A list of ORACLEs keywords may be found in the dictionary view `V$RESERVED_WORDS`.
1. Avoid adding redundant or meaningless prefixes and suffixes to identifiers.
   Example: `CREATE TABLE emp_table`.
1. Always use one spoken language (e.g. English, German, French) for all objects in your application.
1. Always use the same names for elements with the same meaning.

## Naming Conventions for PL/SQL

### Naming Conventions for PL/SQL Rules

1. All variables names must be in lowercase.
1. Avoid double quoted identifiers.
1. Pattern to follow is `{prefix}variablecontent{suffix}`.
1. Function name must start with "f#\_" prefix, where "#" is number in package.
   Example:
   ```plsql
   f4_get_goods();
   ```
1. If function is local, then name must start with prefix "fl#".
   Example:
   ```plsql
   fl4_get_goods();
   ```
1. Nested function or procedure name must start with `{parent_prefix}_{prefix}_`, where `{parent_prefix}` is prefix of parent function or procedure in package and `{prefix}` is type of code block (function - f, procedure - p).
   Example:

```plsql
f4_p_handle_goods_localisation();
f4_f_get_goods_localisation();
p5_p_combine_name();
```

### Set of Naming Conventions for PL/SQL

| Identifier                                | Prefix | Suffix  | Example            |
| ----------------------------------------- | ------ | ------- | ------------------ |
| Global Variable                           | `g_`   |         | `g_variable`       |
| Local Variable                            | `l_`   |         | `l_variable`       |
| Constant                                  | `c_`   |         | `c_variable`       |
| Cursor                                    | `cr_`  |         | `cr_variable`      |
| Record                                    | `r_`   |         | `r_variable`       |
| Array/Table (collection)                  | `t_`   |         | `t_variable`       |
| Object                                    | `o_`   |         | `o_variable`       |
| Exception                                 | `e_`   |         | `e_variable`       |
| Function/Cursor Parameter                 | `p_`   |         | `p_variable`       |
| Procedure IN Parameter                    | `i_`   |         | `i_variable`       |
| Procedure OUT Parameter                   | `o_`   |         | `o_variable`       |
| Procedure IN/OUT Parameter                | `io_`  |         | `io_variable`      |
| Storage table (CREATE TABLE ... STORE AS) | `st_`  |         | `st_variable`      |
| Referenced cursor type                    | `cr_`  | `_type` | `cr_variable_type` |
| Record Type                               | `r_`   | `_type` | `r_variable_type`  |
| Array/Table (collection) Type             | `t_`   | `_type` | `t_variable_type`  |
| Subtype                                   |        | `_type` | `t_variable_type`  |
