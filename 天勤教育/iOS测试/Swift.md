## 1. 基础部分

### 常量和变量

```swift
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
var x = 0.0, y = 0.0, z = 0.0

// 类型标注
var welcomeMessage: String
var red, green, blue: Double
```

**命名：**

+ 可以使用任何字符，包括 Unicode 字符；
+ 不能包含数学符号，箭头，保留的（或者非法的）Unicode 码，连线与制表符。
+ 不能以数字开头；

不能使用相同的名字重复声明变量或常量，不能修改值的类型。

### 类型安全和类型推断

Swift 是类型安全的，所以它会在编译代码时进行类型检查（type checks），并把不匹配的类型标记为错误。如果没有显式指定类型，Swift 会使用类型推断（type inference）来选择合适的类型。

### 数字型字面量

```swift
let decimalInteger = 17
let binaryInteger = 0b10001
let octalInteger = 0o21  // 八进制
let hexadecimalInteger = 0x11
```

### 数值型类型转换

```swift
// 整数
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThounsand + UInt16(one)

// 浮点
```

### 类型别名

```swift
typealias AudioSample = UInt16
var maxAmplitudeFound = AudioSample.min  // UInt16.min
```

### 布尔值

```swift
let orangesAreOrange = true

let i = 1
if i {
  // 这个例子不会通过编译，会报错
  // 在需要使用 Bool 类型的地方使用了非布尔值
}

if i == 1 {
  // 这个例子会编译成功
}
```

### 元组

元组（tuples）把多个值组合成一个复合值。元组内的值可以是任意类型，并不要求是相同类型。

```swift
let http404Error = (404, "Not Found")

// 元组内容分解 decompose
let (statusCode, statusMessage) = http404Error
// statusCode == 404, statusMessage == "Not Found"


```



### 可选类型



### 错误处理



### 断言



## 2. 基本运算符

赋值运算符没有返回值。

```swift
let (x, y) = (1, 2) // x == 1, y == 2
```

算数运算符：+ - * /

求余运算符：%

```swift
9 % 4 // 1
-9 % 4 // -1
// a % b 和 a % -b 结果相同
```



## 3. 字符串和字符

字符串是有序的字符类型的值的集合。

### 初始化空字符串

```swift
var emptyString = ""
var anotherEmptyString = String()

// 检查字符串是否为空
if emptyString.isEmpty {
  print("Nothing to see here")
}
```

### 使用字符

```swift
for character in "Dog!".characters {
  print(character)
}

// 建立字符常量
let exclamationMark: Character = "!"

// 使用 Character 数组初始化字符串
let catCharacters: [Character] = ["C", "a", "t", "!"]
let catString = String(catCharacters)
```

### 连接字符串和字符

```swift
let string1 = "hello"
let string2 = " there"
var welcome = string1 + string2
var instruction = "look over"
instruction += string2
let exclamationMark: Character = "!"
welcome.append(exclamationMark)
```

### 字符串插值

```swift
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
```

### 访问和修改字符串

+ 字符串索引
+ 插入和删除

### 比较字符串



## 5. 控制流

### 提前退出

==不明白 guard==





## 6. 函数

### 定义和调用

```swift
func greet(person: String) -> String {
  let greeting = "Hello, " + person + "!"
  return greeting
}

print(greet(person: "Anna"))
```

为了简化上面的函数，可以将消息的创建和返回写成一句：

```swift
func greetAgain(person: String) -> String {
  return "Hello again, " + person + "!"
}
```



### 参数与返回值

```swift
// 无参函数
func sayHelloWorld() -> String {
  return "hello world"
}

// 多参函数
func greet(person: String, alreadyGreeted: Bool) -> String {
  // Function body
}
print(greet(person: "Tim", alreadyGreeted:true))

// 无返回值，实际返回一个 Void 值，它是一个空的元组(tuple)
func greet(person: String) {
  print("Hello, \(person)!")
}

// 多重返回值函数
func minMax(array: [Int]) -> (min: Int, max: Int) {
  var currentMin = array[0]
  var currentMax = array[0]
  for value in array[1..<array.count] {
    if value < currentMin {
      currentMin = value
    } else if value > currentMax {
      currentMax = value
    }
  }
  return (currentMin, currentMax)
}

// 可选元组返回值
func minMax(array: [Int]) -> (min: Int, max: Int)? {
  if array.isEmpty { return nil }
  // same as above func
}
```



