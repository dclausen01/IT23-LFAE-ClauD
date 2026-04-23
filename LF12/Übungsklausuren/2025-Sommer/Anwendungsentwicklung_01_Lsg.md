# Musterlösungen IHK-Abschlussprüfung Fachinformatiker Anwendungsentwicklung

## **1. Aufgabe: Projektmanagement (20 Punkte)**

### a) Umfeldanalyse (6 Punkte)

**Technisches Umfeld (3 Punkte):**
- **Legacy-Systeme und Inkompatibilität**: Die verschiedenen Kliniken verfügen über heterogene IT-Infrastrukturen mit unterschiedlichen Software-Versionen, Datenbanken und Schnittstellen. Eine Analyse muss die technischen Schnittstellen, Datenformate und Integrationsmöglichkeiten sowie die Migration bestehender Daten bestimmen.

**Rechtliches Umfeld (3 Punkte):**
- **DSGVO und Gesundheitsdatenschutz**: Die Verarbeitung gesundheitsbezogener Daten unterliegt besonderen rechtlichen Anforderungen (Art. 9 DSGVO, BDSG). Es müssen rechtliche Grundlagen für die Datenverarbeitung geschaffen werden, Patienteneinwilligungen eingeholt werden und technische/organisatorische Maßnahmen (TOM) umgesetzt werden.

### b) Stakeholder-Analyse (10 Punkte)

| Stakeholder | Erwartung | Befürchtung |
|-------------|-----------|-------------|
| **Klinikpersonal (Pflege/Ärzte)** | Erleichterung der Arbeitsabläufe durch digitale Prozesse; schnellerer Zugriff auf Patientendaten | Mehraufwand durch Doppelarbeit (Papier + digital); komplizierte Bedienung; Zeitmangel für Einarbeitung |
| **Patienten** | Bessere Behandlungsqualität durch schnellere Informationsverfügbarkeit; mehr Transparenz | Missbrauch ihrer sensiblen Daten; Datenschutzverletzungen; Verlust der persönlichen Arzt-Patienten-Beziehung |

### c) Vorbereitung Abschlussprotokoll (4 Punkte)

1. **Dokumentationssammlung und -aufbereitung**: Sammeln aller relevanten Projektdokumente (Projektplan, Meilensteinberichte, Änderungsanträge, Risikologs) und Zusammenfassen der wichtigsten Ergebnisse, Abweichungen und getroffenen Entscheidungen.

2. **Stakeholder-Feedback einholen**: Durchführung abschließender Interviews/Workshops mit Schlüsselstakeholdern (Vorstand, Projektteam, Anwender) zur Erhebung von Lessons Learned und Bestätigung der Projektergebnisse.

---

## **2. Aufgabe: Datenmodellierung & Sicherheit (27 Punkte)**

### a) ER-Modell (16 Punkte)

```
┌─────────────────────────────────┐
│           Patient               │
├─────────────────────────────────┤
│ PatientID (PK)                  │
│ Nachname                        │
│ Vorname                         │
│ Geburtsdatum                    │
│ Versichertennummer              │
│ KrankenkassenID (FK)            │
└─────────────────────────────────┘
         │ 1
         │
         │ n
┌────────▼──────────────────────┐  ┌──────────────────────┐
│        Medikament             │  │     Krankenkasse     │
├───────────────────────────────┤  ├──────────────────────┤
│ MedikamentID (PK)             │  │ KrankenkassenID (PK) │
│ Hersteller                    │  │ Name                 │
│ Wirkstoff                     │  │ Adresse              │
└───────────────────────────────┘  └──────────────────────┘
         │ n
         │
         │ n
┌────────▼──────────────────────┐
│    Medikation (Behandlung)    │
├───────────────────────────────┤
│ MedikationID (PK)             │
│ PatientID (FK)                │
│ MedikamentID (FK)             │
│ Dosis                         │
│ Einnahmezeitpunkt             │
│ ArztID (FK)                   │
└───────────────────────────────┘

┌─────────────────────────────────┐  ┌──────────────────────┐
│            Arzt                 │  │     Behandlung       │
├─────────────────────────────────┤  ├──────────────────────┤
│ ArztID (PK)                     │  │ BehandlungID (PK)    │
│ Nachname                        │  │ PatientID (FK)       │
│ Vorname                         │  │ ArztID (FK)          │
│ Spezialgebiet                   │  │ Zeitstempel          │
└─────────────────────────────────┘  │ Bericht              │
                                     └──────────────────────┘
         │ 1
         │
         │ n
┌────────▼──────────────────────┐
│       Diagnose                │
├───────────────────────────────┤
│ DiagnoseID (PK)               │
│ PatientID (FK)                │
│ BezeichnungErkrankung         │
│ Feststellungsdatum            │
└───────────────────────────────┘
```

