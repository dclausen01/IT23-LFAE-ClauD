### Aufgabe 2: API-Design - Musterlösung

#### 1. Format-Wahl: JSON
**Begründung:**
- ✅ **Performance**: Bibliotheksverwaltung erfordert häufige CRUD-Operationen → JSON ist schneller zu parsen
- ✅ **Web-Integration**: Moderne Bibliothekssysteme nutzen Web-Frontend → JSON ist Standard für REST-APIs
- ✅ **Einfachheit**: Buchmetadaten sind relativ einfach strukturiert → JSON reicht aus
- ✅ **Mobile Apps**: Bibliotheks-Apps profitieren von geringerer Dateigröße
- ❌ XML wäre nur bei komplexen Dokumentstrukturen (z.B. digitale Volltexte) oder Legacy-Systemen nötig

#### 2. REST-Endpoints Design

**Base URL:** `https://api.bibliothek.de/v1`

| HTTP Verb | Endpoint | Beschreibung |
|-----------|----------|--------------|
| GET | `/books` | Alle Bücher auflisten (mit Pagination) |
| GET | `/books/{id}` | Einzelnes Buch abrufen |
| POST | `/books` | Neues Buch anlegen |
| PUT | `/books/{id}` | Buch vollständig aktualisieren |
| PATCH | `/books/{id}` | Buch teilweise aktualisieren |
| DELETE | `/books/{id}` | Buch löschen |
| GET | `/books?search={query}` | Bücher suchen |
| GET | `/books/{id}/loans` | Ausleihhistorie eines Buchs |
| POST | `/loans` | Buch ausleihen |
| PUT | `/loans/{id}/return` | Buch zurückgeben |

#### 3. Request/Response-Beispiele

**GET /books?limit=10&offset=0**
```json
// Response (200 OK)
{
  "status": "success",
  "data": {
    "books": [
      {
        "id": "978-3-16-148410-0",
        "title": "Clean Code",
        "author": "Robert C. Martin",
        "isbn": "978-3-16-148410-0",
        "publishYear": 2008,
        "category": "IT",
        "available": true,
        "location": "Regal A-12",
        "addedDate": "2024-01-15T10:30:00Z"
      }
    ],
    "pagination": {
      "total": 1250,
      "limit": 10,
      "offset": 0,
      "hasNext": true
    }
  }
}
```

**POST /books**
```json
// Request
{
  "title": "JavaScript: The Definitive Guide",
  "author": "David Flanagan",
  "isbn": "978-1-491-95202-3",
  "publishYear": 2020,
  "category": "IT",
  "location": "Regal B-05"
}

// Response (201 Created)
{
  "status": "success",
  "message": "Book created successfully",
  "data": {
    "id": "978-1-491-95202-3",
    "title": "JavaScript: The Definitive Guide",
    "author": "David Flanagan",
    "isbn": "978-1-491-95202-3",
    "publishYear": 2020,
    "category": "IT",
    "available": true,
    "location": "Regal B-05",
    "addedDate": "2024-01-15T14:22:00Z"
  }
}
```

**PUT /books/978-3-16-148410-0**
```json
// Request
{
  "title": "Clean Code: A Handbook of Agile Software Craftsmanship",
  "author": "Robert C. Martin",
  "isbn": "978-3-16-148410-0",
  "publishYear": 2008,
  "category": "Software Engineering",
  "location": "Regal A-12"
}

// Response (200 OK)
{
  "status": "success",
  "message": "Book updated successfully",
  "data": {
    "id": "978-3-16-148410-0",
    "title": "Clean Code: A Handbook of Agile Software Craftsmanship",
    "author": "Robert C. Martin",
    "isbn": "978-3-16-148410-0",
    "publishYear": 2008,
    "category": "Software Engineering",
    "available": true,
    "location": "Regal A-12",
    "addedDate": "2024-01-15T10:30:00Z",
    "lastModified": "2024-01-15T15:45:00Z"
  }
}
```

**POST /loans**
```json
// Request
{
  "bookId": "978-3-16-148410-0",
  "userId": "user123",
  "loanPeriodDays": 14
}

// Response (201 Created)
{
  "status": "success",
  "message": "Book loaned successfully",
  "data": {
    "loanId": "loan_456789",
    "bookId": "978-3-16-148410-0",
    "userId": "user123",
    "loanDate": "2024-01-15T16:00:00Z",
    "dueDate": "2024-01-29T16:00:00Z",
    "status": "active"
  }
}
```

**Error Responses**
```json
// 404 Not Found
{
  "status": "error",
  "error": {
    "code": "BOOK_NOT_FOUND",
    "message": "Book with ID 978-3-16-148410-1 not found"
  }
}

// 400 Bad Request
{
  "status": "error",
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid request data",
    "details": [
      {
        "field": "isbn",
        "message": "ISBN format is invalid"
      },
      {
        "field": "publishYear",
        "message": "Year must be between 1000 and 2024"
      }
    ]
  }
}
```

**GET /books?search=clean+code**
```json
// Response (200 OK)
{
  "status": "success",
  "data": {
    "books": [
      {
        "id": "978-3-16-148410-0",
        "title": "Clean Code: A Handbook of Agile Software Craftsmanship",
        "author": "Robert C. Martin",
        "relevanceScore": 0.95,
        "matchedFields": ["title", "category"]
      }
    ],
    "searchQuery": "clean code",
    "totalResults": 1
  }
}
```

#### 4. HTTP-Status-Codes
- **200 OK**: Erfolgreiches GET, PUT, PATCH
- **201 Created**: Erfolgreiches POST
- **204 No Content**: Erfolgreiches DELETE
- **400 Bad Request**: Ungültige Anfrage
- **404 Not Found**: Resource nicht gefunden
- **409 Conflict**: Buch bereits ausgeliehen
- **422 Unprocessable Entity**: Validierungsfehler
- **500 Internal Server Error**: Serverfehler