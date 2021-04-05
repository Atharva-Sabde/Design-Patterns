# Design Patterns:

- ← contents →
    1. History
    2. Use cases
        - Resources

            [Gangof Four DP](https://drive.google.com/drive/u/0/my-drive)

Many of the Java APIs and many common Java frameworks use various design patterns extensively. Study their documentation and see how they are put together from a concept and definition perspective.

From there work to implement them. Patterns are exactly that. A template or method to follow. If you are working in certain types of application development, many patterns repeat and are commonly used. Facades, Adapters and Factories being extremely common.

You learn by doing. Some patterns are essential to software design. Virtually every framework I’ve used and every one I’ve designed has some sort of factory pattern associated with it to allow for construction of object instances. Other patterns have operational aspects like Dependency Injection which allow me to defer implementation choices at runtime. Factories are a common way dependency injection can be implemented. Patterns can build upon pattern.

Look at your language and your frameworks. Armed with a pattern list, play the “Find the Pattern” game. You’ll quickly come up with several. Then, if you have the source code, see how that pattern was implemented. Rinse, lather, repeat for each pattern. Not all patterns will be used and some patterns can be really hard to find in the wild.

One piece of advice when you go to implement software using patterns: Amateurs go overboard with patterns. Way overboard. They think everything is a pattern and needs to be named that way. MyFactoryThis, SessionFacadeThat and FooBarAdaptor. Don’t! Honestly, outside of naming factories SomethingFactory, most patterns are organic in nature and are identified in-situ by their usage.

Good pattern usage is obvious in its design. Naming everything SomethingPattern detracts from good organic design. You don’t use every pattern in the book. You use just the ones that make sense in that context to make implementation and maintenance easier.

==============introduction ends======================

RTMNU syllabus: 

![Design%20Patterns%20bc60bbfa4b0f401187b09251fe5297b3/Untitled.png](Design%20Patterns%20bc60bbfa4b0f401187b09251fe5297b3/Untitled.png)

[//Mosh](//mosh) 

![Design%20Patterns%20bc60bbfa4b0f401187b09251fe5297b3/Untitled%201.png](Design%20Patterns%20bc60bbfa4b0f401187b09251fe5297b3/Untitled%201.png)

What are Design Patterns?
They are Elegant solutions to repeating problems

## Catalogue of Patterns:   (23)

1. Creational Pattern : making of classes and objects  (5)
2. Structural Pattern : mediator between two entities  (7)
3. Behavioral Pattern:      (11)

### Advantages:

semantical :
→ improves communication with other developers at more abstract levels.

→ it teaches you how to be a designer , and how to make reusable , maintainable  , extensible code.

→ it helps you learn and adapt new frameworks quickly.

Technical :

The authors claim the following as advantages of interfaces over implementation:

- clients remain unaware of the specific types of objects they use, as long as the object adheres to the interface
- clients remain unaware of the classes that implement these objects; clients only know about the abstract class(es) defining the interface

Use of an interface also leads to [dynamic binding](https://www.wikiwand.com/en/Dynamic_dispatch) and [polymorphism](https://www.wikiwand.com/en/Polymorphism_in_object-oriented_programming), which are central features of object-oriented programming.

![Design%20Patterns%20bc60bbfa4b0f401187b09251fe5297b3/Untitled%202.png](Design%20Patterns%20bc60bbfa4b0f401187b09251fe5297b3/Untitled%202.png)

# Creational:

All about different ways to create objects.

# 1. Singleton

Singleton pattern is a creational design pattern that restricts the number of objects of a class. It ensures that there is only one instance of the class in the JVM. It is a very simple design pattern but when we need to implement it, there are a lot of implementation concerns. Singleton pattern allows an application to have one and only one instance or object of a class per JVM.

- code:

    ```java
    public class SingletonTS {

    	private static SingletonTS uniqueInstance;

    	//	other useful instance variables here

    	private SingletonTS() {}

    	public static synchronized SingletonTS getInstance() {
    		if (uniqueInstance == null) {
    			uniqueInstance = new SingletonTS();
    		}
    		return uniqueInstance;
    	}

    	//	other useful methods here

    }
    ```

# 2. Factory

A factory design pattern is useful when we have a superclass with multiple subclasses and we need to return one of the sub-class based on the input. We can apply a Singleton design pattern on the Factory class or declare the factory method as static. A factory design pattern is most suitable when there is an involvement of complex object creation steps. The factory pattern ensures that these steps work in a centralized manner and not exposed to composing classes.

- code:

    ```java
    public class PizzaStore {

    	SimplePizzaFactory factory;

    	public PizzaStore(SimplePizzaFactory factory) {
    		this.factory = factory;
    	}

    	public Pizza orderPizza(String type) {
    		Pizza pizza;

    		pizza = factory.createPizza(type);

    		pizza.prepare();
    		pizza.bake();
    		pizza.cut();
    		pizza.box();

    		return pizza;
    	}

    }
    ```

# 3. Abstract Factory

Abstract Factory pattern is almost similar to the Factory design pattern and we can say it as a factory of factories. In the Abstract Factory pattern, there is no need to use the if-else block of the factory pattern. We have a factory class for each subclass and then we use an Abstract Factory class that returns the child class on the basis of the input Factory class. Abstract factory pattern is useful whenever we need another level of abstraction over a group of factories produced using the factory pattern.

- code:

    ```java
    public class CheesePizza extends Pizza {

    	PizzaIngredientFactory ingredientFactory;

    	public CheesePizza(PizzaIngredientFactory ingredientFactory) {
    		this.ingredientFactory = ingredientFactory;
    	}

    	void prepare() {
    		System.out.println("Preparing " + name);
    		dough = ingredientFactory.createDough();
    		sauce = ingredientFactory.createSauce();
    		cheese = ingredientFactory.createCheese();
    	}

    }
    ```

# 4.  Builder Pattern

The Builder Design Pattern came into the picture to solve the problems of having many attributes in an Object. Builder Design pattern solves the problem of optional parameters and inconsistent state. It solves the problem by providing a step-by-step way to build the object and a method that returns the final Object. A builder design pattern is an alternative way to build complex objects. We should use it only when we want to build different types of immutable objects using the same object building process.

- code:

    ```java
    public class BuilderDemo {
       public static void main(String[] args) {
          // Placeholder for the Director.
          MealDirector director = new MealDirector();

          // PlaceHolder for the builder
          MealBuilder builder = null;

          boolean isKid = false;

          if (isKid) {
             builder = new KidsMealBuilder();
          } else {
             builder = new AdultMealBuilder();
          }

          // Gets the correct meal.
          Meal meal = director.createMeal(builder);

          System.out.printf("%s\n", meal.toString());
       }  // main
    }
    ```

# 5.  Prototype Pattern

The prototype pattern is useful when the process of object creation is very costly and time-consuming. So using this pattern we can copy the original object to a new object and then change it according to our requirements. This pattern uses a Java cloning mechanism to copy the object.

The prototype pattern is useful when the process of object creation is very costly and time-consuming. So using this pattern we can copy the original object to a new object and then change it according to our requirements. This pattern uses a Java cloning mechanism to copy the object.

- code:

    ```java

    ```

# Structural:

All about Relationships between objects.

# Behavioural:

All about Interaction - Communication between objects.
