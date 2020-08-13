# Домашняя работа для модуля 2

## Dimensional modeling. Star schema
![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/star_model.jpg)

product_id, к сожалению, [не уникальный](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/nonunique_productid.jpg). 
Поэтому сгенерировал отдельный айдишник. Для менеджеров тоже взял суррогатный, фамилия может меняться.

## Запросы для создания таблиц

<ol>
<li>Оригинальные, как в excel документе:<br><br>
stg.orders.sql<br>
stg.people.sql<br>
stg.returns.sql<br>
 </li>
<br><br>
<li>Нормализованные по схеме "Звезда":<br><br>
dw_create_tables.sql -создание таблиц<br>
dw_insert_dimensions.sql - вставка данных в таблицы измерений<br>
dw_insert_facts.sql -вставка данных в таблицу фактов<br><br>
    
  </li>

## SELECT запросы для проверки

Выбираем метрики из stg.orders, а измерения из dw.dim_*<br>


```sql
select
o.sales,
o.quantity,
o.discount,
o.profit,
c.customer_id, 
c.customer_name,
c.segment,
d.order_date,
m.manager_id, 
m.person,
m.region,
p.prod_id,
p.product_id,
p.product_name,
p.category,
p.sub_category,
ord.order_id,
ord.ship_mode,
ord.ship_date,
ord.country,
ord.state,
ord.city,
ord.postal_code,
ord.returned 
from stg.orders o inner join dw.dim_customers c on o.customer_id = c.customer_id
join dw.dim_dates d on o.order_date = d.order_date
join dw.dim_managers m on o.region = m.region
join dw.dim_products p on o.product_id = p.product_id and p.product_name= o.product_name 
join dw.dim_orders ord on o.order_id = ord.order_id
```


 
![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/1.jpg)
 <br><br>
 
Выводим все записи из нормализованных таблиц
<br>

```sql
select * from dw.facts f 
join dw.dim_customers c on c.customer_id =f.customer_id 
join dw.dim_products p on p.prod_id =f.prod_id
join dw.dim_orders o on o.order_id =f.order_id 
join dw.dim_dates d on d.order_date =f.order_date 
join dw.dim_managers m on m.manager_id =f.manager_id 
```

![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/2.jpg)
<br><br>
Получаем 9993, хотя в примере выше 9994. И в экселе тоже 9994(без строки с заголовками). Почему так? Дело в том что, в исходном файле, есть один дубль строки.
Если мы выполним предыдущий запрос, добавив DISTINCT, то тоже получим 9993.
В экселе, если удалить столбец с суррогатным id (первый столбец Row ID), а затем удалить дубликаты, то также будет 9993 строк.


![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/3.jpg)
<br><br>
Поэтому мой расчеты могут немного отличаться от расчетов других пользователей.
В первом модуле я также поправил дашборд с ДЗ, удалив лишнюю строку. Соотвественно данные пересчитались и стали немного отличаться от
[оригинала](https://github.com/Data-Learn/data-engineering/blob/master/DE-101/Module-01/Lab/Sample%20-%20Superstore%20-%20Dashboard.xlsx)




## Ниже будут запросы в sql, чтобы ответить на вопросы из [модуля 01](https://github.com/Data-Learn/data-engineering/tree/master/DE-101/Module-01/Lab#%D0%B0%D0%BD%D0%B0%D0%BB%D0%B8%D1%82%D0%B8%D0%BA%D0%B0-%D0%B2-excel)



 ### Overview (обзор ключевых метрик)

  #### Total Sales <br>
```sql
select round(sum(sales),0) from dw.facts f
```

  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/1.jpg)
 <br><br>
  #### Total Profit <br>
```sql
select round(sum(profit),0) from dw.facts
```

  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/2.jpg)
  
 <br><br>
  #### Profit Ratio <br>
```sql
select ROUND(sum(profit)/sum(sales),2) from dw.facts
```

  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/3.jpg)
 <br><br>
  
  #### Profit per Order <br>
