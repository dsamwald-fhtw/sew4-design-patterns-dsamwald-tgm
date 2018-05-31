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
![Strategy Pattern UML](https://i.imgur.com/RMoV0aZ.png)

Hier sind zwei UML von Verhalten mit ihren unterschiedlichen Verhaltensweisen:
![Strategy Pattern Example UML](https://i.imgur.com/PhAKit6.png)

### Code
Passend zu den Verhalten von oben nun ein Strategy Pattern mit Enten.
Es gibt verschiedene Enten:
- MallardDuck
- DecoyDuck
- RubberDuck

Und wir haben wie in der zweiten Graphik von oben zu sehen ist Verschiedene Flug und Quack Verhalten.

##### Duck.class
```java
public class Duck {

	QuackBehavior quackBehavior;
    FlyBehavior flyBehavior;
    
    public void performQuack() {
    	quackBehavior.quack();
    }
    
    public void performFly() {
    	flyBehavior.fly();
    }
}
```
##### DecoyDuck.class
```java
public class DecoyDuck extends Duck {

	public DecoyDuck() {
    	quackBehavior = new MuteQuack();
        flyBehavior = new FlyNoWay();
    }
    
    public void display() {
    	System.out.println("I'm a decoy duck")
    }
}
```
##### MallardDuck.class
```java
public class MallardDuck extends Duck {

	public MallardDuck() {
    	quackBehavior = new Quack();
        flyBehavior = new FlyWithWings();
    }
    
    public void display() {
    	System.out.println("I'm a real Mallard duck")
    }
}
```
##### Test.class
```java
public class DuckSimulator {
	public static void main(String[] args) {
    
    	Duck decoy = new DecoyDuck();
        decoy.performQuack();
        decoy.performFly();
        
        Duck mallard = new MallardDuck();
        mallard.performQuack();
        mallard.performFly();
    }
}
```

##### Konsolen Output
```
>>> MuteQuack
>>> I can't fly.

>>> Quack
>>> I'm flying!!
```