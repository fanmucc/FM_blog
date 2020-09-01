#### React Hooks

[Hooks官方文档](https://zh-hans.reactjs.org/docs/hooks-reference.html)

> `Hooks`是`React 16.8`的新增特性，它可以让你在不编写`class`的情况下使用`state`以及其他的`React`特性

### Hooks Api

``` js
import React, { useState,       // 基础Hooks API
                useEffect,      // 基础Hooks API
                useContext,     // 基础Hooks API
                createContext,
                useReducer,
                useRef,
                useMemo,
                useRef,
                useImperativeHandle,
                useLayoutEffect,
                useDebugValue} from 'react'
```

### `useState`

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

### `useEffect`
``` js
useEffect(didUpdate)
// 该Hook接收一个包含命令式、且可能有副作用代码的函数
```

``` js
import React, { useState, useEffect } from 'react'
function App(){
    const [items, setItems] = useState([])
    const addItem = () => {
        // setItems([...items, {id: items.length, value: (Math.random() * 100).toFixed(2)}])
        setItems(prevState => {
            console.log(prevState)
            return [...items, {id: items.length, value: (Math.random() * 100).toFixed(2)}]
        })
    }
    useEffect(() => {
        console.log(items, '===')
    })
    return (
        <div>
            <button onClick={addItem}>Add a number</button>
            <ul>
                {items.map(item => (
                <li key={item.id}>{item.value}</li>
                ))}
            </ul>
        </div>
    )
}

// 通过log， 初始化的时候只执行一个输出 [] 数组
// 当点击增加时， 会输出两次， 一个是数据更改之前的内容， 一个是数据修改之后的内容
// 既 对应componentDidMount组件加载完成后及componentDidUpdate数组更新完成后的两个生命周期钩子
```

清除 `effect`

通常组件卸载时需要清除`effect`创建的诸如订阅或计时器ID等资源，要实现这一点，`useEffect`函数需要返回一个清除函数
``` js
useEffect(() => {
    const subscription = props.source.subscribe();
    return () => {
        // 清除订阅
        subscription.unsubscribe();
    };
})
```

``` js
// 示例  在B组件上添加计时器，当切换至a组件时将其计时器删除
function App(){
    const [items, setItems] = useState(true)
    const addItem = () => {
        setItems(!items)
    }
    const A = () => {
        return <h1>我是页面A</h1>
    }
    const B = () => {
        let time = setInterval(() => {
            console.log('我一秒钟执行一次')
        }, 1000)
        useEffect(() => {
            console.log('页面B显示了')
            return () => {
                clearInterval(time)
            }
        })
        return <h1>我是页面B</h1>
    }
    return (
        <div>
            <button onClick={addItem}>页面切换</button>
            <div>
                {items === true?<A/>:<B/>}
            </div>
        </div>
    )
}
```

`useEffect`第二个参数
``` js
useEffect(()=>{
    //
},'参数')
```
参数:
- 不传
- 空数组 []
- 依赖项 [依赖项]

``` js
import React, { useState, useEffect } from 'react';
function App(){
    const [items, setItems] = useState(0)
    const [count, setCount] = useState(0)
    const addItem = () => {
        setItems(items + 1)
    }
    const addCount = () => {
        setCount(count + 1)
    }
    // 依次进行运行
    useEffect(() => {
        console.log(items)
        console.log(count)
    })
    // useEffect(() => {
    //     console.log(items)
    //     console.log(count)
    // }, [])
    // useEffect(() => {
    //     console.log(items)
    //     console.log(count)
    // }, [items])
    return (
        <div>
            <button onClick={addItem}>items增加</button>
            <button onClick={addCount}>count增加</button>
            <p>现在items的数值为:{items}</p>
            <p>现在count的数值为:{count}</p>
        </div>
    )
}
export default App;
```

1. 不传  表示每轮组件渲染完成后执行，也就是渲染一次执行一次。有点像 `componentDidUpdate`
2. 传[]数组  表示没有任何依赖性, 永远只执行一次，有点像 `componentDidMount`
3. 穿衣一个依赖数组[items]  表示依赖项发生改变，渲染后执行。 相当于给 `componentDidUpdate` 添加了执行条件

注意： 初始化时都会被调用


### `useContext 与 createContext`

``` js
const value = useContext(MyContext);
```

``` js
import React, { createContext, useContext, useState } from 'react'

function App () {
    const [list, SetList] = useState([
        'context练习',
        'react hooks学习'
    ])
    const ThemeList = createContext(list)

    function Item () {
        const item = useContext(ThemeList)
        return <div>{item}</div>
    }
    return (
        <div>
            <p>context练习</p> 
            {list.map((item, index) => {
                return (
                    <ThemeList.Provider value={item} key={index}>
                        <Item></Item>
                    </ThemeList.Provider>
                )
                
            })}  
            
        </div>
    )
}

export default App
```

