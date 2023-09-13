## Домашнее задание к занятию 4. «PostgreSQL» Соловьев Д.В.

### Задача 1

Используя Docker, поднимите инстанс PostgreSQL (версию 13). Данные БД сохраните в volume.

Подключитесь к БД PostgreSQL, используя psql.

Воспользуйтесь командой \? для вывода подсказки по имеющимся в psql управляющим командам.

```
docker volume create netology

docker run --name postgresql -e POSTGRES_PASSWORD=netology -d -p 5432:5432 -v kali:/var/lib/postgresql/data postgres:13

docker exec -it postgresql bash

psql -U postgres
```

Найдите и приведите управляющие команды для:

- вывода списка БД
```
postgres=# \l+
                                                                   List of data
bases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privilege
s   |  Size   | Tablespace |                Description
-----------+----------+----------+------------+------------+-------------------
----+---------+------------+--------------------------------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
    | 7909 kB | pg_default | default administrative connection database
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres
   +| 7761 kB | pg_default | unmodifiable empty database
           |          |          |            |            | postgres=CTc/postg
res |         |            |
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres
   +| 7761 kB | pg_default | default template for new databases
           |          |          |            |            | postgres=CTc/postg
res |         |            |
(3 rows)
```

- подключения к БД,
```
postgres=# \conninfo
You are connected to database "postgres" as user "postgres" via socket in "/var/run/postgresql" at port "5432".
```

- вывода списка таблиц,
```
postgres=# \conninfo
You are connected to database "postgres" as user "postgres" via socket in "/var/run/postgresql" at port "5432".
postgres=# \dtS
                    List of relations
   Schema   |          Name           | Type  |  Owner
------------+-------------------------+-------+----------
 pg_catalog | pg_aggregate            | table | postgres
 pg_catalog | pg_am                   | table | postgres
 pg_catalog | pg_amop                 | table | postgres
 pg_catalog | pg_amproc               | table | postgres
 pg_catalog | pg_attrdef              | table | postgres
 pg_catalog | pg_attribute            | table | postgres
 pg_catalog | pg_auth_members         | table | postgres
 pg_catalog | pg_authid               | table | postgres
 pg_catalog | pg_cast                 | table | postgres
 pg_catalog | pg_class                | table | postgres
 pg_catalog | pg_collation            | table | postgres
 pg_catalog | pg_constraint           | table | postgres
 pg_catalog | pg_conversion           | table | postgres
 pg_catalog | pg_database             | table | postgres
 pg_catalog | pg_db_role_setting      | table | postgres
 pg_catalog | pg_default_acl          | table | postgres
 pg_catalog | pg_depend               | table | postgres
 pg_catalog | pg_description          | table | postgres
 pg_catalog | pg_enum                 | table | postgres
 pg_catalog | pg_event_trigger        | table | postgres
 pg_catalog | pg_extension            | table | postgres
 pg_catalog | pg_foreign_data_wrapper | table | postgres
 pg_catalog | pg_foreign_server       | table | postgres
 pg_catalog | pg_foreign_table        | table | postgres
 pg_catalog | pg_index                | table | postgres
 pg_catalog | pg_inherits             | table | postgres
 pg_catalog | pg_init_privs           | table | postgres
 pg_catalog | pg_language             | table | postgres
 pg_catalog | pg_largeobject          | table | postgres
 pg_catalog | pg_largeobject_metadata | table | postgres
 pg_catalog | pg_namespace            | table | postgres
 pg_catalog | pg_opclass              | table | postgres
 pg_catalog | pg_operator             | table | postgres
 pg_catalog | pg_opfamily             | table | postgres
 pg_catalog | pg_partitioned_table    | table | postgres
 pg_catalog | pg_policy               | table | postgres
 pg_catalog | pg_proc                 | table | postgres
 pg_catalog | pg_publication          | table | postgres
 pg_catalog | pg_publication_rel      | table | postgres
 pg_catalog | pg_range                | table | postgres
 pg_catalog | pg_replication_origin   | table | postgres
 pg_catalog | pg_rewrite              | table | postgres
 pg_catalog | pg_seclabel             | table | postgres
 pg_catalog | pg_sequence             | table | postgres
 pg_catalog | pg_shdepend             | table | postgres
 pg_catalog | pg_shdescription        | table | postgres
 pg_catalog | pg_shseclabel           | table | postgres
 pg_catalog | pg_statistic            | table | postgres
 pg_catalog | pg_statistic_ext        | table | postgres
 pg_catalog | pg_statistic_ext_data   | table | postgres
 pg_catalog | pg_subscription         | table | postgres
 pg_catalog | pg_subscription_rel     | table | postgres
 pg_catalog | pg_tablespace           | table | postgres
 pg_catalog | pg_transform            | table | postgres
 pg_catalog | pg_trigger              | table | postgres
 pg_catalog | pg_ts_config            | table | postgres
 pg_catalog | pg_ts_config_map        | table | postgres
 pg_catalog | pg_ts_dict              | table | postgres
 pg_catalog | pg_ts_parser            | table | postgres
 pg_catalog | pg_ts_template          | table | postgres
 pg_catalog | pg_type                 | table | postgres
 pg_catalog | pg_user_mapping         | table | postgres
(62 rows)
```

