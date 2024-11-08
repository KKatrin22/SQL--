Выполняла SQL-запросы для получения, фильтрации и сортировки данных в учебном проекте <a href=https://sqltest.online> sqltest.online</a>

## Основы SQL 

### Задание №20
Найдите все комедии продолжительностью более трёх часов. Напишите запрос возвращающий результат состоящий из трёх столбцов: названия фильма, года выхода на экран и продолжительности в минутах отсортированный по длине фильма.
```sql
SELECT 
  title, 
  release_year, 
  length 
FROM 
  film 
  JOIN film_category ON film.film_id = film_category.film_id 
  JOIN category ON film_category.category_id = category.category_id 
WHERE 
  name = 'Comedy' 
  AND length > 180 
ORDER BY 
  length;
```
### Задание №21
Выберите фамилии, имена и адреса электронной почты клиентов, чьи имя и фамилия не содержат ни одной буквы «А» (латинская буква).Отсортируйте результат по customer_id.
```sql
SELECT 
  last_name, 
  first_name, 
  email 
FROM 
  customer 
WHERE 
  first_name NOT LIKE '%A%' 
  AND first_name NOT LIKE '%a%' 
  AND last_name NOT LIKE '%A%' 
  AND last_name NOT LIKE '%a%' 
ORDER BY 
  customer_id;
```
### Задание №22
Найдите все фильмы с рейтингом NC-17 (только для взрослых), в описании которых содержится подстрока Database Administrator.Выведите название, описание, год выпуска этих фильмов в алфавитном порядке по названию.
```sql
SELECT 
  title, 
  description, 
  release_year 
FROM 
  film 
WHERE 
  rating = 'NC-17' 
  AND description LIKE '%Database Administrator%' 
ORDER BY 
  title;
  ```
### Задание №23
Найдите все фильмы, в описании которых есть слова Dog или Cat, отмеченные рейтингом PG или PG-13 (для просмотра под контролем родителей).Выведите названия, описания, годы выпуска этих фильмов, отсортировав по названию в алфавитном порядке.
```sql
SELECT 
  title, 
  description, 
  release_year 
FROM 
  film 
WHERE 
  (
    description LIKE '%Dog%' 
    OR description LIKE '%Cat%'
  ) 
  AND rating IN ('PG', 'PG-13') 
ORDER BY 
  title;
  ```
### Задание №24
Фильмы с рейтингом R (Ограниченный доступ) и NC-17 (Только для взрослых) не могут быть взяты напрокат молодежью. Получите список этих фильмов в две колонки title и rating, отсортированных по названию фильма. Для решения этой задачи используйте условие с ключевым словом OR.  
```sql
SELECT 
  title, 
  rating 
FROM 
  film 
WHERE 
  rating = 'R' 
  OR rating = 'NC-17' 
ORDER BY 
  title;
  ```
### Задание №25
Фильмы с рейтингом PG (рекомендуется родительский контроль) и PG-13 (родители должны быть осторожны) могут просматриваться детьми только под контролем родителей. Получите список этих фильмов в двух столбцах title, rating, отсортированных по названию.
```sql
SELECT 
  title, 
  rating 
FROM 
  film 
WHERE 
  rating IN ('PG', 'PG-13') 
ORDER BY 
  title;
  ```
### Задание №26
Найдите всех сотрудников, занятых на проекте "Video Database". Напишите запрос, который выводит номер сотрудника, имя, фамилию, дату приёма на работу и код должности. Отсортируйте результат по фамилиям в алфавитном порядке. Если фамилии совпадают, отсортируйте по коду должности.
```sql
SELECT 
  E.EMP_NO, 
  E.FIRST_NAME, 
  E.LAST_NAME, 
  E.HIRE_DATE, 
  E.JOB_CODE 
FROM 
  EMPLOYEE E 
  JOIN EMPLOYEE_PROJECT EP ON E.EMP_NO = EP.EMP_NO 
  JOIN PROJECT PR ON EP.PROJ_ID = PR.PROJ_ID 
WHERE 
  PR.PROJ_NAME = 'Video Database' 
ORDER BY 
  E.LAST_NAME, 
  E.JOB_CODE;
  ```
