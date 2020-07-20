# List ADT

```
public interface list<E> {
	
	/** Returns the number of elements in this list. */
	int size();
	
	/** Returns whether the list is empty. */
	boolean isEmpty();
	
	/** Returns (but does not remove) the element at index i. */
	E get(E e) throws IndexOutOfBoundsException;
	
	/** Replaces the element at index i with e, and returns the replaced element. */
	E set(int i,E e) throws IndexOutOfBoundsException;
	
	
	/** Inserts element e to be at index i, shifting all subsequent elements later. */
	void add(int i, E e) throws IndexOutOfBoundsException;
	
	/** Removes/returns the element at index i, shifting subsequent elements earlier. */
	E remove(int i) throws IndexOutOfBoundsException;
	

}
```

## Array Lists
>  an array-based list to have unbounded capacity

* Methods add(i, e) and remove(i) are more time consuming, as they require shifting elements up or down

```
public void add(int i, E e) throws IndexOutOfBoundsException{
		checkIndex(i, size);
		if(size==list.length) {
			throw new IllegalStateException ("Array is full");
		}
		for (int j=size;j>=i;j--) {
			list[j]=list[j-1];
		}
		list[i]=e;
		
	}
	public E remove(int i) throws IndexOutOfBoundsException {
		checkIndex(i, size);
		E tmp = list[i];
		for (int j=i;j<size-1;j++) {
			list[j]=list[j+1];
		}
		list[size-1]=null;
		return tmp;
	}
	
```

### The Performance of a Simple Array-Based Implementation

<img width="229" alt="Screen Shot 2020-06-24 at 11 02 51 PM" src="https://user-images.githubusercontent.com/27160394/85651890-d5550c80-b66e-11ea-9458-e983b7139bae.png">

## Dynamic Arrays

*  ArrayList implementation requires that a fixed maximum capacity be declared,

* Dynamic Arrays maintains an internal array that often has greater capacity than the current length of the list.

### Implementing a Dynamic Array

1. Allocate a new array B with larger capacity.
2. SetB[k]=A[k],fork=0,...,n−1,where n denotes current number of items.
3. Set A = B, that is, we henceforth use the new array to support the list.
4. Insert the new element in the new array.

<img width="433" alt="Screen Shot 2020-06-24 at 11 12 15 PM" src="https://user-images.githubusercontent.com/27160394/85652366-26193500-b670-11ea-9c51-b14d158680d3.png">

```
protected void resize(int capacity) {
  E[ ] temp = (E[ ]) new Object[capacity]; // safe cast; compiler may give warning 
  for (int k=0; k < size; k++)
  	temp[k] = data[k];
  data = temp; // start using the new array
}

public void add(int i, E e) throws IndexOutOfBoundsException {
  checkIndex(i, size + 1);
  if (size == data.length) // not enough capacity
  resize(2 ∗ data.length);
  // rest of method unchanged.
```
---
# Positional Lists

* achieved constant time insertions and deletions at arbitrary locations

## Positions

`getElement()`:Returns the element stored at this position.

* A position p, which is associated with some element e in a list L, does not change, even if the index of e change in L due to insertion or deletion
* The positions in a positional list should always be defined relative to their neighboring positions, not their indices
## The Positional list ADT

* Positonnal list as a collection of positions, each of which stores an elements

```
first( )//Returns the position of the first element of L (or null if empty). 
last()// Returns the position of the last element of L (or null if empty).
before(p): //Returns the position of L immediately before position p (or null if p is the first position).
after(p)://Returns the position of L immediately after position p (or null if p is the last position).
isEmpty():
size():
```
Traverse a list
```
Position<String> cursor = guest.first();
While(cursor!=null){
   cursor = guests.after(cursor);
}
```


### Interface Definitions
```
public interface PositionalList<E> {
	
	int size();
	
	boolean isEmpty();
	
	Position<E> first();
	
	Position<E> last();
	
	/** Returns the Position immediately before Position p (or null, if p is first). */
	Position<E> before(PositionalList<E> p) throws IllegalArgumentException;
	
	Position<E> after(PositionalList<E> p) throws IllegalArgumentException;
	
	/** Inserts element e at the front of the list and returns its new Position. */
	Position<E> addFirst(E e);
	
	Position<E> addLaist(E e);
	
	/** Inserts element e immediately before Position p and returns its new Position. */
	Position<E> addBefore(Position<E> P, E e) throws IllegalArgumentException;
	
	Position<E> addAfter(Position<E> P, E e) throws IllegalArgumentException;

	E set(Position<E> p, E e) throws IllegalArgumentException;
     
	/** Removes the element stored at Position p and returns it (invalidating p). */
	E remove(Position<E> p) throws IllegalArgumentException;

}
```

