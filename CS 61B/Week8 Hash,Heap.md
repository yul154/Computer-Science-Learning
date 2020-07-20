# Data Index

* if we use data as index. the run time of operstions is constant time.
### an array of booleans indexed by data
* Extremely wasteful of memory
* Need some way to generalize beyond integers.
### an array of String indexed by data
* index by first char number: Other words start with same letter.
* Use all digits by multiplying each by a power of 27: only for lowercase
```
public static int letterNum(String s, int i) {
	int ithChar = s.charAt(i);
	if ((ithChar < 'a') || (ithChar > 'z'))
        { throw new IllegalArgumentException(); }
	return ithChar - 'a' + 1;
}

public static int englishToInt(String s) {
	int intRep = 0;
	for (int i = 0; i < s.length(); i += 1) {       	
        intRep = intRep * 27;
        intRep = intRep + letterNum(s, i);
	}
	return intRep;
}

```
## ASCII Characters and String set index
* value between 0 and 127.
* 33-126 are printable
* `char c = ’D’ `is equivalent to `char c = 68`

<img width="405" alt="Screen Shot 2020-06-18 at 12 59 52 PM" src="https://user-images.githubusercontent.com/27160394/85055708-9a7d4100-b163-11ea-892c-1dbc97a863eb.png">

```
public static int asciiToInt(String s) {
	int intRep = 0;
	for (int i = 0; i < s.length(); i += 1) {       	
        intRep = intRep * 126;
        intRep = intRep + s.charAt(i);
	}
	return intRep;
}

```

* chars in Java also support character sets for other languages and symbols.

### Integer overflow
* In Java, the largest possible integer is 2,147,483,647.
  * If go over it, it starting back ovet at the smallest integer.
  
### Hashcode
* projects a value from a set with many (or even an infinite number of) members to a value from a set with a fixed number of (fewer) members.”
* Different items with same hash code will raise collsions.

## Collision handling
* Instead of storing true in position h, store a “bucket” of these N items at position h.

### implement a “bucket”
* data type
1. linkedlist
2. arraylist
3. arrayset

* Chaining data indexed array
 1. If bucket h is empty, we create a new list containing x and store it at index h.
 2. If bucket h is already a list, we add x to this list if it is not already present.

### Hash table
* Data is converted by a hash function into an integer representation called a hash code. 

<img width="367" alt="Screen Shot 2020-06-18 at 1 25 09 PM" src="https://user-images.githubusercontent.com/27160394/85058036-25ac0600-b167-11ea-9f0c-ff5e958b49c1.png">

### Peformance of hash table
* A fixed number of buckets M. An increasing number of items N.
   * Worst case runtime is now Θ(Q)

* Shorten chain list: An increasing number of buckets M and An increasing number of items N.

When N/M is ≥ 1.5, then double M(resizing) 
* N/M is often called the “load factor”. It represents how full the hash table is.


## HASH TABLE IN JAVA 
In Java, implemented as `java.util.HashMap` and `java.util.HashSet`.
  * how to compute each object’s hash code? : all objects in Java must implement `a .hashCode()` method.

* `Math.floorMod`: the floor modulus of the long arguments(negative work)

Warning #1: Never store objects that can change in a HashSet or HashMap!
Warning #2: Never override equals without also overriding hashCode.

## Computing a hashcode
* Choose a base: A typical hash code base is a small prime.

---
#  Priority Queues


```
/** (Min) Priority Queue: Allowing tracking and removal of the
  * smallest item in a priority queue. */
public interface MinPQ<Item> {
	/** Adds the item to the priority queue. */
	public void add(Item x);
	/** Returns the smallest item in the priority queue. */
	public Item getSmallest();
	/** Removes the smallest item from the priority queue. */
	public Item removeSmallest();
	/** Returns the size of the priority queue. */
	public int size();
}

```

* It only lets you interact with the smallest thing at any time


### Unharmonious Texts

> prepare a report of the M messages that seem most unharmonious using the HarmoniousnessComparator.

* Naive approach
```
public List<String> unharmoniousTexts(Sniffer sniffer, int M){
	ArrayList<Strinng> Allmessages = new ArrayList<String>();

	for (Timer timer= new timer(); timer.hour()<24){
		Allmessages.add(sniffer.getNextMessages());
	}

	Comparator<String> cmp = new HarmoniousnessComparator();
	Collections.sort(Allmessages, cmp,Collections.reverseOrder());

	return Allmessages.sublist(0,m);
	}
```
*  Priority Queues approach
```
public List<String> unharmoniousTexts(Sniffer sniffer, int M){

		Comparator<String> cmp = new HarmoniousnessComparator();

		MinnPQ<String>  unharmoniousTexts = new Heapmin<Transaction>(cmptr);

		for (Timer timer = new Timer(); timer.hours() < 24; ) {
        	unharmoniousTexts.add(sniffer.getNextMessage());
        	if (unharmoniousTexts.size()>M){
        		unharmoniousTexts.removeSmallest();
        	}

        ArrayList<String> textlist = new ArrayList<String>();
        while (unharmoniousTexts.size()>0){
        	textlist.add(unharmoniousTexts.removeSmallest());
        }

       return textlist;

	}
```
## Heaps

