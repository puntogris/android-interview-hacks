### Coroutine
A variant of funtions that enables concurrency(Concurrency allows programs to deal with a lot of tasks at once.) via cooperative multitasking

_ Alternative to multithreading._

Usually we heart something like - coroutines are light weight threads, they allow us to write asynchronous, non-blocking code in a synchronous manner

A _coroutine_ is an instance of suspendable computation. It is conceptually similar to a thread, in the sense that it takes a block of code to run that works concurrently with the rest of the code. However, a coroutine is not bound to any particular thread. It may suspend its execution in one thread and resume in another one.

Coroutines can be thought of as light-weight threads, but there is a number of important differences that make their real-life usage very different from threads.

Coroutines are functions that are cooperative.

How are functions non-cooperative?

Usually, when a function calls a second function, the first cannot continue until the second function finishes and returns to where it was called.

The control remains with the second function until it executes completely and only then can the control return to the first one

How can functions cooperate with one another?

Coroutines are functions where the control is transferred from one function to the other function in a way that the _exit_ point from the _first_ function and the _entry_ point to the _second_ function are remembered – without changing the context.

Thus, each function remembers where it left the execution and where it should resume from.

### Flow
Flow API in Kotlin is a better way to handle the stream of data asynchronously that executes sequentially.

### OOP Concepts

Object-Oriented Programming (or OOP) is a paradigm of programming in which programs are written and structured around objects rather than functions or logic.

