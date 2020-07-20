# Objects in Java
* Software objects also have a state（variable） and a behavior(methods)

## Variable types in Class
* local variables: The variable will be declared and initialized within the method and the variable will be destroyed when the method has completed.
* Instance variables:  These variables are initialized when the class is instantiated. Instance variables can be accessed from inside any method
* Class variables: Class variables are variables declared within a class, outside any method, with the `static` keyword.

## Constructors
* If we do not explicitly write a constructor for a class, the Java compiler builds a default constructor for that class.
* Each time a new object is created, at least one constructor will be invoked.
* The main rule of constructors is that they should have the same name as the class
* A class can have more than one constructor.

## Singleton
>  only one instance of a class.
* Implementing Singletons
```
public class Singletonn{
  private static Singleton singleton = new Singleton();
  
  private Singleton(){};
  
  public static Singleton getInstance(){
        return singleton;
  }
  
```

```
public class ClassicSingleton {
    private static ClassicSingleton instance = null; 
    private ClassicSingleton() {
// Exists only to defeat instantiation. 
    }
    public static ClassicSingleton getInstance() { 
      if(instance == null) {
          instance = new ClassicSingleton(); 
       }
      return instance; 
    }
 }

```

## Creating an Object

Three steps to create an object
* Declaration: A variable declaration with a variable name with an object type.
* Instantiation: The 'new' keyword is used to create the object.
* Initialization: The 'new' keyword is followed by a call to a constructor. This call initializes the new object.
```
int a; //Declaration
List <Integer> lst = new arrayList<Integer>// Instantiation and Initialization
```
