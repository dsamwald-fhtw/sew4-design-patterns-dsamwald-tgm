# Abstract Factory Pattern

### Allgemeines
Das Abstract Factory Pattern gehört zur Kategorie der creational patterns. Es definiert eine Schnittstelle zur Erzeugung einer Familie von Objekten, wobei die konkreten Klassen der zu instanziierenden Objekte nicht näher festgelegt werden
### Verwendung
Die Abstrakte Fabrik wird angewendet, wenn:
- ein System unabhängig von der Art der Erzeugung seiner Produkte arbeiten soll,
- ein System mit einer oder mehreren Produktfamilien konfiguriert werden soll,
- eine Gruppe von Produkten erzeugt und gemeinsam genutzt werden soll oder
- wenn in einer Klassenbibliothek die Schnittstellen von Produkten ohne deren Implementierung bereitgestellt werden sollen.
### UML 
Hier ist ein UML Beispiel für ein Typisches Abstract Factory Pattern:

![Abstract Factory Pattern UML](https://i.imgur.com/pMks2iF.png)


Hier ist ein Beispiel in dem eine Pizza von einer Abstract Factory erzeugt wird:
![Abstract Factory Pattern Example](https://i.imgur.com/vRqQlv8.png)
### Code
Passend zu dem zweiten UML von oben nun eine Pizza Fabrik.

##### Interface PizzaIngredientFactory
```java
public interface PizzaIngridientFactory {
	public Dough createDough();
    public Sauce createSauce();
    public Cheese createCheese();
    public Veggies[] createVegies();
    public Pepperoni createPepperoni();
    public Clams createClam();
}
```

##### NYPizzaIngredientFactory.class
```java
public class NYPizzaIngredientFactory implements PizzaIngredientFactory {
	public Dough createDough() {
    	return ThinCrustDough();
    }
    
    public Sauce createSauce() {
    	return MarinaraSauce();
    }
    
    public Cheese createCheese() {
    	return ReggianoCheese();
    }
    
    public Veggies[] createVeggies() {
    	Veggies veggies[] = { new Garlic(), new Onion(), new Mushroom(), new RedPepper() };
        return veggies;
    }
    
    public Pepperoni createPepperoni() {
    	return SlicedPeperoni();
    }
    
    public Clam createClam() {
    	return FreshClams();
    }
}
```
##### CheesePizza.class
```java
public class CheesePizza extends Pizza {
	PizzaIngredientFactory ingredientFactory;
    
    public CheesePizza(PizzaIngredientFactory ingredientFactory) {
    	this.ingredientFactory = ingredientFactory;
    }
    
    void prepare() {
    	System.out.println("Preparing" + name);
        dough = ingredientFactory.createDough();
        sauce = ingredientFactory.createSauce();
        cheese = ingredientFactory.createCheese();
    }
}
```
##### Pizza.class
```java
public abstract class Pizza {
	String name;
    Dough dough;
    Sauce sauce;
    Veggies veggies[];
    Cheese cheese;
    Pepperoni pepperoni;
    Clams clam;

	abstract void prepare() {
    	System.out.println("Pizza is now prepared")
    }
    
    void bake() {
    	System.out.println("Pizza is now baked")
    }
    
    void cut() {
    	System.out.println("Pizza is now cut")
    }
    
    void box() {
    	System.out.println("Pizza is now boxed")
    }
    
    void setName(String name) {
    	this.name = name;
    }
    
    String getName(){
    	return name;
    }
    
    public String toString() {
    	System.out.println(name)
    }
}
```
##### PizzaStore.class
```java
public abstract class PizzaStore {
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
```
##### NYPizzaStore.class
```java
public class NYPizzaStore extends PizzaStore {
	protected Pizza createPizza(String item) {
    	Pizza pizza = null;
        PizzaIngredientFactory ingredientFactory = new NYPizzaIngredientFactory();
        
        if (item.equals("cheese")) {
        	pizza = new CheesePizza(ingredientFactory);
            pizza.setName("New York Style Cheese Pizza");
        } else if (item.equals("pepperoni")) {
        	pizza = new PepperoniPizza(ingredientFactory);
            pizza.setName("New York Style Pepperoni Pizza");
        } else if (item.equals("clam")) {
        	pizza = new ClamPizza(ingredientFactory);
            pizza.setName("New York Style Clam Pizza");
        } else if (item.equals("veggie")) {
        	pizza = new VeggiePizza(ingredientFactory);
            pizza.setName("New York Style Veggie Pizza");
        }
        return pizza;
    }
}
```