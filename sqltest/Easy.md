# Решения бесплатных задач лёгкого уровня с сайта sqltest

*1. Выберите все записи из таблицы actor. ([ссылка](https://sqltest.online/ru/question/simple/get-the-actors))*

<details>
<summary>Решение</summary>

``` sql
SELECT *
FROM   actor
```
</details>

*2. Получите список значений из колонки name таблицы language. ([ссылка](https://sqltest.online/ru/question/simple/get-the-languages-list))*

<details>
<summary>Решение</summary>

``` sql
SELECT NAME
FROM   language  
```
</details>

*3. Выберите все значения имён и фамилий актёров из таблицы actor. ([ссылка](https://sqltest.online/ru/question/simple/get-list-of-actors-namest))*

<details>
<summary>Решение</summary>

``` sql
SELECT first_name,
       last_name
FROM   actor  
```
</details>

*4. Получите все данные об аэропортах в порядке их кодов. ([ссылка](https://sqltest.online/ru/question/simple/get-airports-data))*

<details>
<summary>Решение</summary>

``` sql
SELECT *
FROM   airports_data
ORDER  BY airport_code
```
</details>

*5. Из таблицы staff выберите все данные сотрудников чья фамилия начинается с буквы 'K' ([ссылка](https://sqltest.online/ru/question/simple/staff-family-starts-with-k))*

<details>
<summary>Решение</summary>

``` sql
SELECT *
FROM   staff
WHERE  family LIKE 'K%'
```
</details>

*6. Получите столбец name из таблицы language в алфавитном порядке. ([ссылка](https://sqltest.online/ru/question/simple/get-the-ordered-list-of-languages))*

<details>
<summary>Решение</summary>

``` sql
SELECT NAME
FROM   language
GROUP  BY language_id
ORDER  BY 1 
```
</details>

*7. Получите названия пяти самых длинных фильмов, отсортированных по продолжительности в порядке убывания. ([ссылка](https://sqltest.online/ru/question/simple/get-the-sorted-list-of-films-with-limit))*

<details>
<summary>Решение</summary>

``` sql
SELECT title
FROM   film
GROUP  BY film_id
ORDER  BY length DESC
LIMIT  5
```
</details>

*8. Найдите сотрудников, работающих в магазине номер 1, и получите все их данные. ([ссылка](https://sqltest.online/ru/question/simple/find-stuff-members-by-condition))*

<details>
<summary>Решение</summary>

``` sql
SELECT *
FROM   staff
WHERE  store_id = 1
```
</details>

*9. Найдите все фильмы продолжительностью более 3 часов и получите их название, год выпуска и продолжительность, отсортированные по продолжительности в порядке возрастания. ([ссылка](https://sqltest.online/ru/question/simple/get-the-sorted-list-of-films-with-condition))*

<details>
<summary>Решение</summary>

``` sql
SELECT title,
       release_year,
       length
FROM   film
WHERE  length > 180
GROUP BY film_id
ORDER BY 3 
```
</details>

*10. Найдите все фильмы, в описании которых есть слово Student. Выведите названия фильмов в алфавитном порядке. ([ссылка](https://sqltest.online/ru/question/simple/find-film-names-by-description))*

<details>
<summary>Решение</summary>

``` sql
SELECT title
FROM   film
WHERE  description LIKE '%Student%'
```
</details>

*11. Найдите актеров по имени Scarlett. ([ссылка](https://sqltest.online/ru/question/simple/find-the-actors-by-name))*

<details>
<summary>Решение</summary>

``` sql
select *
from actor
where first_name = 'Scarlett'
```
</details>


*12. Найдите среднюю продолжительность фильма. Результат выведите в колонке avg_film_length ([ссылка](https://sqltest.online/ru/question/simple/find-the-average-length-of-a-movie))*

<details>
<summary>Решение</summary>

``` sql
select avg(length) as avg_film_length
from film
```
</details>

*13. Напишите запрос, извлекающий список всех сотрудников, работающих за пределами США. ([ссылка](https://sqltest.online/ru/question/simple/find-foreign-employees))*

<details>
<summary>Решение</summary>

``` sql
select *
from EMPLOYEE
where  JOB_COUNTRY <> 'USA'
```
</details>

*14. Выберите названия фильмов из таблицы film. Отсортируйте полученный список по алфавиту ([ссылка](https://sqltest.online/ru/question/simple/get-an-ordered-list-of-movies))*

<details>
<summary>Решение</summary>

``` sql
SELECT title
FROM   film
ORDER  BY 1  
```
</details>

*15. Выберите название, стоимость проката и продолжительность фильмов из таблицы film. ([ссылка](https://sqltest.online/ru/question/simple/get-a-list-of-movies-sorted-by-multiple-fields))*

<details>
<summary>Решение</summary>

``` sql
SELECT title,
       rental_rate,
       length
FROM   film
GROUP  BY film_id
ORDER  BY 2 DESC,
          3 
```
</details>


*16. Выберите фамилии, имена и электронные адреса клиентов у которых фамилия начинается с буквы "A" ([ссылка](https://sqltest.online/ru/question/simple/find-clients-starting-with-the-letter-a))*

<details>
<summary>Решение</summary>

``` sql
SELECT last_name,
       first_name,
       email
FROM   customer
WHERE  last_name LIKE 'A%'
ORDER  BY 1
```
</details>

*17. Выберите фамилии, имена и электронные адреса клиентов у которых и имя и фамилия начинается с буквы "A" ([ссылка](https://sqltest.online/ru/question/simple/find-clients-starting-with-the-letter-a-))*

<details>
<summary>Решение</summary>

``` sql
select 
  last_name, 
  first_name, 
  email 
from 
  customer 
where 
  first_name like 'A%' 
  AND last_name like 'A%' 
order by 
  1
```
</details>

*18. Найдите минимальную и максимальную стоимость замены пленки. ([ссылка](https://sqltest.online/ru/question/simple/find-the-minimal-and-maximal-film-rental-cost))*

<details>
<summary>Решение</summary>

``` sql
select 
  min(replacement_cost) as minimal_replacement_cost, 
  max(replacement_cost) as maximal_replacement_cost 
from 
  film
```
</details>

*19. Найдите среднее время проката фильма (в днях). ([ссылка](https://sqltest.online/ru/question/simple/find-film-average-rental-time-datediff))*

<details>
<summary>Решение</summary>

``` sql
select 
  avg(
    datediff(return_date, rental_date)
  ) as average_rental_time 
from 
  rental
```
</details>

*20. Выберите название, описание и год выхода фильмов из таблицы film. ([ссылка](https://sqltest.online/ru/question/simple/get-the-first-movies-in-alphabetical-order))*

<details>
<summary>Решение</summary>

``` sql
select 
  title, 
  description, 
  release_year 
from 
  film 
order by 
  1 
limit 
  10
```
</details>

*21. Найдите все фильмы продолжительностью более трёх часов ([ссылка](https://sqltest.online/ru/question/simple/find-long-movies))*

<details>
<summary>Решение</summary>

``` sql
select 
  title, 
  description, 
  length 
from 
  film 
where 
  length > 180 
group by 
  film_id 
order by 
  3
```
</details>

*22. Подсчитайте количество фильмов взятых в аренду в зависимости от дня недели ([ссылка](https://sqltest.online/ru/question/simple/find-the-distribution-of-customer-activity))*

<details>
<summary>Решение</summary>

``` sql
select dayofweek(payment_date) as dow, count(rental_id) as rentals_count 
from payment
group by dayofweek(payment_date)
order by rentals_count  desc
```
</details>

*23. Напишите запрос, извлекающий список всех сотрудников, принятых на работу в 1992 году. ([ссылка](https://sqltest.online/ru/question/simple/find-employees-by-hire-date))*

<details>
<summary>Решение</summary>

``` sql
 select   FULL_NAME ,  HIRE_DATE 
 from employee
 where EXTRACT(YEAR FROM  HIRE_DATE ) = 1992
```
</details>

*24. Напишите запрос для вычисления площади круга радиусом 12. ([ссылка](https://sqltest.online/ru/question/simple/calculate-the-area-of-a-circle))*

<details>
<summary>Решение</summary>

``` sql
select round(PI() * (12 * 12),6) as circle_area
```
</details>

*25. Напишите запрос для вычисления длины окружности диаметром 7. ([ссылка](https://sqltest.online/ru/question/simple/calculate-circle-perimeter))*

<details>
<summary>Решение</summary>

``` sql
select pi() * 7 as circle_perimeter
```
</details>

*26. Найдите всех активных в данный момент клиентов (active = 1) в таблице customer ([ссылка](https://sqltest.online/ru/question/simple/find-active-customers))*

<details>
<summary>Решение</summary>

``` sql
select  customer_id , first_name , last_name 
from customer
where active = 1
```
</details>
