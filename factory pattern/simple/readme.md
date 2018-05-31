# Simple Factory Pattern

### Allgemeines
Das Simple Factory Pattern gehört zur Kategorie der creational patterns und beschreibt wie ein Objekt durch den Aufruf einer Methode anstatt durch den direkten Aufruf eines Konstruktors erzeugt wird.
### Verwendung
Das Factory Pattern wird angewendet, wenn eine Klasse die von ihr zu erzeugenden Objekte nicht kennen kann bzw. soll, oder wenn Unterklassen bestimmen sollen, welche Objekte erzeugt werden. Mit dem Factory Pattern kann ein Objekt erstellt werden sodass eine Unterklasse entscheidet welche Klasse initiiert wird.
##### Anwendungsbeispiel
Eine Pizzafabrik soll gebaut werden. Die Vorgänge sind immer die selben Schritte bei jeder Art von Pizza. Alles was sich verändert ist der Belag. Das Simple Factory Pattern sagt, man soll das abkapseln was sich verändern kann. Die Methode die nun die Pizzen belegt muss abgekapselt werden.

### UML 
Hier ist ein UML Beispiel für ein Typisches Simple Factory Pattern:

![Simple Factory Pattern UML](https://i.imgur.com/1i5hkIl.png)


Hier ist ein Beispiel in dem eine Pizza von einer Factory erzeugt wird:
![Simple Factory Pattern Example](https://i.imgur.com/byZuq1U.png)

### Code
Passend zu dem zweiten UML von oben nun eine Pizza Fabrik.

##### CheesePizza.class
```java
public class CheesePizza extends Pizza {
	public void Type() {
    	System.out.println("This is a CheesePizza")
    }
}
```
##### Pizza.class
```java
public abstract class Pizza {
	public void prepare() {
    	System.out.println("Pizza is now prepared")
    }
    
    public void bake() {
    	System.out.println("Pizza is now baked")
    }
    
    public void cut() {
    	System.out.println("Pizza is now cut")
    }
    
    public void box() {
    	System.out.println("Pizza is now boxed")
    }
}
```
##### SimplePizzaFactory.class
```java
public class SimplePizzaFactory {
	public Pizza createPizza(String type) {
    	Pizza pizza = null;
        
        if (type.equals("cheese")) {
        	pizza = new CheesePizza();
        } else if (type.equals("pepperoni")) {
        	pizza = new PepperoniPizza();
        } else if (type.equals("clam")) {
        	pizza = new ClamPizza();
        } else if (type.equals("veggie")) {
        	pizza = new VeggiePizza();
        }
        return pizza;
    }
}
```
##### PizzaStore.class
```java
public class PizzaStore {
	SimplePizzaFactroy factory;
    
    public PizzaStore(SimplePizzaFactory factory) {
    	this.factory = factory;
    }
    
    public Pizza orderPizza(String type) {
    	Pizza pizza;
        
        pizza = factory.createPizza(type)
        pizza.prepare();
        pizza.bake();
        pizza.cut();
        pizza.box();
        return pizza;
}
```
##### MachEinePizza.class
```java
public class MachEinePizza {
	public static void main(String[] args) {
    	SimplePizzaFactory LuigisFactory = new SimplePizzaFactory();
		PizzaStore Luigi = new PizzaStore(LuigisFactory);
        
        Pizza MyPizza = Luigi.orderPizza("cheese");
    }
}
```
##### Konsolen Output
```
>>> This is a Cheese Pizza
>>> Pizza is now prepared
>>> Pizza is now baked
>>> Pizza is now cut
>>> Pizza is now boxed
```