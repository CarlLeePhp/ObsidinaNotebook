#### Abstract Class VS Interface
**Abstract Class/Method**
- An abstract class cannot be instantiated. It only exists to be a base class for others to inherit from. But we can use it like:
```csharp
Shape shape = new Square();
```
- An abstract method is a method with no body, it will be implemented in the inheriting class(es).
- An abstract class may include normal methods, fields and properties.
- Abstract classes often also include virtual methods.

**Interface**
- Interface can only include unimplemented methods. No virtual/real methods, no fields, etc.
- Everything in an interface is automatically public, it doesn't use any visibility keywords.
- Contracts.

#### Polymorphism
- Static or compile-time polymorphism (This comes from method overloading)
- Dynamic or run-time polymorphism (This comes from using interfaces, base classes, and overriding abstract or virtual methods)

#### Method Overloading or Overriding


02 Home work
SOLID Priceples. The SOLID principles were first introduced by the famous Computer Scientist Robert J. Martin (a.k.a Uncle Bob) in his [paper](https://fi.ort.edu.uy/innovaportal/file/2032/1/design_principles.pdf) in 2000.

https://www.freecodecamp.org/news/solid-principles-explained-in-plain-english/
-   The **S**ingle Responsibility Principle
-   The **O**pen-Closed Principle
-   The **L**iskov Substitution Principle
-   The **I**nterface Segregation Principle / ˌsegriˈgeiʃn /
-   The **D**ependency Inversion Principle

We put too many functions into one class. Any of these functions needs to be modified we need to modify the class.

The Open-Closed Principle requires that **classes should be open for extension and closed to modification.
But how are we going to add new functionality without touching the class, you may ask. It is usually done with the help of interfaces and abstract classes.

The Liskov Substitution Principle states that subclasses should be substitutable for their base classes.


Segregation means keeping things separated, and the Interface Segregation Principle is about separating the interfaces.
The principle states that many client-specific interfaces are better than one general-purpose interface. Clients should not be forced to implement a function they do no need.

The Dependency Inversion principle states that our classes should depend upon interfaces or abstract classes instead of concrete classes and functions.
Let's say we need to calculate the area of a shape. At the beginning there are rectangle, square. So we created two classes, rectangle and square. In the main class we create the objects.
Or we create an base class shape. And we only use it in our main class. We also need a factory class to create specific shape for us. Then we don't need to modify our main class when we calculate the area for different shapes.



JSON: key value pairs