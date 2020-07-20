 # Java Programming Basics

<img width="558" alt="Screen Shot 2020-06-03 at 9 16 09 PM" src="https://user-images.githubusercontent.com/27160394/83707357-7526f980-a5df-11ea-8427-7c7613518de4.png">

Identifier: The name of a class, method, or variable in Java,begins with a letter and consists of let- ters, numbers, and underscore characters

Block: Any set of statements between the braces “{” and “}”

## Commentns
* Uses a “//” to begin an inline comment
* Uses a “/*” to begin a block comment and a “*/” to close it
* “/**”: Block comments that begin with, call Javadoc

## Base Types

Type name|description
---------|------------
boolean |a boolean value: true or false
char| 16-bit Unicode character
byte| 8-bit signed two’s complement integer
short| 16-bit signed two’s complement integer
int| 32-bit signed two’s complement integer
long| 64-bit signed two’s complement integer
float| 32-bit floating-point number (IEEE 754-1985) double 64-bit floating-point number (IEEE 754-1985)

```
boolean verbose,debug;
int i,j,k=234;
double e=2.7123, a=6.231;
```
###  Initial Default values
* All numeric types are initialized to zero
* A boolean is initialized to false
* A character is initialized to the null character by default

## Classes and Objects
* Every object is an instance of a class.
* class: 
  1. serves as the type of the object and as a blueprint, 
  2. defining the data which the object stores and the methods for accessing and modi- fying that data.
* Members of a class in Java 
  * Instance variables:which are also called fields, Instance variables must have a type
  * Methods:accessor method,update method
### Reference types
* A reference variable is capable of storing the location (i.e., memory address) of an object from the declared class
* a new object is created by using the `new` operator followed by a call to a constructor for the desired class
* a constructor is a method that always shares the same name as its class
* `new` operator returns a reference to the newly created instance;

### The Dot Operator
*  Dot: an object reference variable is useful for accessing the methods and instance variables associated with an object
* `NullPointerException`:If the dot operator is used on a reference that is currently null
* Signature: A method’s name combined with the number and types of its parameters
* if one remote control is used to change the device, then the (single) object pointed to by all the remotes changes

## Defining a Class

### Modifier

Java provides a number of non-access modifiers to achieve many other functionality. 

#### 1. Access Control Modifiers: 
> limit access among classes supports a key principle of object-orientation known as encapsulation
* `public`: all classes may access the defined aspect.
* `protected`:access to the defined aspect is only granted to the following groups of other classes:
  1. Classes that are designated as subclasses of the given class through inheritance.
  2. Classes that belong to the same package as the given class.
* `private`: access to a defined member of a class be granted only to code within that class.

#### 2. `static`
* Variable level:  its value is associated with the class as a whole, rather than with each individual instance of that class
* Method level: it is typically invoked using the name of the class as a qualifier, not instance of class
```
 Math.sqrt(2)
```

#### 3. `abstract`
* its signature is provided but without an implementation of the method body.
* A class with one or more abstract methods must also be formally declared as abstract
* Java will not allow any instances of an abstract class to be constructed

#### 4. `final`
* A variable is declared with `final`, it can never again be assigned a new value
* Designating a method: only relevant in the context of inheritance.,A final method cannot be overridden by a subclass, 
* Class level: only relevant in the context of inheritance, a final class cannot even be subclassed.


### Declaring

#### Declaring Instance Variables
*  Each instance of a class maintains its own individual set of instance variables
```
[modifiers] type identifier1[=initialValue1], identifier2[=initialValue2];
private     int  a =2, b=3;
```
#### Declaring Methods

1. Signature :  specifies how the method is called
2. Body :  specifies what the object will do when it is called
```
[modifiers] returnType methodName(type1 param1 , ..., typen paramn) { 
    // method body . . .
}

protected int increment(int a, int b){
  return a+b;
}

```
* Return type:
  1. `void`(no return value)
  2. Java methods can return only one value
* Parameters:
 1. All parameters in Java are passed by value：any time we pass a parameter to a method, a copy of that parameter is made for use within the method body
 
### Defining Constructors
Constructor: used to initialize a newly created instance of the clas
```
modifiers name(type0 parameter0 , ..., typen−1 parametern−1) { // constructor body . . .
}
```
* Constructors cannot be static, abstract, or final,only modifiers that are allowed are those that affect visibility
* The name of the constructor must be identical to the name of the class it constructs
* We don’t specify a return type for a constructor,the new operator is responsible for returning a reference to the new instance to the caller
* A class can have many constructors, but each must have a different signature
* If no constructors are explicitly defined, Java provides an implicit default constructor for the class

## Keyword `this`
Within the body of a (nonstatic) method in Java, the keyword this is automatically defined as a reference to the instance upon which the method was invoked
* To store the reference in a variable
* To differentiate between an instance variable and a local variable with the same name
```
public Counter(int count) {
this.count = count; // set the instance variable equal to parameter
}
```
* To allow one constructor body to invoke another constructor body.


# String, Wrappers, Arrays and Eum Types

## String Class
* Java’s char base type stores a value that represents a single text character
* `String` class:   A string instance represents a sequence of zero or more characters
 * Java uses double quotes(" ") to designate string literals.
 
### Character index
* Each character within a string can be referenced by an index
* First character is at index 0, last one is at index n-1.
* Java’s String class supports a method length();
```
char letter= fruit.charAt(3);
int length= fruit.length();
int ran= fruit.indexOf("n",5);
```
### Concatenation
> Combine Strings
```
String term ="yuxuan"+"li"
```
#### 1. `+`
* String is immutable class, it doesn't modify any String object and always create a new String object

#### 2. StringBuilder
> effectively a mutable version of a string

```
public static void stringBuilder_method() {
		StringBuilder strb = new StringBuilder("A");
		strb.append(" append ");
		System.out.println(strb);
		strb.setCharAt(2, 'C');  //Change the character at index k to character c.
		System.out.println(strb);
		strb.insert(3, "insert");//Insert a copy of string s starting at index k of the sequence, shifting existing characters further back to make room.
		System.out.println(strb);
		strb.reverse();
		System.out.println(strb);
		String str= strb.toString();//Return a traditional String instance based on the current character sequence.
		System.out.println(str.getClass());
		
	}
```

### 3. String.concat
* Only accept String argument.
* This method returns a String object, so chaining together the method is a useful feature.
```
String myString = "Both".concat(" fickle")
  .concat(" dwarves")
  .concat(" jinx")
  .concat(" my")
  .concat(" pig")
  .concat(" quiz");
```
### 4. String.format
> allows us to inject a variety of Java Objects into a String template.
* Takes a single String denoting our template
* This template contains ‘%' characters to represent where the various Objects should be placed
```
String myString = String.format("%s %s %.2f %s %s, %s...", "I",
  "ate",
  2.5056302,
  "blueberry",
  "pies",
  "oops");
```
### 5. String.join
> join an array of Strings with a common delimiter
```
public static String join(CharSequence delimiter,
                          CharSequence... elements)
                          
List list<String> = Arrays.asList("Steve", "Rick", "Peter", "Abbey");
String names = String.join(" | ", list);
System.out.println(names); //Steve | Rick | Peter | Abbey
```
### 6. String.joiner
> StringJoiner abstracts all of the String.join functionality into a simple to use class.
* The constructor takes a delimiter, with an optional prefix and suffix

```
public static void main(String[] args) {  
    	/* Passing comma(,) as delimiter and opening bracket
    	 * "(" as prefix and closing bracket ")" as suffix
    	 */
        StringJoiner mystring = new StringJoiner(",", "(", ")");    
          
        // Joining multiple strings by using add() method  
        mystring.add("Negan");  
        mystring.add("Rick");  
        mystring.add("Maggie");  
        mystring.add("Daryl");  
                  
        // Displaying the output String
        System.out.println(mystring);  
    }  
