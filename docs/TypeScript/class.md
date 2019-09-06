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
> # 井号来标记为私有属性

```js
class point {
    # a = 12;
}
// 遗憾的是es6中并未推出，但是tsclass类中可以设置
```

### class 进阶篇