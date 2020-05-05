#### HTML语义化

> 语义化是指根据内容的结构化(内容的语义化)，选择合适的标签(代码语义化), 便于开发者阅读和写出更优雅代码的同时, 让浏览器的爬虫和机器的更好的解析

##### 为什么要语义化？
- 有利于SEO, 有助于爬虫抓取更多的有效信息, 爬虫是依赖于标签来确认上下文和各个关键字的权重;
- 语义化的HTML在没有css的情况下也能较好的展示内容结构和代码结构;
- 方便其他设备的解析;
- 便于团队开发和维护;

![语义化](https://upload-images.jianshu.io/upload_images/11461186-c74242ae8498fc9f.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/619/format/webp)

如上图，这个页面结构中摒弃了所有div元素，取而代之的是HTML语义化标签（用哪些标签取决于你的设计目的）。
同样，W3C制定了这些语义化标签，不可能完全符合我们的设计目标。我们的目标是为了能够让开发者或是爬虫读懂各个模块的语义化内容，因此，div作为一个没有任何语义，仅仅是用来构建结构的元素，是最适合做容器的标签

`header`
1. 定义文章的介绍信息: 标题、logo、 slogan、 包裹目录部分、 搜索框, 一个nav或者任何相关的logo;
2. 一个页面中的header没有个数限制,  可以为每个内容块添加一个header;

`nav`
1. 定义文章导航栏, 链接等;
2. nav一般和ul、li 配合做导航栏;

`main`
1. 定义文章的主要内容;
2. main标签在一份文档中是唯一的, 其后代元素常常包括article;

`article`
1. 定义文档中可以脱离其他部分, 一份独立的内容, 通常带有标题, 当article内嵌article时, 里外层的内容应该是相关的， 比如一遍微博和他的评论;

`section`
1. 与article的差别在于, 它是整体的一部分，或者是文章的一节， 一般来说section也会带有标题;

`aside`
1. 侧边栏(与article并列存在)或者嵌入内容(在article中), 通常认为是独立拆分出来而不受整体影响的一部分， 作为主要内容的附属信息，如索引，词条列表或者页面及站点的附属信息，如广告，作者资料介绍等;

`footer`
1. 页面，通常包括作者、版权信息或者相关链接等；