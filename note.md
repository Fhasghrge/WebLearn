# NOTE
## 语法知识的学习（来源于Github教程）
- 事件的三要素： 事件源 + 事件 + 事件驱动程序
- **为什么用getElementsByClassName不能产生事件驱动程序？**:需要使用序号，因为得    到的是数组
- 对于函数，fn代表整个函数，而fn()代表函数的返回值
- 在js代码中属性名使用camel，属性值使用双引号括起来，属性名也是使用双引号，防止不
  规范的写法
- DOM操作文档上元素的API
- BOM操作浏览器的API
- DOM：
    - **创建标签怎么确定标签所放位置？**：
        - 创建就是为了给插入、删除等事件做准备的
    -  文本是标签的第一个子节点，在DOM树中显示
    - 使用 js 获取内联样式之外的样式（外部样式表）
        ```html
        <script>

            var div1 = document.getElementsByTagName("div")[0];

            console.log(getStyle(div1, "width"));
            console.log(getStyle(div1, "padding"));
            console.log(getStyle(div1, "background-color"));

        //兼容方法获取元素样式，只是通过函数活动，不具有通用性？
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
    - **事件委托我还没学？**
- BOM:`opean close location history navigator`
    - 构造函数： 使用`new`关键字和函数快速批量生产对象
    - **alert 与 throw区别？**
    - 在文档加载完成之后使用`document.write()`,会覆盖原来文档
    - 阻止事冒泡： 就是防止在点击最底层元素之后其祖先元素不断地接收响应
    - 计时器：`setInterval(function, time)  setTimeOut()`分别通过设置事件间隔和
    暂停事件来不断控制函数进行，而对应的停止是`stopInterval() clearTimeOut()`
    - `window.history`包含浏览器历史url的集合`history.back()||forward()||go()`
    - `loaction`是关于当前页面url的对象，能够获得url的一些属性的对象
    - `screen`获得关于用户当前屏幕相关的信息，例如宽高
- **构造函数中prototype什么意思？**
    - 使用js模拟类的实现
    ```html
    <script>
        //使用js模拟类的实现
        function Person(){  //定义一个空的构造函数

        }
        Person.prototype = {  //原生态，也就是类？反正就是这么用的
            name: "zhangshuang",
            age: 19,
            eat: function(){
                alert("chizhe")
            }
        var zhang =new Person(); //构造函数使用
        }
    </script>
    ```
    - 继承：
    ```html
    <script>
        function Person(){

        }
        Person.prototype.say = function(){
            alert("oooo");
        }
        function Student(){

        }
        Student.prototype = new Person();  //继承的过程，把原生类传递过去
        var s = new Student();
        Student.prototype.say = function(){     //对继承来的父类进行复写
            alert("student-hello");
        }
    </script>
    ```

## 记录学习JavaScript的笔记（来源于JavaScript语法精髓）：
- **原生链是什么？**好像往下看看也就简单理解了？
- **什么是反射我也没懂？**
- 函数也是一个对象，所以他也有原型
- 什么是匿名函数`anonymous`：
    ```html
    <script>
    var zhang = function(){ //通过匿名函数以函数返回值的形式赋值来构造函数
        alert("加油呀");
    }
    </script>
    ```
- **什么是闭包？**
    - 内部函数仅仅在内部可以使用
    - 闭包由函数以及创建函数时词法环境决定的，这个环境包括了闭包创建时所能访问的全部
    局部变量(除了`this`和`arguments`)
    - 通过函数字面量创建的函数包含了一个连接函数上下文的连接，**通过匿名函数就不行？**
    - **内部函数的生命周期比外部函数还长？**
    - 函数可以访问在被创建时的上下环境，这种特性被称为`闭包`
- 调用运算符是任何一个产生函数值的表达式之后的一对圆括号
- 函数的实际参数过多过少都没有关系，过多会被忽略，过少会被`undeined`代替
- JavaScript是`基于原型继承`的语言，而大多数主流语言是`基于类`的语言，然后**模拟了所谓的继承？**
- 使用`new`背地里会创建一个连接到函数`prototype`的新对象，同时`this`也会被绑定到这个新对象
- 函数原型也就是函数的一部分成员，可以使用闭包，只不过它可以被所有继承的子对象使用
- 如果一个函数创建的目的就是配合`new`使用，那么这个函数被称为构造器函数，构造器函数默认使用字母大写的函数名
- `apply`传递参数数组给调用函数，两个参数 : `this` 和 `array` **fuck这是啥？**
- `arguments`数组，隐藏的函数参数数组，它可以调用函数在声明时所有的参数列表，包括多余的参数，这使得编写一个无需指定函数参数个数的函数成为可能，`arguments`不是真正的数组，只是一个类似于数组的对象
- 函数如果没有`return`那么返回`undefined`
- 异常处理机制：
    - `throw`中断函数的执行，抛出一个`exception`,包含属性`name`和`message`，可以自己添加属性
    - `exception`可以通过`try`,`catch`语句传递：`try`中抛出异常，控制权就传递到了`catch`中,通过给`catch()`定义形式参数传递`exception`
- JavaScript允许给基本类型扩充功能：即通过原生链`prototype`的功能扩充
- **正则表达式只是简单的表达本来是函数完成的功能？**
- **`for in`就是狗屁？**
- 递归非常高效的处理树型结构
- JavaScript不支持尾递归（循环递归），深度递归会导致堆栈内存溢出而运行失败
- 回调：同步请求使得网页在请求之后进入假死状体，使用异步请求会在请求到达服务器之后就能通过回调函数产生响应（**这就是骗人的响应？**）

## 扎奇巴傻
- 路由： 可以理解为url中网站域名后面的东西
