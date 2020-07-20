# Binary Search Trees

A Tree consists of
* A set of nodes
* A set of edges that connect those nodes.

Root
* Every node N except the root has exactly one parent
* The root is usually depicted at the top of the tree.
* A node with no child is called a leaf.

BST property
* Every key in the left subtree is less than X's key
* Every key in the right subtree is greater than X's key

## BST Operations
### 1.Search
* if search key equal T.key return `true`
* if search key < T.key, search T.left.
* if search key > T.key, search T.right.
```
public static boolean search (BST root, key k) {
	if (root ==null){
		return false;
	}

	if (root.key.equal(k)){
		return true;
	}else if (root.key >k){
		return search (root.left, k)
	}else{
		return search(root.right, k)
	}
}
```
* Runtime is O(log N)

### 2.Insert
```
public staic BST insert(BST root, key k){
	if (root ==null){
		return new BST(k);
	}
	if (k< root.key){
		root.left= insert(root.left,k);
	}else if(k>root.key){
		root.right= insert(root.right,k);
	}
	return root;

}
```

### 3. Delete
#### 3 cases
1. Delete key has no children: directly delete
2. Delete key has one child: move node parent's pointer to node's child
3. Delete key have two children: Choose predecessor(largest item smaller than the key) or successor(smallest item larger than key)
<img width="504" alt="Screen Shot 2020-06-17 at 6 04 59 PM" src="https://user-images.githubusercontent.com/27160394/84959510-12485e80-b0c5-11ea-8a79-3fb62d03d69d.png">


## BST Tree Performance

BST Height
* Θ(log N) in the best case (“bushy”).
* Θ(N) in the worst case (“spindly”).

* Depth : How far it is from the root, we say the root has a depth of 0.
* Height: determines the worst case runtime to find a node.
* average depth: determines the average case runtime to find a node



# B-trees
> Avoid imbalanced
* B-trees are more complex, but they can efficiently handle ANY insertion order.
## Never add new leaves at the bottom
* Avoid new leaves by “overstuffing” the leaf nodes: Overstuffed tree” always has balanced height, because leaf depths never change.
<img width="325" alt="Screen Shot 2020-06-18 at 10 03 56 AM" src="https://user-images.githubusercontent.com/27160394/85037501-0ef7b600-b14b-11ea-929a-0311290bfbdd.png">

* Leaf nodes can get too juicy
  1.Set a limit L on the number of items, say L=3.
  2. If any node has more than L items, give an item to parent.
  3. Pulling item out of full node splits it into left and right.

<img width="364" alt="Screen Shot 2020-06-18 at 10 05 58 AM" src="https://user-images.githubusercontent.com/27160394/85037689-52eabb00-b14b-11ea-889b-b13663b24405.png">

* if the root is too full
1. If we split the root, every node gets pushed down by exactly one level
2. If we split a leaf node or internal node, the height doesn’t change. 
3. All operations have guaranteed O(log N) time.

## B-Trees are most popular in two specific contexts:
* Small L (L=2 or L=3):
  * Used as a conceptually simple balanced search tree (as today).
* L is very large (say thousands).
  * Used in practice for databases and filesystems (i.e. systems with very large records).

## B-tree Invariants
* All leaves must be the same distance from the source.
* A non-leaf node with k items must have exactly k+1 children.

## Runtime Analysis
* Height: Between ~logL+1(N) and ~log2(N)
   * Largest possible height is all non-leaf nodes have 1 item.
   * Smallest possible height is all nodes have L items.
   * Overall height is therefore Θ(log N). 

* Runtime
  * Worst case number of nodes to inspect: H + 1
  * Worst case number of items to inspect per node: L
  * Overall runtime: O(HL)
  * Since H = Θ(log N), overall runtime is O(L log N) (Since L is a constant, runtime is therefore O(log N).)


# Black-red tree
## Tree Rotation
* rotateLeft(Node):Let x be the right child of G. Make G the new left child of x.
   * temporarily merging G and P, then sending G down and left.
<img width="501" alt="Screen Shot 2020-06-18 at 11 19 20 AM" src="https://user-images.githubusercontent.com/27160394/85046101-91857300-b155-11ea-9daa-9897b8bd3fc1.png">

* rotateRight(P): Let x be the left child of P. Make P the new right child of x.
  * temporarily merging G and P, then sending P down and right.
  
<img width="473" alt="Screen Shot 2020-06-18 at 11 20 23 AM" src="https://user-images.githubusercontent.com/27160394/85046209-b679e600-b155-11ea-8bbf-05abac35383a.png">

## Rotation for balance
* Can shorten (or lengthen) a tree.
* Preserves search tree property.

## Black-red tree

*  Create “glue” links with the smaller item off to the left.

<img width="496" alt="Screen Shot 2020-06-18 at 11 38 03 AM" src="https://user-images.githubusercontent.com/27160394/85047956-2e491000-b158-11ea-8cbf-4b2a8b82be59.png">

### Left-Leaning Red Black Binary Search Tree (LLRB):
* A BST with left glue links that represents a 2-3 tree
* LLRBs are normal BSTs! 
* There is a 1-1 correspondence between an LLRB and an equivalent 2-3 tree.
<img width="453" alt="Screen Shot 2020-06-18 at 11 40 30 AM" src="https://user-images.githubusercontent.com/27160394/85048164-8d0e8980-b158-11ea-93c2-3a3e49a24343.png">

* LLRB properties:
1. No node has two red links
2. Every path from root to a leaf has same number of black link

### Insertion
* use a red link when inserting: In 2-3 trees new values are ALWAYS added to a leaf node
* Right red link ->  Rotate left 
* Two consecutive left links  -> Rotate right 
* Two red children -> Color flip 
```
private Node put(Node h, Key key, Value val) {
	if (h == null) { return new Node(key, val, RED); }
 
	int cmp = key.compareTo(h.key);
    if (cmp < 0)      { h.left  = put(h.left,  key, val); }
    else if (cmp > 0) { h.right = put(h.right, key, val); }
    else              { h.val   = val;                    }
 
	if (isRed(h.right) && !isRed(h.left))      { h = rotateLeft(h);  }
	if (isRed(h.left)  &&  isRed(h.left.left)) { h = rotateRight(h); }
	if (isRed(h.left)  &&  isRed(h.right))     { flipColors(h);      } 
 
	return h;
}

```

### LLRB Runtime
* LLRB tree has height O(log N).
* Contains is trivially O(log N).
* Insert is O(log N).

# Summary Search Tree
* BST: simple, but subject to imbalance
* 2-3trees: balanced, but painful to implement and relatively slow
* LLRB: insert is easy to implement, but delete hard
* Java's Treemap is a red-black tree
