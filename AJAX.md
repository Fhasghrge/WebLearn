# AJAX_NOTE
- 不是一种语言，只是XMLHttpRequest和JavaScript和DOM的组合
- 同样可以使用XML传输数据,但是使用json更为常见
- 一切尽在后台，不重新加载页面，但是更新了网页
- 属性：
    - `open(method,url,async)`请求方法，地址，是否异步
        - post 比 get 更加快捷简单，健壮安全
        - url是一个地址，一个服务器上上面的文件
    - `send()` used for GET
    - `send(string)` used for POST
    ```javascript
    <script>
    function loadXMLDoc() { //通过DOM绑定模板XMLHttpRequest函数
        var xmlhttp = new XMLHttpRequest();
        xmlhttp.onreadystatechange = function() {
            if (this.readyState == 4 && this.status == 200) {
                myFunction(this);
            }
        };
        xmlhttp.open("GET", "cd_catalog.xml", true);
        xmlhttp.send();
    }

    function myFunction(xml) {//真正实现的逻辑函数，也就是DOM操作
        var i;
        var xmlDoc = xml.responseXML;
        var table="<tr><th>Artist</th><th>Title</th></tr>";
        var x = xmlDoc.getElementsByTagName("CD");
        for (i = 0; i <x.length; i++) {
            table += "<tr><td>" +
            x[i].getElementsByTagName("ARTIST")[0].childNodes[0]
            .nodeValue +
            "</td><td>" +
            x[i].getElementsByTagName("TITLE")[0].childNodes[0]
            .nodeValue +
            "</td></tr>";
        }
        document.getElementById("demo").innerHTML = table;
    }
    </script>
    ```
- 还可以从txt文件中获取数据
- 通过回调函数进行访问，彻底的模板化了：
    ```javascript
    function loadDoc(url, cFunction) { //url在进行事件监听的时候就传入
    var xhttp;
    xhttp=new XMLHttpRequest();
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            cFunction(this);
        }
    };
    xhttp.open("GET", url, true);
    xhttp.send();
    }

    function myFunction(xhttp) {//回调函数使得函数功能结构更加清晰
        document.getElementById("demo").innerHTML =
        xhttp.responseText;
    }
    ```