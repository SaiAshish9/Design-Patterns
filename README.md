```
https://thecodingsimplified.com/singleton-design-pattern/
https://www.tutorialspoint.com/design_pattern/design_pattern_overview.htm
https://www.youtube.com/watch?v=0Ptcaxyne3s&list=PLt4nG7RVVk1h9lxOYSOGI9pcP3I5oblbx&index=3

Singleton Design Pattern Properties

Creational design pattern 
(It's related to the creation of object in java).
Only one instance of class should exist throughout the implementation.
Other classes should be able to get instance of singleton class
Used in logging, cache, session, drivers

Implementation 

Constructor should be private
Public method for returning instance
Instance type - private static

Initialisation Type

Eager Initialisation

As soon as we initialize the instance , it automatically create
auto sync time.

Whenever we are declaring the variable, we are defining it. This
is the eager initialisation. At the same time, we are doing.

Lazy Initialisation

Whever there's a need ot a call, then only it will create the object.

Thread safe method initialisation
Thread safe block initialisation

class SingletonEagar {
  private static SingletonEagar instance = new SingletonEagar(); 
  private SingletonEagar(){}
  public static SingletonEagar getInstance() {
    return instance;
  }
}

class Singleton {
  private static Singleton instance; 
  private Singleton(){}
  public static Singleton getInstance() {
    if(instance == null) {
      instance = new Singleton(); 
    }
    return instance;
  }
}

class SingletonSynchronizedMethod {
  private static SingletonSynchronizedMethod instance; 
  private SingletonSynchronizedMethod(){}
  public static synchronized SingletonSynchronizedMethod getInstance() {
    if(instance == null) {
      instance = new SingletonSynchronizedMethod();
    }
    return instance;
  }
}

class SingletonSynchronized {
  private static SingletonSynchronized instance; 
  private SingletonSynchronized(){}
  public static SingletonSynchronized getInstance() {
    if(instance == null) {
      synchronized (SingletonSynchronized.class) {
        if(instance == null) {
          instance = new SingletonSynchronized();
        }
      }
    }
    return instance;
  }
}

public class SingletonExample {
  public static void main(String[] args) {
    SingletonSynchronized instance = SingletonSynchronized.getInstance();
    System.out.println(instance);
    SingletonSynchronized instance1 = SingletonSynchronized.getInstance();
    System.out.println(instance1);
  }
}
```

```
Factory Design Pattern

Creational design pattern
Used when we have multiple sub-classes of a super class and based on
input we want to return once class instance.
It provides abstraction between implementation and client classes
Remove the instantiation of client classes from client code.

Implementation 

Super class can be interface or abstract class or basic class
Factory class has a static method which returns the instance of
sub-class on input.

abstract class Vehicle {
  public abstract int getWheel();
  
  public String toString() {
    return "Wheel: " + this.getWheel();
  }
}

class Car extends Vehicle {
  int wheel;
  
  Car(int wheel) {
    this.wheel = wheel;
  }

  @Override
  public int getWheel() {
    return this.wheel;
  }
}

class Bike extends Vehicle {
  int wheel;
  
  Bike(int wheel) {
    this.wheel = wheel;
  }
  
  @Override
  public int getWheel() {
    return this.wheel;
  }
}

class VehicleFactory {
  public static Vehicle getInstance(String type, int wheel) {
    if(type == "car") {
      return new Car(wheel);
    } else if(type == "bike") {
      return new Bike(wheel);
    }
    return null;
  }
}

public class FactoryPatternExample {

  public static void main(String[] args) {
    Vehicle car = VehicleFactory.getInstance("car", 4);
    System.out.println(car);
    Vehicle bike = VehicleFactory.getInstance("bike", 2);
    System.out.println(bike);
  }

}
```

```
Builder Pattern

It's a creational design pattern. It's related to object creation.

Creational design pattern
Used when we have too many arguments to send in constructor and
its hard to maintain the order.
When we don't want to send all parameters in object initialisation 
(Generally we send optional parameters as null)

Implementation

We create a 'static nested class', which contains all arguments of outer
class.
As per naming convention, if class name is 'Vehicle', builder class
should be 'VehicleBuilder'
Builder class have a public constructor with all required parameters

A 'build()' method that will return the final object

The main class 'Vehicle' has private constructor so to create instance only
via Builder class.
The main class 'Vehicle' has only getters

package builder;

class Vehicle {
  //required parameter
  private String engine;
  private int wheel;
  
  //optional parameter
  private int airbags;
  
  public String getEngine() {
    return this.engine;
  }
  
  public int getWheel() {
    return this.wheel;
  }
  
  public int getAirbags() {
    return this.airbags;
  }
  
  private Vehicle(VehicleBuilder builder) {
    this.engine = builder.engine;
    this.wheel = builder.wheel;
    this.airbags = builder.airbags;
  }
  
  public static class VehicleBuilder {
    private String engine;
    private int wheel;
    private int airbags;
    
    public VehicleBuilder(String engine, int wheel) {
      this.engine = engine;
      this.wheel = wheel;
    }
    
    public VehicleBuilder setAirbags(int airbags) {
      this.airbags = airbags;
      return this;
    }
    
    public Vehicle build() {
      return new Vehicle(this);
    }
  }
}

public class BuilderPatternExample {
  
  public static void main(String[] args) {
    Vehicle car = new Vehicle.VehicleBuilder("1500cc", 4).setAirbags(4).build();
    Vehicle bike = new Vehicle.VehicleBuilder("250cc", 2).build();
    
    System.out.println(car.getEngine());
    System.out.println(car.getWheel());
    System.out.println(car.getAirbags());
    System.out.println(bike.getEngine());
    System.out.println(bike.getWheel());
    System.out.println(bike.getAirbags());
  }
}
```
