* http 无状态协议
  * 服务器 set-cookie session-id识别用户
  * 服务器把session-id和用户认证信息绑定记录
  * 浏览器发cookie，服务器收到session-id,去记录查得到之前的状态信息。
  * sessionid被盗走,伪造你的身份进行恶意操作,使用难以推测的字符串
  * Cookie包含的字段：
    * Expires 不设置cookie只在当前会话有效
      * 本地时间决定Cookie是否过期 不精确 max-age代替
    * domain path secure 
    * httpOnly:不能被js读取,只用于服务器发送,防止XSS
    * 修改cookie:key domain path
    * 浏览器发请求自动附上Cookie
  * document.cookie 读全部 写一个
* CSRF 跨站请求伪造
  * 挟制用户在当前已登录的web应用程序上执行非本意攻击
    * 用户刚访问网站不久，cookie还有效
    * 黑客以广告引导受害者访问，网站自动发请求 目标网站黑客的参数
  * 看不到cookie和响应的数据 保护数据改变的操作。
    * 验证请求来源referer 依赖浏览器
    * 黑客伪造不了的信息token 服务器验证
    * 遍历a form
    * 论坛黑客发网址 连接到自己网站才加token
* XSS 多种多样 
  * 跨站脚本，网站应用程序的安全漏洞攻击
  * 恶意用户将代码注入网页，HTML及脚本
  * 攻击脚本通过输入 富文本编辑 改变页面显示或者数据库
  * 最常见的就是 document.cookie
  * 别在页面插不可信的数据，非得插就得好好编码
  * html attr script CSS url编码
  * 闭合
  * Cookie httponly
  * 浏览器端和服务器端验证输入
  * document.createTextNode() 返回的节点当做文本渲染，而不是HTML代码渲染,对大于号小于号进行转义,但不对单引号，双引号转义
  * textContent代替innerHTML 忽略节点内部的HTML标签，返回所有文本内容,自动对HTML标签转义,适合用户提供的内容。
