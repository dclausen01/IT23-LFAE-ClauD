08
``` SQL
SELECT a.name, a.position, d.name FROM employees as a
LEFT JOIN departments AS d ON a.department_id = d.department_id

SELECT a.name, p.name FROM employees as a 
LEFT JOIN projects as p ON a.department_id = p.department_id

SELECT a.name, a.position, a.salery, AVG(a.salery) FROM employees as a
LEFT JOIN departments as d ON a.department_id = d.department_id
WHERE a.salery > AVG(a.salery)

SELECT p.name, a.name FROM projects as p
RIGHT JOIN employees as a ON p.department_od = a.department_id

SELECT d.name, a.name FROM departments as d
Left Join employees as a ON p.department_od = a.department_id
Full Join projects as p ON p.department_id = d.department_id
Where a.department_id != p.department_id
GROUP BY d.name

SELECT d.name, SUM(a.salery) as Gesamtgehalt FROM departments as d
Left Join employees as a ON p.department_od = a.department_id

SELECT p.name, SUM(a.name) as Anzahl FROM projects as p
RIGHT JOIN employees as a ON p.department_od = a.department_id
WHERE Anzahl >= 2
```

08a
``` SQL
UPDATE RP 
SET RP.RgPos_RabattProzent = 12 
FROM RechnungPosition RP 
JOIN Rechnung R ON RP.RgPos_RgIdKey = R.Rg_IdKey 
JOIN Artikel A ON RP.RgPos_ArtIdKey = A.Art_IdKey 
WHERE R.Rg_Datum like '2023%' AND A.Art_WaIdKey = 2 AND RP.RgPos_RabattProzent = 0
```

