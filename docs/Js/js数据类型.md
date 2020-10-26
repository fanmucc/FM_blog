#### javaScript基础数据类型

##### 概述
在讲数据类型之前，先讲一下变量。 `JavaScript` 的变量是松散型的，既可以保存任何数据类型的数据，在JavaScript中我们使用`var`关键字来声明一个变量(ES6中新增`let`、`const`来声明变量)

``` js
var message1 = 10;
var message2 = true;
var message3 = "hellow world";
```

因为松散型，也可以改变同一变量值的类型，虽然不推荐这么做，但是在JavaScript中完全有效

``` js
var message = 10;
message = true;  // 重新给变量message赋不同类型的值，不推荐这么做
```

而我们所有数据类型的值都是保存在自定义的某一个变量中。 `JavaScript`一共有7中数据类型，其中有6中基本数据类型，1中引用数据类型；

6中基础数据类型分别是:
- `Undefined`
- `Null`
- `Number`
- `String`
- `Boolean`
- `Symbol(ES6新增)`

1种引用数据类型

- `Object`

新增基本数据类型`BigInt`

### 1、Undefined类型
`Undefined`类型只有一个值，既特殊的`undefined`，一个变量在声明后为初始化时， 这个变量的值就是`undefined`

``` js
var message;
console.log(message)  // undefined
```

需要注意的是声明了但未初始化的变量与未声明的变量是不一样的
``` js
var message;
// var a
console.log(message)  // undefined
console.log(a)  // 报错 a is not defined
``` 

但是使用 `typeof` 操作符来检测上面两个变量时，都会返回 undefined
``` js
var msg;
// var a;
console.log(typeof msg)  // undefined
console.log(typeof a)   // undefined
```

这个结果又其逻辑上的合理性。因为虽然这两种变量从技术角度上看有本质的区别，但实际上无论对那种变量也不可能执行真正的操作

> 未初始化的变量会自动被赋予undefined值，没有必要将变量显示的设置为 undefined ,但显示的初始化变量依然是明智的选择。如果能够做到这一点，那么当 typeof 操作符返回 undefined 值时，我们就知道被检测的变量还没有被声明，而不是未初始化

### 2、Null
`Null`类型是第二个只有一个值的数据类型，这个特殊的值是`null`。`null`值表示一个空对象指针，使用`typeof`操作符检测时返回`"object"`
``` js
var obj = null;
console.log(typeof obj)  // object
```

虽然`typeof null`会输出`object`，但这是 js 存在的一个悠久的 Bug。在js的最初版本中使用的是32位系统，为了性能考虑使用低位储存变量的类型信息， 000开头代表是对象，然而`null`表示为全零，所以将它错误的判断为`object`。`null`值的主要作用是如果定义的变量在将来用于保存对象，那么最好将该变量初始化为`null`值。

### 3、Boolean

`Boolean`类型是`JavaScript`中使用最多的一种基本数据类型，只有两个值`true`、`false`。

``` js
var a = true;
var b = false;
```

虽然`Boolean`类型只有两个值，但`JavaScript`中所有类型的值都有与这两个`Boolean`值等价的值，可以调用转型函数`Boolean()`将其他类型的值转化为`Boolean`值

``` js
var msg = "hello world"
var msgBoolean = Boolean(msg)
```

根据转换值的数据类型及实际值，返回一个`Boolean`值。各种数据类型及其对应的转换规则如下:

|数据类型|转为true|转为false|
|---|---|---|
|Boolean|true|false|
|String|任何非空字符串|" "（空字符串）|
|Number|任何非零数字（包括无穷大）|0和NaN|
|Object|任何对象|null|
|Undefined|not applicable（不适用）|undefined|

### 4、Number
`Number`类型算是`Js`中最复杂也最令人关注的基本数据类型了，Number可以同时表示整数和浮点数，同时也支持各种进制和科学计数法。
``` js
var intNum = 10; // 整数
var floatNum1 = 1.1;  // 浮点数
var floatNum2 = 0.1;  // 浮点数
var floatNumb3 = .1;  // 浮点数， 但不推荐此写法

// 科学计数法
var floatNum = 2.125e7;  // 3.125 * 10 的7次方

// 八进制(以0开头)， 数字序列0~7
var octalNum1 = 070;  // 八进制的56
var octalNum2 = 079;  // 无效的八进制数值--解析为 78
var octalNum3 = 08;  // 无效的八进制数值-- 解析为 8

// 十六进制(以0x开头)，数字序列0~9以及A~F不区分大小写
var hexMum1 = 0xA  // 十六进制 10
var hexNum2 = 0x1f  // 十六进制 31
```

`JavaScript`能够表示的最小数值保存在 `Number.MIN_VALUE` 中——在大多数浏览器中，这个值是 5e-324；能够表示的最大数值保存在`Number.MAX_VALUE` 中——在大多数浏览器中，这个值是 1.7976931348623157e+308。如果某次计算的结果得到了一个超出 JavaScript 数值范围的值，那么这个数值将被自动转换成特殊的 Infinity 值(有正负)。
这里要特别说明一下，浮点数值的最高精度是 17 位小数，但在进行算术计算时其精确度远远不如整数。例如，0.1 + 0.2的结果不是 0.3，而是 0.30000000000000004。这是因为0.1和0.2在转换成二进制后会无限循环，由于标准位数的限制后面多余的位数会被截掉，此时就已经出现了精度的损失，相加后因浮点数小数位的限制而截断的二进制数字在转换为十进制就会变成0000000000000004。所以上面提到的BigInt就应运而生。

#### NaN
`NaN (not a Number)`，既非数值，用于表示一个本来要返回数值的操作数未返回数值的情况。