### Задание №27
Напишите запрос, извлекающий список всех сотрудников, работающих за пределами США. Результат должен содержать все столбцы таблицы EMPLOYEE.
```sql
SELECT * 
FROM 
  EMPLOYEE 
WHERE 
  JOB_COUNTRY NOT LIKE 'USA';      
```
### Задание №28
Напишите запрос, извлекающий список всех сотрудников, принятых на работу в 1992 году. Результат должен содержать следующие столбцы FULL_NAME - полное имя сотрудника и HIRE_DATE - дата приёма на работу. Отсортируйте результат по возрастанию даты приёма.
```sql
SELECT 
    last_name || ', ' || first_name AS FULL_NAME, 
    hire_date AS HIRE_DATE
FROM 
    employee
WHERE 
    EXTRACT (YEAR FROM hire_date) = 1992
ORDER BY 
    HIRE_DATE ASC;
```
### Задание №29
Напишите SQL-запрос, чтобы получить список фильмов, отсутствующих в прокате (таблица inventory). Отобразите названия этих фильмов в столбце с названиемfilm_title в алфавитном порядке. Используйте для решения задачи соединение таблиц.
```sql
SELECT 
  title AS film_title 
FROM 
  film 
  LEFT JOIN inventory ON film.film_id = inventory.film_id 
WHERE 
  inventory_id IS NULL 
ORDER BY 
  film_title;
  ```
### Задание №30
Напишите SQL-запрос для получения списка языков из таблицы language, на которых нет доступных фильмов. Представьте результат в таблице с одним столбцом - language, отсортированным по алфавиту. Используйте для решения задачи соединение таблиц. 
```sql
SELECT 
  name AS language 
FROM 
  language 
  LEFT JOIN film ON language.language_id = film.language_id 
WHERE 
  film.language_id IS NULL 
ORDER BY 
  language;
  ```
### Задание №31
Напишите SQL-запрос, который выводит названия всех фильмов и их категорий из базы данных Sakila.
```sql
SELECT 
  f.title, 
  c.name AS name 
FROM 
  film f 
  JOIN film_category fc ON f.film_id = fc.film_id 
  JOIN category c ON fc.category_id = c.category_id 
ORDER BY 
  name ASC;
  ```
