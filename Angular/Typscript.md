> Angular 权威教程

## 2.5 类

类的声明、属性、方法和构造函数。

```typescript
// 类的声明
class Person {
    // 属性
    first_name: string;
    last_name: strign;
    age: number;

    // 方法
    greet() {
        console.log("Hello", this.first_name);
    }

    // 构造函数
    constructor (first_name: string, last_name: string, age: number){
        this.first_name = first_name;
        this.last_name = last_name;
        this.age = age;
    }
}
```

类的继承

？？？

## 2.6 工具

#### 箭头函数

```typescript
// ES5
function (line) {
    console.log(line);
}

// Typscript
(line) => {
    console.log(line);
}
```

箭头函数共享环绕它的外部代码的 this。

### 模板字符串

1. 可以在模板字符串中使用变量；
2. 支持多行字符串。

```typescript
var firstName = "Carl";
var lastName = "Li";

var greeting = `Hello ${firstName} ${lastName}`;

var template = `
<div>
    <h1>Hello</h1>
</div>`
```
