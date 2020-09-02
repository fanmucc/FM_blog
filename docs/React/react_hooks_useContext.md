#### useContext 与 createContext

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

[更多Context使用方法](https://zh-hans.reactjs.org/docs/context.html)