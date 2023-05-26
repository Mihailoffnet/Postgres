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

### Работа с данными INSERT, UPDATE и DELETE
- INSERT INTO table_name (name1, name2) VALUES('value1', 'value2'); - вставить в таблицу table_name столбцы name1 и name2 значения value1 и value2
- INSERT INTO table_name VALUES('value1', 'value2'); - тоже самое, но без указания атрибутов (возможно только при заполнении всех имеющихся в таблице атрибутов)
- UPDATE table_name SET name = 'value' WHERE id = xxx; - изменить атрибут name с id xxx в таблице table_name на новое значение value
- DELETE FROM table_name WHERE id = xxx; - удалить из таблицы table_name все записи у объекта с id = xxxvalue
#### Внимание!!! Если не указать параметр WHERE то будут удалены ВСЕ записи из таблицы!!!

### SELECT запросы
- SELECT * FROM table_name; - показать все записи из таблицы table_name
- SELECT name FROM table_name; - Вывести атрибут name из таблицы table_name
- SELECT name * X FROM table_name; - Вывести атрибут name умноженный на X из таблицы table_name. Кроме умножения, доступно деление, сложение, вычитание и взятие по остатку.
- SELECT name1 - name2 FROM table_name; Вывести разность двух атрибутов name1 и name2 из таблицы table_name. Кроме умножения, доступно деление, сложение, вычитание и взятие по остатку.
- SELECT DISTINCT name FROM table_name; - Вывести только уникальные значения атрибута name из таблицы table_name 
- SELECT name1, name2 FROM table_name; - Вывести указанные атрибуты из таблицы table_name 
- SELECT * FROM table_name WHERE id = xxx; показать записи c id xxx из таблицы table_name
- SELECT name1, name2 FROM table_name WHERE name2 >= X; - фильтрация данных по условию. Вывести атрибуты name1 и name2 из таблицы table_name при условии, что name3 >= X (доступно так же <=, =, <. >, <>)
- SELECT name1, name2  FROM table_name WHERE name3  = 'value'; - тоже самое, что и выше.
- SELECT name1, name2 FROM table_name WHERE name3 = true AND NOT name4 = X; - фильтрация по нескольким условиям, используя команды AND и NOT

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

## Примеры команд PostgreSQL для консоли

- СОЗДАТЬ ТАБЛИЦУ с именем student со столбцами: id тип SERIAL (самоувеличивается на единицу) с ограничением PRIMARY KEY и второй столбец name тип строка VARCHAR с ограничением длины имени (60) символов и ограничением NOT NULL (не может быть пустой). 
> CREATE TABLE student (
>   id SERIAL PRIMARY KEY, 
>   name VARCHAR(60) NOT NULL);

- добавлена команда IF NOT EXIST что значит "если такой таблицы еще нет". То есть таблица будет создана если ее не было, и будет пропущена без ошибки, если такая таблица уже есть в БД.
> CREATE TABLE IF NOT EXIST student (
>   id SERIAL PRIMARY KEY, 
>   name VARCHAR(60) NOT NULL);

- ИЗМЕНИТЬ ТАБЛИЦУ student ПЕРЕИМЕНОВАТЬ столбец name на first_name
> ALTER TABLE student 
> RENAME name TO first_name;

- Добавить в таблицу Student атрибут surname строковый с ограничением 60 символовб который не может быть пустым.
> ALTER TABLE Student 
> ADD COLUMN surname VARCHAR(60) NOT NULL;

- один к одному (1 вариант)
> CREATE TABLE IF NOT EXISTS Student (
>	email VARCHAR(80) PRIMARY KEY,
>	name VARCHAR(40) NOT NULL,
>	password VARCHAR(128) NOT NULL); 
>	
> CREATE TABLE IF NOT EXISTS StudentInfo (
>	email VARCHAR(80) PRIMARY KEY REFERENCES Student(email),
>	birthday date,
>	city VARCHAR(60),
>	roi TEXT);

- один к одному (2 вариант)
> CREATE TABLE IF NOT EXISTS Student (
>	id SERIAL PRIMARY KEY,
>	email VARCHAR(80) UNIQUE NOT NULL,
>	name VARCHAR(40) NOT NULL,
>	PASSWORD VARCHAR(128) NOT NULL);
>
> CREATE TABLE IF NOT EXISTS StudentInfo (
>	id INTEGER PRIMARY KEY REFERENCES Student(id),
>	birthday date,
>	city VARCHAR(60),
>	roi TEXT);

- один ко многим
> CREATE TABLE IF NOT EXISTS Course (
>	id SERIAL PRIMARY KEY,
>	name VARCHAR(60) NOT NULL,
>	description TEXT);
>
> CREATE TABLE IF NOT EXISTS HomeworkTask (
>	id SERIAL PRIMARY KEY,
>	course_id INTEGER NOT NULL REFERENCES Course(id),
>	number INTEGER NOT NULL,
>	description TEXT NOT NULL);

