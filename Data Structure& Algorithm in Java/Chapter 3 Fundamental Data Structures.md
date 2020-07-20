# Using Arrays
## Sorting in array
### 1. Insertion-sort
* considering one element at a time
* start with the first element in the arra
* When considering the next element in the array, if it is smaller than the first, we swap them
* Next we consider the third element in the array
* Swapping it leftward until it is in its proper order relative to the first two elements
```
public static void insertSort(char[] data) {
		int n=data.length;
		for (int i=0;i<n;i++) {
			char cur= data[i];
			int j=i;
			while (j>0 && data[j-1]>cur) {
				data[j]=data[j-1];
				j--;
			}
			data[j]=cur;
		}
	}
```

## `java.util` Methods for Arrays and Random Numbers
<img width="566" alt="Screen Shot 2020-06-17 at 7 00 15 PM" src="https://user-images.githubusercontent.com/27160394/84962578-c994a380-b0cc-11ea-8c09-27614c8135db.png">

### PseudoRandom Number Generation
* ` java.util.Random`: whose instances are pseudorandom number generators
* `seed`:such a generator always needs a place to start
```
public static void main(String[] args) {
		int[] data= new int[10];
		Random rand= new Random();
		rand.setSeed(System.currentTimeMillis());//set the seed to the current time in milliseconds
		for (int i=0;i<data.length;i++) {
			data[i]=rand.nextInt();
		}
		int[] orig= Arrays.copyOf(data, data.length);
		System.out.println("arrays equal before sort: "+Arrays.equals(data, orig));
		Arrays.sort(data);
		System.out.println("arrays equal after sort: " + Arrays.equals(data, orig)); 
		System.out.println("orig = " + Arrays.toString(orig));
		System.out.println("data = " + Arrays.toString(data));
		
	}
```
  
# Simple Cryptography with Character Arrays
* plaintext:  This field involves the process of encryption, in which a message
* ciphertext: converted into a scrambled message 
* decryption: turning a ciphertext back into its original plaintext.

##  Converting Between Strings and Character Arrays
```
S="bird";
A= S.toCharArray( )
// A={'b', 'i', 'r', 'd'}.
```

## Two-Dimensional Arrays and Positional Games
* The first index usually refers to a row number and the second to a column number
* matrix: We can create a two-dimensional array as an array of arrays
```
int [][] data =new int[8][10];// 8 rows and 10 columns
```

# Singly Linked Lists
> a collection of nodes that collectively form a linear sequence
*  it does not have a predetermined fixed size

* Node: stores a reference to an object that is an element of the sequence, as well as a reference to the next node of the list
<img width="307" alt="Screen Shot 2020-06-18 at 5 30 42 PM" src="https://user-images.githubusercontent.com/27160394/85078174-72a0d400-b189-11ea-91b3-8faa41d79014.png">

* Head:  the linked list instance must keep a reference to the first node of the list
* Tail:  the node having null as its next reference

## Operations of Linked list
* Insert at the head

```
new = Node(value);
new.next= head;
head= new
size+=1;
```
* Insert at the tail
```
new =Node(value);
new.next= null;
tai.next=new;
tail=new;
size+=1;
```
* Remove at the head
```
if (head==null){
    return;
}
head=head.next;
size-=1
```
## Implement Linked list

* nested classes: 
  1. provides strong encapsulation,
  2. shielding users of our class from the un- derlying details 
  3. differentiate this node type from forms of nodes
