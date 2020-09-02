#### useRef

``` js
const refContainer = useRef(initialValue)
```

`useRef` 返回一个可变的 ref 对象， 其 `.current` 属性被初始化传入的参数 (`initialValue`). 返回的 ref 对象在组件的整个生命周期内保持不变

返回 ref 对象
``` js
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    // `current` 指向已挂载到 DOM 上的文本输入元素
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

使用 useRef 进行数据缓存
``` js
import React, { useState, useEffect, useRef } from 'react'

function App () {
    const [text, setText] = useState('useRef缓存数据')
    const inputEl = useRef(null)
    const textRef = useRef()
    const onButtonClick = () => {
        // `current` 指向已挂载到 DOM 上的文本输入元素
        inputEl.current.focus();
        inputEl.current.value="123"
        console.log(inputEl)
    };

    useEffect(() => {
        textRef.current = text
        console.log(textRef)
    }, [text]) // 监听text的变化然后进行更新textRef

    return (
        <>
            <input ref={inputEl} type="text" />
            <button onClick={onButtonClick}>Focus the input</button>
            <input value={text} onChange={(e) => {setText(e.target.value)}}/>
        </>
    )
}

export default App
```