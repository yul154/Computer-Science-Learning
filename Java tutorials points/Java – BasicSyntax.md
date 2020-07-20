# Basic keyword
Java program can be defined as a collection of objects that communicate via invoking each other's methods

* Object:  Objects have states and behaviors.
* Class: A class can be defined as a template/blueprint that describes the behavior/state that the object of its type supports.
* Methods: A method is basically a behavior.
* Instance Variables: An object's state is created by the values assigned to these instance variables.

## Basic Syntax

* Class Names - For all class names the first letter should be in Upper Case
* Method Names - All method names should start with a Lower Case letter.
* Program File Name - Name of the program file should exactly match the class name.

## Java Identifiers
>  Names used for classes, variables, and methods
* All identifiers should begin with a letter 

## Java Modifiers

###  Access Modifiers
default, public , protected, private

### Non-access Modifiers
final, abstract, strictfp

## Java Variables

* Local Variables
* Class Variables (Static Variables)
* Instance Variables (Non-static Variables)

## Java Enums
Enums restrict a variable to have one of only a few predefined values. 
The values in this enumerated list are called enums

```
class FreshJuice {
    enum FreshJuiceSize{ SMALL, MEDIUM, LARGE }
    FreshJuiceSize size;
 }

public class FreshJuiceTest {
  public static void main(String args[]){
      FreshJuice juice = new FreshJuice();
      juice.size = FreshJuice.FreshJuiceSize.MEDIUM ; 
      System.out.println("Size: " + juice.size);
  } 
}
```
## Inheritance
> allows you to reuse the fields and methods of the existing class without having to rewrite the code in a new class

## Interfaces

> In Java language, an interface can be defined as a contract between objects on how to communicate with each other

* An interface defines the methods, a deriving class (subclass) should use. But the implementation of the methods is totally up to the subclass.

