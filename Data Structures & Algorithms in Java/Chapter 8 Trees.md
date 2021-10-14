# Contents
1. General Trees
2. Bianry Trees
3. Implementing Trees
4. Tree Travesal Algorithms
---
## 8.1 Tree Definitions and Properties

Node Relationship
* A node is *external* if it has no children, and *internal* if it has at least one node, *External* node is leaf
* A node u is an *ancestor* of a node v if u = v or u is an ancestor of the parent of v. Conversely, a node v is a descendant of a node u if u is an ancestor of v
* The *subtree* of T rooted at a node v is the tree consisting of all the descendants of v in T.

**Edge and Paths**
* An *edge* of tree is a pair of nodes
* A *path* of T is a sequence of nodes

**Ordered Trees**
There is a meaningful linear order among the children of each node

### 8.1.1 Tree adt
The tree ADT
```
public interface Tree<E> extends Iterable<E> {
  Position<E> root();
  Position<E> parent(Position<E> p) throws IllegalArgumentException; 
  Iterable<Position<E>> children(Position<E> p)throws IllegalArgumentException; 
  int numChildren(Position<E> p) throws IllegalArgumentException;
  boolean isInternal(Position<E> p) throws IllegalArgumentException; 
  boolean isExternal(Position<E> p) throws IllegalArgumentException; 
  boolean isRoot(Position<E> p) throws IllegalArgumentException; int size();
  boolean isEmpty();
  Iterator<E> iterator(); 
  Iterable<Position<E>> positions();
}
```

AbstractTree base class, demonstrating how many tree-based algorithms can be described independently of the low-level representation of a tree data structure.
```
public abstract class AbstractTree<E> implements Tree<E> {
  public boolean isInternal(Position<E> p) { return numChildren(p) > 0; }
  public boolean isExternal(Position<E> p) { return numChildren(p) == 0; } 
  public boolean isRoot(Position<E> p) { return p == root(); }
  public boolean isEmpty() { return size() == 0; }
}
```
### 8.1.2 Computing Depth and Height

The *depth* of p is the number of ancestors of p, other than p itself.
```
public int depth(Position<E> e) 
{
			if (isRoot(e)) return 0;
			return 1+depth(parent(e));
}
```
The height of a tree to be equal to the maximum of the depths of its positions 
```
private int heightBad(Position<E> e) {
			int h = 0;
			for(Position<E> p :childern(e)) {
				if (isExternal(p))
					h = Math.max(h, 1+height(p));
			}
			
		}
```
---
## 8.2 Binary Trees
### 8.2.1 The Binary Tree Abstract Data Type
```
public interface BinaryTree<E> extends Tree<E> {
	
	/**Returns the Position of p's left child (or null if no child exists). */
	Position<E> left(Position<E> p) throws IllegalArgumentException;

	/** Returns the Position of p's right child (or null if no child exists). */
	Position<E> right(Position<E> p) throws IllegalArgumentException;

	/** Returns the Position of p's sibling (or null if no sibling exists). */
	Position<E> sibling(Position<E> p) throws IllegalArgumentException;
 }
```