**Hinweis**: Die Beziehungen sind: Patient 1:n Medikament (über Medikation/Behandlung), Patient 1:n Arzt (über Behandlung), Patient 1:n Diagnose.

### b) Mockup Benutzeroberfläche (8 Punkte)

```
┌─────────────────────────────────────────────────────────────┐
│                   Digitale Krankenakte                      │
│                    Patient erfassen                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Nachname:  [______________________________]  *            │
│  Vorname:   [______________________________]  *            │
│  Geburtsdatum: [___.___._____] (DD.MM.JJJJ)  *            │
│                                                             │
│  Krankenkasse:  [▼ Auswahl aus Dropdown      ]  *          │
│                 (AOK Nordost, TK, DAK-Gesundheit, ...)     │
│                                                             │
│  Versichertennummer:  [_____________________]  *           │
│                        (123456789)                         │
│                                                             │
│                [Abbrechen]  [Speichern]                    │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**Elemente:** Formularfelder mit klaren Labels, Pflichtfelder-Kennzeichnung (*), Dropdown für Krankenkassen (Datenkonsistenz), Eingabemasken für Datum, Validierung, klar positionierte Aktionsschaltflächen.

### c) Passwort-Speicherung (3 Punkte)

**Möglichkeit: Hash-Verfahren mit Salt (z. B. bcrypt, Argon2)**

**Beschreibung:** Das Passwort wird nicht im Klartext, sondern als Einweg-Hash gespeichert. Vor dem Hashing wird ein eindeutiger Salt (Zufallswert) dem Passwort angefügt. Dies verhindert Regenbogen-Tabellen-Angriffe und stellt sicher, dass identische Passwörter unterschiedliche Hash-Werte erzeugen. Bei Login wird der eingegebene Wert mit dem gespeicherten Salt kombiniert und gehasht – die Hash-Werte werden verglichen.

---

## **3. Aufgabe: Prozessanalyse & Optimierung (29 Punkte)**

### a) Aktivitätsdiagramm (17 Punkte)

```
[Start] → (Ärzte/Pflege versammeln sich) → [Laborergebnisse abfragen] → 
[Patientenreihenfolge planen] → [Patientenakte öffnen] → 
├─► (Vitalwerte prüfen & notieren) ──┐
│                                    │
└─► (Patient nach Symptomen befragen) → [Symptome notieren] → 
[Behandlungsplan anpassen] → [Behandlungsplan mit Patient besprechen] → 
[Neue Laborergebnisse vorhanden?] ──► (Ja) → [Laborergebnisse mit Patient besprechen] → 
[Ärztliche Untersuchung durchführen] → [Behandlungsstand handschriftlich notieren] → 
[Weiterer Patient?] ──► (Ja) → [Patientenakte öffnen] (Schleifenstart)
                     └──► (Nein) → [Änderungen in Software übertragen] → [Ende]
