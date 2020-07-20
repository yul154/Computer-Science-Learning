# Number Class

## Wrapper class
>  need to use objects instead of primitive data types

* All  wrapper classes are subclass of the abstract class number
* Boxing: convert primitive data types into object.
* The Number class is part of the java.lang package
```
Integer x = 5;// boxes int to an Integer object
x = x+10;// unboxes the Integer to a int
```

## Number Methods
1. `XXXValue Method` : returns the primitive data type that is given in the signature.
```
Integer x =5 ;
System.out.println( x.byteValue() );
System.out.println(x.doubleValue());
System.out.println( x.longValue() );
```

2. `compareTo()`: two different types cannot be compared

```
Integer x = 5; 
System.out.println(x.compareTo(3)); // 1
System.out.println(x.compareTo(5));// 0
System.out.println(x.compareTo(8));// -1
```
3. `equal()`
>  whether the Number object that invokes the method is equal to the object that is passed as an argument.

```
public boolean equals(Object o)
```

4. `valueof()`

* returns the relevant Number Object holding the value of the argument passed
* The argument can be a primitive data type, String

```
static Integer valueOf(int i)
static Integer valueOf(String s)
static Integer valueOf(String s, int radix) //  returns an Integer object holding the integer value of the specified string representation, parsed with the value of radix.
```

5. `toString()`
> get a String object representing the value of the Number Object.

```
 String toString()
 static String toString(int i)
 
 Integer x =5;
 x.toString();
 Integer.toString(12);
```

6. `parseInt()`
> get the primitive data type of a certain String

* parseXxx() is a static method

```
int a = Integer.parseInt("9");
double c = Double.parseDouble("5"); 
int b = Integer.parseInt("444",16);
```

7. abs()
> gives the absolute value of the argument
* parameter is Any primitive data type

8. `ceil()` & `floor()`
>  ceil() gives the smallest integer that is greater than or equal to the argument. `floor` gives the largest integer that is less than or equal to the argument.
* parameters:A double or float primitive data type
* return value: innteger
```
Math.ceil(5.5555);// 6.0
Math.floor(5.5555);// 5.0
```

9. `rint()`
> returns the integer that is closest in value to the argument.
```
double rint(double d)// d accepts a double value as parameter.

Math.rint(6.72)// 7.0
```

10.`round()`
> returns the closest long or int, as given by the methods return type.

```
 long round(double d)
 int round(float f)
```

11.` min()` & `max()`
>  gives the smaller  or larger() of the two arguments

* The argument can be int, float, long, double.
```
System.out.println(Math.min(12.123, 12.456));//12.123
System.out.println(Math.max(23.12, 23.0));// 23.12
```
12. `exp()`
> returns the base of the natural logarithms,
```
 double exp(double d)
  Math.exp(x)
```

13. `log`
> returns the natural logarithm of the argument.
```
 double log(double d)
```
14. `pow()` `sqrt()`
> returns the value of the first argument raised to the power of the second argument.

```
double pow(double base, double exponent)
double sqrt(double d)
Math.pow(4, 3)//64
Math.sqrt(64)//8
```

15 `random()`
> generate a random number between 0.0 and 1.0
```
static double random()
System.out.println( Math.random() );//
```
* This is a default method and accepts no parameter.
