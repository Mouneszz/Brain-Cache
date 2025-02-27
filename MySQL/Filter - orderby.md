When we want to select a specific records by a field we use `where` keyword,
```mysql
select  * from students where age>18;
```

when we need to order them by their age

```mysql 
select * from students 
where age>18
order by age;
```