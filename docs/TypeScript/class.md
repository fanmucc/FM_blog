### class类型
- 简单复习class基础
- 学习ts class类型

### es5构造函数 以及 es6 class

```js
// es5构造函数
function point(x,y) {
    this.x = x;
    this.y = y;
}
point.prototype.getPostion = function() {
    return '这是x'+this.x+'这是y'+this.y;
}

var p1 = new point(1,2)
p1.getPostion()   // 这是x1这是y2

// es6 class
class point {
    constructor(x,y) {
        this.x = x;
        this.y = y;
    }
    getPostion () {
        return `这是x${this.x}这是y${this.y}`
    }
}
const p1 = new point(1,2)
p1.getPostion()  // 这是x1这是y2
// constructor 必有，不进行设置，则默认设置
```

### 取值函数，存值函数
> get set

```js
// es5 get set
var info = {
    _age: 18,
    set age(newValue) {             // 存值
        if (newValue > 18) {
            console.log('我真的这么大了吗')
        } else {
            console.log('我说我没这么大嘛')
        }
    },
    get age() {                     // 取值
        return this._age;
    }
}
info.age        // 读值  输出18
info.age = 18   // 存值， 存的值为newValue 根据判断输出 我真的这么大了吗;

// es6  get set
class Info {
    constructor(age) {
        this._age = age;
    }
    set age(newValue) {
        if (newValue > 18) {
            console.log('我真的这么大了吗')
        } else {
            console.log('我说我没这么大嘛')
        }
    }
    get age() {
        return this._age;
    }
}
const info = new Info(18);
info.age        // 输出 18
info.age = 18   // 输出 我真的这么大了吗;
```

### 表达式

```js
// es5 表达式
const func = function () {}
function func () {}

// es6表达式
class func () {constructor() {}}
const func = class {constructor() {}}
```

### 静态方法
> 静态方法，写在class里面的方法，不都是可以被创建的实例进行继承使用的


```js
// 关键字 static

class info {
    constructor(x,y) {
        this.x = x;
        this.y = y;
    }
    static getName() {
        return info.name;
    }
}
const p1 = new info(1,2)
p1.getName()    // 错误
info.getName()  // 输出  Info

```

### 静态属性
> es6中有静态方法没有静态属性   有偏门方法

```js
class point {
    constructor(x,y) {
        this.x = x;
        this.y = y;
    }
}
pint.z = 2;
const p = new ppint(1,2)
p.z   // 错误
point.z  // 输出 2
```

### 私有方法
> 偏门技巧

```js
// 方法1
class point {
    constructor () {

    }
    func1 () {
        
    }
    _func2 () {
        // 通过下划线进行特殊提示，但是意义不大
    }
}

// 方法2 将私有方法移出模块
const _func2 = () => {}
const poin {
    constructor() {

    }
    func1 () {
        _func2.call(this)
    }
}

// 方法3 通过es6 的sybmol 基础属性
// 暂定

```

### 私有属性
> 井号来标记为私有属性

```js
class point {
    # a = 12;
}
// 遗憾的是es6中并未推出，但是tsclass类中可以设置
```

### class 进阶篇
- 继承
### 继承
> es5继承  es6继承 super()函数

```js
// es5
function Food () {
    this.type = 'food'
}
Food.prototype.getType = function() {
    return this.type;
}

function vegetTables(name) {
    this.name = nanme;
}
vegetTables.prototype = new Food();
const tomato = new vegetTables('fanmu');
tomato.getType()    // food;

// es6
class Food {
    constructor(name) {
        this.type = name
    }
    getType () {
        return this.type;
    }
}
class vegetTables extends Food {
    constructor(name, age) {
        super(name);
        this.age = age;
    }
}
const c = new vegetTables('fanmu', 18)
c.getType()            // fanmu

// 通过Object.getPrototypeOf(vegetTables) === Food;可以判断类的父类
Object.getPrototypeOf(vegetTables) === Food;  // true;
```

### super()函数/对象
> - 函数: 子类中必须调用super()，只能在子类的constructor()中使用，其this指向子类的实例，继承父类的constructor()函数
- 对象: super() 作为对象； 普通方法中指向的是父类的原型对象； 静态方法中指向的是父类；

```js
// super()函数
class parent {
    constructor() {
        this.type = 'parent';
    }
    getName() {
        return this.type;
    }
}

parent.getType = () => {return 'is parent'};

class child extends parent {
    constructor() {
        super()
        console.log(super.getName())
    }
    static getParentName() {
        console.log(super.getType())
    }
}
const c = new child()   // 输出parent， 说明super.getName()作为普通方法，指向的是父类的原型对象
c.getParentName() // 无法拿到，报错 c.getParentName is not a function
child.getParentName()  // 输出 is parent; 静态方法，指向的是父类
```
- super 要么做方法，要么做对象

### prototype 和 __proto__
- 子类的__proto__指向父类本省；
- 子类的prototype属性上的__proto__指向父类的prototype属性
- 实例的__proto__属性的__proto__指向父类实例的__proto__

### 原生构造函数的继承
- Boolean    // es5不可继承，而生可以
- Number
- String
- Array
- Date
- function
- RegExp
- Error
- Object

```js
// 示例

class cus extends Array {
    constructor(...args) {
        super(...args)
    }
}
const arr = new cus(3)      // 指创建一个长度为三的数组
// cus(3) [empty × 3]
//      length: 3
//      __proto__: Array

arr.fill(1)         // fill 填充属性，将内容填充值arr中 arr = 【1,1,1】
```
[fill使用方法](https://www.runoob.com/jsref/jsref-fill.html)

### ts中的class类型

- public 公共的
- private 私有属性
- protected 受保护的，修饰符可以在继承的子类中访问；

示例
```ts
class Point {
    public x: number;
    public y: number;
    consrtuctor(x: number, y: number) {
        this.x = x;
        this.u = y;
    }
    public getPostion() {
        return `我是x值为${this.x}, y值为${this.y}`
    }
}
const p1 = new Point(1,5);
p1()
// 当我们不进行定义方法或者变量是不是公共或者私有，ts会默认帮我们进行设置public
```

### private 私有属性
> 只能通过类本身进行使用，继承也不可以访问

```ts
class Parent {
    private age: number;
    constructor(age: number) {
        this.age = age
    }
}
const p = new Parent(18)
p.age   // 错误
Parent.age   // 18
```

### readonly 
> 设置只读属性

```ts
class userInfo {
    readonly name: string;
    constructor(name: string) {
        this.name = name;
    }
}
const p = new userInfo('fanmu');
p.name   // fanmu
p.name = 'a'   // 报错；
```
