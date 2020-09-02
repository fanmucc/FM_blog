## useState

``` js 
// initialState 传入的参数
const [conut, setCount] = useState(initialState) 
```
返回一个`state`, 以及更新的`state`的函数

在初始渲染期间，返回的状态(`state`)与传入的第一个参数(`initialState`)值相同（请注意，只有初始化时state才是自己传入的值，每一次修改时传入的state都是最新的)

`setState`函数用于更新`state`.它接收一个新的`state`值并将组件的一次重新渲染加入队列
``` js
setState(newState)
```
在后续的重新渲染中，`useState`返回地一个值将始终是更新后最新的`state`

对于 hooks，state 不必是对象，它可以是你想要的任何类型-数组、数字、布尔值、字符串等等。每次调用useState都会创建一个state块，其中包含一个值。

``` js
// 示例
import React, { useState } from 'react'
function App () {
    const [count, setCount] = useState(0)
    const handleClickAdd = () => {
        setCount(count + 1)
    }
    return (
        <div>
            <p>count: {count.nums}</p>
            <button onClick={handleClickAdd}>增加</button>
        </div>
    )
}
```

值得注意的是，可以在一个函数中声明多个 `useState`, 但是不能够在判断语句中声明，React是根据useState出现的顺序来进行确认的

``` js
import React, { useState } from 'react'
let showSex = true
function App(){
    const [ age , setAge ] = useState(18)
    if(showSex){
        const [ sex , setSex ] = useState('男')
        showSex=false
    }

    const [ work , setWork ] = useState('前端程序员')
    return (
        <div>
            <p>JSPang 今年:{age}岁</p>
            <p>性别:{sex}</p>
            <p>工作是:{work}</p>
        </div>
    )
}

// error: React Hook "useState" is called conditionally. React Hooks must be called in the exact same order in every component render  react-hooks/rules-of-hooks  就会提示需要按照顺序进行调用
```
[更多useState应用示例](https://juejin.im/post/6844903920515416077)

!> 注意 与 class 组件中的 setState 方法不同，useState 不会自动合并更新对象。你可以用函数式的 setState 结合展开运算符来达到合并更新对象的效果。
``` js
setState(prevState => {
  // 也可以使用 Object.assign
  return {...prevState, ...updatedValues};
});
```
useReducer 是另一种可选方案，它更适合用于管理包含多个子值的 state 对象。
