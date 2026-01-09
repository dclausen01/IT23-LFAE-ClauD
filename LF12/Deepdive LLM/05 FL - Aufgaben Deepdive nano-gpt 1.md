# LLM Datenfluss-Analyse

**Tool**: bbycroft.net/llm -> Modell: nano-gpt

<u><b>Aufgaben für den Start</b></u>

1. **Die Struktur:** Aus wie vielen "Blocks" (Layern) besteht das nano-gpt Modell in der Visualisierung?
	1. Aus drei übergeordneten Blocks mit insgesamt fünf Verarbeitungsschichten
    
2. **Attention:** Klicke in einem Block auf "Self-Attention". Fahre mit der Maus über die Matrix. Kannst du erkennen, dass die Pixel heller werden, wenn Tokens eine Verbindung zueinander haben? Was bedeutet das?
	1. Die Helligkeit der Pixel repräsentiert den Vektorwert des entsprechenden Matrix-Wertes. Je höher ein Wert, desto näher liegen die Tokens kontextuell beieinander
    
3. **Feed Forward:** Nach der Attention kommt ein "Feed Forward" Teil. In neuronalen Netzen sagt man, hier ist das "Wissen" gespeichert. Wie verändern sich die Datenpunkte hier im Vergleich zur Attention? (Beobachtung reicht)
	1. Zu viel, zu hoch...
    
4. **Output:** Warum ist der Output immer nur _ein_ Token? Wie entstehen dann ganze Sätze? (Erkläre den Loop).
	1. Der "Vorhergesagte" Output-Token wird zurück in den Input gespeist. Anschließend beginnen die Berechnungen mit dem ergänzten Input von vorne, bis schließlich ein fertiges Resultat entstanden ist. Ich vermute, das Modell errechnet auf die gleiche Weise das Ende einer Antwort, wie dessen Inhalt.

