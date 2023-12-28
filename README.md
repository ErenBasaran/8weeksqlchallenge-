--What is the total amount each customer spent at the restaurant?-- <br>

Solution : <br>

select s.customer_id, sum(m.price) from sales as s
join menu as m on m.product_id = s.product_id
group by s.customer_id
order by s.customer_id ; <br>

--How many days has each customer visited the restaurant?-- <br>

Solution : <br>

select s.customer_id, count(distinct s.order_date) from sales as s
join menu as m on m.product_id = s.product_id
group by s.customer_id
order by s.customer_id ;


--What was the first item from the menu purchased by each customer?-- <br>

Solution : <br>

select s.customer_id, m.product_name, min(s.order_date) from sales as s
join menu as m on m.product_id = s.product_id
where s.order_date in(select min_order_date from (
							select customer_id, min(order_date) as min_order_date from sales
							group by customer_id
							order by customer_id))
group by s.customer_id, m.product_name
order by s.customer_id ; <br>

--What is the most purchased item on the menu and how many times was it purchased by all customers?-- <br>

Solution : <br>

select s.product_id, m.product_name, count(s.customer_id) as tatal_sales from sales as s
join menu as m on m.product_id = s.product_id
group by s.product_id, m.product_name
order by s.product_id desc
limit 1 ; <br>


