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

*5. Вывести количество рейсов, совершенных на TU-134 ([ссылка](https://sql-academy.org/ru/trainer/tasks/5))*

<details>
<summary>Решение</summary>

``` sql
SELECT COUNT(plane) AS COUNT
FROM Trip
WHERE plane = 'TU-134'
```
</details>

*6. Какие компании совершали перелеты на Boeing ([ссылка](https://sql-academy.org/ru/trainer/tasks/6))*

<details>
<summary>Решение</summary>

``` sql
SELECT DISTINCT name
FROM Company
	INNER JOIN Trip ON Company.id = Trip.Company
WHERE Trip.plane = 'Boeing'
```
</details>

*7. Вывести все названия самолётов, на которых можно улететь в Москву (Moscow) ([ссылка](https://sql-academy.org/ru/trainer/tasks/7))*

<details>
<summary>Решение</summary>

``` sql
SELECT DISTINCT plane
FROM Trip
WHERE town_to = 'Moscow'
```
</details>

*9. Какие компании организуют перелеты из Владивостока (Vladivostok)? ([ссылка](https://sql-academy.org/ru/trainer/tasks/9))*

<details>
<summary>Решение</summary>

``` sql
SELECT name
FROM Company
	INNER JOIN Trip ON Company.id = Trip.company
WHERE town_to = 'Vladivostok'
```
</details>

*12. Выведите идентификаторы всех рейсов и количество пассажиров на них. Обратите внимание, что на каких-то рейсах пассажиров может не быть. В этом случае выведите число "0". ([ссылка](https://sql-academy.org/ru/trainer/tasks/12))*

<details>
<summary>Решение</summary>

``` sql
SELECT trip,
	IF(COUNT(passenger) = 0, 0, SUM(passenger)) AS COUNT
FROM Pass_in_trip
GROUP BY trip;
```
</details>

*14. В какие города летал Bruce Willis ([ссылка](https://sql-academy.org/ru/trainer/tasks/14))*

<details>
<summary>Решение</summary>

``` sql
SELECT town_to
FROM trip
	JOIN Pass_in_trip ON Trip.id = Pass_in_trip.trip
	JOIN Passenger ON Pass_in_trip.passenger = Passenger.id
WHERE name = 'Bruce Willis';
```
</details>

*15. Выведите идентификатор пассажира Стив Мартин (Steve Martin) и дату и время его прилёта в Лондон (London) ([ссылка](https://sql-academy.org/ru/trainer/tasks/15))*

<details>
<summary>Решение</summary>

``` sql
SELECT time_in
FROM trip
	JOIN Pass_in_trip ON Trip.id = Pass_in_trip.trip
	JOIN Passenger ON Pass_in_trip.passenger = Passenger.id
WHERE Passenger.name = 'Steve Martin'
	AND Trip.town_to = 'London';
```
</details>
