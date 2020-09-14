交叉类型
``` js
const mergeFunc = <T, U>(arg1: T, arg2: U): T & U => {
    let res = {} as T & U
    res = Object.assign(arg1, arg2)
    return res
}

mergeFunc({a: 'a'}, {b: 'b'})

// 联合烈性
type1 | type2 | type3

const getLengthFunc = (conent: string | number): number => {
    if(typeof conent === 'string') {return conent.length}
    else return conent.toString().length
}

// 类型保护
const valueList = [123, 'abc']
const getRandomValue = () => {
    const number = Math.rendom() * 10
    if (number < 5) return valueList[0]
    else return valueList[1]
}
let item = getRandomValue()
function isString(value: number | string): value is string {
    return typeof value === 'sting'
}

if(isString(item)) {    // 或者 if(typeof item === 'string')   typeof 只能判断 string number boolean symbol
    console.log(item.length)
} else {
    console.log(item.length)
}

// instanceof 类型保护

// null undefined


// 类型别名
type TypeString = string
let str: TypeString
type PositionType<T> = {x: T, y: T}
const postion1: PositionType<number> {
    x: 1,
    y: 2
}
const postion1: PositionType<string> {
    x: '1',
    y: '2'
}


```