```

**Korrekturhinweise:** Parallele Verarbeitung (Vitalwerte + Befragung), Entscheidungen (Laborergebnisse?, Weiterer Patient?), korrekte Symbole (Start/Ende, Aktion, Entscheidung), sinnvolle Ablaufreihenfolge.

### b) Probleme und Digitalisierungslösungen (12 Punkte)

| Problem | Digitalisierungslösung |
|---------|------------------------|
| **Medienbruch (Papier → Software)** | Direkte Eingabe in digitale Patientenakte auf Tablets während der Visite eliminiert doppelte Datenerfassung, reduziert Fehler und spart Zeit. |
| **Fehlende Aktualität von Daten** | Echtzeit-Synchronisation mit Laborsystemen zeigt neue Ergebnisse sofort auf dem Tablet an; automatische Benachrichtigungen bei kritischen Werten. |
| **Manuelle Priorisierung fehleranfällig** | Algorithmus schlägt automatisch optimale Reihenfolge vor basierend auf: Dringlichkeit, Laborwerten, Terminen, Beatmungsstatus – reduziert Wartezeiten und verbessert Patientensicherheit. |

---

## **4. Aufgabe: Software-Entwurf (24 Punkte)**

### a) Factory Method Pattern (9 Punkte)

**aa) Zwei Aspekte (6 Punkte):**
1. **Kapselung der Objekterstellung:** Das Pattern kapselt die Instanziierung von Objekten in einer dedizierten Factory-Methode anstatt direkte Konstruktor-Aufrufe im Client-Code. Dies ermöglicht flexiblere Erweiterbarkeit.
2. **Polymorphe Objekterstellung:** Subklassen können die Factory-Methode überschreiben und so unterschiedliche konkrete Produkt-Objekte erzeugen, die alle das gemeinsame Interface implementieren. Dies fördert Lose Kopplung.

**ab) Einschränkung (3 Punkte):**
- **Gemeinsame Basisklasse/Interface erforderlich:** Alle Produkte, die von den Factory-Methoden erzeugt werden, müssen ein gemeinsames Interface oder eine gemeinsame Basisklasse haben, damit Client-Code unabhängig vom konkreten Produkttyp arbeiten kann. Der Rückgabetyp der Factory-Methode ist fest definiert.

### b) Abstrakte Klassen vs. Interfaces (6 Punkte)

1. **Implementierung/Konstellation vs. reine Vertragsdefinition:** Abstrakte Klassen können sowohl abstrakte Methoden (ohne Implementierung) als auch konkrete Methoden (mit Implementierung) enthalten und Attribute definieren. Interfaces definieren nur Verträge (Methodensignaturen) ohne Implementierung (bis Java 8) und keine Instanzattribute.

2. **Vererbung vs. Multi-Implementierung:** Eine Klasse kann nur von einer einzigen abstrakten Klasse erben (einfache Vererbung), aber mehrere Interfaces implementieren. Interfaces ermöglichen so flexiblere Typkompositionen.

### c) Klassenmodell-Ergänzung (6 Punkte)

```
┌─────────────────────────────────┐
│       EtikettenDrucker          │
├─────────────────────────────────┤
│ <<abstract>>                    │
│ +druckeEtikett()                │  ← Factory-Methode
└─────────────────────────────────┘
          ▲
          │
    ┌─────┴──────┬─────────────────┬──────────────┐
    │            │                 │              │
┌───▼─────┐ ┌───▼──────┐   ┌────▼──────┐   ┌───▼─────────┐
│ Labor-  │ │  EKG-    │   │ Hilfsmittel-│   │  Medikament-│
│ Etiketten││ Etiketten│   │  Etiketten  │   │  Etiketten  │
│ Drucker │ │  Drucker │   │   Drucker   │   │   Drucker   │
└─────────┘ └──────────┘   └─────────────┘   └─────────────┘
     │           │               │                 │
     └─────┬─────┴───────┬───────┴─────────┬───────┴────────
           │             │                 │
        ┌──▼──────────▼──▼────┐    ┌────▼────────────▼────┐
        │   Hilfsmittel        │    │     Etikett          │
        ├──────────────────────┤    ├──────────────────────┤
        │ HilfsmittelID        │    │ <<Interface>>         │
        │ Bezeichnung          │    │ +generiereAusgabe()  │
        │ PatientID            │    └──────────────────────┘
        └──────────────────────┘
```

### d) Weiteres Entwurfsmuster (3 Punkte)

**Pattern: Observer (Beobachter)**

**Beschreibung:** Das Observer Pattern definiert eine 1:n-Abhängigkeit zwischen Objekten. Wenn ein Subjekt (z. B. Patientenakte) seinen Zustand ändert, werden alle registrierten Observer (z. B. zuständige Ärzte, Pflegepersonal) automatisch benachrichtigt und aktualisiert. Dies ermöglicht lose Kopplung und ereignisgesteuerte Updates.
