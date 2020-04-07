#### 打包

> 

实现一个大整数加法库的打包
- 需要打包压缩版与非压缩版代码
- ⽀持 `AMD/CJS/ESM` 模块引⼊, 或者`CDN`的引入

``` js
// ⽀持 ES module
import * as largeNumber from 'large-number';
// ...
largeNumber.add('999', '1');
// ⽀持 CJS
const largeNumbers = require('large-number');
// ...
largeNumber.add('999', '1');
// ⽀持 AMD
require(['large-number'], function (large-number) {
    // ...
    largeNumber.add('999', '1');
});
```
