# Задачи 

*1. Вывести имена всех людей, которые есть в базе данных авиакомпаний ([ссылка](https://sql-academy.org/ru/trainer/tasks/1))*

<details>
<summary>Решение</summary>

``` sql
SELECT name
FROM Passenger
```
</details>

*2. Вывести названия всеx авиакомпаний ([ссылка](https://sql-academy.org/ru/trainer/tasks/2))*

<details>
<summary>Решение</summary>

``` sql
SELECT name
FROM Company;
```
</details>

*3. Вывести все рейсы, совершенные из Москвы ([ссылка](https://sql-academy.org/ru/trainer/tasks/3))*

<details>
<summary>Решение</summary>

``` sql
SELECT *
FROM Trip
WHERE town_from LIKE 'Moscow'
```
</details>

*4. Вывести имена людей, которые заканчиваются на "man" ([ссылка](https://sql-academy.org/ru/trainer/tasks/4))*

<details>
<summary>Решение</summary>

``` sql
SELECT name
FROM Passenger
WHERE name LIKE '%man'
```
</details>