```

## Wrapper Types

There are some library which are specif- ically designed so that they only work with object types,To get around this obstacle, Java defines a wrapper class for each base type.

* An instance of each wrapper type store a single valu of base type

<img width="564" alt="Screen Shot 2020-06-09 at 10 50 58 PM" src="https://user-images.githubusercontent.com/27160394/84225019-b4ec5600-aaa3-11ea-8592-156f8e527d0d.png">

* Java automatic boxing and unboxing base type and wrapper type
```
intj=8;
Integer a = new Integer(12);
int k=a; // a is automatically unboxed before the addition
int m=j+a;// result is automatically boxed before assignment
a=3∗m;
```

## Arrays
> A sequenced collection of variables all of the same type
* Element: Each value stored in an array 
* An instance of an array is treated as an object by Java
* Variables of an array type are reference variables
```
type [] variablename;
elementType[] arrayName = {initialValue0, initialValue1, . . . , initialValueN−1};
double[ ] measurements = new double[1000];
```
## Enum Types
> a more elegant approach to representing choices from a finite set
```
modifier enum name { valueName0 , valueName1 , . . . , valueNamen−1 };
public enum Day { MON, TUE, WED, THU, FRI, SAT, SUN };
Day today;
today = Day.TUE;
```

# Expressions
> Java expressions involve composing literals and variables with operators

## Literals
> A literal is any “constant” value that can be used in an assignment or other expres- sion
* Java allow following literals
 1. The null object reference
 2. Boolean
 3. Integer
 4. Floating
 5. Character
 6. String Literal

## Operators
### 1. Arithmetic Operators.

symbol| name|
------|-------|
`+` | addition
`-`| subtraction
`*` | multiplication
`/` | division
`%` | the modulo operator

### 2. Increment and Decrement Operators
* If such an operator is used in front of a variable reference, then 1 is added to (or subtracted from) the variable and its value is read into the expression
* If it is used after a variable reference, then the value is first read and then the variable is incremented or decremented by 1.
```
int i=1;
int j=i++;//j=1,i=2
int k=++i;//i=3,k=3
int m=i--;//m=3,i=2
int n= 9+--i;//i=1,n=10
```
### 3. Logical Operators
 *  result of any of these comparison is a boolean.
 
symbol| name
------|-------
`<` |less than
`<=` |less than or equal to == equal to
`!=` | not equal to
`>=` |greater than or equal to
`>` | greater than
`!` | not (prefix)
`&&`| conditional and 
`||` | conditional or

### 4.The Assignment Operator
> The standard assignment operator in Java is “=”
* The value of an assignment operation is the value of the expression that was assigned
```
j = k = 25;
```

### Type Conversions
#### Casting 
> an operation that allows us to change the type of a value.
* we can take a value of one type and cast it into an equivalent value of another type
##### 1. Explicit Casting
*  without explicit use of the casting operator. However, if attempting to do an implicit narrowing cast, a compiler error results
```
(type) exp
```
##### 2. Implicit Casting
* Implicit casting also occurs when performing arithmetic operations involving a mixture of numeric types.
* There is one situation in Java when only implicit casting is allowed, and that is in string concatenation.
```
String s = Integer.toString(22); // this is good
String t = "" + 4.5;// correct, but poor style
String u ="Value="+ 13; // this is good
```

# Control Flow
## Switch Statements
> Java provides for multiple-value control flow

*  If there is no matching label, then control flow jumps to “default.”
* Control flow “falls through” to the next case if the code for a case is not ended with a break statement
```
switch (d) { 
 case MON:
  System.out.println("This is tough.");
  break; 
 case TUE:
  System.out.println("This is getting better.");
  break; 
 default:
  System.out.println("Day off!"); }
```

# Simple Input and Output

## Simple Output Methods
* `System.out`: performs output to the “standard output” device
	* characters are put in a temporary location, called a buffer

## Simple Input
* Using the `java.util.Scanner` class
   * A simple way of reading input with this object is to use it to create a Scanner object
   * The Scanner class reads the input stream and divides it into tokens
   *  which are strings of characters separated by delimiters(default: whitespace)
   
* `System.in`:  performing input from the Java console window(standard input devic)

```
public static void main(String[] args) {
	Scanner scan =new Scanner(System.in);
	System.out.println("Please enter some thing");
	double age= scan.nextDouble();
	System.out.println("Please enter heart rate");
	int rate= scan.nextInt();
	System.out.println(age+" "+rate);
	}
```
# 	
