## useEffect
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

