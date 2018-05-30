# Decorator Pattern

### Allgemeines
Das Decorator Pattern gehört zur Kategorie der structural patterns und dient als flexible Alternative zur Unterklassenbildung, um eine Klasse um zusätzliche Funktionalitäten zu erweitern.
### Verwendung
Die Instanz eines Dekorierers wird vor die zu dekorierende Klasse geschaltet. Der Dekorierer hat die gleiche Schnittstelle wie die zu dekorierende Klasse. Aufrufe an den Dekorierer werden dann verändert oder unverändert weitergeleitet (Delegation), oder sie werden komplett in Eigenregie verarbeitet. Der Dekorierer ist dabei „unsichtbar“, da der Aufrufende gar nicht mitbekommt, dass ein Dekorierer vorgeschaltet ist.
##### Anwendungsbeispiel
Ein Kaffee von bspw. Starbucks besteht aus verschiedenen Zutaten. Diese Zutaten kosten alle ihren Aufpreis und haben ihre speziellen Eigenschaften. Nun kann man mit einem Decorator Pattern einen Kaffee zusammenstellen der alle Eigenschaften der verschiedenen Zutaten kombiniert.

### UML 
Hier ist ein UML Beispiel für ein Typisches Decorator Pattern:
![Strategy Pattern](https://i.imgur.com/g8StIVx.png)


Hier ist ein Beispiel in dem ein Getränk(Kaffee) Decorated wird:
![Strategy Pattern](https://i.imgur.com/nBqsS15.png)

### Code
Passend zu dem zweiten UML von oben nun ein Decorator Pattern um einen Kaffee zu dekorieren.

##### Beverage.class
```java
public abstract class Beverage {
	String description = "Unknown Beverage";
    
    public String getDescription() {
    	return description;
    }
    public abstract double cost();
}
```
##### CondimentDecorator.class
```java
public abstract class CondimentDecorator extends Beverage {
	public abstract String getDescription();
}
```
##### Espresso.class
```java
public class Espresso extends Beverage {
	public Espresso() {
    	description = "Espresso";
    }
    
    public double cost() {
    	return 1.99;
    }
}
```
##### HouseBlend.class
```java
public class HouseBlend extends Beverage {
	public HouseBlend() {
    	description = "House Blend Coffee";
    }
    
    public double cost() {
    	return 0.89;
    }
}
```
##### Mocha.class
```java
public class Mocha extends CondimentDecorator {
	Beverage beverage;
    
    public Mocha(Beverage beverage) {
    	this.beverage = beverage;
    }
    
    public String getDescription() {
    	return beverage.getDescription() + ", Mocha";
    }
    
    public double cost() {
    	return 0.20 + beverage.cost();
    }
}
```
##### Soy.class
```java
public class Soy extends CondimentDecorator {
	Beverage beverage;
    
    public Soy(Beverage beverage) {
    	this.beverage = beverage;
    }
    
    public String getDescription() {
    	return beverage.getDescription() + ", Soy";
    }
    
    public double cost() {
    	return 0.15 + beverage.cost();
    }
}
```
##### StarbuzzCoffee.class
```java
public class StarbuzzCoffee {
	public static void main(String[] args) {
    	Beverage beverage1 = new Espresso();
        System.out.println(beverage1.getDescription()
        	+ " $" + beverage1.cost());
      	
        Beverage beverage2 = new HouseBlend();
        beverage2 = new Mocha(beverage2);
        beverage2 = new Mocha(beverage2);
        System.out.println(beverage2.getDescription()
        	+ " $" + beverage2.cost());
        
        Beverage beverage3 = new HouseBlend();
        beverage3 = new Soy(beverage3);
        System.out.println(beverage3.getDescription()
        	+ " $" + beverage3.cost());
    }
}
```
##### Konsolen Output
```
>>> Espresso $1.99
>>> House Blend Coffee, Mocha, Mocha $1.29
>>> House Blend Coffee, Soy $1.04
```