## 记录学习JSON中的问题：
### JavaScript中的XMLHttpRequest与Web API
- `XML HttpRequest`负责在客户端发起请求 `Web API`负责在服务端返回响应
- `URL`全称是：“通用资源标识符 ”
- `Web API`通过HTTP服务进行交互的一组指令和标准（包括：创建，读取，更新，删除等）
- 一旦`JSON`被创建就可以请求（读取），更新，删除这个json了
- 异步操作通常指那些在幕后操作，不会中断主进程的操作,JavaScript中的异步操作指的是AJAX  
- `XMLHttpRequest`
    - 是用来根据http协议来请求数据的
    - 允许我们通过访问站点进行数据交流的基础就是HTTP(超文本传输协议))
    - 只是JavaScript中的一个对象，但是他有实现请求数据的功能
    - 有许多属性来操作获取以及解析JSON
        - open send onreadstatechange readState status responseText
    - 同源策略：为了安全，浏览器对资源共享有限制，这个策略就是要求后台的请求仅仅能要求来自同一域名的资源
- 跨域资源共享：
    