- вывода описания содержимого таблиц,
```
postgres=# \dS+
                                            List of relations
   Schema   |              Name               | Type  |  Owner   | Persistence |    Size    | Description
------------+---------------------------------+-------+----------+-------------+------------+-------------
 pg_catalog | pg_aggregate                    | table | postgres | permanent   | 56 kB      |
 pg_catalog | pg_am                           | table | postgres | permanent   | 40 kB      |
 pg_catalog | pg_amop                         | table | postgres | permanent   | 80 kB      |
 pg_catalog | pg_amproc                       | table | postgres | permanent   | 64 kB      |
 pg_catalog | pg_attrdef                      | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_attribute                    | table | postgres | permanent   | 456 kB     |
 pg_catalog | pg_auth_members                 | table | postgres | permanent   | 40 kB      |
 pg_catalog | pg_authid                       | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_available_extension_versions | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_available_extensions         | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_cast                         | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_class                        | table | postgres | permanent   | 136 kB     |
 pg_catalog | pg_collation                    | table | postgres | permanent   | 248 kB     |
 pg_catalog | pg_config                       | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_constraint                   | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_conversion                   | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_cursors                      | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_database                     | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_db_role_setting              | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_default_acl                  | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_depend                       | table | postgres | permanent   | 488 kB     |
 pg_catalog | pg_description                  | table | postgres | permanent   | 376 kB     |
 pg_catalog | pg_enum                         | table | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_event_trigger                | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_extension                    | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_file_settings                | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_foreign_data_wrapper         | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_foreign_server               | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_foreign_table                | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_group                        | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_hba_file_rules               | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_index                        | table | postgres | permanent   | 64 kB      |
 pg_catalog | pg_indexes                      | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_inherits                     | table | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_init_privs                   | table | postgres | permanent   | 56 kB      |
 pg_catalog | pg_language                     | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_largeobject                  | table | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_largeobject_metadata         | table | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_locks                        | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_matviews                     | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_namespace                    | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_opclass                      | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_operator                     | table | postgres | permanent   | 144 kB     |
 pg_catalog | pg_opfamily                     | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_partitioned_table            | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_policies                     | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_policy                       | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_prepared_statements          | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_prepared_xacts               | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_proc                         | table | postgres | permanent   | 688 kB     |
 pg_catalog | pg_publication                  | table | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_publication_rel              | table | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_publication_tables           | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_range                        | table | postgres | permanent   | 40 kB      |
 pg_catalog | pg_replication_origin           | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_replication_origin_status    | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_replication_slots            | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_rewrite                      | table | postgres | permanent   | 656 kB     |
 pg_catalog | pg_roles                        | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_rules                        | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_seclabel                     | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_seclabels                    | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_sequence                     | table | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_sequences                    | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_settings                     | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_shadow                       | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_shdepend                     | table | postgres | permanent   | 40 kB      |
 pg_catalog | pg_shdescription                | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_shmem_allocations            | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_shseclabel                   | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_stat_activity                | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_all_indexes             | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_all_tables              | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_archiver                | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_bgwriter                | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_database                | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_database_conflicts      | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_gssapi                  | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_progress_analyze        | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_progress_basebackup     | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_progress_cluster        | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_progress_create_index   | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_progress_vacuum         | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_replication             | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_slru                    | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_ssl                     | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_subscription            | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_sys_indexes             | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_sys_tables              | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_user_functions          | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_user_indexes            | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_user_tables             | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_wal_receiver            | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_xact_all_tables         | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_xact_sys_tables         | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_xact_user_functions     | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stat_xact_user_tables        | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_statio_all_indexes           | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_statio_all_sequences         | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_statio_all_tables            | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_statio_sys_indexes           | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_statio_sys_sequences         | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_statio_sys_tables            | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_statio_user_indexes          | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_statio_user_sequences        | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_statio_user_tables           | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_statistic                    | table | postgres | permanent   | 248 kB     |
 pg_catalog | pg_statistic_ext                | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_statistic_ext_data           | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_stats                        | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_stats_ext                    | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_subscription                 | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_subscription_rel             | table | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_tables                       | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_tablespace                   | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_timezone_abbrevs             | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_timezone_names               | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_transform                    | table | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_trigger                      | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_ts_config                    | table | postgres | permanent   | 40 kB      |
 pg_catalog | pg_ts_config_map                | table | postgres | permanent   | 56 kB      |
 pg_catalog | pg_ts_dict                      | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_ts_parser                    | table | postgres | permanent   | 40 kB      |
 pg_catalog | pg_ts_template                  | table | postgres | permanent   | 40 kB      |
 pg_catalog | pg_type                         | table | postgres | permanent   | 120 kB     |
 pg_catalog | pg_user                         | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_user_mapping                 | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_user_mappings                | view  | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_views                        | view  | postgres | permanent   | 0 bytes    |
(129 rows)
```