### Задание №32
Извлеките имя и домен из адресов электронной почты клиентов в базе данных Sakila. Напишите запрос, возвращающий три столбца: email, address – часть адреса электронной почты перед знаком «@» и domain — часть после «@». Отсортируйте результат по полю email.
```sql
SELECT 
  email, 
  SUBSTRING_INDEX(email, '@', 1) AS address, 
  SUBSTRING_INDEX(email, '@', -1) AS domain 
FROM 
  customer 
ORDER BY 
  email;
```
### Задание №33
Получить определения столбцов таблицы address.
```sql
 DESCRIBE address;
```
### Задание №34            
Получить список индексов таблицы film и их определений.
```sql
SHOW INDEX 
FROM 
  film;
```
### Задание №35
Найдите фильмы из базы данных Sakila, для которых нет записей об учавствоваших в них актёрах. Выведите результирующую с полями title, release_year отсортированных по названию фильма.
```sql
SELECT 
  title, 
  release_year 
FROM 
  film 
  LEFT JOIN film_actor ON film.film_id = film_actor.film_id 
WHERE 
  film_actor.actor_id IS NULL 
ORDER BY 
  title;
```
### Задание №36
Найдите клиентов чьё имя является фамилией другого клиента. Выведите таблицу с полями customer_id, first_name, last_name для первого клиента и такие же поля customer_id, first_name, last_name для второго. 
Отсортируйте по customer_id первого клиента.
```sql
SELECT 
  c1.customer_id AS customer_id, 
  c1.first_name AS first_name, 
  c1.last_name AS last_name, 
  c2.customer_id AS customer_id, 
  c2.first_name AS first_name, 
  c2.last_name AS last_name 
FROM 
  customer c1 
  JOIN (
    SELECT 
      customer_id, 
      first_name, 
      last_name 
    FROM 
      customer
  ) c2 
WHERE 
  c1.first_name = c2.last_name 
ORDER BY 
  c1.customer_id ASC;
```
### Задание №37
Найдите клиентов которые встречали друг друга в одном из пунктов проката. 
Выведите таблицу с полями meet_time - согласно времени аренды, store_id, customers список встречавшихся клиентов в формате JOHN SHOW, DAENERYS TARGARYEN - в порядке их фамилий. Результирующую таблицу отсортируйте по времени встречи и номеру пункта проката (Клиенты встречались если брали в аренду фильмы в одном отделении в одно время).
```sql
SELECT 
  r.rental_date AS meet_time, 
  s.store_id, 
  GROUP_CONCAT(
    DISTINCT CONCAT(c.first_name, ' ', c.last_name) 
    ORDER BY 
      c.last_name, 
      c.first_name SEPARATOR ','
  ) AS customers 
FROM 
  customer c 
  JOIN rental r ON r.customer_id = c.customer_id 
  JOIN staff s ON s.staff_id = r.staff_id 
GROUP BY 
  r.rental_date, 
  s.store_id 
HAVING 
  COUNT(*) > 1;
```
### Задание №38
Напишите SQL-запрос для поиска фильмов в базе данных Sakila, которые есть в наличии (в таблице inventory), но никогда не выдавались в прокат. Выведите названия этих фильмов в алфавитном порядке. Для решения задачи используйте соединение таблиц.
```sql
SELECT 
  film.title 
FROM 
  film 
  JOIN inventory ON film.film_id = inventory.film_id 
  LEFT JOIN rental ON inventory.inventory_id = rental.inventory_id 
WHERE 
  rental.rental_id IS NULL 
ORDER BY 
  film.title;
```
### Задание №39
Получите все фильмы в следующих категориях: Comedy, Music и Travel. Выведите таблицу со столбцами film_id, title и category, отсортированными по film_id. Напишите запрос без использования ключевого слова OR в условии.
```sql
SELECT 
  f.film_id, 
  f.title, 
  c.name AS category 
FROM 
  film f 
  JOIN film_category fc ON f.film_id = fc.film_id 
  JOIN category c ON fc.category_id = c.category_id 
WHERE 
  c.name = 'Comedy' 
UNION 
SELECT 
  f.film_id, 
  f.title, 
  c.name AS category 
FROM 
  film f 
  JOIN film_category fc ON f.film_id = fc.film_id 
  JOIN category c ON fc.category_id = c.category_id 
WHERE 
  c.name = 'Music' 
UNION 
SELECT 
  f.film_id, 
  f.title, 
  c.name AS category 
FROM 
  film f 
  JOIN film_category fc ON f.film_id = fc.film_id 
  JOIN category c ON fc.category_id = c.category_id 
WHERE 
  c.name = 'Travel' 
ORDER BY 
  film_id;
```
### Задание №40
Выберите имена и фамилии клиентов, чьи имя и фамилия начинаются на одну и ту же букву. Отсортируйте результат по имени и фамилии.
```sql
SELECT 
  first_name, 
  last_name 
FROM 
  customer 
WHERE 
  LEFT(first_name, 1)= LEFT(last_name, 1) 
ORDER BY 
  first_name, 
  last_name;
```
### Задание №41
Найдите все фильмы взятые в прокат KATIE ELLIOTT. Выведите результат в два столбца title и rating. Отсортируйте список так что бы сначала шли фильмы "для взрослых" (с рейтингом R), а затем все остальные по алфавиту.
```sql
SELECT 
  f.title, 
  f.rating 
FROM 
  customer c 
  JOIN rental r ON c.customer_id = r.customer_id 
  JOIN inventory i ON r.inventory_id = i.inventory_id 
  JOIN film f ON i.film_id = f.film_id 
WHERE 
  c.first_name = 'KATIE' 
  AND c.last_name = 'ELLIOTT' 
ORDER BY 
  CASE when f.rating = 'R' then 1 else 2 END, 
  f.title;
```

