# Stacks

* A stack is a collection of objects that are inserted and removed according to the last-in, first-out (LIFO) principle
* only access or remove the most recently inserted object that remains (at the so-called “top” of the stack)


## `java.util.Stack` Class

- Java’s Stack class remains only for historic reasons, and its interface is not consistent with most other data structures in the Java library.
- In fact, the current documentation for the Stack class recommends that it not be used,
- LIFO functionality (and more) is provided by a more general data struc- ture known as a double-ended queue (which we describe in Section 6.3).
- methods `pop` and `peek` of the java.util.Stack class throw a custom EmptyStackException


## The Stack Abstract Data Type


|methods| descriptions|
|-------|-------------|
| push(e)|Adds element e to the top of the stack|
| pop()|Removes and returns the top element from the stack (or null if the stack is empty)
| top()|Returns the top element of the stack, without removing it (or null if the stack is empty).|
|size()|Returns the number of elements in the stack.|
|isEmpty()|Returns a boolean indicating whether the stack is empty.|


### Array-based Stack
```
public class ArrayStack<E> implements Stack<E> {
	public static final int capatical = 1000;
	private int size = 0 ;
	private E[] stack;
	
	public ArrayStack(){this(capatical);}
	
	public ArrayStack(int length) {
		stack = (E[]) new Object[length];
	}
	
	public int size() {return size;};
	
	public boolean isEmpty() {
		return size==0;
	}
	
	
	public void push(E e) throws IllegalStateException {
		if (size() == stack.length) throw new IllegalStateException("Stack is full");
		stack[++size]=e;
	}
	
	public E top() {
		if (isEmpty()) {
			return null;
		}
		return stack[size-1];
	}
	public E pop() {
		if (isEmpty()) return null;
		E res = stack[size-1];
		stack[size-1]=null;
		size--;
		return res;
	}

}
```

#### Analyzing the Array-Based Stack Implementation
* Drawback: it relies on a fixed-capacity array
* each method runs in constant time, that is, they each run in O(1) time.

### Linkedlist-based Stack

#### The Adapter Pattern
Purpose: we effectively want to modify an existing class so that its methods match those of a related, but different, class or interface.

- One general way to apply the adapter pattern
  1. Define a new class in such a way that it contains an instance of the existing class as a hidden field
  2. Implement each method of the new class using methods of this hidden instance variable.
  
```
public class LinkedStack<E> implements Stack<E> {
    private SinglyLinkedList<E> list = new SinglyLinkedList<>(); // an empty list
    public LinkedStack() { } // new stack relies on the initially empty list
    public int size() { return list.size(); }
    public boolean isEmpty() { return list.isEmpty(); }
    public void push(E element) { list.addFirst(element); }
    public E top() { return list.first(); }
    public E pop() { return list.removeFirst(); }
 }
```
### Matching Delimiters

```
public static boolean isHTMLMatched(String html) {
		Stack<String> stack = new ArrayStack<>();
		int i = html.indexOf('<');
		while(i!=-1){
			int j = html.indexOf('>', i+1);
			if (j==-1)
				return false;
			String tag = html.substring(i+1, j);
			if (! tag.startsWith("/")) {
				stack.push(tag);
			}else {
				if (stack.isEmpty()) {
					return false;
				}else {
					if (!tag.substring(1).equals(stack.pop())) {
						return false;
								
					}
				}
			}
			
			i=html.indexOf('<', j+1);
		}
		return true;
	}
```
----
# Queue
> a collection of objects that are inserted and removed according to the first-in, first-out (FIFO) principle

* elements enter a queue at the back and are removed from the front.

## The Queue Abstract Data Type

|methods| descriptions|
|-------|-------------|
|enqueue(e)|Adds element e to the back of queue.|
|dequeue()|Removes and returns the first element from the queue (or null if the queue is empty).|
| first()|Returns the first element of the queue, without removing it (or null if the queue is empty).|
|size()|Returns the number of elements in the queue.|
|isEmpty()|Returns a boolean indicating whether the queue is empty.|

