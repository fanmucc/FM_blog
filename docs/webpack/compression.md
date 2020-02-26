#### 代码压缩

代码压缩主要分为3块
- js
- html
- css

##### js压缩
`webpack` 自带 `uglifyjs-webpack-plugin` 当将mode模式设置为 `production` 生产模式时，`js` 代码会自动进行压缩

配置`uglifyjs-webpack-plugin`
``` js
const UglifyJsPlugin = require('uglifyjs-webpack-plugin');
module.exports = {
    plugins: [
        new UglifyJsPlugin({                     // js压缩
            include: /\.js$/,                    // 文件正则匹配
            parallel: true,                      // 压缩代码
            uglifyOptions: {
                output: {
                    comments: false,             // js文件多线程并发
                },
            }
        }),
    ]
}
```
#### css压缩
``` js
const OptimizeCssAssetsWebpackPlugin = require('optimize-css-assets-webpack-plugin')

// 这里我们需要 cssnano包 来进行配置
module.exports = {
    plugins: [
        new OptimizeCssAssetsWebpackPlugin({     // css文件压缩
            assetNameRegExp: /\.css$/,           // 一个正则表达式，指示应优化\最小化的文件名称。提供的正则表达式是针对ExtractTextPlugin配置中实例所导出文件的文件名而不是源CSS文件的文件名运行的。默认为/\.css$/g
            cssProcessor: require('cssnano'),    // 用于优化\最小化CSS的CSS处理器，默认为cssnano。这应该是遵循cssnano.process界面的函数（接收CSS和options参数并返回Promise）
            cssProcessorPluginOptions: {},       // 传递给的选项cssProcessor，默认为{}
            canPrint: true,                      // 一个布尔值，指示插件是否可以将消息打印到控制台，默认为 true
        })
    ]
}
```

#### html文件压缩
``` js
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
    plugins: [
        new HtmlWebpackPlugin({                                     // html文件压缩
            template: path.join(__dirname, 'src/react.html'),       // 压缩模板
            filename: 'react.html',                                  // 压缩后的文件名
            chunks: ['react'],                                      // 文件对应的chunk
            inject: true,                                           // 是否压缩
            minify: {
                html5: true,            
                collapseWhitespace: true,
                preserveLineBreaks: false,
                minifyCSS: true,                                    // 压缩html文件中的内联css
                minifyJS: true,                                     // 压缩内联的js文件
                removeComments: false
            }
        })
    ]
}
```
