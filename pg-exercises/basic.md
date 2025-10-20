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

## Basics

### Question
How can you produce a list of all facilities with the word 'Tennis' in their name?

### Answer
```shell
exercises=# select * from cd.facilities 
where name like '%Tennis%';
 facid |      name      | membercost | guestcost | initialoutlay | monthlymaintenance 
-------+----------------+------------+-----------+---------------+--------------------
     0 | Tennis Court 1 |          5 |        25 |         10000 |                200
     1 | Tennis Court 2 |          5 |        25 |          8000 |                200
     3 | Table Tennis   |          0 |         5 |           320 |                 10
(3 rows)

```
### Question
How can you retrieve the details of facilities with ID 1 and 5? Try to do it without using the OR operator.

### Answer
```shell
exercises=# select * from cd.facilities
exercises-# where facid in (1,5);
 facid |      name      | membercost | guestcost | initialoutlay | monthlymaintenance 
-------+----------------+------------+-----------+---------------+--------------------
     1 | Tennis Court 2 |          5 |        25 |          8000 |                200
     5 | Massage Room 2 |         35 |        80 |          4000 |               3000
(2 rows)

```

### Question
How can you produce a list of facilities, with each labelled as 'cheap' or 'expensive' depending on if their monthly maintenance cost is more than $100? Return the name and monthly maintenance of the facilities in question.

### Answer
```shell
exercises=# select name,
case
when monthlymaintenance > 100 then 'expensive'
else 'cheap'
exercises-# end as cost
exercises-# from cd.facilities;
      name       |   cost    
-----------------+-----------
 Tennis Court 1  | expensive
 Tennis Court 2  | expensive
 Badminton Court | cheap
 Table Tennis    | cheap
 Massage Room 1  | expensive
 Massage Room 2  | expensive
 Squash Court    | cheap
 Snooker Table   | cheap
 Pool Table      | cheap
(9 rows)

```

### Question
How can you produce a list of members who joined after the start of September 2012? Return the memid, surname, firstname, and joindate of the members in question.

### Answer
```shell
exercises=# select memid, surname, firstname, joindate
exercises-# from cd.members
exercises-# where joindate > '2012-09-01'::date;
 memid |      surname      | firstname |      joindate       
-------+-------------------+-----------+---------------------
    24 | Sarwin            | Ramnaresh | 2012-09-01 08:44:42
    26 | Jones             | Douglas   | 2012-09-02 18:43:05
    27 | Rumney            | Henrietta | 2012-09-05 08:42:35
    28 | Farrell           | David     | 2012-09-15 08:22:05
    29 | Worthington-Smyth | Henry     | 2012-09-17 12:27:15
    30 | Purview           | Millicent | 2012-09-18 19:04:01
    33 | Tupperware        | Hyacinth  | 2012-09-18 19:32:05
    35 | Hunt              | John      | 2012-09-19 11:32:45
    36 | Crumpet           | Erica     | 2012-09-22 08:36:38
    37 | Smith             | Darren    | 2012-09-26 18:08:45
(10 rows)

```

### Question
How can you produce an ordered list of the first 10 surnames in the members table? The list must not contain duplicates.
### Answer
```shell
exercises=# select distinct surname
exercises-# from cd.members 
exercises-# order by surname
exercises-# limit 10;
 surname 
---------
 Bader
 Baker
 Boothe
 Butters
 Coplin
 Crumpet
 Dare
 Farrell
 Genting
 GUEST
(10 rows)

```

### Question
You, for some reason, want a combined list of all surnames and all facility names. Yes, this is a contrived example :-). Produce that list!

### Answer
```shell
exercises=# select surname from cd.members 
exercises-# union
exercises-# select name from cd.facilities;
      surname      
-------------------
 Hunt
 Farrell
 Tennis Court 2
 Table Tennis
 Dare
 Rownam
 GUEST
 Badminton Court
 Smith
 Tupperware
 Owen
 Worthington-Smyth
 Butters
 Rumney
 Tracy
 Crumpet
 Purview
 Massage Room 2
 Sarwin
 Baker
 Pool Table
 Snooker Table
 Jones
 Coplin
 Mackenzie
 Boothe
 Joplette
 Stibbons
 Squash Court
 Tennis Court 1
 Pinker
 Genting
 Bader
 Massage Room 1
(34 rows)

exercises=# 

```
### Comments

The UNION operator does what you might expect: combines the results of two SQL queries into a single table. The caveat is that both results from the two queries must have the same number of columns and compatible data types.
UNION removes duplicate rows, while UNION ALL does not. Use UNION ALL by default, unless you care about duplicate results.


### Question
You'd like to get the signup date of your last member. How can you retrieve this information?

### Answer
```shell
exercises=# select max(joindate) as latest from cd.members;
       latest        
---------------------
 2012-09-26 18:08:45
(1 row)

```

### Comments
The MAX() function returns the maximum value of a specified column. In this case, it retrieves the most recent (latest) join date from the joindate column in the cd.members table.


### Question
You'd like to get the first and last name of the last member(s) who signed up - not just the date. How can you do that? 

### Answer
```shell
exercises=# select firstname, surname, joindate from cd.members 
where joindate = (select max(joindate) from cd.members);
 firstname | surname |      joindate       
-----------+---------+---------------------
 Darren    | Smith   | 2012-09-26 18:08:45
(1 row)

```