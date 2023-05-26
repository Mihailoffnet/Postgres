##### Все типы данных PostgreSQL https://www.postgresql.org/docs/12/datatype.html
##### Ограничения в PostgreSQL: https://www.postgresql.org/docs/current/ddl-constraints.html


### Команды CREATE
- createDB -U postgress name - Создать базу данных name
- Выполнить загрузку данных: pg_restore -U postgres -d dvdrental путь_к_вашему_файлу.tar
- psql -U postgress -d name - Переключиться на управление БД name
- CREATE TABLE name (column, ...); - создать таблицу с указанными столбцами
- CREATE TABLE IF NOT EXIST name (column, ...); - создать таблицу если такой еще нет
- DROP TABLE name - удалить таблицу name

### Команды DROP
- DROP TABLE student; - УДАЛИТЬ ТАБЛИЦУ student.
В случае удачной команды в конcоли видим DROP TABLE, то есть таблица удалена.

### Команды ALTER TABLE table_name
- ADD COLUMN name TYPE CONSTRAINTS - добавить атрибут (столбец) name
- RENAME TO new_name - переименовать таблицу table_name в new_name
- RENAME name TO new_name - переименовать атрибут name в new_name
- ALTER COLUMN name SET DATA TYPE type - изменить тип атрибута name на type
- ADD CONSTRAINT col_name constraint - добавить ограничение
- DROP CONSTRAINT col_name - удалить ограничение
- DROP COLUMN name - удалить атрибут name

### Работа с данными
вставить в таблицу name:
- INSERT INTO table_name (name1, name2) VALUES('value1', 'value2'); - вставить в таблицу table_name столбцы name1 и name2 значения value1 и value2
- INSERT INTO table_name VALUES('value1', 'value2'); - тоже самое, но без указания атрибутов (возможно только при заполнении всех имеющихся в таблице атрибутов)
- UPDATE table_name SET name = 'value' WHERE id = xxx; - изменить атрибут name с id xxx в таблице table_name на новое значение value
- DELETE FROM table_name WHERE id = xxx; - удалить из таблицы table_name все записи у объекта с id = xxxvalue
#### Внимание!!! Если не указать параметр WHERE то будут удалены ВСЕ записи из таблицы!!!

### SELECT запросы
- SELECT * FROM table_name; - показать все записи из таблицы table_name
- SELECT name FROM table_name; - Вывести атрибут name из таблицы table_name
- SELECT name * X FROM table_name; - Вывести атрибут name умноженный на X из таблицы table_name. Кроме умножения, доступно деление, сложение, вычитание и взятие по остатку.
- SELECT DISTINCT name FROM table_name; - Вывести только уникальные значения атрибута name из таблицы table_name 
- SELECT name1, name2 FROM table_name; - Вывести указанные атрибуты из таблицы table_name 
- SELECT * FROM table_name WHERE id = xxx; показать записи c id xxx из таблицы table_name

### Загрузить базу из файла *.tar
- Создать БД с нужным названием createdb -U postgres name
- Выполнить загрузку данных: pg_restore -U postgres -d dvdrental путь_к_вашему_файлу.tar

### Ограничения столбцов
- UNIQUE - Все значения в этом поле должны быть уникальным
- SERIAL - используется для ID, сам увеличивается на единицу, является уникальным
- NOT NULL - Значение не может быть пустым (не может отсутствовать)
- VARCHAR(60) строковый, с ограничением длины 60 символов
- PRIMARY KEY - Первичный ключ, обязывает поле
быть уникальным и не пустым
- FOREIGN KEY - Внешний ключ, обязывает значение соответствовать значению из другой таблицы
- PRIMARY KEY REFERENCES name(name) - главный ключ, который хранится в таблице name столбце (name)
- CONSTRAINT name PRIMERY KEY (id_1, id_2) - составной основной ключ, создающийся в отдельной таблице с двумя основными ключами от других таблиц. Позволяет делать связи МНогие ко многим.
- CHECK - Добавить проверку значения на описанное условие
- REFERENCES name(id) - ссылается на стодбец id таблицы name
  
### Типы данных
- TEXT - строки произвольной длины
- VARCHAR или character varying - строки ограниченной длины
- DATE - дата (без времени)
- NTEGER integer - целые числа 
- SERIAL - целые числа с автоинкрементом
- NUMERIC - Десятичные числа
- TIMESTAMP - Дата+время
- BOOLEAN - логическийб булевы значения
- JSONB - json-поля
-
## Примеры команд PostgreSQL для консоли

### CREATE TABLE student (id SERIAL PRIMARY KEY, name VARCHAR(60) NOT NULL); 
- СОЗДАТЬ ТАБЛИЦУ с именем student со столбцами: id тип SERIAL (самоувеличивается на единицу) с ограничением PRIMARY KEY и второй столбец name тип строка VARCHAR с ограничением длины имени (60) символов и ограничением NOT NULL (не может быть пустой). 
В случае удачной команды в консоли видим CREATE TABLE - то есть таблица создана.
### CREATE TABLE IF NOT EXIST student (id SERIAL PRIMARY KEY, name VARCHAR(60) NOT NULL); 
- добавлена команда IF NOT EXIST что значит "если такой таблицы еще нет". То есть таблица будет создана если ее не было, и будет пропущена без ошибки, если такая таблица уже есть в БД.
### ALTER TABLE student RENAME name TO first_name;
- ИЗМЕНИТЬ ТАБЛИЦУ student ПЕРЕИМЕНОВАТЬ столбец name на first_name
В случае удачной команды в конcоли видим ALTER TABLE, то есть изменения применены.
### ALTER TABLE Student ADD COLUMN surname VARCHAR(60) NOT NULL;
- Добавить в таблицу Student атрибут surname строковый с ограничением 60 символовб который не может быть пустым.
  

