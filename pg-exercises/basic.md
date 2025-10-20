## Basics

### Question
How can you retrieve all the information from the cd.facilities table? 

### Answer
```shell
exercises=# select * from cd.facilities;
 facid |      name       | membercost | guestcost | initialoutlay | monthlymaintenance 
-------+-----------------+------------+-----------+---------------+--------------------
     0 | Tennis Court 1  |          5 |        25 |         10000 |                200
     1 | Tennis Court 2  |          5 |        25 |          8000 |                200
     2 | Badminton Court |          0 |      15.5 |          4000 |                 50
     3 | Table Tennis    |          0 |         5 |           320 |                 10
     4 | Massage Room 1  |         35 |        80 |          4000 |               3000
     5 | Massage Room 2  |         35 |        80 |          4000 |               3000
     6 | Squash Court    |        3.5 |      17.5 |          5000 |                 80
     7 | Snooker Table   |          0 |         5 |           450 |                 15
     8 | Pool Table      |          0 |         5 |           400 |                 15
(9 rows)
```
### Question
You want to print out a list of all of the facilities and their cost to members. How would you retrieve a list of only facility names and costs?

### Answer
```shell
exercises=# select name, membercost from cd.facilities;
      name       | membercost 
-----------------+------------
 Tennis Court 1  |          5
 Tennis Court 2  |          5
 Badminton Court |          0
 Table Tennis    |          0
 Massage Room 1  |         35
 Massage Room 2  |         35
 Squash Court    |        3.5
 Snooker Table   |          0
 Pool Table      |          0
(9 rows)

```

### Question
How can you produce a list of facilities that charge a fee to members?


### Answer
```shell
exercises=# select name from cd.facilities
where membercost > 0;
      name      
----------------
 Tennis Court 1
 Tennis Court 2
 Massage Room 1
 Massage Room 2
 Squash Court
(5 rows)

```


### Question
How can you produce a list of facilities that charge a fee to members, and that fee is less than 1/50th of the monthly maintenance cost? Return the facid, facility name, member cost, and monthly maintenance of the facilities in question.

### Answer
```shell
exercises=# select name, membercost, monthlymaintenance from cd.facilities
where membercost > 0 and  membercost < 0.02 * monthlymaintenance;

      name      | membercost | monthlymaintenance 
----------------+------------+--------------------
 Massage Room 1 |         35 |               3000
 Massage Room 2 |         35 |               3000
(2 rows)

```