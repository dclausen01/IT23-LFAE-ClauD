## 9. Übungsaufgaben

### Aufgabe 1: Format-Analyse
Gegeben ist folgende Datenstruktur. Implementieren Sie diese sowohl in JSON als auch in XML beispielhaft:
- Eine Bestellung mit ID und Datum
- Ein Kunde mit Name und E-Mail
- Mehrere Artikel mit Name, Menge und Einzelpreis (wählen Sie selbst 3 konkrete Artikel aus)
- Gesamtsumme der Bestellung

JSON:


``` JSON
"Aufgabe_1": 
{
	"Bestellung": 
	{
		"ID": 01,
		"Datum": "25.09.2025",
		"Kunde": 
		{
			"Name": "Walter von der Vogelweide",
			"Email": "Walter.vogel@freemail.com"
		},
		"Artikel": 
		[
			{
				"Name": "Promega3000XD",
				"Menge": 200, 
				"Einzelpreis": 150
			},
			{
				"Name": "Laptop",
				"Menge": 200,
				"Einzelpreis": 150
			},
			{
				"Name": "Taplog", 
				"Menge": 200, 
				"Einzelpreis": 150
			}
		],
		"Gesamtsumme": 130000
	},
}
```



### Aufgabe 2: API-Design
Entwerfen Sie eine REST-API für eine Bibliotheksverwaltung:
1. Welches Format (JSON, XML) würden Sie wählen und warum?
	1. JSON, wegen: 
		1. Datentransfergeschwindigkeit
		2. Kompatibilität
2. Definieren Sie Endpoints für CRUD-Operationen
	1. swagger.io/agloerkslib/
		1. addnewbook (POST)
		2. getbookbyname/*name* (GET)
		3. Request: swagger.io/aglorkslib/getbookbyname/farbe-der-magie
			2. Response: CORS-Error
		4. getbookbyid/*id*
			1. Request: swagger.io/aglorkslib/getbookbyid/1086745
			2. Response: CORS-Error
		5. listbooksbyauthor/*author*
			1. Request: swagger.io/aglorkslib/listbooksbyauthor/pratchet
			2. Response: CORS-Error
		6. listbooksbygenre/*genre*
			1. Request: swagger.io/aglorkslib/listbooksbygenre/fantasy
			2. Response: CORS-Error
		8. updatebookbyid/*id*
			1. Request: swagger.io/aglorkslib/listbooksbyid/01805
			2. Response: CORS-Error
		10. deletebookbyid/*id*
			1. Request: swagger.io/aglorkslib/listbooksbyid/01805
			2. Response: CORS-Error
3. Erstellen Sie Beispiel-Request/Response-Paare



### Aufgabe 3: Konvertierung
Schreiben Sie eine Funktion (Pseudocode), die:
- JSON in XML konvertiert
- Dabei Arrays korrekt behandelt
- Datentypen erhält (über Attribute)

```
function convertJsonToXml(jsonObject):
	for(element in jsonObject):
		result = ""
		if (type(element) == Object):
			xmlTag = element.key
			xmlValue = convertJsonToXml(element)
			result = <xmlTag>xmlValue</xmlTag>
		else:
			xmlTag = element.Key
			xmlValue = element.vlaue
			result = <xmlTag>xmlValue</xmlTag>
		return(result)
```