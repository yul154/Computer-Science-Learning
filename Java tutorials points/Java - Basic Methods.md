# Java – Date & Time
> This class encapsulates the current date and time.

* Available in `java.util` package

* Constructors of Date
```
/** This constructor initializes the object with the current date and time.*/
Date()

/** This constructor accepts an argument that equals the number of milliseconds that have elapsed since midnight, January 1, 1970.*/
Date(long millisec)
```

## Methods with Description

1. `boolean after(Date date)` & `boolean before(Date date)`& `boolean equals(Object date)`: Returns true if the invoking Date object contains a date that is later (eariler) than the one specified by date, otherwise, it returns false.
2. `Object clone()`:Duplicates the invoking Date object.
3. `int compareTo(Date date)` & `int compareTo(Object obj)`:Compares the value of the invoking object with that of date. Returns 0 if the values are equal. Returns a negative value if the invoking object is earlier than date. Returns a positive value if the invoking object is later than date.
4.`long getTime( )`: Returns the number of milliseconds that have elapsed since January 1, 1970.
5.`int hashCode( )`:Returns a hash code for the invoking object.
6. `void setTime(long time)`: Sets the time and date as specified by time, which represents an elapsed time in milliseconds from midnight, January 1, 1970
7. `String toString( )`: Converts the invoking Date object into a string and returns the result.

### Date Formatting
#### 1. `SimpleDateFormat` 
> is a concrete class for formatting and parsing dates in a locale-sensitive manner
* To specify the time format, use a time pattern string. In this pattern, all ASCII letters are reserved as pattern letters.

<img width="440" alt="Screen Shot 2020-06-24 at 1 39 34 PM" src="https://user-images.githubusercontent.com/27160394/85614067-27227600-b620-11ea-81db-daeb02e440d4.png">

#### 2. `printf`
>  format the output.

```
System.out.printf(format, arguments);
System.out.printf(locale, format, arguments);
```

* Format Rules
```
%[flags][width][.precision]conversion-character
```
 - [flags] define standard ways to modify the output and are most common for formatting integers and floating point numbers.

 - [width] specifies the field width for outputting the argument. It represents the minimum number of characters written to the  output.

 - [.precision] specifies the number of digits of precision when outputting floating-point values. Additionally, we can use it to define the length of a substring to extract from a String.
 
 |conversion character| description|
 |--------------------|------------|
 |s| formats strings| 
 |d|formats decimal integers
 |f|formats the floating-point numbers
 |t| formats date/time values
 
 
 ### Sleeping for a While
 > sleep for any period of time from one millisecond up to the lifetime of your computer. 
 
 ## `GregorianCalendar` Class
 >  implements the normal Gregorian calendar 
 * a concrete implementation of a Calendar class 
 ---
 
 # Regular Expressions
> pattern matching with regular expressions

*  In the java.util.regex package 
* A regular expression is a special sequence of characters that helps you match or find other strings or sets of strings, using a specialized syntax held in a pattern.

`java.util.regex` package primarily consists of three classes:

1. Pattern Class:  a compiled representation of a regular expression
2. Matcher Class: the engine that interprets the pattern and performs match operations against an input string
3. PatternSyntaxException:an unchecked exception that indicates a syntax error in a regular expression pattern.

## Capturing Groups
>  a way to treat multiple characters as a single unit. 
* They are created by placing the characters to be grouped inside a set of parentheses
* one pair of parentheses is one group.
* `groupCount`: To find out how many groups are present in the expression

## Basic Regular Expressionn Syntax
1. Common matching symbols
<img width="542" alt="Screen Shot 2020-06-24 at 2 07 01 PM" src="https://user-images.githubusercontent.com/27160394/85616912-ffcda800-b623-11ea-9e6b-46817871ffb1.png">

2.  Meta characters
<img width="542" alt="Screen Shot 2020-06-24 at 2 07 46 PM" src="https://user-images.githubusercontent.com/27160394/85616982-1bd14980-b624-11ea-8b73-2a47754bd3d7.png">

