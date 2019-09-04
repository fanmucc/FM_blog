### 基础类型

1. 布尔值
```ts
let bool: boolean = false;
    bool: boolean;
    bool = false;
```

2. 字符串
```ts
let str: string = 'a';
    str: string;
    str = 'a';
```

3. 数组型
```ts
let num: number = 1;
    num: number;
    num = 1;
```

4. 数组类型
```ts
let numArr: number[] = [1,2,3]
    numArr: number[];
    numArr = [1,2,3]
let numArrs: Array<number> = [1,2,3]
    numArrs: Array<number>
    numArrs = [1,2,3]
```

5. 元组类型
> 固定长度，固定类型

```ts
let tuple: [string, number, boolean];
    tuple = ['a', 1, true]
    if tuple = [1, 'a', true]   error // 错误，长度正确，但是类型不正确;
```

6. 枚举类型

```ts
enum Roles {
    SUPER_ADMIN,
    ADMIN,
    USER
};
console.log(Roles.SUPER_ADMIN)   === 0;
console.log(Roles.ADMIN) === 1;
console.log(Roles.USER) === 2;
console.log(Roles[0]) === 'SUPER_ADMIN';
console.log(Roles[1]) === 'ADMIN';
console.log(Roles[2]) === 'USER';

// 可以自定义对应数组
enum Roles {
    SUPER_ADMIN = 1;
    ADMIN,
    USER
};
console.log(Roles.ADMIN) === 2;
console.log(Roles.USER) === 3;
// 如果ADMIN = 3;
console.log(Roles.SUPER_ADMIN)   === 1;
console.log(Roles.USER) === 4;
```

7. any类型 
> 任意值

```ts
let value: any = 1;
    value = '123'  // === true;
    value = false  // === true;
```

8. void 
> 什么类型都不是，常用于没有返回值

```ts
conloetex => (text): void {
    console.log(text)
}
// 是指log text内容，没有return;
// 同时void可以为null 或者 undefined
let a: void;
    a = null;
    a = undefined;
```

9. null 和 undefined;
> 是其他类型的子类型，可以赋值给其他类型，其本事即时值也是类型;

```ts
let n: null = null;
let num: number = 1;
    num = null / undefined;
// undefined同理
```

10. never类型
> 不存在的类型, 死循环和抛错的返回值类型为never类型;
never是所有类型的子类型，可以赋值给其他类型，但是其他类型不能赋值给never类型

```ts
while(true): never {
    // 死循环
}
```

11. object类型
```ts
function getObject(obj: object): void {
    console.log(obj)
}
```

12. 类型断言
```ts
const getLength = (target: string | number): number => {
    // 传递的值target 是 string类型或者为number类型，返回值类型为number;
    if (<string>target).length || (target as string).length) {
        // 类型断言                   类型断言
        return ...
    } else {
        return ...
    }
}
// 推荐使用(target as string) as 类型因为在jsx文件中，<string>可能会被当作标签；
```