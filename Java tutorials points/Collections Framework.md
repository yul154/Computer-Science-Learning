# Collections Framework
> A unified architecture for representing and manipulating collections.
The goals of Collections framework

1. The implementations for the fundamental collections (dynamic arrays, linked lists, trees, and hashtables) were to be highly efficient.
2. The framework had to extend and/or adapt a collection easily.
3. The framework had to allow different types of collections to work in a similar manner and with a high degree of interoperability.

## Collection Interfaces
> The collections framework defines several interfaces. 

The collection interfaces are divided into two groups
 
 1. `java.utl.Collection`: 
<img width="434" alt="Screen Shot 2020-06-30 at 10 36 09 AM" src="https://user-images.githubusercontent.com/27160394/86146191-83bcdf80-babd-11ea-8de5-a0f2271efcae.png">

 2. `java.utl.Map`
 
 <img width="473" alt="Screen Shot 2020-06-30 at 10 37 00 AM" src="https://user-images.githubusercontent.com/27160394/86146270-a2bb7180-babd-11ea-82ba-901739e7692c.png">

---

# Collection interface
 > The root interface in the collection hierarchy.
 
 <img width="442" alt="Screen Shot 2020-06-30 at 12 58 44 PM" src="https://user-images.githubusercontent.com/27160394/86160498-70b40a80-bad1-11ea-9e37-f513860086ee.png">

 
 * The JDK does not provide any direct implementation of this interface;it's provide some specific subbinterfaces
 ```
 public interface Collection<E> extend Iterable<E>{
        boolean add(E e);
        boolean addAll(Collection c);
        void clear( );
        boolean contains(Object obj);
        boolean retainAll(Collection c)
        Iterator itObject[ ];
        Object[ ] toArray( );
        boolean remove(Object obj)
 }
 ```
 ---
 # The List Interface
 >  An ordered Collection
It's a subinterface of Collection 

* The user of this interface has precise control over location of elemennt insertion, and access element by index.
* A list may contain duplicate elements.

```
public interface List<E> extends Collectionn<E>{
       void add(int index, E e);
       boolean addAll(int index, Collection c);;
       Object get(int index);
       int indexOf(Object obj);
       int lastIndexOf(Object obj);
       ListIterator listIterator( )// Returns an iterator to the invoking list;
       Object set(int index, Object obj);
       List subList(int start, int end);
}
```
---
# The Set Interface
> A subinterface of Collection which contains no duplicate.

*  The Set interface contains only methods inherited from Collection and adds the restriction that duplicate elements are prohibited.
*  Set also adds a stronger contract on the behavior of the equals and hashCode operations

All Superinterfaces
1. Collection<E>
2. Iterable<E>

All subinterfaces
1. NavigableSet<E>
2. SortedSet<E>

All implementations
* AbstractSet, ConcurrentSkipListSet, CopyOnWriteArraySet, HashSet, EnumSet, LinkedHashSet, TreeSet


```
public interface Set<E> extends Collections<E>{
    add(E e);
    clear();
    contains(E e);
    iterator();
  
}
```

## SortedSet Interface
> A set that further provides a total orderinng onn its elements

* The elements are ordered using their natural ordering, or by a comparator provided at set creation time.
* All elements inserted into a sorted set must implement the `Comparable` interface
* All such elements must be mutually comparable: e1.compareTo(e2) (or comparator.compare(e1, e2)) must not throw a ClassCastException for any elements e1 and e2 in the sorted set
* Ordering maintained by a sorted set must be consistent with `equals`

All Superinterfaces:
* Collection<E>, Iterable<E>, Set<E>

All Known Subinterfaces:
* NavigableSet<E>

All Known Implementing Classes:
* ConcurrentSkipListSet, TreeSet


```
public interface SortedSet<E> extends Set<E>{
       Comparator comparator( )// Returns the comparator used to order the elements in this set, or null if this set uses the natural ordering of its elements.
       E first();
       SortedSet headSet(E end);// Returns a SortedSet containing those elements less than end that are contained in the invoking sorted set.
       E last();
       spliterator();
       SortedSet subSet(Object start, Object end);
       
}
```

---
# Map Interface
> Element that maps keys to values.

