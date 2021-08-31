# Naming Conventions

## Table of Contents

- [General Rules](#user-content-general-rules)
- [Naming Conventions for PL/SQL](#user-content-naming-conventions-for-plsql)
  - [Naming Conventions for PL/SQL Rules](#user-content-naming-conventions-for-plsql-rules)
  - [Set of Naming Conventions for PL/SQL](#user-content-set-of-naming-conventions-for-plsql)
- [Naming Convention for Schema Objects](#user-content-naming-convention-for-schema-objects)
  - [Naming Convention for Tables](#user-content-naming-convention-for-tables)
  - [Naming Convention for Global Temporary Tables](#user-content-naming-convention-for-global-temporary-tables)
  - [Naming Convention for Private Temporary Tables](#user-content-naming-convention-for-private-temporary-tables)
  - [Naming Convention for SODA Tables](#user-content-naming-convention-for-soda-tables)
  - [Naming Convention for Columns](#user-content-naming-convention-for-columns)
  - [Naming Convention for Indexes](#user-content-naming-convention-for-indexes)
  - [Naming Convention for Constraints](#user-content-naming-convention-for-constraints)
  - [Naming Convention for Sequences](#user-content-naming-convention-for-sequences)
  - [Naming Convention for Triggers](#user-content-naming-convention-for-triggers)
  - [Naming Convention for System Triggers](#user-content-naming-convention-for-system-triggers)
  - [Naming Convention for Views](#user-content-naming-convention-for-views)
  - [Naming Convention for Materialized Views](#user-content-naming-convention-for-materialized-views)
  - [Naming Convention for Synonyms](#user-content-naming-convention-for-synonyms)
  - [Naming Convention for Directories](#user-content-naming-convention-for-directories)
  - [Naming Convention for Packages](#user-content-naming-convention-for-packages)
  - [Naming Convention for Functions](#user-content-naming-convention-for-functions)
  - [Naming Convention for Procedures](#user-content-naming-convention-for-procedures)
  - [Naming Convention for Scheduler Objects](#user-content-naming-convention-for-scheduler-objects)
  - [Naming Convention for Types](#user-content-naming-convention-for-types)

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
1. All exceptions and constants must be uppercase.
1. Avoid double quoted identifiers.
1. Pattern to follow is `{prefix}variablecontent{suffix}`.
1. Nested function or procedure name must start with name of parent and it's own name divided by `__`.
   Example:

```plsql
PARENT: fetch_data
CHILD: fetch_data__handle_record
CHILD OF A CHILD: fetch_data__handle_record__log
```

### Set of Naming Conventions for PL/SQL

| Identifier                                | Prefix | Suffix  | Example            |
| ----------------------------------------- | ------ | ------- | ------------------ |
| Global Variable                           | `g_`   |         | `g_variable`       |
| Local Variable                            | `l_`   |         | `l_variable`       |
| Constant                                  | `C_`   |         | `C_VARIABLE`       |
| Cursor                                    | `cr_`  |         | `cr_variable`      |
| Record                                    | `r_`   |         | `r_variable`       |
| Array/Table (collection)                  | `t_`   |         | `t_variable`       |
| Object                                    | `o_`   |         | `o_variable`       |
| Exception                                 | `E_`   |         | `E_VARIABLE`       |
| Function/Cursor Parameter                 | `p_`   |         | `p_variable`       |
| Procedure IN Parameter                    | `i_`   |         | `i_variable`       |
| Procedure OUT Parameter                   | `o_`   |         | `o_variable`       |
| Procedure IN/OUT Parameter                | `io_`  |         | `io_variable`      |
| Storage table (CREATE TABLE ... STORE AS) | `st_`  |         | `st_variable`      |
| Referenced cursor type                    | `cr_`  | `_type` | `cr_variable_type` |
| Record Type                               | `r_`   | `_type` | `r_variable_type`  |
| Array/Table (collection) Type             | `t_`   | `_type` | `t_variable_type`  |
| Subtype                                   |        | `_type` | `t_variable_type`  |

## Naming Convention for Schema Objects

Never enclose objects names in double quotes.

Never use numbers in name for order.

```sql
carts
carts1
carts_idx
carts_idx1
```

### Naming Convention for Tables

All table names should be plural. If the table name contains several words, only the last one should be plural. Chose short, unambiguous names, using no more than one or two words.

```sql
carts
red_machines
```

Prefix lookup tables with the name of the table they relate to.

```sql
cart_statuses
```

For a linking (or junction) table, concatenate the names of the two tables being linked in alphabetical order. This rule will expresses composite purpose of the table.

```sql
carts_vendors
```

For linking table for generic lookup table use double underline to separate concatenated tables names. But, better to avoid this rule using name, that can describe the table content.

```sql
cart__cart_statuses
```

If table designed to always hold one row only - then you should use singular name.

```
profile
```

Tables protected by an editioning view suffixed by `_eb`.

External tables should have `_ext` suffix.

Denormalized tables should have `_denorm` suffix.

If your database deals with different logical functions and you want to group your tables according to the logical group they belong to, then prefix your table name with a two or three character prefix that can identify the group.

```
rw_railways
rw_stations
```

### Naming Convention for Global Temporary Tables

Use naming rules as described for tables [Naming Convention for Tables](#user-content-naming-convention-for-tables) with suffix `_gtt`.

```sql
june_carts_tmp
```

### Naming Convention for Private Temporary Tables

Use naming rules as described for tables [Naming Convention for Tables](#user-content-naming-convention-for-tables).
The `PRIVATE_TEMP_TABLE_PREFIX` initialisation parameter, which defaults to `ora$ptt_`, defines the prefix that must be used in the name when creating the private temporary table.

```sql
ora$ptt_june_carts
```

### Naming Convention for SODA Tables

Use naming rules as described for tables [Naming Convention for Tables](#user-content-naming-convention-for-tables) with suffix `_soda`. This rule warnings developer, that this table is actually a collection with documents.

```
orders_soda
```

### Naming Convention for Columns

Singular name of what is stored in the column (unless the column data type is a collection, in this case you use plural names).

### Naming Convention for Indexes

All index should be named by template `{table_name}_{column_name...}_{suffix}`, where `{column_name...}` are columns names of index divided by `_` char without `_` char in names, example:

```
waybill_id - waybillid
```

Suffix rules:

| Index Type  | Unique | Functional | Composite | Suffix    |
| ----------- | ------ | ---------- | --------- | --------- |
| B-tree      |        |            |           | `_idx`    |
| B-tree      | ✔︎     |            |           | `_uidx`   |
| B-tree      |        | ✔︎         |           | `_fidx`   |
| B-tree      | ✔︎     | ✔︎         |           | `_fuidx`  |
| B-tree      |        |            | ✔︎        | `_cidx`   |
| B-tree      | ✔︎     |            | ✔︎        | `_cuidx`  |
| B-tree      |        | ✔︎         | ✔︎        | `_cfidx`  |
| B-tree      | ✔︎     | ✔︎         | ✔︎        | `_cfuidx` |
| Bitmap      |        |            |           | `_bidx`   |
| Bitmap      |        | ✔︎         |           | `_bfidx`  |
| Bitmap      |        |            | ✔︎        | `_bcidx`  |
| Bitmap      |        | ✔︎         | ✔︎        | `_bcfidx` |
| Bitmap join |        |            |           | `_bjidx`  |

If table `waybills` must have unique index over column `waybill_number`, than index will have name:
`waybills_waybillnumber_uidx`.

If table `waybills` must have composite functional unique index over columns `waybill_number` and `TRUNC(waybill_date)`, than index will have name:
`waybills_waybillnumber_waybilldate_cfuidx`.

### Naming Convention for Constraints

All constraint should be named by template `{table_name}_{column_name...}_{suffix}`, where `{column_name...}` are columns names of constraint divided by `_` char without `_` char in names, example:

```
waybill_id - waybillid
```

Suffix rules:

| Constraint Type | Deferrable | Suffix |
| --------------- | ---------- | ------ |
| Unique          |            | `uk`   |
| Unique          | ✔︎         | `duk`  |
| Primary Key     |            | `pk`   |
| Primary Key     | ✔︎         | `dpk`  |
| Foreign Key     |            | `fk`   |
| Foreign Key     | ✔︎         | `dfk`  |
| Check           |            | `ck`   |
| Check           | ✔︎         | `dck`  |

If table `waybills` must have unique constraint over column `waybill_number`, than constraint will have name:
`waybills_waybillnumber_uk`.

If table `waybills` must have unique constraint over columns `waybill_number` and `waybill_date`, than constraint will have name:
`waybills_waybillnumber_waybilldate_uk`.

### Naming Convention for Sequences

Each sequence must have suffix `_seq`. If sequence used only by one table, than it should be named as table with suffix `_seq`.

Example:

```
Table: waybills
Sequence: waybills_seq
```

### Naming Convention for Triggers

Trigger names should be made up of the table name, an acronym representing the triggering action and the suffix `_trg`.

Acronym rules:

| Before | After | Insert | Update | Delete | Statement Level | Row Level | Acronym   |
| ------ | ----- | ------ | ------ | ------ | --------------- | --------- | --------- |
| ✔︎     |       | ✔︎     |        |        | ✔︎              |           | `_bis`    |
| ✔︎     |       |        | ✔︎     |        | ✔︎              |           | `_bus`    |
| ✔︎     |       |        |        | ✔      | ✔︎              |           | `_bds`    |
| ✔︎     |       | ✔︎     | ✔︎     |        | ✔︎              |           | `_bius`   |
| ✔︎     |       | ✔︎     |        | ✔      | ✔︎              |           | `_bids`   |
| ✔︎     |       |        | ✔︎     | ✔      | ✔︎              |           | `_buds`   |
| ✔︎     |       | ✔︎     | ✔︎     | ✔      | ✔︎              |           | `_biuds`  |
| ✔︎     |       | ✔︎     |        |        |                 | ✔︎        | `_bir`    |
| ✔︎     |       |        | ✔︎     |        |                 | ✔︎        | `_bur`    |
| ✔︎     |       |        |        | ✔      |                 | ✔︎        | `_bdr`    |
| ✔︎     |       | ✔︎     | ✔︎     |        |                 | ✔︎        | `_biur`   |
| ✔︎     |       | ✔︎     |        | ✔      |                 | ✔︎        | `_bidr`   |
| ✔︎     |       |        | ✔︎     | ✔      |                 | ✔︎        | `_budr`   |
| ✔︎     |       | ✔︎     | ✔︎     | ✔      |                 | ✔︎        | `_biudr`  |
|        | ✔︎    | ✔︎     |        |        | ✔︎              |           | `_ais`    |
|        | ✔︎    |        | ✔︎     |        | ✔︎              |           | `_aus`    |
|        | ✔︎    |        |        | ✔      | ✔︎              |           | `_ads`    |
|        | ✔︎    | ✔︎     | ✔︎     |        | ✔︎              |           | `_aius`   |
|        | ✔︎    | ✔︎     |        | ✔      | ✔︎              |           | `_aids`   |
|        | ✔︎    |        | ✔︎     | ✔      | ✔︎              |           | `_auds`   |
|        | ✔︎    | ✔︎     | ✔︎     | ✔      | ✔︎              |           | `_aiuds`  |
|        | ✔︎    | ✔︎     |        |        |                 | ✔︎        | `_air`    |
|        | ✔︎    |        | ✔︎     |        |                 | ✔︎        | `_aur`    |
|        | ✔︎    |        |        | ✔      |                 | ✔︎        | `_adr`    |
|        | ✔︎    | ✔︎     | ✔︎     |        |                 | ✔︎        | `_aiur`   |
|        | ✔︎    | ✔︎     |        | ✔      |                 | ✔︎        | `_aidr`   |
|        | ✔︎    |        | ✔︎     | ✔      |                 | ✔︎        | `_audr`   |
|        | ✔︎    | ✔︎     | ✔︎     | ✔      |                 | ✔︎        | `_aiudr`  |
| ✔︎     | ✔︎    | ✔︎     |        |        | ✔︎              |           | `_bais`   |
| ✔︎     | ✔︎    |        | ✔︎     |        | ✔︎              |           | `_baus`   |
| ✔︎     | ✔︎    |        |        | ✔      | ✔︎              |           | `_bads`   |
| ✔︎     | ✔︎    | ✔︎     | ✔︎     |        | ✔︎              |           | `_baius`  |
| ✔︎     | ✔︎    | ✔︎     |        | ✔      | ✔︎              |           | `_baids`  |
| ✔︎     | ✔︎    |        | ✔︎     | ✔      | ✔︎              |           | `_bauds`  |
| ✔︎     | ✔︎    | ✔︎     | ✔︎     | ✔      | ✔︎              |           | `_baiuds` |
| ✔︎     | ✔︎    | ✔︎     |        |        |                 | ✔︎        | `_bair`   |
| ✔︎     | ✔︎    |        | ✔︎     |        |                 | ✔︎        | `_baur`   |
| ✔︎     | ✔︎    |        |        | ✔      |                 | ✔︎        | `_badr`   |
| ✔︎     | ✔︎    | ✔︎     | ✔︎     |        |                 | ✔︎        | `_baiur`  |
| ✔︎     | ✔︎    | ✔︎     |        | ✔      |                 | ✔︎        | `_baidr`  |
| ✔︎     | ✔︎    |        | ✔︎     | ✔      |                 | ✔︎        | `_baudr`  |
| ✔︎     | ✔︎    | ✔︎     | ✔︎     | ✔      |                 | ✔︎        | `_baiudr` |

Example: before insert statement level trigger for table `waybills` will be `waybills_bis_trg`.

Compound triggers should have acronym `_cmp` and suffix `_trg`.

Example: `waybills_cmp_trg`.

### Naming Convention for System Triggers

System triggers should be named of event the trigger is based on with `_trg` suffix. DDL events triggers must have prefix `ddl_`.

Examples:

```
db_startup_trg
logon_trg
logoff_trg
server_error_trg
ddl_alter_trg
ddl_create_trg
ddl_drop_trg
ddl_grant_trg
ddl_rename_trg
```

### Naming Convention for Views

All view must contain `_v` suffix. If view represents more that one row, than it must have plural name of what is contained in view. If view used to represent data for one table, than it should be named as table (table: `waybills`, view `waybills_v`).

If there is a view combining two tables `table1` and `table2`, name the view as `table1_table2_v`. Same naming convention can be used with junction tables that are used to link two many-to-many related base tables.

Editioning views are named like the original underlying table to avoid changing the existing application code when introducing edition based redefinition (EBR).

### Naming Convention for Materialized Views

All view must contain `_mv` suffix. If view represents more that one row, than it must have plural name of what is contained in view.

### Naming Convention for Synonyms

Synonyms should be used to address an object in a foreign schema rather than to rename an object. Therefore, synonyms should share the name with the referenced object.

### Naming Convention for Directories

All directories must contain `_dir` suffix.

### Naming Convention for Packages

All packages can be logically divided by types of their usage. Base on this, name of package must have special suffix. Name is built from the content that is contained within the package.

| Logical Package Type | Description                                                                    | Suffix    |
| -------------------- | ------------------------------------------------------------------------------ | --------- |
| Table API            | Select one, insert, update, delete, constants and types, subtypes for DML      | `_tapi`   |
| Table Manager        | Processes with more than one DML statements or complex functionality for table | `_mng`    |
| REST API             | Procedures and functions, constants, types for REST API                        | `_rest`   |
| Jobs                 | Procedures and functions, constants, types for jobs                            | `_jobs`   |
| Deterministic        | Deterministic functions and constants for table                                | `_determ` |
| Pipelined            | Functions, constants, types for pipelines based on table                       | `_pipe`   |
| Common               | Common functionality, used in other packages                                   |           |

Packages with common functionality don't have suffix.

Examples:

```
Table - waybills

Packages for table:
Table API - waybills_tapi
Table Common - waybills_cmn
REST API - waybills_rest
Jobs - waybills_jobs
Deterministic - waybills_determ
Pipelined - waybills_pipe
```

### Naming Convention for Functions

Name is built from a verb followed by a noun in general. Nevertheless, it is not sensible to call a function `get_...` as a function always gets something.
The name of the function should answer the question “What is the outcome of the function?”.

### Naming Convention for Procedures

Name is built from a verb followed by a noun. The name of the procedure should answer the question “What is done?”.

### Naming Convention for Scheduler Objects

Job must be named as noun with `_job` suffix and should answer the question "What is this?". Name can contain one or more words.

Example:

```
manager_job
waybills_handler_job
orders_fetcher_job
emails_sender_job
```

Programs should have suffix `_prg`.

Chains should have suffix `_chn`.

File Watchers should have suffix `_fw`.

Credentials should have suffix `_cred`.

### Naming Convention for Types

A collection type should include the name of the collected objects in their name and suffix `_ct`.

The name of an object type is built by its content (singular) followed by a `_ot` suffix.
