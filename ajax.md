# Ajax
* XMLHttpRequest对象用来在浏览器与服务器之间传送数据
* XMLHttpRequest对象的属性：
  * readyState：XMLHttpRequest请求当前所处的状态
    * 0 open之前
    * 1 open之后 send之前 
    * 2 send之后 头信息和状态码已经收到 
    * 3 正在接收body部分的数据
    * 4 数据完全接收，或者本次失败了。
  * response数据体 
  * responseType 字符串text document json blob arraybuffer
  * overrideMimeType()
  * responseText 字符串 json
  * responseXML document
  * status HTTP状态码
    * readyState == 4 status >= 200 status < 300 status == 304
  * statusText
    * 整个状态信息 200 OK
  * timeout
    * 多少毫秒后，就会自动终止
  * xhr.ontimeout = function () {}
  * withCredentials
    * 跨域请求是否发送Cookie
* XMLHttpRequest对象的方法：
  * abort()
    * 终止已经发出的HTTP请求。
  * getAllResponseHeaders()
  * getResponseHeader()
  * open(五个参数)
    * method：HTTP动词 GET POST PUT DELETE
    * url async请求是否异步
  * send()
    * 实际发出HTTP请求
* 发送二进制数据，用ArrayBufferView或Blob,使得通过Ajax上传文件成为可能。
* FormData 构造表单数据。
* new FormData(form节点);
  * 模拟File控件，进行文件上传 formData.append(file.name, file);
* setRequestHeader()
  * open()后 send()前
* XMLHttpRequest实例的事件：
  * 事件监听接口:
    * onloadstart 请求发出
    * onloadend 请求完成，不管成果或失败
    * onload 请求成功完成
    * onerror 请求失败
    * onabort 请求被中止，比如用户调用了abort()方法
    * ontimeout 用户指定的时限到期，请求还未完成
    * readyStateChange readyState值每次变化或xhr.abort()
  * progress
    * 不断返回上传的进度: xhr.upload.onprogress
    * 不断返回下载的进度: xhr.onprogress
    ```
      <progress>
      xhr.upload.onprogress=function(){}
      lengthComputable  loaded  total
      progress节点.value=loaded/total*100
    ```