* A map cannot contain duplicate keys, each key can map to at most one value.
* It is not permissible for a map to contain itself as a key. While it is permissible for a map to contain itself as a value 
* if mutable objects are used as map keys. The behavior of a map is not specified if the value of an object is changed in a manner that affects equals comparisons while the object is a key in the map

All Known Subinterfaces:
* Bindings, ConcurrentMap<K,V>, ConcurrentNavigableMap<K,V>, LogicalMessageContext, MessageContext, NavigableMap<K,V>, SOAPMessageContext, SortedMap<K,V>

All Known Implementing Classes:
* AbstractMap, Attributes, ConcurrentHashMap, ConcurrentSkipListMap,TreeMap,WeakHashMap, EnumMap, HashMap, Hashtable, IdentityHashMap, LinkedHashMap, Properties, Provider, RenderingHints, SimpleBindings, TabularDataSupport,

```
public interface Map<K,V>{
 void clear( );
 boolean containsKey(Object k);
 boolean containsValue(Object v);
 Set entrySet( );
 Object get(Object k);
 Object put(Object k, Object v)
 boolean equals(Object obj);
 Set keySet( );//Returns a Set view of the keys contained in this map.
 Collection values( )//Returns a Collection view of the values contained in this map.
```
## The Map.Entry Interface
> key-value pair

* The `Map.entrySet()` return a collection-view of the maop
* The only way to obtain a reference to a map entry is from the iterator 
```
public static interface Map.entry<K,V>{
    boolean equals(Object obj)//
    comparactor comparingByKey()//
    comparactor comparingByValue()//
    K getKey();
    V getValue();
    V setValue(V);
}
```

## SortedMap Interface
> A Map that further provides a total ordering on its keys. 
* The map is ordered according to the natural ordering of its keys, or by a Comparator typically provided at sorted map creation time
* All keys inserted into a sorted map must implement the Comparable interface 

All Superinterfaces:
* Map<K,V>
All Known Subinterfaces:
* ConcurrentNavigableMap<K,V>, NavigableMap<K,V>
All Known Implementing Classes:
* ConcurrentSkipListMap, TreeMap

```
public interface SortedMap<K,V> extends Map<K,V>{
        Comparator comparator();
        Set enntryset();
        K firstKey();
        SortedMap headMap(K, toKey);
        Set<K> keySet();
        K lastKey();
        SortedMap subMap(K,K);
        SortedMap tailMap(K);
        Collection values()
}
```
---
# Collection Implementations
> Java provides a set of standard collection classes that implement Collection interfaces.

## List implementations

<img width="398" alt="Screen Shot 2020-06-30 at 1 03 25 PM" src="https://user-images.githubusercontent.com/27160394/86160894-17001000-bad2-11ea-9c35-1521d7e2323e.png">

### 1. The LinkedList Class

The LinkedList class extends `AbstractSequentialList` and implements the `List` interface. It provides a linked-list data structure.

```
public class LinkedList<E>
extends AbstractSequentialList<E>
implements List<E>, Deque<E>, Cloneable, Serializable{
    void add(int index, Object element);
    boolean add(Object o);
    void addFirst(Object o);
    void addLast(Object o);
    Object clone();
    Object get(int index);
    Object getFirst();
    Object getLast();
    int indexOf(Object o);
    ListIterator listIterator(int index);
    boolean remove(Object o);
    Object remove(int index);
    Object removeFirst();
    Object removeLast();
    Object set(int index, Object element);
    
}
```

### ArrayList Class
> Resizable-array implementation of the List interface

* The `size`, `isEmpty`, `get`, `set`, `iterator`, and `listIterator` operations run in constant time
* that this implementation is not synchronized

All Implemented Interfaces:
* Serializable, Cloneable, Iterable<E>, Collection<E>, List<E>, RandomAccess
Direct Known Subclasses:
* AttributeList, RoleList, RoleUnresolvedList

```
public class ArrayList<E>
extends AbstractList<E>
implements List<E>, RandomAccess, Cloneable, Serializable{
   void add(int index, Object element);
   boolean add(Object o);
   void clear();
   boolean contains(Object o);
   void ensureCapacity(int minCapacity);//Increases the capacity of this ArrayList instance, if necessary, to ensure that it can hold at least the number of elements specified by the minimum capacity argument.
   int indexOf(Object o);
   int lastIndexOf(Object o);
   Object remove(int index);
   void trimToSize();
}
```
---
## Set Implementations

