#### 数据修改

小程序数据定义在`data`中
``` js
data: {
    message: '我是一条数据'
}
```
此时在页面中通过`{{message}}`就能进行数据的展示。

修改数据时使用`this.setData`进行修改
``` js
// <view bindtap="setMessageData">{{message}}</view>
// 修改message数据
setMessageData() {
    this.setData({
        message: '新值'
    })
}
```