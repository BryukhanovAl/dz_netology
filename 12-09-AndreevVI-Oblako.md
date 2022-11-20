# Домашнее задание к занятию 12.09 "Базы данных в облаке"- Андреев В.И.
Домашнее задание выполните в Google Docs и отправьте в личном кабинете на проверку ссылку на ваш документ.

Используйте следующие рекомендации во избежание лишних трат в Яндекс.Облаке:

Сразу после выполнения задания удалите кластер;
Если вы решили взять паузу на выполнение задания, то остановите кластер.

# Задание 1
Создание кластера

Перейдите на главную страницу сервиса Managed Service for PostgreSQL.

Создайте кластер PostgreSQL со следующими параметрами:

Класс хоста: s2.micro, диск network-ssd любого размера;

Хосты: нужно создать два хоста в двух разных зонах доступности и указать необходимость публичного доступа (публичного IP адреса) для них;

Установите учетную запись для пользователя и базы.

Остальные параметры оставьте по умолчанию либо измените по своему усмотрению.

Нажмите кнопку "Создать кластер" и дождитесь окончания процесса создания (Статус кластера = RUNNING). Кластер создается от 5 до 10 минут.

Подключение к мастеру и реплике

Используйте инструкцию по подключению к кластеру, доступную на вкладке "Обзор": cкачайте SSL сертификат и подключитесь к кластеру с помощью утилиты psql, указав hostname всех узлов и атрибут 

target_session_attrs=read-write.

Проверьте, что подключение прошло к master-узлу.

select case when pg_is_in_recovery() then 'REPLICA' else 'MASTER' end;

Посмотрите количество подключенных реплик:

select count(*) from pg_stat_replication;

Проверьте работоспособность репликации в кластере

Создайте таблицу и вставьте одну-две строки.**

CREATE TABLE test_table(text varchar);

insert into test_table values('Строка 1');


Выйдите из psql командой \q.

Теперь подключитесь к узлу-реплике. Для этого из команды подключения удалите атрибут 

target_session_attrs ,

 и в параметре атрибут host передайте только имя хоста-реплики. 

 Роли хостов можно посмотреть на соответствующей вкладке UI консоли.

Проверьте, что подключение прошло к узлу-реплике.

select case when pg_is_in_recovery() then 'REPLICA' else 'MASTER' end;

Проверьте состояние репликации**

select status from pg_stat_wal_receiver;

Для проверки, что механизм репликации данных работает между зонами доступности облака, выполните запрос к таблице, созданной на предыдущем шаге:

 select * from test_table;

По итогу пришлите скриншоты:

Созданной базы данных;
Результата вывода команды на реплике select * from test_table;.
___

**Ответ**

## **Создание кластера**

Перехожу на главную страницу сервиса Managed Service for PostgreSQL.

Создаю кластер PostgreSQL со следующими параметрами:

Класс хоста: s2.micro, диск network-ssd любого размера;


Установаю учетную запись для пользователя -andreevvi и базы -bd_andreevvi

___
## **Подключаюсь к мастеру и реплике**

Использую инструкцию по подключению к кластеру, доступную на вкладке "Обзор": cкачайте SSL сертификат и подключитесь к кластеру с помощью утилиты psql, указав hostname всех узлов и атрибут target_session_attrs=read-write.
___
**Проверяю, что подключение прошло к master-узлу.**

## select case when pg_is_in_recovery() then 'REPLICA' else 'MASTER' end;
**Скриншот**

