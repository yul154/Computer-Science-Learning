# The Priority Queue Abstract Data Type
* This is a collection of prioritized elements that allows arbitrary element insertion, and allows the removal of the element that has first priority

|Methods|Description|
|-------|-----------|
|insert(k,v)|Creates an entry with key k and value v in the priority queue.|
|min()|Returns (but does not remove) a priority queue entry (k,v) having minimal key; returns null if the priority queue is empty.|
|removeMin()|Removes and returns an entry (k,v) having minimal key fromthe priority queue; returns null if the priority queue is empty.|
|size()|Returns the number of entries in the priority queue.|
|isEmpty()|Returns a boolean indicating whether the priority queue is empty.|


## Implementing a Priority Queue

* Composition design pattern: defining an Item class that paired each element with its associated count in our primary data structure

```
public interface Entry<K,V> {
	K getKey();
	V getValue();

}

public interface PriorityQueue<K,V> {
	int size();
	boolean isEmpty();
	Entry<K,V> insert(K key, V value) throws IllegalArgumentException;
	Entry<K,V> min();
	Entry<K,V> removeMin();

}
```

### Comparing Keys with Total Orders
> Java provides two means for defining comparisons between object types
1. define what is known as the `natural ordering` of its instances by formally implementing the `java.lang.Comparable` interface, which includes a single method `compareTo`.
2. `java.util.Comparator`interface. A comparator is an object that is external to the class of the keys it compares.It provides a method with the signature `compare(a, b)` that returns an integer
```
public class StringLengthComparator implements Comparator<String>{
       public int compare(String a, String b){
         if(a.length()<b.length()) return -1;
         else if(a.length()==b.length()) return 0;
         else return 1;
       
       }
 }
```
* Allow a user to choose any key type and to send an appropriate comparator instance as a parameter to the priority queue constructor.
```
public class DefaultComparator<E> implements Comparator<E> {
        public int compare(E a, E b) throws ClassCastException{
        	return ((Comparable<E>) a).compareTo(b);
        }
}
```

### AbstractPriorityQueue Base Class
```
public abstract class AbstractPriorityQueue<K,V> implements PriorityQueue<K, V> {
       protected static class PQEntry<K,V> implements Entry<K,V> {
    	   private K k;
    	   private V v;
    	   public PQEntry(K key, V value){
    		   k = key;
    		   v = value;
    	   }
    	   public K getKey() {return k;}
    	   public V getValue() {return v;}
    	   protected void setKey(K key) {k=key;}
    	   protected void setValue(V value) {v=value;}
		
	}
       
    private Comparator<K> comp;
    protected AbstractPriorityQueue(Comparator<K> c) {comp = c;}
    protected AbstractPriorityQueue() {this (new DefaultComparator<K>());}
    protected int compare(Entry<K,V> a , Entry<K,V> b) {
    	return comp.compare(a.getKey(), b.getKey());
    }
    protected boolean checkKey(K key) throws IllegalArgumentException{
    	try {
    		return (comp.compare(key, key)==0);
    	}catch(ClassCastException e){
    		throw new IllegalArgumentException("inncompatible key");
    	}
    }
    public boolean isEmpty() {return size() ==0;}
}
```

###  Implementing a Priority Queue with an Unsorted List
* Store entries within an unsorted linked list.
<img width="248" alt="Screen Shot 2020-08-18 at 12 07 24 PM" src="https://user-images.githubusercontent.com/27160394/90543475-61555300-e14b-11ea-8fa4-f7ffaf3f0724.png">

```
private Position<Entry<K,V>> findMin(){
	   Position<Entry<K,V>> small = list.first();
	   for(Position<Entry<K,V>> walk : list.positions())
	      if (compare(walk.getElment(),small.getElement())<0)
	    	  small = walk;
	   return small;
   }
public Entry<K,V> insert(K key, V value) throws IllegalArgumentException{
   checkKey(key);
   Entry<K,V> newest = new PQEntry<>(key, value);
   list.addLast(newest);
   return newest;
 }

public Entry<K,V> min(){
   if(list.isEmpty()) return null;
   return findMin().getElement();
 }
```

### Implementing a Priority Queue with a Sorted List

* Uses a positional list, yet maintains entries sorted by nondecreasing keys, This ensures that the first element of the list is an entry with the smallest key.

<img width="309" alt="Screen Shot 2020-08-18 at 12 20 16 PM" src="https://user-images.githubusercontent.com/27160394/90544727-2d7b2d00-e14d-11ea-9227-a4d279e0d0d5.png">

```
public Entry<K,V> insert(K key, V value) throws IllegalArgumentException{
    	  checkKey(key);
    	  Entry<K,V> newest = new PQEntry<>(key,value);
    	  Position<Entry<K, V>> walk = list.last();
    	  while(walk!=null && compare(newest,walk.getelement())<0)
    		  walk=list.before(walk);
    	  if(walk==null)
    		  list.addFirst(newest);
    	  else
    		  list.addAfter(walk, newest);
    	  return newest;
      }
```
---
# Heap
* Realization of a priority queue using a data structure called a binary heap.
* This data structure allows us to perform both insertions and removals in logarithmic time,

