#### 自定义Hooks

我们想在两个函数之间共享逻辑时，我们会把它提取到第三个函数中。而组件和 Hook 都是函数，所以也同样适用这种方式。

自定义 Hook 是一个函数，其名称以 “use” 开头，函数内部可以调用其他的 Hook。 例如，`useSize`

这里通过自定义 Hook 来获取浏览器窗口的大小

``` js
import React, { useState, useEffect } from 'react'

function useSize () {
    const [state, setState] = useState({
        width: document.documentElement.clientWidth,
        height: document.documentElement.clientHeight
    })

    const onResize = useCallback(() => {
        setState({
            width: document.documentElement.clientWidth,
            height: document.documentElement.clientHeight
        })
    }, [])

    useEffect(() => {
        window.addEventListener('resize', onResize)
        return () => {
            window.removeEventListener('resize', onResize)
        }
    }, [])

    return size;
}
```