##### Все типы данных PostgreSQL https://www.postgresql.org/docs/12/datatype.html
##### Ограничения в PostgreSQL: https://www.postgresql.org/docs/current/ddl-constraints.html

### Команды CREATE
- createDB -U postgress name 
    Создать базу данных name
- pg_restore -U postgres -d dvdrental путь_к_вашему_файлу.tar
    Выполнить загрузку данных:
- psql -U postgress -d name 
    Переключиться на управление БД name
- CREATE TABLE table_name (id PRIMARY KEY, column_name1 VARCHAR(80) UNIQUE NOT NULL, column_name2 DATA NOT NULL, column_name3 VARCHAR(128) NOT NULL); 
    создать таблицу table_name с столбцом id первичный ключ, столбцом column_name1 тип текст длиной 80 символов, столбцом column_name2 тип DATA и столбцом column_name3 тип текст длиной 120 символом, который не может быть пустым.
- CREATE TABLE IF NOT EXISTS table_name (id INTEGER PRIMARY KEY REFERENCES another_table(another_id), column_name1 VARCHAR(80), column_name2 тип DATA, column_name3 TEXT); 
    создать таблицу table_name с столбцом id внешний ключ, ссылающийся на первичный ключ другой таблицы another_table атрибут another_id, столбцом column_name1 тип текст длиной 80 символов, столбцом column_name2 тип DATA и столбцом column_name3 тип текстбез ограничения.
- CREATE TABLE IF NOT EXIST name (column, ...);
    создать таблицу если такой еще нет
- DROP TABLE name
    удалить таблицу name

### Команды DROP
- DROP TABLE student; - УДАЛИТЬ ТАБЛИЦУ student.

### Команды ALTER TABLE table_name
- ALTER TABLE table_name ADD COLUMN name TYPE CONSTRAINTS - добавить атрибут (столбец) name
- ALTER TABLE table_name RENAME TO new_name - переименовать таблицу table_name в new_name
- ALTER TABLE table_name RENAME name TO new_name - переименовать атрибут name в new_name
- ALTER TABLE table_name ALTER COLUMN name SET DATA TYPE type - изменить тип атрибута name на type
- ALTER TABLE table_name ADD CONSTRAINT col_name constraint - добавить ограничение
- ALTER TABLE table_name DROP CONSTRAINT col_name - удалить ограничение
- ALTER TABLE table_name DROP COLUMN name - удалить атрибут name

### Работа с данными INSERT, UPDATE и DELETE
- INSERT INTO table_name (name1, name2) VALUES ('value1', 'value2'); - вставить в таблицу table_name столбцы name1 и name2 значения value1 и value2
- INSERT INTO table_name VALUES ('value1', 'value2'); - тоже самое, но без указания атрибутов (возможно только при заполнении всех имеющихся в таблице атрибутов)
- UPDATE table_name SET name = 'value' WHERE id = xxx; - изменить атрибут name с id xxx в таблице table_name на новое значение value
- DELETE FROM table_name WHERE id = xxx; - удалить из таблицы table_name все записи у объекта с id = xxxvalue
#### Внимание!!! Если не указать параметр WHERE то будут удалены ВСЕ записи из таблицы!!!

### SELECT запросы
#### Все ни жеприведенные команды можно сочетать внутри одного запроса и создавать запросы любой сложности

