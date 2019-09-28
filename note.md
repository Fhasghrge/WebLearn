# NOTE  (JavaScript)
## 语法知识的学习（来源于Github教程）
- 大致概要：
    - 在js代码中属性名使用camel，属性值使用双引号括起来，属性名也是使用双引号，防止不规范的写法，导致数据交换的时候导致不兼容
    ---
- DOM：
    - 获取节点：
        - `var a = document.getELementById(" ")`
        - `document.getElementById(" ")`
        - 通过访问关系获取节点
    - 节点操作：
        - 创建节点：
            - **创建标签怎么确定标签所放位置？**：
            - 创建就是为了给插入、删除等事件做准备的，暂时不用指定位置
            - `var a = document.createElement(" ")   `
        - 插入节点：`appendChild(), insertBefore()`
        - 删除节点： `removeChild()`
        - 复制节点： `cloneNode()` **我不知道怎么使用**
        - 获取节点的属性：
            - `. `
            - `[]`
            - `getAttribute("属性名")`
        - 设置节点属性：
            - `. `
            - `setAttribute("属性名","属性值")`
        - 删除节点属性：`removeAttribute("AttrName")`
    - 对象属性（节点属性）：
        - `value` `innerHTML` `innerText`
    - nodeType: 用于修改元素内容时判断类型的？
    -  `window`属性：
        - `onload`
    - **绑定事件：**
        - `.`
        - 监听器`addElemetListener(事件，驱动程序，默认false冒泡)`
        - 事件对象： 在驱动程序中会隐藏一个参数对象event  **隐藏对象就是window下的全局对象？**,其实不算隐藏的属性，window下的对象在哪里都可以用`event`下面有很多属性，很有用

    - 文本是标签的第一个子节点，在DOM树中显示
    - *使用 js 获取内联样式之外的样式（外部样式表）*
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
    - 事件对象 ： 在触发事件时自动生成的`event`包含了关于鼠标的信息
    - 事件捕获顺序：`window > document > html > body > 祖先 > 父亲 > 儿子`也就是说会按照这个顺序处理事件驱动程序
    - 事件冒泡，当一个元素的事件触发时，其父亲祖先都会触发事件，直到DOM树的最上层
    - 事件冒泡的顺序与事件捕获的顺序刚好相反 阻止冒泡：`event.stopPropagation() || event.canselBubble = true`
    - **事件委托我还没学？**
    - 以函数调用时，`this`指的是`window`，以方法形式调用时，`this`指的是方法的对象
    ---
- BOM:`opean close location history navigator`
    - `window`是顶级对象，所有的对象都在这里
        - alert()
        - open(url, target,param)param中有很多参数**用json写的？**和json的open不一样，这里是打开新的页面
        - close()
    - `window.history`包含浏览器历史url的集合
        - `back()`
        - `forward()`
        - `go()`
    - `loaction`是关于当前页面url的对象，能够获得url的一些属性的对象以及方法
        - **有很多属性，方法我都没有看**
    - `navigator`获取客户端的信息
    - `screen`获得关于用户当前屏幕相关的信息，例如宽高
        - 属性：userAgent platform
    - DOM是BOM中很大的对象`document`和上面的几个对象都是同一级别的
    - 构造函数： 使用`new`关键字和函数快速批量生产对象
    - **alert 与 throw区别？**
    - 在文档加载完成之后使用`document.write()`,会覆盖原来文档
    - 阻止事件冒泡： 就是防止在点击最底层元素之后其祖先元素不断地接收响应
    - 计时器：`setInterval(function, time)  setTimeOut()`分别通过设置事件间隔和
    暂停事件来不断控制函数进行，而对应的停止是`stopInterval() clearTimeOut()`
    - **构造函数中prototype什么意思？**
        原型链
    - 使用js模拟类的实现
        ```html
        <script>
            //使用js模拟类的实现
            function Person(){  //定义一个空的构造函数

            }
            Person.prototype = {  //原型链，也就是类？反正就是这么用的
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
            Student.prototype = new Person();  //继承的过程，把原型链传递过去
            var s = new Student();
            Student.prototype.say = function(){     //对继承来的父类进行复写
                alert("student-hello");
            }
        </script>
        ```
