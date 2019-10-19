#### 打印样式
> 打印调用以及打印样式的修改；

[flex样式](https://changk99.github.io/flexbox/)
[table打印示例](https://github.com/fanmucc/printTable) 

常见打印内容
- 表格打印
- 吊牌打印
- 不干胶打印
- 洗唛打印

##### 区别

!> 表格打印与其下面三种打印的区别

1. 表格只需要适应宽度即可;即将表格的宽度调制100%就能展示出相应的样式
2. 吊牌\不干胶\洗唛等打印都有具体格式都是确定相应宽高;
3. 表格打印内容较多时会自动打印到下一张,样式不用担心变形,但吊牌\不干胶\洗唛等固定宽高的样式如果调整不好,样式将变形;

##### 样式的调试
> 针对吊牌\不干胶\洗唛等打印

1. 样式写在`ul > li` 中或者 `div`中;
2. 给`li` 或 `div` 确定高度 `约等于` 打印材料的样式;
3. 调整内容块(1中的`li` 或 `div`)之间的`margin`值;
4. 高度宽度使用`mm`毫米计量单位,比`px`更加准确;

##### 简单使用方法(printThis)
```js
1. printThis
// $(".print-box")为需要打印内容的class名, 可以自行调换成其他class,并不固定;
$(".print-box").printThis({
    importCSS: true,        // 导入父级css
    importStyle: true       // 导入样式标记
})// 打印的一个方式调用jq就行
// printThis可以传入的参数为

2. jqprint 0.3
$("#table").jqprint({
    debug: false,
    importCSS: true,
    printContainer: true,
    operaSupport: false
});
```

##### printThis全部参数
> [printThis官网](https://github.com/jasonday/printThis) 打开翻译查看具体参数内容；

```js
$("#mySelector").printThis({
    debug: false,               // show the iframe for debugging
    importCSS: true,            // import parent page css
    importStyle: false,         // import style tags
    printContainer: true,       // print outer container/$.selector
    loadCSS: "",                // path to additional css file - use an array [] for multiple
    pageTitle: "",              // add title to print page
    removeInline: false,        // remove inline styles from print elements
    removeInlineSelector: "*",  // custom selectors to filter inline styles. removeInline must be true
    printDelay: 333,            // variable print delay
    header: null,               // prefix to html
    footer: null,               // postfix to html
    base: false,                // preserve the BASE tag or accept a string for the URL
    formValues: true,           // preserve input/form values
    canvas: false,              // copy canvas content
    doctypeString: '...',       // enter a different doctype for older markup
    removeScripts: false,       // remove script tags from print content
    copyTagClasses: false,      // copy classes from the html & body tag
    beforePrintEvent: null,     // function for printEvent in iframe
    beforePrint: null,          // function called before iframe is filled
    afterPrint: null            // function called before iframe is removed
});
```