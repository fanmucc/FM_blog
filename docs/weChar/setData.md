#### 数据修改

#### data

`data` 是页面第一次渲染使用的初始数据

页面加载时，`data` 将会以JSON字符串的形式由逻辑层传至渲染层，因此data中的数据必须是可以转成`JSON`的类型：字符串，数字，布尔值，对象，数组。

渲染层可以通过 `WXML` 对数据进行绑定。

小程序数据定义在`data`中
``` js
data: {
    message: '我是一条数据'
}
```
此时在页面中通过`{{message}}`就能进行数据的展示。

修改数据时使用`this.setData`内数据进行简单修改
``` js
// <view bindtap="setMessageData">{{message}}</view>
// 修改message数据
setMessageData() {
    this.setData({
        message: '新值'
    })
}
```

- 修改`data`数据中的数组对象数据
``` data
data: {
    message: 'data',
    images: [{
        index: 0,
        imgPath: '*****',
        text: '照片1'
    },
    {
        index: 1,
        imgPath: '*****',
        text: '照片2'
    }]
}
```

这个时候在通过就会报错
```  
// 报错
this.setData({
    images[1].imgPath = ***
})
```

1. 拿到需要修改位置的下标
2. 获得需要修改信息的属性名(完整的属性名)
``` js
data: {
    images: [{
        index: 0,
        imgPath: '*****',
        text: '照片1'
    },
    {
        index: 1,
        imgPath: '*****',   // 需要修改的图片地址
        text: '照片2'
    }]
}
```
3. 下标和属性名拼接(以上面的数据为例):  `images[1].imgPath`  这一点要注意看 前面没有`this.data.images`直接就是`imgPath`
4. 拼接对象, 设置一个空对象如:
``` js
let newObj = {}
newObj[第三部下标和属性名的拼接] = '新的图片地址'
```
5. 将设置的新对象使用 `setData` 动态的传递过去 `this.setData(newObj)`

完整示例
``` js
let index = 1;   // 获取下标
let objName = `images[${index}].imagePath`; // 通过下标获取到要修改的属性名
let newObj = {};   // 设置空对象
newObj[objName] = '新的图片地址';
this.setData(newObj);
```