```
public class SingleLinkedList {
	
	private static class Node<E>{
		private E element;
		private Node<E> next;
		public Node(E e, Node<E> n){
			element= e;
			next = n;
		}
		
		public E getElement() {return element ;};
		
		public Node<E> getnext(){return next;}
		
		public void setnext(Node<E> n) {next = n;}
	}

}

```
```
private Node<E> head =null;
	private Node<E> tail = null;
	private int size=0;
	public SingleLinkedList() {};
	public int size() {return size;}
	public boolean isEmpty() {return size==0;}
	public E first() {
		if (isEmpty()) {return null;}
		return head.getElement();
	}
	
	public void addFirst(E e) {
		head = new Node<>(e, head);
		if (size==0) {
			tail=head;
		}
		size+=1;
	}
	
	public void addLast(E e) {
		Node<E> newest = new Node<> (e,null);
		if (isEmpty()) {
			head=newest;
		}else {
			tail.setnext(newest);
		}
		newest=tail;
		size++;
	}
	
	public E removeFirst() {
		if (isEmpty()){return null;}
		E first = head.getElement();
		head= head.getnext();
		size--;
		if (size==0) {
			tail =null;
		}
		return first;
	}
```

## Circularly Linked Lists
> well-defined neighboring relationships, but no fixed beginning or end.

### Round-Robin Scheduling
* time slice: A process is given a short turn to execute,but it is interrupted when the slice ends

<img width="315" alt="Screen Shot 2020-06-18 at 6 00 11 PM" src="https://user-images.githubusercontent.com/27160394/85079931-90703800-b18d-11ea-9a68-c7e1723a386a.png">

### Designing and Implementing a Circularly Linked List


## Doubly Linked Lists

* drawback of single linked list: unable to efficiently delete a node at the tail of the list 
  * Solution: each node keeps an explicit reference to the node before it and a reference to the node after it

* add special nodes (sentinels) at both ends of the list: 
  * a header node at the beginning of the list
  * a trailer node at the end of the list
  
<img width="565" alt="Screen Shot 2020-06-18 at 6 08 25 PM" src="https://user-images.githubusercontent.com/27160394/85080416-b6e2a300-b18e-11ea-8bb3-a7c9150ea8ea.png">

###  Advantage of Using Sentinels

* the header and trailer nodes never change—only the nodes between them change.
* we can treat all insertions in a unified manner
* Every element that is to be deleted is guaranteed to be stored in a node that has neighbors on each side.

### Implementing a Doubly Linked List Class

* Methods
<img width="400" alt="Screen Shot 2020-06-18 at 6 11 22 PM" src="https://user-images.githubusercontent.com/27160394/85080559-2062b180-b18f-11ea-9ac9-37d11d690391.png">

* Nested class: Node
```
private static class Node<E>{
		
		private Node<E> pre;
		private Node<E> next;
		private E element;
		
		public Node (E e, Node p, Node n) {
			element =e;
			pre= p;
			next = n;
		}
		public E getElement() {return element;}
		public Node<E> getNext(){return next;}
		public Node<E> getPre(){return pre;}
		public void setNext(Node<E> n ) {next = n;}
		public void setPre(Node<E> p ) {pre = p;}
	}
```

* List implementation
```
private Node<E> header;
private Node<E> trailer;
private int size = 0;
/∗∗ Constructs a new empty list. ∗/ 
public DoublyLinkedList( ) {
	header = new Node<>(null, null, null); 
	trailer = new Node<>(null, header, null); 
	header.setNext(trailer);
}
public int size() { return size; }
/∗∗ Tests whether the linked list is empty. ∗/
public boolean isEmpty() { return size == 0; }

public E first(){
	}
```

## Equivalence Testing


` a.equals(b)`
*  serves as a superclass for all reference types
* `equals` : to compare the state of two objects or contents of the object.
  * default implementation of equals() method work like == means it will check the memory reference of the object 
  * The author of each class has a responsibility to provide an implementation of the equals method, which overrides the one inherited from Object
* `==`: whether a and b refer to the same object 

### Equivalence Testing with Arrays

<img width="470" alt="Screen Shot 2020-06-18 at 6 30 44 PM" src="https://user-images.githubusercontent.com/27160394/85081524-d4fdd280-b191-11ea-8305-415d20676d6d.png">

