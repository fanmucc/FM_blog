### 接口类型
> 设置接收参数类型，严格规范操作，减少Bug

```ts
// 接口
interface Inter {
    color: string,
    num: number
}

// 使用
const InterInfo = ({color, number}: Inter) => {return `${color} + ${num}`};
```

#### 设置可有可无属性
```ts
interface Vegetable {
    color?: string,
    num: number
}

// 使用
const getVegetable = ({color, type}: Vegetable) => { return `${color ? color : ' '} + ${num}`}
```

#### 设置只读属性(只读属性不可进行修改)
```ts
interface Read {
    color: string,
    readonly type: string
}

// 使用
const readOnlys: Read = {color: 'red', type: '只读'}
readOnlys.type = '不可修改'    // 提示不可进行修改

interface Arrys {
    0: number,
    readonly 1: string
}
let arrs: Arrys = [1, '只读']
arrs[1] = '不可修改'        // 提示不可进行修改
```

#### 接口继承
```typescript
interface Vegetables {
    color: string,
}

interface Tomato {
    color: string,
    radius: number
}
interface Carrot {
    color: string,
    length: number
}

const toma: Tomato = {
    color: 'red',
    radius: 2,
}

// 上述接口中都有共同属性color: sting， 我们可以设置其继承Vegetables 的接口
interface Extend extends Vegetables{
    // color: string,
    num: number
}
```

#### 绕过多余属性检查
> js中，总会有多余属性的传入，但是最终并不会印象其最终结果

```ts
interface Vegetables {
    color: string,
    type: string
} 
const getVegettables = ({color, type}: Vegetable) => {
    return `一个 ${color} + ${type}`
}
```

1. 类型断言
```ts
getVegettables({
    color: 'red',
    type: '辣椒',
    size: 2
} as Vegetables)
```
2. 索引签名
```ts
interface Vegetable {
    color: string,          
    type: string
    [prop: sring]: any   // 可有可无属性
}
```
3. 类型兼容性
```ts
const vergetableInfo = {
    color: 'red',
    type: '苹果',
    size: 2,
}
getVegettables(vergetableInfo)
```