#### Простые SELECT запросы
- SELECT * FROM table_name; - показать все записи из таблицы table_name
- SELECT name FROM table_name; - Вывести атрибут name из таблицы table_name
- SELECT name1, name2 FROM table_name; - Вывести указанные атрибуты из таблицы table_name 
#### SELECT запросы с математическими функциями
- SELECT name * X FROM table_name; - Вывести атрибут name умноженный на X из таблицы table_name. Кроме умножения, доступно деление, сложение, вычитание и взятие по остатку.
- SELECT name1 - name2 FROM table_name; Вывести разность двух атрибутов name1 и name2 из таблицы table_name. Кроме умножения, доступно деление, сложение, вычитание и взятие по остатку.
- SELECT DISTINCT name FROM table_name; - Вывести только уникальные значения атрибута name из таблицы table_name 
#### SELECT запросы с условием WHERE
- SELECT * FROM table_name WHERE id = xxx; показать записи c id xxx из таблицы table_name
- SELECT name1, name2 FROM table_name WHERE name2 >= X; - фильтрация данных по условию. Вывести атрибуты name1 и name2 из таблицы table_name при условии, что name3 >= X (доступно так же <=, =, <. >, <>)
- SELECT name1, name2  FROM table_name WHERE name3  = 'value'; - тоже самое, что и выше.
#### SELECT запросы с несколькими условиями AND / OR / NOT / IN / BETWEEN
- SELECT name1, name2 FROM table_name WHERE name3 = true AND NOT name4 = X; - фильтрация по нескольким условиям, используя команды AND и NOT
- SELECT name1, name2 FROM table_name WHERE name3 <= X AND name4 <= Y OR name5 < Z; - фильтрация по нескольким условиям. Выполняется сначала AND потом OR
- SELECT name1, name2, name3 FROM table_name WHERE name3 IN ('value1', 'value2'); - Вывести атрибутs name1, name2 и name3 у которых name3 равно value1 или value2
- SELECT name1, name2, name3 FROM table_name WHERE name3 NOT IN ('value1', 'value2'); - Вывести атрибутs name1, name2 и name3 у которых name3 не равно value1 или value2
- SELECT name1, name2 FROM table_name WHERE name2 BETWEEN X AND Y; - Вывести атрибуты name1, name2 у которых name2 находится в диапазоне между X и Y включая границы
- SELECT name1, name2 FROM table_name WHERE name2 NOT BETWEEN X AND Y; - Вывести атрибуты name1, name2 у которых name2 не находится в диапазоне между X и Y (не включая границы)
#### SELECT запросы с условием вхождения LIKE
- SELECT name1, name2, name3 FROM table_name WHERE name1 LIKE 'value'; - Вывести атрибуты name1, name2  name3 у которых name1 содержит внутри слово или значение value
- SELECT name1, name2, name3 FROM table_name WHERE name1 LIKE '%value%'; - Вывести атрибуты name1, name2  name3 у которых name1 содержит внутри вхождение части слова или значения value
- SELECT name1, name2, name3 FROM table_name WHERE name1 LIKE '%value'; - Вывести атрибуты name1, name2  name3 у которых name1 содержит внутри значение с окончанием value (или с началом значения value%) 
- SELECT name1, name2, name3 FROM table_name WHERE name1 LIKE '%value_'; - Вывести атрибуты name1, name2  name3 у которых name1 содержит внутри значение с окончанием value после которого идет еще один любой симвод (_ - любой один символ)
#### SELECT запросы c сортировкой ORDER BY
- SELECT name1, name2 FROM table_name ORDER BY name2; - Вывести атрибуты name1, name2 с сортировкой по возрастанию по столбцу name2
- SELECT name1, name2 FROM table_name ORDER BY name2 ASC; - Вывести атрибуты name1, name2 с сортировкой по возрастанию по столбцу name2
- SELECT name1, name2 FROM table_name ORDER BY name2 DESC; - Вывести атрибуты name1, name2 с сортировкой по убыванию по столбцу name2
- SELECT name1, name2, name3 FROM table_name WHERE name3 LIKE '%value%' ORDER BY name1, name2; - Вывести атрибуты name1, name2 и name3 с сортировкой по возрастанию сначала по столбцу name1 потом по столбцу name2 с уловием вхождения value внутри значения name3
#### SELECT запросы c лимитом LIMIT
- SELECT name1, name2, name3 FROM table_name ORDER BY length name1, name2 LIMIT 15; - Вывести атрибуты name1, name2 и name3 первые 15 записей с сортировкой по возрастанию сначала по столбцу name1 потом по столбцу name2

