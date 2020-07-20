* Filtering, slicing, and matching
* Finding, matching, and reducing
* Using numeric streams such as ranges of numbers
* Creating streams from multiple sources
* Infinite streams

# Filtering and slicing

**Filtering with a predicate**
```
List<Dish> vegetarianMenu = menu.stream().filter(Dish::isVegetarian).collection(toList());
```
**Filtering unique elements**
> distinct that returns a stream with unique elements
```
List<Integer> numbers = Arrays.asList(1,2,3,3,2,4);
numbers.stream()
       .filter(i ->i%2 ==0)
       .distinct()
       .forEach(System.out::println)
```

**Truncating a Stream**
> Streams support the `limit(n)` method, which returns another stream that’s no longer than a given size.
```
List<Dish> dishes = menu.stream()
                        .filter(d -> d.getCalories()>300)
                        .limit(3)
                        .collect(toList())
```

**Skipping elements**
> Streams support the `skip(n)` method to return a stream that discards the first n elements.

```
List<Dish> dishes = menu.stream()
                        .filter(d -> d.getCalories()>300)
                        .skip(2)
                        .collect(toList())
```
## Mapping
> transform each element of the stream by applying a function to each element

**Applying a function to each element of a stream**
> takes a function as argument. The function is applied to each element, mapping it into a new element

```
List<String dishNames> = menu.stream()
                             .map(Dish::getName)
                             .collect(toList())
                             
                             
List<Integer> dishNameLengths = menu.stream()
                                    .map(Dish::getName)
                                    .map(String::length)
                                    .collect(toList());
```

**Flattening streams**
Question: convert a collection of collectionｓ to a collection
```
word.stream()
    .map(word -> word.split(""))//  Stream<String[]> !=  Stream<String> 
    .distinct()
    .collect(toList())
```
* Arrays.stream(): takes an array and produces a stream
```
String[] arrayOfWords = {"Goodbye", "World"};
Stream<String> streamOfwords = Arrays.stream(arrayOfWords);

word.stream()
    .map(word -> word.split(""))
    .map(Arrays.stream)// Stream<Stream<String>>
    .disinct()
    .collectionn
```

* flatMap: All the separate streams flattened into a single stream
```
word.stream()
    .map(word -> word.split(""))
    .flatMap(Arrays.stream)// mapping each array not with a stream but with the contents of that stream
    .disinct()
    .collectionn
```

*  Given two lists of numbers, how would you return all pairs of numbers? 
```
List<Integer> numbers1 = Arrays.asList(1, 2, 3);
List<Integer> numbers2 = Arrays.asList(3, 4);
List<int[]> pairs = numbers1.stream()
                            .flatMap(i -> number2.stream().map(j -> new int[]{i,j}))
                            .collect(toList())
```
# Finding and Matching
> terminal operations
## Matching
**`anyMatch()`**: Is there an element in the stream matching the given predicate
```
if(menu.stream().anyMatch(Dish::isVegetarian))
```
**`allMatch()`: if a predicate matches all elements**
```
boolean isHealthy = menu.stream().allMatch(d ->d.getCalories()<1000);
```
**`noneMatch()`:no elements in the stream match the given predicate**
```
boolean isHealthy = menu.stream().noneMatch(d ->d.getCalories()>=1000);
```
* Short-circuiting operations: The operation only needs to create a stream of a given size without processing all the elements in the stream.

## Finding

**`findAny`**:returns an arbitrary element of the current stream.
```
Optional<Dish> dish = menu.stream()
                          .filter(Dish::isVegetarian)
                          .findAny();
```
### `Optional`
>  Optional<T> class (java.util.Optional) 
*  a container class to represent the existence or absence of a value
* Optional to avoid bugs related to null checking.
  
| Method|description|
|-------|-----------|
|isPresent()| returns true if Optional contains a value, false otherwise.
|ifPresent(Consumer<T> block) |executes the given block if a value is present.it lets you pass a lambda that takes an argument of type T and returns void.
| T get()| returns the value if present; otherwise it throws a NoSuchElement-Exception.
| T orElse(T other)| returns the value if present; otherwise it returns a default value.

#### `findFirst()`
```
List<Integer> someNumbers = Arrays.asList(1, 2, 3, 4, 5); 
Optional<Integer> firstSquareDivisibleByThree = someNumbers.stream()
                                                           .map(x ->x*x)
                                                           .filter(x ->x%3 ==0)
                                                           .findFirst()
                                                           .ifPresent(d -> System.out.println(d));

```

## Reducting
> Such queries combine all the elements in the stream repeatedly to produce a single value such as an Integer.

### Sum

```
int sum = numbers.stream.reduce(0,(a,b) -> a+b)
int sum = numbers.stream.reduce(0,Integer::sum)
Optional<Integer> sum = numbers.stream().reduce((a, b) -> (a + b));
```

### Maximum and minimum
reduce takes two parameters:
1. An initial value
2. A lambda to combine two stream elements and produce a new value
```
Optional<Integer> max = number.stearm().reduce(Integer::max);
Optional<Integer> min = number.stearm().reduce(Integer::min);
```

![image](https://user-images.githubusercontent.com/27160394/87620847-3491c400-c6e5-11ea-8f16-b1e1c049bf30.png)

# Primitive stream specializations

* each Integer needs to be unboxed to a primitive before performing methods
* `IntStream`, `DoubleStream`, and `LongStream`, that respectively specialize the elements of a stream to be int, long, and double—and thereby avoid hidden boxing costs

```
int calories = menu.stream()
                   .mapToInt(Dish :: getCalroies) // return an IntStream
                   .sum()
                   
```
* Converting back to a stream of objects
```
IntStream iS = menu.stream().mapToInt(Dish::getCalories);
Stream<Integer> stream = is.boxed()
```

*  primitive specialized version of Optional: `OptionalInt`,` OptionalDouble`, and `OptionalLong.`

```
OptionalInt maxCalories = menu.stream().mapToInt(Dish::getCalories).max()
int max = maxCalories.orElse(1);
```
* Numeric ranges
> Java 8 introduces two static methods available on `IntStream` and `LongStream` to help generate such ranges: `range` and `rangeClosed`.
```
IntStream evenNumbers = IntStream.rangeClosed(1,100).filter(n -> n%2==0);
```

# Building streams

* Streams from values
```
Stream<String> stream = Stream.of("Java8","lambda","In")
stream.map(String::toUpCase).forEach(System.out::println)
```
* create empty stream
```
Stream<String> emptyStream = Stream.empty();
```

* Stream from arrays
> Arrays.stream()
```
int[] numbers  ={2,3,5,7,11,13};
int sum = Arrays.stream(numbers).sum()
```
* Streams from functions: creating infinite streams
1. Stream.iterate: apply successively a function on each new produced value.
```
Stream.iterate(new int[]{0,1},t-> new int[]{t[1],t[0]+t[1]})
      .limit(20)
      .forEach(t -> System.out.println(t))
```
2. Stream.generate: takes a lambda of type Supplier<T> to provide new value
