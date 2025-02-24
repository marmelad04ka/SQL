# Решения бесплатных задач лёгкого уровня с сайта sql-academy 

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

*19. Определить, кто из членов семьи покупал картошку (potato) ([ссылка](https://sql-academy.org/ru/trainer/tasks/19))*

<details>
<summary>Решение</summary>

``` sql
SELECT DISTINCT STATUS
FROM FamilyMembers
	JOIN Payments ON FamilyMembers.member_id = Payments.family_member
	JOIN Goods ON Payments.good = Goods.good_id
WHERE good_name = 'potato';
```
</details>

*22. Найти имена всех матерей (mother) ([ссылка](https://sql-academy.org/ru/trainer/tasks/22))*

<details>
<summary>Решение</summary>

``` sql
SELECT member_name
FROM FamilyMembers
WHERE STATUS = 'mother';
```
</details>

*28. Сколько рейсов совершили авиакомпании из Ростова (Rostov) в Москву (Moscow) ? ([ссылка](https://sql-academy.org/ru/trainer/tasks/28))*

<details>
<summary>Решение</summary>

``` sql
SELECT COUNT(*) AS COUNT
FROM trip
WHERE town_from = 'Rostov'
	AND town_to = 'Moscow';
```
</details>

*34. Сколько всего 10-ых классов ([ссылка](https://sql-academy.org/ru/trainer/tasks/34))*

<details>
<summary>Решение</summary>

``` sql
SELECT COUNT(name) AS 'count'
FROM class
WHERE name LIKE '10%';
```
</details>

*36. Выведите информацию об обучающихся живущих на улице Пушкина (ul. Pushkina)? ([ссылка](https://sql-academy.org/ru/trainer/tasks/36))*

<details>
<summary>Решение</summary>

``` sql
SELECT *
FROM Student
WHERE address LIKE '%ul. Pushkina%';
```
</details>

*38. Сколько Анн (Anna) учится в школе ? ([ссылка](https://sql-academy.org/ru/trainer/tasks/38))*

<details>
<summary>Решение</summary>

``` sql
SELECT COUNT(*) AS COUNT
FROM Student
WHERE first_name = 'Anna';
```
</details>

*39. Сколько обучающихся в 10 B классе ? ([ссылка](https://sql-academy.org/ru/trainer/tasks/39))*

<details>
<summary>Решение</summary>

``` sql
SELECT COUNT(student) AS COUNT
FROM Student_in_class
	JOIN Class ON Student_in_class.class = Class.id
WHERE Class.name = '10 B';
```
</details>

*41. Выясните, во сколько по расписанию начинается четвёртое занятие. ([ссылка](https://sql-academy.org/ru/trainer/tasks/41))*

<details>
<summary>Решение</summary>

``` sql
SELECT DISTINCT start_pair
FROM Timepair
	JOIN Schedule ON Timepair.id = Schedule.number_pair
WHERE number_pair = '4';
```
</details>

*53. Измените имя "Andie Quincey" на новое "Andie Anthony". ([ссылка](https://sql-academy.org/ru/trainer/tasks/53))*

<details>
<summary>Решение</summary>

``` sql
UPDATE FamilyMembers
SET member_name = 'Andie Anthony'
WHERE member_name = 'Andie Quincey';
```
</details>

*56. Удалить все перелеты, совершенные из Москвы (Moscow). ([ссылка](https://sql-academy.org/ru/trainer/tasks/56))*

<details>
<summary>Решение</summary>

``` sql
DELETE FROM trip
WHERE town_from = 'Moscow';
```
</details>

*74. Выведите идентификатор и признак наличия интернета в помещении. Если интернет в сдаваемом жилье присутствует, то выведите «YES», иначе «NO». ([ссылка](https://sql-academy.org/ru/trainer/tasks/74))*

<details>
<summary>Решение</summary>

``` sql
SELECT id,
	IF(has_internet = 1, 'YES', 'NO') AS has_internet
FROM Rooms
```
</details>


*75. Выведите фамилию, имя и дату рождения студентов, кто был рожден в мае. ([ссылка](https://sql-academy.org/ru/trainer/tasks/75))*

<details>
<summary>Решение</summary>

``` sql
SELECT last_name,
	first_name,
	birthday
FROM Student
WHERE MONTH(birthday) = 5
```
</details>

*99. Посчитай доход с женской аудитории (доход = сумма(price * items)). Обратите внимание, что в таблице женская аудитория имеет поле user_gender «female» или «f». ([ссылка](https://sql-academy.org/ru/trainer/tasks/99))*

<details>
<summary>Решение</summary>

``` sql
SELECT SUM(amount) AS income_from_female
FROM (
		SELECT SUM(price * items) AS amount
		FROM Purchases
		WHERE user_gender LIKE '%f%'
		GROUP BY user_gender
	) AS time_table #LIMIT 1
```
</details>

*103. Вывести список имён сотрудников, получающих большую заработную плату, чем у непосредственного руководителя. ([ссылка](https://sql-academy.org/ru/trainer/tasks/103))*

<details>
<summary>Решение</summary>

``` sql
SELECT name
FROM Employee AS e
	INNER JOIN (
		SELECT id,
			salary
		FROM Employee
	) AS b ON e.chief_id = b.id
WHERE e.salary > b.salary
```
</details>

*109. Выведите название страны, где находится город «Salzburg» ([ссылка](https://sql-academy.org/ru/trainer/tasks/109))*

<details>
<summary>Решение</summary>

``` sql
SELECT co.name AS country_name
FROM regions r
	JOIN cities c ON r.id = c.regionid
	JOIN countries co ON r.countryid = co.id
WHERE c.name = 'Salzburg'
```
</details>

*114. Напишите запрос, который выведет имена пилотов, которые в качестве второго пилота (second_pilot_id) в августе 2023 года летали в New York ([ссылка](https://sql-academy.org/ru/trainer/tasks/114))*

<details>
<summary>Решение</summary>

``` sql
SELECT name
FROM Pilots
	INNER JOIN Flights ON pilot_id = second_pilot_id
WHERE destination = 'New York'
	AND YEAR(flight_date) = 2023
	AND MONTH(flight_date) = 08
```
</details>
