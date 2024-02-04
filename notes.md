## Notes From SQLite Studios:

## Northwind.db3 practice

--select
    --*
--from orders as o
--join shippers as s
    --on o.shipperid = s.shipperid;

--this says I want to get all of the records from Orders(and alias Orders as simply 'o')
--THEN I want to add shippers(which I want to alias as 's') as well to the table, combining them essentially

--select
    --o.orderid,
    --o.orderdate,
    --s.shippername
--from orders as o
--join shippers as s
    --on o.shipperid = s.shipperid;

--This one only combines the orderid from orders, the orderdate from orders, and the shippername from shippers!

--technically orderid, orderdate, AND shippername are unambiguous and are only present in 1 of the tables we want to show.
--Because of that we dont HAVE to put o. or s. in front of them(I just choose to)

--select
    --orderid,
    --orderdate,
    --shippername
--from orders as o
--join shippers as s
    --on o.shipperid = s.shipperid
--group by s.shipperid;

--this collapses all the rows until there are only 3(since there are only 3 Shipper Companies)

--select
    --count(orderid) as ordercount,
    --shippername
--from orders as o
--join shippers as s
    --on o.shipperid = s.shipperid
--group by s.shipperid
--order by ordercount;

--This, even though it still has the companies collapsed down to just the 3 names
--IT COUNTS how many times each id was present! Speedy-54 / United-74 / Federal-68!
-- aliased line 35 to ORDERCOUNT but it could have just been written like this / count(orderid),
-- The last line just put them in numerical order by the amount of ordercounts (can put desc to make it greater than first)

--select
    --o.orderid,
    --o.orderdate,
    --(e.firstname || ' ' || e.lastname) as employee
--from orders as o
--join employees as e
    --on o.employeeid = e.employeeid

--lists a list of orderid along with the order dates and the full names of the employees involved with the order 'aggregated'/concatenated togather!

--select
--count(o.orderid) as orders,
    --(e.firstname || ' ' || e.lastname) as employee
--from orders as o
--join employees as e
    --on o.employeeid = e.employeeid
--group by e.employeeid;

--This makes it where it shows all of the employees who have worked on orders before
--Also shows the number of orders they have participated in
-- as well as, does not show the name of the 1 employee who has NOT dealt with an order (Adam West LOL)
-- THESE HAVE BEEN INNER JOINS

--An example of a LEFT JOIN (outer join) would be:
--to show the employee without an order under his belt, it needs to be 'moved to the left' which is by from

--select
--count(o.orderid) as orders,
    --(e.firstname || ' ' || e.lastname) as employee
--from employees as e
--left join orders as o
    --on o.employeeid = e.employeeid
--group by e.employeeid;

--the orders and the employees places should be swapped!
--the keyword left should also be added in front of the join!
--This time it shows all of the same data from earlier except for one thing:
--ADAM WEST HAS BEEN ADDED WITH THE COUNT OF 0 ORDERS BY HIS NAME LOL
--If, for example, we were to put orderdate in the function as well, the orderdate by Adam West would be NULL

## Blog.db3 practice

--select
    --*
--from posts as p
--join users as u
    --on p.user_id = u.id

-- CAREFUL!! The foreign id inside posts (p.user_id) and the one inside users (u.id) are given 2 different names!
--Though they are talking about the same thing
--When this is ran, it doesn't show the the 12th post that doesn't have a user_id

--select
    --p.id as post_id,
    --p.contents,
    --u.username
--from posts as p
--join users as u
    --on p.user_id = u.id

--shows the id(aliased as post_id) as well as the pontents from inside of posts and the username from inside of users!
--Almost the exact sequence the findPosts function inside of user-model.js is asking for!

--Because hypatia doesn't have a quote/post, when we run a get request for his posts, we get an empty array ([])
--next we need to do the configuration of the find function!

 --select
     --u.id as user_id,
     --u.username,
     --count(p.id) as post_count
 --from users as u
 --join posts as p
     --on u.id = p.user_id
 --group by u.id

--this works to get the philosophers and tells the amount of posts they have but there is one problem:
--HYPATIA is never shown/mentioned!
--remember, because there wasn't any information joining her in, we would need a left join to pull her up!

 --select
     --u.id as user_id,
     --u.username,
     --count(p.id) as post_count
 --from users as u
 --left join posts as p
     --on u.id = p.user_id
 --group by u.id;

--this works with virtually the same code because users (what we were trying to find all of) was already on the LEFT TABLE!

 --select
     --u.id as user_id,
     --u.username,
     --p.contents,
     --p.id as post_id
 --from users as u
 --left join posts as p
     --on u.id = p.user_id
 --where u.id = 1;

--Works fine for the findById one!!


--How to return Hypatia's stolen post??
--update posts
    --set user_id = 4
--where id = 12;

--now Hypatia has her post posted!
