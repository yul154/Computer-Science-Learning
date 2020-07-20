# Naive Array Lists

* Accessing the ith element of an array takes constant time on a modern computer.


# Testing

* `!=` and `==` compare the context of memory box(they are pointing the same object?)
* `.equals()`: compare all items of object not address
* When you create a new method, write down a corresponding test method which have signature and expected output.

## Unit Test
<img width="314" alt="Screen Shot 2020-06-08 at 5 10 15 PM" src="https://user-images.githubusercontent.com/27160394/84085329-f3521a00-a9aa-11ea-8a74-d9523de8e768.png">

### Pors
* Build confidence in basic modules.
* Decrease debugging time.
* Clarify the task.

### Cons
* Building tests takes time.
* May provide false confidence.
* Hard to test units that rely on others.

## Integration Test
> Individual units are combined and tested as a group

### Pro
* The purpose of this level of testing is to expose faults in the interaction between integrated units.
* Unit testing is not enough to ensure modules interact properly or that system works as expected.

### Cons
* Can be tedious to do manually.
* Can be challenging to automate.
* Testing at highest level of abstraction may miss subtle or rare errors.


## Test-Driven Development (TDD)

Steps
* Identify a new feature
* Write a unit test for that feature
* Run the test, fail(red)
* Write code that passes test(green)
* Refactor code to make it more cleaner or faster

<img width="282" alt="Screen Shot 2020-06-08 at 5 14 29 PM" src="https://user-images.githubusercontent.com/27160394/84085589-88eda980-a9ab-11ea-8c50-378978703a01.png">

## Junit

### New Syntax
* Annotate each test with `@org.junit.Test`
* Change all test methods to non-static.
* Use a JUnit runner to run all tests and tabulate results
```
@org.junit.Test
	public void testfindSmallest() {
		int[] input= {2,3,1,6,5,7,0};
		int expect= 0;
		int actual = Sort.findSmallest(input,1);
		Assert.assertEquals(expect, actual);	
	}
```
### New Syntax 2
* import: To avoid this we’ll start every test file with:
```
import org.junit.Test;
import static org.junit.Assert.*;

```

## Select Sort
1. Find the smallest item
2. Move it to the front
3. Selection sort the remaining N-1 items


