# Java – Variable Types

*  Variable Types determines the size and layout of the variable's memory
*  must declare all variables before they can be used

```
data type variable  = value;
int a,b,c;
int a =10,b=10;
char a = ‘a’;
```

## Local Variables

* which are declared in methods, constructors

* which created when the method, constructors is called

* the variable will be destroyed once it exits the method, constructor, or block.

* Access modifiers cannot be used for local variables.

* Local variables are visible only within the declared method, constructor, or block.

* Local variables are implemented at stack level internally.

* There is no default value for local variables
```
public class Test{
   public void pupAge(){
      int age;// Local variables should be declared and an initial value should be assigned before the first use.
      age = age + 7;
      System.out.println("Puppy age is : " + age);
      }
public static void main(String args[]){ 
    Test test = new Test(); 
     test.pupAge();
    }  
}
```

## Instance Variables
* Instance variables are declared in a class, but outside a method, constructor or any block.

* When a space is allocated for an object in the heap, a slot for each instance variable value is created.

* Instance variables are created when the keyword 'new' is used

* Instance variables have default values.

* Instance variables can be accessed directly by calling the variable name inside the class.


## Class/static Variables
* Class variables also known as static variables are declared with the static keyword in a class

* There would only be one copy of each class variable per class,

* Static variables are stored in the static memory

* Static variables can be accessed by calling with the class name `ClassName.VariableName`.


# Modifier Types

## Java Access Modifiers
> set access levels for classes, variables, methods, and constructors.

* Visible to the package, the default. No modifiers are needed.
* Visible to the class only (private).
* Visible to the world (public).
* Visible to the package and all subclasses (protected).

## Default Access Modifier - No Keyword
* A variable or method declared without any access control modifier is available to any other class in the same package.

* The fields in an interface are implicitly public static final 

* the methods in an interface are by default public

## Private Access Modifier - Private

* Methods, variables, and constructors that are declared private can only be accessed within the declared class itself.

*  Class and interfaces cannot be private.

* Variables that are declared private can't accessed outside the class, beside public getter methods are present in the class.

## Public Access Modifier - Public

* If the public class we are trying to access is in a different package, then the public class still needs to be imported.

## Protected Access Modifier - Protected

* Variables, methods, and constructors, which are declared protected in a superclass can be accessed only by the subclasses in other package or any class within the package of the protected members' class.

* The protected access modifier cannot be applied to class and interfaces

* methods and fields in a interface cannot be declared protected.


### Access Control and Inheritance

* Methods declared public in a superclass also must be public in all subclasses.
* Methods declared protected in a superclass must either be protected or public in subclasses; they cannot be private.
* Methods declared private are not inherited at all, so there is no rule for them.

## Java Non-Access Modifiers

* `static`: creating class methods and variables.
* `final`:  finalizing the implementations of classes, methods, and variables.
* `abstract`:  creating abstract classes and methods.
* `synchronized`,`volatile`: used for threads.

### `Static`

*  Static variable: 
  1. Only one copy of the static variable exists regardless of the number of instances of the class.
  2. will exist independently of any instances created for the class
*  Static Methods:
  1. Static methods do not use any instance variables of any object of the class they are defined in
  2. Static methods take all the data from parameters and compute something from those parameters, with no reference to variables.

### `Final`

* Finnal variable
   * A `final` variable can be explicitly initialized only once
   * cannot change the value of final variable(It will be constant).
* Final Methods
  * cannot be overridden by any subclasses.
* Final Classes
  * prevent the class from being subclassed.
  * no class can inherit any feature from the final class.
  
### `Abstract`
* Abstract class
  * An abstract class can never be instantiated.
  * The sole purpose is for the class to be extended.
  * A class cannot be both abstract and final 
  * If a class contains abstract methods then the class should be declared abstract
* Abstract Methods
  * a method declared without any implementation
  * Any class that extends an abstract class must implement all the abstract methods of the super class, 


### `Synchronized`,`Transient`, `Volatile`

* `Synchronized` indicate that a method can be accessed by only one thread at a time. 
*  `transient` variable  indicate the JVM to skip the particular variable when serializing the object containing it.
* `Volatile`: let the JVM know that a thread accessing the variable must always merge its own private copy of the variable with the master copy in the memory.

# Basic Operators
* Arithmetic Operators
* Relational Operators
* Bitwise Operators
* Logical Operators
* Assignment Operators
* Misc Operators

## The Arithmetic Operators
<img width="423" alt="Screen Shot 2020-06-18 at 10 54 39 PM" src="https://user-images.githubusercontent.com/27160394/85095337-b3631200-b1b6-11ea-805b-0de6209e738e.png">

## Relational Operators

## The Bitwise Operators
<img width="400" alt="Screen Shot 2020-06-18 at 10 55 58 PM" src="https://user-images.githubusercontent.com/27160394/85095386-e2798380-b1b6-11ea-96f7-da9938c187f9.png">

## The Logical Operators
<img width="482" alt="Screen Shot 2020-06-18 at 10 58 50 PM" src="https://user-images.githubusercontent.com/27160394/85095544-4e5bec00-b1b7-11ea-9073-10932d60d1eb.png">

## Miscellaneous Operators

*  Conditional Operator ( ? : )
```
variable x = (expression) ? value if true : value if false

int a = 10;
int b;
b = (a == 10) ? 20: 30; // b = 20
```
* instanceof Operator

```
( Object reference variable ) instanceof (class/interface type)

String name = "James"; // following will return true since name is type of 
String boolean result = name instanceof String;
```
