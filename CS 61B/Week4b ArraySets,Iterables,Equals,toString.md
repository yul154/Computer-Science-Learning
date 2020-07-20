# List
> build-in `List` interface
```
List<Integer> L= new ArrayList<>();
L.add(5);
L.add(10);
L.add(15);
System.out.println(L);
```
# Set
> 
* Stores a set of values without duplicats
* Has no sense of order
```
Set<String> s = new HashSet<>();
S.add("Beijing");
S.add("Tokyo");
System.out.println(S.contansin("Tokyo"));
```
* Set can have null value

## Exceptions
> When something goes really wrong, break the normal flow of control.
### Explicit Exceptions
* `throw`:  throw our own exceptions 
  * provide more informative message to a user.
  * provide more information to code that “catches” the exception

## Iteration
* Java allows us to iterate through Lists and Sets using a shorthand syntax the “foreach” or “enhanced for” loop
* Iterator: An uglier way to iterate through a List is to use the iterator() method.
```
public interface Iterator<T> {
	boolean hasNext();
    T next();
}

```
```
Iterator<Integer> seer = javaset.iterator();
while (seer.hasNext()) {
  System.out.println(seer.next());
}
```
### Iterable
> An implementation of Iterable is one that provides an Iterator of itself

* if you claim that one class implement iterable interface
  * you must have method iterator
  
```
public interface Iterable<T>:
  {
      Iterator<T> iterator();
  }
```
## Object method:`toString()`
> provides a string representation of an object.
* `System.out.println(Object x)` calls `x.toString()`
* The implementation of `toString()` in Object is the the name of the class, then an @ sign, then the memory location of the object.
```
ArraySet@75412c2f
```
* Adding even a single character to a string creates an entirely new string
```
@Override
	public String toString() {
		String res= "{";
		for (int i=0;i<size-1;i+=1) {
			res+=items [i].toString();
			res+=",";
		}
		res+=items[size-1];
		res+="}";
		return res;
	}
```
*  Append operation for a StringBuilder is fast.
```
@Override
	public String toString() {
		StringBuilder res= new StringBuilder("{");
		for (int i=0;i<size-1;i+=1) {
			res.append(items [i].toString());
			res.append(",");
		}
		res.append(items[size-1]);
		res.append("}");
		return res.toString();
	}
```
* `String.join`: concatenates the given elements with the delimiter and returns the concatenated string
```
@Override
public String toString() {
    List<String> listOfItems = new ArrayList<>();
    for (T x : this) {
        listOfItems.add(x.toString());
    }
    return "{" + String.join(", ", listOfItems) + "}";
}
```
* `.of`: static method for Map，List，Set
```
 List<String> list = List.of("a", "b", "c", "d");
        System.out.println(list);
```



## Object method: `equals(Object obj)`
* == compares the bits. For references == means “referencing the same object.”
* `.equal(Ojbect)` to test equality in the sense 

```
@Override
public boolean equals(Object o) {
  if (o == null) { return false; }
  if (this == o) { return true; } // optimization
  if (this.getClass() != o.getClass()) { return false; }
  ArraySet<T> other = (ArraySet<T>) o;
  if (this.size() != other.size()) { return false; }
    for (T item : this) {
      if (!other.contains(item)) {
        return false;
      }
    }
  return true;
}
```
