# Naming Conventions

## Table of Contents

- [General Rules](#user-content-general-rules)
- [Naming Conventions for PL/SQL](#user-content-naming-conventions-for-plsql)
  - [Naming Conventions for PL/SQL Rules](#user-content-naming-conventions-for-plsql-rules)
  - [Set of Naming Conventions for PL/SQL](#user-content-set-of-naming-conventions-for-plsql)
- [Naming Convention for Schema Objects](#user-content-naming-convention-for-schema-objects)
  - [Naming Convention for Tables](#user-content-naming-convention-for-tables)
  - [Naming Convention for Global Temporary Tables](#user-content-naming-convention-for--global-temporary-tables)
  - [Naming Convention for Private Temporary Tables](#user-content-naming-convention-for-private-temporary-tables)
  - [Naming Convention for SODA Tables](#user-content-naming-convention-for-soda-tables)
  - [Naming Convention for Indexes](#user-content-naming-convention-for-indexes)
  - [Naming Convention for Constraints](#user-content-naming-convention-for-constraints)
  - [Naming Convention for Sequences](#user-content-naming-convention-for-sequences)
  - [Naming Convention for Triggers](#user-content-naming-convention-for-triggers)

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

```sql
profile
```

If your database deals with different logical functions and you want to group your tables according to the logical group they belong to, then prefix your table name with a two or three character prefix that can identify the group.

```sql
rw_railways
rw_stations
```

### Naming Convention for Global Temporary Tables

Use naming rules as described for tables [Naming Convention for Tables](#user-content-naming-convention-for-tables) with suffix `_tmp`.

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

Trigger names should be made up of the table name, an acronym representing the triggering action and the suffix “\_trg”.

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

### Naming Convention for Types
