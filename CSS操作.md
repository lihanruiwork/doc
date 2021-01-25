# CSS操作：
```
div.setAttribute("style","background-color:red;");
div.getAttribute("style");
div.removeAttribute("style");
```
* Style对象：div.style
* div.style.width
* Style对象的cssText属性能够读写document整个样式
```
div.style.cssText; //background-color: red;
```
* 带不带连字符都行
```
div.style["backgroundColor"]
div.style["background-color"]
div.style.backgroundColor 
```
* 如果设置了该属性，返回属性值
* 如果没设置该属性，返回空串
* 如果当前浏览器不支持该属性，返回undefined
* Css模块的侦测：
  * typeof div.style.width==="string"
  * Css模块的侦测把不同浏览器的CSS规则前缀也考虑进去
    ```
    function isPropertySupported(property){
      if (property in document.body.style) return true;
      var prefixes = ['Moz', 'Webkit', 'O', 'ms', 'Khtml'];
      var prefProperty=property.charAt(0).toUpperCase() + property.substr(1);
      for(var i = 0; i < prefixes.length; i++){
        if((prefixes[i] + prefProperty) in document.body.style) 	return true;
      }
      return false;
    }
    ```
    * isPropertySupported('background-clip')// true
* Style对象的三个方法 
  * setProperty 
  * getPropertyValue 
  * removeProperty
* 浏览器最终计算出的样式规则
  ```
  window.getComputedStyle(div).backgroundColor; // rgb(255,0,0)
  window.getComputedStyle(div).getPropertyValue(“height”) // 200px
  ```
  * 由getComputedStyle计算返回的CSS值都是绝对单位，长度都是像素单位（px后缀），颜色是rgb(#, #, #)或rgba(#, #, #, #)格式。
  * DOM节点的style对象无法读写伪元素的样式，要用到window对象的getComputedStyle
  * getComputedStyle可接受第二个参数 当前节点的伪元素
    ```
    window.getComputedStyle(div,":after").content;
    window.getComputedStyle(div,":after").getPropertyValue("content");
    ```
* StyleSheet对象：代表网页的一张样式表
  * document.styleSheets 网页中所有StyleSheet对象
  * <link><style>节点的sheet属性也为stylesheet对象
  ```
  document.styleSheets[0]==document.querySelector("style").sheet
  ```
  * StyleSheet对象的属性：
    * media :screen屏幕 print打印 all
      * stylesheet.media.mediaText  //all
    * disabled:打开或关闭一张样式表
    * href 
    * title 
    * type
    * parentStyleSheet 包含当前样式表的那张样式表
      * @import在样式表中加载其他样式表
    * ownerNode:stylesheet对象所在的DOM节点，通常为link或style
    * cssRules 当前样式表中的规则,类似数组
      * sheet.cssRules[0].cssText
        * body { background-color: red; margin: 20px; }
      * sheet.cssRules[0].style.color
    * 在当前样式表的cssRules对象插入CSS规则
      * sheet.insertRule(“#block{color:white;}”,插入位置索引);
      * sheet.deleteRule(1);
* 添加样式表：
  * 内置样式表 <style>
    ```
    var style = document.createElement(style);
    style.setAttribute(“media”,”screen”);
    style.innerHTML=”body{color:red;}”;
    document.head.appendChild(style);
    ```
  * 外部样式表 <link>
    ```
    var link = document.createElement(link);
    link.setAttribute(“rel”,”stylesheet”);
    link.setAttribute(“href”,””);
    document.head.appendChild(link); 
    ```
* Css规则：
  * cssRule接口的属性：
    * cssText 
    * parentStyleSheet 定义当前规则的样式表对象
    * parentRule 包含当前规则的CSS规则，比如当前规则包含在@media代码块中
    * type:当前规则的类型 
      * 1 样式规则 cssStyleRule
      * 3 输入规则 cssImportRule
      * 4 Media规则 CSSMediaRule
      * 5 字体规则 cssFontFaceRule
* 一条CSS规则部署的接口：
  * CSSStyleRule接口
  * selectorText:当前规则的选择器  .myClass
  * style 样式声明 {}中的内容
  * CSSMediaRule接口 @media代码块
  * media：media规则
* 大括号内部的部分都是一个CSSStyleDeclaration对象
  * 主要包括三部分：
    * HTML 元素的行内样式（<elem style="...">）
    * CSSStyleRule接口的style属性
    * window.getComputedStyle()的返回结果
    * styleObj = document.styleSheets[0].cssRules[1].style;
      ```styleObj.color // "red";```
  * CSSStyleDeclaration的其他属性和方法：
    * cssText 
    * length 
    * parentRule
  * getPropertyPriority(“color”):声明的优先级 important或空串
  * getPropertyValue(“color”) 
  * removeProperty(“color”) 
  * setProperty(“color”,”green”,”important”)
* window.matchMedia方法用来检查CSS的mediaQuery语句
  * 显示媒介（包括浏览器和屏幕等）满足mediaQuery语句设定的条件，就会执行区块内部的语句
    ```
    @media all and (max-width:700px){
      body{
        background:#FFF;
      }
    }
    // 该区块对所有媒介有效，且视口最大宽度不得超过700px
    ```
  * mediaQuery接受两种宽度/高度的度量，视口和设备
    * max-width 视口  
    * max-device-width:设备
  * 视口用documentElement.clientWidth/clientHeight来衡量
  * 设备用screen.width/height来衡量
  * result=window.matchMedia(“(min-width:600px)”)
    * 返回一个mediaQueryList对象
    * result.media  //返回所查询的mediaQuery语句字符串
    * result.matches  //布尔值，表示当前环境是否匹配查询语句。
    * result.addListener(mqCallBack)
    * result.removeListener(mqCallBack)
      * 回调函数的参数 MediaQueryList对象
* CSS事件：
  * Transition效果结束后，触发transitionEnd事件
    * Event的属性：
      * propertyName:发生transition效果的css属性名
      * elapsedTime：transition效果持续的秒数
      * pseudoElement：如果发生在伪元素，返回伪元素的名称，以::开头
  * animationstart 动画开始 
  * animationend 动画结束 
  * animationiteration 开始新一轮动画循环时触发
    * 他们仨都有 event.animationName event.elapsedTime