A max (min) heap is an array representation of a binary tree such that every node is larger (smaller) than all of its children. This definition naturally applies recursively.

* Min- heap Binary tree that is complete and obeys min-heap property.
 * Min-heap: Every node is less than or equal to both of its children.
 * Complete: Every node should have two child unless at the bottom level, all nodes are as far left as possible.
 
### Heap Operations
| Operations|Functionality|
|-----------|-------------|
getSmallest() | return the item in the root node.
add(x) | Add to end of heap and then Swim up to rightful place.
removeSmallest() | delete the root node, put the latest node into root and then sink down

###  Implementation of a Priority Queue

<img width="462" alt="Screen Shot 2020-06-19 at 11 31 28 AM" src="https://user-images.githubusercontent.com/27160394/85156968-6ddb2f00-b220-11ea-85b6-c1281fc3d172.png">

## Data Structures Summary
<img width="560" alt="Screen Shot 2020-06-19 at 11 48 02 AM" src="https://user-images.githubusercontent.com/27160394/85159167-bc89c880-b222-11ea-9b3d-42bea989bbce.png">

---

# Tries
> Short for Retrieval Tree

Suppose keys ar always Strings
* Store each letter of the string as a node in a tree.
* Nodes can be shared by multiple keys.
* Change the last of existing key as markable color

Search `Miss`
* Final node is not markable color
* if fall off th tree

> Implementation as set 

<img width="201" alt="Screen Shot 2020-06-19 at 1 37 23 PM" src="https://user-images.githubusercontent.com/27160394/85169788-0332ef00-b232-11ea-9e82-759d133e1d91.png">

> Implementation as map 

<img width="554" alt="Screen Shot 2020-06-19 at 1 38 15 PM" src="https://user-images.githubusercontent.com/27160394/85169852-22318100-b232-11ea-8132-66970e850206.png">


## Trie Implementation and Performance

Implementation
```
public class TrieSet {
  private static final int R = 128; // ASCII
  private Node root;	// root of trie

  private static class Node {
    private char ch;  
    private boolean isKey;   
    private DataIndexedCharMap next;
    private Node(char c, boolean b, int R) {
       ch = c; isKey = b;
       next = new DataIndexedCharMap<Node>(R);
    }
 }
}

public class DataIndexedCharMap<V> {
   private V[] items;// very memory hungry.
   public DataIndexedCharMap(int R) {
       items = (V[]) new Object[R];//Every node has to store R links, most of which are null.

   }
   ...
}

```
<img width="303" alt="Screen Shot 2020-06-19 at 2 03 31 PM" src="https://user-images.githubusercontent.com/27160394/85171953-a9ccbf00-b235-11ea-938c-b85c91c9ad3c.png">

### Alternate Child Tracking Strategies

1. The Hash-Table Based Trie

<img width="348" alt="Screen Shot 2020-06-19 at 2 03 53 PM" src="https://user-images.githubusercontent.com/27160394/85171980-b8b37180-b235-11ea-9f2f-f438a565e3a4.png">

2. The BST-Based Trie

<img width="344" alt="Screen Shot 2020-06-19 at 2 04 36 PM" src="https://user-images.githubusercontent.com/27160394/85172024-cff25f00-b235-11ea-95f7-8245231e128e.png">

#### Performance of the DataIndexedCharMap, BST, and Hash Table Trie 
* Using a BST or a Hash Table will take slightly more time.
  1. DataIndexedCharMap is Θ(1).
  2. BST is O(log R), where R is size of alphabet.
  3. Hash Table is O(R), where R is size of alphabet.

* Using a BST or a Hash Table to store links to children will usually use less memory.
 1. DataIndexedCharMap: 128 links per node.
 2. BST: C links per node, where C is the number of children.
 3. Hash Table: C links per node.
 4. Note: Cost per link is higher in BST and Hash Table.

Performance 
* the length of the key
* Add: Θ(L)
* Contains: O(L)

<img width="434" alt="Screen Shot 2020-06-19 at 1 51 23 PM" src="https://user-images.githubusercontent.com/27160394/85171097-f7e0c300-b233-11ea-82ec-adc2b41292c0.png">

* downside of tries: huge memory cost of storing R links per node.

## Trie String Operations

main appeal of tries is their ability to efficiently support string specific operations(prefix matching).
* 


## Autocomplete
<img width="344" alt="Screen Shot 2020-06-19 at 2 19 59 PM" src="https://user-images.githubusercontent.com/27160394/85173057-f9ac8580-b237-11ea-9f01-57b0813cdf25.png">


