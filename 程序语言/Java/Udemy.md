## Scanner

```java
import java.util.Scanner;
Scanner scan = new Scanner(System.in);
int receiver;
receiver = scan.nextInt();
```



## 80 Minimum Element Challenge

+ Write a method called **readIntegers()** with a parameter called count that represents how many **integers** the user needs to enter.
+ The method needs to read from the console until all the numbers are entered, and then return an **array** containing the numbers entered.
+ Write a method **findMin()** with the **array** as a parameter. The method needs to return the **minimum value** in the **array**.
+ In the **main()** method read the **count** from the console and call the method **readIntegers()** with the **count** parameter.
+ Then call the **findMin()** method passing the **array** returned from the call to the **readIntegers()** method.
+ Finally, print the **minimum** element in the **array**.



## Array

Some good things:

```java
System.out.println("Array is " + Arrays.toString(myIntArray));
```



## LinkedList

```java
LinkedList<String> placesToVisit = new LinkedList<String>();
placesToVisit.add("Sydney");
placesToVisit.add("Perth");

placesToVisit.add(1, "Invercargill");

Iterator<String> i = placesToVisit.iterator();
while(i.hasNext()){
    System.out.println("Now visiting " + i.next());
    // ....
}
```



## Abstract Class and Interface

Use abstract class when ...

![1547694605660](E:\Notebook\Java\1547694605660.png)















