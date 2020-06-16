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

## Запросы в sql, чтобы ответить на вопросы из модуля 01
https://github.com/Data-Learn/data-engineering/tree/master/DE-101/Module-01/Lab#%D0%B0%D0%BD%D0%B0%D0%BB%D0%B8%D1%82%D0%B8%D0%BA%D0%B0-%D0%B2-excel


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

 

