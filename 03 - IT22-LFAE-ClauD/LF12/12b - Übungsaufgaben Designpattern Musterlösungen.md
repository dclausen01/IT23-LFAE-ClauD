## Musterlösungen: Design Patterns

1. **Singleton vs. Factory**:  
   - *Singleton*: Stellt sicher, dass nur eine Instanz einer Klasse existiert (z. B. Datenbankverbindung). Struktur: private Konstruktor, statische `getInstance()`-Methode.  
   - *Factory*: Versteckt Objekterstellung hinter einer Schnittstelle (z. B. verschiedene Button-Typen je nach OS). Struktur: Interface + konkrete Factory-Klassen.  
   - *Einsatz*: Singleton für globale Zustände, Factory für dynamische Objekterzeugung mit Variabilität.

2. **Observer-Pattern**:  
   - *Vorteile*: Lose Kopplung, automatische Aktualisierung, erweiterbar (neue Observer ohne Änderung am Subjekt).  
   - *Nachteile*: Leistungsüberhead bei vielen Observern, schwer zu debuggen (nicht deterministische Aufrufreihenfolge).  
   - *Kopplung*: Reduziert direkte Abhängigkeiten – Subjekt kennt nur die Observer-Schnittstelle.

3. **Strategy-Pattern**:  
   - Struktur: Interface `Strategy` + konkrete Implementierungen (z. B. `SortAlgorithmA`, `SortAlgorithmB`) + Kontext, der Strategy nutzt.  
   - *Vorteil gegenüber if-else*: Neue Strategien werden hinzugefügt, ohne den Kontext zu ändern → Open/Closed-Prinzip erfüllt.

4. **Decorator vs. Vererbung**:  
   - Vererbung: Statische, zur Compile-Zeit festgelegte Funktionalität.  
   - Decorator: Dynamische, zur Laufzeit kombinierbare Funktionalitäten (z. B. `BorderDecorator`, `ScrollDecorator` um ein Textfeld).  
   - *Flexibilität*: Kombination mehrerer Decorators ohne Klassen-Hierarchie-Explosion.

5. **Programmieren gegen Interfaces**:  
   - Bedeutet: Abhängigkeiten von abstrakten Schnittstellen, nicht von konkreten Klassen.  
   - *Unterstützt durch*: Factory, Strategy, Observer.  
   - *Begründung*: Erleichtert Austausch, Testbarkeit und Erweiterung (z. B. `PaymentProcessor`-Interface → PayPal oder Stripe implementieren).

6. **Template Method & Klassenanzahl**:  
   - Jede Variation der Algorithmus-Schritte erfordert eine eigene Subklasse (z. B. `ReportGeneratorPDF`, `ReportGeneratorCSV`).  
   - *Nachteile*: Hohe Komplexität, schwer wartbar bei vielen Subklassen, „Feature-Sprawl“.

7. **Command-Pattern & Undo**:  
   - Jede Aktion wird als Objekt (`Command`) mit `execute()` und `undo()` encapsuliert.  
   - *Notwendige Komponenten*: Command-Interface, ConcreteCommands, Invoker, History-Stack (z. B. für Undo-Liste).

8. **Adapter-Pattern**:  
   - Löst das Problem: Komponenten mit inkompatiblen Schnittstellen zusammenzubringen.  
   - *Beispiel*: Legacy-System mit altem Kundenformat („KundeID, Name“) soll mit neuer CRM-Software („customer_id, full_name“) kommunizieren. Adapter übersetzt die Felder.

9. **Factory – immer eine Verbesserung?**  
   - *Nein*. Bei einfachen, statischen Objekten (z. B. nur ein Typ) ist Factory überengineering.  
   - *Gegenbeispiel*: Ein `Logger`-Objekt, das immer `ConsoleLogger` ist – kein Mehrwert durch Factory.

10. **Lernkurve & Teammanagement**:  
   - *Auswirkung*: Muster erhöhen Anfangsbelastung durch neues Vokabular und Konzepte.  
   - *Management*: Dokumentation mit Mustern + Code-Beispielen, Pair Programming, regelmäßige Code-Reviews, „Pattern-Cheat-Sheet“ im Teamwiki.