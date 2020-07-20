# Intro,Hello World, Java
## First Java Code
```
public class HelloWorld {
  /** First program */
	public static void main(String[] args) {
		System.out.println("hello world");
	}
}
```
* In Java, All code must in a class
* Classes are defined with "public class CLASSNAME"
* We delimit the beginning and end of segments of code using '{}'.
* We Must end lines with a semicolon.
* The code we want to runn must be inside main method

## Staic Typed Language
1. Before Java variables can be used, they must be declared
2. Java variables must have a specific type
3. Java variabbles types can never change.
4. The compiler checks that all the types in your program are compatible before the program ever runs!

## Defining functions in Java

1. Functions must be declared as part of a class in Java. A function that is part of a class is called a "method".
   So in Java, all functions are methods.
2. To define a function in Java, we use "public static",We will see alternate ways of defining functions later.
3. All parameter of a function must have a declared type, and the return value of the function must have a declated type.
4. Functions in Java return only one value!
```
public static int string// not allowed
```
5. it's nice to put a little comment at the top descripting what it does


# Using and Defining Classes
## Compilation
<img width="514" alt="Screen Shot 2020-06-02 at 2 09 39 PM" src="https://user-images.githubusercontent.com/27160394/83559764-bc779200-a4da-11ea-88f3-11e862e786a7.png">

* javac is used to compile programs. 
* java is used to execute programs. 
* We must always compile before execution.
### .class file
* .class file has been type checked.
* .class file are simpler for machine to execute

## Defining and Instantiating Classes
* Every method is assoicated with some class
* To run a class, we must define a main method

### Object Instantiation 
* Classes can contain not only functions but also data
* Classes can be instantiated as objects.
* Instantiating a class is almost always done using the new keyword
* Constructors tell Java what to do when a program tries to create an instance of a class
```
public class Dog {
  public int weightInPounds;// instance variable:

  public Dog(int startingWeight) {// constructor: construct an object with parameters
  weightInPounds = startingWeight;
  }
 
  public void makeNoise() { // no-static method(instance method): invoked by an instance
  if (weightInPounds < 10) {
  System.out.println("yipyipyip!");
        } else if (weightInPounds < 30) {
          System.out.println("bark. bark.");
      } else {
          System.out.println("woof!");
      }
     }
}
```

```
public class DogLauncher {
  public static void main(String[] args) 
{
    Dog smallDog;//declaration
    new Dog(20);// instantiation
    smallDog = new Dog(5);//instantiation and assignment
    Dog hugeDog = new Dog(150);//Declaration, Instantiation and Assignment
    smallDog.makeNoise();
    hugeDog.makeNoise();
 
 }
}

```
### Arrays of Objects
* Use the `new` keyword to create th array
* Use new again for each object tha you want to put in the array
```
Dog[] dogs= new Dog[2
dogs[0]=new Dog(8);
dogs[1]= new Dog(10);
```
### Static VS Instance Method
* Static methods are invoked using the class name, e.g. Dog.makeNoise();
* Instance methods are invoked using an instance name, e.g. maya.makeNoise();
* Some classes are never instantiated. For example, Math.
* Static variables
  * apply for all objects and shared with all object.
  * Static variables should be accessed using the class name
* Use the `this` keyword to refer to the current instance. This is equivalent to self in Python.

# Terminal

* `cd` : change your working directory
* `pwd`:present working directory
* `.`: your current directory
* `..`:one parent directory above your current directory
* `ls`:list files/folders in directory
* `mkdir`: make a directory
* `rm`:remove a file
* `cp lab1/original lab2/duplicate`:copy a file
* ` mv lab1/original lab2/original` :move or rename a file

# Git
## Local repositories

commit | fucntionality
-------|-----------------
`$ git init`|initialize a Git repository, Git creates a .git subdirectory. Inside this directory
`$ git status`| determining the exact status of each file in your repository.
`$ git add FILE`| lets you stage a file
`$ git commit -m MESSAGE`| commit them as one block with a message
`$ git log` | In order to see previous commits
`$ git reset HEAD [file]` |Unstage a file that you haven’t yet committed
`$ git add [forgotten-file]; $ git commit --amend` | Amend latest commit 
`$ git checkout -- [file]` |file back to how it was before your modifications

## Remote repositories
commit | fucntionality
-------|-----------------
`git clone [remote-repo-URL]`| 1. Makes a copy of the specified repository, but on your local computer 2. creates a working directory that has files arranged exactly like the most recent snapshot in the download repository 3. Also records the URL of the remote repository for subsequent network data transfers,gives it the special remote-repo-name “origin”.
`git remote add [remote-repo-name] [remote-repo-URL]`| Records a new location for network data transfers.
`git remote -v`| Lists all locations for network data transfers.
`git pull [remote-repo-name] master`| Get the most recent copy of the files as seen in remote-repo-name
`git push [remote-repo-name] master`| Pushes the most recent copy of your files to the remote-repo-name.
  
