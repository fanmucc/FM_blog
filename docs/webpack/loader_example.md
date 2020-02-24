#### `Loader` 的简单使用

##### ES6/ES7转ES5
- [babel相关博客](https://juejin.im/post/5bfe541bf265da6179748834)
- ES6/ES7转ES5
- 安装 babel `npm i @babel/core @babel/preset-env babel-loader`
- 创建 `.babelrc`文件
- 配置需要使用到的`babel`插件

``` json
// .babelrc
{
   "presets": {
       "@babel/preset-env"
   } 
}
```
``` js
// webpack.config.js
let path = require('path');
module.exports = {
    mode: 'development',
    entry: '.src/index.js',
    output: {
        filename: 'dev.js',
        path: path.resolve(__dirname, 'dist')
    },
    module: {                               // Loader 配置 
        rules: [
            {
                test: /.js$/,               // 正则匹配以js文件结尾
                use: 'babel-loader'         // 结合.babelrc的配置文件使用babel-loader
            }
        ]
    }
}
```
##### 使用`react`的`jsx`语法
- 安装 `npm i react react-dom @babel/preset-react`
- 配置`.babelrc`文件


``` json
// .babelrc
{
   "presets": {
       "@babel/preset-env",
       "@babel/preset-react"
   } 
}

``` js
// react.js
import React from 'react';
import ReactDom from 'react-dom';
class Search extends React.Component {
    render () {
        return <div>使用react Loaderr</div>
    }
}
ReactDom.render(
    <Search/>,
    document.getElementById('root')
)
```

``` js
// webpack.config.js
let path = require('path');
module.exports = {
    mode: 'development',
    entry: '.src/react.js',
    output: {
        filename: 'dev.js',
        path: path.resolve(__dirname, 'dist')
    },
    module: {                               // Loader 配置 
        rules: [
            {
                test: /.js$/,               // 正则匹配以js文件结尾
                use: 'babel-loader'         // 结合.babelrc的配置文件使用babel-loader
            }
        ]
    }
}
```
打包好后添加`HTML`文件添加`id`为`root`的`div`，引入打包好后的`js`文件就可以看到效果了

##### 使用`css`及`less(sass)`
- 安装 `npm css-loader style-loader less less-loader`
- 创建`css`文件，写好样式引入到`react.js`中，通过`className`设置样式

``` js
import React from 'react';
import ReactDom from 'react-dom';
import './color.css'
class Search extends React.Component {
    render () {
        return <div className="color">使用loader</div>
    }
}
ReactDom.render(
    <Search/>,
    document.getElementById('root')
)
```

``` js
// 安装css-loader 和 style-loader
let path = require('path');
// webpack.config.js
module.exports = {
    mode: 'development',
    entry: './src/index.js',
    output: {
        filename: 'index.js',
        path: path.resolve(__dirname, 'dist')
    },
    modlue: {               // Loader 配置
        rules: [
            {
                test: /.\css$/,    // 正则搜索以css结尾的文件
                use: [
                    'style-loader',
                    'css-loader'            // 先解析css，解析好后传递为style-loader设置dom的样式
                ]
            }
        ]
    }
}
```

##### 使用`less`或者`sass`
- 步骤和安装`less`一样

``` js
import React from 'react';
import ReactDom from 'react-dom';
import './color.less'
class Search extends React.Component {
    render () {
        return <div className="color">使用loader</div>
    }
}
ReactDom.render(
    <Search/>,
    document.getElementById('root')
)
```

``` js
// 安装css-loader 和 style-loader
let path = require('path');
// webpack.config.js
module.exports = {
    mode: 'development',
    entry: './src/index.js',
    output: {
        filename: 'index.js',
        path: path.resolve(__dirname, 'dist')
    },
    modlue: {               // Loader 配置
        rules: [
            {
                test: /.\css$/,    // 正则搜索以css结尾的文件
                use: [
                    'style-loader',
                    'css-loader'，            // 先解析css，解析好后传递为style-loader设置dom的样式
                    'less-loader'            // 解析成为css
                ]
            }
        ]
    }
}
```

#### 解析图片、文字
- `npm i file-loader -D`

``` js
import React from 'react';
import ReactDom from 'react-dom';
import './color.less';
import logo from './assets/images/tree.png';
class Search extends React.Component {
    render () {
        return <div className="color">使用loader
            <img src={ logo } />
        </div>
    }
}
ReactDom.render(
    <Search/>,
    document.getElementById('root')
)
```

``` js
// 安装css-loader 和 style-loader
let path = require('path');
// webpack.config.js
module.exports = {
    mode: 'development',
    entry: './src/index.js',
    output: {
        filename: 'index.js',
        path: path.resolve(__dirname, 'dist')
    },
    modlue: {               // Loader 配置
        rules: [
            {
                test: /.\css$/,    // 正则搜索以css结尾的文件
                use: [
                    'style-loader',
                    'css-loader'，            // 先解析css，解析好后传递为style-loader设置dom的样式
                    'less-loader'            // 解析成为css
                ]
            },
            {
                test: /.(png|gif|jpg|jpeg)$/,
                use: 'file-loader'
            }
        ]
    }
}
```

##### 字体文件
将字体文件包导入到项目中
``` less
@font-face {
    font-family: '字体文件名';
    src: url('字体文件包目录')
}
.color {
    font-family: '字体文件名'
}
```
``` js
let path = require('path');
// webpack.config.js
module.exports = {
    mode: 'development',
    entry: './src/index.js',
    output: {
        filename: 'index.js',
        path: path.resolve(__dirname, 'dist')
    },
    modlue: {               // Loader 配置
        rules: [
            {
                test: /.\css$/,    // 正则搜索以css结尾的文件
                use: [
                    'style-loader',
                    'css-loader'，            // 先解析css，解析好后传递为style-loader设置dom的样式
                    'less-loader'            // 解析成为css
                ]
            },
            {
                test: /.(woff|woff2|eot|ttf|otf)$/,
                use: 'file-loader'
            }
        ]
    }
}
```



``` js
let path = require('path');
// webpack.config.js

```