- многие ко многим (1 вариант)
> CREATE TABLE IF NOT EXISTS CourseStudent (
>	course_id INTEGER REFERENCES Course(id),
>	student_id INTEGER REFERENCES Student(id),
>	CONSTRAINT pk PRIMARY KEY (course_id, student_id));

- многие ко многим (2 вариант)
> CREATE TABLE IF NOT EXISTS HomeworkSolution (
>	id SERIAL PRIMARY KEY,
>	task_id INTEGER NOT NULL REFERENCES HomeworkTask(id),
>	student_id INTEGER NOT NULL REFERENCES Student(id),
>	solution TEXT NOT NULL);

- выберем все поля из таблицы film
> SELECT * FROM film;
> 
- выберем столбец title таблицы film
> SELECT title FROM film; - выберем столбец title таблицы film

- выберем 2 столбца из таблицы film
> SELECT title, release_year FROM film;

### DISTINCT
- выведем столбец rating из film
> SELECT DISTINCT rating FROM film;

### Примеры с арифметикой
- переведем цены в условные рубли
> SELECT amount * 70 FROM payment;
- узнаем время аренды по позициям
> SELECT return_date - rental_date FROM rental;

### WHERE
- найдем фильмы, вышедшие после 2000
> SELECT title, release_year FROM film 
> WHERE release_year >= 2000;
- найдем сотрудников, которые сейчас работают
> SELECT first_name, last_name, active FROM staff 
> WHERE active = true;
- атрибут с критерием не обязательно должен входить в выборку
> SELECT first_name, last_name FROM staff 
> WHERE active = true;
- найдем ID, имена, фамилии актеров, которых зовут Joe
> SELECT actor_id, first_name, last_name FROM actor 
> WHERE first_name = 'Joe';
- найдем всех сотрудников, которые работают не во втором магазине
> SELECT first_name, last_name FROM staff 
> WHERE store_id != 2;
- найдем только работающих сотрудников из всех магазинов, кроме 1
> SELECT first_name, last_name FROM staff 
> WHERE active = true AND NOT store_id = 1;
- найдем фильмы, цена проката которых меньше 0.99, а цена возмещения меньше 9.99
> SELECT title, rental_rate, replacement_cost FROM film 
> WHERE rental_rate <= 0.99 AND replacement_cost <= 9.99;
- найдем фильмы аналогичные предыдущему примеру или продолжительностью меньше 50 минут
> SELECT title, length, rental_rate, replacement_cost FROM film 
> WHERE rental_rate <= 0.99 AND replacement_cost <= 9.99 OR length < 50;

### IN / NOT IN
- найдем фильмы с рейтингом R, NC-17
> SELECT title, description, rating FROM film 
> WHERE rating IN ('R', 'NC-17');
- найдем недетские фильмы
> SELECT title, description, rating FROM film 
> WHERE rating NOT IN ('G', 'PG');

### BETWEEN
- в диапазоне (включая границы)
> SELECT title, rental_rate FROM film 
> WHERE rental_rate 
> BETWEEN 0.99 AND 3;
- вне диапазона (границы тоже инвертируются => не включая границы)
> SELECT title, rental_rate FROM film 
> WHERE rental_rate NOT 
> BETWEEN 0.99 AND 3;

### LIKE
- найдем фильм, в описании которого есть Scientist
> SELECT title, description FROM film 
> WHERE description 
> LIKE '%Scientist%';
- найдем ID, имена, фамилии актеров, фамилия которых содержит gen
> SELECT actor_id, first_name, last_name FROM actor 
> WHERE last_name 
> LIKE '%gen%';
- найдем ID, имена, фамилии актеров, фамилия которых оканчивается на gen
> SELECT actor_id, first_name, last_name FROM actor 
> WHERE last_name 
> LIKE '%gen';

### ORDER BY
- отсортируем фильмы по цене проката
> SELECT title, rental_rate FROM film 
> ORDER BY rental_rate;
- по убыванию
> SELECT title, rental_rate FROM film 
> ORDER BY rental_rate DESC;
- сортируем по нескольким столбцам: продолжительности и цене проката
> SELECT title, length, rental_rate FROM film 
> ORDER BY length DESC, rental_rate ASC;
- найдем ID, имена, фамилии актеров, чья фамилия содержит li, отсортируем в алфавитном порядке по фамилии, затем по имени
> SELECT actor_id, first_name, last_name FROM actor 
> WHERE last_name LIKE '%li%' 
> ORDER BY last_name, first_name;

### LIMIT
- выведем первые 15 записей
> SELECT title, length, rental_rate FROM film
>  ORDER BY length DESC, rental_rate 
>  LIMIT 15;
  

