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

Также загрузил [dashboard в формате .twbx на github](https://github.com/freemastera/data-engineering-homework/blob/master/DE-101/Module3/datalearn-tableau-superstore-kpi.twbx)
С этим форматом не нужно подключаться к источнику данных, которые у меня в amazon rds. Данные выгружены и идут в комплекте.
