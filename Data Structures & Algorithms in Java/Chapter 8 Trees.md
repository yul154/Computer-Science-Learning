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
