#### 布尔类型

```
let bool: b = true;
bool = false;
bool = 1; // 报错
```

#### number 类型

```
let num: number = 1;
num = 2.32;
num = 0b1011; // 二进制
num = 0xa2f; // 十六进制
num = 0o275; // 八进制
```
#### string 类型

```
let str: string = 'hello';
```
#### 数组类型

```
let arr1: number[] = [1, 2, 3];
let arr2: Array<string> = ['a', 'b', 'c'];
```
#### 元组类型
> 元组是代表已知数组成员的个数和类型。
```
let tup1: [number, string] = [1, 'a'];
```
#### 枚举类型
> 枚举是一个可被命名的整形常数的集合

```
enum Color {red, green, blue};
let color: Color = Color.red;
console.log(color); // 输出：0

enum Week {Monday=1, Quesday, Wednesday=7, Thursday};
let today: Week = Week.Quesday;
console.log(today); // 输出2
today = Week.Thursday;
console.log(today); // 输出8
```
#### null 和 undefine 类型
> 默认情况下，这两种类型都可以赋值给其他类型。但是如果开启了严格空校验时，这两种类型只能赋值给本身对应的类型或者 void 类型。

```
let boy: number | undefine;
a = 1;
a = undefine;
a = null; // 错误
```
#### any 类型
> any 为任意类型，可随意赋值

#### void 类型
> void 表示为没有任何类型，一般用于函数没有返回值的情况

#### never 类型
> 代表从不会出现的类型

#### 函数类型

```
// 函数声明法
function fn(a: number, b: number): number {
    return a + b;
};

function fnTwo(): void {
}

// 可选参数的函数, b 是可选参数，在其后面加个?
function fnThree(a: number, b?: str){
}

// 拥有默认参数的函数
function fn (a: number, b: number = 20): number {
    return a + b;
}

// 函数表达式法
var b = function (a: number, b: number): number {
    return a + b;
}

// 剩余参数函数
function fn (a: number, ...b: number[]): number {
    return a;
}
```