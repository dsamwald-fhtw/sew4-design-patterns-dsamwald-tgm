# Observer Pattern

### Allgemeines
Das Observer Pattern gehört zur Kategorie der behavioral patterns und dient der Weitergabe von Änderungen an einem Objekt an von diesem Objekt abhängige Strukturen.
### Verwendung
Das Observer-Pattern definiert eine Eins-zu-viele-Abhängigkeit zwischen Objekten in der Art, dass alle abhängigen Objekte benachrichtigt werden, wenn sich der Zustand des einen Objekts ändert.
##### Anwendungsbeispiel
Eine oder auch mehrere Komponenten(Wetteranzeigen) stellen den Zustand eines Objektes(Wetterstation) grafisch dar. Sie kennen die gesamte Schnittstelle dieses Objektes(Wetterstation). Ändert sich der Zustand des Objektes(Wetterstation), müssen die Komponenten(Wetteranzeigen) darüber informiert werden. Andererseits soll das Objekt(Wetterstation) aber von den Komponenten(Wetteranzeigen) unabhängig bleiben, ihre Schnittstelle also nicht kennen.

### UML 
Hier ist ein UML Beispiel für ein Typisches Observer Pattern:
![Strategy Pattern](https://i.imgur.com/08ws8I4.png)


Hier ist ein Beispiel in Form einer Wetterstation zu sehen:
![Strategy Pattern](https://i.imgur.com/tXBtsyz.png)

### Code
Passend zu dem zweiten UML von oben nun ein Observer Pattern mit einer Wetterstation.

##### Interface Subject
```java
public interface Subject {
	public void registerObserver(Observer o);
    public void removeObserver(Observer o);
    public void notifyObservers();
}
```
##### Interface Observer
```java
public interface Observer {
	public void update(float temp, float humidity, float pressure);
}
```
##### Interface DisplayElement
```java
public interface DisplayElement {
	public void display();
}
```
##### WeatherData.class
```java
public class WeatherData implements Subject {
	private ArrayList observers;
    private float temperature;
    private float humidity;
    private float pressure;
    
    public WeatherData() {
    	observers = new ArrayList();
    }
    
    public void registerObserver(Observer o) {
    	observers.add(o);
    }
    
    public void removeObserver(Observer o) {
    	int i = observers.indexOf(o);
        if(i >= 0) {
        	observers.remove(i);
        }
    }
    
    public void notifyObservers() {
    	for(int i = 0; i < observer.size(); i++) {
    		Observer observer = (Observer)observer.get(i);
            observer.update(temperature, humidity, pressure);
    	}
    }
    
    public void measurementsChanged() {
    	notifyObservers();
    }
    
    public void setMeasurements(float temperature, float humidity, float pressure) {
    	this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        measurementsChanged();
    }
}
```
##### CurrentConditionsDisplay.class
```java
public class CurrentConditionsDisplay implements Observer, DisplayElement {
	private float temperature;
    private float humidity;
    private Subject weatherData;
    
    public CurrentConditionsDisplay(Subject weatherData) {
    	this.weatherData = weatherData;
        weatherData.registerObserver(this);
    }
    
    public void update(float temperature, float humidity, float pressure) {
    	this.temperature = temperature;
        this.humidity = humidity;
        display();
    }
    
    public void display() {
    	System.out.println("Current conditions: " + temperature 
        	+ "F degrees and " + humidity + "% humidity");
    }
}
```
##### WeatherStation.class
```java
public class WeatherStation {
	public static void main(String[] args) {
    	WeatherData weatherData = new WeatherData();
        
        CurrentConditionsDisplay currentDisplay = new CurrentConditionsDisplay(weatherData);
        
        weatherData.setMeasurements(80, 65, 30.4f);
        weatherData.setMeasurements(82, 70, 29.2f);
        weatherData.setMeasurements(78, 90, 29.2f);
    }
}
```
##### Konsolen Output
```
>>> Current conditions: 80.0F degrees and 65.0% humidity
>>> Current conditions: 82.0F degrees and 70.0% humidity
>>> Current conditions: 78.0F degrees and 90.0% humidity
```