## Вычисления

### Задание №1
Напишите запрос для вычисления длины окружности диаметром 7. Результат выведите в колонке circle_perimeter.
```sql
SELECT 
  PI()* 7 AS circle_perimeter;
```
### Задание №2
Напишите запрос для вычисления площади круга радиусом 12. Результат округлите до шести десятичных знаков и выведите в колонке circle_area.
```sql
SELECT 
  pi()* 12 * 12 AS circle_area;
```
### Задание №3
Напишите запрос возвращающий таблицу значений факториала для целых чисел от 0 до 10. Таблица должна содержать две колонки n - число от 0 до 10 и f значение факториала этого числа.
```sql
WITH RECURSIVE Factorials (n, f) AS (
  SELECT 
    0 AS n, 
    1 AS f 
  UNION ALL 
  SELECT 
    n + 1, 
    f *(n + 1) 
  FROM 
    Factorials 
  Where 
    n < 10
) 
SELECT 
  n, 
  f 
FROM 
  Factorials;
```
### Задание №4
Сформируйте список фильмов в формате JSON вида 
{"id": 1, "title": "ACADEMY DINOSAUR", "category": "Documentary"} в таблице 
с одним столбцом film отсортированным по идентификатору фильма.
```sql
SELECT 
  JSON_OBJECT(
    'id', f.id, 'title', f.title, 'category', 
    c.category_name
  ) AS film 
FROM 
  film f 
  JOIN category c ON f.category_id = c.id 
ORDER BY 
  f.id;
```
### Задание №5
Получите все записи из таблицы address, где почтовый индекс представляет 
собой четное число. Выведите таблицу с двумя столбцами address_id и postal_code, отсортированными по address_id.
```sql
SELECT 
  address_id, 
  postal_code 
FROM 
  address 
WHERE 
  (postal_code % 2)= 0 
ORDER BY 
  address_id;
```
### Задание №6
Составьте общий список адресов электронной почты клиентов и персонала. Выведите таблицу со следующими столбцами:record_type – customer или employee, last_name, first_name, email — персональные данные. Отсортируйте таблицу по фамилии и затем по имени.  
```sql
SELECT 
  'customer' AS record_type, 
  last_name, 
  first_name, 
  email 
FROM 
  customer 
UNION ALL 
SELECT 
  'employee' AS record_type, 
  last_name, 
  first_name, 
  email 
FROM 
  staff 
ORDER BY 
  last_name ASC, 
  first_name;
```
### Задание №7
Составьте месячный счет за прокат фильмов DOROTHY TAYLOR в августе 2005 года. Счет должен представлять собой таблицу со следующими столбцами:
title – названия взятых напрокат фильмов. 
rental_date, return_date, payment_date — соответствующие даты, rental_rate - стоимость проката фильма, lateness_penalty - разница между ставкой аренды и уплаченной суммой, amount - оплаченная сумма. Отсортируйте таблицу по дате платежей. Добавьте в счет сводную строку с Total в столбце title, nulls значениями во всех столбцах данных и суммами в других столбцах.
```sql
SELECT 
  f.title, 
  r.rental_date, 
  r.return_date, 
  p.payment_date, 
  f.rental_rate, 
  p.amount - f.rental_rate AS lateness_penalty, 
  p.amount 
FROM 
  rental r 
  JOIN customer c ON r.customer_id = c.customer_id 
  JOIN payment p ON r.rental_id = p.rental_id 
  JOIN inventory i ON r.inventory_id = i.inventory_id 
  JOIN film f ON i.film_id = f.film_id 
WHERE 
  c.first_name = 'DOROTHY' 
  AND c.last_name = 'TAYLOR' 
  AND MONTH(r.rental_date) = 8 
  AND YEAR(r.rental_date) = 2005 
UNION ALL 
SELECT 
  'Total' AS title, 
  NULL AS rental_date, 
  NULL AS return_date, 
  NULL AS payment_date, 
  SUM(f.rental_rate) AS rental_rate, 
  SUM(p.amount - f.rental_rate) AS lateness_penalty, 
  SUM(p.amount) AS amount 
FROM 
  rental r 
  JOIN customer c ON r.customer_id = c.customer_id 
  JOIN payment p ON r.rental_id = p.rental_id 
  JOIN inventory i ON r.inventory_id = i.inventory_id 
  JOIN film f ON i.film_id = f.film_id 
WHERE 
  c.first_name = 'DOROTHY' 
  AND c.last_name = 'TAYLOR' 
  AND MONTH(r.rental_date) = 8 
  AND YEAR(r.rental_date) = 2005 
ORDER BY 
  CASE WHEN title = 'Total' THEN 1 ELSE 0 END, 
  payment_date;
```
### Задание №8
Составьте список фамилий встречающихся как среди пользователей так и среди актёров. Выведите таблицу с одной колонкой last_name отсортированной по алфавиту.
```sql
SELECT 
  last_name 
FROM 
  customer 
INTERSECT 
SELECT 
  last_name 
FROM 
  actor 
ORDER BY 
  last_name;
```
### Задание №9
Найдите в таблице customer имена палиндромы. Отсортируйте результат по first_name.
```sql
SELECT 
  first_name 
FROM 
  customer 
WHERE 
  first_name = REVERSE(first_name) 
ORDER BY 
  first_name;
```
### Задание №10
Выведите список клиентов в формате Meladze M. (фамилия с большой буквы плюс первая буква имени с точкой) в столбце customer_name. Отсортируйте результат по фамилии.
```sql
SELECT 
  concat(
    UPPER(
      LEFT(last_name, 1)
    ), 
    LOWER(
      MID(
        last_name, 
        2, 
        LENGTH(last_name)
      )
    ), 
    ' ', 
    UPPER(
      LEFT(first_name, 1)
    ), 
    '.'
  ) AS customer_name 
FROM 
  customer 
ORDER BY 
  last_name;
```
## Агрегатные функции

