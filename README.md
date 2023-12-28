# 🍜 🍛 🍣 Case Study #1: Danny's Diner

![image](https://github.com/alankritm95/8weeksqlchallenge/assets/129503746/2bdc7367-1f13-447d-9183-59e055475c83)

Please access the case study by clicking [here](https://8weeksqlchallenge.com/case-study-1/)

## Introduction

Danny has a deep passion for Japanese cuisine, leading him to take a bold step at the start of 2021. He opens a charming eatery featuring his top three favorite dishes: sushi, curry, and ramen.

Now, Danny's Diner seeks your support to ensure the restaurant's success. Despite collecting fundamental data during the initial months of operation, the team is unsure about leveraging this information to effectively manage and enhance their business.

## Issue Overview

Danny aims to utilize the gathered data to address specific inquiries about his clientele, particularly focusing on their visitation patterns, expenditure, and preferred menu items. Establishing a more profound understanding of his customers will enable him to provide an enhanced and personalized dining experience for his loyal patrons. He envisions utilizing these insights to determine the feasibility of expanding the existing customer loyalty program.

## Utilized Datasets

Three pivotal datasets form the foundation of this case study:

1. **Sales Dataset:**
   The sales table comprehensively records individual customer purchases, including customer_id, order_date, and product_id details, shedding light on when and what menu items were ordered.

2. **Menu Dataset:**
   The menu table serves as a key reference, mapping product_id to corresponding product_name and price for each menu item.

3. **Members Dataset:**
   The members table plays a crucial role by documenting the join_date when a customer_id becomes part of the beta version of Danny's Diner loyalty program.

## Question and Solution

### 1. What is the total amount each customer spent at the restaurant?
   
Select customer_id, sum(price) from sales s join menu m on 
s.product_id = m.product_id group by customer_id
order by customer_id;

![image](https://github.com/alankritm95/8weeksqlchallenge/assets/129503746/f388d606-b1dc-498c-b265-6f3121cbaaaa)

### 2. How many days has each customer visited the restaurant?

select customer_id, count(distinct order_date) as total_days from sales group by customer_id;

![image](https://github.com/alankritm95/8weeksqlchallenge/assets/129503746/92707033-eef8-42b7-a29f-4fd77ca264b8)

### 3. What was the first item from the menu purchased by each customer?

with cte as 
(select customer_id, product_name, dense_rank() over(partition by customer_id order by order_date) as dr from sales s join menu m 
on s.product_id = m.product_id )

select customer_id, product_name from cte where dr = 1 group by customer_id, product_name;

![image](https://github.com/alankritm95/8weeksqlchallenge/assets/129503746/34aa1f8e-294b-4173-8707-d9e24b7e4a05)

### 4. What is the most purchased item on the menu and how many times was it purchased by all customers?

Select product_name, count(product_name) as total_count from sales s join menu m on
s.product_id = m.product_id group by product_name order by total_count desc limit 1;

![image](https://github.com/alankritm95/8weeksqlchallenge/assets/129503746/161d53e8-f5ed-40a1-a757-e10232f65f71)

### 5. Which item was the most popular for each customer?

with cte as (
  SELECT product_name,
          customer_id,
          count(product_name) AS order_count,
          rank() over(PARTITION BY customer_id
                      ORDER BY count(product_name) DESC) AS rank_number
   FROM menu
   INNER JOIN sales ON menu.product_id = sales.product_id
   GROUP BY customer_id,
            product_name
            )
  select product_name,
          customer_id, order_count from cte where rank_number = 1;     

![image](https://github.com/alankritm95/8weeksqlchallenge/assets/129503746/32f58547-cab3-452d-b019-6b8d214db6ec)

### 6. Which item was purchased first by the customer after they became a member?

with cte as(
select m.customer_id, product_id, order_date, 
dense_rank() over(partition by m.customer_id order by order_date) as rnk
from sales s right join members m
on s.customer_id = m.customer_id and
order_date >= join_date)

select customer_id, product_name from cte join menu on
 cte.product_id = menu.product_id
 where rnk = 1 order by customer_id;

 ![image](https://github.com/alankritm95/8weeksqlchallenge/assets/129503746/ee7ba277-6b6b-4976-a10f-13c9561c13c0)


 












