#  Inheritance

* Overloading: Multiple methods with same name,but different parameters in Java

# Is-a hierarchy
* Hypernyms: dog is a hypernym of poodle, malamute
* Hyponym: poodle os hyponym of dog
<img width="355" alt="Screen Shot 2020-06-08 at 5 50 06 PM" src="https://user-images.githubusercontent.com/27160394/84087794-86da1980-a9b0-11ea-8282-5ce12718ab4a.png">

 ## Express in java
#### 1. Define a referennce type for hypernym
Use the keyword `interface` instead of class to define hypernym.
* Interface is a specification of what is able to do, not how to do it.(no implementations)
```
public interface hypernym(){
  public void todo(object smt);
}
```
    
#### 2. Specify that subtypes are hyponym of that types

Use the keyword `implements` to tell the java compiler that what are hyponyms of hypernym.

* It is mandatory to implement all the methods in a class that implements an interface unless and until that class is an Abstract class.

```
public class hyponyms implements hypernym{
    public void todo(String){
      System.out.println(String)
    }
}
```
#### 2b.Overriding
* If a “subclass” has a method with the exact same signature as in the “superclass”
* we’ll always mark every overriding method with the @Override annotation.
  * if not overriding, it will not compile.
  * Even if you don’t write @Override, subclass still overrides the method.
  * Reminds that method definition came from somewhere higher up in the inheritance hierarchy.

```
@Override
public void todo(String){
      System.out.println(String)
    }
```

# 1. Interface Inheritance
> Specifying the capabilities of a subclass using the implements.

* Interface: The list of all method signatures.
* Subclasses must override all of these methods!
  * Will fail to compile otherwise.
* Such relationships can be multi-generational.
* If X is a superclass of Y, then memory boxes for X may contain Y.
```
public static void main(String[] args) {
   List61B<String> someList = new SLList<String>();	
   someList.addFirst("elk");
}
```

### 2. Implementation Inheritance: Default Methods
* Default Method :specify that a method definition in an interface,with the default keyword at the beginning of the method signature.
```
default public void print() {
      for (int i = 0; i < size(); i += 1) {
         System.out.print(get(i) + " ");
      }
      System.out.println();
   }

```
* An implementing class can override the default implementation provided by the interface

#### Static and Dynamic Type 
* Static Type : Every variable in Java has a “compile-time type”(specified at declaration)
* Dynamic type: Variables also have a “run-time type”(specified at instantiation)

#### Dynamic Method Selection
* if dynamic type variable overrides the method from static type , dynamic method is used instead
```
Animal a = new Dog();
Dog d = new Dog();
a.flatter(d);
```
* If there are multiple methods that can handle T1, the compiler records the “most specific” one. 
```
TPrime foo = new dog();//has bar(Dog) and bar(Animal)
T1 x1= new dog();
foo.bar(x1)//it will record bar(Dog)
```


# 2. Implementation Inheritance: Extends
* When a class is a hyponym of an interface, use implements.
* when a class is a hyponym of another class, use extends
* extends should only be used for is-a relationships.

## Constructors
* Constructors are not inherited. 
* the rules of Java say that all constructors must start with a call to one of the super class’s constructors 
```
public VengefulSLList() {
   super();//If you don’t explicitly call the constructor, Java will automatically do it for 
   deletedItems = new SLList<Item>();
}
```
* If you want to use a super constructor other than the no-argument constructor, can give parameters to super.

## The Object Class
> Class Object is the root of the class hierarchy. Every class has Object as a superclass.

* Interfae do not extend the object class.

|Common method|Description
|-------------|------------
|equals(obj)|indicates whether some other object is "equal to" this one.
|hashCode ()| Returns a hash code value for the object.
|toString ()|Returns a string representation of the object.


# Encapsulation
#### Managing complexity
* Hierarchical abstraction: Create layers of abstraction.
* Design for change
  1. Organize program around objects
  2. Let objects decide how things are done.
  3. Hide information others don’t need.
#### Modules
> A set of methods that work together as a whole to perform some task or set of related tasks
* A module is said to be encapsulated if its implementation is completely hidden, 
* It can be accessed only through a documented interface.

## Checking
### 1. Compile-Time Type Checking
* If overridden, decide which method to call based on run-time type of variable.
* Compiler allows <> calls based on compile-time type of variable.
  1. method
  2. assignments
  3. expression
* An expression using the new keyword has the specified compile-time type
```
Object<String> ob= new Dog<String>();//compile-time type of right hand side (RHS) expression is dog, dog is an object
```
* Method calls have compile-time type equal to their declared type.
```
public staitc Dog maxDog(Dog d1,Dog d2)//Any call to maxDog will have compile-time type Dog!
```
* The dynamic type of parent can be child type, But the dynamic type of child type only can be themselives.
```
Object<String> ob= new Dog<String>(); // correct
Dog<String> big = new Object<String>(); //wrong 
```
### Casting
> specifying the compile-time type of any expression.
* Put desired type in parenthesis before the expression
```
maxDog(frank, frankJr);//Compile-time type Dog:
(Poodle) maxDog(frank, frankJr);//Compile-time type Poodle
Poodle largerPoodle = (Poodle) maxDog(frank, frankJr); // compiles! Right hand side has compile-time type Poodle after casting
```

###  Higher Order Function
> A function that takes other functions as data.
* Old java: Pass a function by Using Interfaces
* Java 8: can hold references to methods


# Summary of Implementation Inheritance 
* `extends` means is-an. Inherits all members!
  1. Variables, methods, nested classes.
  2. Not constructors.
  3. Subclass constructor must invoke superclass constructor first.
  4. Use super to invoke overridden superclass methods and constructors
* Invocation of overridden methods follows two simple rules:
  1. Compiler plays it safe and only lets us do things allowed by static type.
  2. For overridden methods the actual method invoked is based on dynamic type of invoking expression,
  3. Can use casting to overrule compiler type checking.

# Polymorphism
> providing a single interface to entities of different type
## Writing a General Max Function

```
public static Object max(Object[] items){
	int maxindex=0;
	for (int i=0;i<items.length;i++){
		if (items[i]>items[maxindex]){//Objects cannot be compared to other objects with >
			maxindex=i;
		}
	}
	return items[maxindex];
}
```
* Write a max method in the Dog class.: if cat/horse class need to use same methods. it's repeatable.
* Solution: Create an interface that guarantees a comparison method.

## Build-in Comparable
```
public interface Comparable<T>{// generics type
    public int compareTo(T obj)
}
```
#### Pros
* Lots of built in classes implement Comparable (e.g. String).
* Lots of libraries use the Comparable interface (e.g. Arrays.sort)
* Avoids need for casts.

  
## Comparator
> Compare objects in different way(multiple orderings)
*  “Natural Order” :sometimes used to refer to the ordering implied by a Comparable’s compareTo method.
```
public interface Comparator<T>{
    int compare(T o1, T o2);
}
```

## Comparable and Comparator Summary

Interfaces provide us with the ability to make callbacks:
* Sometimes a function needs the help of another function that might not have been written yet.
* In Java, we do this by wrapping up the needed function in an interface 
  * (e.g. Arrays.sort needs compare which lives inside the comparator interface)

## 