```sql
select ROUND(sum(f.profit) / count(distinct f.order_id),0) from dw.facts f
join dw.dim_orders o on o.order_id =f.order_id  
```

  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/4.jpg)
 <br><br>
 
   #### Sales per Customer <br>
```sql
select ROUND(sum(f.sales) / count(DISTINCT c.customer_id),0) from dw.facts f
join dw.dim_customers c on c.customer_id =f.customer_id
``` 

  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/5.jpg)
 <br><br>
  #### Avg. Discount <br>
```sql
select ROUND(avg(discount),2) from dw.facts
```


  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/6.jpg)
 <br><br>
 
  #### Monthly Sales by Segment  <br>
```sql
select EXTRACT(year FROM d.order_date) as year,EXTRACT(month FROM d.order_date) as month,sum(f.sales),c.segment from dw.facts f
join dw.dim_dates d on d.order_date =f.order_date
join dw.dim_customers c on c.customer_id =f.customer_id
group by c.segment,year,month
order by year DESC,month DESC,segment
```

  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/7.jpg)
 <br><br>

  #### Montly Sales by Product Category  <br>
```sql
select EXTRACT(year FROM d.order_date) as year,EXTRACT(month FROM d.order_date) as month,sum(f.sales),p.category from dw.facts f
join dw.dim_dates d on d.order_date =f.order_date
join dw.dim_products p on p.prod_id =f.prod_id
group by p.category,year,month
order by year DESC,month DESC,p.category
```

  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/8.jpg)
 <br><br>
   
### Product Dashboard (Продуктовые метрики)
#### Sales by Product Category over time (Продажи по категориям) <br>
```sql
select d.order_date as month,sum(f.sales),p.category from dw.facts f
join dw.dim_dates d on d.order_date =f.order_date
join dw.dim_products p on p.prod_id =f.prod_id
group by p.category,d.order_date
order by d.order_date DESC,p.category
```

  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/9.jpg)
 <br><br>

### Customer Analysis
#### Sales and Profit by Customer <br>
```sql
select sum(f.sales) as sales,sum(f.profit) as profit,c.segment from dw.facts f
join dw.dim_customers c on c.customer_id =f.customer_id
group by c.segment
order by segment
```

  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/10.jpg)
 <br><br>
 #### Customer Ranking <br>
??? Нужна формула
 <br><br>
 #### Sales per region <br>
```sql
select m.region, ROUND(sum(f.sales)) as sales from dw.facts f
join dw.dim_managers m on m.manager_id =f.manager_id
group by region
order by sales DESC
```

  ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/mod1/11.jpg)
 <br><br>
 
 ## Зарегестрировался в Amazon Web Services(AWS) и добавил данные в базу данных в облако<br>
 
  ### Amazon Lightsail<br>
 ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/aws_db.jpg)
 <br><br>
 
 Так как в Lightsail бесплатный доступ только на месяц, потом перенес базу данных в Amazon RDS (где бесплатных 12 месяцев).
 Заодно добавил схемы stg и dw 
 
 ![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/aws_rds.jpg)
 <br><br>
 
  ## Подключился к базе данных в облаке из Data Sudio и создал визуализацию<br>
  
 С датой в поле order_date возникли проблемы. Data studio путал месяц и день, поэтому в запросе создал новое поле FormattedDate с преобразованным форматом даты.
 
```sql
select *,to_char(f.order_date, 'YYYY-MM-DD') AS FormattedDate from dw.facts f 
join dw.dim_dates d on d.order_date =f.order_date 
join dw.dim_customers c on c.customer_id =f.customer_id 
join dw.dim_products p on p.prod_id =f.prod_id
join dw.dim_orders o on o.order_id =f.order_id 
join dw.dim_managers m on m.manager_id =f.manager_id
```

<br><br>
Ссылка на отчет в Data Studio
<br>
https://datastudio.google.com/reporting/f31df262-28da-46e6-bf50-068a8fd3589c
