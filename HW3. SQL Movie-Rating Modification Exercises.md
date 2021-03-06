Q1.
Add the reviewer Roger Ebert to your database, with an rID of 209.

```sql
insert into reviewer values(209, 'Roger Ebert')
```

Q2.
Insert 5-star ratings by James Cameron for all movies in the database. Leave the review date as NULL.

```sql
insert into rating
select rid, mid, 5, null
from reviewer, movie
where name='James Cameron'
```

Q3.
For all movies that have an average rating of 4 stars or higher, add 25 to the release year. (Update the existing tuples; don't insert new tuples.)

```sql
Update movie set year=year+25
where mid in (select mid from rating
group by mid
having avg(stars)>=4);
```

Q4.
Remove all ratings where the movie's year is before 1970 or after 2000, and the rating is fewer than 4 stars. 

```sql
delete from rating
where mid in
(select mid from movie
where year<1970 or year>2000
group by mid
having avg(stars)<4)
```