## The Heap Data Structure（Minmum Heap）
* In a heap T , for every position p other than the root, the key stored at p is greater than or equal to the key stored at p’s parent.
  - A minimal key is always stored at the root of T.
* Heap T satisfy an additional structural property; it must be what we term complete. 
  -  new node should be placed at a position p just beyond the rightmost node at the bottom level of the tree, 
  -  as the leftmost position of a new level,
 
* Inserting: up-heap bubbling - The upward movement of the newly inserted entry by means of swaps
```
public Entry<K, V> insert(K key, V value)throws IllegalArgumentException{
		checkKey(key);
		Entry<K, V> newest = new PQEntry<>(key,value);
		heap.add(newest);
		upheap(heap.size()-1);
		return newest;
	}
protected void upheap(int j) {
		while(j>0) {
			int p = parent(j);
			if(compare(heap.get(j),heap.get(p))>=0) break;
			swap(j,p);
			j=p;
		}
	}
```
* Removing: Down-Heap Bubbling - If p has no right child,let c be the left child of p. Otherwise (p has both children), let c be a child of p with minimal key.
```
public Entry<K, V> removeMin(){
		if(heap.isEmpty()) return null;
		Entry<K, V> ans = heap.get(0);
		swap(0,heap.size()-1);
		heap.remove(heap.size()-1);
		downheap(0);
		return ans;
	}
  
  
protected void downheap(int j) {
		while(hasLeft(j)) {
			int li = left(j);
			int si = li;
			if(hasRight(j)) {
				int ri = right(j);
				if(compare(heap.get(li),heap.get(ri))>0) {
					si= ri;
				}
			}
			if(compare(heap.get(si),heap.get(j))>=0)
					break;
			swap(j,si);
			j=si;
		}
	}
```

## Array-Based Representation of a Complete Binary Tree
> The tree are stored in an array-based list such that the element at position p is stored in A with index equal to the level number f(p) of p
- If p is the root,then f(p)=0.
- If p is the left child of position q, then f(p) = 2f(q)+1.
- If p is the right child of position q, then f(p) = 2f(q)+2.

### Java Heap Implementation

```
protected int parent(int j) {return (j-1)/2;}
protected int left(int j) {return j*2+1;}
protected int right(int j) {return j*2+2;}
protected boolean hasLeft(int j) { return left(j) < heap.size(); }
protected boolean hasRight(int j ) {return right(j) < heap.size();}
protected void swap(int i, int j) {
  Entry<K, V> temp = heap.get(i);
  heap.set(i, heap.get(j));
  heap.set(j, temp);
}
protected void upheap(int j) {}
protected void downheap(int j) {}
public Entry<K, V> min(){
  if (heap.isEmpty()) return null;
  return heap.get(0);
}

public Entry<K, V> insert(K key, V value)throws IllegalArgumentException{}
public Entry<K, V> removeMin(){}

```

* Analysis of a Heap-Based Priority Queue
<img width="268" alt="Screen Shot 2020-08-18 at 1 41 10 PM" src="https://user-images.githubusercontent.com/27160394/90552454-7ab0cc00-e158-11ea-9302-47e6a249816d.png">

### Bottom-Up Heap Construction
1. we construct (n + 1)/2 elementary heaps storing one entry each.
2. weform(n+1)/4heaps,eachstoring three entries, by joining pairs of elementary heaps and adding a new entry
3. we form (n + 1)/8 heaps, each storing 7 entries, by joining pairs of 3-entry heaps (constructed in the previous step)
4. The new entry is placed at the root and may have to be swapped with the entry stored at a child to preserve the heap-order property.

* heapify:downheap on each nonleaf position, beginning with the deepest and concluding with a call at the root of the tree.

```
 public HeapPriorityQueue(K[] keys, V[] values) {
	   super();
	   for(int j=0;j<Math.min(keys.length, values.length);j++) {
		   heap.add(new PQEntry<>(keys[j], values[j]));
		   heapify();
	   }
   }
   
protected void heapify() {
 int si = parent(size()-1);
 for(int i = si;i>=0;i--) {
   downheap(i);
 }
}
```

## Using the `java.util.PriorityQueue` Class
* the `java.util.PriorityQueue` class processes its entries according to a priority The “front” of the queue will always be a minimal element, with priori- ties based either on the natural ordering of the elements
* the `java.util.PriorityQueu`e class relies on a single element type. That element is effectively treated as a key.

<img width="301" alt="Screen Shot 2020-08-18 at 2 08 17 PM" src="https://user-images.githubusercontent.com/27160394/90554991-463f0f00-e15c-11ea-8266-abc49128a90e.png">
---
# Sorting with a Priority Queue