## Methods of the Matcher Class
1. `public int start()`: Returns the start index of the previous match.
2. `public int end()`: Returns the offset after the last character matched.
3. `public boolean lookingAt()`: Attempts to match the input sequence, starting at the beginning of the region, against the pattern.
4. `public boolean find()`: Attempts to find the next subsequence of the input sequence that matches the pattern.
5. `public boolean matches()`:Attempts to match the entire region against the pattern.
---

# Methods
> A Java method is a collection of statements that are grouped together to perform an operation. 

## Creating Method

```
modifier returnType nameOfMethod (Parameter List) { 
    // method body
}
```
* modifier: It defines the access type of the method and it is optional to use.
* returnType: Method may return a value.
* nameOfMethod: This is the method name. The method signature consists of the method name and the parameter list.
   
## Method Calling
1. When a program invokes a method
2. the program control gets transferred to the called method.
3. This called method then returns control to the caller in two conditions, 
  1. the return statement is executed.
  2. it reaches the method ending closing brace.
  
*  `void`: allows us to create methods which do not return a value

## Method Overloading
* When a class has two or more methods by the same name but different parameters
* It is different from overriding. In overriding, a method has the same method name, type, number of parameters,

## Command-Line Arguments
* pass some information into a program when you run it
* accomplished by passing command-line arguments to main( ).

## Constructors
* initializes an object when it is created.
* Has the same name as its class and is syntactically similar to a method
* Have no explicit return type.
* Parameterized Constructor: need a constructor that accepts one or more parameters.


## `this`
>  as a reference to the object of the current class
* with in an instance method or a constructor.

<img width="241" alt="Screen Shot 2020-06-24 at 2 24 01 PM" src="https://user-images.githubusercontent.com/27160394/85618395-5d62f400-b626-11ea-8270-6790a8385409.png">

Used to
1. Differentiate the instance variables from local variables if they have same names, within a constructor or a method.
```
class Student{
  int age; 
  Student(int age){ 
  this.age=age;
  }
}
```
2. Call one type of constructor (parametrized constructor or default) from other in a class. It is known as explicit constructor invocation.
```
 class Student{
    int age
    Student(){
      this(20);
    }
    Student(int age){ 
      this.age=age;
    }
}
```
## Variable Arguments(var-args)
*  pass a variable number of arguments of the same type to a method.
* `...`:Only one variable-length parameter may be specified in a method, and this parameter must be the last paramete

```
public static void printMax( double... numbers)
```

## `finalize()`
> define a method that will be called just before an object's final destruction by the garbage collector. 
* it can be used to ensure that an object terminates cleanly.
* This method is used to perform some final operations or clean up operations on an object before it is removed from the memor
---

# Files and I/O

* All these streams represent an input source and an output destination.
* The stream in the java.io package supports many data such as primitives, object, localized characters

## Stream
> A stream can be defined as a sequence of data. 
* InPutStream: The InputStream is used to read data from a source.
* OutPutStream: The OutputStream is used for writing data to a destination.

### 1.Byte Streams
* perform input and output of 8-bit bytes. 

```
public static void main(String[] args) {
		
		FileInputStream input =null;
		FileOutputStream output = null;
		
		try {
			input = new FileInputStream("input,txt");
			output = new FileOutputStream("output.txt");
			
			int c;
			
			while ((c = input.read()) != -1) {
				output.write(c);
			}
			
		}finally {
			if (input !=null) {
				input.close();
			}
			if (out != null) {
				
				output.close();
			}
		}
		
	}
```

### 2. Character Streams
* Java Character streams are used to perform input and output for 16-bit unicode. 
```
in = new FileReader("input.txt");
out = new FileWriter("output.txt");
```

## Standard Streams
* provide support for standard I/O where the user's program can take input from a keyboard
* produce an output on the computer screen

