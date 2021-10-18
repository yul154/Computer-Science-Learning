# 13.2 Quick-Sort
> Divide and conquer

* All the hard work is done before the recursive calls.

High-Level Description of Quick-Sort
1. Divide: choose the pivot x to be the last element in S. Remove all the elements from S and put them into three sequences:
 * L, storing the elements in S less than x
 * E, storing the elements in S equal to x
 * G, storing the elements in S greater than x
 
2. Conquer: Recursively sort sequences L and G.
3. Combine:Put back the elements into S in order by first inserting the elements of L, then those of E, and finally those of G.

<img width="378" alt="Screen Shot 2021-10-18 at 3 57 29 PM" src="https://user-images.githubusercontent.com/27160394/137691021-cef5a4f1-d89f-4a8b-9e4e-5ec823336de0.png">

<img width="496" alt="Screen Shot 2021-10-18 at 3 58 45 PM" src="https://user-images.githubusercontent.com/27160394/137691195-6df09a9b-3aa1-4e1a-b1d1-893718d5456f.png">


**Performing Quick-Sort on General Sequences**
```
public static<K> void quickSort(Queue<K> S, Comparator<K> comp) {
		
		int n  = S.size();
		if(n<2) return;
		K pivot = S.peek();
		Queue<K> L = new LinkedQueue<>();
		Queue<K> E = new LinkedQueue<>();
		Queue<K> G = new LinkedQueue<>();
		While(!S.isEmpty()){
			K  element = S.dequeue();
			int c = comp.compare(element, pivot);
			if(c<0) L.enqueue(element);
			else if(c == 0) E.enqueue(element);
			else G.enqueue(element);
			
		}
		quickSort(L,comp);
		quickSort(G,comp);
		while (!L.isEmpty()) {
			S.enqueue(L.dequeue());
		}
		while (!E.isEmpty()) {
			S.enqueue(E.dequeue());
		}
		while (!G.isEmpty()) {
			S.enqueue(G.dequeue());
		}
	}
```
*  The Running time of quickSort is depend on pivot selections, worstcase is O(n2),best is O(nlogn).
### 12.2.1 Randomized Quick-Sort
Having pivots close to the “middle” of the set of elements leads to an O(n log n) running time for quick-sort.

* Picking Pivots at Random
* the running time of random- ized quick-sort is O(n log n) with high probability.

### 12.2.2 Additional Optimizations for Quick-Sort