## Агрегирующие функции
- SELECT MAX(name1) FROM table_name; - найдем максимальное значение атрибута name1 в таблице table_name
- SELECT AVG(name1) FROM table_name; - найдем среднее значение атрибута name1 в таблице table_name
- SELECT COUNT(DISTINCT name1) FROM table_name; - найдем количество (DISTINCT - уникальных) атрибутов name1 в таблице table_name
- SELECT SUM(name1)б AVG(name1) FROM table_name WHERE name2 = X; - найдем сумму атрибутов name1 и среднее значение атрибутов name1 у которых name2 = X в таблице table_name 

## Вложенные запросы
### Вложенных запросов может быть любое количество. Обратите внимание, что сначала выполняется вложенный запрос, а потом уже общий с учетом значения вложенного запроса
- SELECT name1, name2 FROM table_name WHERE name2 >= (SELECT AVG(name2) FROM table_name); найдем все записи с name2 больше или равному среднему значению. 
- SELECT name1, name2 FROM table_name WHERE name2 < (SELECT MAX(name2) FROM table_name) ORDER BY name1 DESC; - найдем все записи с name2 которое меньше максимумального значения и отслортируем в обратном порядке по name1. 

## Группировки
- SELECT name1, COUNT(*) FROM table_name GROUP BY name1 ORDER BY COUNT(*) DESC; сгруппируем и посчитаем количество name1, отсортируем в обратном порядке
- SELECT name1, COUNT(name2) FROM table_name GROUP BY name1 ORDER BY COUNT(name2) DESC; - посчитаем количетсво name2 в разрезе name1 и отсортируем по name2 в обратном порядке
- SELECT name2, MAX(name1) FROM table_name GROUP BY name2; - найдем максимальные name1 в разрезе name2 с группировкой в таблице table_name
- SELECT name1, name2, AVG(name3) FROM table_name GROUP BY name1, name2 ORDER BY AVG(name3) DESC; - найдем средние name3 каждого name1 каждому name2 с группировкой по name1, name2 и отсортируем в обратном порядке по name3 в таблице table_name

-- найдем среднюю продолжительность фильма в разрезе рейтингов в 2006 году
SELECT rating, AVG(length) FROM film
WHERE release_year = 2006
GROUP BY rating;

## Оператор HAVING
### Тоже, что и WHERE, но работает после выполнения WHERE по результатам первой выборки
- SELECT name1, COUNT(*) FROM table_name GROUP BY name1 HAVING COUNT(*) = 1; - отберем только name1, которые не повторяются и выведем все столбцы
- SELECT name1, COUNT(*) FROM table_name GROUP BY name1 HAVING COUNT(*) > 1 ORDER BY COUNT(*) DESC; - отберем и посчитаем только name1, которые повторяются (больше одного)
- SELECT name1, SUM(name2) FROM table_name WHERE name1 LIKE '%Value%' GROUP BY title HAVING SUM(name2) > X; - найдем name1, у которых есть Value в названии и name2 в сумме больше Х

## ALIAS -псевдонимы
- SELECT name1 AS n1, SUM(name2n) AS sum_n2 FROM table_name WHERE n1 LIKE '%Value%' GROUP BY n1 HAVING sum_n2 > X; - предыдущий запрос с псевдонимами
- SELECT name1 n1, SUM(name2n) sum_n2 FROM table_name WHERE n1 LIKE '%Value%' GROUP BY n1 HAVING sum_n2 > X; - ключевое слово AS можно не писать, это все тот же запрос

## JOIN - Объединение таблиц 
- SELECT name1, name2, name3 FROM table_name1 t_n1 LEFT JOIN table_name2 t_n2 ON t_n1.foreign_id = t_n2.primery_id; - выведем name1, name2 (из table_name1) и name3 (из table_name2) объединив их на основании table_name1 (все строки из левой таблицы, из table_name1) через сопоставление внешнего ключа из table_name1 (t_n1) и первичного ключа из table_name2 (t_n2)
- SELECT t_n1.name2, COUNT(name4) FROM table_name3 t_n3 LEFT JOIN table_name1 t_n1 ON t_n3.foreign_id = t_n1.primery_id GROUP BY t_n1.name2; - в продолжение прошлого кода определим количество name4 (из таблицы table_name3) для каждого name2 (из таблицы table_name1)

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