<img width="394" alt="Screen Shot 2020-06-30 at 1 19 11 PM" src="https://user-images.githubusercontent.com/27160394/86162374-4d3e8f00-bad4-11ea-9a4f-535475d7b427.png">

### HashSet
> It creates a collection that uses a hash table for storage.

* It does not guarantee that the order will remain constant over time
* This class permits the null element.
* Note that this implementation is not synchronized. 

All Implemented Interfaces:
* Serializable, Cloneable, Iterable<E>, Collection<E>, Set<E>
Direct Known Subclasses:
* JobStateReasons, LinkedHashSet

```
public class HashSet<E>
extends AbstractSet<E>
implements Set<E>, Cloneable, Serializable{
   boolean add(Object o);
   void clear();
   boolean contains(Object o);
   boolean isEmpty();
   Iterator iterator();
   boolean remove(Object o);
   int size();
}
```

### LinkedHashSet
> Hash table and linked list implementation of the Set interface
* This implementation differs from HashSet in that it maintains a doubly-linked list running through all of its entries
* Insertion order is not affected if an element is re-inserted into the set.

All Implemented Interfaces:
* Serializable, Cloneable, Iterable<E>, Collection<E>, Set<E>

```
public class LinkedHashSet<E>
extends HashSet<E>
implements Set<E>, Cloneable, Serializable{
  
}
```

### TreeSet
> A NavigableSet implementation based on a TreeMap. The elements are ordered using their natural ordering,

* This implementation provides guaranteed log(n) time cost for the basic operations (add, remove and contains).
* Uses a tree for storage. Objects are stored in a sorted and ascending order.

```
public class TreeSet<E>
extends AbstractSet<E>
implements NavigableSet<E>, Cloneable, Serializable{
 void add(Object o);
 Comparator comparator();
 boolean contains(Object o);
 SortedSet headSet(Object toElement);
 SortedSet subSet(Object fromElement, Object toElement);
 SortedSet tailSet(Object fromElement);
 Object first();
 Object last();

}
```
---
## Map Implementations

<img width="355" alt="Screen Shot 2020-06-30 at 1 34 18 PM" src="https://user-images.githubusercontent.com/27160394/86163811-68120300-bad6-11ea-9fc8-a79216c52207.png">

### HashMap
> Hash table based implementation of the Map interfac

* permits null values and the null key.
* This class makes no guarantees as to the order of the map。

All Implemented Interfaces:
* Serializable, Cloneable, Map<K,V>
Direct Known Subclasses:
* LinkedHashMap, PrinterStateReasons

```
public class HashMap<K,V>
extends AbstractMap<K,V>
implements Map<K,V>, Cloneable, Serializable{
   void clear();
   boolean containsKey(Object key);
   boolean containsValue(Object value);
   Object get(Object key);
   putAll(Map m);
   Set keySet();
   Collection values();
   Object remove(Object key);
}
```
### TreeMap
> A Red-Black tree based NavigableMap implementation.

* The map is sorted according to the natural ordering of its keys, or by a Comparator provided at map creation time, depending on which constructor is used.
* This implementation provides guaranteed log(n) time cost for the containsKey, get, put and remove operations.

```
public class TreeMap<K,V>
extends AbstractMap<K,V>
implements NavigableMap<K,V>, Cloneable, Serializable{
     Object firstKey();
     Object get(Object key);
     Object lastKey();
     SortedMap subMap(Object fromKey, Object toKey);
     SortedMap tailMap(Object fromKey);
     
}
```

### WeakHashMap
> Hash table based implementation of the Map interface, with weak keys.

**Weak Reference: If the only references to an object are weak references, the garbage collector can reclaim the object's memory at any time.it doesn't have to wait until the system runs out of memory. Usually, it will be freed the next time the garbage collector runs.**

*  An entry in a WeakHashMap will automatically be removed when its key is no longer in ordinary use.

```
public class WeakHashMap<K,V>
extends AbstractMap<K,V>
implements Map<K,V>{
 
}
```

###  LinkedHashMap
> Hash table and linked list implementation of the Map interface, with predictable iteration order. 

* This implementation differs from HashMap in that it maintains a doubly-linked list running through all of its entries
* This linked list defines the iteration ordering, which is normally the order in which keys were inserted into the map (insertion-order).
```
public class LinkedHashMap<K,V>
extends HashMap<K,V>
implements Map<K,V>
```

