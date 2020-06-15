# Домашняя работа для модуля 2

## Модель данных
![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/data_model_superstore.jpg)

profuct_id, к сожалению, [не уникальный](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/product_id%20%D0%BD%D0%B5%20%D1%83%D0%BD%D0%B8%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9.jpg). 
Поэтому сгенерировал отдельный айдишник. Для менеджеров тоже взял суррогатный, фамилия может меняться.

## Запросы для создания таблиц
<ol>
<li>Оригинальные денормализованные:<br><br>
[orders](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/orders.sql)<br>
[people](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/people.sql)<br>
[returns](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/returns.sql)<br>
 </li>
<br><br>
<li>Нормализованные по схеме "Звезда":<br><br>
 [Создание таблиц](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/dm_create_tables.txt)<br>
 [Вставка данных в таблицы измерений](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/dm_insert_dim_tables.txt)<br>
   [Вставка данных в таблицу фактов](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/dm_insert_fact_tables.txt)<br><br>
    
  </li>

## SELECT запросы для проверки
<ol>
<li>
[SELECT метрик из таблицы order и измерений из dim таблиц](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/select_dim_tables_and_orders.txt)</li><br>
![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/select_dim_tables_and_orders.jpg)
 <br><br>
<li>[SELECT метрик из таблицы фактов и измерений из dim таблиц](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/dm_select_dim_tables_and_facts.txt)</li><br>

![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module2/img/select_dim_tables_and_facts.jpg)

