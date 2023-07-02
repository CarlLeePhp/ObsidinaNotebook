## Section 1

#### Introduction to Data Structures



Important

+ There can be many algorithms that accomplish the same task
+ There can be many implementations of the same algorithm



## Section 2 Arrays and Big-O Notation

#### Big-O Notation

Time complexity.



#### Arrays in Memory

+ Contiguous block in memory
+ Every element occupies the same amount of space in memory
+ If an array starts at memory address x, and the size of each element in the array is y, we can calculate the memory address of the ith element by using the following expression: x+i*y
+ If we know the index of an element, the time to retrieve the element will be the same, no matter where it is in the array

#### Big-O Values for Arrays Operations

Retrieve an Element from an Array

1. Multiply the size of the element by its index
2. Get the start address of the array
3. Add the start address to the result of the multiplication

Constant time complexity -> O(1), reads as o of one. 



| Operation                                         | Time Complexity         |
| ------------------------------------------------- | ----------------------- |
| Retrieve with index                               | O(1) Constant time      |
| Retrieve without index                            | O(n) Linear time        |
| Add an element to a full array                    | O(n) Create a new array |
| Add an element to the end of an array (has space) | O(1)                    |
| Insert or update an element at a specific index   | O(1)                    |
| Delete an element by setting it to null           | O(1)                    |
| Delete an element by shifting elements            | O(n)                    |



## Section 3 Sort Algorithms

####  Bubble Sort

+ In-place algorithm
+ O(n^2) time complexity - quadratic
+ It will take 100 steps to sort 10 items, 10,000 steps to sort 100 items, 1,000,000 steps to sort 1000 items
+ Algorithm degrades quickly

#### Selection Sort



