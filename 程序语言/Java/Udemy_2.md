### Scope

From packages to ...



### Packages

**Package Challenge** 

Create a suitably named package containing a class called Series with the following static methods:

nSum(int n) returns the sum of all numbers from 0 to n. The first 10 number are:

0, 1, 3, 6, 10, 15, 21, 28, 36, 45, 55

factorial(int n) returns the product of all number from 1 to n. i.e. 1 * 2 * 3 * ... * (n - 1) * n.

fibonacci(n) returns the nth Fibonacci number. These are defined as:

f(0) = 0;

f(1) = 1;

f(n) = f(n - 1) + f(n - 2)



**Expose to jar file:**

File > Project Structure > Artifacts > Add (+) > JAR > From modules with dependencies ...

Build > Make project > Build Artifacts

**Import a jar file:**

File > Project Structure > Libraries > Add (+) > find the jar file