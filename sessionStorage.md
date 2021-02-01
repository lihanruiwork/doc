* 在浏览器端储存数据
* sessionStorage:保存的数据用于浏览器的一次会话，会话结束窗口关闭，sessionStorage保存的数据就被清空。
* localStorage:保存的数据长期存在。
* 比cookie能动用大得多的存储空间
* Cookie 4KB
* 他俩 根据浏览器不同 2.5MB-10MB
* 他俩的方法都一样：
  * 以键值对形式存在
  * setItem(key,value)
  * getItem(key)
  * removeItem(key)：清除某个键名对应的数据
  * clear()：清除所有保存的数据
* 遍历操作：
  * localStorage.key(数字索引)
  * localStorage.length
* storage事件：
  * window.addEventListener(“storage”,处理函数)
  * event事件四个属性：
    * key oldValue newValue url
  * 该事件不在导致数据变化的当前页面触发。
  * 如果浏览器同时打开一个域名下面的多个页面，其中一个页面改变
  * sessionStorage或localStorage的数据时，其他所有页面的storage事件会被触发，而原始页面不会触发。可以通过这种机制，实现多个窗口之间的通信。
