# Inheritance

Inheritance: one class acquires the properties of another

* Key word : `extend`

```
class superclass{

}

class subclass extends superclass{

}
```

* When an object of subclass is created, a copy of conntens of superclass is made within it
* it is recommended to always create reference variable to the subclass.
  * The Superclass reference variable can hold the subclass object, but using that variable you can access only the members of the superclass
```
Superclass super = new Subclass();
super.supermethod()//
super.submethod()// cannot call the method which belong to the subclass ,
```

* A subclass inherits all the members (fields, methods, and nested classes) from its superclass. 
* Constructors are not members, so they are not inherited by subclasses,
* the constructor of the superclass can be invoked from the subclass.


## `super`

Uses scenarios

* It is used to differentiate the members of superclass from the members of subclass, if they have same names.
```
super.variable 
super.method();
```
* It is used to invoke the superclass constructor
  * If a class is inheriting the properties of another class, the subclass automatically acquires the default constructor of the superclass. 
  * if you want to call a parameterized constructor of the superclass, you need to use the super keyword
```
class Superclass{
    int age;
    
    Superclass(int age){
      this.age =age
    }
  }

class Subclass extends Superclass{
      Subclass(int age){
        super(age)
      }
}
```
* `extends` and `implements` are IS-A Relationship
* `instace of` check determine whether IS-A Relationship
```
Mammal m= new Mammal();
System.out.println( m instanceof Animal );
```
* An IS-A relationship is inheritance. The classes which inherit are known as sub classes or child classes. On the other hand, HAS-A relationship is composition.

<img width="407" alt="Screen Shot 2020-06-29 at 12 57 11 PM" src="https://user-images.githubusercontent.com/27160394/86039443-0edb9e00-ba08-11ea-9694-d685b9947e07.png">

## Overriding
* Overriding is ability to define a behavior that's specific to the subclass type
  * a subclass can implement a parent class method based on its requirement.

**In compile time, the check is made on the reference type. However, in the runtime, JVM figures out the object type and would run the method that belongs to that particular object**

```
Animal a = new Animal(); // Animal reference and object 
Animal b = new Dog(); // Animal reference but Dog object
```
* If the superclass method is declared public then the overridding method in the sublass cannot be either private or protected.
* A subclass within the same package as the instance's subclass can override any superclass method that is not declared private or final
* A subclass in a different package can only override the non-final methods declared public or protected.
---

# Polymorphism
> an object to take on many forms.

*The most common use of polymorphism in OOP occurs when a parent class reference is used to refer to a child class object.*

## Reference type

```
A a = new A();  //statement 1
```

> the right of the = creates an object of class A.
>> the left defines the variable to store it in, in this case a variable of type A. 
>>> the = is an assignment. So this creates an object of class A and saves the reference to it in a variable of type A.

```
A a1= new B(); //statement 2
```
> the right of the = creates an object of class B;
>> the left defines the variable to store it in, in this case a variable of type A; 
>>> the = is an assignment. So this creates an object of class B and saves the reference to it in a variable of type A. 
>>>> This means that when accessing the object through that variable, you only have access to the things defined by A, even though the object is a B. 


The only possible way to access an object is through a reference variable.

A reference variable can be of only one type. Once declared, the type of a reference variable cannot be changed.

The type of the reference variable would determine the methods that it can invoke on the object.

```
Deer d = new Deer(); 
Animal a = d; 
Vegetarian v = d; 
Object o = d;//All the reference variables d, a, v, o refer to the same Deer object in the heap. 
```
--
# Abstraction

**In Object-oriented programming, abstraction is a process of hiding the implementation details from the user, only the functionality will be provided to the user.**

## Abstract Class
> A class with `abstract` key word is knows as abstract class.

* Abstract methods within inAbstract classes are uncertain
* If a class has at least one abstract method, then the class must be declared abstract.
* If a class is declared abstract, it cannot be instantiated.
* To use an abstract class, you have to inherit it from another class, provide implementations to the abstract methods in it.
* If you inherit an abstract class, you have to provide implementations to all the abstract methods in it.

### Abstract Methods
> If you want a class to contain a particular method 
>> but you want the actual implementation of that method to be determined by child classes
>>> you can declare the method in the parent class as an abstract.

* An abstract method contains a method signature, but no method body.
*  Instead of curly braces, an abstract method will have a semoi colon (;) at the end.

```
public abstract class Employee{
    public abstract double computePay();
}
```
* Any class inheriting the current class must either override the abstract method or declare itself as abstract.
--

# Encapsulation
>  wrapping the data (variables) and code acting on the data (methods) together as a single unit.

* In encapsulation, the variables of a class will be hidden from other classes, and can be accessed only through the methods of their current class

## To achieve encapsulation in Java

1. Declare the variables of a class as private.
2. Provide public setter and getter methods to modify and view the variables values.


## Benefits of Encapsulation
1. The fields of a class can be made read-only or write-only.
2. A class can have total control over what is stored in its fields.
3. The users of a class do not know how the class stores its data. A class can change the data type of a field and users of the class do not need to change any of their code.
---

# Interfaces

**An interface is similar to a class in the following ways:**
* An interface can contain any number of methods.
* An interface is written in a file with a .java extension, with the name of the interface matching the name of the file.
* The byte code of an interface appears in a .class file.
* Interfaces appear in packages, and their corresponding bytecode file must be in a directory structure that matches the package name.

**An interface is different from a class in several ways**

* An interface does not contain any constructors.(abstract can have)
* All of the methods in an interface are abstract.
* An interface cannot contain instance fields. The only fields that can appear in an interface must be declared both static and final.
* An interface is not extended by a class; it is implemented by a class.
* An interface can extend multiple interfaces.

## Declaring and Implementing Interfaces

* Methods in an interface are implicitly public.

* Checked exceptions should not be declared on implementation methods other than the ones declared by the interface method or subclasses of those declared by the interface method.

* The signature of the interface method and the same return type or subtype should be maintained when overriding the methods.

* An implementation class itself can be abstract and if so, interface methods need not be implemented.

### Tagging Interfaces
> An interface with no methods in it is referred to as a tagging interface

* Creates a common parent:you can use a tagging interface to create a common parent among a group of interfaces. 
* Adds a data type to a class: tagging comes from. A class that implements a tagging interface does not need to define any methods (since the interface does not have any), but the class becomes an interface type through polymorphism.

---
# Packages
> prevent naming conflicts, to control access, to make searching/locating and usage of classes, interfaces, enumerations and annotations easier,

Commonn packages.

```
java.lang - bundles the fundamental classes
java.io - classes for input, output functions are bundled in this package
```

* the package creates a new namespace: group related classes implemented 
