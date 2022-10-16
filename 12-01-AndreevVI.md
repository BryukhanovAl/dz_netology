# Домашнее задание к занятию 12.1 "Базы данных.- Андреев В.И."


# Легенда

Заказчик передал Вам файл в формате Excel, в котором сформирован отчет.

На основе этого отчета, нужно выполнить следующие задания:

**Задание 1.**

Опишите таблицы (не менее 7), из которых состоит База данных:

какие данные хранятся в этих таблицах,
какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.
Приведите решение к следующему виду:

Сотрудники (

идентификатор, первичный ключ, serial,
фамилия varchar(50),
...
идентификатор структурного подразделения, внешний ключ, integer).
___

**Ответ**

Какие данные хранятся в этих таблицах :

1 фио  - фамилия имя и отчество сотрудника 

2 ОКЛАД  - заработная плата сотрудника

3 должность  - Занимаемая должность сотрудника

4 Тип подразделения - отдел в котором работает сотрудник

5 Дата - дата найма сотрудника

6 Адрес - местонахождение филиала

7 Проэкт - наименование проэкта для конкретного сотрудника.
___

Какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.

1 фио  -  строковый (varchar)

2 ОКЛАД  - числовой (decimal/numeric)

3 должность  - строковый (varchar)

4 Тип подразделения - строковый (varchar)

5 Дата - дата и время (tinyint)

6 Адрес - местонахождение филиала (varchar)

7 Проэкт - строковый (varchar)
___
решение к следующему виду: 


staff (
<<<<<<< HEAD

 Employee (ID), primary key, serial varchar(50),
 
 FName VARCHAR(50) ,
 
 LName VARCHAR(50) ,
 
 Patronymic varchar(50),
 
 Structura varchar(50),
 
 date_price datetime,
 
 position varchar(50),
 
 salary numeric,
 
 address VARCHAR(50),
 
 project VARCHAR(50),
 
 PRIMARY KEY(Id),
 
 FOREIGN KEY (ManagerId) REFERENCES Employees(Id).
 
=======
 staff_id primary_key
 FName_id VARCHAR(50) ,
 LName_id VARCHAR(50) ,
 Patronymic_id varchar(50),
 Structura_id varchar(50),
 divisions_id varchar(50),
 date_off_Employee datetime,
 position_id varchar(50),
 salary_id numeric,
 address_id VARCHAR(50),
 Employee's project_id VARCHAR(50),
>>>>>>> 085628c (initial commit)
)

Structura (
Structura_id primary_key
Group_id varchar(50)
structura_type 
Structura_title
)

divisions (
divisions_id primary_key
department_id varchar(50)
Unit Group_id varchar(50)
department_type
)

date_off_Employee )
date_off_id primary_key
date_id datetime
(

salary (
salary_id primary_key
pay_id numeric
)

branch address (
address_id primary_key
edge_id VARCHAR(50)
city_id VARCHAR(50)
street_id VARCHAR(50)
house_id VARCHAR(50)
)

Employee's project (
project_id primary_key
FName_id VARCHAR(50) ,
LName_id VARCHAR(50) ,
Patronymic_id varchar(50)
)



Дополнительные задания (со звездочкой*)
Эти задания дополнительные (не обязательные к выполнению) и никак не повлияют на получение вами зачета по этому домашнему заданию. Вы можете их выполнить, если хотите глубже и/или шире разобраться в материале.

# Задание 2*.
Перечислите, какие, на Ваш взгляд, в данной денормализованной таблице встречаются функциональные зависимости и какие правила вывода нужно применить, чтобы нормализовать данные.
