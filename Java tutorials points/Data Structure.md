# Data Structures in Java Utiliy package

* Enumeration
* BitSet
* Vector
* Stack
* Dictionary
* Hashtable
* Properties
---

# The Enumeration

```
public interface Ennumeration<E>{
  boolean hasMoreElements( )//it must return true while there are still more elements to extract, and false when all the elements have been enumerated.
  E nextElement( )// This returns the next object in the enumeration as a generic Object reference.
}

public static void main(String args[]) { 
      Enumeration days;
      Vector dayNames = new Vector(); 
      dayNames.add("Sunday"); 
      dayNames.add("Monday"); 
      dayNames.add("Tuesday"); 
      dayNames.add("Wednesday"); 
      dayNames.add("Thursday");
      dayNames.add("Friday"); 
      days = dayNames.elements(); 
      while (days.hasMoreElements()){
        System.out.println(days.nextElement());
     }
}

```
---
# The BitSet
> a group of bits or flags that can be set and cleared individually.

*  Useage: where you need to keep up with a set of Boolean values;

The BitSet class creates a special type of array that holds bit values. The BitSet array can increase in size as needed. This makes it similar to a vector of bits

```
public class BitSet extends Object implements Cloneable,Serializable{
        BitSet();
        BitSet(int n bits);
        void and(BitSet bitSet); //
        void andNot(BitSet bitSet);
        int cardinality( )//
        void clear( )//Zeros bits.
        void flip(int index)//Reverses the bit specified by the index.//
        boolean intersects(BitSet bitSet);
        int nextClearBit(int startIndex)//Returns the index of the next cleared bit
        void set(int index)//
        void xor(BitSet bitSet)//
        
}
```
---
# The Vector
> a growable arrat of objects

* Elements of a Vector object can be accessed via an index into the vector.

## Vector Class
Vector implements a dynamic array. It is similar to ArrayList, but with two differences:
* Vector is synchronized.
* Vector contains many legacy methods that are not part of the collections framework.

```
public class Vector<E> extend AbstractList<E> implement list<E>, RandomAccess, Cloneable, Serializable{
    protect int capacityIncrement;
    protect int elementCount;
    protect Object[] elementData;
    void add(int index, Object element)// Inserts the specified element at the specified position in this Vector.
    void addElement(Object obj)// Adds the specified component to the end of this vector, increasing its size by one.
    boolean add(Object o);
    boolean addAll(Collection c);
    int capacity();
    void clear();
    Enumeration elements(); //Returns an enumeration of the components of this vector.
    Object firstElement();
    Object lastElement();
    boolean remove(Object o);
    boolean retainAll(Collection c);
    Object[] toArray();
    List subList(int fromIndex, int toIndex);
    void trimToSize();
}
```
---
# The Stack
> represent a LIFO stack of objects

* extends class `Vector` with five operations that allow a vector to be treated as a stack
* Stack only defines the default constructor, which creates an empty stac

```
public class Stack<E> extends Vectors<E>{
     boolean empty();
     E peek();
     E pop();
     E push(E item);
     int search(Object o);
}
```
---
# The Dictionary
> an abstract parent class that defines a data structure for mapping keys to values.

* In any one Dictonary object, every key is assocaited wit at most one value
* Any non-null object can be used as a key and as a value
* the `equals` to decide if two keys are same

```
public abstract class Dictionary<K,V> extennds Object{
      Enumeration elements( ); // Returns an enumeration of the values contained in the dictionary.
      Object get(Object key)// Returns the object that contains the value associated with the key. If the key is not in the dictionary, a null object is returned.
      boolean isEmpty();
      Enumeration keys( );
      Object put(Object key, Object value);
      Object remove(Object key);
      int size( );
}
```

## The Map Interface
* Several methods throw a `NoSuchElementException` when no items exist in the invoking map.
* A `ClassCastException` is thrown when an object is incompatible with the elements in a map.
* A `NullPointerException` is thrown if an attempt is made to use a null object and null is not allowed in the map.
* An `UnsupportedOperationException` is thrown when an attempt is made to change an unmodifiable map.

```
public interface Map<K,V>{
   void clear( );
   boolean containsKey(Object k);
   boolean containsValue(Object v);
   Set entrySet( );
   boolean equals(Object obj);
   Object get(Object k);
   Object put(Object k, Object v);
   void putAll(Map m);
   Object remove(Object k);
   Collection values( );
   
}
```
## The Hashtable

```
public class Hashtable<K,V> extends Dictionary<K,V> implements Map<K,V>, Cloneable, Serializable{

     Hashtable(int size);
     Hashtable(int size, float fillRatio);
     void clear( );
     Object clone( );
     boolean contains(Object value);
     void rehash( );
     String toString( )

}
```
### The Properties
> represents a persistent set of properties

* Each key and its corresponding value in proeprty list is a String.
* The Properties can be saved t a stream or loaded from a stream

```
public class Properties extends Hashtabe<Object,Object>{
    Properties(Properties propDefault);
    String getProperty(String key);
    String getProperty(String key, String defaultProperty);
    void list(PrintStream streamOut);// Prints the property list out to specific streamOut.
    void load(InputStream streamIn) throws IOException;// Read a property list from the input stream linked to streamIn.
    Enumeration propertyNames( );// returns an enumeration of the keys. 
    Object setProperty(String key, String value); //  Calls the Hashtable method put
    void store(OutputStream streamOut, String commit); // Writes this property list in this properties table to the output stream
    void storeToXml(OutputStream streamOut, String commit); // emit an XML document representing all of the properties contained in this table
    stringPropertyNames();// return a set of String keys 
}
```
