-   `page.json`只能覆盖`app.json`中 window 对象的内容
-   console.dir()打印对象，以树的方式呈现在控制台
-   getApp()获取全局程序对象
-   getCurrentPages()获取当前页面的调用栈(数组最后一个元素就是当前页面)
-   wx => 提供核心 API 的调用对象
-   模块（CommonJs 规范）
    -   导出模块
        ```javascript
        function say(msg) {
            console.log('hello' + msg);
        }
        module.exports = {
            say: say
        };
        ```
    -   载入模块
        ```javascript
        const foo = require('../files/foo.js);
        //获取上面抛出的对象
        foo.say("World");
        //Hello World
        ```
-   wx 绑定属性也是用{{}}，其中可以放字面量和简单的逻辑运算符，以及存放 boolean 类型的值以避免歧义

#### 列表渲染

-   wx 的列表渲染和 vue 不太相同
    ```javascript
    <view wx:for = "{{aray}}">
    <!-- 可以循环数组或者对象 -->
        <checkbox chencked = "{{item.completed}}"></checkbox>
        <text>{{item.name}}</text>
    </view>
    ```
-   如果 item 与数据又冲突可以使用
    -   `wx:for-item = "qqq"`
-   index 与 item 又类似的用法

#### 事件处理：

-   bindtap == onclick
-   catchtap == 阻止冒泡的 onclick

-   bind+事件名 == 不能阻止冒泡的监听器
-   catch+事件名 == 阻止冒泡的监听器

-   事件处理参数不能传递参数，只能通过元素的 dataset 属性获取所需要的参数，
    ```javascript
    function tap(e) {
        console.log(e.target.dataset.name);
        //dataset指的是元素属性中所有以`data-`前缀开头的属性所形成的集合
    }
    ```
#### 数据流
- 小程序没有实现双向数据绑定
- 小程序的数据不是响应式的
- 实现双向数据绑定
    - 逻辑层 => 界面层 ： 1、使用数据绑定（大胡子，但是不能实现响应式）；2、使用this.setData({})通知事项更新
    - 界面层 => 逻辑层 ： 通过实践处理函数:侦听器`bindinput`事件处理函数的event对象e.detail.vlaue如此获取界面上的数据