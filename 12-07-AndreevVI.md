# Домашнее задание к занятию 12.7 "Репликация и масштабирование. Часть 2" -Андреев В.И.


Любые вопросы по решению задач задавайте в чате учебной группы.

# Задание 1.
Опишите основные преимущества использования масштабирования методами:

активный master-сервер и пассивный репликационный slave-сервер,
master-сервер и несколько slave-серверов,
активный сервер со специальным механизмом репликации – distributed replicated block device (DRBD), SAN-кластер.
Дайте ответ в свободной форме.
___
**Ответ:**
Репликация мастер-мастер - Преимуществом является гибкость, поскольку каждый участвующий экземпляр базы данных хорошо инкапсулирован, а сценарии гибридной репликации возможны с несколькими наборами мастеров. 
___
Репликация Master-Slave - Преимущество заключается в том, чтобы избежать использования очень дорогих запасных серверов, простаивающих в большинстве случаев.
___
master-slave. уменьшает нагрузку на основной сервер.
___
master-slave-slave-...уменьшает в разы нагрузку и скорость чтения информации пропорционально увеличению колличества slave серверов
___
master-drbd. по сути преимущество только в увеличении отказоустойчивости
___
SAN-кластер - быстродействие и масштабируемость, центральное управление и резервирование данных без загрузки локальной сети и серверов.


# Задание 2.
Разработайте план для выполнения горизонтального и вертикального шаринга базы данных. База данных состоит из трех таблиц:

пользователи,
книги,
магазины (столбцы произвольно).

Опишите принципы построения системы и их разграничение или (и) разбивку между базами данных.

Пришлите блок схему, где и что будет располагатся. Опишите, в каких режимах будут работать сервера.
___
**Ответ:**
База данных состоит из трех таблиц:

пользователи,
книги,
магазины.

# Вертикальный шардинг

Каждая таблица находится на отдельном сервере. 


![Вертикальное шардирование ](https://user-images.githubusercontent.com/94833070/200164189-4bde1720-e2bd-40de-9d1a-3943297397db.png)





# Горизонтальный шардинг
таблица Books разделена на 2 сервера по названию книги от A-N и от O-Z
таблица Users разделена по тоже разделена на 2 сервера по принципу аутонтификации и данных users
таблица Stores была перенесена полностью в отдельный сервер без изменений 


![Снимок экрана от 2022-11-06 01-49-39](https://user-images.githubusercontent.com/94833070/200164193-2e558350-6133-4a6a-87c4-4e302dc43479.png)




# Дополнительные задания (со звездочкой*)
Эти задания дополнительные (не обязательные к выполнению) и никак не повлияют на получение вами зачета по этому домашнему заданию. Вы можете их выполнить, если хотите глубже и/или шире разобраться в материале.

# Задание 3*.
Выполните настройку выбранных методов шардинга из задания 2.

Пришлите конфиг docker и sql скрипт с командами для базы данных
___
**Ответ:**