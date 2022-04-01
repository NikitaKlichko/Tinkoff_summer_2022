# Tinkoff_summer_2022

## Math 

1) 16  
2) 4090505  
3) 370000/9801  
4) 11201  
5) 13  
6) 3/4  
7) 1/6  

## Programming  

[Здесь](https://github.com/NikitaKlichko/Tinkoff_summer_2022/blob/main/Tinkoff_summer.ipynb)  

## SQL  

```
1)  SELECT Пилоты.*
	FROM 
	(SELECT second_pilot_id
	FROM Рейсы
	WHERE destination = 'Шереметьево' AND
	flight_dt BETWEEN cast('2022-08-01' as date) AND cast('2022-08-31' as date) 
	GROUP BY second_pilot_id
	HAVING COUNT(flight_dt) = 3) r
	JOIN Пилоты ON r.second_pilot_id = Пилоты.pilot_id;
	
2)	SELECT Пилоты.*
	FROM 
	(SELECT first_pilot_id
	FROM Рейсы
	JOIN Самолеты
	ON Рейсы.plane_id = Самолеты.plane_id
	WHERE Самолеты.cargo_flg = 0
	GROUP BY first_pilot_id
	HAVING COUNT(Рейсы.quantity) > 30) r_s
	JOIN Пилоты ON r_s.first_pilot_id = Пилоты.pilot_id
	WHERE Пилоты.age > 45
	
	UNION
	
	SELECT Пилоты.*
	FROM 
	(SELECT second_pilot_id
	FROM Рейсы
	JOIN Самолеты
	ON Рейсы.plane_id = Самолеты.plane_id
	WHERE Самолеты.cargo_flg = 0
	GROUP BY second_pilot_id
	HAVING COUNT(Рейсы.quantity) > 30) r_s
	JOIN Пилоты ON r_s.second_pilot_id = Пилоты.pilot_id
	WHERE Пилоты.age > 45;	
	
3)	SELECT Пилоты.*
	FROM 
	(SELECT first_pilot_id, COUNT(Рейсы.flight_dt) AS Количество
	FROM Рейсы
	JOIN Самолеты ON Рейсы.plane_id = Самолеты.plane_id
	WHERE Самолеты.cargo_flg = 1
	GROUP BY first_pilot_id) tab
	JOIN Пилоты ON  tab.first_pilot_id = Пилоты.pilot_id
	ORDER BY Количество DESC
	LIMIT 10;
``` 