Object-Oriented Programming is a methodology of designing a program using classes, objects, [inheritance](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)),[polymorphism](https://en.wikipedia.org/wiki/Polymorphism_(computer_science)), [abstraction](https://en.wikipedia.org/wiki/Abstraction_(software_engineering)) and [encapsulation](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)).


#### Encapsulation
The binding of data and methods into a single unit is called encapsulation. Encapsulation is accomplished when each object inside the class keeps its state private. The data inside this unit is not accessible by outside objects, and only those functions inside this unit are able to access it. Thus, the object manages its state with the help of its methods and communicates with this object; we will require the help of the public methods of this class.

Encapsulation is a process of binding data members (variables, properties) and member functions (methods) into a single unit. It is also a way of restricting access to certain properties or component. The best example for encapsulation is a class.

#### Abstraction

Abstraction is an extension of encapsulation. It means providing only the necessary information to the outside world while hiding the internal details of implementation. It reveals only the appropriate operations for other objects. The advantage of this is that we can change the implementation without affecting the class, as the method interface remains the same.

Let us take the example of a calculator, which takes the input from us, and at the press of a button, gives us the desired output while sparing us the internal details of how it has arrived at that answer.

Abstraction occurs when a programmer hides any irrelevant data about an object or an instantiated class to reduce complexity and help users interact with a program more efficiently. The term abstraction vs encapsulation can be used to describe the process of hiding some of the information contained in an object or class, but it may also refer to the object itself. An abstraction is any named entity that contains a selection of data and behaviors specific to a particular usage of the originating entity.

#### Inheritance 
Inheritance is a mechanism that allows one class to gain the properties of another class, in the same way, that a child inherits some attributes from each of their parents. Inheritance allows programmers to create a new class that reuses the data members and methods of an existing class.

Often, objects are similar in functionality, sharing part of the logic but differing in the rest. So how do we reuse the common logic and separate the different logic? This can be achieved by inheritance. In inheritance, we create a new class called the child class, which is derived from the class called the parent class, thus forming a hier0archy of classes. The child class reuses the data fields and methods required from the parent class and implements its unique functionality on its own.

For example, a vehicle can be a parent class, from which we can derive child classes like Bike and Car. They share the common properties of running on fuel and carrying passengers but differ in the number of passengers they can carry and more such properties.

#### Polymorphism

Polymorphism is the ability to take more than one form. For example, suppose we have a parent class and a few of its child classes. Now we want to use attributes from both the parent and the child classes, so how will it be achieved? This can be done using Polymorphism. In Polymorphism, abstract entities are executed in multiple ways. It gives a way to consume a class exactly like the parent class, such that there is no confusion with mixing the type of classes, and each child class continues to keep its methods the way it was. This can be done by reusing a parent interface so that the child class can implement these methods in their own version.


##### Resume

-    **Abstraction −** It refers to, providing only essential information to the outside world and hiding their background details. For example, a web server hides how it processes data it receives, the end user just hits the endpoints and gets the data back.
-    **Encapsulation −** Encapsulation is a process of binding data members (variables, properties) and member functions (methods) into a single unit. It is also a way of restricting access to certain properties or component. The best example for encapsulation is a class.
-    **Inheritance −** The ability to create a new class from an existing class is called Inheritance. Using inheritance, we can create a Child class from a Parent class such that it inherits the properties and methods of the parent class and can have its own additional properties and methods. For example, if we have a class Vehicle that has properties like Color, Price, etc, we can create 2 classes like Bike and Car from it that have those 2 properties and additional properties that are specialized for them like a car has numberOfWindows while a bike cannot. Same is applicable to methods.
-    **Polymorphism −** The word polymorphism means having many forms. Typically, polymorphism occurs when there is a hierarchy of classes and they are related by inheritance. C++ polymorphism means that a call to a member function will cause a different function to be executed depending on the type of object that invokes the function.

### Classes

 Classes are where we create a blueprint for the structure of methods and attributes. Individual objects are instantiated, or created from this blueprint.
 
In a nutshell, classes are essentially **user defined data types**. 

### Composition
Is a class that references one or more object of another classes in instace variables
A class that contains another class as a variable

Composition implies that a class cannot exist independely of the container

Example: `book = Book(Page())`

if we destroy the book instance the page instace is also destroyed

### Aggregation
The child can exist independetly of the parent, if we destroy car, engine still exits.
`engine = Engine()
car = Car(engine)`

Agregation and composition are both an associaton relationship
 
 ### What is the difference between a constructor and a method?
 
 The name of the constructor is same as that of the class name, whereas the name of the method can be anything.
 
 When you make an object of a class, then the constructor of that class will be called automatically. But for methods, we need to call it explicitely.
 
 would be the same as calling init{} and defining the variables in the primary consturcotr in kotlin
 
 ### Differences between abstract classes and interfaces
    
An abstract class, is a class that contains both concrete and abstract methods (methods without implementations). An abstract method must be implemented by the abstract class sub-classes. Abstract classes cannot be instantiated and need to be extended to be used.

An interface is like a blueprint/contract of a class (or it may be thought of as a class with methods, but without their implementation). It contains empty methods that represent, what all of its subclasses should have in common. The subclasses provide the implementation for each of these methods. Interfaces are implemented.

**Type of variables:** Abstract class can have final, non-final, static and non-static variables. The interface has only static and final variables.

**Implementation:** Abstract class can provide the implementation of the interface. Interface can’t provide the implementation of an abstract class.

**Multiple implementations:** An interface can extend another Java interface only, an abstract class can extend another Java class and implement multiple Java interfaces.


### Method overriding vs overloading

Overlading means having the same method name with diferent parameter

Overrider means having same methid name with same parameter

Static methods can be overloaded which means a class can have more than one static method of same name. Static methods cannot be overridden, even if you declare a same static method in child class it has nothing to do with the same method of parent class as overridden static methods are chosen by the reference class and not by the class of the object.

The most basic difference is that overloading is being done in the same class while for overriding base and child classes are required. Overriding is all about giving a specific implementation to the inherited method of parent class.

###  What are the access modifiers you know? What does each one do?
    
  There are four access modifiers in Java language (from strictest to the most lenient):
     
   1.  `private` _variables_, _methods_, _constructors_ or _inner classes_ are only visible to its' containing class and its' methods. This modifier is most commonly used, for example, to allow variable access only through getters and setters or to hide underlying implementation of classes that should not be used by user and therefore maintain encapsulation. Singleton constructor is also marked `private` to avoid unwanted instantiation from outside.
   
   2.  `Default` (no keyword is used) this modifier can be applied to _classes_, _variables_, _constructors_ and _methods_ and allows access from classes and methods inside the same package.
    3.  `protected` can be used on _variables_, _methods_ and _constructors_ therefore allowing access only to subclasses and classes that are inside the same package as protected members' class.
    4.  `public` modifier is widely-used on _classes_, _variables_, _constructors_ and _methods_ to grant access from any class and method anywhere. It should not be used everywhere as it implies that data marked with `public` is not sensitive and can not be used to harm the program.

### Desing patterns
So, it is basically a pattern that can be followed to solve a particular feature. These are the best practices that can be used by any programmer to build an application.

Design Patterns are reusable solutions to common software problems. App Architectures provide solutions to an app’s data flow or extensibility issues.

-   _Creational patterns_: How you _create_ objects.
For handling object creating.

-   _Structural patterns_: How you _compose_ objects.
For identifying ways to realize relations between objects
**Structural design patterns** are concerned with how classes and objects can be composed, to form larger structures.

The structural design patterns **simplifies the structure by identifying the relationships**.

-   _Behavioral patterns_: How you _coordinate_ object interactions.
For habdling communication between different objects

Design patterns usually deal with objects. They present a solution to a reoccurring problem that an object shows and help eradicate design-specific problems. In other words, they represent challenges, other developers already faced and prevent you from reinventing the wheel by showing you proven ways to solve those problems.

_Creational Patterns_

-   Builder
-   Dependency Injection
-   Singleton
-   Factory

_Structural Patterns_

-   Adapter
-   Facade
-   Decorator
-   Composite

_Behavioral Patterns_

-   Command
-   Observer
-   Strategy
-   State

#### Creational Patterns
The Creational Pattern is used to create some object without showing the logic or the steps that are involved in creating the object. So, every time you want an object, **you need not instantiate the object by using the new operator**.

_“When I need a particularly complex object, how do I get an instance of it?” – Future You_

Future You hopes the answer isn’t “_Just copy and paste the same code every time you need an instance of this object_“. Instead, _Creational_ patterns make object instantiation straightforward and repeatable.

##### Builder
In a builder pattern, you are only concerned about what you need from a class and not everything that a class has.

 The _Builder_ pattern simplifies the creation of objects from its representation.
 
 Example: 
 ```kotlin
 AlertDialog.Builder(this)
    .setTitle("Hey")
    .setContent("Message") // we could use this or not
    .show()
 ```
 
 This builder proceeds step-by-step and lets you specify only the parts of `AlertDialog` that you need to specify.
 
##### Dependency Injection
In the Dependency Injection pattern, we provide the dependency of a class from outside the class and no dependency will be provided in the same class.

In software terms, dependency injection has you provide any required objects to instantiate a new object. This new object doesn’t need to construct or customize the objects themselves.

For example using Hilt:

```kotlin
//In the module
@Provides
fun provideCar() = Car()
  
//Somewhere in the app
@Inject lateinit var car: Car
```

##### Singleton 
This pattern restrics the instantiation of a class to one single instance. meaning we only have one instance of that class across the system.

The _Singleton_ pattern specifies that only a single instance of a class should exist with a global access point. This pattern works well when modeling real-world objects with only one instance. For example, if you have an object that makes network or database connections, having more than one instance of the project may cause problems and mix data. That’s why in some scenarios you want to restrict the creation of more than one instance.

The Kotlin `object` keyword declares a singleton without needing to specify a static instance like in other languages.

Or with the `@Singleton` in Dagger-Hilt

##### Factory 
This pattern uses factory methods to deal with the problem of [creating objects](https://en.wikipedia.org/wiki/Object_creation "Object creation") without having to specify the exact [class](https://en.wikipedia.org/wiki/Class_(computer_programming) "Class (computer programming)") of the object that will be created.

As the name suggests, _Factory_ takes care of all the object creational logic. In this pattern, a factory class controls which object to instantiate. Factory pattern comes in handy when dealing with many common objects. You can use it where you might not want to specify a concrete class.

Used for example:
```kotlin
sealed class Review{
    class Positive(): Review()
    class Negative(): Review()
    
    companion object Factory{
        fun from(score: Int): Review{
            return if(score >= 0) Review.Positive()
            else Review.Negative()
        }
    }
}

val review = Review.Factory.from(5) // Review.Postitive
```

#### Structural patterns
_“So, when I open this class, how will I remember what’s it doing and how it’s put together?” – Future You_

Future You will undoubtedly appreciate the Structural Patterns you used to organize the guts of your classes and objects into familiar arrangements that perform typical tasks. _Adapter_ and _Facade_ are two commonly-seen patterns in Android.

##### Adapter 
An Adapter is something like a connector that is used to connect two or more incompatible interface. This pattern lets the classes work together.

In software terms, this pattern lets two incompatible classes work together by converting a class’s interface into the interface the client expects.

For example using an Adapter to map a list of Models to a RecyclerView, to bind the data in the ViewHolder and inflate the layout.

Adapter pattern lets two incompatible classes to work with each other without the need to modify both their source codes. This is done by converting the interface of one class into an interface expected by the clients.

In Android, it uses a lot of adapter pattern when it comes to handling ListView or RecyclerView data. In the example below, MovieAdapter does not know what is Movie, but it simply handles the data and sends the configuration to the correct ViewHolder to display.

##### Facade 
"The Facade Pattern provides a unified interface to a set of interfaces in a subsytem. Facade defines a higher level interface that makes the subsystem easier to use."

_The Facade pattern simplifies and hides the complexity of large code blocks or APIs, providing a cleaner, understandable and easy of use interface._

In the Facade pattern, a complicated system is wrapped into a simpler system that will help us in getting the values from the complicated system without having knowledge of how the data is being fetched and returned to the view or the presenter

 Hides the complexities of the system and provides an interface to the client using which the client can access the system.
 
 The _Facade_ pattern provides a higher-level interface that makes a set of other interfaces easier to use.
 
Example:
Basically an interface/ class / method that runs another methods.

```kotlin
car.start()
phone.off()
garage.open()

//Insted of that we create a class that does all of this for us.
class TravelFacade(car: Car, phone: Phone, garage: Garage){
    fun start(){
        car.start()
        phone.off()
        garage.open()
    }
}
```


Retrofic
 
 ```kotlin
 interface BooksApi {
  @GET("books")
  fun listBooks(): Call<List<Book>>
}
 
val retrofit = Retrofit.Builder()
  .baseUrl("http://www.myexampleurl.com")
  .addConverterFactory(GsonConverterFactory.create())
  .build()

val api = retrofit.create<BooksApi>(BooksApi::class.java)
 ```
 
The client needs to call `listBooks()` to receive a list of `Book` objects in the callback. It’s nice and clean.
 
This lets you make all types of customizations underneath without affecting the client. For example, you can specify a customized JSON deserializer that the Activity has no clue about.

Notice the use of `GsonConverterFactory`, working behind the scenes as a JSON deserializer. With Retrofit, you can further customize operations with `Interceptor` and `OkHttpClient` to control caching and logging behavior without the client knowing what’s going on.

The less each object knows about what’s going on behind the scenes, the easier it’ll be for Future You to manage changes in the app.

##### Decorator
The _Decorator_ pattern dynamically attaches additional responsibilities to an object to extended its functionality at runtime.

```kotlin
//1
interface Salad {
  fun getIngredient(): String
}

//2
class PlainSalad : Salad {
  override fun getIngredient(): String {
    return "Arugula & Lettuce"
  }
}

//3
open class SaladDecorator(protected var salad: Salad) : Salad {
  override fun getIngredient(): String {
    return salad.getIngredient()
  }
}

//4
class Cucumber(salad: Salad) : SaladDecorator(salad) {
  override fun getIngredient(): String {
    return salad.getIngredient() + ", Cucumber"
  }
}

//5
class Carrot(salad: Salad) : SaladDecorator(salad) {
  override fun getIngredient(): String {
    return salad.getIngredient() + ", Carrot"
  }
}


val cucumberSalad = Cucumber(Carrot(PlainSalad()))
print(cucumberSalad.getIngredient()) // Arugula & Lettuce, Carrot, Cucumber
val carrotSalad = Carrot(PlainSalad())
print(carrotSalad.getIngredient()) // Arugula & Lettuce, Carrot
```

##### Composite

You use the _Composite_ pattern when you want to represent a tree-like structure consisting of uniform objects. A Composite pattern can have two types of objects: composite and leaf. A composite object can have further objects, whereas a leaf object is the last object.

```kotlin
//1
interface Entity {
  fun getEntityName(): String
}

//2
class Team(private val name: String) : Entity {
  override fun getEntityName(): String {
    return name
  }
}

//3
class Raywenderlich(private val name: String) : Entity {
  private val teamList = arrayListOf<Entity>()

  override fun getEntityName(): String {
    return name + ", " + teamList.map { it.getEntityName() }.joinToString(", ")
  }

  fun addTeamMember(member: Entity) {
    teamList.add(member)
  }
}

val composite = Raywenderlich("Ray")
val ericTeamComposite = Raywenderlich("Eric")
val aaqib = Team("Aaqib")
val vijay = Team("Vijay")
ericTeamComposite.addTeamMember(aaqib)
ericTeamComposite.addTeamMember(vijay)
composite.addTeamMember(ericTeamComposite)
print(composite.getEntityName()) // Ray, Eric, Aaqib, Vijay
```


#### Behavioural patterns
 _“So… how do I tell which class is responsible for what?” – Future You_

_Behavioral_ Patterns let you assign responsibility for different app functions. Future You can use them to navigate the project’s structure and architecture.

These patterns can vary in scope, from the relationship between two objects to your app’s entire architecture. Often, developers use several behavioral patterns together in the same app.
##### Observer 
The _Observer_ pattern defines a one-to-many dependency between objects. When one object changes state, its dependents get a notification and updates automatically.

LiveData is one example, one live data can have multiple observers.

#####  Command 
In the Command pattern, we give commands and we want our output and nothing else. We are not bothered about who will do our operation to give the desired result. All we want is our things to be done at the right time.

Similarly, the _Command_ pattern lets you issue requests without knowing the receiver. You encapsulate a request as an object and send it off. Deciding how to complete the request is an entirely separate mechanism.

EventBuss is one example of this.

This would be a Navigation Example.
```kotlin
sealed class NavigationCommand {
  data class To(val directions: NavDirections): NavigationCommand()
  object Back: NavigationCommand()
  data class BackTo(val destinationId: Int): NavigationCommand()
  object ToRoot: NavigationCommand()
}
```

##### Strategy
You use a _Strategy_ pattern when you have multiple objects of the same nature with different functionalities. For a better understanding, take a look at the following code:

```kotlin
// 1
interface TransportTypeStrategy {
  fun travelMode(): String
}

// 2
class Car : TransportTypeStrategy {
  override fun travelMode(): String {
    return "Road"
  }
}

class Ship : TransportTypeStrategy {
  override fun travelMode(): String {
    return "Sea"
  }
}

class Aeroplane : TransportTypeStrategy {
  override fun travelMode(): String {
    return "Air"
  }
}

// 3
class TravellingClient(var strategy: TransportTypeStrategy) {
  fun update(strategy: TransportTypeStrategy) {
    this.strategy = strategy
  }

  fun howToTravel(): String {
    return "Travel by ${strategy.travelMode()}"
  }
}
```

##### State
In the _State_ pattern, the state of an object alters its behavior accordingly when the internal state of the object changes.

```kotlin
// 1
interface PrinterState {
  fun print()
}

// 2
class Ready : PrinterState {
  override fun print() {
    print("Printed Successfully.")
  }
}

// 3
class NoInk : PrinterState {
  override fun print() {
    print("Printer doesn't have ink.")
  }
}

class Printer(){
    var ink = 2

    fun startPrinting(){
        //check if ink is > 0
        //print result
    }
    
    fun installInk(){
        ink += 2
    }
}

val printing = Printer()
printing.startPrinting() // Printed Successfully.
printing.startPrinting() // Printed Successfully.
printing.startPrinting() // Printer doesn't have ink.
printing.installInk() // Ink installed.
printing.startPrinting() // Printed Successfully.
```

So, you create an object of the class `Printer` to print. The `Printer` class handles all the states of the printer internally. It’s either on a `Ready` state or in a `NoInk` state.

##### App architecture

_“Could there ever be a requirement where I’ll have to modify or implement new features in this project?” – Future You_

App architectures play a vital part in structuring a loosely coupled codebase. You can use it anywhere, irrespective of the platform. App architectures help you write easily testable, extensible and decoupled code.

In simple terms, Architecture refers to the overall organization of your code in things like:

1.  Responsibilities for each class
2.  Folder organization
3.  Structure of the code: network calls, responses, errors.

The App Architectures used to create solid and maintainable codebases are many.

Like MVVM, MVP, MVC, MVI

### Architecture
_“Could there ever be a requirement where I’ll have to modify or implement new features in this project?” – Future You_

App architectures play a vital part in structuring a loosely coupled codebase. You can use it anywhere, irrespective of the platform. App architectures help you write easily testable, extensible and decoupled code.

In simple terms, Architecture refers to the overall organization of your code in things like:

1.  Responsibilities for each class
2.  Folder organization
3.  Structure of the code: network calls, responses, errors.

The App Architectures used to create solid and maintainable codebases are many.

Goals?
 - Scalable: Add new features quickly
 - Maintable: No spaghetti code
 - Testing: Easy to mock

Why?
 - Easier to add new features
 - Easier to understand
 - Easier to police
 - Make our life easier
 - Make Unit Testing easier

Like MVVM, MVP, MVC, MVI

## MVC vs MVP vs MVVM

#### In MVC:
View: XML
Controller: Activity / Fragment
Model: Data
The user input is done in the Controller

#### In MVP:
View: Activity / Fragment
Presenter: Gateway between model and view
Model: Data

We use interfaces to connect the view to the Presenter and the presenter to the Model
The user input is done in the View.

#### In MVVM:
View: Activity / Fragment
ViewModel: Connects the view and the model
Model: Data
We dont use interfaces for the view - viewModel, we use DataBinding and observers pattern.

---

#### MVP

##### Presenter

It is a gateway between model and view as they do not interact each other directly. Every data passes through this gateway. It updates the view by taking the data from the model and update the model with data provided by the view.

Base of the presenter also have a minimum of two parts, among them first is MvpPresenter as interface and second is BasePresenter as class implementing this interface. It’s base part can also be divided into various parts as per the use case.

##### Model

It handles the data part of the application. It does not interact directly with the view. It provides data to Presenter, and presenter forwards data to the view and intake data from presenter which is provided by the view. Model is not even aware of view and vice versa.

Model is divided into various parts, at center we have datamanager which is the single part of the model with which the presenter interacts, then datamanager on further interacts with other components of the model.

#### MVC
**Controller** – Controller can be imagined as an extension or a personal assistant to the view, all the events originated from the view is handled by the controller. Controller will also inform the Model on behalf of view that some event happened on the view and some new data might be required.

Normally the controller is the activity/ fragment, thats why they grow so big.

### MVC vs MVP
I'm MVC the controller is the fragment/ activity

In MVP the view tell the controller what happend, the contoller tell the model and the model tells the view

In MVP view is dumb, in mvc the view can talk with the model directly

In MVC, the view is updated only by the model (by listening to its events). It is never updated by the controller. This is problematic when you need to format model data for the view, hence the need for MVP.

In MVP-Passive View, the view is updated only by presenter (presenter sets view properties). The presenter listens to events on the model [modifying the data if required] prior to updating the view.

In MVP-Supervising Controller, the view is updated by either the model or the presenter. If no formatting is required, the view updates itself via the model. If formatting is required, it updates itself via the presenter.

---

As you can see, these architectural patterns are very similar. The key differences are:

1. In MVC, the view gets notified of any change in model’s state by the model itself. In MVP, the view knows nothing about the model, and it becomes presenter’s job to fetch the up to date data from the model, understand whether the view should be updated and bind a new data to the view.
2. Views in MVC tend to have more logic in them because they are responsible for handling notifications from the model. In MVP, the same logic is located in the presenter, which makes the views very “dumb” – their sole purpose becomes rendering of the data that was bound to them by the presenter and capturing user input.

---

-   The component that encapsulates domain logic and stores system’s domain state (whether persistent or not). That’s a Model.
-   The component that handles input-output from/to the user. That’s a View.
-   The component that controls user’s navigation within the app, processes user input and acts upon changes in domain state. That’s Controller/Presenter.

### MVVM
This unfortunately-quite-confusingly-named presentation architectural pattern is similar to the MVC pattern. The Model and View components are the same.

The ViewModel object is the _glue_ between the model and view layers but operates differently than the Controller component. Instead, it exposes commands for the view and binds the view to the model. When the model updates, the corresponding views update via the data binding.

Similarly, as the user interacts with the view, the bindings work in the opposite direction to automatically update the model.

### Clean architecture
_Clean Architecture_ is not in itself an architecture but a concept. It describes the overall app architecture: how the various layers of an app, business objects, use cases, presenters, data storage and UI, communicate with one another. MVC and MVVM exist within Clean Architecture at the outer presentation and UI layers.

The following are good pointers that I received from that book :

-   **Writing clean code** is what you must do in order to call yourself a professional. There is no reasonable excuse for doing anything less than your best.
-   It is not the language that makes programs appear simple. It is the programmer that make the language appear simple!
-   **Single Responsibility Principle :** It states that every module or class should have responsibility over a single part of the functionality provided by the software, and that responsibility should be entirely encapsulated by the class. All its services should be narrowly aligned with that responsibility. [Robert C. Martin](https://en.wikipedia.org/wiki/Robert_C._Martin)(Author of the book) expresses the principle as: ** _A class should have only one reason to change._**

-   **Say what you mean. Mean what you say :** Your function name should follow this rule.
-   **Open Closed Principle :** In object-oriented programming, the open/closed principle states that the software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification, that is, such an entity can allow its behaviour to be extended without modifying its source code.
-   **Use Descriptive Names :** Remember Ward’s principle: “You know you are working on clean code when each routine turns out to be pretty much what you expected.” Half the battle to achieving that principle is choosing good names for small functions that do one thing. The smaller and more focused a function is, the easier it is to choose a descriptive name.
-   **DRY(Don’t Repeat Yourself) :** The duplication is a problem because it bloats the code and will require four-fold modification when the algorithm need to be changed. It is also a four-fold opportunity for an error of omission. Duplication may be the root of all evil in software. Many principles and practices have been created for the purpose of controlling or eliminating it.
-   **Writing software is like any other kind of writing :** When you write a paper or an article, you get your thoughts down first, then you massage it until it reads well. The first draft might be clumsy and disorganized, so you wordsmith it and restructure it and refine it until it reads the way you want it to read.
-   **Use Exceptions Rather Than Return Codes :** The problem with Return-Code approaches is that they clutter the caller. The caller must check for errors immediately after the call. Unfortunately, it’s easy to forget. For this reason it is better to throw an exception when you encounter an error. The calling code is cleaner. Its logic is not obscured by error handling.
-   **Always Provide Context with Exceptions :** Each exception that you throw should provide enough context to determine the source and location of an error. In Java, you can get a stack trace from any exception; however, a stack trace can’t tell you the intent of the operation that failed. Create informative error messages and pass them along with your exceptions. Mention the operation that failed and the type of failure. If you are logging in your application, pass along enough information to be able to log the error in your catch.

### Array , Arraylist and List

  - arrays are always mutable
  - list is not, mutablelist is 
  - arrays are fixed size as list
  - mutabelist and arraylist are not
  - cant use generics with arrays, we can with list() ?? maybe?? mutablelist cant use generics ???? cehck this
  
 ### Generics in java
Generics were included in Java language to provide stronger type checks, by allowing the programmer to define, which classes can be used with other classes
 ` List<Integer> list = new ArrayList<>();`
    
###  What is Java PriorityQueue?
In Priority Queue, each element is having some priority and all the elements are present in a queue. The operations are performed based on the priority.

### Strings
There is no primitive variant of `String` class in Java language - all strings are just wrappers around underlying array of characters, which is declared `final`. This means that, once a `String` object is instantiated

`String` was made immutable to prevent malicious manipulation of data, when, for example, user login or other sensitive data is being send to a server.

**What does it means to say that a `String` is immutable?**

It means that once created, `String` object's `char[]` (its' containing value) is declared `final` and, therefore, it can not be changed during runtime.

#### string.intern()
The method intern () creates an exact copy of a String object in the heap memory and stores it in the String constant pool. Note that, if another String with the same contents exists in the String constant pool, then a new object won't be created and the new reference will point to the other String.

### List some primitives in java
-   `byte`
-   `short`
-   `int`
-   `long`
-   `float`
-   `double`
-   `char`
-   `String`
-   `boolean`

### Difference Integer and Int
`int` is a primitive data type (with `boolean`, `byte`, `char`, `short`, `long`, `float` and `double`), while `Integer` (with `Boolean`, `Byte`, `Character`, `Short`,`Long`, `Float` and `Double`) is a [wrapper](https://docs.oracle.com/javase/tutorial/java/data/numberclasses.html) class that encapsulates primitive data type, while providing useful methods to perform different tasks with it.

**What is Autoboxing and Unboxing?**
    
Autoboxing and Unboxing is the process of automatic wrapping (putting in a box) and unwrapping (getting the value out) of primitive data types, that have "wrapper" classes. So `int` and `Integer` can (almost always) be used interchangeably in Java language, meaning a method `void giveMeInt(int i) { ... }` can take `int` as well as `Integer` as a parameter.

### Typecast in Java
n Java, you can use casts to polymorph one class into another, compatible one. For example:

    long i = 10l;
    int j = (int) i;
    long k = j;
    
 ### Do objects get passed by reference or value in Java?

In Java all primitives and objects are passed by value, meaning that their copy will be manipulated in the receiving method. But there is a caveat - when you pass an object reference into a method, a _copy of this reference_ is made, so it still points to the same object. This means, that any changes that you make to the insides of this object are retained, when the method exits.

### Initialize and Instantiate / Creating object in java

when we create a class `new Dog("doggie")` we instantiate the class with the `new` keyword, by alocating memory for a new object and returning a reference to that memory.

inside the class, we initialize the class/ variables
```java
class Dog{
    string name; 
    public Dog(string dogName){
        name = dogName
    }
}
```

### References
- [SoftReference](https://docs.oracle.com/javase/8/docs/api/java/lang/ref/SoftReference.html): Soft reference objects are cleared at the discretion of the garbage collector in response to memory demand. Soft references are most often used to implement memory-sensitive caches. All soft references to softly reachable objects are guaranteed to have been cleared before the virtual machine throws an `OutOfMemoryError`.

**SoftReferences** can be used to implement a cache that can grow without risking an application crash. To do this, you need to implement a Map interface in which **values** are stored, wrapped inside a SoftReference. SoftReferences will keep the objects alive until there is memory available on the heap, but it will discard them before an OutOfMemoryError.

- **[WeakReference](https://docs.oracle.com/javase/8/docs/api/java/lang/ref/WeakReference.html)**: Weak reference objects do not prevent their referents from being made finalizable, finalized, and then reclaimed. Weak references are most often used to implement canonicalizing mappings. (Here, Canonicalizing mappings means mapping only reachable object instances.)

**WeakReferences** can be used, for example, to store some information related to an object until the object gets finalized. To do this, you can implement a Map in which the **keys** are wrapped in a WeakReference. As soon as GC reclaims the key object, you can remove the value as well.

- **[PhantomReference](https://docs.oracle.com/javase/8/docs/api/java/lang/ref/PhantomReference.html)**: Phantom reference objects are enqueued after the collector determines that their referents may otherwise be reclaimed. Phantom references are most often used for scheduling pre-mortem cleanup actions in a more flexible way than is possible with the Java finalization mechanism. Unlike soft and weak references, phantom references are not automatically cleared by the garbage collector as they are enqueued. An object that is reachable via phantom references will remain so until all such references are cleared or themselves become unreachable.

can be used to notify you when some object is out of scope to do some resource cleanup. Remember that the object.finalize() method is not guaranteed to be called at the end of the life of an object, so if you need to close files or free resources, you can rely on Phantom. Since Phantom doesn't have a link to the actual object, a typical pattern is to derive your own Reference type from Phantom and add some info useful for the final freeing, for example filename.

### What is the difference between using `==` and `.equals` on an object?

 - `==` compares memory adress
 - `equals` check content and can be overrided

 - In kotlin `==` is the same as equals 
 - `===` is the same as `==` in java

### What are these `final`, `finally` and `finalize` keywords?

`final` is a keyword in the java language. It is used to apply restrictions on class, method and variable. Final class can't be inherited, final method can't be overridden and final variable value can't be changed.

`finally` is a code block and is used to place important code, it will be executed whether exception is handled or not.

`Finalize` is a method used to perform clean up processing just before object is garbage collected.

### What is the difference between "throw" and "throws" keyword in Java?
`throws` is just used to indicated which exception is to be thrown. But the `throw` keyword is used to throw some exception from any static block or any method.

### DSL domain specific language 
In general human terms, DSL provides you a flexible tool of any specific language to leverage the power provided by the specific programming language.

`forEach` is a DSL

### High order functions
A higher-order function is a function that takes functions as parameters or returns a function.

### const vs val
The `const` keyword is used to declare those properties which are immutable in nature i.e. these properties are read-only properties.

 - we know this at compile time
 - `vals` can be created in runtime

### Check if latini is initialized
`this::latinit::isInitialized`

### Companion object

In Kotlin, if you want to write a function or any member of the class that can be called without having the instance of the class then you can write the same as a member of a **companion** object inside the class. So, by declaring the **companion** object, you can access the members of the class by class name only(which is without explicitly creating the instance of the class).

### Visibility

- Private is only available for that class / file
- Protected is visible inside that file and also in the subclass of that class
- Public, visible for everyon, by default is like this
- Internal, visible in the same module, by module, we mean agroup of file that are compile together

### pair, triple
class in koltin that is used to store 2,3 variables of the same type
provide method like first,second


### lazy vs lateinit
lateinit is mutable, lazy is not
lazy has a cache and wont be initialized unles we call it

### inline
Inline function instruct compiler to insert complete body of the function wherever that function got used in the code.

Advantages of inline function are as follows:

-   **Function** call overhead doesn't occur.
-   It also saves the overhead of push/pop variables on the stack when the **function** is called.
-   It also saves the overhead of a return call from a **function**. Such optimizations are not possible for normal **function** calls.

### no inline
if we have a function with 2 lambdas , we can inline the function, and declare no inlince if we dont want to inline a lambda
inline fun dostuff(a:()-> Unit, noinline b: ()-> Unit)

### crossline
if a function contains a inline faunction and does operations
if we return inside the lambda, the fcuntion will stop
if we use crossline it wont allow us to return from there
This is how the **crossinline** can help us to avoid the "non-local returns".

###  Why Sealed Class over Enum?

Sealed classes give us the flexibility of having **different** **types of subclasses and also containing the state**. The important point to be noted here is the subclasses that are extending the Sealed classes should be either nested classes of the Sealed class or should be declared in the same file as that of the Sealed class. 

### String vs StringBuffer

Since String is immutable in Java, whenever we do String manipulation like concatenation, substring, etc. it generates a new String and discards the older String for garbage collection.

These are heavy operations and generate a lot of garbage in heap. So Java has provided StringBuffer and StringBuilder classes that should be used for String manipulation.

StringBuffer and StringBuilder are mutable objects in Java. They provide append(), insert(), delete(), and substring(), reverse, methods for String manipulation.

### StringBuffer vs StringBuilder

StringBuffer was the only choice for String manipulation until Java 1.4. But, it has one disadvantage that all of its public methods are synchronized. StringBuffer provides Thread safety but at a performance cost.

In most of the scenarios, we don’t use String in a multithreaded environment. So Java 1.5 introduced a new class StringBuilder, which is similar to StringBuffer except for thread-safety and synchronization.

StringBuffer has some extra methods such as substring, length, capacity, trimToSize, etc. However, these are not required since you have all these present in String too. That’s why these methods were never implemented in the StringBuilder class.

StringBuffer was introduced in Java 1.0 whereas StringBuilder class was introduced in Java 1.5 after looking at shortcomings of StringBuffer.

If you are in a single-threaded environment or don’t care about thread safety, you should use StringBuilder. Otherwise, use StringBuffer for thread-safe operations.


### What is an Algorithm?

In computer science, whenever we want to solve some computational problem then we define a set of steps that need to be followed to solve that problem. These steps are collectively known as an algorithm.

#### What do you mean by a good Algorithm?
-   **Correctness:** An algorithm is said to be correct if for every set of input it halts with the correct output. If you are not getting the correct output for any particular set of input, then your algorithm is wrong.
-   **Finiteness:** Generally, people ignore this but it is one of the important factors in algorithm evaluation. The algorithm must always terminate after a finite number of steps. For example, in the case of recursion and loop, your algorithm should terminate otherwise you will end up having a stack overflow and infinite loop scenario respectively.
-   **Efficiency:** An efficient algorithm is always used. By the term efficiency, we mean to say that:

1. The algorithm should efficiently use the resources available to the system.
2.  The computational time (the time taken to generate an output corresponding to a particular input) should be as less as possible.
3.  The memory used by the algorithm should also be as less as possible. Generally, there is a trade-off between computational time and memory. So, we need to find if the time is more important than space or vice-versa and then write the algorithm accordingly.

#### Algorithm Efficiency

The efficiency of an algorithm is mainly defined by two factors i.e. space and time. A good algorithm is one that is taking less time and less space, but this is not possible all the time. There is a trade-off between time and space. If you want to reduce the time, then space might increase. Similarly, if you want to reduce the space, then the time may increase. So, you have to compromise with either space or time. Let's learn more about space and time complexity of algorithms.

#### Space Complexity

Space Complexity of an algorithm denotes the total space used or needed by the algorithm for its working, for various input size

for an array of size n the space complexity would be n

#### Time Complexity

The time complexity is the number of operations an algorithm performs to complete its task with respect to **input size** (considering that each operation takes the same amount of time)


#### **_Bubble Sort:_**

 _Bubble sort is a comparison-based algorithm that compares each pair of elements in an array and swaps them if they are out of order until the entire array is sorted. For each element in the list, the algorithm compares every pair of elements._
 
 goes one by one and check withthe next one, if it is smllaer/ bigger it swap places, keep doing for every elemtn
 
 #### _Selection Sort:_** n*n

 _Selection sort is an in-place comparison-based algorithm that divided the list into two parts, the sorted part at the left end and the unsorted part at the right end. Initially, the sorted part is empty and the unsorted part is the entire list.  
 The smallest element is selected from the unsorted array and swapped with the leftmost element, and that element becomes a part of the sorted array. This process continues moving unsorted array boundary by one element to the right._
 
 goies one by one and checks the whole list to see if it winds a smaller/bigger value, if it does it swap it
 

#### **_Insertion Sort:_**

 _Insertion sort is a comparison-based algorithm that builds a final sorted array one element at a time. It iterates through an input array and removes one element per iteration, finds the place the element belongs in the array, and then places it there._
 
 check the next value to sort, if it finds one it will go back and start swaping value to mach the new value
 and stop until this isnt true anymore

#### _Heap Sort:_**

 _Heap sort is a comparison-based algorithm that uses a binary heap data structure to sort elements. It divides its input into a sorted and an unsorted region, and it iteratively shrinks the unsorted region by extracting the largest element and moving that to the sorted region._
 
 
#### **_Quick Sort:_**

 _Quick sort is a comparison-based algorithm that uses divide-and-conquer to sort an array. The algorithm picks a pivot element, A[q] and then rearranges the array into two subarrays A[p . . . . q-1] , such that all elements are less than A[q] and A[q+1 . . . r] , such that all elements are greater than or equal to A[q]._
 
 ### Why use kotlin
 concise
 type safe
 is interoperable, we can call the java code from kotlin and kotlin from the java
 adopted by google as native from android
 
 ### Solid principles
 These principles establish practices that lend to developing software with considerations for maintaining and extending as the project grows. Adopting these practices can also contribute to avoiding code smells, refactoring code, and Agile or Adaptive software development.
 
 #### Single responsability principle
This principle states that “_a class should have only one reason to change_” which means every class should have a single responsibility or single job or single purpose
 
 #### Open / closed principle
 This principle states that “_software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification_” which means you should be able to extend a class behavior, without modifying it.  
Suppose developer A needs to release an update for a library or framework and developer B wants some modification or add some feature on that then developer B is allowed to extend the existing class created by developer A but developer B is not supposed to modify the class directly. Using this principle separates the existing code from the modified code so it provides better stability, maintainability and minimizes changes as in your code.

 #### Liskov subtituion principle
 This principle ensures that any class that is the child of a parent class should be usable in place of its parent without any unexpected behavior.
 
 Meaning if we override the methond from the parent maybe we are doing something wrong and maybe it is not a child
 
 Example: if a human has a child, it should be a child not a duck
 
#### Interface segration principle
Here your main goal is to focus on avoiding fat interface and give preference to many small client-specific interfaces. You should prefer many client interfaces rather than one general interface and each interface should have a specific responsibility.

#### Dependency inversion princible
-   High-level modules/classes should not depend on low-level modules/classes. Both should depend upon abstractions.
-   Abstractions should not depend upon details. Details should depend upon abstractions.

The above lines simply state that if a high module or class will be dependent more on low-level modules or class then your code would have tight coupling and if you will try to make a change in one class it can break another class which is risky at the production level. So always try to make classes loosely coupled as much as you can and you can achieve this through _abstraction_. The main motive of this principle is decoupling the dependencies so if class A changes the class B doesn’t need to care or know about the changes.

```kotlin
//this violtes the principle
class A{
    fun connect(){
    //...
    }
}

class B(a: A) {
    
}
```


```kotlin
//we should do this
interface DoStuff{
    fun connect()
}

class A: DoStuff{
    override fun connect(){
    //...
    }
}

class B(do: doStuff) {
    
}
```

### Agile
Rather, Agile is a mindset that drives an approach to software development. As there is no single approach that works for all situations, the term _Agile_ has come to represent a variety of methods and practices that align with the value statements in the manifesto.

Agile methods (often called frameworks) are comprehensive approaches to phases of DevOps lifecycle:  planning, development, delivery, and operations. They prescribe a method for accomplishing work, with clear guidance and principles.

Agile is a collection of principles used in software development and project management. Agile focuses on enabling teams to deliver work in small, workable increments, thus delivering value to their customers with ease. Evaluation of the requirements, plans, and results take place continuously. This helps the team in responding to changes in a quick manner.

 - Individuals and Interactions OVER Process and Tools

 - Working Products OVER Comprehensive Documentation

  - Customer Collaboration OVER Contract Negotiation

 - Responding to Changes OVER Following a Plan

### Scrum
It is a framework used by teams to establish a hypothesis, test it, reflect on the experience, and make adjustments. It enables teams to incorporate practices from other frameworks depending on the requirements. It is used by cross-functional teams that are working on product development, and the work is split into more than one 2-4 week iterations.

In Scrum, you divide your project team into smaller Scrum teams of 3–11 members that have to self-organize and work in Scrum sprints that last from one to four weeks. The team includes the Project Owner representing the business side and the Scrum Master responsible for minimizing roadblocks.

Before every sprint, the Scrum team should review their product backlog that serves as an in-depth project plan replacement listing all the features that a final product needs. After that, they prioritize a few features to work on in each iteration. So, as you see, each sprint ends up with a user test of the new product version. After the sprint is finished, there is a team meeting organized to discuss possible improvements that can be made in further sprints.

#### Product owner

Responsible for what the team is building, and why they're building it. The product owner is responsible for keeping the backlog up-to-date and in priority order.

#### Scrum master

Responsible to ensure the scrum process is followed by the team. Scrum masters are continually on the lookout for how the team can improve, while also resolving impediments and other blocking issues that arise during the sprint. Scrum masters are part coach, part team member, and part cheerleader.

#### Scrum team

These are the individuals that actually build the product. The team owns the engineering of the product, and the quality that goes with it.

#### Product backlog

The _product backlog_ is a prioritized list of value the team can deliver. The product owner is responsible for the backlog and adds, changes, and reprioritizes as needed. The items at the top of the backlog should always be ready for the team to execute on.

#### Sprint planning and the sprint backlog

In sprint planning, the team chooses the backlog items they will work on in the upcoming sprint. The team chooses backlog items based on priority and what they believe they can complete in the sprint. The _sprint backlog_ is the list of items the team plans to deliver in the sprint. Often, each item on the sprint backlog is broken down into tasks. Once all members agree the sprint backlog is achievable, the sprint starts.

### Kanbam

It is a method that’s used to design, manage, and improve the flow of systems. Kanban enables organizations to visualize their flow of work and limit the amount of work in progress. It is used in situations where work arrives unpredictably, and where it needs to be deployed immediately without waiting for other work items.

Kanban is another Agile framework but comparing with Scrum it doesn’t have team units or special positions. Everybody sticks to their roles, teams, and responsibilities.

Kanban doesn’t make you work in incremental sprints but rather requires teams to work together to improve the product continuously. Kanban goes hand in hand with the Kanban board visualizing the workflow for fixing issues or adding features without strict timeframes. All your teammates are involved in the to-do items creation. And after the scope of work is clear, the work items are prioritized and allocated to responsible members.

#### Pull-model

Software development teams historically have had work pushed on them as stakeholders request more functionality. This is often accompanied by tight deadlines. A common side effect of this behavior is that quality suffers as the team is forced to take shortcuts necessary to deliver the functionality within the timeframe.

Kanban helps teams focus on maintaining an agreed-upon level of quality. This measure must be met before a team can claim a piece of work is done. To support this model, stakeholders do not push work upon teams that are alredy working at capacity. Instead, they add requests to a backlog that the team "pulls" into their workflow as capacity becomes available.

#### Visualize work

Understanding the status of a software development team in terms of both process and progress can be challenging. It is easier to understand the current state of work when progress is presented visually, as opposed to as a long list of work items or as a document.

Visualization of work is a key Kanban principle primarily addressed through the use of _Kanban boards_. These boards employ the use of cards that are organized by progress in order to communicate overall status.

Visualizing the work to be done as cards on a board, in different states, allows you to easily see the "big picture" of where the project currently stands, as well as identify potential bottlenecks that could affect productivity.

#### Limit work in progress

Teams that try to work on too many things often suffer from reduced productivity due to frequent and costly context switching. The team is busy but work just doesn't seem to be getting done resulting in unacceptably high lead times. To address this, limiting the number of backlog items a team is working on at any given time helps increase focus while reducing context switching. The items currently being worked on by the team are known as _work in progress_ (WIP).

The maximum number of items a team decides to work on at any point in time is known as the _WIP limit_. A well-disciplined team will work to ensure they are not exceeding their WIP limit. Should this occur, the team will investigate the reason, and work to solve the root cause for the issue.

#### Continuous improvement

For software development teams to continuously improve, they need ways to measure their team's effectiveness and throughput. Kanban, through the use of the Kanban board, provides a dynamic view of the state of work in a workflow. This allows the team to experiment with different processes and evaluate the impact on the flow of work more easily. Teams that practice Kanban often utilize measurements such as lead times and cycle times and generally embrace the benefits offered for continuous improvement.

#### Kanban boards

A Kanban board is just one of many tools teams use to implement Kanban practices in a team. A Kanban board can be a physical board or a software application that shows cards arranged into columns. Typical column names include **To-do**, **Doing**, and **Done**, but teams can customize this to suit the states in their workflow. For example, a team may prefer **New**, **Development**, **Testing**, **UAT**, and **Done**.

### FDD is feature driven development

### Multipart request
Allow us to in a post request send more that one type of data
For example image and text, also we can send chucks of that image to just not upload it all at once for better performance

### Requests
#### HTTP request
Client make the request to the server
- Handshake
- Open connection
- Close conection

#### HTTP Polling
Client keep making a http request in an regular interval
- Regular interval
- Empty response ,sometimes the server wont have a new update for the client so it will return empty
- Unnecessary network calls
- Drain battery of device

#### HTTP Long Pooling
- Client waits for a response from a server and open a connection if there is something to send back and then close it
- Long time open connection
- Timeout in case it it takes too much time

And then the client makes the same operation

#### Websockets
A websocket is a persistent connection between a client and a server.
they provide a bidirectional full duplex comunication channel that operates over HTTP through a single TP/IP connection.
At its core, the websocket protocol facilitates message passing between a client and a server.

A connection gets estabilshed from the client to the server

- Bidirectional
- Server to clietn
- Client to server
- Reduce overhead of the handshake every time

#### Server Send Events (SSEs)
It is a server push technology enabling a client to receive automatic updates from a server, like websockets but onlike one side, client cant send data.

### Stack, 
Stack uses LIFO, last in, first out

### Queue
FIFO, first in, first out

### What is cache
Stores data to speed up future request, may be a pervious computaion or a redundant copy of data.

### LRU cache
LRU (least recently used)
It is a cached of a fixed size using the LRU cache eviction policy.

Most left: last used
Most right: least used

For example size 4 -> 0, 3, 5, 6

If we use 5 now -> 5, 0, 4, 6

If we add 7 -> 7, 5, 0, 4, 6

But our cache is size 4 so we need to evict(remove) one item, we remove the least recently used, meaning the most in the right one -> 7, 5, 0, 4

### Software Architecture Patterns

**1. Layered Pattern :**  
As the name suggests, components(code) in this pattern are separated into layers of subtasks and they are arranged one above another.  

Each layer has unique tasks to do and all the layers are independent of one another. Since each layer is independent, one can modify the code inside a layer without affecting others.  

It is the most commonly used pattern for designing the majority of software. This layer is also known as ‘N-tier architecture’. Basically, this pattern has 4 layers.  

1.  Presentation layer (The user interface layer where we see and enter data into an application.)
2.  Business layer (this layer is responsible for executing business logic as per the request.)
3.  Application layer (this layer acts as a medium for communication between the ‘presentation layer’ and ‘data layer’.
4.  Data layer (this layer has a database for managing data.)

Ideal for:  

E-commerce web applications development like Amazon.  

**2. Client-Server Pattern :**  
The client-server pattern has two major entities. They are a server and multiple clients.  

Here the server has resources(data, files or services) and a client requests the server for a particular resource. Then the server processes the request and responds back accordingly.

Examples of software developed in this pattern:  

-   Email.
-   WWW.
-   File sharing apps.
-   Banking, etc…

So this pattern is suitable for developing the kind of software listed in the examples.  

**3. Event-Driven Pattern :**  
Event-Driven Architecture is an agile approach in which services (operations) of the software are triggered by events.  

Well, what does an event mean?  

When a user takes action in the application built using the EDA approach, a state change happens and a reaction is generated that is called an event.

**Eg:** A new user fills the signup form and clicks the signup button on Facebook and then a FB account is created for him, which is an event.

Ideal for:    

Building websites with JavaScript and e-commerce websites in general.  

**4. Microkernel Pattern :**  
Microkernel pattern has two major components. They are a core system and plug-in modules. 

-   The core system handles the fundamental and minimal operations of the application.
-   The plug-in modules handle the extended functionalities (like extra features) and customized processing.

**Let’s imagine**, you have successfully built a chat application. And the basic functionality of the app is that you can text with people across the world without an internet connection. After some time, you would like to add a voice messaging feature to the application, then you are adding the feature successfully. You can add that feature to the already developed application because the microkernel pattern facilitates you to add features as plug-ins.  

Microkernel pattern is ideal for:  

Product-based applications and scheduling applications. We love new features that keep giving dopamine boost to our brain. Such as Instagram reels, YouTube Shorts and a lot more that feasts us digitally. So this pattern is mostly preferred for app development.  

**5. Microservices Pattern :**  
The collection of small services that are combined to form the actual application is the concept of microservices pattern. Instead of building a bigger application, small programs are built for every service (function) of an application independently. And those small programs are bundled together to be a full-fledged application.  

So adding new features and modifying existing microservices without affecting other microservices are no longer a challenge when an application is built in a microservices pattern.  

Modules in the application of microservices patterns are loosely coupled. So they are easily understandable, modifiable and scalable.  

**Example** Netflix is one of the most popular examples of software built-in microservices architecture. This pattern is most suitable for websites and web apps having small components.

### Git
Git is a distribution version control system that allows multiple people to colaborate in the same project.

#### Common commands

 - git add .
 - git commit -m ""
 - git push 
 - git pull
 - git status
 - git log
 - git log --stat show more info( number of insertions and deletions)
 - git log -p ( will show what changed in every file)

##### Branches
 - git brach "name" (creates branch)
 - git branch -v (show branches)
 - git branch (shows what branch i am in)
 - git checkout "branch name" (move us to the branch)
 - git checkout -b " name" creates and changes branch
 - git push origin "branch name" in this case origin ins the main one
 - git merge "branch name", this merges it locally
 - git push origin master push it to the main

#### Branches
In Git, a `branch` is a new/separate version of the main repository.

**git fetch** really only downloads new data from a remote repository - but it doesn't integrate any of this new data into your working files. Fetch is great for getting a fresh view on all the things that happened in a remote repository.  
Due to it's "harmless" nature, you can rest assured: fetch will never manipulate, destroy, or screw up anything. This means you can never fetch often enough.

**git pull**, in contrast, is used with a different goal in mind: to update your current HEAD branch with the latest changes from the remote server. This means that pull not only downloads new data; it also directly **integrates** it into your current working copy files.

Git fetch pulls every branch data, meaning if we create a new branch and want to sync locally
we need to git fetch, git pull wil fail
