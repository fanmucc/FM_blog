## 类型推论
 
``` js
let name = 'fanmu'
name = 123  // error


let arr = [1, 'a']  => arr: Array<number | string> = [1, 'a']


// 上下文类型

// 类型兼容性
interface Info {
    name: string
}
let infos: Info
const infos1 = {name: 'fanmu'}
const infos2 = {age: 18}
const infos3 = {name: 'fanmu', age: 18}
infos = infos1
infos = infos2   // 报错
infos = infos3   // 不报错 可以多但是必须包含响应的参数 检测是深拷贝递归检测

如
interface Info {
    name: string,
    info: {age: number}
}
此时 infos1 = {name: 'fanmu', info: {}}  // 还是会报错 必须为 info:{age: 18}

// 函数兼容性
// 参数个数
let x = (a: number) => 0
let y = (a: number, c: string) => 0
x = y // 正确
y = x // 错误   y中有x中没有的参数，只能多赋少

// 参数类型
let x = (a: number) => 0
let y = (c: string) => 0
x = y // 错误 参数类型不一致

// 可选参数和剩余参数
const getSum = (arr: number[], callback(...args: number[]) => number): number => {
    return callback(...arr)
}
getSum([1,2], (...args: number[]): number => args.reduce((a,b) => a + b, 0))

// 函数参数双向协变
let funcA = (arg: number | string): void => {}
let funcB = (arg: number): void => {}
funcA = funcB  // 正确
funcB = funcA  // 正确


// 返回值类型
let x = (): stirng | number => 0
let y = (): stirng => 'a'


// 类  会对实例进行检测  私有属性和受保护属性影响
class AnimaClass {
    public static age: number               // 有
    constructor(public name: string) {}
}
class PeopleClass {
    public static age: number               // 有 相同 所以animal = people 不报错
    constructor(public name: string) {}
}
class FoodClass {
    constructor(public name: string) {}     // 无 报错
}

let animal: AnimaClass
let people: PeopleClass
let food: FoodClass
animal = people
animal = food
```