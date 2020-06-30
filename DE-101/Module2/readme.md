# Домашняя работа для модуля 2

## Модель данных
![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/data_model_superstore.jpg)

product_id, к сожалению, [не уникальный](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/product_id%20%D0%BD%D0%B5%20%D1%83%D0%BD%D0%B8%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9.jpg). 
Поэтому сгенерировал отдельный айдишник. Для менеджеров тоже взял суррогатный, фамилия может меняться.

## Запросы для создания таблиц

<ol>
<li>Оригинальные денормализованные:<br><br>
orders.sql<br>
people.sql<br>
returns.sql<br>
 </li>
<br><br>
<li>Нормализованные по схеме "Звезда":<br><br>
dm_create_tables.txt -создание таблиц<br>
dm_insert_dim_tables.txt - вставка данных в таблицы измерений<br>
dm_insert_fact_tables.txt -вставка данных в таблицу фактов]<br><br>
    
  </li>

## SELECT запросы для проверки

select_dim_tables_and_orders.txt - SELECT  метрик из таблицы orders, а измерений из dim таблиц<br>
 
![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/select_dimtables_and_orders.jpg)
 <br><br>
 
SELECT метрик из таблицы фактов, а измерений из dim таблиц<br>

![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/select_dimtables_and_facts.jpg)

## Запросы в sql, чтобы ответить на вопросы из [модуля 01](https://github.com/Data-Learn/data-engineering/tree/master/DE-101/Module-01/Lab#%D0%B0%D0%BD%D0%B0%D0%BB%D0%B8%D1%82%D0%B8%D0%BA%D0%B0-%D0%B2-excel)



 ### Overview (обзор ключевых метрик)

  #### Total Sales <br>
  select round(sum(sales),0) from facts f 
  <br>
  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/1.png)
 <br><br>
  #### Total Profit <br>
  select round(sum(profit),0) from facts <br>
  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/2.png)
 <br><br>
  #### Profit Ratio <br>
select ROUND(sum(profit)/sum(sales),2) from facts
  <br>
  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/3.png)
 <br><br>
  
  #### Profit per Order <br>
select ROUND(sum(f.profit) / count(o.order_id),0) from facts f<br>
join dim_orders o on o.order_id =f.order_id 
<br>
  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/4.png)
 <br><br>
 
   #### Sales per Customer <br>
select ROUND(sum(f.sales) / count(c.customer_id),0) from facts f <br>
join dim_customers c on c.customer_id =f.customer_id  
<br>
  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/5.png)
 <br><br>
  #### Avg. Discount <br>
 select ROUND(avg(discount),2) from facts 
<br>
  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/6.png)
 <br><br>
 
  #### Monthly Sales by Segment  <br>
select EXTRACT(year FROM d.order_date) as year,EXTRACT(month FROM d.order_date) as month,sum(f.sales),c.segment from facts f <br>
join dim_dates d on d.order_date =f.order_date  <br>
join dim_customers c on c.customer_id =f.customer_id <br>
group by c.segment,year,month <br>
order by year DESC,month DESC,segment  <br>
<br>
  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/7.png)
 <br><br>

  #### Montly Sales by Product Category  <br>
  select EXTRACT(year FROM d.order_date) as year,EXTRACT(month FROM d.order_date) as month,sum(f.sales),p.category from facts f <br>
join dim_dates d on d.order_date =f.order_date  <br>
join dim_products p on p.prod_id =f.prod_id <br>
group by p.category,year,month <br>
order by year DESC,month DESC,p.category  <br>
<br>
  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/8.png)
 <br><br>
   
### Product Dashboard (Продуктовые метрики)
#### Sales by Product Category over time (Продажи по категориям) <br>
select d.order_date as month,sum(f.sales),p.category from facts f<br>
join dim_dates d on d.order_date =f.order_date <br>
join dim_products p on p.prod_id =f.prod_id<br>
group by p.category,d.order_date<br>
order by d.order_date DESC,p.category<br>
  <br>
  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/9.png)
 <br><br>

### Customer Analysis
#### Sales and Profit by Customer <br>
select sum(f.sales) as sales,sum(f.profit) as profit,c.segment from facts f<br>
join dim_customers c on c.customer_id =f.customer_id<br>
group by c.segment<br>
order by segment <br>
  <br>
  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/10.png)
 <br><br>
 #### Customer Ranking <br>
??? Нужна формула
 <br><br>
 #### Sales per region <br>
select m.region, sum(f.sales) as sales from facts f<br>
join dim_managers m on m.manager_id =f.manager_id<br>
group by region<br>
order by sales DESC<br>
  <br>
  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/11.png)
 <br><br>
 
 ## Зарегестрировался в Amazon Web Services(AWS) и добавил данные в базу данных в облако<br>
 ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/aws_db.jpg)
 <br><br>
 
  ## Подключился к базе данных в облаке из Data Sudio и создал визуализацию<br>
  
 С датой в поле order_date возникли проблемы. Data studio путал месяц и день, поэтому в запросе создал новое поле FormattedDate с преобразованным форматом даты.
 
 `
select *,to_char(f.order_date, 'YYYY-MM-DD') AS FormattedDate from facts f 
join dim_dates d on d.order_date =f.order_date 
join dim_customers c on c.customer_id =f.customer_id 
join dim_products p on p.prod_id =f.prod_id
join dim_orders o on o.order_id =f.order_id 
join dim_managers m on m.manager_id =f.manager_id `

<br><br>
Ссылка на отчет в Data Studio
<br>
https://datastudio.google.com/reporting/f31df262-28da-46e6-bf50-068a8fd3589c
