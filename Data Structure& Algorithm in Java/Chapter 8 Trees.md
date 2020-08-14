# Tree
* General Trees
* Binary Trees
* Implementing Trees
* Tree Traversal Algorithms

## General Trees
* Each element in a tree has a parent element and zero or more children elements
* Two nodes that are children of the same parent are siblings
* A node v is external if v has no children. A node v is internal if it has one or more children. External nodes are also known as leaves.

### The Tree Abstract Data Type

|Method|Description|
|------|-----------|
|getElement()| Returns the element stored at this position.The tree ADT then supports the following accessor methods, allowing a user to navigate the various positions of a tree T :
|root()|Returns the position of the root of the tree (or null if empty)|
|parent(p)|Returns the position of the parent of position p (or null if p is the root).
|children(p)|Returns an iterable collection containing the children of position p (if any).
|numChildren(p)|Returns the number of children of position p.
|isInternal(p)| Returns true if position p has at least one child.
|isExternal(p)| Returns true if position p does not have any children. 
|isRoot(p)| Returns true if position p is the root of the tree.


* A Tree Interface in Java

```
public interface Tree<E> extends Iterable<E> {
	
	Position<E> root();
	Position<E> parent(Position<E> p) throws IllegalArgumentException;
	Iterable<Position<E>> children(Position<E> p) throws IllegalArgumentException;
	int numChildren(Position<E> p) throws IllegalArgumentException;
	boolean isInternal(Position<E> p )throws IllegalArgumentException;
	boolean isExternal(Position<E> p ) throws IllegalArgumentException;
	boolean isRoot(Position<E> p) throws IllegalArgumentException;
	int size();
	boolean isEmpty();
	Iterator<E> iterator();
	Iterable<Position<E>> positions();

}
```

### Depth and Height
* The depth of p is the number of ancestors of p,the depth of the root of T is 0
* The height of a tree to be equal to the maximum of the depths of its positions (or zero, if the tree is empty)

```
public int depth(Position<E> p){
   if(isRoot(p))
     return 0;
   else
     return 1+ depth(parent(p));

}

public int height(Position<E> p){
    int h =0;
    for(Position<E> c: children(p))
      h = Math.max(h,1+height(c));
    return h;
    
}
```

## Binary Trees
A binary tree is an ordered tree with the following properties:
1. Every node has at most two children.
2. Each child node is labeled as being either a left child or a right child.
3. A left child precedes a right child in the order of children of a node.

### The Binary Tree Abstract Data Type

* left(p) -> Returns the position of the left child of p (or null if p has no left child).
* right(p) -> Returns the position of the right child of p (or null if p has no right child).
* sibling(p) -> Returns the position of the sibling of p (or null if p has no sibling).

**Interface**
```
public abstract class AbstractBinaryTree<E> extends AbstractTree<E> 
                                   implements BinaryTree<E> {
     public Position<E> sibling(Position<E> p){
    	 Position<E> parent = parent(p);
    	 if(parent == null) return null;
    	 if(p == left(parent))
    		 return right(parent);
    	 else
    		 return right(parent);
     }
     
     public int numChildren(Position<E> p) {
    	 int count=0;
    	 if (left(p) != null)
    	 count++;
    	 if (right(p) != null)
    	 count++; return count;
    	 }
    
     public Iterable<Position<E>> children(Position<E> p) {
    	 List<Position<E>> snapshot = new ArrayList<>(2); 
    	 if (left(p) != null)
    	    snapshot.add(left(p)); 
    	 if (right(p) != null)
    	     snapshot.add(right(p)); 
    	 return snapshot;
    	 }
}

```
