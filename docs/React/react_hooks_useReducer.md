#### useReducer

>! 往下都是 React Hooks 提供的额外API

``` js
const [state, dispatch] = useReducer(reducer, initialArg, init)
```

useState 的代替方案。 接收一个`(state, action) => newState`的 reducer， 并返回当前的 state 以及其配套使用的 dispatch 方法

在某些场景下， useReducer 会比 useState 更适用。

``` js
import React, { useReducer } from 'react'

const initaialState = {count: 0}
function reducer(state, action) {
    switch (action.type) {
        case 'increment':
            return {count: state.count + 1}
        case 'decrement':
            return {count: state.count - 1}
        default: 
            throw new Error();
    }
}
function App () {
    // const [state, dispatch] = useReducer(reducer, initaialState)  // 参数传递
    const [state, dispatch] = useReducer(reducer, {count: 0})   // 参数传递
    return (
        <>
            Count: {state.count}
            <button onClick={() => dispatch({type: 'decrement'})}>-</button>
            <button onClick={() => dispatch({type: 'increment'})}>+</button>
        </>
    )
}
```

##### 惰性初始化

可以选择惰性的创建初始state。为此，需要将 init 函数作为 useReducer 的第三个参数传入，这样初始 seate 将被设置为 init(initialArg)

这样做可以将用于计算 state 的逻辑提取到 reducer 外部， 这也将来对重置 state 的 action 做处理提供了遍历

``` js
import React, { useReducer } from 'react'

function init(initialCount) {
    return {count: initialCount}
}

function reducer(state, action) {
    switch (action.type) {
        case 'increment':
            return {count: state.count + 1};
        case 'decrement':
            return {count: state.count - 1};
        case 'reset':
            return init(action.payload);
        default:
            throw new Error();
    }
}

function Counter({initialCount}) {
    const [state, dispatch] = useReducer(reducer, initialCount, init)
    return (
        <>
            Count: {state.count}
            <button
                onClick={() => dispatch({type: 'reset', payload: 0})}>       {*// 将initialCount 改为0看看效果 *}
                Reset
            </button>
            <button onClick={() => dispatch({type: 'decrement'})}>-</button>
            <button onClick={() => dispatch({type: 'increment'})}>+</button>
        </>
    )
}
```

*注意* 当使用 `init` 时， 在函数调用时应传入 解构赋值 `{initialCount}`