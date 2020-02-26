#### 静态资源内联

> `raw-loader`  

资源内联的意义
- 代码层面
    1. 页面框架的初始化脚本
    2. 上报相关打点
    3. css内联避免相关页面闪屏
- 请求层面 减少 `HTTP` 的请求次数

##### HTML 内联
在需要内联的模板中进入
`${require('raw-loader!需要引入的html文件路径')}`

#### JS 内联
在需要内联的模板中进入
`<script>${require('raw-loader!babel-loader!../node_modules/lib-flexibel')}</script>`

#### CSS 内联

- `style-loader`
- `html-inline-css-webpack-plugin`

`style-loader`
``` js
module.exports = {
    module: {
        rules: [
            text: /.css/,
            {
                loader: 'style-loader',
                options: {
                    insertAt: 'top'.    // 将样式插入到<head>
                    singleton: true,    // 将所有的style变迁合并成一个
                }
            }
        ]
    }
}
```

之前的示例都是讲`css`打包成文件，那就看看如何处理打包后的`css`

安装 `html-inline-css-webpack-plugin`

```

```
