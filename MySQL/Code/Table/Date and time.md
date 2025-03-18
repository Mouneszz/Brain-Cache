```mysql
%%sql
create table events (
    id int auto_increment primary key,
    event_name varchar(100),
    event_date datetime,
    created_at timestamp default current_timestamp
    );
```
we can give a simple `date` for date only and if we need both date and time `datetime`.

`current_timestamp` gives the current time of the machine you are running on.

`date` format =  `yyyy-mm-dd`
`datetime` format = `yyyy-mm-dd hh-mm-ss`

To get only year from datetime
```mysql\
select year(event_date) as year from events;
```
To get only date from datetime
```mysql
select date(event_date) as date from events;
```
To get only day from datetime
```mysql
select day(event_date) as day from events;
```

To add 30 days  into the datetime field
```mysql
select event_date,event_date + interval 30 day as after_30 from events;
```
`interval` important as it adds in the basis of time but if we simply add 30 it acts as addition of 30 int.
so `interval 30 day`


**date format**
To get the day in the week, month we have to use format.
```mysql
select date_format(event_date,'%W,%M,%e,%Y') as formatted_date from events;
```
`%W` -  will get the day in week
`%M` - will get the month
`%e` -  will get the day
`%Y` - will get the year

To format the time
```mysql
select date_format(event_date,'%h:%i %p') as formatted_date from events;
```
`%h` - hour in 12 hour format
`%i` - minutes 
`%p` - AM or PM
