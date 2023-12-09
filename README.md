# SQL-Project
Used MySQL to analyse data stored in database 'Awesome Chocolate'

Please find the script below:

show tables;

/* The above query gives me all the tables stored in the database*/

select * from sales;

/* The above query gives me all the data stored in sales table*/

select saledate, amount, customers from sales;

/* The above query gives me the mentioned columns from sales table

select saledate, amount, boxes, amount/boxes as 'amount per box' from sales;

/* The above query gives me the mentioned columns along with the calculated column 'amount per box' from sales table*/

select * from sales where amount>10000;

/* The above query gives me all the data stored in sales table where the amount is greater than 10000*/

select * from sales where amount>10000 order by amount;

/* The above query gives me all the data stored in sales table where the amount is greater than 10000 in the ascending order of amount*/

SELECT * FROM sales WHERE amount > 10000 ORDER BY amount DESC;
/* The above query gives me all the data stored in sales table where the amount is greater than 10000 in the descending order of amount*/
select * from sales where geoid='g1' order by pid, amount desc;
/* The above query gives me all the data stored in sales table where the geoid is g1 and order it by ascending order of pid and descending order of amount*/
select * from sales where amount>10000 and saledate>'2022-01-01';
/* The above query gives me all the data stored in sales table where amount is greater than 10000 and saledate is greater than '2022-01-01' */
select saledate, amount from sales where amount>10000 and year(SaleDate)=2022 order by amount desc;
/* The above query gives me all the data stored in sales table where amount is greater than 10000 and year of saledate is 2022 and order by descending order of amount*/
select sum(amount) as 'total sales in 2022' from sales where amount>10000 and year(SaleDate)=2022;
/* The above query gives me the total sales in the year 2022*/
select * from sales where boxes between 1 and 50 order by boxes;
/* The above query gives me all the data stored in sales table where the number of boxes is between 1 and 50*/
select saledate, amount, boxes, weekday(saledate) as 'Day of week' from sales where weekday(saledate)=4;
/* The above query gives me saledate, amount, boxes of weekday number of saledate from sales table where weekday number is 4*/
select * from people;
/* The above query gives me all the data stored in people table*/
select * from people where team = 'Delish' or team = 'Jucies';
/* The above query gives me all the data stored in people table where team is either "Delish' or 'Jucies'*/
select * from people where team in ('Delish','Yummies','Jucies');
/* The above query gives me all the data stored in people table people where team is either "Delish' or 'Jucies' or 'Yummies'*/
select * from people where salesperson like 'B%';
/* The above query gives me all the data stored in people table people where salesperson name starts with 'B"*/
select SaleDate, amount,
	case  when amount < 1000 then 'Under 1K'
          when amount < 5000 then 'Under 5K'
		  when amount < 10000 then 'Under 10K'
          else '10K or more'
     end as 'Amount Category'
  from sales;   
  /* The above query gives me saledate, amoubt column from sales sales along with Amount Category table where is categorises amount as per the given condition*/
  select s.saledate, s.amount, p.salesperson,p.spid 
  from sales s 
  join people p on s.spid=p.spid;
  /* The above query gives me saledate, amount, salesperson and spid column from sales and people table by joining sales and people table by column spid*/
  select s.saledate,s.amount,pr.product
  from sales s 
  left join products pr on s.pid=pr.pid;
  /* The above query gives me saledate, amount, product from sales and product table by joining sales and product table by column pid */
  select s.saledate, s.amount, p.salesperson,pr.product,p.team
  from sales s 
  join people p on s.spid=p.spid
  join products pr on s.pid=pr.pid;
  /* The above query gives me saledate, amount, product, salesperson,team from sales, product and people table by joining sales and product table by column pid and by joining sales and people table by column spid */
  select s.saledate, s.amount, p.salesperson,pr.product,p.team
  from sales s 
  join people p on s.spid=p.spid
  join products pr on s.pid=pr.pid
  where s.amount <500 and p.team ='Delish';
  /* The above query gives me saledate, amount, product, salesperson,team from sales, product and people table by joining sales and product table by column pid and by joining sales and people table by column spid where amount < 500 and team is 'Delish' */
  select s.saledate, s.amount, p.salesperson,pr.product,p.team,g.geo as 'Geography'
  from sales s 
  join people p on s.spid=p.spid
  join products pr on s.pid=pr.pid
  join geo g on g.geoid=s.geoid
  where s.amount <500 and p.team ='Delish' and g.geo in ('New Zealand','India');
  /* The above query gives me saledate, amount, product, salesperson,team,geography from sales, product,geo and people table by joining sales and product table by column pid and by joining sales and people table by column spid and geo and sales table by column geoid where amount < 500 and team is 'Delish' and geography is New Zealand or India */
  select geoid, sum(amount) as 'Total Amount', avg(amount) as 'Average Amount'
  from sales 
  group by geoid;
  /* The above query gives me geoid, sum of amount and average of amount by each group of geoid*/
  select g.geo as 'Geography', sum(amount),avg(amount),sum(boxes)
  from sales s 
  join geo g on s.geoID = g.geoID
  group by geo;
  /* The above query gives me geography, sum of amount and average of amount and su, of boxes by joining sales and geo table by column geoid by each group of geography*/
  
  
