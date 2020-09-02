#### useMemo

``` js
const memoizedValue = useMemo(() => computeExpensiveValue(a,b), [a,b])
```

返回一个 `memoized` 值

把“创建”函数和依赖项数组作为参数传入 useMemo，它仅会在某个依赖项改变时才重新计算 memoized 值。这种优化有助于避免在每次渲染时都进行高开销的计算。

记住，传入 useMemo 的函数会在渲染期间执行。请不要在这个函数内部执行与渲染无关的操作，诸如副作用这类的操作属于 useEffect 的适用范畴，而不是 useMemo。

如果没有提供依赖项数组，useMemo 在每次渲染时都会计算新的值。

``` js
import React, { useState, useMemo } from 'react';

function ChildComponent({name,children}){   // 此时的children为 调用ChildComponent组件显示的内容
    function changeXiaohong(name){
        console.log(`${name}她来了，她来了。小红向我们走来了`)
        return name+',小红向我们走来了'
    }
    const actionXiaohong = useMemo(()=>changeXiaohong(name),[name]) 
    return (
        <>
            <div>{actionXiaohong}</div>
            <div>{children}</div>
        </>
    )
}

function App () {
    const [xiaohong, setXiaohong] = useState('小红')
    const [xiaolv, setXiaolv] = useState('小绿')
    return (
        <>
            <button onClick={()=>{setXiaohong(new Date().getTime())}}>小红</button>
            <button onClick={()=>{setXiaolv(new Date().getTime()+',小绿向我们走来了')}}>志玲</button>
            <ChildComponent name={xiaohong}>{xiaolv}</ChildComponent>
        </>
    )
}

export default App
```

