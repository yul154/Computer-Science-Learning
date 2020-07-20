# OOD Principle and Patterns
#### 1.Abstraction
> describing the parts of a system involves naming them and explaining their functionality

##### Abstract data types
* An ADT specifies what each operation does, but not how it does it.
  * In Java, an ADT can be expressed by an interface
* An ADT is realized by a concrete data structure, which is modeled in Java by a class.

#### 2. Encapsulation
> Different components of a software system should not reveal the internal details of their respective implementations.
*  It gives one programmer freedom to implement the details of a component, without concern that other programmers

#### 3. Modularity
* Keeping these interactions straight requires that these different components be well orga- nized.


# Design Patterns
> a solution to a “typical” software design problem

* A pattern provides a general template for a solution that can be applied in many different situations
* Patterns for solving algorithm design problems: Recursion, Divide-and-conquer ,Amortization,Dynamic programming
* Patterns for solving software engineering problems: Template method, Composition ,Adapter, Factory Method

# Inheritance
> “is a” relationship

* This allows a new class to be defined based upon an existing class as the starting point.
* Java is said to allow only single inheritance among classes
* Constructors are never inherited in Java
* The first operation performed within the body of a constructor must be to invoke a constructor of the superclass.
```
public PredatoryCreditCard(String cust, String bk, String acnt, int lim, double initialBal, double rate) {
      super(cust, bk, acnt, lim, initialBal); // initialize superclass attributes
      apr = rate;
}
```
*  If a constructor for a subclass does not make an explicit call to `super` or `this` as its first command, then an implicit call to super()
  * the zero-parameter version of the superclass constructor.
```
public boolean charge(double price) { 
  boolean isSuccess = super.charge(price); 
    if (!isSuccess)
        balance += 5; 
    return isSuccess;
}
```

## Polymorphism
> It refers to the ability of a reference variable to take different forms.
* Liskov Substitution Principle: a variable (or parameter) with a declared type can be assigned an instance from any direct or indirect subclass of that type.
```
CreditCard card = new PredatoryCreditCard(...);
//polymorphic :it may take one of many forms, depending on the specific class of the object to which it refers.
```
* Dynamic dispatch: at runtime to call the version of the method that is most specific to the actual type of the referenced object
```
card.charge(100)// Even if the reference variable has a declared type of CreditCard,  it will execute the PredatoryCreditCard.charge method
```
* `instanceof`:  whether an in- stance satisfies as a particular type

## Inheritance Hierarchies
* Although a subclass may not inherit from multiple superclasses in Java, 
* A superclass may have many subclasses.

# Interface and Abstract

## Interface
>  a collection of method declarations with no data and no bodies
* Strong type: the types of parameters that are actually passed to methods rigidly conform with the type specified in the in- terface
* multiple inheritance: multiple inheritance is allowed for interfaces but not for classes

## Abstract Classes
> Serves a role somewhat between that of a traditional class and that of an interface.
*  abstract methods: define signatures for one or more methods without body;
*  An abstract class may define one or more fields and any number of methods with implementation
*  No object can be created directly from an abstract class
* Single in heritance for abstract class in java
* The primary purpose of the abstract class is to provide common functionality to subclasses
* Template method pattern: an abstract base class provides a concrete behavior that relies upon calls to other abstract behaviors.



# Exceptions
> Unexpected events that occur during the execution of a program

## Catching
* `try-catch`:a guarded fragment of code that might throw an exception is executed
```
try{
    guardedBody
    }catch(exceptionType1 variable1){
      remedyBody1
    }catch(exceptionType variable2){
      remedyBody2
    }
```
* `finally` clause: will be executed whether or not an exception happens in the origi- nal guarded body


## Throwing
### `throw`
* `throw`:an instance of the exception type to be thrown
* Throw keyword is used in the *method body* to throw an exception
* This exception must be a subclass of Throwable
* `throw` explicitly throw only one exception
```
throw new exceptionType(parameters);
```
```
public double divide(double a, double b) {
    if (b == 0) {
        throw new ArithmeticException("Divider cannot be equal to zero!");
    }
    return a / b;
}
```
### `throws`
* Used in method signature to declare the exceptions that can occur in the statements present in the method.
* method signature level
* The method may throw multiple exceptions.
```
public static void execute() throws SocketException, ConnectionException, Exception
```
### Java’s Exception Hierarchy
<img width="572" alt="Screen Shot 2020-06-10 at 6 34 05 PM" src="https://user-images.githubusercontent.com/27160394/84328970-19adbc00-ab49-11ea-8e75-bd948dc29a01.png">

