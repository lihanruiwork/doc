* display:none 将元素与其子元素从普通文档流中移除
* visibility:hidden 依然占据原来的空间
* display:inline 
  * 行内级元素/内联元素 
  * 宽度随元素的内容变化 
  * width height属性无效 
  * padding-left/right margin-left/right产生边距效果 
  * 竖直方向不会产生边距效果 
  * span a strong em label input select textarea img br 
* display：block 
  * 独占一行 
  * 可以设置width height 
  * 可以设置margin padding
  * div form table p pre h1-h6 dl ol ul 
  * block元素可以包含block和inline元素，但inline元素只能包含inline元素
* display:inline-block
  * 将对象呈现为inline
  * 之后的内联元素会被排列在同一行内，但内容作为block呈现
  * 可以设宽度，高度等inline没有的属性
* display:list-item 
  * 列表项呈现
  * 可以被list-style属性进行样式修饰的标记框
* 基于表格的布局
  * display:table
  * display:table-header-group  <thead>
  * display:table-row-group     <tbody>
  * display:table-footer-group  <footer>
  * display:table-column-group  <colgroup>
  * display:table-row           <tr>
  * display:table-cell          <td>
  * display:table-column        <col>
  * display:table-caption       <caption>
  * display:inline-table        表现为表格HTML元素，但是是一个内联块而不是块级元素
* display:flex 弹性盒子
  * flex容器属性：
    * flex-direction:row column row-reverse column-reverse
    * flex-wrap:nowrap wrap wrap-reverse 
    * flex-flow：前两个合并
    * justify-content：项目在主轴上的对齐方式
      * flex-start 、flex-end 、center 、space-between 、space-around
    * align-items：项目在侧轴对齐方式
      * flex-start 、flex-end 、center 、stretch、baseline
    * align-content：多行在容器中如何分布
      * flex-start、flex-end、center、stretch
  * flex项的相关属性：
    * order：flex项目根据order值重新排序 没order的放前面有order的放后面
    * flex-grow：默认0（不会扩展） 1会扩展填充可用空间
    * flex-shrink：空间不够，是否可缩小 默认1
    * flex-basis：指定项目初始大小 auto(基于内容的多少来自动计算) 150px(固定宽度) 比width优先级高
    * flex:前三个的合并
    * 伸展度不一样：一个项目 flex-grow=1另一个项目 flex-grow=2  
      * 前一个占1/3  后一个占2/3
    * align-self：改变一个弹性项目沿着侧轴的位置，而不影响相邻的弹性项目
      * flex-start flex-end center baseline stretch auto  
    * 自动外边距
      * margin-right:auto 右边占据所有剩余空间
      * margin:auto 两边分割剩余空间
      * 有了自动外边距，justify-content 就不起作用了