Java provides three standard streams:
 
1. Standard Input:This is used to feed the data to user's program and usually a keyboard is used as standard input stream and represented as `System.in`.
2. Standard Output: This is used to output the data produced by the user's program and usually a computer screen is used for standard output stream and represented as `System.out`.
3. Standard Error:This is used to output the error data produced by the user's program and usually a computer screen is used for standard error stream and represented as `System.err`.

```
cin = new InputStreamReader(System.in);
```
## Reading and Writing Files

<img width="438" alt="Screen Shot 2020-06-24 at 3 01 28 PM" src="https://user-images.githubusercontent.com/27160394/85621877-9782c480-b62b-11ea-8d33-76b14e4f64f7.png">

### FileInputStream
```
InputStream f = new FileInputStream("C:/java/hello");

File f = new File("C:/java/hello");
InputStream f = new FileInputStream(f);
```
### ByteArrayInputStream
-- allows a buffer in the memory to be used as an InputStream.
```
ByteArrayOutputStream bOutput = new ByteArrayOutputStream(12);
```
 
### DataInputStream : used in the context of DataOutputStream and can be used to read primitives.
* DataInputStream is a kind of InputStream to read data directly as primitive data types
```
InputStream in = DataInputStream(InputStream in);
```

### FileOutputStream
> used to create a file and write data into it.
* The stream would create a file

```
OutputStream f = new FileOutputStream("C:/java/hello")

File f = new File("C:/java/hello");
OutputStream f = new FileOutputStream(f);
```

### ByteArrayOutputStream
>  creates a buffer in memory and all the data sent to the stream is stored in the buffer.
```
ByteArrayOutputStream bOutput = new ByteArrayOutputStream(12);//  creates a ByteArrayOutputStream having buffer of the given size
```

### DataOutputStream
> lets you write the primitives to an output source.
```
DataOutputStream dataOut = new DataOutputStream(new FileOutputStream("E:\\file.txt"));
```

## File Navigation and I/O

### 1.File Class
* Used for creation of files and directories, file searching, file deletion,

#### 2.FileReader Class
* This class inherits from the InputStreamReader class.
* FileReader is used for reading streams of characters.

### 3.FileWriter Class
* This class inherits from the OutputStreamWriter class. 
* The class is used for writing streams of characters.

### Directories in Java
> A directory is a File which can contain a list of other files and directories
* use `File` object to create directories,
* There are two useful utility methods to create directories
1. `mkdir( )`:creates a directory, returning true on success and false on failure.
2. `mkdirs()`:creates both a directory and all the parents of the directory.
```
public class CreateDir {
	public static void main(String args[]) {
		String dirname = "/tmp/user/java/bin"; 
		File d = new File(dirname); // Create directory now.
		d.mkdirs();
	} 
}
```

* `list()`:provided by File object to list down all the files and directories available in a directory
---

# Exceptions
> An exception (or exceptional event) is a problem that arises during the execution of a program. 

* Checked exceptions: occurs at the compile time, these are also called as compile time exceptions.
* Unchecked exceptions:An unchecked exception is an exception that occurs at the time of execution. These are also called as Runtime Exception

Exception Hierarchy
<img width="364" alt="Screen Shot 2020-06-24 at 6 02 31 PM" src="https://user-images.githubusercontent.com/27160394/85635990-e1c46f80-b644-11ea-9ddf-df879324635b.png">

##  Important methods available in the Throwable class.

1. `public String getMessage()`:Returns a detailed message about the exception that has occurred. 
2. `public Throwable getCause()`:Returns the cause of the exception as represented by a Throwable object.
3. `public String toString()`:Returns the name of the class concatenated with the result of getMessage
4. `public void printStackTrace()`: Prints the result of toString() along with the stack trace to System.err, the error output stream.
5. `public StackTraceElement [] getStackTrace()`:Returns an array containing each element on the stack trace. The element at index 0 represents the top of the call stack, and the last element in the array represents the method at the bottom of the call stack.
6. `public Throwable fillInStackTrace()`:Fills the stack trace of this Throwable object with the current stack trace, adding to any previous information in the stack trace.

