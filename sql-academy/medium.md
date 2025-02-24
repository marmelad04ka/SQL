# Решения бесплатных задач среднего уровня с сайта sql-academy 

*8. В какие города можно улететь из Парижа (Paris) и сколько времени это займёт? ([ссылка](https://sql-academy.org/ru/trainer/tasks/8))*

<details>
<summary>Решение</summary>

``` sql
SELECT town_to,
	TIMEDIFF(time_in, time_out) AS flight_time
FROM trip
WHERE town_from = 'Paris';
```
</details>

*10. Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г. ([ссылка](https://sql-academy.org/ru/trainer/tasks/10))*

<details>
<summary>Решение</summary>

``` sql
SELECT *
FROM trip
WHERE time_out BETWEEN '1900-01-01 10:00:00' AND '1900-01-01 14:00:00'
```
</details>

*11. Выведите пассажиров с самым длинным ФИО. Пробелы, дефисы и точки считаются частью имени. ([ссылка](https://sql-academy.org/ru/trainer/tasks/11))*

<details>
<summary>Решение</summary>

``` sql
SELECT name
FROM passenger
WHERE LENGTH(name) = (
		SELECT max(LENGTH(name))
		FROM passenger
	);
```
</details>

*13. Вывести имена людей, у которых есть полный тёзка среди пассажиров ([ссылка](https://sql-academy.org/ru/trainer/tasks/13))*

<details>
<summary>Решение</summary>

``` sql
SELECT name
FROM Passenger
GROUP BY name
HAVING COUNT(name) > 1;
```
</details>

*16. Вывести отсортированный по количеству перелетов (по убыванию) и имени (по возрастанию) список пассажиров, совершивших хотя бы 1 полет. ([ссылка](https://sql-academy.org/ru/trainer/tasks/16))*

<details>
<summary>Решение</summary>

``` sql
SELECT name,
	COUNT(passenger) AS COUNT
FROM Passenger p
	LEFT JOIN Pass_in_trip pit ON pit.passenger = p.id
GROUP BY p.id
HAVING COUNT(passenger) >= 1
ORDER BY 2 DESC,
	1
```
</details>

*17. Определить, сколько потратил в 2005 году каждый из членов семьи. В результирующей выборке не выводите тех членов семьи, которые ничего не потратили. ([ссылка](https://sql-academy.org/ru/trainer/tasks/17))*

<details>
<summary>Решение</summary>

``` sql
SELECT member_name,
	STATUS,
	sum(amount * unit_price) AS 'costs'
FROM FamilyMembers
	JOIN Payments ON FamilyMembers.member_id = Payments.family_member
WHERE YEAR(date) = 2005
GROUP BY member_name,
	STATUS;
```
</details>

*18. Выведите имя самого старшего человека. Если таких несколько, то выведите их всех. ([ссылка](https://sql-academy.org/ru/trainer/tasks/18))*

<details>
<summary>Решение</summary>

``` sql
SELECT member_name
FROM FamilyMembers
WHERE birthday = (
		SELECT min(birthday)
		FROM FamilyMembers
	);
```
</details>

*20. Сколько и кто из семьи потратил на развлечения (entertainment). Вывести статус в семье, имя, сумму ([ссылка](https://sql-academy.org/ru/trainer/tasks/20))*

<details>
<summary>Решение</summary>

``` sql
SELECT STATUS,
	member_name,
	sum(amount * unit_price) AS costs
FROM FamilyMembers
	JOIN Payments ON FamilyMembers.member_id = Payments.family_member
	JOIN Goods ON Payments.good = Goods.good_id
	JOIN GoodTypes ON Goods.type = GoodTypes.good_type_id
WHERE good_type_name = 'entertainment'
GROUP BY STATUS,
	member_name;
```
</details>

*21. Определить товары, которые покупали более 1 раза ([ссылка](https://sql-academy.org/ru/trainer/tasks/21))*

<details>
<summary>Решение</summary>

``` sql
SELECT good_name
FROM Goods
	JOIN Payments ON Goods.good_id = Payments.good
GROUP BY good
HAVING COUNT(good) > 1;
```
</details>

*23. Найдите самый дорогой деликатес (delicacies) и выведите его цену ([ссылка](https://sql-academy.org/ru/trainer/tasks/23))*

<details>
<summary>Решение</summary>

``` sql
SELECT good_name,
	unit_price
FROM GoodTypes
	INNER JOIN Goods ON good_type_id = TYPE
	INNER JOIN Payments ON good_id = good
WHERE good_type_name = 'delicacies'
ORDER BY unit_price DESC
LIMIT 1
```
</details>

*24. Определить кто и сколько потратил в июне 2005 ([ссылка](https://sql-academy.org/ru/trainer/tasks/24))*

<details>
<summary>Решение</summary>

``` sql
SELECT member_name,
	SUM(amount * unit_price) AS costs
FROM FamilyMembers
	INNER JOIN Payments ON member_id = family_member
WHERE YEAR(date) = 2005
	AND MONTH(date) = 06
GROUP BY member_name
```
</details>

*25. Определить, какие товары не покупались в 2005 году ([ссылка](https://sql-academy.org/ru/trainer/tasks/25))*

<details>
<summary>Решение</summary>

``` sql
SELECT good_name
FROM Goods
WHERE good_name NOT IN (
		SELECT DISTINCT good_name
		FROM Goods
			INNER JOIN Payments ON good_id = good
		WHERE YEAR(date) = 2005
	)
```
</details>

*26. Определить группы товаров, которые не приобретались в 2005 году ([ссылка](https://sql-academy.org/ru/trainer/tasks/26))*

<details>
<summary>Решение</summary>

``` sql
SELECT good_type_name
FROM GoodTypes
WHERE good_type_name NOT IN (
		SELECT DISTINCT gt.good_type_name
		FROM payments p
			JOIN goods g ON p.good = g.good_id
			JOIN GoodTypes gt ON g.type = gt.good_type_id
		WHERE year(p.date) = '2005'
	)
```
</details>

*27. Узнайте, сколько было потрачено на каждую из групп товаров в 2005 году. Выведите название группы и потраченную на неё сумму. Если потраченная сумма равна нулю, т.е. товары из этой группы не покупались в 2005 году, то не выводите её. ([ссылка](https://sql-academy.org/ru/trainer/tasks/27))*

<details>
<summary>Решение</summary>

``` sql
SELECT gt.good_type_name,
	sum(amount * unit_price) AS costs
FROM payments p
	JOIN goods g ON p.good = g.good_id
	JOIN GoodTypes gt ON g.type = gt.good_type_id
WHERE year(p.date) = '2005'
GROUP BY 1
```
</details>

*29. Выведите имена пассажиров улетевших в Москву (Moscow) на самолете TU-134. В ответе не должно быть дубликатов. ([ссылка](https://sql-academy.org/ru/trainer/tasks/29))*

<details>
<summary>Решение</summary>

``` sql
SELECT DISTINCT name
FROM Passenger
	JOIN Pass_in_trip ON Passenger.id = Pass_in_trip.passenger
	JOIN Trip ON Pass_in_trip.trip = Trip.id
WHERE town_to = 'Moscow'
	AND plane = 'TU-134';
```
</details>

*30. Выведите нагруженность (число пассажиров) каждого рейса (trip). Результат вывести в отсортированном виде по убыванию нагруженности. ([ссылка](https://sql-academy.org/ru/trainer/tasks/30))*

<details>
<summary>Решение</summary>

``` sql
SELECT trip,
	COUNT(passenger) AS COUNT
FROM Pass_in_trip
GROUP BY trip
ORDER BY COUNT DESC
```
</details>
