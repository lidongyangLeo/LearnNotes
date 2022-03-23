## 基础类型

#### 布尔值

```typescript
let isDone: boolean = false;
```

####  数字

和javascrip一样，tyscript里的所有数字都是浮点数。这些浮点数的类型是number。除了支持十进制和十六进制字面量，TypeScript还支持ECMAScript 2015中引入的二进制和八进制字面量。

```typescript
let decLiteral: number = 6;
let hexLiteral: number = 0xf00d;
let binaryLiteral: number = 0b1010;
let octalLiteral: number = 0o744;
```



#### 字符串

```typescript
let name: string = "bob";
name = "swift";
```

模版字符串 ``

```typescript
let name: string = `Gene`;
let age: number = 37;
let sentence: string = `Hello, my name is ${ name }.

I'll be ${ age + 1 } years old next month.`;
```

#### 数组

第一种，可以在元素类型后面接上[], 表示由此类型元素组成的一个数组。

```typescript
let list: number[] = [1,2,3];
```

第二种方式是使用数组泛型，`Array<元素类型>`；

```typescript
let list: Array<number> = [1, 2, 3];
```

#### 元组Tuple 

元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。比如，你可以定义一对值分别为`string`和`number` 类型的元组。

```typescript
// Declare a tuple type
let x: [string, number];
// Initialize it
x = ['hello', 10]; // OK
// Initialize it incorrectly
x = [10, 'hello']; // Error
```

当访问一个已知索引的元素，会得到正确的类型：

```typescript
console.log(x[0].substr(1)); // OK
console.log(x[1].substr(1)); // Error, 'number' does not have 'substr'
```

当访问一个越界的元素，会使用联合类型替代

```typescript
x[3] = 'world'; // OK, 字符串可以赋值给(string | number)类型

console.log(x[5].toString()); // OK, 'string' 和 'number' 都有 toString

x[6] = true; // Error, 布尔不是(string | number)类型
```

#### 枚举

`enum` 类型是对JavaScript标准数据类型的一个补充。像C#等其他语言一样，使用枚举类型可以为一组数值赋予友好的名字。

```typescript
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```

默认情况下，从`0`开始为元素编号。你也可以手动的指定成员的数值。

```typescript
enum Color {Red = 1, Green, Blue}
let c: Color = Color.Green;
```

枚举类型提供的一个便利是你可以由枚举的值得到它的名字。 例如，我们知道数值为2，但是不确定它映射到Color里的哪个名字，我们可以查找相应的名字：

```typescript
enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2];

alert(colorName);  // 显示'Green'因为上面代码里它的值是2
```



#### 任意值

有时候，我们会想要为那些在编程阶段还不清楚类型的变量指定一个类型。这些值可能来自于动态的内容，比如来自用户输入或第三方代码库。这种情况下，我们不希望类型检查器对这些值进行检查而是直接让它们通过编译阶段的检查。那么我们可以使用`any` 类型来标记这些变量

```typescript
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean
```

```typescript
let list: any[] = [1, true, "free"];

list[1] = 100;
```



#### 空值

 某种程度上来说，`void`类型像是与`any`类型相反，它表示没有任何类型。当一个函数没有返回值时，你通常会见到其返回值类型时`void`

```typescript
function warnUser(): void {
    alert("This is my warning message");
}
```

 声明一个`void`类型的变量没有什么用，因为你只能为它赋予`undefined`和`null`

```typescript
let unusable: void = undefined;
```

#### Null 和 Undefined

TypeScript里，`undefined` 和`null` 两者各自有自己的类型分别叫做 `undefined` 和`null` 和`void`

相似，它们的本身的类型用处不是很大。

```typescript
// Not much else we can assign to these variables!
let u: undefined = undefined;
let n: null = null;
```



#### Never 

`never`类型表示的是那些用不存在的值的类型。例如，`never`类型是那些总是会抛出异常或根本就不回有返回值的函数表达式或箭头函数表达式的返回值类型；变量也可能是`never`类型

#### 类型断言

通过类型断言这种方式可以告诉编译器“相信我， 我知道自己在干什么”。类型断言好比其他语言里的类型转换，但是不进行特殊的数据检查和解构。它没有运行时的影响，只是在编译阶段起作用。

类型断言两种形式

- 尖括号

  ```typescript
  let someValue: any = "this is a string";
  
  let strLength: number = (<string>someValue).length;
  ```

  

- `as`语法

  ```typescript
  let someValue: any = "this is a string";
  
  let strLength: number = (someValue as string).length;
  ```

  

#### 关于`let`

尽可能地使用`let` 来代替`var`