### Задание №1
Найдите среднюю продолжительность фильма. Результат выведите в колонке avg_film_length.
```sql
SELECT 
  AVG (length) AS avg_film_length 
FROM 
  film;
```
### Задание №2
Найдите минимальную и максимальную стоимость замены пленки.
Отобразите результат в виде таблицы с двумя столбцами: minimal_replacement_cost и maximal_replacement_cost.
```sql
SELECT 
  MIN(replacement_cost) AS maximal_replacement_cost, 
  MAX(replacement_cost) AS minimal_replacement_cost 
FROM 
  film;
```
### Задание №3
Найдите среднее время проката фильма (в днях). Отобразите результат в колонке с именем average_rental_time. Время аренды рассчитывается как разница между return_date и rental_date в таблице аренда. Округлите результат до ближайшего целого числа.
```sql
SELECT 
  ROUND(
    AVG(
      DATEDIFF(return_date, rental_date)
    )
  ) AS average_rental_time 
FROM 
  rental 
WHERE 
  rental_date IS NOT NULL;
```
### Задание №4
Найдите среднее время проката фильма. Отобразите результат в виде таблицы с одним столбцом average_rental_time. Время аренды рассчитывается как разница между return_date и rental_date в таблице rental.
```sql
SELECT 
  AVG(
    DATEDIFF(return_date, rental_date)
  ) AS average_rental_time 
FROM 
  rental;
```
### Задание №5
Найти количество сотрудников в каждом подразделении. Выведите имя подразделения DEPARTMENT и число сотрудников в нём EMP_COUNT. Отсортируйте результат по убыванию числа сотрудников.
```sql
SELECT 
  DEPARTMENT, 
  COUNT(E.EMP_NO) AS EMP_COUNT 
FROM 
  DEPARTMENT D 
  LEFT JOIN EMPLOYEE E ON D.DEPT_NO = E.DEPT_NO 
GROUP BY 
  DEPARTMENT 
ORDER BY 
  EMP_COUNT DESC;
```
### Задание №6
Найти количество фильмов в каждой категории. Выведите таблицу состоящую из двух колонок category и film_count отсортируйте её по названию категорий в алфавитном порядке.  
```sql
SELECT 
  c.name AS category, 
  COUNT(film_id) AS film_count 
FROM 
  category c 
  LEFT JOIN film_category fc ON c.category_id = fc.category_id 
GROUP BY 
  c.name 
ORDER BY 
  category;
```
### Задание №7
Найдите среднюю стоимость проката фильма для каждой категории. Результат выведите в две колонки category и avg_rental_rate отсортировав по убыванию цены.
```sql
SELECT 
  c.name AS category, 
  AVG(rental_rate) AS avg_rental_rate 
FROM 
  category c 
  JOIN film_category fc ON c.category_id = fc.category_id 
  JOIN film f ON fc.film_id = f.film_id 
GROUP BY 
  1 
ORDER BY 
  2 DESC;
```
### Задание №8
Найдите минимальную и максимальную и среднюю продолжительность фильма для каждой категории. Отобразите результат в виде таблицы с колонками: category - название категории фильмов, min_length, mах_length и avg_length отсортированной по категории в алфавитном порядке.
```sql
SELECT 
  c.name AS category, 
  MIN(f.length) AS min_length, 
  MAX(f.length) AS max_length, 
  AVG(f.length) AS avg_length 
FROM 
  film f 
  JOIN film_category fc ON f.film_id = fc.film_id 
  JOIN category c ON fc.category_id = c.category_id 
GROUP BY 
  c.name 
ORDER BY 
  c.name;
```
### Задание №9
Найдите категории со средней продолжительностью фильма более двух часов. Отобразите результат в виде таблицы с колонками: category - название категории фильмов и avg_length отсортированной по убыванию средней длины фильма.
```sql 
SELECT 
  c.name AS category, 
  AVG(length) AS avg_length 
FROM 
  film f 
  JOIN film_category fc ON fc.film_id = f.film_id 
  JOIN category c ON fc.category_id = c.category_id 
GROUP BY 
  1 
HAVING 
  avg_length > 120 
ORDER BY 
  avg_length DESC;
```
## Подзапросы

