# Strategy Pattern

### Allgemeines
Das Strategy Pattern gehört zur Kategorie der behavioral design pattern und definiert eine "Familie" austauschbarer Algorythmen.
### Verwendung
Strategie-Objekte werden ähnlich wie Klassenbibliotheken verwendet. Im Gegensatz dazu handelt es sich jedoch nicht um externe Programmteile, sondern um integrale Bestandteile des eigentlichen Programms, die deshalb als eigene Objekte definiert wurden, damit sie durch andere Algorithmen ausgetauscht werden können.

Eine verwendung des Strategy Pattern bietet sich an, wenn
- viele verwandte Klassen sich nur in ihrem Verhalten unterscheiden.
- unterschiedliche (austauschbare) Varianten eines Algorithmus benötigt werden.
- Daten innerhalb eines Algorithmus vor Klienten verborgen werden sollen.
- verschiedene Verhaltensweisen innerhalb einer Klasse fest integriert sind (meist über Mehrfachverzweigungen), aber
	-  die verwendeten Algorithmen wiederverwendet werden sollen bzw.
	-  die Klasse flexibler gestaltet werden soll.

### UML 
Hier ist ein UML Beispiel für ein Typisches Strategy Pattern:
![Strategy Pattern](https://raw.githubusercontent.com/dsamwald-tgm/sew4-design-patterns-dsamwald-tgm/master/strategy%20pattern/img/strategy_pattern_uml.PNG)

Hier sind zwei UML von Verhalten mit ihren unterschiedlichen Verhaltensweisen:
![Strategy Pattern Verhalten](https://raw.githubusercontent.com/dsamwald-tgm/sew4-design-patterns-dsamwald-tgm/master/strategy%20pattern/img/strategy_pattern_verhalten_uml.PNG)