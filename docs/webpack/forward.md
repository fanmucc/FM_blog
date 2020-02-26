#### 自动补全css3前辍

> `postcss-loader`  `autoprefixer` `browserslist`

在前端开发中，需要兼容各种浏览器，使用css时应当注意css属性是否在其他一些浏览器中不兼容，但是记忆又是一个很耗时间的工程

[can i use](https://caniuse.com/) 可以查看css属性在各个浏览器的兼容情况

``` js
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
module.exports = {
    module: {
        rules: [
            {
                test: /.css$/,
                use: [
                    MiniCssExtractPlugin.loader,        // 将css分离出文件
                    "css-loader",
                    {
                        loader: "postcss-loader",
                        options: {                      // loader参数配置
                            plugins: [
                                require('autoprefixer')
                            ]
                        }
                    }
                ]
            }
        ]
    },
    plugins: [
        new MiniCssExtractPlugin({
            filename: '[name]_[contenthash:8].css'
        })
    ]
}
```
同时安装 `npm i browserslist -D`

在文件根目录下创建`.browserslistrc`文件
```
# .browserslistrc  文件备注以#开始  在这里设置我们需要补全的设置，如补全ios 7 ，或者浏览器使用率在 2%以上的前辍
last 3 version          # 最近3个版本的信息
> 1%                    # 用户大于1%
ios 7                   # ios 7 

```

详情 [browserslist](https://www.npmjs.com/package/browserslist)