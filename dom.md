# DOM模型
* 操作网页的接口
* ELement 1 Attribute 2 Text 3 Comment 8 
* Document 9 DocumentType 10 DocumentFragment 11
* Node.nodeName /nodeType/nodeValue(text/comment节点)
* Node.textContent 当前节点的文本内容
* Node.ownerDocument:document对象。
* nextSibling previousSibling parentNode parentElement
* childNodes 动态集合
* firstChild lastChild 
* hasChildNodes是否有子节点
* cloneNode 注意相同ID
* appendChild 作为最后一个子节点插入,如果是现有的节点,该节点将从原有的位置移除
* 父节点.insertBefore(所要插入的节点,当前节点的子节点不能是后代节点)
* 如果是现有的节点,该节点将从原有的位置移除
* 结合nextSibling属性模拟insertAfter
* removeChild(必须是子节点不能是非子节点的后代节点) 被移除的节点依然存在于内存之中
* 父节点.replaceChild(新节点,要被替换走的子节点)
* contains参数是否为后代节点。
* compareDocumentPosition二进制值
* 0 相同 1 不在同一个文档 2 参数在前 4 参数在后 8 参数包含当前节点 16 当前节点包含参数 
* isEqualNode两个节点是否相等,相等的节点子节点相同。
* normalize 清理Text子节点
* 两种节点的集合：NodeList和HTMLCollection。
* typeof NodeList/HTMLCollection // "function"
* Node.childNodes/document.querySelectorAll()
* Node.childNodes动态    document.querySelectorAll静态
* length属性和数字索引
* Array.prototype.slice.call(div_list);
* forEach.call(element.childNodes, function(child){
* 不要使用for...in循环去遍历NodeList实例对象,会将length属性也遍历进去，而且不保证顺序。
* for (var item of list) {
* item方法，数字索引,从零开始计数
* document.links/forms/images HTMLCollection
* HTMLCollection可以用元素的id name属性引用
* document.myform===document.forms.myform;
* HTMLCollection与NodeList的区别
* HTMLCollectionm只能是Element节点
* HTMLCollectionm动态集合
* HTMLCollection用id属性或name属性，NodeList只能使用数字索引。
* HTMLCollection item(数字索引,ID,name)，namedItem(ID,name)
* 都可以用方括号运算符代替,建议一律使用方括号
* ParentNode接口
* Element,Document,DocumentFragment节点
* children:HTMLCollection Element子节点
* firstElementChild lastElementChild childElementCount
* ChildNode接口
* Element,DocumentType,CharacterData
* Elem.remove() 移除当前节点 replaceWith() 使用参数指定的节点，替换当前节点。 
* before/after在当前节点的前面，插入一个同级节点。 
* document节点
* 获取document节点
* document,window.document,iframe节点的contentDocument
* XMLHttpRequest的responseXML,ownerDocument
* document.doctype==document.firstChild：当前文档类型DTD 
* document.documentElement：<html>
* document.defaultView：document对象所在window对象
* document.body <body>
* document.head <head>
* document.activeElement当前文档获得焦点的元素
* document.scripts
* document.styleSheets：当前网页所有的样式表
* document.documentURI(所有文档)/document.URL(HTML文档)
* Node.baseURI(绝对路径)
* document.domain
* document.lastModified(最后修改的时间戳) 字符串不能比较
* 用Date.parse转化一下
* document.location:URL
* document.location.href 
* document.location.protocol/host/hostname/port/pathname
* search(?x=111)/hash/user/password/
* document.location.assign() 跳转到另一个网址
* document.location.reload(true(从服务器)/false(从缓存)) 
* document.location.toString()=document.location.href
* document.location = baidu.com 网页直接跳转
* document.location = '#top' 自动滚动到锚点处
* 点击后退就可以回到前一个网页。
* document.referrer来源/title/characterSet字符集
* readyState:loading正在html代码，尚未完成解析/interactive正在加载页面资源/complete加载完成
* document.implementation.hasFeature(“HTML”,”2.0”);
* document.compatMode:CSS1Compat/BackCompat
* 设置了明确的DOCTYPE,compatMode的值都为CSS1Compat。
* document.open() 清除文档，重新写入内容
* document.close() 用于关闭document.open新建的文档
* document.write() 内容会当做HTML代码解析
* 渲染中不会调用open，DOMContentLoaded后，先open再写入
* querySelector/querySelectorAll不支持伪元素,伪类getElementsByTagName(p) HTML标签 
* getElementsByClassName() 空格分隔 符合所有 顺序不重要
* document.getElementsByName()
* document.getElementById() 效率比querySelector高
* document.elementFromPoint视口 最上层的元素 
* document.createElement/createTextNode/createAttribute
* node.setAttributeNode(a);
* node.setAttribute(“me”,”value”);
* document.createDocumentFragment() 不会重新渲染 性能好document.hasFocus() 是否有元素被激活

```
var nodeIterator = document.createNodeIterator(document.body);
var pars = [];
var currentNode;
while (currentNode = nodeIterator.nextNode()) {
  pars.push(currentNode);
}
```
* document.createNodeIterator(根节点,节点类型)
* NodeFilter.SHOW_ALL/SHOW_ELEMENT/SHOW_TEXT/SHOW_COMMENT
* nodeIterator .nextNode()/previousNode()
* treewalker=document.createTreeWalker(根节点,节点类型);
* treewalker.nextNode() treewalker.currentNode;
* document.importNode(节点，深/浅拷贝) 拷贝外部节点
* 不会把原来的节点删掉
# Element
* 不同标签 HTMLAnchorElement HTMLButtonElement
* Element.attributes/id/tagName
* innerHTML 包含& < >,读取时会转码，写入会解析成节点
* outerHTML 赋值替换掉当前元素
* className/classList
  * classList:add/remove/contains/toggle/item/toString
* getBoundingClientRect().top/left 视口
* getBoundingClientRect().left+scroll距网页
  * 网页元素本身的高宽：
    * Element.getBoundingClientRect().width/height
    * Element.offsetHeight/offsetWidth
    * clientHeight和clientWidth:视觉面积 内容+padding
  * 浏览器窗口的高和宽：
    * document.documentElement.clientWidth/clientHeight
    * IE6 quirks:document.body.clientWidth
    * 必须在页面加载完成，否则document对象还没生成
    * 滚动条滚过的长宽:每个元素scrollHeight和scrollWidth
* Element.offsetParent:position不等于static 最近 上层元素
* offsetTop offsetLeft:元素左上角距offsetParent左上角
  * 元素的绝对位置：offsetLeft/offsetTop累加
  * 元素的相对位置：绝对坐标减去页面滚动
  * document.documentElement.scrollLeft/scrollTop
* 相对位置：Element.getBoundingClientRect().left/top
* 绝对位置：Element.getBoundingClientRect().left/top+document.documentElement.scrollLeft/scrollTop
* children/childNodes
* childElementCount===children.length
* firstElementChild/lastElementChild/nextElementSibling/previousElementSibling
* closest(CSS选择器) 本身或最近的父元素 
* match(CSS选择器)
* Element和document共有的四个方法
  * getElementsByTagName()
  * getElementsByClassName()
  * querySelector()
  * querySelectorAll()
* Element.scrollIntoView():true：顶部对齐 false尾部对齐
* getBoundingClientRect() 视口 边框+padding
* getClientRects():块级元素一个，行内元素占据多少行
  * 当前元素在页面上形成的所有矩形
  * 用于判断行内元素是否换行，以及行内元素的每一行的位置偏移
  * top,left，bottom,right,width,height
* Element.insertAdjacentHTML(position，HTML字符串)
  * 解析HTML字符串生成节点 
  * beforebegin/beforeend/afterbegin/afterend：元素节点的后面
* Element.remove()/focus()
