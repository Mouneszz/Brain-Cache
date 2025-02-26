To create a Database
```mysql
create database databasename;
```
To remove a database
```mysql
drop database databasename;
```
After using use command the commands which we use after that will work on the database we currently using 
```mysql
use databasename;
```
To **create** a  table we should have at least one column and it should have a datatype
```mysql
create table tablename(sno int, name varchar(100));
```
To **show/retrieve** data we use select command.
```mysql
select * from tablaname;
```
 **Insert**
 To **insert** values into the table the syntax is 
```mysql
 insert into tablename(sno,name) value{202,'Mounesh'};
```
also in database we can rerun the insert code to insert any number of entries

**Update**
The syntax for the update is 
```mysql
update tablename set name = 'Mouneshwaran' where sno = 204;
```

here the `set` is  to set name 'Mouneshwaran' we can use comma `,`  for multiple columns tro change ,`where` `sno` is 204

**Delete**
The syntax to delete is 
```mysql
delete from tablename 
```