### Doubly Linked List Implementation

**The Performance of a Linked Positional List**
<img width="330" alt="Screen Shot 2020-07-02 at 11 35 34 AM" src="https://user-images.githubusercontent.com/27160394/86387002-26a96100-bc58-11ea-97e9-ce0bafe6433b.png">


### Implementing a Positional List with an Array

Instead of storing the elements of L directly in array A, we store a new kind of position object in each cell of A. A position p stores the element e as well as the current index i of that element within the list

<img width="300" alt="Screen Shot 2020-07-02 at 11 34 49 AM" src="https://user-images.githubusercontent.com/27160394/86386936-0aa5bf80-bc58-11ea-8dc6-8397972f043a.png">

---
# Iterators
> a software design pattern that abstracts the process of scanning through a sequence of elements, one element at a time.

**`java.util.Iterator`
```
hasNext(): Returns true if there is at least one additional element in the sequence, and false otherwise.
next(): Returns the next element in the sequence.
remove(): Removes from the collection the element returned by the most recent call to next(). Throws an IllegalStateException if next has not yet been called, or if remove was already called since the most recent call to next.
```
## Iterable interface

**Cons of iterator**
* A single iterator instance supports only one pass through a collection
* calls to next can be made until all elements have been reported, but there is no way to “reset” the iterator back to the beginning of the sequence.

Interable interface:  
1. A data structure that wishes to allow repeated iterations can support a method that returns a new iterator, each time it is called
2. Each call to iterator() returns a new iterator instance, thereby allowing multiple (even simultaneous) traversals of a collection.
3. Java’s Iterable class also plays a fundamental role in support of the “for-each” loop syntax 
```
for (ElementType variable : collection) {
     loopBody // supported for any instance, collection, of an iterable class
}

Iterator<ElementType> iter = collection.iterator(); 
while (iter.hasNext()) {
	ElementType variable = iter.next();
	loopBody // may refer to ”variable”
}

```
## Implementing Iterators

There are two general styles for implementing iterators
1. A snapshot iterator : maintains its own private copy of the sequence of elements,is therefore unaffected by any subsequent changes to the primary collection that may occur. it requires O(n) time and O(n) auxiliary space
2. A lazy iterator is one that does not make an upfront copy, performing a piecewise traversal of the primary structure. the iterator requires only O(1) space and O(1) construction time, its behavior is affected if the primary structure is modified (by means other than by the itera- tor’s own remove method) before the iteration completes

* Iterations with the ArrayList class
```
public class ArrayIterator implements Iterator<E> {
	
	private int cur = 0 ;
	private boolean removable = false;
	
	public boolean hashNext() {return cur <size;}
	
	public E next() throws NoSuchElementException{
		if (cur == size) throw new NoSuchElementException("no next");
		removable = true;
		return data[cur++];
	}
	
	public void remove() throws IllegalStateException{
		if(!removable) throw new IllegalStateException("nothing to remove");
		Arraylist.this.remove(cur-1);
		cur--;
		removable = false;
	}

}
```
---
# The Java Collections Framework

* The root interface in the Java collections framework is named `Collection`
* Robust classes provide support for concurrency, allowing multiple processes to share use of a data structure in a thread-safe manner.
* Blocking: retrieve an element from an empty collection waits until some other process inserts an element

<img width="474" alt="Screen Shot 2020-07-02 at 12 20 32 PM" src="https://user-images.githubusercontent.com/27160394/86390856-6d9a5500-bc5e-11ea-9ce3-67e3ce0cf9e9.png">

* if a java.util.LinkedList object L has returned five different iterators and one of them modifies L, a ConcurrentModificationException is thrown if any of the other four is subsequently used.

## List-Based Algorithms in the Java Collections Framework

* copy(Ldest , Lsrc): Copies all elements of the Lsrc list into corresponding in- dices of the Ldest list
* disjoint(C, D):Returns a boolean value indicating whether the collections C and D are disjoint.
* fill(L, e): Replaces each element of the list L with element e.
* frequency(C, e):Returns the number of elements in the collection C that are equal to e.
* max(C):
* min(C):
* replaceAll(L, e, f ):Replaces each element in L that is equal to e with element f .
* reverse(L):
* rotate(L, d):Rotates the elements in the list L by the distance d (which can be negative), in a circular fashion.
* shuffle(L):Pseudorandomly permutes the ordering of the elements in the list L.
* sort(L): 
* swap(L, i, j):Swap the elements at indices i and j of list L.

## Converting between Lists and Arrays

```
toArray(): Returns an array of elements of type Object containing all the elements in this collection.
toArray(A): Returns an array of elements of the same element type as A containing all the elements in this collection.
asList(A): Returns a list representation of the array A, with the same element type as the elements of A.
```
