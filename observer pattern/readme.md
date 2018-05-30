# Observer Pattern

### Allgemeines
Das Observer Pattern gehört zur Kategorie der behavioral patterns und dient der Weitergabe von Änderungen an einem Objekt an von diesem Objekt abhängige Strukturen.
### Verwendung
Das Observer-Pattern definiert eine Eins-zu-viele-Abhängigkeit zwischen Objekten in der Art, dass alle abhängigen Objekte benachrichtigt werden, wenn sich der Zustand des einen Objekts ändert.
##### Anwendungsbeispiel
Eine oder auch mehrere Komponenten(Wetteranzeigen) stellen den Zustand eines Objektes(Wetterstation) grafisch dar. Sie kennen die gesamte Schnittstelle dieses Objektes(Wetterstation). Ändert sich der Zustand des Objektes(Wetterstation), müssen die Komponenten(Wetteranzeigen) darüber informiert werden. Andererseits soll das Objekt(Wetterstation) aber von den Komponenten(Wetteranzeigen) unabhängig bleiben, ihre Schnittstelle also nicht kennen.

### UML 
Hier ist ein UML Beispiel für ein Typisches UML Pattern:
![Strategy Pattern](https://i.imgur.com/08ws8I4.png)



