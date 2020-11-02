---
layout: post
title: Notes on Design Principles
date: 2020-08-01
category: category
---
## DRY (Don't repeat yourself)
* Abstract a common piece of code into abstract class, interface, constants or parent classes.
* Extend the abstract class or the parent class to use the common piece.
* Call the interface to invoke the common code which is written in the implementation class.
* Violation of DRY is WET (Write everthing twice). Sometimes makes sense where the code is not related at all.

## KISS (Keep it simple and stupid)
* Short, human readable, testable and the rubber duck must understand the program.

## SPR (Single Responsibility Principle)
* A class must have only one responsibility/functionality. Extending from the class becomes easy if the class is responsible for only 1 functionality.
* Is it a good idea to seperate functionalities w.r.t one entity into different class to keep SPR ?

* SPR - Controller, service, DB

## Open/Closed
* Open for extension and closed for modifications

~~~java
// Sorts anything that implements Comparable interface
// The behaviour(sorting) do not change with the different implementation
Collections.sort(); 
~~~

## LSP (Liskov Substitution principle)
* derived classes should be able to substitute their base classes without the behavior of your code changing.
* Violation of SPR or ISP leads to violation of LSP.
* Example of a Square class extending from the Rectangle class. 
* I cannot substitute the Square class methods to Rectangle class methods.

## ISP (Interface segregation principle)
* The interface must only have the common methods that would be implemented by the class.
* Implementing class specific methods should in the same class and not in the interface.

## DIP (Dependency Inversion principle)
* When 2 classes are related, the relation should be abstracted. This helps in decoupling the code and changes in either of the classes will not affect the other and the changes are easy to make.

## Composition over Inheritance 
* If the class is going to implement all of the functionalities and your child class can be used as a substitute for your parent class, use inheritance.
* If the class is going to implement some specific functionalities, use composition.

Design patterns adhere to 2 principles - Programe an interface and not implementation and use composition over interfaces.

## Law of Demeter
The Law of Demeter for functions/methods requires that a method M of an object O may only invoke the methods of the following kinds of objects:
* O itself
* M’s parameters
* Any objects created/instantiated within M
* O’s direct component objects
* A global variable, accessible by O, in the scope of M

~~~Java
public class LawOfDemeterInJava
{
  private Topping cheeseTopping;
  
  /**
   * Good examples of following the Law of Demeter.
   */
  public void goodExamples(Pizza pizza)
  {
    Foo foo = new Foo();
    
    // (1) it's okay to call our own methods
    doSomething();
    
    // (2) it's okay to call methods on objects passed in to our method
    int price = pizza.getPrice();
    
    // (3) it's okay to call methods on any objects we create
    cheeseTopping = new CheeseTopping();
    float weight = cheeseTopping.getWeightUsed();
    
    // (4) any directly held component objects
    foo.doBar();
  }
  
  private void doSomething()
  {
    // do something here ...
  }

  /**
  * Scenarios where the law is violated
  **/
  public void badExample(Pizza pizza) {
  	pizza.getPizzaBase().getRawMaterial().doSomething();
  }
}
~~~
* To overcome using a method of an indirect object (PizzaBase and RawMaterial), the clear solution is to pass the respective methods object into the method.
* The other way is to write wrapper methods around the methods, and when needs to be called, call the delegators. 

[Reading Link 1](https://stackabuse.com/object-oriented-design-principles-in-java/)
[Reading Link 2](https://alvinalexander.com/java/java-law-of-demeter-java-examples/)
