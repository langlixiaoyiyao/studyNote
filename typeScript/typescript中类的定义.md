#### 类的定义

```
class Animals {
    constructor(): void {  // 构造函数，实例化的时候会被调用
        
    }
}
```
#### 类中属性的定义

```
class Animals {
    private one: string; // 私有属性只能使用类名访问，或者在类的内部使用
    public two: string; // 公共属性
    protected three: string; // 被保护的属性，本类和子类可以使用，实例对象不可以使用
}
```
#### 类中方法的定义

```
class Animals {
    private name: string;
    constructor(name: string) {
        this.name = name;
    }
    get(): string {   // 实例方法，在该方法中可以调用静态方法、私有属性
        return this.getName();
    }
    static getName(): string { // 静态方法，只能类中使用，实例不可使用，不可在其内部调用实例属性和实例方法
        return this.name;
    }
}
```
> 小小知识点：
> 静态方法和私有属性在类定义的时候就被创建了。但是实例方法和实例属性是在类被实例化之后才创建的，所以静态方法中无法使用实例属性和实例方法

#### 类的继承
> 子类会继承父类中所有非私有的属性和方法。
> 子类中如果定义了和父类一样名字的方法或属性，则父类的同名属性、同名方法将会被子类中的覆盖。

```
class Father {
    constructor() {
        
    }
}
class Children extends Father { // 子类通过extends关键字继承父类
    contructor() {
        super(); // 子类必须通过super()调用父类的构造函数
    }
}
```
#### 抽象类
> 抽象类无法被实例化，唯一的作用是能是被继承

```
abstract class Animals { // 通过 abstract 关键字定义
    abstract eat(): void; // 抽象方法：没有函数体，只有声明，子类必须实现函数体，
    
}
class Dogs extends Animals {
    eat(): void {
    }
}
```
#### 类的参数属性
> 使用类的参数属性可以省去属性的定义和赋值

```
class Animals {
    constructor(
        private name: string
    ) {
        
    }
}
// 上面的代码相当于
class Animals {
    private name: string;
    constructor(name: string) {
           this.name = name;
    }
}
```