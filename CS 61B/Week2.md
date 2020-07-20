# References and Recursion

## Bits

All information in your computer is stored in memory as a sequence of ones and zeros.

* 8 primitive types in Java: byte, short, int, long, float, double, boolean, char
* declaring a variable of a certain type in Java
  1. Your computer sets aside exactly enough bits to hold a thing of that type.
  2. Java finds a contiguous block(bits) with exactly enough bits to hold a thing of that type
  3. Java does NOT write anything into the reserved boxes
* When you write `y = x`, you are telling the Java interpreter to copy the bits from x into y

## Reference Type
> Everything exclude primitive type.Including arrays, is a reference type.

### Object instantiation
<img width="291" alt="Screen Shot 2020-06-03 at 11 48 39 AM" src="https://user-images.githubusercontent.com/27160394/83664868-37e74b00-a590-11ea-9eb3-bec373b4646a.png">

* Java first allocates a box of bits for each instance variable of the class and fills them with a default value 
* The constructor then usually fills every such box with some other value
* Key word `New` as returning the address of the object

### Reference variable declarations
<img width="499" alt="Screen Shot 2020-06-03 at 11 47 28 AM" src="https://user-images.githubusercontent.com/27160394/83664759-0f5f5100-a590-11ea-9c4a-00497294481c.png">

1. Java allocates a box of 64 bits, no matter what type of object.
2. The 64 bit box contains Null or address (narrow) of the object in memory

### Box and Pointer Notation

* The box of variable is the address of variables values
* The cotent of box is the narrow (address) of variabls values

### Reference Types Obey the Golden Rule of Equals
```
Walrus a = new Walrus(1000, 8.3);
Walrus b;
b = a;
```
<img width="302" alt="Screen Shot 2020-06-03 at 11 49 40 AM" src="https://user-images.githubusercontent.com/27160394/83664949-551c1980-a590-11ea-8642-634c66b4a4c6.png">

Just as with primitive types, the equals sign copies the bits.
* copies the bits in the a box into the b box
*  b will copy exactly the arrow in a 

### Parameter Passing
When the function is invoked, 
* the function has its own scope 
* with new boxes labeled as variables
* And then the bits are simply copied in ("pass by value".)
* when we call this method and pass in variables. Copy the bits from those variables into the parameter variables

###  Instanntiation of Arrays
Variables that store arrays are reference variables just like any other.

 ```
 int[] x;//declaration
 x = new int[]{1,2,3,4,5}//instantiation
 int [] a = new int[]{1,2,3,4,5}//assignment
 ```
 <img width="487" alt="Screen Shot 2020-06-03 at 12 23 14 PM" src="https://user-images.githubusercontent.com/27160394/83668063-015fff00-a595-11ea-8087-df25008619a8.png">

1. Declaration :Creates a 64 bit box for storing an int array address.
2. Instantiation: Then the new keyword creates size boxes of type bits each nd returns the address of the overall object for assignment to x.
3. Assignment: Puts the address of this new Object into the 64 bit box named a.

## Node Based Lists

### 2.Bureaucracy
* Construct Hidden data structure: Don't need to know recursively abou Java reference.
* Introduce a middleman.

### 3. Access Control
> Use the private keyword to prevent code in other classes from using members (or constructors) of a class.

* `private`:  can only be accessed by code inside the same .java file
* `public` : a declaration that a method is available and will work forever exactly as it does now.

### 4. Nested class: 
> embed a class declaration inside of another for just this situation
* Keeping code organized: Make the nested class private if other classes should never use the nested class.
* Declare the nested classes to be `private` as well; this way, other classes can never use this nested class.

#### `static`
1. If the nested class has no need to use any of the instance methods or variables of parent class
2. saves memory: Methods inside the static class can not access any of the members of the enclosing class
3. Static variables is for storing the total number of objects that have been created of a class. There needs to be only one variable per class for storing something like this!
 
### 5. Caching
* putting aside data to speed up retrieval.

### 6. Representing the Empty List
> Easily represent the empty list
*  sentinel node: We can do this by creating a special node that is always there. it will hold a value, which we won't care about.

### 7. Invariants
*  a condition that is guaranteed to be true during code execution 
* size, sentinel reference

## Generics 
> create data structures that hold any reference type.
Generics: Parametrize the type.
* In the .java file implementing your data structure, specify your “generic type” only once at the very top of the file.
* Write out desired type during declaration
* Use the empty diamond operator <> during instantiation 
* When declaring o instantiating data structure, use reference type
```
DLList<Double> s1 = new DLList<>(5.3);
```
## Array
>  a special kind of object which consists of a numbered sequence of memory boxes.

Consist of
*  A fixed integer length
*  A sequence of N memory boxes where N=length
  *  All of the boxes hold the same type of value
  *  The boxes are numbered 0 through length-1

Array are instantiated with `new`
```
y=new int[3];
x= new int[]{1,2,3,4,5};
int [] x= {2,4,5,3,6};
```
Arraycopy
* Item by item using a loop
* Using `arraycopy.` takes 5 parameters
  * Source array
  * Start position in source
  * Target array
  * Start position in target
  * Number to copy
```
x[3:5]=b[0:2] //in Python
System.arraycopy(b,0,x,3,2);
```
### 2D array
```
int[][] arrays = new int[3][];
int[] row = arrays[0];
int [][] matrix = new int[4][4];
int[][] pascalAgain = new int[][]{{1}, {1, 1},
                              	{1, 2, 1}, {1, 3, 3, 1}};
```

### Array VS Class
Arrays and Classes can both be used to organize a bunch of memory boxes.

| Array|Class
-------|-----
Array boxes are accessed using [] notation|Class boxes are accessed using dot notation.
Array boxes must all be of the same type.| Class boxes may be of different types.
Both have a fixed number of boxes.


