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

*31. Вывести всех членов семьи с фамилией Quincey. ([ссылка](https://sql-academy.org/ru/trainer/tasks/31))*

<details>
<summary>Решение</summary>

``` sql
SELECT *
FROM FamilyMembers
WHERE member_name LIKE '%Quincey%';
```
</details>

*32. Вывести средний возраст людей (в годах), хранящихся в базе данных. Результат округлите до целого в меньшую сторону. ([ссылка](https://sql-academy.org/ru/trainer/tasks/32))*

<details>
<summary>Решение</summary>

``` sql
SELECT FLOOR(AVG(TIMESTAMPDIFF(YEAR, birthday, CURDATE()))) AS age
FROM FamilyMembers
```
</details>

*33. Найдите среднюю цену икры на основе данных, хранящихся в таблице Payments. В базе данных хранятся данные о покупках красной (red caviar) и черной икры (black caviar). ([ссылка](https://sql-academy.org/ru/trainer/tasks/33))*

<details>
<summary>Решение</summary>

``` sql
SELECT AVG(ab) AS cost
FROM (
		SELECT unit_price AS ab
		FROM Goods
			INNER JOIN Payments ON good_id = good
		WHERE good_name IN ('red caviar', 'black caviar')
	) AS a
```
</details>

*35. Сколько различных кабинетов школы использовались 2 сентября 2019 года для проведения занятий? ([ссылка](https://sql-academy.org/ru/trainer/tasks/35))*

<details>
<summary>Решение</summary>

``` sql
SELECT COUNT(DISTINCT classroom) AS COUNT
FROM Schedule
WHERE YEAR(date) = 2019
	AND MONTH(date) = 09
	AND DAY(date) = 02
```
</details>

*37. Сколько лет самому молодому обучающемуся ? ([ссылка](https://sql-academy.org/ru/trainer/tasks/37))*

<details>
<summary>Решение</summary>

``` sql
SELECT MIN(TIMESTAMPDIFF(YEAR, birthday, CURDATE())) AS year
FROM Student
```
</details>

*40. Выведите название предметов, которые преподает Ромашкин П.П. (Romashkin P.P.). ([ссылка](https://sql-academy.org/ru/trainer/tasks/40))*

<details>
<summary>Решение</summary>

``` sql
SELECT name AS 'subjects'
FROM subject
	JOIN Schedule ON Subject.id = Schedule.subject
	JOIN Teacher ON Schedule.teacher = Teacher.id
WHERE Teacher.last_name = 'Romashkin'
	AND Teacher.first_name LIKE 'P%'
	AND Teacher.middle_name LIKE 'P%';
```
</details>

*42. Сколько времени обучающийся будет находиться в школе, учась со 2-го по 4-ый уч. предмет? ([ссылка](https://sql-academy.org/ru/trainer/tasks/42))*

<details>
<summary>Решение</summary>

``` sql
SELECT TIMEDIFF(
		(
			SELECT end_pair
			FROM Timepair
			WHERE id = 4
		),
		(
			SELECT start_pair
			FROM Timepair
			WHERE id = 2
		)
	) AS time
FROM Timepair
LIMIT 1
```
</details>

*43. Выведите фамилии преподавателей, которые ведут физическую культуру (Physical Culture). Отсортируйте преподавателей по фамилии в алфавитном порядке. ([ссылка](https://sql-academy.org/ru/trainer/tasks/43))*

<details>
<summary>Решение</summary>

``` sql
SELECT t.last_name #, su.name
FROM Teacher t
	INNER JOIN Schedule s ON t.id = s.teacher
	INNER JOIN Subject su ON su.id = s.subject
WHERE su.name = 'Physical Culture'
ORDER BY t.last_name
```
</details>

*46. В каких классах введет занятия преподаватель "Krauze" ? ([ссылка](https://sql-academy.org/ru/trainer/tasks/46))*

<details>
<summary>Решение</summary>

``` sql
SELECT DISTINCT name
FROM Class
	JOIN Schedule ON Class.id = Schedule.class
	JOIN Teacher ON Schedule.teacher = Teacher.id
WHERE Teacher.last_name = 'Krauze';
```
</details>

*47. Сколько занятий провел Krauze 30 августа 2019 г.? ([ссылка](https://sql-academy.org/ru/trainer/tasks/47))*

<details>
<summary>Решение</summary>

``` sql
SELECT COUNT(*) AS COUNT
FROM Teacher t
	JOIN Schedule s ON t.id = s.teacher
WHERE last_name = 'Krauze'
	AND s.date BETWEEN '2019-08-30' AND '2019-08-31'
```
</details>

*48. Выведите заполненность классов в порядке убывания ([ссылка](https://sql-academy.org/ru/trainer/tasks/48))*

<details>
<summary>Решение</summary>

``` sql
SELECT name,
	COUNT(sis.id) AS COUNT
FROM Class c
	JOIN Student_in_class sis ON c.id = sis.class
GROUP BY name
ORDER BY 2 DESC
```
</details>

*49. Какой процент обучающихся учится в "10 A" классе? Выведите ответ в диапазоне от 0 до 100 с округлением до четырёх знаков после запятой, например, 96.0201. ([ссылка](https://sql-academy.org/ru/trainer/tasks/49))*

<details>
<summary>Решение</summary>

``` sql
WITH count_student AS (
	SELECT name,
		COUNT(sis.id) AS coun
	FROM Class c
		JOIN Student_in_class sis ON c.id = sis.class
	GROUP BY name
),
all_student AS (
	SELECT sum(coun) AS sc
	FROM count_student
)
SELECT round(coun /(sc * 1.0) * 100, 4) AS percent
FROM all_student,
	count_student
WHERE name = '10 A'
```
</details>

*50. Какой процент обучающихся родился в 2000 году? Результат округлить до целого в меньшую сторону. ([ссылка](https://sql-academy.org/ru/trainer/tasks/50))*

<details>
<summary>Решение</summary>

``` sql
SELECT floor(
		COUNT(
			CASE
				WHEN year(birthday) = '2000' THEN 1
			END
		) / COUNT(id) * 100
	) AS percent
FROM student
```
</details>

*51. Добавьте товар с именем "Cheese" и типом "food" в список товаров (Goods). ([ссылка](https://sql-academy.org/ru/trainer/tasks/51))*

<details>
<summary>Решение</summary>

``` sql
INSERT INTO Goods(good_id, good_name, TYPE)
SELECT MAX(good_id) + 1,
	'Cheese',
	(
		SELECT good_type_id
		FROM GoodTypes
		WHERE good_type_name = 'food'
	)
FROM Goods
```
</details>

*52. Добавьте в список типов товаров (GoodTypes) новый тип "auto". ([ссылка](https://sql-academy.org/ru/trainer/tasks/52))*

<details>
<summary>Решение</summary>

``` sql
INSERT INTO GoodTypes (good_type_id, good_type_name)
SELECT COUNT(*) + 1,
	'auto'
FROM GoodTypes
```
</details>

*54. Удалить всех членов семьи с фамилией "Quincey". ([ссылка](https://sql-academy.org/ru/trainer/tasks/54))*

<details>
<summary>Решение</summary>

``` sql
DELETE FROM FamilyMembers
WHERE member_name LIKE '%Quincey%';
```
</details>

*57. Перенести расписание всех занятий на 30 мин. вперед. ([ссылка](https://sql-academy.org/ru/trainer/tasks/57))*

<details>
<summary>Решение</summary>

``` sql
UPDATE Timepair
SET start_pair = addtime(start_pair, '00:30:00'),
	end_pair = addtime(end_pair, '00:30:00')
```
</details>

*59. Вывести пользователей,указавших Белорусский номер телефона ? Телефонный код Белоруссии +375. ([ссылка](https://sql-academy.org/ru/trainer/tasks/59))*

<details>
<summary>Решение</summary>

``` sql
SELECT *
FROM Users
WHERE phone_number LIKE '+375%';
```
</details>

*61. Выведите список комнат, которые были зарезервированы хотя бы на одни сутки в 12-ую неделю 2020 года. ([ссылка](https://sql-academy.org/ru/trainer/tasks/61))*

<details>
<summary>Решение</summary>

``` sql
SET @start_date = '2020-01-01';
SET @week = 12;
WITH min_one_day AS (
	SELECT room_id
	FROM Reservations
	WHERE start_date BETWEEN DATE_ADD(@start_date, INTERVAL @week * 7 - 6 DAY)
		AND DATE_ADD(@start_date, INTERVAL @week * 7 DAY)
)
SELECT *
FROM Rooms
WHERE id IN (
		SELECT *
		FROM min_one_day
	)
```
</details>

*62. Вывести в порядке убывания популярности доменные имена 2-го уровня, используемые пользователями для электронной почты. Полученный результат необходимо дополнительно отсортировать по возрастанию названий доменных имён. ([ссылка](https://sql-academy.org/ru/trainer/tasks/62))*

<details>
<summary>Решение</summary>

``` sql
SELECT SUBSTRING_INDEX(email, '@', -1) AS domain,
	COUNT(SUBSTRING_INDEX(email, '@', -1)) AS COUNT
FROM Users
GROUP BY 1
ORDER BY COUNT DESC,
	domain
```
</details>

*63. Выведите отсортированный список (по возрастанию) фамилий и имен студентов в виде Фамилия.И. ([ссылка](https://sql-academy.org/ru/trainer/tasks/63))*

<details>
<summary>Решение</summary>

``` sql
SELECT CONCAT(last_name, '.', left(first_name, 1), '.') AS name
FROM student
WHERE last_name IS NOT NULL
ORDER BY 1
```
</details>

*64. Вывести количество бронирований по каждому месяцу каждого года, в которых было хотя бы 1 бронирование. Результат отсортируйте в порядке возрастания даты бронирования. ([ссылка](https://sql-academy.org/ru/trainer/tasks/64))*

<details>
<summary>Решение</summary>

``` sql
SELECT year(start_date) AS year,
	MONTH(start_date) AS MONTH,
	COUNT(*) AS amount
FROM Reservations
GROUP BY year,
	MONTH
ORDER BY year,
	MONTH
```
</details>

*65. Необходимо вывести рейтинг для комнат, которые хоть раз арендовали, как среднее значение рейтинга отзывов округленное до целого вниз. ([ссылка](https://sql-academy.org/ru/trainer/tasks/65))*

<details>
<summary>Решение</summary>

``` sql
SELECT room_id,
	floor(AVG(rating)) AS rating
FROM Reservations
	JOIN Reviews ON Reservations.id = Reviews.reservation_id
GROUP BY room_id
```
</details>

*66. Вывести список комнат со всеми удобствами (наличие ТВ, интернета, кухни и кондиционера), а также общее количество дней и сумму за все дни аренды каждой из таких комнат. ([ссылка](https://sql-academy.org/ru/trainer/tasks/66))*

<details>
<summary>Решение</summary>

``` sql
SELECT home_type,
	ro.address,
	sum(
		CASE
			WHEN re.price IS NOT NULL THEN total / re.price
			ELSE 0
		END
	) AS days,
	sum(
		CASE
			WHEN total IS NOT NULL THEN total
			ELSE 0
		END
	) AS total_fee
FROM Rooms ro
	LEFT JOIN Reservations re ON ro.id = re.room_id
WHERE has_tv = 1
	AND has_internet = 1
	AND has_kitchen = 1
	AND has_air_con = 1
GROUP BY home_type,
	ro.address
```
</details>

*67. Вывести время отлета и время прилета для каждого перелета в формате "ЧЧ:ММ, ДД.ММ - ЧЧ:ММ, ДД.ММ", где часы и минуты с ведущим нулем, а день и месяц без. ([ссылка](https://sql-academy.org/ru/trainer/tasks/67))*

<details>
<summary>Решение</summary>

``` sql
SELECT CONCAT(
		DATE_FORMAT(time_out, '%H:%i'),
		', ',
		DAY(time_out),
		'.',
		MONTH(time_out),
		' - ',
		DATE_FORMAT(time_in, '%H:%i'),
		', ',
		DAY(time_in),
		'.',
		MONTH(time_in)
	) AS flight_time
FROM trip
```
</details>

*70. Необходимо категоризовать жилье на economy, comfort, premium по цене соответственно <= 100, 100 < цена < 200, >= 200. В качестве результата вывести таблицу с названием категории и количеством жилья, попадающего в данную категорию ([ссылка](https://sql-academy.org/ru/trainer/tasks/70))*

<details>
<summary>Решение</summary>

``` sql
SELECT CASE
		WHEN price <= 100 THEN 'economy'
		WHEN price >= 200 THEN 'premium'
		ELSE 'comfort'
	END AS category,
	COUNT(*) AS COUNT
FROM Rooms
GROUP BY 1
```
</details>

*72. Выведите среднюю цену бронирования за сутки для каждой из комнат, которую бронировали хотя бы один раз. Среднюю цену необходимо округлить до целого значения вверх. ([ссылка](https://sql-academy.org/ru/trainer/tasks/72))*

<details>
<summary>Решение</summary>

``` sql
SELECT room_id,
	ceil(avg(price)) AS avg_price
FROM reservations
GROUP BY room_id
```
</details>

*73. Выведите id тех комнат, которые арендовали нечетное количество раз ([ссылка](https://sql-academy.org/ru/trainer/tasks/73))*

<details>
<summary>Решение</summary>

``` sql
SELECT room_id,
	COUNT(*) AS COUNT
FROM Reservations
GROUP BY room_id
HAVING COUNT(*) %2 = 1
```
</details>

*76. Вывести имена всех пользователей сервиса бронирования жилья, а также два признака: является ли пользователь собственником какого-либо жилья (is_owner) и является ли пользователь арендатором (is_tenant). В случае наличия у пользователя признака необходимо вывести в соответствующее поле 1, иначе 0. ([ссылка](https://sql-academy.org/ru/trainer/tasks/76))*

<details>
<summary>Решение</summary>

``` sql
SELECT name,
	CASE
		WHEN id IN (
			SELECT owner_id
			FROM Rooms
		) THEN 1
		ELSE 0
	END AS is_owner,
	CASE
		WHEN id IN (
			SELECT user_id
			FROM Reservations
		) THEN 1
		ELSE 0
	END AS is_tenant
FROM Users
```
</details>

*77. Создайте представление с именем "People", которое будет содержать список имен (first_name) и фамилий (last_name) всех студентов (Student) и преподавателей(Teacher) ([ссылка](https://sql-academy.org/ru/trainer/tasks/77))*

<details>
<summary>Решение</summary>

``` sql
CREATE VIEW People AS
SELECT first_name,
	last_name
FROM Student
UNION
SELECT first_name,
	last_name
FROM Teacher;
```
</details>
