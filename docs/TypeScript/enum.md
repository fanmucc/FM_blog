#### 数字枚举

```ts
enum Status {
    Uploading,
    Success,
    Failed
}
console.log(Status.Uploading)   // 0
```
##### 反向映射
```ts
console.log(Status[0])      // 输出 ‘Uploading’
```

##### 内容赋值
```ts
enum Status {
    Uploading = 'loading',
    Success = 'true',
    Failed = Uploading
}
console.log(Status.Failed)      // 'loading'
```

#### 异构枚举
```ts
enum Result {
    Faild = 0,
    Success = 'Success'
}
```

#### 枚举类型使用
> 枚举作为类型来使用，需要满足一下情况之一，枚举中的所有属性都需满足

- `enum E {A}`              没有赋值
- `enum E {A = 'a'}`        字符串 
- `enum E {A = 1 || -1}`    正数或者负数

##### 枚举成员类型
```ts
enum Animals {
    Dog = 1,
    Cat = 2
}
interface Dog {
    type: Animals.Dog
}
const dog: Dog = {
    type: Animals.Dog
    //   type: Animals.Cat   报错
}
```

#### 联合类型
```ts
enum Status {
    Off,
    On
}
interface Light {
    status: Status
}
const ligth: Light = {status: Status.Off}
const ligth: Light = {status: Status.On}
```

#### 通过常量来设置
```ts
const enum Animals {
    Dog = 1
}
const dog = Animals.Dog
console.log(dog)        // 1
```