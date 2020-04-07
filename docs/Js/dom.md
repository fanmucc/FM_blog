#### js对于Dom的操作
### 查询节点api

- `document.getElementById('id名')`
- `document.getElementsByTagName('元素名')`  返回一个包括所有给定标签名称的元素的HTML集合`HTMLCollection`。 整个文件结构都会被搜索，包括根节点。返回的 HTML集合是动态的, 意味着它可以自动更新自己来保持和 `DOM` 树的同步而不用再次调用
- `document.getElementsByName('id名')` 主要是通过指定的`name`属性来获取元素，它返回一个即时的NodeList对象
- `document.getElementsByClassName('class名')` 返回查询指定`class`名集合
- `document.querySelector()`和`document.querySelectorAll()` 


### 创建节点api