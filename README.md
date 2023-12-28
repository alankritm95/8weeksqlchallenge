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






