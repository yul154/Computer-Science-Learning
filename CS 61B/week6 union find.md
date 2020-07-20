#  Disjoint Sets
## operations
* `connect(x, y)`: Connects x and y.
* `isConnected(x, y)`: Returns true if x and y are connected. Connections can be transitive, i.e. they don’t need to be direct.
```
public interface Disjoint{
  void connect (int p, int q);
  boolean isConnected(int p , int q);
  }
```
## Approach 
1. List<Set<Integer>>:Store connected components as a List of Sets (slow, complicated).
2. Quick Find : Store connected components as set ids.
3. Quick Union: Store connected components as parent ids.,improve Connect operations(just changed one value)
4. Weighted Quick Union: Modify quick-union to avoid tall trees.use size(number of nodes) to decide on new tree root.
5. Weighted quick union with path compression: When find is called, every node along the way is made to point at the root.

<img width="566" alt="Screen Shot 2020-06-17 at 10 17 42 AM" src="https://user-images.githubusercontent.com/27160394/84916537-d0e38f00-b083-11ea-965c-61536ef06770.png">

# Binary Search
* Compare key against middle enntry
  1. Too small, go left
  2. Too bigm go right
  3. Equal, found

# Merge Sort
1. If array is of size 1, return.
2.Mergesort the left half: Θ(??).
3. Mergesort the right half: Θ(??).
4. Merge the results: Θ(N).
* runtime of Mergesort: Θ(N log N)

# Abstract Data Types
> Defined only by it's operations, not by its implementaion.
* Stack is an ADT
* syntax differentiation between ADT and implementations: 
```
List<Integer> L = new ArrayList<>();// Allow you to write ADT on the right, not specify what kind
```

## Collections
> Among the most important interfaces in the java.util library are those that extend the Collection interface 
* Lists of things.
* Sets of things.
* Mappings between items

<img width="706" alt="Screen Shot 2020-06-17 at 12 45 50 PM" src="https://user-images.githubusercontent.com/27160394/84931501-7b65ad00-b098-11ea-9c9b-9761a360db6a.png">


