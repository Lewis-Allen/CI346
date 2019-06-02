## CI346 Glossary (maintained by UoB students)

1. [Programming languages](#programming-languages)
2. [Concurrency](#concurrency)
3. [Client-server computing](#client-server-computing)

Programming Languages
---

**Object-oriented Paradigm**

Object-oriented (OO) programming solves computing concepts and problems by modelling objects. Objects have **states** and **behaviours**; for example, a person has a certain hair colour (state) and this person can change the colour(behaviour). **Inheritance** is part of the core functionality of objects in OO languages. **Classes** can have subclasses, which enables the subclass to inherit the methods and fields of its superclass. The core concept of inheritance is simple, but it can be used to model complex systems. **Encapsulation** is used to enclose methods and state in bundles and to restrict access to them.

Using _Java_ as the example language
```java
class Person {
    String hairColour;

    Person(String hairColour) {
        this.hairColour = hairColour;
    }

    void changeHairColour(final String colour){
        this.hairColour = colour;
    }
}

class Java {
    public static void main(String[] args) {
        Person pete = new Person("blue");

        System.out.println(pete.hairColour);
        pete.changeHairColour("white");
        System.out.println(pete.hairColour);
    }
}
```

-TODO: expand on this

**Functional Paradigm**  
Functional programming solves computing problems by chaining functions together. Functions are computations that have the same effect whether done once or multiple times (**idempotent**), similar to mathematical functions. They have referential transparency - that is a function always returns the same output for a given input. Typically there is no state and therefore no side-effects. Iterative loops are not allowed in functional programs, instead recursive calls are used.

Using _Haskell_ as the example language
```haskell
fib :: Integer -> Integer
fib 0 = 0
fib 1 = 1
fib n = fib (n-1) + fib (n-2)

main :: IO()
main = print (fib 10)
```
-TODO: expand on this



**Functional Paradigm vs Object-Oriented**

**SOLID Principles**

| Principle | Description | Code Smell | Benefits |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|----------|
| Single Responsibility | Class should have only one responsibility which means class should be highly cohesive and  implement strongly related logic. Class implementing feature 1 AND feature 2 AND feature 3 (and  so on) violates SRP. | <ul><li>More than one contextually separated piece of code within single class.</li><li>Large setup in tests (TDD is very useful when it comes to detecting SRP violation).</li></ul> | <ul><li>Separated classes responsible for given use case can be now reused in other parts of an application.</li><li>Separated classes responsible for given use case can be now tested separately.</li></ul> |
| Open/Closed | Class should be open for extension and closed for modification. You should be able to extend class’ behavior without the need to modify its implementation (how? Don’t modify existing code of class X but write a new piece of code that will be used by class X). | <ul><li>If you notice class X directly references other class Y from within its code base, it’s a sign that class Y should be passed to class X (either through constructor/single method) e.g. through dependency injection.</li><li>Complex if-else or switch statements.</li><ul> | <ul><li>Class’ X functionality can be easily extended with new functionality encapsulated in a separate class without the need to change class’ X implementation (it’s not aware of introduced changes).</li><li>Code is loosely coupled.</li><li>Injected class Y can be easily mocked in tests.</li></ul> |
| Liskov Substitution | Extension of open/closed principle stating that new derived classes extending the base class should not change the behavior of the base class (behavior of inherited methods). Provided that if a class Y is a subclass of class X any instance referencing class X should be able to reference class Y as well (derived types must be completely substitutable for their base types.). | <ul><li>If it looks like a duck, quacks like a duck but needs batteries for that purpose - it’s probably a violation of LSP.</li><li>Modification of inherited behavior in subclass</li><li>Exceptions raised in overridden inherited methods</li></ul> | <ul><li>Avoiding unexpected and incorrect results.</li><li>Clear distinction between shared inherited interface and extended functionality.</li></ul> |
| Interface Segregation | Client should not depend on interface/methods which it is not using. | <ul><li>One fat interface implemented by many classes where none of these classes implement 100% of interface’s methods. Such fat interface should be split into smaller interfaces suit able for client needs.</li></ul> | <ul><li>Highly cohesive code.</li><li>Avoiding coupling between all classes using a single fat interface (once a method in the single fat interface gets updated, all classes - no matter they use this method or not - are forced to update accordingly).</li><li>Clear separation of business logic by grouping responsibilities into separate interfaces.</li></ul> |
| Dependency Inversion | High-level modules (e.g. business logic) should not depend on low-level modules (e.g. database operations or I/O). Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions. | <ul><li>Instantiation of low-level modules in high-level ones.</li><li>Calls to class methods of low-level modules/classes.</li></ul> | <ul><li>Increase reusability of higher-level modules by making them independent of lower-level modules.</li><li>Injected class can be easily mocked in tests.</li></ul> |

Adapted from [SOLID Cheatsheet](https://www.monterail.com/hubfs/PDF%20content/SOLID_cheatsheet.pdf)

**Design Patterns**

A software design pattern is a general, reusable solution to a commonly occurring problem within a given context in software design. It is a description or template for how to solve a problem that can be used in many different situations. Design patterns are formalized best practices that the programmer can use to solve common problems when designing an application or system. Object-oriented design patterns typically show relationships and interactions between classes or objects, without specifying the final application classes or objects that are involved.

***List of Design Patterns***

Most Design patterns can be grouped into one of the following categories: creational patterns, structural patterns, and behavioral patterns. Patterns defined as per the [Gang of Four](https://en.wikipedia.org/wiki/Design_Patterns).

****Creational****

| Name | Description |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Abstract factory | Provide an interface for creating families of related or dependent objects without specifying their concrete classes. |
| Builder | Separate the construction of a complex object from its representation allowing the same construction process to create various representations. |
| Dependency Injection | A class accepts the objects it requires from an injector instead of creating the objects directly. |
| Factory method | Define an interface for creating a single object but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses. |
| Prototype | Specify the kinds of objects to create using a prototypical instance, and create new objects from the 'skeleton' of an existing object, thus boosting performance and keeping memory footprints to a minimum. |
| Singleton | Ensure a class has only one instance, and provide a global point of access to it. |

****Structural****

| Name | Description |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Adapter | Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces. |
| Bridge | Decouple an abstraction from its implementation so that the two can vary independently. |
| Composite | Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly. |
| Decorator | Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to sub-classing for extending functionality. |
| Facade | Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use. |
| Flyweight | Use sharing to support large numbers of fine-grained objects efficiently. |
| Proxy | Provide a surrogate or placeholder for another object to control access to it. |

****Behavioural****

| Name | Description |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Chain of Responsibility | Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.  |
| Command | Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations. |
| Interpreter | Given a language, define a representation for its grammar along with an interpreter that uses the representation to interpret sentences in the language. |
| Iterator | Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation. |
| Mediator | Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and lets you vary their interaction independently. |
| Memento | Without violating encapsulation, capture and externalize an object's internal state so that the object can be restored to this state later. |
| Observer | Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically. |
| State | Allow an object to alter its behaviour when its internal state changes. The object will appear to change its class. |
| Strategy | Define a family of algorithms, encapsulate each one, and make them interchangable. Strategy lets the algorithm vary independently from clients that use it. |
| Template Method | Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure. |
| Visitor | Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates. |

Concurrency
---

**Process** - TODO


**Thread** - A thread is a spawnable unit of work in a program.
The Java Virtual Machine allows an application to have multiple threads of execution running concurrently.

[Source](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Thread.html)

```
Thread t = new Thread(() -> {
    // some code to run on new thread
});
t.start();
```

**Concurrency Advantages**

**Concurrency Issues and Solutions**


Client-server Computing
---

**TCP** - TODO

**UDP** - TODO