### Примеры по БД DVD
- выберем все поля из таблицы film
> SELECT * FROM film;

- выберем столбец title таблицы film
> SELECT title FROM film; - выберем столбец title таблицы film

- выберем 2 столбца из таблицы film
> SELECT title, release_year FROM film;

- найдем максимальную стоимость проката
> SELECT MAX(rental_rate) FROM film;

- посчитаем среднюю продолжительность фильма
> SELECT AVG(length) FROM film;

- сколько уникальных имен актеров?
>  SELECT COUNT(DISTINCT first_name) FROM actor

- посчитаем сумму и средние продажи по конкретному продавцу
> SELECT SUM(amount), AVG(amount) FROM payment
> WHERE staff_id = 1;

#### DISTINCT
- выведем столбец rating из film
> SELECT DISTINCT rating FROM film;

#### Примеры с арифметикой
- переведем цены в условные рубли
> SELECT amount * 70 FROM payment;
- узнаем время аренды по позициям
> SELECT return_date - rental_date FROM rental;

#### WHERE
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

#### AND / OR / NOT 
##### Логика: Выполняется сначала AND потом OR
> WHERE active = true AND NOT store_id = 1;
- найдем фильмы, цена проката которых меньше 0.99, а цена возмещения меньше 9.99
> SELECT title, rental_rate, replacement_cost FROM film 
> WHERE rental_rate <= 0.99 AND replacement_cost <= 9.99;
- найдем фильмы аналогичные предыдущему примеру или продолжительностью меньше 50 минут
> SELECT title, length, rental_rate, replacement_cost FROM film 
> WHERE rental_rate <= 0.99 AND replacement_cost <= 9.99 OR length < 50;

#### IN / NOT IN
- найдем фильмы с рейтингом R, NC-17
> SELECT title, description, rating FROM film 
> WHERE rating IN ('R', 'NC-17');
- найдем недетские фильмы
> SELECT title, description, rating FROM film 
> WHERE rating NOT IN ('G', 'PG');

#### BETWEEN
##### BETWEEN X AND Y - между X и Y
- в диапазоне (включая границы)
> SELECT title, rental_rate FROM film 
> WHERE rental_rate 
> BETWEEN 0.99 AND 3;
- вне диапазона (границы тоже инвертируются => не включая границы)
> SELECT title, rental_rate FROM film 
> WHERE rental_rate NOT 
> BETWEEN 0.99 AND 3;

#### LIKE
##### LIKE позволяет искать вхождение внутри слов
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

#### ORDER BY
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

#### LIMIT
- выведем первые 15 записей
> SELECT title, length, rental_rate FROM film
>  ORDER BY length DESC, rental_rate 
>  LIMIT 15;
  
#### Вложенные запросы
- найдем все фильмы с продолжительностью ваше среднего
> SELECT title, length FROM film
> WHERE length >= (SELECT AVG(length) FROM film);

- найдем названия фильмов, стоимость проката которых не максимальная
> SELECT title, rental_rate FROM film
> WHERE rental_rate < (SELECT MAX(rental_rate) FROM film)
> ORDER BY rental_rate DESC;

#### Группировки
- посчитаем количество актеров в разрезе фамилий (найдем однофамильцев)
> SELECT last_name, COUNT(*) FROM actor
> GROUP BY last_name
> ORDER BY COUNT(*) DESC;

- посчитаем количество фильмов в разрезе рейтингов (распределение рейтингов)
> SELECT rating, COUNT(title) FROM film
> GROUP BY rating
> ORDER BY COUNT(title) DESC;

- найдем максимальные продажи в разрезе продавцов
> SELECT staff_id, MAX(amount) FROM payment
> GROUP BY staff_id;

- найдем средние продажи каждого продавца каждому покупателю
> SELECT staff_id, customer_id, AVG(amount) FROM payment
> GROUP BY staff_id, customer_id
> ORDER BY AVG(amount) DESC;

- найдем среднюю продолжительность фильма в разрезе рейтингов в 2006 году
> SELECT rating, AVG(length) FROM film
> WHERE release_year = 2006
> GROUP BY rating;