### Задание №1
Напишите запрос, который возвращает адреса и почтовые индексы всех адресов, расположенных в London. Не используйте JOIN для этой задачи.
```sql
SELECT 
  address, 
  postal_code 
FROM 
  address 
WHERE 
  city_id =(
    SELECT 
      city_id 
    FROM 
      city 
    WHERE 
      city = 'London' 
    LIMIT 
      1
  );
```
### Задание №2
Найдите клиентов ни разу не бравших в аренду фильмы с участием EMILY DEE.
В качестве результата выведите таблицу с колонками last_name, first_name - фамилия и имя клиента. Отсортируйте список по фамилии клиента.
```sql
SELECT 
  c.last_name, 
  c.first_name 
FROM 
  customer c 
WHERE 
  NOT EXISTS (
    SELECT 
      rental_id 
    FROM 
      rental r 
      JOIN inventory i ON r.inventory_id = i.inventory_id 
      JOIN film_actor fa ON i.film_id = fa.film_id 
      JOIN actor a ON fa.actor_id = a.actor_id 
    WHERE 
      r.customer_id = c.customer_id 
      AND a.first_name = 'Emily' 
      AND a.last_name = 'Dee'
  ) 
ORDER BY 
  c.last_name;
```
### Задание №3
В случае утери, кражи, порчи или невозврата арендованного диска с клиента взимается стоимость замены (replacement_cost). Найдите в базе данных фильмы с самой высокой стоимостью замены используя условие с под-запросом. Напишите запрос, который возвращает поля film_id, title и replacement_cost в возрастающем порядке поля film_id.  
```sql
SELECT 
  film_id, 
  title, 
  replacement_cost 
FROM 
  film 
WHERE 
  replacement_cost IN (
    SELECT 
      max(replacement_cost) 
    FROM 
      film
  ) 
ORDER BY 
  film_id;
```
### Задание №4
Напишите SQL-запрос, чтобы найти фильмы, стоимость проката которых выше средней стоимости всех фильмов. Используйте подзапрос для расчета среднего рейтинга. Полученная таблица должна включать следующие столбцы: film_id - идентификатор фильма, title - название фильма и rental_rate - стоимость проката фильма.
Отсортируйте результат по убыванию арендной ставки.
```sql
SELECT 
  film_id, 
  title, 
  rental_rate 
FROM 
  film 
WHERE 
  rental_rate >(
    SELECT 
      AVG(rental_rate) 
    FROM 
      film
  ) 
ORDER BY 
  rental_rate DESC;
```
### Задание №5
Создайте запрос SQL, чтобы найти клиентов, которые взяли напрокат больше фильмов, 
чем среднее количество прокатов среди всех клиентов. Используйте подзапрос для расчета среднего количества аренд. Результирующая таблица должна содержать следующие столбцы: customer_id – уникальный идентификатор клиента, 
first_name – имя клиента, last_name — фамилия клиента. rental_count — количество взятых напрокат фильмов.
```sql
WITH customer_rentals AS (
  SELECT 
    c.customer_id, 
    c.first_name, 
    c.last_name, 
    count(r.rental_id) AS rental_count 
  FROM 
    customer c 
    JOIN rental r ON c.customer_id = r.customer_id 
  GROUP BY 
    c.customer_id, 
    c.first_name, 
    c.last_name
) 
SELECT 
  cr.customer_id, 
  cr.first_name, 
  cr.last_name, 
  rental_count 
FROM 
  customer_rentals cr 
WHERE 
  rental_count >(
    SELECT 
      AVG(rental_count) 
    FROM 
      customer_rentals
  );
```
### Задание №6
В этом задании вы нашли среднее время проката фильма (в днях). Напишите запрос, 
чтобы получить список фильмов, у которых время проката ниже среднего. Отобразите результат в таблице со столбцами film_id, title и average_rental_time. Отсортируйте таблицу по столбцу film_id.    
```sql
WITH AverageRentalTimes AS (
  SELECT 
    f.film_id, 
    f.title, 
    ROUND(
      AVG(
        DATEDIFF(r.return_date, r.rental_date)
      )
    ) AS average_rental_time 
  FROM 
    rental r 
    JOIN inventory i ON r.inventory_id = i.inventory_id 
    JOIN film f ON i.film_id = f.film_id 
  GROUP BY 
    f.film_id, 
    f.title
), 
OverallAverageRentalTime AS (
  SELECT 
    ROUND(
      AVG(
        DATEDIFF(return_date, rental_date)
      )
    ) AS overall_average_rental_time 
  FROM 
    rental
) 
SELECT 
  a.film_id, 
  a.title, 
  a.average_rental_time 
FROM 
  AverageRentalTimes a 
  JOIN OverallAverageRentalTime o ON a.average_rental_time < o.overall_average_rental_time 
ORDER BY 
  a.film_id;
```
### Задание №7
Найдите фильмы из базы данных Sakila, для которых нет записей об учавствоваших в них актёрах. Выведите результирующую с полями title, release_year отсортированных по названию фильма.
```sql
SELECT 
  title, 
  release_year 
FROM 
  film f 
WHERE 
  NOT EXISTS (
    SELECT 
      actor_id, 
      film_id 
    FROM 
      film_actor fa 
    WHERE 
      fa.film_id = f.film_id
  ) 
ORDER BY 
  title;
```
### Задание №8
Рейтинг NC-17 — это рейтинг фильмов, подходящих только для взрослых. Найдите всех актеров, которые никогда не снимались в фильмах с этим рейтингом. Выведите результирующую таблицу из двух столбцов first_name и last_name, отсортированных по фамилии в алфавитном порядке.  
```sql
SELECT 
  first_name, 
  last_name 
FROM 
  actor a 
WHERE 
  actor_id NOT IN (
    SELECT 
      actor_id 
    FROM 
      film_actor fa 
      JOIN film f ON fa.film_id = f.film_id 
    WHERE 
      f.rating = 'NC-17'
  ) 
ORDER BY 
  last_name;
```
## Аналитические запросы

