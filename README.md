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
is the eager initialisation.

Lazy Initialisation
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