- 原型链
    - 构造函数
        - 实例：
            ```javascript
                function Foo(name, age) {
                    this.name = name;
                    this.age = age;
                    //retrun this;   //默认有这一行。new一个构造函数，返回一个对象

                }

                var fn1 = new Foo('smyhvae', 26);
                var fn2 = new Foo('vae',30);    //new 多个实例对象
            ```
        - **当使用`new`之后，`this`先变成一个空对象，然后通过`this.name = name`赋值？**
        - `var a = {}`实际是`var a = new Object(){}`
        - `var a = []`实际是`var a = new Array(){}`
        - `function Foo(){...}`实际是`var Foo = new function(){...}`
        - `instanceof`用来判断变量是否是构造函数
    - 原型规则：
        - 所有引用类型都有对象特性，都可以自由扩展属性
        - 所有的引用类型都有`_proto_`属性，其属性值是一个对象，含义是隐式原型
        - 所有函数（非对象，数组）都有`prototype`属性，含义是显示原型
        - 所有引用类型的`_proto_`都指向他的构造函数的`prototype`
        - 获取一个对象的属性时，如果对象本身没有这个属性，那就如他的`_proto_`找
    - `for in`能够遍历对象的属性，但是默认只能遍历本身属性，不包含原型
- `callback`时函数的参数，如果参数存在则执行，如果不存在就不执行
- 创建对象的方法：
    - 构建`object`空对象，然后逐渐添加属性
    - 使用对象字面量
    - 工厂模式 把对象返回回来就行了，并不需要使用new,使用的时返回值
    - 自定义构造函数，使用`new`,不需要使用返回值
- 继承的几种方式：
    - 原型链继承：通过把父对象（构造函数形式）添加到子对象的`prototype`
    - 借用函数构造继承：在子对象中使用`Father.call(this,参数1,参数2)`
    就是相当于把父对象的原型复制到子对象中，但是只能继承父对象，不能继承父对象的原型
- 浅拷贝和深拷贝：主要针对的时`object`和`array`的复杂数据类型，
- **变量提升我还不明白？**
- 函数声明和函数表达式：
    - 举个栗子
        ```javascript
        //函数声明
        function Foo(){
            console.log("name")
        }
        //函数表达式
        var Foo = function(){
            console.log("name")
        }
        ```
    - 函数表达式会在完全赋值之后才会调用，也就是函数声明可以在任何地方被提升，但是函数表达式只有在赋值以后才能使用
    - 全局执行流程:var全局变量不赋值， function函数声明赋值，this属性声明赋值
    - 函数执行流程（也称上下文）：
        - 预处理：除了var布局变量不赋值以外，其他都可以赋值
        - 执行函数
- 构造函数的实质：
    ```javascript
    function Foo(name){
        //this = {};
        this.name = name;
        //return this;
    }
    ```
- 已经没有块作用域了版本修订的时候删除了，，但是如果使用`let`任然会有块级作用域
- var定义的变量作用域在活动对象上，因此有闭包的存在，可以被接收，let定义的变量，作用域在代码块中
- 作用域链：如果有多个嵌套的函数，就会形成作用域链
- `call & apply`都用来改变`this`的指向第一个参数都是对象，显式绑定`this`，后面跟着实参，`apply`是需要使用数组进行封装实参的，实际上这两个方法就是为了对函数进行内部对象变相的构造以及传参？
---
## 进阶JavaScript的笔记（来源于JavaScript语法精髓）：
- **什么是反射我也没懂？**
- 函数也是一个对象，所以他也有原型
- 什么是匿名函数`anonymous`：
    ```html
    <script>//函数表达式？
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
    - 常见的闭包：
        - 一个函数作为另一个函数的返回值
        - 闭包中的变量保存在内存中，闭包由多大，取决于外部函数调用几次
        - 将一个函数作为实参传给另一个函数使用**foreach使用？**
        - 闭包一直存在的原因是：变量一直被其他函数不断接收了，原来的函数或许已经不存在了但是之前函数中的变量，内存被接收了
        - 不能通过外部函数访问内部变量，但是可以通过闭包操控它（操控的手段都在闭包中，已经定义好的）
        - 闭包什么时候死亡？当嵌套函数被垃圾回收时，`f = null`**但是！内存没有回收啊？？**上面就是回收了，但是这就是缺点，如果不能及时回收占用内存事件过长，回到是内存泄漏
        - 闭包的作用，通过把数据私有化，并且只提供暴露的方法和函数来实现功能
        - 可以通过对象字面量的形式包裹，暴露多个函数
        - 可以通过直接把函数传给`window`作为对象方法
    - 内存溢出：运行的内存超过了剩余的内存
    - 内存泄漏：占用内存没有及时释放
        - 常见的内存泄漏：意外全局变量，没有及时回收计时器或回调函数， 闭包

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
- 模块：**我并没有理解**
    - 是一个提供接口但是隐藏状态和实现函数的对象
    - 通过模块可以摒弃使用全局变
- 级联：允许我们在一条语句中调用一个对象的多个方法

## 扎奇巴傻
- 路由： 可以理解为url中网站域名后面的东西