### Задание №1
Найдите среднее время активности клиента (время между датами первой и последней аренды) в днях. Результат выведите в поле avg_life_time, округлив его до целого числа.
```sql
SELECT 
  ROUND(
    AVG(life_time)
  ) AS avg_life_time 
FROM 
  (
    SELECT 
      DATEDIFF(
        MAX(rental_date), 
        MIN(rental_date)
      ) AS life_time 
    FROM 
      rental 
    GROUP BY 
      customer_id
  ) AS customer_life_times;
```
### Задание №2
Найдите среднюю сумму выручки с приносимой каждым платящим клиентом. Результат выведите в поле avg_customer_payment, округлив его до двух десятичных знаков. 
```sql
SELECT 
  ROUND(
    SUM(amount) / COUNT(DISTINCT customer_id), 
    2
  ) AS avg_customer_payment 
FROM 
  payment;
```
### Задание №4
Для каждого клиента в таблице payment найдите даты его первого и последнего платежа, а также сумму всех платежей. Запрос должен вернуть четыре колонки: customer_id, first_payment_date – дата первого платежа (в формате «ГГГГ-ММ-ДД»), last_payment_date – дата последнего платежа (в формате «ГГГГ-ММ-ДД») и total_paid – общая сумма платежей клиента отсортированных по убыванию суммы платежей (в случае равных сумм платежей по возрастанию customer_id).   
```sql
SELECT 
  customer_id, 
  DATE(
    MIN(payment_date)
  ) AS first_payment_date, 
  DATE(
    MAX(payment_date)
  ) AS last_payment_date, 
  SUM(amount) AS total_paid 
FROM 
  payment 
GROUP BY 
  customer_id 
ORDER BY 
  total_paid DESC, 
  customer_id ASC;
```
### Задание №5
Напишите запрос для расчета суммы платежей за каждый месяц и отображения результатов в порядке убывания месяца платежа. Запрос должен вернуть только два столбца: payment_month – месяц платежа (в формате «ГГГГ-ММ») и payment_amount – общая сумма платежа за каждый месяц.  
```sql
SELECT 
  DATE_FORMAT(payment_date, '%Y-%m') AS payment_month, 
  SUM(amount) AS payment_amount 
FROM 
  payment 
GROUP BY 
  payment_month 
ORDER BY 
  payment_month DESC;
```
### Задание №6
Напишите запрос для расчета суммы платежей за каждый месяц 2005 года и нарастающей суммы с начала года. Запрос должен вернуть три столбца: payment_month – месяц платежа (в формате «ГГГГ-ММ»), monthly_amount – общая сумма платежей за месяц и yearly_amount – сумма с начала года.  
```sql 
SELECT 
  DATE_FORMAT(payment_date, '%Y-%m') AS payment_month, 
  SUM(amount) AS monthly_amount, 
  SUM(
    SUM(amount)
  ) OVER (
    ORDER BY 
      DATE_FORMAT(payment_date, '%Y-%m')
  ) AS yearly_amount 
FROM 
  payment 
WHERE 
  YEAR(payment_date) = 2005 
GROUP BY 
  payment_month 
ORDER BY 
  payment_month;
```




