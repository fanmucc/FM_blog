#### 移动端视图

> <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">

##### `viewport`的基础概念

是指视窗、视口、浏览器(也可能是一个app中的webview)用来显示网页的那部分区域，在移动端和pc端的窗口是不同的, pc端的视口是浏览器窗口区域, 而在移动端有三个不同的视口概念: 布局视口、视觉视口、理想视口

- 布局视口: 在浏览器窗口的css的布局区域, 布局视口的宽度限制css布局的宽度, 为了能在移动设备上正常显示那些为pc端浏览器设计的网站, 移动端浏览器可视区域大很多, 所以就会出现浏览器出现横向滚动条的情况;

- 视觉视口: 用户通过屏幕看到的页面区域, 通过缩放查看显示内容的区域, 在移动端缩放不会改变布局视口的宽度, 当缩小的时候, 屏幕覆盖的css像素变多, 视觉视口变大, 当放大 的时候, 屏幕覆盖的css像素变少, 视觉视口变小;

- 理想视口: 一般来讲, 这个视口其实不是真实存在的, 它对于设备来说是一个理想布局视口尺寸, 在用户不进行手动缩放的情况下, 可以将页面理想的展示, name所谓的理想官渡就是浏览器(屏幕)的宽度了;


``` html
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
```

|属性|定义|取值|
|:---|:---|:---|
|width|定义视口的宽度,单位为像素|正整数或设备宽度device-width|
|heigth|定义视口的高度,单位为像素|正整数或者设备高度device-height|
|initial-scale|定义初始缩放值|整数或者小数|
|maximum-scale|定义放大最大比例,它必须大于或者瞪目minimum-scale设置|整数或者小数|
|minimum-scale|定义缩放最小比例,它必须小于或等于maximum-scale设置|整数或者小数|
|user-scalable|定义是否允许用户手动缩放页面,默认值为yes|yes/no|