#### Оператор HAVING
- отберем только фамилии актеров, которые не повторяются
> SELECT last_name, COUNT(*) FROM actor
> GROUP BY last_name
> HAVING COUNT(*) = 1;

- отберем и посчитаем только фамилии актеров, которые повторяются
> SELECT last_name, COUNT(*) FROM actor
> GROUP BY last_name
> HAVING COUNT(*) > 1
> ORDER BY COUNT(*) DESC;

- найдем фильмы, у которых есть Super в названии и они сдавались в прокат суммарно более, чем на 5 дней
> SELECT title, SUM(rental_duration) FROM film
> WHERE title LIKE '%Super%'
> GROUP BY title
> HAVING SUM(rental_duration) > 5;

#### ALIAS
- предыдущий запрос с псевдонимами
> SELECT title AS t, SUM(rental_duration) AS sum_t FROM film AS f
> WHERE title LIKE '%Super%'
> GROUP BY t
> HAVING SUM(rental_duration) > 5;

- ключевое слово AS можно не писать, тот же предыдущий запрос
> SELECT title t, SUM(rental_duration) sum_t FROM film f
> WHERE title LIKE '%Super%'
> GROUP BY t
> HAVING SUM(rental_duration) > 5;

#### JOIN Объединение таблиц
- выведем имена, фамилии и адреса всех сотрудников
> SELECT first_name, last_name, address FROM staff s
> LEFT JOIN address a ON s.address_id = a.address_id;

- определим количество продаж каждого продавца
> SELECT s.last_name, COUNT(amount) FROM payment p
> LEFT JOIN staff s ON p.staff_id = s.staff_id
> GROUP BY s.last_name;

- посчитаем, сколько актеров играло в каждом фильме
> SELECT title, COUNT(actor_id) actor_q FROM film f
> JOIN film_actor a ON f.film_id = a.film_id
> GROUP BY f.title
> ORDER BY actor_q DESC;

- сколько копий фильмов со словом Super в названии есть в наличии
> SELECT title, COUNT(inventory_id) FROM film f
> JOIN inventory i ON f.film_id = i.film_id
> WHERE title LIKE '%Super%'
> GROUP BY title;

- выведем список покупателей с количеством их покупок в порядке убывания
> SELECT c.last_name n, COUNT(p.amount) amount FROM customer c
> LEFT JOIN payment p ON c.customer_id = p.customer_id
> GROUP BY n
> ORDER BY amount DESC;

- выведем имена и почтовые адреса всех покупателей из России
> SELECT c.last_name, c.first_name, c.email FROM customer c
> JOIN address a ON c.address_id = a.address_id
> JOIN city ON a.city_id = city.city_id
> JOIN country co ON city.country_id = co.country_id
> WHERE country = 'Russian Federation';

- фильмы, которые берут в прокат чаще всего
> SELECT f.title, COUNT(r.inventory_id) count FROM film f
> JOIN inventory i ON f.film_id = i.film_id
> JOIN rental r ON i.inventory_id = r.inventory_id
> GROUP BY f.title
> ORDER BY count DESC;

- суммарные доходы магазинов
> SELECT s.store_id, SUM(p.amount) sales FROM store s 
> JOIN staff st ON s.store_id = st.store_id
> JOIN payment p ON st.staff_id = p.staff_id
> GROUP BY s.store_id;

- найдем города и страны каждого магазина
> SELECT store_id, city, country FROM store s 
> JOIN address a ON s.address_id = a.address_id
> JOIN city ON a.city_id = city.city_id
> JOIN country c ON city.country_id = c.country_id;

- выведем топ-5 жанров по доходу
> SELECT c.name, SUM(p.amount) revenue FROM category c 
> JOIN film_category fc ON c.category_id = fc.category_id
> JOIN inventory i ON fc.film_id = i.film_id
> JOIN rental r ON i.inventory_id = r.inventory_id
> JOIN payment p ON r.rental_id = p.rental_id
> GROUP BY c.name
> ORDER BY revenue DESC 
> LIMIT 5;

