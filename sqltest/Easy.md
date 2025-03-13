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

*27. Напишите SQL запрос, чтобы найти фильмы, стоимость проката которых выше средней стоимости всех фильмов. ([ссылка](https://sqltest.online/ru/question/simple/find-movies-with-above-average-rental-rates))*

<details>
<summary>Решение</summary>

``` sql
select  film_id , title , rental_rate 
from film
where  rental_rate > (select avg( rental_rate ) from film)
group by film_id
order by 3 desc
```
</details>

*28. Из таблицы customer выберите все записи о фамилии - last_name, имени - first_name и адресе электронной почты email отсортировав их по фамилии в алфавитном порядке. ([ссылка](https://sqltest.online/ru/question/simple/get-list-of-clients))*

<details>
<summary>Решение</summary>

``` sql
select  last_name , first_name , email 
from customer
group by  customer_id 
order by 1
```
</details>

*29. Напишите SQL запрос, который выводит список уникальных значений rating из таблицы film в алфавитном порядке. ([ссылка](https://sqltest.online/ru/question/simple/get-a-list-of-movie-ratings))*

<details>
<summary>Решение</summary>

``` sql
select distinct rating 
from film
order by 1
```
</details>

*30. Получить список таблиц в базе данных sakila. ([ссылка](https://sqltest.online/ru/question/simple/get-list-of-tables))*

<details>
<summary>Решение</summary>

``` sql
select table_name as Tables_in_sakila from INFORMATION_SCHEMA.TABLES where table_schema = 'sakila'; 
```
</details>

*31. Получить определения столбцов таблицы address ([ссылка](https://sqltest.online/ru/question/simple/get-table-columns-data))*

<details>
<summary>Решение</summary>

``` sql
DESCRIBE address
```
</details>

*32. Получить список индексов таблицы film и их определений ([ссылка](https://sqltest.online/ru/question/simple/get-list-of-indexes))*

<details>
<summary>Решение</summary>

``` sql
SHOW INDEX FROM film;
```
</details>

*33. Найдите фильмы из базы данных Sakila, в которых нет записей об актерах. ([ссылка](https://sqltest.online/ru/question/simple/find-movies-without-cast-records))*

<details>
<summary>Решение</summary>

``` sql
select  title , release_year 
from film f1
where not exists (select film_id from film_actor f2 where f1.film_id = f2.film_id)
```
</details>

*34. Фильмы с рейтингом PG (рекомендуется родительский контроль) и PG-13 (родители должны быть осторожны) могут просматриваться детьми только под контролем родителей. 
Получите список этих фильмов в двух столбцах title, rating, отсортированных по названию. ([ссылка](https://sqltest.online/ru/question/simple/get-the-restricted-films-list))*

<details>
<summary>Решение</summary>

``` sql
select  title , rating 
from film
where rating like '%PG%'
```
</details>

*35. Фильмы с рейтингом R (Ограниченный доступ) и NC-17 (Только для взрослых) не могут быть взяты напрокат молодежью. 
Получите список этих фильмов в две колонки title и rating, отсортированных по названию фильма. ([ссылка](https://sqltest.online/ru/question/simple/get-list-of-restricted-films))*

<details>
<summary>Решение</summary>

``` sql
select  title , rating 
from film
where rating = 'R' or rating = 'NC-17'
group by film_id
order by 1
```
</details>

*36. Найдите все фильмы с рейтингом NC-17 (только для взрослых), в описании которых содержится подстрока Database Administrator.  ([ссылка](https://sqltest.online/ru/question/simple/find-adult-only-films-about-database-administrator))*

<details>
<summary>Решение</summary>

``` sql
select  title , description , release_year 
from film
where rating = 'NC-17' and  description like '%Database Administrator%'
group by film_id
order by 1
```
</details>

*37. ННапишите запрос на добавление новой записи в таблицу address  ([ссылка](https://sqltest.online/ru/question/simple/create-new-address-record))*

<details>
<summary>Решение</summary>

``` sql
insert into address( address , district , city_id , postal_code , phone )
values('898 Homer St', 'Yaletown', 565, 26336, 0523323201)
```
</details>

*38. Обновите почтовый индекс в таблице address по адресу 1411 Lillydale Drive на 365894.  ([ссылка](https://sqltest.online/ru/question/simple/update-the-postal-code))*

<details>
<summary>Решение</summary>

``` sql
update address
set  postal_code = 365894
where  address = '1411 Lillydale Drive'
```
</details>

*39. Удалите из таблицы customer записи о неактивных клиентах.  ([ссылка](https://sqltest.online/ru/question/simple/remove-customer-records))*

<details>
<summary>Решение</summary>

``` sql
delete from customer
where active = 0
```
</details>

*40. Получите все записи из таблицы address, для которых не указан почтовый индекс.   ([ссылка](https://sqltest.online/ru/question/simple/find-addresses-without-postal-code))*

<details>
<summary>Решение</summary>

``` sql
select *
from address
where  postal_code is Null
order by address_id
```
</details>

*41. Получите все записи из таблицы address, где почтовый индекс представляет собой четное число.   ([ссылка](https://sqltest.online/ru/question/simple/find-an-addresses-with-even-postal-codes))*

<details>
<summary>Решение</summary>

``` sql
select  address_id , postal_code 
from address
where postal_code%2 = 0
order by 1
```
</details>

*42. Составьте список фамилий встречающихся как среди пользователей так и среди актёров.   ([ссылка](https://sqltest.online/ru/question/simple/build-shared-surnames-list))*

<details>
<summary>Решение</summary>

``` sql
select last_name
from customer
intersect
select last_name
from actor
order by 1
```
</details>

*43. Получите список самолетов с дальностью полета более 5000 км. Отсортируйте результаты в порядке убывания дальности.   ([ссылка](https://sqltest.online/ru/question/simple/find-long-range-aircrafts))*

<details>
<summary>Решение</summary>

``` sql
select * 
from  aircrafts_data 
where  range > 5000
order by range desc
```
</details>

*44. Найдите в таблице customer имена палиндромы. ([ссылка](https://sqltest.online/ru/question/simple/find-the-palindrome-names))*

<details>
<summary>Решение</summary>

``` sql
select  first_name
from  customer 
where first_name = reverse( first_name )
group by  customer_id 
order by  first_name 
```
</details>

*53. Обновите стоимость аренды фильма и стоимость замены диска для фильмов в категории NC-17 (фильмы для взрослых). Напишите запрос который увеличивает стоимость проката на 20%, а стоимость замены на $5. ([ссылка](https://sqltest.online/ru/question/simple/perform-price-update))*

<details>
<summary>Решение</summary>

``` sql
update film
set  rental_rate =  rental_rate * 1.20,
 replacement_cost = replacement_cost + 5
 where  rating = 'NC-17'
```
</details>

*54. В адресе клиента JO FOWLER обнаружена ошибка. Исправьте её указав верный почтовый индекс 98322. ([ссылка](https://sqltest.online/ru/question/simple/update-customer-address))*

<details>
<summary>Решение</summary>

``` sql
update address
join customer using(address_id)
set postal_code = 98322
where first_name = 'JO'
```
</details>

*55. Выполните коррекцию стоимости аренды фильмов следующим образом: стоимость аренды для фильмов в категории G должна быть снижена на 5%,  для фильмов в категориях R и NC-17 (фильмы для взрослых) повышена на 20%, для всех остальных фильмов стоимость повышается на 5%. ([ссылка](https://sqltest.online/ru/question/simple/adjust-the-rental-cost))*

<details>
<summary>Решение</summary>

``` sql
update film
set  rental_rate = case
                        when  rating = 'G' then rental_rate * 0.95
                        when rating = 'R' or rating = 'NC-17' then rental_rate * 1.2
                        else rental_rate * 1.05
                        end
```
</details>

*56. Обновите таблицу film так чтобы стоимость замены replacement_cost стала равна пятикратной стоимости аренды rental_rate округленной вверх до ближайшего целого значения. ([ссылка](https://sqltest.online/ru/question/simple/update-replacement-cost))*

<details>
<summary>Решение</summary>

``` sql
update film
set replacement_cost = ceil(rental_rate * 5)
```
</details>

*57. Напишите запрос, который возвращает завтрашнюю дату в формате ГГГГ-ММ-ДД в столбце с именем tomorrow. ([ссылка](https://sqltest.online/ru/question/simple/find-the-tomorrow-date))*

<details>
<summary>Решение</summary>

``` sql
SELECT DATE_ADD(CURDATE(), INTERVAL 1 DAY) AS tomorrow;
```
</details>

*60. Выведите список подразделений и их местонахождений отсортировав его по названию в алфавитном порядке. ([ссылка](https://sqltest.online/ru/question/simple/display-list-of-departments))*

<details>
<summary>Решение</summary>

``` sql
select  DEPARTMENT , LOCATION 
from  DEPARTMENT 
order by 1
```
</details>
