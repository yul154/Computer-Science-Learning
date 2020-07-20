* What is a stream?
* Collections vs. streams
* Internal vs. external iteration
* Intermediate vs. terminal operations

# What is a stream?
> manipulate collections of data in a declarative way 

Question: return the names of dishes that are low in calories, sorted by number of calories,
```
List<Dish> lowClaricDishes = new ArrayList(); // filter
For (Dish d: menu){
     if (d.getCalories()<400){
         lowCalorichDishes.add(d)
     }
}

lowCalorichDishes.sort(comparing::(Dish.getCloaries())// sort

lowCalorichDishes.foreach(Dish::getName());// process the sorted list
```

Stream implementation

```
List<String> lowCaloricDishName = menu.stream()
                                              .filter(d -> d.getCalories()<400)
                                              .sorted(comparing(Dish::getCalories))
                                              .map(Dish::getName)
                                              .collection(toList())
```   

* To exploit a multicore architecture and execute this code in parallel
```
menu.parallelStream()
```

Stearm help you specify what you want to achieve (that is, filter dishes that are low in calories) as opposed to specifying how to implement an operation (using control-flow blocks such as loops and if conditions). 

To summarize of the Streams API

* Declarative— More concise and readable
* Composable— Greater flexibility
* Parallelizable— Better performance


```
List<String> ThreeHighCaloricDishes = 
  menu.stream() // get a stream from menu
      .filter(d -> d.getCalories()>300)
      .map(Dish::getName)
      .limit(3)
      .collection(toList())
```
* All these operations except collect return another stream so they can be connected to form a pipeline,
* the `collect` operation starts processing the pipeline to return a result 

<img width="359" alt="Screen Shot 2020-07-03 at 6 09 46 PM" src="https://user-images.githubusercontent.com/27160394/86500675-6192be00-bd58-11ea-8856-0114c2f06af7.png">

---

# Stream VS collections

|Collection|Stream|
|----------|------|
|A collection is an in-memory data structure that holds all the values the data structure currently has|a stream is a conceptually fixed data structure (you can’t add or remove elements from it) whose elements are computed on demand.|
|Collections are mainly used to store and group the data.| Streams are mainly used to perform operations on data.
|You can add to or remove elements from collections|Stream consumes a source, performs operations on it and returns a result. They don’t modify even the source|
|Collections have to be iterated externally.|Streams are internally iterated.|
|Collections can be traversed multiple times.|Streams are traversable only once.To traverse it again, you have to get new stream from the source again|
|Collections are eagerly constructed i.e all the elements are computed at the beginning itself.| streams are lazily constructed i.e intermediate operations are not evaluated until terminal operation is invoked.|
<img width="400" alt="Screen Shot 2020-07-03 at 6 20 55 PM" src="https://user-images.githubusercontent.com/27160394/86500889-f8ac4580-bd59-11ea-9f15-ed51b62e91b3.png">

**similarly to iterators, a stream can be traversed only once. After that a stream is said to be consumed.**
* external iteration:  iteration to be done by the user 
* Internal Iteration:  pass a function object to a method to run over a list

---
# Stream operations
> `java.util.stream.Stream`

<img width="379" alt="Screen Shot 2020-07-06 at 10 14 36 PM" src="https://user-images.githubusercontent.com/27160394/86699732-17b70b80-bfd6-11ea-8a6a-a0425dbf70fc.png">

**Intermediate operations**
* Intermediate operations return another stream as the return type
* Lazy: don’t perform any processing until a terminal operation is invoked on the stream pipeline

<img width="312" alt="Screen Shot 2020-07-06 at 10 18 54 PM" src="https://user-images.githubusercontent.com/27160394/86700383-b04d8b80-bfd6-11ea-9eec-5aeaf719b620.png">


**Terminal Operations**
* produce a result from a stream pipeline.
* A result is any nonstream value such as a List, an Integer, or even void.

<img width="333" alt="Screen Shot 2020-07-06 at 10 19 58 PM" src="https://user-images.githubusercontent.com/27160394/86700571-d4a96800-bfd6-11ea-8163-e782794bba1d.png">



