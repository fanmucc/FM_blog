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

##### Session

session是什么？ Session 是一种记录客户状态的机制，不同于 Cookie 的是 Cookie 保存在客户端的浏览器中，而 Session 保存在服务器上，避免了在客户端 Cookie 中存储敏数据。

Session 机制

Session 从字面意思上可以理解为会话， 谁与谁的会话呢？ 其实是客户端浏览器与服务器之间一系列交互的动作称之为 Session。

创建Session(java)

1. Session 在服务器端程序运行的过程中创建的， 不同语言实现的应用程序有不同穿件 Session 的方法；
2. Session 被创建之后，就可以调用 Session 相关的方法往 Session 中增加内容，而这些内容只会保存在服务器中，发到客户端的只有 session id；
3. 当客户端再次发送请求的时候，会将这个 session id 带上， 服务器接受到请求之后就会依据 session id 找到相应的 Session， 从而再此使用 Session.

Session的生命周期

Session 保存在服务器端，为了获得更高的存取速度，服务器一般吧 Session 放在内存中， 每个用户都会有一个独立的 Session。 如果 Session 内容过于复杂，当大量客户访问服务器时可能会导致内存溢出，因此， Session 里面的信息应该尽量精简

Session 在用户第一次访问服务器的时候自动创建，需要注意只有访问 JSP、Servlet 等程序时才会创建 Session， 只访问 HTML、IMAGE 等静态资源并不会创建 Session。如果尚未生成 Session， 也可以使用 request.getSession(true) 强制生成 Session 。

Session 生成后，只要用户继续访问，服务器就会更新 Session 的最后访问时间，并维护改 Session。 用户每次访问服务器一次， 无论是否读写 Session， 服务器都认为该用户的 Session 活跃(avtive)了一次；

Session 有效期

由于会有越来越多的用户访问服务器， 因此 Session 也会越来越多， 为防止内存溢出， 服务器会把长时间内没有活跃额 Session 用内存中删除， 这个时间就是 Session 的超时时间，如果超过了超时时间没有访问过服务器， Session 就自动失效了。

Session 的超时时间为 maxInactiveInterval 属性， 可以通过对应的getMaxInactiveInterval()获取，通过setMaxInactiveInterval(longinterval)修改。Session的超时时间也可以在web.xml中修改。 另外，通过调用Session的invalidate()方法可以使Session失效。

三种方法让 Session 失效

- 服务器以外关闭；（服务器正常关闭时session是会被服务器保存在服务器的 session.ser 文件中（在work文件夹下））
- session自杀： 调用 session.invalidate()方法可以立刻杀死 session;
- 可以在服务器下的 web.xml 文件中 <session-timeout> 30 </session-timeout> 修改这个默认值(30分钟)，是以分为单位；

浏览器关闭 Session 会失效？

为什么失效

下面梳理一下session为什么会在浏览器关闭时失效，其实这样说并不准确：

- 在服务器端生成session，并且把sessionid通过set-cookie发送给浏览器
- 以后每次请求除了图片、静态文件请求，其它的请求都会带上服务端写入浏览器中cookie
- 服务端接收到sessionid，通过sessionid找到对应的session信息
- 当浏览器关闭时，当前域名中设置的cookie会被清空
- 再下次请求使，服务端接收到的session为null，服务端就会认为当前用户是一个新的用户，重新登录或者直接设置新的sessionid

上面也就是为什么会说session会在浏览器关闭时会失效。

怎么能让它不失效？

在Set-Cookie时设置Expries或Max-Age，其实就是设置Cookie的失效时间。或者直接把Sessionid储存在本地。


