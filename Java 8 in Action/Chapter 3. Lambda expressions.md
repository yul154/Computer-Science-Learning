# Lambdas in a nutshell
A lambda expression can be understood as a concise representation of an anonymous function that can be passed around: it doesn’t have a name, but it has a list of parameters, a body, a return type,

* A lambda expression is composed of parameters, an arrow, and a body.

(parameters) -> expression.

(parameters) -> { return statements; }

<img width="401" alt="Screen Shot 2020-07-02 at 7 33 06 PM" src="https://user-images.githubusercontent.com/27160394/86420047-db647200-bc9a-11ea-9e9c-112c014eff77.png">

```
(String s) -> {"Iron Man";}  // is an expression, not a statement.
(Integer i) -> return "Alan" + i;  //curly braces are required as
() -> {return "Mario";}  // correct
() -> "Raoul"  // correct
```

# Where and how to use lambdas

Where: You can use a lambda expression in the context of a functional interface

## Functional interface
>an interface that specifies exactly one abstract method.

* An interface is still a functional interface if it has many default methods as long as it specifies only one abstract method.

```
public interface Comparator<T>{
     int compare(T t1, T t2);
}

public interface Runnable{
     void run();
}
```
* Lambda expressions let you provide the implementation of the abstract method of a functional interface 
  * directly inline 
  * treat the whole expression as an instance of a functional interface 
  
* The signature of the abstract method of the functional interface essentially describes the signature of the lambda expression.


#  Putting lambdas into practice: the execute around pattern

1. Remember behavior parameterization
* Passing behavior is exactly what lambdas are for.
```
public static String processFile(BufferedReaderProcessor p) throws IOException {
    try (BufferedReader br =  new BufferedReader(new fileReader("data.txt")))
        return br.readLine() // define a behavior
}
```
2. Use a functional interface to pass behaviors
*  lambdas can be used only in the context of a functional interface
 ```
 @FunctionalInterface
public interface BufferedReaderProcessor {
    String process(BufferedReader b) throws IOException; }
 ```
 3. Execute a behavior!
```
public static String processFile(BufferedReaderProcessor p) throws IOException {
    try (BufferedReader br =  new BufferedReader(new fileReader("data.txt")))
        return p.process(br); // define a behavior
}
```
4. Pass lambdas
> Implement lambda of functional interface

```
String oneline = processFiles(BufferedReader br) -> br.readLine();
String twoLines = processFile((BufferedReader br) -> br.readLine() + br.readLine());
```
# Using functional interfaces

function descriptor:The signature of the abstract method of a functional interface

## 1. Predicate
`java.util.function.Predicate<T>`
* defines an abstract method named test that accepts an object of generic type T and returns a boolean.
```
@FunctionalInterface
public interface Predicate<T>{
  boolean test(T t); 
}

public static <T> List<T> filter(List<T> list, Predicate<T> p) { 
    List<T> results = new ArrayList<>();
    for(T s: list){
      if(p.test(s)){ results.add(s);
    } 
    }
return results; 
}
Predicate<String> nonEmptyStringPredicate = (String s) -> !s.isEmpty();
List<String> nonEmpty = filter(listOfStrings, nonEmptyStringPredicate);
```

## 2. Consumer
`java.util.function.Consumer<T>`
* defines an abstract method named `accept` that takes an object of generic type T and returns no result (void)
* Use this interface when you need to access an object of type T and perform some operations on it.

```
@FunctionalInterface
public interface Consumer<T>{
  Void accept(T t); 
}

```

## 3.Function
`java.util.function.Function<T, R>`
* defines an abstract method named `apply` that takes an object of generic type T as input and returns an object of generic type R
* Use this interface when you need to define a lambda that maps information from an input object to an output 
```
@FunctionalInterface
public interface Function<T,R>{
  R apply(T t); 
}

public static <T,R> List<R> map(List<T> list, Function<T,R> f) { 
    List<T> results = new ArrayList<>();
    for(T s: list){
       results.add(f.apply(s))
    }
    return results; 
}

List<Integer> l = map{
                       Array.asList("a","asd"), (String s) -> s.length();
}
```

<img width="473" alt="Screen Shot 2020-07-02 at 8 27 01 PM" src="https://user-images.githubusercontent.com/27160394/86422302-639a4580-bca2-11ea-99af-81055a8dc0e5.png">


# Type checking, type inference, and restrictions
>The type of a lambda is deduced from the context in which the lambda is used.

*  The type expected for the lambda expression inside the context is called the target type.
The type-checking process 
1. First, you look up the declaration of the filter method.
2. Second, it expects as the second formal parameter an object of type Predicate-<Apple> (the target type).
3. Third, Predicate<Apple> is a functional interface defining a single abstract method called test.
4. Fourth, the method test describes a function descriptor that accepts an Apple and returns a boolean.
5. Finally, any actual argument to the filter method needs to match this requirement.

**the same lambda expression can be associated with different functional interfaces if they have a compatible abstract method signature, checkingn target type to decide functional interface**

