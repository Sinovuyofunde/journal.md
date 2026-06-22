Error Diagnosis Challenge (Java)

## Selected Error
Here is a recursive factorial function (Java) for your reference.For reference, here is the recursive factorial function (Java): Stack Overflow java

---

# Error Analysis: StackOverflowError

## Error Description
A 'StackOverflowError' is thrown when a method continues to call itself without stopping.  
This will load the call stack until it overflows causing the program to crash.

The program crashes during this calculation when computing a factorial in this case.

---

## Root Cause
The calculateFactorial() method is recursive with the following:

To prevent recursion, there is no base case.
It continues to recurse with num - 1 indefinitely.It will recur indefinitely with num - 1.

```java
return num * calculateFactorial(num - 1);