___![1](https://user-images.githubusercontent.com/94833070/201700610-5d3678bb-165b-4919-b669-f45225df761a.png)


**Посмотрю количество подключенных реплик:**

## select count(*) from pg_stat_replication;
**Скриншот**

____![2](https://user-images.githubusercontent.com/94833070/201706940-221bde4d-a506-411c-8b69-959f595c29a1.png)


**Проверяю работоспособность репликации в кластере**

**Создаю таблицу и вставьте одну-две строки.**

## CREATE TABLE test_table(text varchar);
**Скриншот**

![3](https://user-images.githubusercontent.com/94833070/201707560-538142d3-47f4-4676-ae32-44e4d620f145.png)

## insert into test_table values('Строка 1');

![Снимок экрана от 2022-11-13 19-30-08](https://user-images.githubusercontent.com/94833070/201707992-8c5e2b54-479a-4616-883a-27e542f04edb.png)

и добаюляю insert into test_table values('netology'); 

Подключаюсь к узлу-реплике. Для этого из команды подключения удалите атрибут 
target_session_attrs , и в параметре атрибут host передайте только имя хоста-реплики. 

Роли хостов можно посмотреть на соответствующей вкладке UI консоли.

## **Проверяю, что подключение прошло к узлу-реплике.**

## select case when pg_is_in_recovery() then 'REPLICA' else 'MASTER' end;
**Скриншот**

![1](https://user-images.githubusercontent.com/94833070/201708359-4d14b439-0af1-41ee-9429-6f815642c73d.png)


**Проверяю состояние репликации**

## select status from pg_stat_wal_receiver;

**Скриншот**

![2](https://user-images.githubusercontent.com/94833070/201708560-169f1376-10b4-40a3-8efa-4aa82ff78dcd.png)


## **Для проверки, что механизм репликации данных работает между зонами доступности облака, выполните запрос к таблице, созданной на предыдущем шаге:**

## select * from test_table;

**Скриншот**

и добаюляю insert into test_table values('netology');   и дополнительные столбцы в таблице.

![Снимок экрана от 2022-11-14 20-58-55](https://user-images.githubusercontent.com/94833070/201708687-bad85272-7104-4153-95d8-6f46f44f0f31.png)



# Задание 2*

Создайте кластер, как в задании 1 с помощью terraform.

По итогу пришлите скришоты:

Скриншот созданной базы данных;
Код terraform, создающий базу данных.

Задания, помеченные звездочкой * - дополнительные (не обязательные к выполнению) и никак не повлияют на получение вами зачета по этому домашнему заданию. Вы можете их выполнить, если хотите глубже и/или шире разобраться в материале.
___
**Ответ**

# Файл terraform main.tf


terraform {
  required_providers {
    yandex = {
      source = "yandex-cloud/yandex"
    }
  }
}

provider "yandex" {
  token     = "AQAAAAAcqg_6AATuwaDX7AESpEjukDp47GhLDe4"
  cloud_id  = "b1go4pl3bsgk4sbe8rjq"
  folder_id = "b1g6fhreiogi307vbba9"
  zone      = "{{ zone-id }}"
}

resource "yandex_mdb_postgresql_cluster" "mypg" {
  name                = "mypg"
  environment         = "PRODUCTION"
  network_id          = yandex_vpc_network.mynet.id
  security_group_ids  = [yandex_vpc_security_group.pgsql-sg.id]
  deletion_protection = true

  config {
    version = 13
    resources {
      resource_preset_id = "s2.micro"
      disk_type_id       = "network-ssd"
      disk_size          = "10"
    }
  }


  host {
    zone      = "ru-central1-a"
    subnet_id = yandex_vpc_subnet.mysubnet-a.id
  }


  host {
    zone      = "ru-central1-b"
    subnet_id = yandex_vpc_subnet.mysubnet-b.id
  }


  host {
    zone      = "ru-central1-c"
    subnet_id = yandex_vpc_subnet.mysubnet-c.id

  }
}


resource "yandex_mdb_postgresql_database" "db1" {
  cluster_id = yandex_mdb_postgresql_cluster.mypg.id
  name       = "db1"
  owner      = "andreevvi"
}

resource "yandex_mdb_postgresql_user" "andreevvi" {
  cluster_id = yandex_mdb_postgresql_cluster.mypg.id
  name       = "andreevvi"
  password   = "master0629"
}


resource "yandex_vpc_network" "mynet" {
  name = "mynet"
}

resource "yandex_vpc_subnet" "mysubnet-a" {
  v4_cidr_blocks = ["10.5.0.0/16"]
  zone           = "ru-central1-a"
  network_id     = yandex_vpc_network.mynet.id
}
resource "yandex_vpc_subnet" "mysubnet-b" {
  v4_cidr_blocks = ["10.6.0.0/16"]
  zone           = "ru-central1-b"
  network_id     = yandex_vpc_network.mynet.id
}
resource "yandex_vpc_subnet" "mysubnet-c" {
  v4_cidr_blocks = ["10.7.0.0/16"]
  zone           = "ru-central1-c"
  network_id     = yandex_vpc_network.mynet.id
}

resource "yandex_vpc_security_group" "pgsql-sg" {
  name       = "pgsql-sg"
  network_id = yandex_vpc_network.mynet.id


  ingress {
    description    = "PostgreSQL"
    port           = 6432
    protocol       = "TCP"
    v4_cidr_blocks = ["0.0.0.0/0"]
  }
}

**Скриншот**

![Снимок экрана от 2022-11-20 16-24-32](https://user-images.githubusercontent.com/94833070/202895019-5f50b48e-76dd-4e4f-b043-3cc8aa49928e.png)

**Скриншот db1**

![Снимок экрана от 2022-11-20 16-25-24](https://user-images.githubusercontent.com/94833070/202895053-31bdcbf2-ec7f-4aa3-a586-1c259876350d.png)

**Скриншот terraform в облаке**

![Снимок экрана от 2022-11-20 16-24-53](https://user-images.githubusercontent.com/94833070/202895092-aef051e8-961d-47e2-81dd-d312a3896262.png)

**и хосты **

![Снимок экрана от 2022-11-20 16-25-26](https://user-images.githubusercontent.com/94833070/202895138-2978cf89-dc70-4c58-8406-e3d58c863928.png)












