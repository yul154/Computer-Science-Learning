# Java 8: why should you care?

CPUs have become multicore, but the vast majortiry of Java programs use only a small fractio of them


**Stream processing**

Stream is a sequence of data items that are conceptually produced one at a time
* Streams API has many methods that can be chained to form a complex pipeline
* Java 8 can transparently run pipeline of Stream operations on several CPU cores on disjoint parts of the input.
* external iteration : terate through each element one by one using a for-each loop and then process the elements
* internal iteration :The data processing happens internally inside the library.


**Passing code to methods with behavior parameterization**
* Pass methods (your code) as arguments to other methods
* Java 8 decided to allow methods to be values(Method references,lambda expression)


**default methods**
you can update an interface only if you update all the classes that implement it — a logistic nightmare! 
* an interface can now contain method signatures for which an implementing class doesn’t provide an implementation

**Optional<T> class**
help you avoid NullPointer exceptions. It’s a container object that may or not contain a value
* Optional<T> includes methods to explicitly deal with the case where a value is absent, and as a result you can avoid NullPointer exceptions. 
* it uses the type system to allow you to indicate when a variable is anticipated to potentially have a missing value
---
# Passing code with behavior parameterization
Behavior parameterization:  taking a block of code and making it available without executing it,This block of code can be called later by other parts of your programs.
 
## Coping with changing requirements
1.  First attempt: filtering green apples
```
public static List<Apple> filterGreenApple(List<Apple> inventory){
      List<Apple> res = new ArrrayList<>();
      For(Apple apple : inventory){
          if("green".euqals(apple.Getcolor())){
              res.add(apple);
          }
      }
}
```

2. parameterizing requirements
  
```
public static List<Apple> filterGreenApple(List<Apple> inventory, String color){
      List<Apple> res = new ArrrayList<>();
      For(Apple apple : inventory){
          if(color.euqals(apple.Getcolor())){
              res.add(apple);
          }
      }
}

public static List<Apple> filterApplesByWeight(List<Apple> inventory, int weight) {
          List<Apple> result = new ArrayList<>(); 
          For (Apple apple: inventory){
                if ( apple.getWeight() > weight ){ result.add(apple);
          }
          return result; 
}
```
  *  duplicate most of the implementation for traversing the inventory and applying the filtering criteria on each apple

3. filtering with every attribute you can think of
```
public static List<Apple> filterApples(List<Apple> inventory, String color, int weight, boolean flag)//add a flag to differentiate between color and weight queries. 
```
  * The client code looks terrible.
  * this solution doesn’t cope well with changing requirements. 
  
  
## Behavior parameterization

4. Prediction
* model your selection criteria, returning a boolean based on some attributes of Apple**
```
public interface ApplePredicate{
     boolean test(Apple apple);
}

public class AppleHeavyWeightPredicate implements ApplePredicate{
     public boolean test(Apple apple){
         return apple.getWeight()>150;// selectio criteria
     }
}

public class AppleColorPredicate implements ApplePredicate{
     public boolean test(Apple apple){
         return apple.getColor().euqals("green");
     }
}
```
These criteria as different behaviors for the filter method.

* behavior parameterization: the ability to tell a method to take multiple behaviors (or strategies) as parameters and use them internally to accomplish different behaviors.

5. filtering by abstract criteria
```
public static List<Apple> filterApple(List<Apple> inventory, ApplePredicate p){
      List<Apple> res = new ArrrayList<>();
      For(Apple apple : inventory){
          if(p.test(apple)){
              res.add(apple);
          }
      }
      return res;
}

public class AppleRedAndHeavyPredicate implements ApplePredicate{ 
    public boolean test(Apple apple){
            return "red".equals(apple.getColor()) && apple.getWeight() > 150;
} 
}
List<Apple> redAndHeavyApples = filter(inventory, new AppleRedAndHeavyPredicate());
```
*  the behavior of the filterApples method depends on the code you pass to it via the ApplePredicate object.
*  Parameterized the behavior of the filterApples method!

## Tackling verbosity

Verbosity
1. declare several classes that implement the ApplePredicate interface
2. then instantiate several ApplePredicate objects that you allocate only once,

### Anonymous classes
>  declare and instantiate a class at the same time
6.  using an anonymous class
```
List<Apple> redApples = filterApples(inventory, new ApplePredicate()){// parameterizing the behavior without name inline
        public boolean test(Apple apple){
             returnn "red".euqals(apple.getColor());
        }
}
```
7. using a lambda expression
```
List<Apple> res = filterApples(inventory,(Apple apple)) -> "red".euqals(apple.getColor());
```
8. abstracting over List type

```
public interface Predicate<T>{
     boolean test(T t);
}

public static List<T> filter(List<T> list, Predicate<T> p)
```
## Real-world examples
### 1. Sorting with a Comparator
```
public interface Comparator<T> {
    public int compare(T o1, T o2); 
}

inventory.sort(new Comparator<Apple>(){// anonymous class
      public int compare(Apple a1,Apple a2){
         return a1.getWeight().compareTo(a2.getWeight());
      }
})

inventory.sort(Apple a1, Apple a2) -> a1.getWeight().compareTo(a2.getWeight()));

```

### 2. Executing a block of code with Runnable
*  In Java, you can use the Runnable interface to represent a block of code to be executed
```
public interface Runnable{
    public void run();
}

Thread t = new Thread(new Runnable(){
     public void run(){
          System.out.println("Hello world");
     }
});

Thread t = new Thread(() -> System.out.println("Hello world"));
```

### 3. GUI event handling
* In JavaFX you can use an EventHandler to represent a response to an event by passing it to setOnAction:
```
Button button = new Button("Send"); 
button.setOnAction(new EventHandler<ActionEvent>() {
    public void handle(ActionEvent event) { 
    label.setText("Sent!!");
} 
});

button.setOnAction(ActinonEvent event) -> label.setText("Sent!!")
```
