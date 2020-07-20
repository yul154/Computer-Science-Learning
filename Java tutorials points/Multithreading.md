# Multithreading
A multi-threaded program 
* Contains two or more parts that can run concurrently 
* Each part can handle a different task at the same time making optimal use of the available resources specially when your computer has multiple CPUs.
* Each of the threads can run in paralle

## Life Cycle of a thread

* `new`:  A new thread begins its life cycle in the new state. It remains in this state until the program starts the thread.
* `Runnable`:A thread in this state is considered to be executing its task.
* `Waiting`: a thread transitions to the waiting state while the thread waits for another thread to perform a task. A thread transitions back to the runnable state only when another thread signals the waiting thread to continue executing.
* `Timed Waiting`: A runnable thread can enter the timed waiting state for a specified interval of time. A thread in this state transitions back to the runnable state when that time interval expires or when the event it is waiting for occurs.
* `Terminated`: A runnable thread enters the terminated state when it completes its task or otherwise terminates.

<img width="410" alt="Screen Shot 2020-07-01 at 11 16 04 AM" src="https://user-images.githubusercontent.com/27160394/86267394-41ae9f00-bb8c-11ea-8465-7840be20aff6.png">


## Thread Priorities
> Operating system determine the order in which threads are scheduled.

* Thread scheduler assigns processor to a thread based on priority of thread.
* Accepted value of priority for a thread is in range of 1 to 10
* There are 3 static variables defined in Thread class for priority.
```
public static int MIN_PRIORITY;
public static int NORM_PRIORITY;
public static int MAX_PRIORITY;
```
* Get and Set Thread Priority
```
public final int getPriority()
public final void setPriority(int newPriority)
```

## Create a Thread

**There are two ways to create a thread**
1. implement Runnable interface
2. extends Thread class

**Implement Runnable interface**

1. implement a run() method provided by a Runnable interface.
```
class RunnableDemo implements Runnable{
   public void run(){}
}
```
2. you will instantiate a Thread object 
```
Thread(Runnable threadObj, String threadName);
```
3. start it by calling start( ) method, which executes a call to run( ) method.
```
 MyThread mt = new MyThread();
Thread t = new Thread(mt);
t.start();
```

**Extends Thread class**
1. Override run( ) method available in Thread class
  * This method provides an entry point for the thread and you will put your complete business logic inside this method.
2. start it by calling start( ) method, which executes a call to run( ) method
```
public class MyThread extends Thread{
    public void run(){
       //
    }
    
    public static void main( String args[] )
     {
        MyThread mt = new  MyThread();
        mt.start();
     }
}
```

## Class Thread

A *thread* is a thread of execution in a program.

Object Methods
```
Thread(Runnable target)
public void start();
public void run();
public final void setName(String name);
public final void setPriority(int priority);
public final void setDaemon(boolean on)
public void interrupt()
public final void join(long millisec)//Waits at most millis milliseconds for this thread to die.
public final boolean isAlive()
```

Static Methods
```
public static void yield()//A hint to the scheduler that the current thread is willing to yield its current use of a processor.
public static void sleep(long millisec) //Causes the currently executing thread to sleep (temporarily cease execution) for the specified number of milliseconds, subject to the precision and accuracy of system timers and schedulers.
public static boolean holdsLock(Object x)// Returns true if the current thread holds the lock on the given Object.
public static Thread currentThread() //Returns a reference to the currently running thread, which is the thread that invokes this method.
public static void dumpStack()// Prints the stack trace for the currently running thread, which is useful when debugging a multithreaded application.
```
---
#  Multithreading

## Thread Synchronization

**Monitor**
* Synchronize the action of multiple threads and make sure that only one thread can access the resource at a given point in time
* Each object in Java is associated with a monitor, which a thread can lock or unlock. Only one thread at a time may hold a lock on a monitor

**synchronized blocks** 
* creating threads and synchronizing their task
```
synchronized(objectidentifier) { // objectidentifier a reference to an object whose lock associates with the monitor that the synchronized statement represents.
// Access shared variables and other shared resources
}

```

**Interthread Communication**
>  two or more threads exchange some information.

There are three simple methods and a little trick which makes thread communication possible.
```
public void wait()// Causes the current thread to wait until another thread invokes the notify() method or the notifyAll() method for this object
public void notify()// Wakes up a single thread that is waiting on this object's monitor.
public void notifyAll()// Wakes up all the threads that called wait( ) on the same object.
```
* All three methods can be called only from within a synchronized context.

### Thread Deadlock
> two or more threads are blocked forever, waiting for each other. 

Occur scenarios: when multiple threads need the same locks but obtain them in different order.


### Thread Control
```
public void suspend();//puts a thread in the suspended state and can be resumed using resume() method.
public void stop();// This method stops a thread completely.
public void resume();// This method resumes a thread, which was suspended using suspend() method.
```

