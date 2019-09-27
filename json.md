# 记录学习JSON中的问题：
## JavaScript中的XMLHttpRequest与Web API
- `XML HttpRequest`负责在客户端发起请求 `Web API`负责在服务端返回响应
- `URL`全称是：“通用资源标识符 ”
- `Web API`通过HTTP服务进行交互的一组指令和标准（包括：创建，读取，更新，删除等）
- 一旦`JSON`被创建就可以请求（读取），更新，删除这个json了
- 异步操作通常指那些在幕后操作，不会中断主进程的操作,JavaScript中的异步操作指的是AJAX
- `XMLHttpRequest`
    ```javascript
    var xmlhttp = new XMLHttpRequest();
    xmlhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            var myObj = JSON.parse(this.responseText);

            //除了这一句其他的都是模板
            document.getElementById("demo").innerHTML = myObj.name;

        }
    };
    xmlhttp.open("GET", "/example/json/json_demo.txt", true);
    xmlhttp.send();
    ```
    - 是用来根据http协议来请求数据的
    - 允许我们通过访问站点进行数据交流的基础就是HTTP(超文本传输协议))
    - 只是JavaScript中的一个对象，但是他有实现请求数据的功能
    - 有许多属性来操作获取以及解析JSON
        - open send onreadstatechange readState status responseText
    - 同源策略：为了安全，浏览器对资源共享有限制，这个策略就是要求后台的请求仅仅能要求来自同一域名的资源
- 跨域资源共享：
    - 实现跨站资源共享的关键是服务器，只要服务端实现了CORS接口，就可以实现跨源共享,意味着加载资源必须在同一台服务器上
- JSON-P
    - 指的是带padding的json，利用了`<script>`标签不受同源策略的影响向不同域名的站点请求`JSON`，简单来说就是把请求json改成请求脚本文件，避开了同源策略
        ```javascript
        //创建一外联式的脚本，并且通过外部链接读取
        var script = document.creatElement("script");
        script.type = "text/javascript";
        script.src = "http://notarealdomain.com/animal.json";
        document.getElementByTagName("head")[0].appendChild(scrip）;
        ```
- 接收数据： 通过parse()方法对传输的数据进行解析，然后通过DOM实现显示
- 存储数据：把json文件转换成文本文件stringify()方法转换，用localStorage.setItem()方法保存，通过localStorage.getItem()从存储中读取数据；
- parse()函数：
    - 解析传输的JSON,参数1：json
    - 参数2：函数，函数有两个隐藏参数（key,value），可对传输的json进行检查，替换操作
    - json不允许有函数，如果要写，之后还要进行转换对象之后还要eval()解析函数
- stringify()函数
     - 会删除转换对象中所有函数，包括key value,正确的操作是在stringify之前就使用toString()提前转换函数，但是总归结底还是避免在json中使用函数
## json-php
- json常规用途是从Web服务器中读取数据，然后在网页中显示这些数据
- 通过PHP中的json_encode()可以使得php中对象转换为json便于传输，同样数组也可以被转换，使用json_decode()把json转化为PHP中的对象
    ```javascript
    <script>
    var xmlhttp = new XMLHttpRequest();

    xmlhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            myObj = JSON.parse(this.responseText);
            document.getElementById("demo").innerHTML = myObj.name;
        }
        };
    xmlhttp.open("GET", "/demo/demo_php_json_encode.php", true);
    //这里还是获取PHP文件？
    xmlhttp.send();
    </script>
    ```
- 请求时可以添加要求：
    ```javascript
    //对请求的内容加以限制
    obj = {"table":"customers", "limit":10};
    dbParam = JSON.stringify(obj);
    xmlhttp = new XMLHttpRequest();
    xmlhttp.onreadystatechange = function(){
        if(this.readystate ==4 && this.status == 200){
            document.getElementById("demo").innerHTML = this.responseText;
        }
    }
    xmlhttp.open("GET","demo_json_db.php?x=" + dbParam, true);
    //或者是xmlhttp.send("x=" + dbParam)
    xmlhttp.send(); //get不能send()不能有参数
    ```
- 向服务器发送数据：
    - 使用POST方法，指定正确的头部
    ```javascript
    <script>
    obj = { "table":"customers", "limit":10 };
    dbParam = JSON.stringify(obj);
    //以上是对于请求数据要求的模板

    xmlhttp = new XMLHttpRequest();
    xmlhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            myObj = JSON.parse(this.responseText);

            //以下是模板，也就是转换成对象之后你想干什么
            for (x in myObj) {
                txt += myObj[x].name + "<br>";
            }
            //以上是模板

            document.getElementById("demo").innerHTML = txt;
        }
    };
    xmlhttp.open("POST", "demo_json_db.php", true);
    xmlhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
    xmlhttp.send("x=" + dbParam);//这里可以对请求数据做出要求
    </script>
    ```