**Type inference**
> deduce an appropriate signature for the lambda because the function descriptor is available through the target type.
* when a lambda has just one parameter whose type is inferred, the parentheses surrounding the parameter name can also be omitted.
```
List<Apple> greenApples = filter(inventory, a -> "green".eqauls(a.getColor)) // omit type of a
```

**Using local variables**
capturing lambdas: lambda expressions are also allowed to use free variables (variables that aren’t the parameters and defined in an outer scope) just like anonymous classes can.
```
int portnumber = 8080;
Runnnable r = () -> System.out.println(portnumber);
```
*  Lambdas are allowed to capture (that is, to reference in their bodies) instance variables and static variables without restrictions.
     * local variables have to be explicitly declared final or are effectively final.
     * In other words, lambda expressions can capture local variables that are assigned to them only once.
```
int portnumber = 8080;
Runnnable r = () -> System.out.println(portnumber);
portnumber = 231; // portnumber is not final
```

# Method references
>  if a lambda represents “call this method directly,” 
* it’s best to refer to the method by name rather than by a description of how to call it.
* the target reference  + `::` + method name.
```
List<String> messages = Arrays.asList("hello", "baeldung", "readers!");
messages.forEach(word -> StringUtils.capitalize(word));
messages.forEach(StringUtils::capitalize);
```
## Recipe for constructing method references
1. A method reference to a static method (for example, the method parseInt of Integer, written `Integer::parseInt`)
2. A method reference to an instance method of an arbitrary type (for example, the method length of a String, written `String::length`)
3.  A method reference to an instance method of an existing object (for example, suppose you have a local variable `expensiveTransaction` that holds an object of type Transaction, which supports an instance method getValue; you can write `expensiveTransaction::getValue`)

<img width="407" alt="Screen Shot 2020-07-03 at 12 34 21 PM" src="https://user-images.githubusercontent.com/27160394/86489292-86237180-bd29-11ea-9c11-c7d1da6aeddd.png">

## Constructor references
>  create a reference to an existing constructor.

`ClassName::new`

*  each element of a List of Integers is passed to the constructor of Apple
```
List<Integer> weights = Arrays.asList(7,4,3,10);
List<Apple> apples = map(weight, Apple:new);
```
* If you have a two-argument constructor
```
BitFunction<String, Integer,Apple> c3 = Apple :: new;
Apple c3 = c3.apply("green",110);
```
---
# lambdas and method references into practice!
>  sorting a list of Apples with different ordering strategies 

1. Pass code
```
public class AppleComparator implements Comparator<Apple> {}
inventory.sort(new AppleComparator())
```
2. Use an anonymous class
```
inventory.sort(new Comparator(Apple){
   public int compare(Apple a1, Apple a2){
        return a1.getWeight().compareTo(a2.getWeight())
   }
})
```
3. Use lambda expressions
```
inventory.sort((a1, a2) -> a1.getWeight().compareTo(a2.getWeight())
```
*  `Comparator` has a static helper method called `comparing` that takes a Function extracting a Comparable key and produces a Comparator object 
```
Comparator<Apple> c =Comparator.comparing((Apple a) -> a.getWeight());
```
```
inventory.sort(comparing((a) -> a.getWeight()));
```
4. Use method references
```
inventory.sort(comparing(Apple::getWeight))
```
---
#  Useful methods to compose lambda expressions
> combine several simple lambda expressions to build more complicated ones

## Composing Comparators
Single functional comparator
```
Comparator<Apple> c =Comparator.comparing((Apple a) -> a.getWeight());
```
+ Reversed order
```
inventory.sort(comparing(Apple::getWeight.reversed())
```
Chaininnng Comparators
```
inventory.sort(comparing(Apple::getWeight
         .reversed()
         .thenComparing(Apple::getConuntry)
)
```
## Composing Predicates
Negation of a prediction
```
Predicate<Apple> noRedApple = redApple.negate();
```
And Heavy
```
Predicate<Apple> RedAndHeavyApple = redApple.and(a -> a.getWeight()>150);
```
or just green apples
```
Predicate<Apple> RedAndHeavyApple = redApple.and(a -> a.getWeight()>150)
                                            .or(a -> a.gerColor().equals("green"))
```

## Composing Functions
> two default methods, andThen and compose
`andThen`:a function that first applies a given function to an input and then applies another function to the result of that application
```
Function <Integer,Integer> g = x -> x+2;
Function <Integer,Integer> f = x -> x*2;
Function <Integer,Integer> andthen = f.andThen(g);
int res = andthen.apply(1);// res = 4 
```
`compose`:apply the function given as argument to compose and then apply the function to the result 
```
Function <Integer,Integer> g = x -> x+2;
Function <Integer,Integer> f = x -> x*2;
Function <Integer,Integer> compos = f.compose(g);
int res = compos.apply(1); // res = 6
```
* differet: the parameter of function `compose` take first but `andthen` take second


