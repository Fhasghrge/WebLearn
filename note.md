##NOTE
- 事件的三要素： 事件源 + 事件 + 事件驱动程序
- **为什么用getElementsByClassName不能产生事件驱动程序？**:需要使用序号，因为得    到的是数组
- 对于函数，fn代表整个函数，而fn()代表函数的返回值
- 在js代码中属性名使用camel，属性值使用双引号括起来
- DOM操作文档上元素的API
- BOM操作浏览器的API
- **创建标签怎么确定标签所放位置？**：创建就是为了给插入、删除等事件做准备的
-  文本是标签的第一个子节点
- 使用js获取内联样式之外的样式
    ```html
    <script>

        var div1 = document.getElementsByTagName("div")[0];

        console.log(getStyle(div1, "width"));
        console.log(getStyle(div1, "padding"));
        console.log(getStyle(div1, "background-color"));

    //兼容方法获取元素样式
        function getStyle(ele, attr) {
            if (window.getComputedStyle) {
                return window.getComputedStyle(ele, null)[attr];
            }
            return ele.currentStyle[attr];
        }
        
    </script>
    ```
- 绑定事件(事件捕获)有两种方法：`.` `addElementListener`(事件监听器)不会发生层叠
- 事件对象 ： 在触发事件时自动生成的`event`包含了关于鼠标的信息
- 事件捕获顺序：`window > document > html > body > 祖先 > 父亲 > 儿子`也就是说会按照这个顺序处理事件驱动程序
- 事件冒泡，当一个元素的事件触发时，其父亲祖先都会触发事件，知道DOM树的最上层
- 事件冒泡的顺序与事件捕获的顺序刚好相反 阻止冒泡：`event.stopPropagation() || event.canselBubble = true`
- **事件委托我还没学**
- BOM:`opean close location history navigator`
- 构造函数： 使用`new`关键字和函数快速批量生产对象
- **alert 与 throw区别？**
- 在文档加载完成之后使用`document.write()`,会覆盖原来文档
- 阻止事冒泡： 就是防止在点击最底层元素之后其祖先元素不断地接收响应
- 计时器：`setInterval(function, time)  setTimeOut()`分别通过设置事件间隔和
  暂停事件来不断控制函数进行，而对应的停止是`setInterval() clearTimeOut()`
- `window.history`包含浏览器历史url的集合`history.back()||forward()||go()`
- `loaction`是关于当前页面url的对象，能够获得url的一些属性的对象
- `screen`获得关于用户当前屏幕相关的信息，例如宽高