```
public interface Queue<E> {
	/** Returns the number of elements in the queue. */
	int size();
	
	/** Inserts an element at the rear of the queue. */
	void enqueue(E e);
	
	/** Tests whether the queue is empty. */
	boolean isEmpty();
	
	/** Removes and returns the first element of the queue (null if empty). */
	E dequeue();
	
	/** Returns, but does not remove, the first element of the queue (null if empty). */
	E first();	
}
```
### `java.util.Queue` Interface

<img width="442" alt="Screen Shot 2020-06-24 at 11 20 09 AM" src="https://user-images.githubusercontent.com/27160394/85593446-aad26780-b60c-11ea-89b7-800ab1552281.png">

###  Array-Based Queue Implementation

```
	public static final int CAPACITY = 1000;
	private E[] queue;
	private int f =0;
	private int size =0;
	
	public ArrayQueue() {this(CAPACITY);}
	public ArrayQueue(int length) {
		queue = (E[]) new Object[length];
	}
	
	public int size() {return size;}
	
	public boolean isEmpty() {return size==0;}
	
	public E first() {
		if (isEmpty()) {
			return null;
		}
		return queue[f];
	}
	
	public void enqueue(E e) throws IllegalStateException{
		if (size==queue.length) {
			throw new IllegalStateException("full");
		}
		int id = (f+size)%queue.length;
		
		queue[id]=e;
		size+=1;
				
	}
	
	public E dequeue() {
		if(isEmpty()) {
			return null;
		}
		E res = queue[f];
		queue[f]=null;
		f=(f+1)&queue.length;
		size--;
		return res;
	}
}
```
*  each method in this implementa- tion runs in O(1) time.
* The space usage is O(N)(array size)

### Implementing a Queue with a Singly Linked List

```
public class LinkedQueue<E> implements Queue<E> {
  private SinglyLinkedList<E> list = new SinglyLinkedList<>(); // an empty list 
  public LinkedQueue() { } // new queue relies on the initially empty list 
  public int size() { return list.size(); }
  public boolean isEmpty() { return list.isEmpty(); }
  public void enqueue(E element) { list.addLast(element); } 
  public E first() { return list.first(); }
  public E dequeue() { return list.removeFirst(); }
}
```
* Linked list uses more space per element than a properly sized array of references.


### A Circular Queue with The Josephus Problem

Josephus Problem
*  every kth person is removed from the circle, for some fixed value k
*  determining the winner for a given list of children

```
public static <E> E Josephus(CircularQueue<E> queue, int k) {
		if(queue.isEmpty()) return null;
		while (queue.size()>1) {
			for(int i =0; i<k;i++) {
				 queue.rotate();
			}
			E e = queue.dequeue();
			System.out.println(" " + e +" is out");
		}
		return queue.dequeue()l
		
	}
```

### Double-Ended Queues
>  supports insertion and deletion at both the front and the back of the queue.

#### The Deque Abstract Data Type

|methods| descriptions|
|-------|-------------|
|addFirst(e)|Insert a new element e at the front of the deque.|
|addLast(e)| Insert a new element e at the back of the deque.|
|removeFirst()|Remove and return the first element of the deque (or null if the deque is empty).|
|removeLast()|Remove and return the last element of the deque (or null if the deque is empty).|
```
public interface Deque<E> {
	
	/** Returns the number of elements in the deque. */
	int size();
	
	/** Tests whether the deque is empty. */
	boolean isEmpty();
	
	/** Returns, but does not remove, the first element of the deque (null if empty). */
	E first();
	
	/** Returns, but does not remove, the last element of the deque (null if empty). */
	E last();
	
	/** Inserts an element at the front of the deque. */
	void addFirst(E e);
	
	/** Inserts an element at the back of the deque. */
	void addLast(E e);
	
	/** Removes and returns the first element of the deque (null if empty). */
	E removeFirst();
	
	/** Removes and returns the last element of the deque (null if empty). */
	E removeLast();
}
```
### Deques in the Java Collections Framework

* The Java Collections Framework includes its own definition of a deque, as the `java.util.Deque` interface
* several implementations of the deque interface including one based on use of a circular array (`java.util.ArrayDeque`) and one based on use of a doubly linked list (`java.util.LinkedList`).

<img width="441" alt="Screen Shot 2020-06-24 at 12 16 39 PM" src="https://user-images.githubusercontent.com/27160394/85602020-9003f100-b614-11ea-9297-15fd7ec07278.png">
