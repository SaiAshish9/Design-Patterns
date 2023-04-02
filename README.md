```
https://thecodingsimplified.com/singleton-design-pattern/
https://www.tutorialspoint.com/design_pattern/design_pattern_overview.htm

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

