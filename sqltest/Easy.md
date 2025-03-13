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
