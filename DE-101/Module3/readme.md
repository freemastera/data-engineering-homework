# Модуль 3: Визуализация данных, дашборды и отчетность - Business Intelligence

## Домашняя работа для модуля 3
Плотно взялся за обучение по Tableau.
Прошел их основные курсы на официальном сайте. 
![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module3/img/1.jpg)
В начале covid эпидемии они раздавали промокод на 90 дней бесплатного обучения, чем я и воспользовался.
Сдача на сертификат стоит немалых денег, поэтому ограничился бейджами.
Ссылка на бейдж Tableau Analyst
https://www.youracclaim.com/badges/0fec76ee-aa2f-4741-ae38-99c5c162728d/public_url


Установил Tableau server в облако на AWS. Но, к сожалению, мощностей бесплатного тарифа не хватило, чтобы его развернуть.
Минимально необходимый по мощности сервер обойдется около 800 рублей в день, поэтому пришлось отказаться от этой затеи. 

Но зато потренировался в Tableau Online, благо интерфейсы очень похожи.
Загрузил туда свой первый дашборд в tableau. 
Отобразил на нем фактоиды с основными KPI и спарклайны. Также добавил сравнение с предыдущим годом. 2019(последний в статистике) и 2018. 
Сверил с excel(модуль 1) и с sql запросами к бд(модуль 2) - данные сошлись.

![image](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module3/img/2.jpg)


[Ссылка на сам dashboard в Tableau Public](https://public.tableau.com/views/datalearn-tableau-superstore-kpi/KPIDashboard?:language=en&:display_count=y&publish=yes&:origin=viz_share_link)

UPDATE: Обновил дашборд, добавив динамику по месяцам за предыдущий год. Все это в рамках одной визуализации через dual axis и LOD  с условием.
Линия - это статистика за последний год, area за прошлый.
Теперь можно быстро оценить, как KPI менялись по месяцам. В какие месяцы была просадка или наоборот взлет по сравнению с предыдущим годом. 
К тому же переверстал отчет для лучшего просмора с мобильного.
[Ссылка на обновленный дашборд](https://public.tableau.com/views/datalearn-tableau-superstore-kpi_year_over_year/KPIDashboard?:language=en&:display_count=y&publish=yes&:origin=viz_share_link)
<br>
UPDATE 2: Добавил отображение динамики цветом. Если график зеленый, то значит положительный тренд, если красный, то негативный. 
У avg discount цвет не стал менять, т.к сложно однозначно сказать. С одной стороны, чем больше скидка, тем меньше прибыль и это плохо. Но с другой стороны, возможно и продаж было больше из-за скидок.

UPDATE 3: Добавил дашборды [с когортным анализом](https://public.tableau.com/views/cohort_analysis_by_years/DashboardCohortAnalysis?:language=en&:retry=yes&:display_count=y&:origin=viz_share_link)
и [retention rate по месяцам](https://public.tableau.com/views/monthly_retention_rate/CohortAnalysis-month?:language=en&:display_count=y&publish=yes&:origin=viz_share_link)

UPDATE 4: Добавил дашборд [для детального продуктового анализа](https://public.tableau.com/views/product-analysis-dashboard/Dashboard?:language=en&:display_count=y&publish=yes&:origin=viz_share_link)


Загрузил [дашборды в формате .twbx на github](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module3/)
С этим форматом не нужно подключаться к источнику данных, которые у меня в amazon rds. Данные выгружены и идут в комплекте.
