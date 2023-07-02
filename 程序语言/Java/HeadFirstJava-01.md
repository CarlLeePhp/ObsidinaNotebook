### Basic Structure

```java
public class BeerSong {
    public static void main (string[] args) {
        // coding here
    }
}
```



### Complier and Run

```shell
$ javac HelloWorld.java
$ java HelloWorld
```



### 基本语法

+ 大小写敏感
+ 类名：首字母大写，每个单词的首字母大写；
+ 方法名：小写字母开头，之后每个单词的首字母大写；
+ 源文件名：于类名一样；
+ 主方法入口：public static void main (String [] args)




### Array and Object

I learnt how to make an object array from chapter 4.

```java
Dog[] myDogs = new Dog[5];
int x = 0;
while (x < myDogs.length) {
    myDogs[x] = new Dog();
    // Codes ...
    
    x = x + 1;
}
```

