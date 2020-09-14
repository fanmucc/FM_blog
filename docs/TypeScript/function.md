### 函数类型
> 设置接口参数类型

#### 基本使用
```ts
let add: (x: number, y: number) => number;
add = (x: number, y: number): number => x + y
```

#### 上章接口类型写法
```ts
// interface Add {
//    (x: number, y: number): number;    
// }  // 等于下面
type Add = (x: number, y: number) => number;
let add: Add;
add = (x: number, y: number) => x + y;
```

#### 函数可选参数
> 必须写到必选参数的后面

```ts
type Add = (x: number, y: number, z?: number) => number;
let add: Add;
add = (x: number, y: number) => x + y;
//
add = (x:number, y: number, z: number) => x + y + z;
```

#### 默认参数
> 可以设置默认值

```ts
type Add = (x: number, y: number, z?: number) => number;
let add: Add;
add = (x: number, y: number, z: number = 3) => x + y + z;
console.log(add(1,2))
console.log(add(1,2,5))
```

#### 拆解操作符
> ... 为es6语法，可自行搜索

```ts
// 接受第一个参数，第二个参数为数组，进行...操作符拆解
const handleData = (x: number, ...y: number[]) => {
    //
}
```

#### 函数重载
!> 函数重载只能使用function 定义；不能使用接口或者类型类名进行设置

```ts
function handleDate(x: string): string[];           // 函数重载
function handleDate(x: number): number[];           // 函数重载
function handleDate(x: any): any {                  // 函数实体，不是重载的一部分；
    if (typeof x === 'string') {
        return x.split('')
    } else {
        return x.toString().split('').map((item) => Number(item));
    }
}
let func = handleDate 
func(a:number)
```