Two-dimensional arrays in Java are really one-dimensional arrays nested
 * But the one-dimensional arrays that make up the rows of a and b (such as a[0] and b[0]) are stored in different memory locations, even though they have the same internal content
 * a call to the method `java.util.Arrays.equals(a,b)` will return false in this case --> an int[][] is an instanceof Object[], which invokes the Object class’s definition of equals. 
 * `Arrays.deepEquals(a,b)` :To support the more natural notion of multidimensional arrays being equal 
 
 ### Equivalence Testing with Linked Lists
 ```
public boolean equals(Object o) {
	if (o == null) return false;
	if (getClass() != o.getClass()) return false; 
	SinglyLinkedList other = (SinglyLinkedList) o; 
	if (size != other.size) return false;
	Node walkA = head;
	Node walkB = other.head;
	
	while (walkA != null) {
	if (!walkA.getElement().equals(walkB.getElement())) return false; //mismatch 
	walkA = walkA.getNext();
	walkB = walkB.getNext();}
	return true;
 ```


## Cloning Data Structures

`clone` Method
*  shallow copy
* if the field is a reference type, then an initialization of the form duplicate.field = original.field causes the field of the new object to refer to the same underlying instance as the field of the original object.
* Java intentionally disables use of the clone() method by declaring it as `protected`

###  class level
* must explicitly declare support for cloning by formally declaring that the class implements the `Cloneable` interface
*  declaring a public version of the clone() method

### Cloning Arrays

* The assignment of variable backup to data does not create any new array;
```
int data ={2, 3, 5, 7, 11, 13, 17, 19};;
int [] backup;
backup = data;
```
<img width="376" alt="Screen Shot 2020-06-19 at 5 13 56 PM" src="https://user-images.githubusercontent.com/27160394/85183114-43a16580-b250-11ea-96bd-b5d8fe919e91.png">

* make a copy of the array, data, and assign a reference to the new array to variable
  * when executed on an array, initializes each cell of the new array to the value that is stored in the corresponding cell of the original array
```
backup = data.clone();
```
<img width="349" alt="Screen Shot 2020-06-19 at 5 15 23 PM" src="https://user-images.githubusercontent.com/27160394/85183177-76e3f480-b250-11ea-834d-635d19c61bfb.png">

* copying an array that stores reference types
  * The `clone()` method produces a shallow copy of the array,
  * producing a new array whose cells refer to the same objects referenced by the first array.
  
<img width="389" alt="Screen Shot 2020-06-19 at 5 17 27 PM" src="https://user-images.githubusercontent.com/27160394/85183277-c1fe0780-b250-11ea-9e77-ceaa73688b12.png">

* A deep copy of class can be created by iteratively cloning the individual elements, if that class is declared as Cloneable.

```
Person[ ] guests = new Person[contacts.length]; 
for (int k=0; k < contacts.length; k++)
    guests[k] = (Person) contacts[k].clone(); // returns Object type
```

* the `java.util.Arrays` class does not provide any “deepClone” method
   * we can implement our own method by cloning the individual rows of an array
 ```
public static int[ ][ ] deepClone(int[ ][ ] original) { 
     int[ ][ ] backup = new int[original.length][ ];
     for (int k=0; k < original.length; k++)
	backup[k] = original[k].clone(); 
     return backup;
}
 ```
 
 ## Cloning Linked Lists
 
1. The first step to making a class cloneable in Java is declaring that it implements the Cloneable interface
 
 ```
 public class SinglyLinkedList<E> implements Cloneable {
 ```
 2. The remaining task is implementing a public version of the clone() method
 
 ```
public SinglyLinkedList<E> clone() throws CloneNotSupportedException {
     SinglyLinkedList<E> other = (SinglyLinkedList<E>) 	super.clone(); // safe cast
     if (size > 0) { // we need independent chain of nodes 
         other.head = new Node<>(head.getElement(), null); 
         Node<E> walk = head.getNext(); Node<E> 
	 otherTail = other.head; 
	 while (walk != null) {
            Node<E> newest = new Node<>(walk.getElement(), null);
	    otherTail.setNext(newest); 
	    otherTail = newest;
	   walk = walk.getNext()；
	   }
     }
  return other;
} 
 ```
