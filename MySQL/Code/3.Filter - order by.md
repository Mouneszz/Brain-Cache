When we want to select a specific records by a field we use `where` keyword,
```mysql
select  * from students
where age>18 and gender = 'female';
```
In where can give more conditions by using `and`

when we need to order them by their age

```mysql 
select * from students 
where age>18
order by age;
```

To order in descending order
```mysql
select * from students 
where age>18
order by age desc;
```