### IdentityHashMap
> This class implements AbstractMap. It is similar to HashMap except that it uses reference equality when comparing the elements.

** Equal if and only if (k1==k2)
**This class is not a general-purpose Map implementation! While this class implements the Map interface, it intentionally violates Map's general contract, which mandates the use of the equals method when comparing objects. This class is designed for use only in the rare cases wherein reference-equality semantics are required.**

```
public class IdentityHashMap<K,V>
extends AbstractMap<K,V>
implements Map<K,V>, Serializable, Cloneable
```
---
# The Collection Algorithms

* These algorithms are defined as static methods within the Collections class.

## Search
```
static int binarySearch(List list, Object value, Comparator c)

static int binarySearch(List list, Object value)

static int indexOfSubList(List list, List subList) //Searches list for the first occurrence of subList. 

static int lastIndexOfSubList(List list, List subList)
```

## Suffling
```
static void shuffle(List list, Random r);

static void rotate(List list, int n);
```


## Sorting
```
static void sort(List list, Comparator comp);

```
## Routine Data Manipulation
```
static void copy(List list1, List list2);

static void fill(List list, Object obj);// Assigns obj to each element of the list.

static void reverse(List list);

static void swap(List list, int idx1, int idx2)

static Comparator reverseOrder( )
```

## Finding Extreme Values
```
static Object max(Collection c);
static Object max(Collection c, Comparator comp);

static Object min(Collection c, Comparator comp)
```

## Transformation
```
static Enumeration enumeration(Collection c);

static ArrayList list(Enumeration enum);

static List nCopies(int num, Object obj);//Returns num copies of obj contained in an immutable list. num must be greater than or equal to zero.

static Set singleton(Object obj);

static List synchronizedList(List list);

static List unmodifiableList(List list);
```
---
# Iterator
> enables you to cycle through a collection, obtaining or removing elements.

### Diff betweenn Iterator and Iterable
* An `Iterable` is a simple representation of a series of elements that can be iterated over. It does not have any iteration state such as a "current element". 
* Implementinng the `Iterable` interface allows an object to make use of for-each loop.
* An Iterator is the object with iteration state. It lets you check if it has more elements using hasNext() and move to the next element (if any) using next().
* Any classes implements the Iterable needs to override the Iterator() method
* Any classes implements the Iteratro needs to override `hasNext()` and `next()` methods


#### Usage

1. Obtain an iterator to the start of the collection by calling the collection's iterator( ) method.
2. Set up a loop that makes a call to hasNext( ). Have the loop iterate as long as hasNext( ) returns true.
3. Within the loop, obtain each element by calling next( ).

```
public interface Iterator<E>{
    boolean hasNext( );
    Object next( );
    void remove( );
}
```

## ListIterator
> An iterator for lists that allows the programmer to traverse the list in either direction
>> modify the list during iteration
>>> obtain the iterator's current position in the list.

```
public interface ListIterator<E>
extends Iterator<E>{
  void add(Object obj);
  boolean hasNext( );
  boolean hasPrevious( );
  int nextIndex( );
  int previousIndex( );
  Object next( );
  Object previous( );
  void remove( );
  void set(Object obj);//Assigns obj to the current element. 
  
}
```
---
# Comparator
> comparator that defines precisely what sorted order means.
#### Usage
* The Comparator interface defines two methods: compare( ) and equals( ). The compare( ) method,
```
@FunctionalInterface
public interface Comparator<T>{
    int compare(Object obj1, Object obj2)// It returns a positive value if obj1 is greater than obj2. 
    Comparator comparinf(fuction keyExtractor, comparator keycomparator)//accepts a sort key Function and returns a Comparator
    boolean equals(Object obj)
}
```
## Comparable 

* Comparable is an interface which defines a way to compare an object with other objects of the same type.This is called the class's “natural ordering”.
* the class's compareTo method is referred to as its natural comparison method.

```
public interface Comparable<T>{
    int compareTo(T o);
}
````

* Comparator interface is used to provide different ways of sorting.
* A Comparator is present in the java.util package.
* Java 8 provides new ways of defining Comparators by using lambda expressions and the comparing() static factory method.
```
Comparator<Player> byRanking = Comparator.comparing(Player::getRanking);
```