Defining an AbstractBinaryTree Base Class
```
public abstract class AbstractBinaryTree<E> extends  AbstractTree<E> {
	
	public Position<E> sibling(Position<E> p) {
		Position<E> parent = parent<E>;
		if(parent == None) return null;
		if(p == left(parent)) {
			return right(parent);
		}else {
			return left(parent);
		}
	}
	
	public int numChildren(Position<E> p) {
		int count = 0;
		if(left(p) != null) count+=1;
		if(right(p)!= null) count+=1;
		return count;
	}
	
	/** Returns the Position of p's sibling (or null if no sibling exists). */
	public Iterable<Position<E>> children(Position<E> p){
		List<Position<E>> snapshot = new ArrayList<>();
		if(left(p)!= null) snapshot.add(left(p));
		if(right(p)!= null) snapshot.add(right(p));
		return snapshot;
		
	}
	
}
```
### 8.2.2 Properties of Binary Trees
![Screen Shot 2021-10-13 at 9 41 34 PM](https://user-images.githubusercontent.com/27160394/137144416-ed16eba1-715f-4da6-b9a0-8fa5f835c26e.png)

![Screen Shot 2021-10-13 at 10 28 21 PM](https://user-images.githubusercontent.com/27160394/137153311-b4464e22-ebb2-422c-a4a2-01e3d59de823.png)

---
## 8.3 Implementing Trees
*  How a tree will be represented internally
*  How we can effectively navigate between parents and children.
* 
### 8.3.1 Linked Structure for Binary Trees
![Screen Shot 2021-10-13 at 10 31 30 PM](https://user-images.githubusercontent.com/27160394/137154009-39f86166-7092-4cae-8e51-dc45ee055963.png)

Operations for Updating a Linked Binary Tree
|Operation names| Description|
|---------------|------------|
|`addRoot(e)`|Creates a root for an empty tree, storing e as the element, and returns the position of that root; an error occurs if the tree is not empty.|
|`addLeft(p, e)`|Creates a left child of position p, storing element e, and returns the position of the new node; an error occurs if p already has a left child.|
|`addRight(p, e):`|Creates a right child of position p, storing element e, and returns the position of the new node; an error occurs if p already has a right child.|
|`set(p, e)`|Replaces the element stored at position p with element e, and returns the previously stored element|
|`attach(p, T1, T2)`|Attaches the internal structure of trees T1 and T2 as the respective left and right subtrees of leaf position p and resets T1 and T2 to empty trees; an error condition occurs if p is not a leaf.|
|`remove(p)`|Removes the node at position p,replacing it with its child (if any), and returns the element that had been stored at p; an error occurs if p has two children.|

Java Implementation of a Linked Binary Tree Structure

Node class
```
public class LinkedBinaryTree<E> extends AbstractBinaryTree {
	
	protected static  class Node<E> implements Position<E>{
		private E element;
		private Node<E> parent;
		private Node<E> left;
		private Node<E> right;
		private Node(E e, Node<E> above, Node<E> leftChild, Node<E> rightChild) {
			element = e;
			left = leftChild;
			right = rightChild;
			parent = above;
		}
		public E getElement() { return element; }
		public Node<E> getParent() { return parent; }
		public Node<E> getLeft() { return left; }
		public Node<E> getRight() { return right; }
		// update methods
		public void setElement(E e) { element = e; }
		public void setParent(Node<E> parentNode) { parent = parentNode; } public void setLeft(Node<E> leftChild) { left = leftChild; }
		public void setRight(Node<E> rightChild) { right = rightChild; }
	}
	
	protected Node<E> createNode(E e, Node<E> parent,Node<E> left, Node<E> right)  //factory method pattern,
	{ return new Node<E>(e, parent, left, right);}
	
	protected Node<E> root = null; 
	private int size = 0;
	public LinkedBinaryTree() { }
```
* The Factory Method defines an interface for creating objects, but lets subclasses decide which classes to instantiate

```
// nonpublic utility
/** Validates the position and returns it as a node. */
protected Node<E> validate(Position<E> p) throws IllegalArgumentException {
	if(!(p instanceof Node)) throw new IllegalArgumentException("Not valid position type");
	Node<E> node = (Node<E>) p;
	if(node.getParent() == node) {
		throw new IllegalArgumentException("p is no longer in the tree");
	}
	return node;
}
// accessor methods (not already implemented in AbstractBinaryTree)
/** Returns the number of nodes in the tree. */
public int size( ) {return size; }
/** Returns the root Position of the tree (or null if tree is empty). */ 
public Position<E> root( ) {return root; }
/** Returns the Position of p's parent (or null if p is root). */
public Position<E> parent(Position<E> p) throws IllegalArgumentException {Node<E> node = validate(p); return node.getParent(); }
/** Returns the Position of p's left child (or null if no child exists). */
public Position<E> left(Position<E> p) throws IllegalArgumentException { Node<E> node = validate(p); return node.getLeft(); }
/** Returns the Position of p's right child (or null if no child exists). */
public Position<E> right(Position<E> p) throws IllegalArgumentException { Node<E> node = validate(p);return node.getRight(); }

```

Six update methods for a linked binary tree.
```
public Position<E> addLeft(Position<E> p, E e)
{
    	 throws IllegalArgumentException { Node<E> parent = validate(p);
	     if (parent.getLeft() != null)  throw new IllegalArgumentException("p already has a left child");
	     Node<E> child = createNode(e, parent, null, null); 
	     parent.setLeft(child);
	     size++;
	     return child;
 }
 public void attach(Position<E> p, LinkedBinaryTree<E> t1, LinkedBinaryTree<E> t2) throws IllegalArgumentException {
	 Node<E> node = validate(p);
	 if (isInternal(p)) throw new IllegalArgumentException("p must be a leaf");
	 size = t1.size+t2.size;
	 if(!t1.isEmpty()) {
		 t1.root.setParent(node); 
		 node.setLeft(t1.root); 
		 t1.root = null;
		 t1.size = 0;
	 }
	 if(!t2.isEmpty()) {
		 t2.root.setParent(node);
		 node.setRight(t2);
		 t2.root == null;
		 t2.size = 0;
	 }
}
public E remove(Position<E> p) throws IllegalArgumentException {
     Node<E> node = validate(p);
     if(numChildren(p)==2) throw new IllegalArgumentException("p has two children");
     Node<E> child = node.getLeft()!=null?node.getLeft():node.getRight();
     if(child!=null)
	 child.setParent(node.getParent());
     if(node ==root) {
	 root =child;
     }else {
	 Node<E> parent = node.getParent();
	 if (node == parent.getLeft()) parent.setLeft(child);
	 else parent.setRight(child);
	 }
     size --;
     E temp =node.getElement();
     node.setElement(null);
     node.setLeft(null);
     node.setRight(null);
     node.setParent(node);
     return temp
}
```
### 8.3.2 Array-Based Representation of a Binary Tree

let `f(p)` be the integer defined as follows.
• If `p` is the root of `T`,then `f(p)=0`.
• If `p` is the left child of position `q`, then f(p) = 2f(q)+1. 
• If `p` is the right child of position `q`, then f(p) = 2f(q)+2.

One advantage of an array-based representation of a binary tree is that a posi- tion p can be represented by the single integer f(p),
*  Based on our formula for the level numbering, the left child of p has index 2f(p)+1, 
*  the right child of p has index 2f(p)+2, 
*  the parent of p has index [(f(p) − 1)/2]

On drawnback is the space usage of an array-based representation depends greatly on the shape of the tree.
* In fact, in the worst case, the exponential worst-case space
* have a number of empty cells that do not refer to existing positions of T

Another drawback of an array representation is that many update operations for trees cannot be efficiently supported. 
* For example, removing a node and promoting its child takes O(n) time 
* because it is not just the child that moves locations within the array, but all descendants of that child.

### 8.3.3 Linked Structure for General Trees
 A general tree T as a linked structure is to have each node store a single container of references to its children.
 
 <img width="534" alt="Screen Shot 2021-10-14 at 4 29 48 PM" src="https://user-images.githubusercontent.com/27160394/137280649-08cb53b1-9be5-4149-aee9-0a6ead7f3a13.png">
 
---

## 8.4 Tree Traversal Algorithms
### 8.4.1 Preorder and Postorder Traversals of General Trees
In a preorder traversal of a tree T 
* the root of T is visited first and then the subtrees rooted at its children are traversed recursively.
```
Algorithm preorder(p): 
  p.visited();
  for (child : p.children()):
  	preorder(r);
````
<img width="360" alt="Screen Shot 2021-10-14 at 5 35 51 PM" src="https://user-images.githubusercontent.com/27160394/137291814-64f1db9d-7575-45f7-b79d-0fbeb49f3e06.png">

**Postorder traversal.**
* It recursively traverses the subtrees rooted at the children of the root first

```
Algorithm postorder(p):
  for (child : p.children()):
  	postorder(r);
  p.visited();
```
<img width="360" alt="Screen Shot 2021-10-14 at 5 38 16 PM" src="https://user-images.githubusercontent.com/27160394/137292229-facc65d5-1d1a-4968-8717-d241083e47ef.png">

### 8.4.2 Breadth-First Tree Traversal
> Visit all the positions at depth d before we visit the positions at depth d + 1.
Use a queue to produce a FIFO (i.e., first-in first-out) semantics to store one level node.
```
Algorithm breadthfirst(root):
  Deque<Node> bFS = new LinkedList<>();
  bst.add(root)
  while (!bfs.isEmpty())
       current Node = bst.poll();
       Node.visited();
       for child : Node.children();
       	   bfs.add(Child);
       
```
### 8.4.3 Inorder Traversal of a Binary Tree
> visiting the nodes of T “from left to right.” 
The inorder traversal visits p after all the positions in the left subtree of p and before all the positions in the right subtree of p.
```
Algorithm inOrder(root):
     if(root.left):
     	inOrder(root.left);
     root.visited();
     if(root.right):
     	inOrder(root.right);
```
<img width="432" alt="Screen Shot 2021-10-14 at 5 53 38 PM" src="https://user-images.githubusercontent.com/27160394/137294860-0daba226-220b-44c6-a322-5018200850dc.png">

### 8.4.5 Applications of Tree Traversals