`NaN` 有两个非同寻常的特点:
1. 任何涉及 `NaN` 的操作(例如 NaN/10)都会返回 `NaN`
2. `NaN` 与其他值都不相等，包括 `NaN` 本身

针对这两个特点， js定义了 `isNaN()` 函数， 这个函数接收一个参数，该参数可以是任何类型。 `isNan()`在接收一个之后，会尝试将这个值转换为数值，而任何不能转换为数值的值都会导致函数返回`true`

``` js
console.log(isNaN(NaN))  // true
console.log(isNaN(10))  // false 
console.log(isNaN("10"))  // false
console.log(isNaN("blue"))  // true 不能转换成数值
console.log(isNaN(true))  // false
```

#### 数值转换
js 提供3个函数可以把非数值转换为数值

- Number() 可以用于任何类型
- parseInt() 和 parseFloat() 专门用于把字符串转换为数值

Number()函数的转换规则很多，这里直接引用红宝书里的描述：
- 如果是 Boolean 值，true 和 false 将分别被转换为 1 和 0。
- 如果是数字值，只是简单的传入和返回。
- 如果是 null 值，返回 0。如果是 undefined，返回 NaN。
- 如果是字符串，遵循下列规则：
      a、中只包含数字（包括前面带正号或负号的情况），则将其转换为十进制数值，即"1" 会变成 1，"123"会变成 123，而"011"会变成 11（注意：前导的零被忽略了）；
      b、串中包含有效的浮点格式，如"1.1"，则将其转换为对应的浮点数值（同样，也会忽 略前导零）；
      c、字符串中包含有效的十六进制格式，例如"0xf"，则将其转换为相同大小的十进制整 数值；
      d、字符串是空的（不包含任何字符），则将其转换为 0；  如果字符串中包含除上述格式之外的字符，则将其转换为 NaN。
- 如果是对象，则调用对象的 valueOf()方法，然后依照前面的规则转换返回的值。如果转换 的结果是 NaN，则调用对象的
- toString()方法，然后再次依照前面的规则转换返回的字符 串值。

``` js
var num1 = Number("hello")  // NaN
var num2 = Number("") // 0
var num3 = Number("0001")  // 1
var num4 = Number(true) // 1
```

`parseInt()`函数在转换字符串时，更多的是看其是否符合数值模式。它会忽略字符串前面的空格，直至找到第一个非空格字符串。如果第一个字符串不是数字字符或者符号， `parseInt()` 就会返回`NaN`；也就是说，用`parseInt()`转换空字符串会返回`NaN`(`Number()`对空字符返回0)。如果第一个字符是数字字符， `parseInt()`会继续向下解析，知道解析完成所有后组字符或者遇到一个非数字字符.

``` js
var num1 = parseInt("1234blue"); // 1234 
var num2 = parseInt(""); // NaN 
var num3 = parseInt("0xA"); // 10（十六进制数）
var num4 = parseInt(22.5); // 22 
var num5 = parseInt("070"); // 56（八进制数）
var num6 = parseInt("70"); // 70（十进制数）
var num7 = parseInt("0xf"); // 15（十六进制数）
```

`parseInt()`可以传入第二个参数，来确认需要转换数据的进制类型
``` js
var num1 = parseInt("10", 2); //2 （按二进制解析）
var num2 = parseInt("10", 8); //8 （按八进制解析）
var num3 = parseInt("10", 10); //10 （按十进制解析）
var num4 = parseInt("10", 16); //16 （按十六进制解析）
```

`parseFloat()` 与 `parseInt()` 函数类似，`parseFloat()` 也是从第一个字符开始解析每个字符。而且也是一直解析到字符串末尾，或者解析到遇到一个无效浮点数字字符为止
``` js
var num1 = parseFloat("1234blue"); //1234 （整数）
var num2 = parseFloat("0xA"); //0 
var num3 = parseFloat("22.5"); //22.5 
var num4 = parseFloat("22.34.5"); //22.34 第二个小数点无效
var num5 = parseFloat("0908.5"); //908.5 
var num6 = parseFloat("3.125e7"); //31250000
```

### 5、String
`String` 既字符串， 由一对双引号或者单引号表示
``` js
var str1 = 'hello'
var str2 = "world"
```

JS 中字符串是不可变的，也就是说，字符串一旦创建，他们的值就不能改变。要改变某个变量保存的字符串，首先要销毁原来的字符串，然后再用另一个包含新值的字符串填充该变量.
``` js
var str = 'hello'
str = str + ' world'
console.log(str) // 'hello world'
```

实际开发中经常为方便存储，经常需要将值转化为字符串。要把一个值转换为字符串有两种方式
`toString()` 除了`null`和`undefined`值没有`toString()`方法，其他值都有这个方法，该方法返回字符串的一个模本。

``` js
var age = 11; 
var ageAsString = age.toString(); // 字符串"11" 
var found = true; 
var foundAsString = found.toString(); // 字符串"true"
```

`toString()` 可以传入一个参数: 输出数值的技术。可以输入以二进制、八进制、十六进制、乃至其他任意有效进制格式表示的字符串值。
``` js
var num = 10; 
alert(num.toString()); // "10" 
alert(num.toString(2)); // "1010" 
alert(num.toString(8)); // "12" 
alert(num.toString(10)); // "10" 
alert(num.toString(16)); // "a"
```

使用+" " 既可以通过要转换的值 + 空字符串(" "), 也可以实现转换；
``` js
var num = 10;
var numAsString = num + " ";// "10"
var boolean = true;
var booleanAsString = boolean + " ";// "true"

var a ;
var b = a + " ";// "undefined "

var c = null;
var d = c + " ";// "null "

var o = {
   valueOf: function() {
           return -1;
                }
} 
 var m = o + " ";// "-1 "

```

### 6、Symbol

###### 引用数据类型-Object类型