### 参数标签和参数名称

参数标签 argument label，参数名称 parameter name

==输入输出参数==

```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
  let temporaryA = a
  a = b
  b = temporaryA
}

var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)
```



### 函数类型

函数的类型由函数的参数类型和返回类型组成。

```swift
func addTwoInts(_ a: Int, _ b: Int) -> Int {
  return a + b
}

func multiplyTwoInts(_ a: Int, _ b: Int) -> Int {
  return a * b
}
```

这两个函数都接受两个 Int 值，返回一个 Int 值。它们的类型是 (Int, Int) -> Int。

```swift
var mathFunction: (Int, Int) -> Int = addTwoInts
// addTwoInts 和 mathFunction 有同样的类型，所以这个赋值过程在 Swift 类型检查(type-check)中是允许的

print("Result: \(mathFunction(2, 3))")
// Result: 5

mathFunction = multiplyTwoInts
print("Result: \(mathFunction(2, 3))")
// Result: 6
```

就像其它类型一样，当赋值一个函数给常量或变量时，可以让 Swift 来推断其函数类型：

```swift
let anotherMathFunction = addTwoInts
// 被推断为 (Int, Int) -> 类型
```



**函数类型作为参数类型**



### 嵌套函数

把函数定义在别的函数体中，称作嵌套函数(nested functions)。

```swift
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
  func stepForward(input: Int) -> Int { return input + 1 }
  func stepBackward(input: Int) -> Int { return input - 1 }
  return backward ? stepBackward : stepForward
}
var currentValue = -4
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
// moveNearerToZero now refers to the nested stepForward() function
while currentValue != 0 {
  print("\(currentValue)...")
  currentValue = moveNearerToZero(currentValue)
}
print("zero!")
// -4...
// -3...
// -2...
// -1...
// zero!
```



## 8. 枚举

### 语法

枚举为一组相关的值定义了一个共同的类型，使你可以在你的代码中以类型安全的方式来使用这些值。

```swift
enum CompassPoint {
  case north
  case south
  case east
  case west
}
var directionToHead = CompassPoint.west
```



### 使用 Switch 语句匹配枚举值

```swift
directionToHead = .south  // 类型已知可以省略枚举类型名
switch directionToHead {
  case .north:
  	print("Lots of planets have a north")
  case .south:
  	print("Watch out for penguins")
  case .east:
  	print("Where the sun rises")
  case .west:
  	print("Where the skies are blue")
}
```



### 关联值

```swift
enum Barcode {
  case upc(Int, Int, Int, Int)
  case qrCode(String)
}
var productBarcode = Barcode.upc(8, 85909, 51226, 3)
productBarcode = .qrCode("ABCDEFGHIJKLMNOP")

switch productBarcode {
  case .upc(let numberSystem, let manufacturer, let product, let check):
  	print("UPC: \(numberSystem), \(manufacturer), \(product), \(check).")
  case .qrCode(let productCode):
  	print("QR code: \(productCode).")
}
// 如果一个枚举成员的所有关联值都被提取为常量，或者都被提取为变量，可简化为
switch productBarcode {
  case let .upc(numberSystem, manufacturer, product, check):
  	print("UPC: \(numberSystem), \(manufacturer), \(product), \(check).")
  case let .qrCode(productCode):
  	print("QR code: \(productCode).")
}
```





### 原始值



### 递归枚举



## 9. 类和结构体





### 类和结构体的选择

当符合一条或多条以下条件时，请考虑构建结构体：

+ 该数据结构的主要目的是用来封装少量相关简单数据值。
+ 有理由预计该数据结构的实例在被赋值或传递时，封装的数据会被拷贝而不是被引用。
+ 该数据结构存储的值类型属性，也应该被拷贝，而不是被引用。
+ 该数据结构不需要去继承另一个既有类型的属性或者行为。

### 字符串、数组和字典类型的赋值与复制行为

Swift 中，许多基本类型，诸如 string, Array 和 Dictionary 类型均以结构体的形式实现。



## 10. 属性

### 存储属性



### 计算属性



### 属性观察器



### 全局变量和局部变量