- выхода из psql.
```
postgres=# \q
```
### Задача 2

Используя psql, создайте БД test_database.
```
postgres=# CREATE DATABASE test_database;
```
Изучите бэкап БД.

Восстановите бэкап БД в test_database.
```
docker cp /home/solovev/test_dump.sql postgresql:/tmp
docker exec -it postgresql bash
psql -U postgres -f /tmp/test_dump.sql test_database
```
Перейдите в управляющую консоль psql внутри контейнера.
```
psql -U postgres
```
Подключитесь к восстановленной БД и проведите операцию ANALYZE для сбора статистики по таблице.
```
postgres=# \c test_database
You are now connected to database "test_database" as user "postgres".
test_database=# \dt
         List of relations
 Schema |  Name  | Type  |  Owner
--------+--------+-------+----------
 public | orders | table | postgres
(1 row)

test_database=# ANALYZE VERBOSE public.orders;
INFO:  analyzing "public.orders"
INFO:  "orders": scanned 1 of 1 pages, containing 8 live rows and 0 dead rows; 8 rows in sample, 8 estimated total rows
ANALYZE
```
Используя таблицу pg_stats, найдите столбец таблицы orders с наибольшим средним значением размера элементов в байтах.

Приведите в ответе команду, которую вы использовали для вычисления, и полученный результат.
```
test_database=# SELECT avg_width FROM pg_stats WHERE tablename='orders';
 avg_width
-----------
         4
        16
         4
(3 rows)
```

### Задача 3

Архитектор и администратор БД выяснили, что ваша таблица orders разрослась до невиданных размеров и поиск по ней занимает долгое время. Вам как успешному выпускнику курсов DevOps в Нетологии предложили провести разбиение таблицы на 2: шардировать на orders_1 - price>499 и orders_2 - price<=499.

Предложите SQL-транзакцию для проведения этой операции.
```
test_database=# CREATE TABLE orders_more_499_price (CHECK (price > 499)) INHERITS (orders);
CREATE TABLE
test_database=# INSERT INTO orders_more_499_price SELECT * FROM orders WHERE price > 499;
INSERT 0 3
test_database=# CREATE TABLE orders_less_499_price (CHECK (price <= 499)) INHERITS (orders);
CREATE TABLE
test_database=# INSERT INTO orders_LESS_499_price SELECT * FROM orders WHERE price <= 499;
INSERT 0 5
test_database=# DELETE FROM ONLY orders;
DELETE 8
test_database=# \dt
                 List of relations
 Schema |         Name          | Type  |  Owner
--------+-----------------------+-------+----------
 public | orders                | table | postgres
 public | orders_less_499_price | table | postgres
 public | orders_more_499_price | table | postgres
(3 rows)
```

Можно ли было изначально исключить ручное разбиение при проектировании таблицы orders?

- можно
```
CREATE RULE orders_insert_to_more AS ON INSERT TO orders WHERE ( price > 499 ) DO INSTEAD INSERT INTO orders_more_499_price VALUES (NEW.*);
CREATE RULE orders_insert_to_less AS ON INSERT TO orders WHERE ( price <= 499 ) DO INSTEAD INSERT INTO orders_less_499_price VALUES (NEW.*);
```

### Задача 4 

Используя утилиту pg_dump, создайте бекап БД test_database.
```
export PGPASSWORD=netology && pg_dump -h localhost -U postgres test_database > /tmp/test_database_backup.sql
```
Как бы вы доработали бэкап-файл, чтобы добавить уникальность значения столбца title для таблиц test_database?

- Добавить UNIQUE

```
CREATE TABLE public.orders_unique (
    id integer,
    title character varying(80) UNIQUE,
    price integer
);
```

