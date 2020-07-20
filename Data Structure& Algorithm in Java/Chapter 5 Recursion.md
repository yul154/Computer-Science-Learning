#  Recursion

 recursion: a technique by which a method makes one or more calls to itself during execution
 
 ##  Factorial Function
 * base cases:  fixed values of the function --> n! = 1 for n = 0.
 * recursive cases: which define the function in terms of itsel --> n! = n · (n − 1)! 
 
 ```
 public static int factorial(int n) throws IllegalArgumentException{
		if (n<0) {
			throw new IllegalArgumentException();
		}else if (n==0) {
			return 1;
		}
		return n*factorial(n-1);
	}
 ```
 ### Activation Frame
 > created to store information about the progress of that invocation of the method
 
 * This frame stores the parame- ters and local variables specific to a given call of the method
 * When the execution of a method leads to a nested method call
  1. the execution of the former call is suspended and its frame 
  2. A new frame is then created for the nested method call
 
 ## Binary Search
 
 * the sequence is sorted and indexable
 ```
 public static boolean binarySearch(int[] data, int target, int low,int high) {
		if (low > high) {
			return false;
		}else {
			int mid =(low+high)/2;
			if (target== data[mid]) {
				return true;
			}else if (target>data[mid]) {
				return binarySearch(data,target,mid+1,high);
			}else {
				return binarySearch(data,target,low,mid-1);
			}
		}
 ```
 
 ## File Systems
 
 *  immediate disk space: used by each entry
 *  cumulative disk space:  used by that entry and all nested feature
 
 ### `java.io.File` Class
 
 -- `new File(pathString)` or `new File(parentFile, childString)` :  A new File instance can be constructed either by providing the full path as a string
 
 -- `file.length()`: Returns the immediate disk usage (measured in bytes) for the operating sys- tem entry represented by the File instance 
 
 -- `file.isDirectory()`: Returns true if the File instance represents a directory; false otherwise.
 
 -- `file.list()`:Returns an array of strings designating the names of all entries within the given directory.
 
 
 -- DiskUsage Algorithm
 
```
 public static long diskUsage(File root) {
		long total = root.length();
		if (root.isDirectory()) {
			File Child = new File(root,childname);
			total+= diskUsage(Child);
		}
		System.out.println(total + "\t" + root); 
		return total;
	}
```
  
##  Linear Recursion
> each invocation of the body makes at most one new recursive call

* only one branch is followed during a particular execution of the body

--  power function
```
public static double power(double x, int n) {
		if (n==0) {
			return 1;
		}
		double partial = power(x,n/2);
		double res = partial * partial;
		if (n%2==1)
			res*=x;
		return res;
	}
```
  
## Binary Recursion
> each invocation of the body makes two new recursive call
```
public static int binarySum(int[] data,int l,int r) {
		if (l>r) {
			return 0;
		}else if(l==r) {
			return data[l];
		}else {
			int mid = (l+r)/2;
			return binarySum(data,l,mid)+binarySum(data, mid+1, r);
		}
	}
```
# Designing Recursive Algorithms

An algorithm that uses recursion typically has the following form:
-- Test for base cases
-- Recur

* Parameterizing a Recursion
 -  without exposing the user to the recursive parameterization
 - make the recursive version private,
 - introduce a cleaner public method (that calls the private one with appropriate parameters
 
 ```
 public static boolean binarySearch(int[ ] data, int target) {
    return binarySearch(data, target, 0, data.length − 1); // use parameterized version 
   }
 ```
 
 # Inefficiency recursion
 
## An Inefficient Recursion for Computing Fibonacci Numbers
 ```
public static long fibonacciBad(int n) {
    if (n <= 1) 
      return n;
    else
      return fibonacciBad(n−2) + fibonacciBad(n−1);

 ```
 * most of results of same name from different call is compute multiple times
  * solutions: Memorize the results
 ```
 public static long[] fibonacciGood(int n) {
		if (n<=1) {
			long[] res = {n,0};
			return res;
		}else {
			long[] temp = fibonacciGood(n-1);
			long[] res= {temp[0]+temp[1],temp[0]};
			return res;
		}
	}
 ```
 
 # Eliminating Tail Recursion
 * Java Virtual Machine must maintain frames that keep track of the state of each nested call
  1.  use the stack data structure-->convert a recursive algorithm into a nonrecursive algorithm 

## tail recursion:
 tail recursion
 * if any recursive call that is made from one context is the very last operation in that context,
 * with the return value of the recursive call (if any) immediately returned by the enclosing recursion.
 * able to automatically reimplemented nonrecursively by enclosing the body in a loop for repetition
