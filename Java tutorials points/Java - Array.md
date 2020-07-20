# Arrays
> stores a fixed-size sequential collection of elements of the same type.

## Create array variables

* declare
```
datatype[] arrayname;

double[] mylist;
```
* create
```
arrayname = new datatype[arraysize];
```

## Arrays Class Methods

1. `public static int binarySearch(Object[] a, Object key)`
> Searches the specified array of Object ( Byte, Int , double, etc.) 
* for the specified value using the binary search algorithm. 
* The array must be sorted prior to making this call. 
* This returns index of the search key, if it is contained in the list; otherwise, it returns ( – (insertion point + 1)).

2. `public static boolean equals(long[] a, long[] a2)`
> Returns true if the two specified arrays of longs are equal to one another.

* Two arrays are considered equal if both arrays contain the same number of elements, and all corresponding pairs of elements in the two arrays are equal. 
* This returns true if the two arrays are equal. 
* Same method could be used by all other primitive data types (Byte, short, Int, etc.)

3. `public static void fill(int[] a, int val)`
> Assigns the specified int value to each element of the specified array of ints

4. `public static void sort(Object[] a)`
> Sorts the specified array of objects into an ascending order
* according to the natural ordering of its elements. 
* The same method could be used by all other primitive data types ( Byte, short, Int, etc.)
