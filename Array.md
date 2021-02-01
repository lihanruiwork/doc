* 生成新的数组：
  * var array = new Array(2);//length=2 [undefined,undefined]
  * var array = Array(2);等同于上面
    * 参数是非正整数的数值会报错
    * 多参数时，所有参数都是新成员
    * 非数值参数是新成员
    * var arr = [1,2];
* 判断一个值是否为数组：
  ```value instanceof Array```
  * 缺点：假定单一的全局执行环境，如果包含多个框架，存在两个以上不同版本的Array构造函数，从一个框架向另一个框架传入一个数组，就不行啦 
  * 所以有了Array.isArray(arr)
  * typeof 只能显示Object
  * typeof 检测基本数据类型
  * instanceof 检测引用数据类型
  * 所有引用类型都是Object的实例
    * 引用类型：Object Array Date Regex Function 
    * typeof几种可能的值:undefined boolean string number object function
* 基本类型值不是对象，引用类型值都是Object实例。
* 自动创建的基本包装类型的对象，只存在于一行代码的执行瞬间
```
var a= new Number(123);
console.log(typeof a);
//object
console.log(a instanceof Number);
//true
console.log(a instanceof Object);
//true
var b=Number(123);
console.log(typeof b);
//number
console.log(b instanceof Number);
//false
console.log(b instanceof Object);
//false
```
* typeof是一个操作符
* 对未初始化和未声明的变量执行typeof都会返回undefined
* valueOf() [1,2,3] 
* toString() “1,2,3”  
* 改变原数组：
  * push() 返回新的数组长度 
  * pop() 返回被删除的元素
  * shift() 返回被删除的元素
  * unshift() 返回新的数组长度
  * reverse() 颠倒元素的顺序 返回改变后的数组
  * splice() 返回被删除的元素 (起始位置，被删除的个数，要被插入的新元素)
    * 第二个参数为0:只是单纯的插入 
    * 只有一个参数:将从参数位置一直删到最后，拆分成两个数组
  * sort()：按字符串的字典顺序排 先转成字符串再排
     * 按自定义排：传一个函数 函数返回值大于零就交换位置
     ```
        [].sort(function(a,b){
          return a-b;
        })
      ```
    * 原数组不变：
  * concat() 返回合并的新数组 接受其他类型的数值作为参数
  * slice(起始位置，终止位置) 提取元素的一部分，返回一个新数组， 终止位置元素本身不包括在内 参数是负数表示倒数计数位置
  * 将类似数组的对象转为真正的数组
    * Array.prototype.slice.call(document.querySelectorAll(“”)
    * 或者arguments
  * map(function(item，index，array){}) 
    * 所有成员依次调用一个函数 根据结果返回一个新数组
  * forEach() 没有返回值 无法中断 
  * 如果要中断用for
  * filter() 返回结果为true的新数组 
  * some() 返回true false 有一个数组成员返回true就是true 
  * every() 返回true false 所有数组成员返回true才是true
  * reduce
    ```
      reduce(function（累计变量，当前变量，当前位置，原数组）{
         ...
      },累计变量的初值);
    ```
    * 最终累计为一个值  
  * reduceRight() 
  * indexOf(给定元素，开始搜索的位置) 返回元素在数组中第一次出现的位置 
    * 没有返回-1 内部使用===进行比较
  * lastIndexOf() 返回元素在数组中最后一次出现的位置
  * 合并两个数组：
    ```Array.prototype.push.apply(a,b)```
  * 为对象添加元素:
    * 对象变得有length属性
    ```
      var a = {a:1};
      [].push.call(a,2)
      //{a:1,0:2,length:2}
    ```
  * push pop 后进先出 栈结构
  * unshift shift 
  * push shift 先进先出 队列
  * join 用参数作为分隔符，默认为逗号
    * 数组成员undefined null 转为空字符串
    ```
      Array.prototype.join.call('abc','-'); 
      //a-b-c
    ```
  * concat也可以将对象合并为数组
    ```
      [].concat.call({a:1},{b:2}); 
      [{a:1},{b:2}]
    ```
