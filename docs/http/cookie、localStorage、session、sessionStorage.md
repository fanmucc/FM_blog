#### cookie、localStorage、session、sessionStorage

##### cookie 

在 HTTP 请求建立连接时,有一个客户端、服务端它们两个之间建立的连接。但是 HTTP 协议每次建立连接都是独立的额，也可以说是 HTTP 协议是无状态的连接。

- 第一次建立连接，客户在客户端中登录，服务器验证登录信息，生成 TOKEN 为以后的请求不需要重新登录。
- 第二次建立连接，客户端携带服务器在登录成功时返回 TOKEN, 但是这个 TOKEN 要储存在哪里? 一般会存在 cookie 里。

简单总结一下就是，因为 HTTP 协议是无状态的所以客户需要一个 cookie 来存储起来；

HTTP Cookie (也叫Web Cookie或浏览器Cookie)是服务器发送到用户浏览器并保存在本地的一小块数据，它会在浏览器下次向同一服务器再发送请求时被携带并发送到服务器上。

Cookie 主要用于以下三个方面:

- 会话状态管理(如用户登录状态、购物车、游戏分数或者其他需要记录的信息)
- 个性化设置(如用户自定义设置、主题等)
- 浏览器行为跟踪(如跟踪分析用户行为等)

创建 Cookie

当服务器收到 HTTP 请求时，服务器可以在响应头里面添加一个 `Set-Cookie` 选项。浏览器收到相应后会通常保存下 cookie，之后对该服务器每一次请求中都通过 cookie 请求头部将 cookie 信息发送给服务器

在创建cookie是可以设置很多属性，如Expires、Max-Age、Domain、Path、Secure、HttpOnly，因为它会自动携带到服务器端，同事又支持服务器端设置。所以有很多的方面要注意，比如时效性、作用于、安全性。

时效性

如果在 Set-Cookie时不通过 Expries、Max-Age 两个字段设置 Cookie 的时效性， 那么这个 cookie 是一个简单的会话期Cookie。它在关闭浏览器是会被自动删除。

如果设置了 Expries、Max-Age 那么这个 Cookie 在指定时间内都是有效的。

> 提示： 当 Cookie 设置过期时间时，设置的日期和时间只与客户端相关，而不是服务端

作用域

Domain 和 Path 标识定义了 Cookie 的作用域: 既 Cookie 应该发给哪些 URL。

Domain 标识指定了哪些主机可以接受 Cookie。 如果不指定， 默认为当前文档的主机(不包含子域名)。如果指定了 Domain， 则一般包含子域名；

Path 标识指定了主机下哪些路径可以接受 Cookie (该URL路径必须存在于请求URL中)。以字符串%x2F("/")作为路径分割符，子路径也会被匹配；

安全性

标记为 Secure 的 Cookie 只应通过被 HTTPS 协议加密过得请求发送给服务端，但即便设置了 Secure 标记，敏感信息也不应该通过 Cookie 传输， 因为 Cookie 有其固有的不安全性， Secure 标记也无法提供确实的安全保障；

>! 从 Chrome 52 和 Firefox 52 开始， 不安全的站点(http:)无法使用 Cookie 的 Secure 标记

为避免跨域脚本(XSS)攻击，通过 JavaScript 的 Document.cookie API无法访问带有 HttpOnly 标记的 Cookie， 它们只应该发送给服务端；

cookie 的特点

优点: 
- 储存用户信息(用户token)；
- 编辑用户行为(uuid、埋点)；

弊端: 
- Cookie 会被附加到每个 HTTP 请求中，所以无形中增加了流量；
- Cookie 可能被禁用，当用户非常注意个人隐私保护时， 他很有可能禁用浏览器的 Cookie 功能；
- 由于在 HTTP 请求中的 Cookie 是明文传递，潜在的安全风险为 Cookie 可能被篡改；
- Cookie 数量和长度的限制。每个域名(Domain)下 IE6或IE6-(IE6以下版本)：最多20个cookie、 IE7或IE7+(IE7以上版本)：最多50个cookie、FF:最多50个cookie、Opera:最多30个cookie Chrome和safari没有硬性限制当超过单个域名限制之后，再设置cookie，浏览器就会清除以前设置的cookie。IE和Opera会清理近期最少使用的cookie，FF会随机清理cookie；
- 每个 Cookie 长度不能超过4KB

Cookie 安全问题

Cookie 面临什么样的安全问题，常见的 XSS、CSRF 等

xss和 防御xss

如果在服务器端 Set-Cookie 时没有设置 HttpOnly=true 时， 在浏览器端可以通过 document.cookie 来读取和修改 Cookie 中的值， 这是十分安全的会造成 xss。当 Cookie 中有关键性信息时要设置 HttpOnly=true。

防止中间人劫持

大致的分布图是 

``` js
         DNS
     <----->
用户          中间人       外网
     <----->
       HTTP
```

当使用 HTTPS 协议和购买正规的CA证书时，即使中间人劫持也无法解密。并且在 Set-Cookie设置 Secure=true 时 Cookie 只应通过被 HTTPS 协议加密过得请求发送给服务器端

csrf 和 csrf防御

CSRF: 跨站请求伪造 (CSRF) 是一种冒充受信任用户, 向服务器发送非预期请求的攻击方式。

例如，这些非预期请求可能是通过再跳转链后的 URL 中加入恶意参数来完成：

``` html
<img src="https://www.example.com/index.php?action=delete&id=123"/>
```

对于在`https://www.example.com`有权限的用户，这个`<img>`标签会在他们根本注意不到的情况下对`https://www.example.com`执行这个操作,即使这个标签根本不在`https://www.example.com` 内亦可。

`SameSite Cookie` 允许服务器要求某个 `cookie` 在跨站请求时不会被发送, 从而可以组织跨站请求 伪造攻击`(CSRF)`。但是目前 `SameSite Cookie`还处于试验阶段，并不是所有浏览器都支持。

- `strict`: 浏览器在任何跨域请求中都不会携带 Cookie, 这样可以有效的防御 `CSRF` 攻击，但是对于有多个子域名的网站采用主域名存储用户登录信息的场景，每个子域名都需要用户重新登录, 造成用户体验非常差；
- `lax`: 相对于`strict`，它允许从三方网站跳转过来的时候使用 `Cookie`.

其他防御

- 设置 Cookie 有效期时间
- 防止 Cookie 是明文，服务器端生成秘钥验证
- 生成随机数和 Cookie 发送给服务器端
- `flash编程安全`, 审核 `flash代码`, 尽量不要用 `flash` 用最新的HTML5标签：如 `Video`等