#### Error and Exception
* Error: typically thrown only by the Java Virtual Machine, 
  * designate the most serious situations that are unlikely to be recoverable
  * Errors should not be caught or handled
* Exceptions: designate situations in which a running program might reasonably be able to recover
#### Checked and Unchecked Exceptions
* A checked exception : it's checked at the compile time. 
* Unchecked exceptions : subtypes of RuntimeException in Java
* all checked exceptions that might propagate upward from a method must be explicitly declared in its signature

# Casting and Generics
## Casting
* Widening Conversions(automatically performed): T -> U
1. T and U are class types and U is a superclass of T.
2. T and U are interface types and U is a superinterface of T .
3. T is a class that implements interface U .
```
CreditCard card = new PredatoryCreditCard(...);
```
* Narrowing Conversions(explicit cast): T -> S
1. T and S are class types and S is a subclassof T.
2. T and S are interface types and S is a subinterface of T .
3. T is an interface implemented by class S. 
```
CreditCard card = new PredatoryCreditCard(...);
PredatoryCreditCard pc = (PredatoryCreditCard) card;
```
### Casting Exceptions
* `ClassCastException`: if object o is not also of type S, then attempting to cast o to type S will throw an exception
 *  Java provides a way to make sure an object cast will be correct:` instanceof`
```
Number n;
Integer i;
n = new Integer(3);
if (n instanceof Integer)
i = (Integer) n;
n = new Double(3.1415); if (n instanceof Integer)
i = (Integer) n;
```

## Generics
> Operate on a variety of data types while often avoiding the need for explicit casts.
* The goal of generic programming is to be able to write a single class that can represent different type of data.
* Don' need to specify actuall type parameters.
* enable a class, interface and, method, accept all (reference) types as parameters

### Object class generics
* generic programming was implemented by relying heavily on Java’s Object class
* The drawback of the object classic approach involves use of the accessors
 * Still return Object reference which hard to narrow conversion.
### Generics Framework
```
public class Pairs<A,B>

Pair<String,Double> bid;
bid = new Pair<>("ORCL", 32.07);
```
1. After the new operator, we provide the name of the generic class, 
2. then an empty set of angle brackets (known as the “diamond”), 
3. finally the parameters to the constructor

Type inference: the actual types for the formal type parameters determined based upon the original declaration of the variable to which it is assigned

### Generics Arrays
> don't go well together
Nonparametric array: it allows an array defined with a parameterized type to be initialized with a newly created

####  create a generic class that can store a fixed number of generic entries in an array
1. Instantiate an array of type Object[ ]
2. Make a narrowing cast to type T[ ]
```
data = new T[capacity];// illegal; compiler error
data = (T[ ]) new Object[capacity];// legal, but compiler warning
```
### Generics Methods
 * Use of the <T> modifier to declare the method to be generic
 * By default, when using a type name such as T in a generic class or method
```
public static <T> void reverse(T[ ] data) {
    int low = 0, 
    high = data.length − 1; 
    while (low < high) {
        T temp = data[low]; 
        data[low++] = data[high]; 
        data[high−−] = temp;
                      }
     }
}
```
* Bounded Generic Types : A formal parameter type can be restricted by using the extends keyword followed by a class or interface

```
public class ShoppingCart<T extends Sellable>
```
# Nested Classes
> when defining a class that is strongly affiliated with another class
* as an instance of a nested use can be used to represent a small portion of a larger data structure
* its fully qualified name is `OuterName.NestedName`.
* `private` nested class can be used by the outer class, but by no other classes.
* `static` nested class  have no association with any specific instance of the outer class.

## Nonstatic nested class(inner class)
*  An instance of an inner class can only be created from within a nonstatic method of the outer class
* Each instance of an inner class implicitly stores a reference to its associated outer instance,
* Access from within the inner class methods using the syntax OuterName.this
