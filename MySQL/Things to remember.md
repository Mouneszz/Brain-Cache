When and where we have to use table key word before the table name.
- You **must** use `TABLE` when creating, altering, dropping, or truncating a table.
- You **don't** use `TABLE` when performing actions like `SELECT`, `INSERT`, `UPDATE`, or `DELETE`.


```mysql 
drop table students;
```
when we run this code but the students table exist , it pops ups error to solve those.
```mysql
drop table if exists students;
```
here it check it drops if the student exists

Soft delete:
When we want to delete but we dont want it permanently  we add a new column for a flag like `is_delete` we default this to `0` which means its not deleted.
- if we want to delete than mark 1 in the record we want to.

**Minimal** (Theory)
-  what is minimal ,it is the last part of composite primary key where if we remove any one field and it breaks the primary  constraint.

**Natural key** (Theory)
- its when naturally the input from the user is going to be  unique.
- Example : Aadhar is a natural key because it is naturally unique for everybody.
- But we have to assign the field as a primary key , because still human errors can be possible.

**Surrogate key** (Theory)
- when we want  a primary key field but we dont have any so we create one artificially.
- create a field of datatype int with `auto_increment`.
```mysql
order_id int auto_increment;
```