## Catching Exceptions

* use a combination of the try and catch keywords
```
try{

}catchc(Exceptioname e1){

}
```
* If an exception occurs in protected code, the catch block (or blocks) that follows the try is checked
* If the type of exception that occurred is listed in a catch block, the exception is passed to the catch block much as an argument is passed into a method parameter.

* Catching Multiple Type of Exceptions using only one catch block
```
catch (IOException|FileNotFoundException ex) { 
	logger.log(ex);
	throw ex;
}
```

## `Throws/Throw`

* `throws`:If a method does not handle a checked exception, the method must declare it 
* `throw`:You can throw an exception, either a newly instantiated one or an exception that you just caught
* A method can declare that it throws more than one exception, in which case the exceptions are declared in a list separated by comma
```
public void withdraw(double amount) throws RemoteException, InsufficientFundsException
```

## `finally`
> The finally block follows a try block or a catch block. A finally block of code always executes, irrespective of occurrence of an Exception.

* A catch clause cannot exist without a try statement.
* It is not compulsory to have finally clauses whenever a try/catch block is present.
* The try block cannot be present without either catch clause or finally clause.
* Any code cannot be present in between the try, catch, finally blocks.

## The try-with-resources
* automatically closes the resources used within the try catch block.
* Simply need to declare the required resources within the parenthesis
* the created resource will be closed automatically at the end of the block.
```
try(FileReader fr=new FileReader("file path")) {
    //use the resource
    }catch(){
       //body of catch
     }
}
```

## User-defined Exceptions
* All exceptions must be a child of Throwable.
* If you want to write a checked exception that is automatically enforced by the Handle or Declare Rule, you need to extend the Exception class.
* If you want to write a runtime exception, you need to extend the RuntimeException class.
---
# Inner Classes

## Nested Classes
> A class withinn another class
```
class Outer_class{
   class Nested_class{
   	}
}
```
There are two types of nested classes
* Non-static nested classes: These are the non-static members of a class.
* Static nested classes: These are the static members of a class.

<img width="351" alt="Screen Shot 2020-06-24 at 6 37 52 PM" src="https://user-images.githubusercontent.com/27160394/85637819-d0ca2d00-b649-11ea-975b-0a7480604625.png">

## Inner Classes
*  if we have the class as a member of other class, then the inner class can be made private

Three types of inner classes
1. Inner Class: write a class within a class. Unlike a class, an inner class can be private 
```
class Outer_Demo {
	//private variable of the outer class private int num= 175;
	//inner class
	public class Inner_Demo{
	   public int getNum(){
		System.out.println("This is the getnum method of the inner class"); 
			return num;
       } 
    }
}
```
2. Method-local Inner Class :write a class within a method and this will be a local type. the scope of the inner class is restricted within the method.
```
void my_Method(){
   int num = 23;
  //method-local inner class 
  class MethodInner_Demo{ 
    public void print(){
         System.out.println("This is method inner class "+num); 
       }
    }//end of inner class
      
  //Accessing the inner class
  MethodInner_Demo inner = new MethodInner_Demo(); 
  inner.print();
}

```
3. Anonymous Inner Class: An inner class declared without a class name 
  * Generally, they are used whenever you need to override the method of a class or an interface.
```
abstract class AnonymousInner{
    public abstract void mymethod();
}
public class Outer_class {
   public static void main(String args[]){
       AnonymousInner inner = new AnonymousInner(){ 
          public void mymethod(){
              System.out.println("This is an example of anonymous inner class");
         } 
      };
       inner.mymethod(); }
}

```
### Static Nested Class
>  a nested class which is a static member of the outer class

* It can be accessed without instantiating the outer class
```
class MyOuter {
    static class Nested_Demo{
    }
}
```
