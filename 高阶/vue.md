## vue 实例：

#### 数据与方法：

-   只有数据创建时就存在的属性才是响应的，后面再添加的不算
-   `Object.freeze()`，这会阻止修改现有的属性，也意味着响应系统无法再追踪变化
-   前缀 `$` 把用户定义的属性与实例中的属性区分开

#### 实例生命周期钩子

-   vue 实例创建需要一系列初始化过程
    -   设置数据监听
    -   编译模板
    -   把实例挂载到 DOM
    -   数据变化时更新 DOM
-   在这个过程中会创建生命周期钩子的函数，给用户在不同阶段添加代码的机会
-   created 钩子在实例创建之后执行代码
-   mounted
-   updated
-   destroyed

## 模板语法

#### 插值

-   文本
    -   `v-once` 指令使得只能一次性插值，数据不变化时不会改变
-   原始 html
    -   为了输出真正的 html 文本，需要使用 `v-html` 指令
-   特性
    -   v-bind (同样可以先子组件中传递值)
-   使用 Javascript 表达式
    -   vue 对于数据提供表达式解析，仅限单个表达式以及三元运算符

#### 指令

-   参数
    -   一些指令能够接收参数，例如 `v-bind` 接收参数可以响应式更新 html 特性
    -   `v-on` 监听 DOM 事件
-   动态参数
    -   可以使用方括号括起来的 JavaScript 表达式作为指令的参数，也就是说属性以及属性值都可以使用表达式赋值
    -   这里的动态参数必须使用小写，因为浏览器会强制转换 attribute 为小写
-   修饰符
    -   修饰符是以半角语句`.`指名的特殊后缀，用于指出一个指令是否以特殊方式绑定

#### 缩写

-   `v-bind` => `:`
-   `- v-on` => `@`

## 计算属性和侦听器

#### 计算属性

-   computed

-   计算属性缓存 VS 方法
    -   methods
    -   计算属性是基于他们的响应式依赖缓存
    -   只有重新渲染才能，调用方法才会再次调用执行函数
-   计算属性 VS 侦听属性
    -   不需要对每个数据都侦听，代替使用计算属性，因为它是响应式的
-   计算属性的 setter
    -   计算属性默认只有 getter
    -   可以自定义 setter （当赋值的时候调用）

#### 侦听器

-   当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的
-   数据发生变化就会执行

## Class 与 Style 绑定

-   通过`v-bind`处理他们，只需要通过表达式计算出字符串结果就行了，表达式除了字符串之外还可以是对象或者数组

#### 绑定 HTML Class

-   对象语法
    -   传给`v-bind:class`对象，动态切换 class
    -   1
        -   显示的传给对象的属性和值
        -   class 中属性和属性的值取决于数据属性
        -   可以由多个动态的 class，也可以与普通的 class 属性共存
    -   2
        -   绑定的数据对象也可以直接在数据属性中
    -   3
        -   也可以直接返回计算属性（返回一个数组）
-   数组语法
    -   把数组显示传给`v-bind:class`，以此应用一个 class 列表
    -   和上面的 class 有点像
    -   列表中每一项可以使用三元运算符
-   用在组件上
    -   可以在定义组件的模板的根元素上添加 class
    -   使用自定义组件时添加 class 会添加不会重写

#### 绑定内联样式

-   对象语法
    -   `v-bind:style`,css 属性名可以使用驼峰式或者短横线分割
    -   显示绑定
    -   绑定样式对象会更清晰
    -   返回方法
-   数组对象
    -   显示绑定数组对象，其中数组对象的每一项都是样式对象
-   自动添加前缀
    -   vue.js 会自动侦测并添加相应的前缀
-   多重值
    -   可以为 style 绑定中的属性提供一个包含多个值的数组，常用于提供多个带前缀的值

## 条件渲染

#### v-if

-   `v-if` & `v-else-if` & `v-else`条件渲染这一块内容，如果 false 就渲染 else 中内容
-   在`<template>`元素上使用 `v-if`条件渲染分组
-   使用 key 管理可复用的元素（模板）

#### v-show

#### v-if VS v-show

-   v-if 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。
-   频繁切换最好使用 v-show,因为 v-if 切换开销太大

## 列表渲染

#### 用`v-for`把一个数组对应为一组元素

-   例子：
    -   `v-for = "item in items"`
    -   `v-for = "(item, index) in items"`
-   可以使用 of 代替 in 更接近 JavaScript 迭代器语法

#### 在`v-for`里使用对象

-   例子：
    -   `v-for = "value in object"`
    -   `v-for = "(value, name) in object"`
    -   `v-for = "(value, name, index) in object"`

#### 维护状态

-   为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 key 属性

#### 数组更新检测

-   变异方法
    -   Vue 将被侦听的数组的变异方法进行了包裹，所以它们也将会触发视图更新。
-   替换数组
    -   变异方法，顾名思义，会改变调用了这些方法的原始数组。相比之下，也有非变异方法，例如 filter()、concat() 和 slice() 。它们不会改变原始数组，而总是返回一个新数组。
-   注意事项
    -   由于 JavaScript 限制，问题：
        -   不能利用索引直接设置一个数组
        -   不能直接修改数组的长度
    -   解决方案
        -   Vue.set(vm.items, indexOfItem, newValue)
        -   vm.items.splice(indexOfItem, 1, newValue)
        -   vm.items.splice(newLength)

#### 对象变更检测注意事项

-   Vue 不能检测对象属性的添加或删除
- 解决方法：
    - Vue.set(object, propertyName, value) 方法向嵌套对象添加响应式属性
    - vm.$set(vm.userProfile, 'age', 27)
    - 
        ```javascript
        vm.userProfile = Object.assign({},                   vm.userProfile, {
                age: 27,
                favoriteColor: 'Vue Green'
        })
        ```
#### 显示过滤/排序后的结果
- 在计算属性中返回经过处理的结果
- 直接使用方法的返回值
#### 在v-for里使用值范围
- 接收整数
#### 在`<template>`上使用v-for
- 可以渲染包含多个元素的内容

## 事件处理
#### 监听事件
- 可以使用v-on监听DOM事件
#### 事件处理方法
- 可以是JavaScript表达式，也可以是方法中的函数（逻辑复杂时）
#### 内联处理器中的方法
- 传递参数的函数？
#### 事件修饰符
- 用事件修饰符替代原生的事件处理程序
- 事件修饰符
    - .stop
        - 阻止单击事件继续传播
    - .prevent
        - 提交事件不重载页面
    - .capture
        - 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理
    - .self
    - .once
    - .passive
## 表单输入绑定
- `v-model`在`<input>`, `textarea>`, `<select>`元素上创建双向数据绑定
- 应用
    - 单选按钮z
    - 复选按钮
    - 选择框
    - 值绑定
- 修饰符
    - `.lazy`转变为change事件时同步
    -  `.number`自动将用户输入值转化为数值类型
    - `.trim`
- 默认参数和显式参数`$event`
## 组件基础
- 传递数据（单向数据流）
    - 通过组件属性传递数据
    - 子组件通过props数组接收传递数据
- 传递事件
    - `$emit()`向父组件传递事件，也可以同时传递参数
    - 父组件通过`v-on:`接收事件，通过$event访问参数，或者在方法中隐式访问参数
# 深入了解组件
## 组件注册
- 模块系统
    - 基础组件的自动化全局注册
## prop
- html中使用短横线方法传递数据到组件后需要使用驼峰命名法接收数据，因为html对大小写不敏感，所有的大写都会转化成小写
- 类型：
    - 数组：字符串接收
    - 对象： 键值对方式指定类型
- 单向数据流
    - prop传递的数据最好使用本地data属性存储作为初始值
- 禁止组件根元素继承特性
    - `inheritAttrs : false` 传入新特性而不修改原来的
## 自定义事件
- 事件名
    - html对大小写不敏感，所以最好使用kebab-case命名事件名
- 自定义`v-model`
- 在自定义组件上实现`v-model`
    - model对象中使用prop和event，一个用来指定 双向绑定 绑定的数据，event子组件通知父组件什么时候更新数据
- 将原生事件绑定到组件上
- `.sync` ：子组件向父组件绑定的语法糖
## 插槽
- `<slot>`元素作为承载分发内容的出口
- 如果组件中没有插槽，则任何传入它的内容都会被抛弃
- 具名插槽
    - `<slot>`具有name属性
    - 插槽内容具有`slot`属性
    - 没有slot属性的元素都会同意输出到未命名插槽上（默认插槽
- 插槽的默认内容：
    - 如果父组件为插槽提供内容，默认的插槽内容就会被替换
- 编译作用域
    - 父组件模板的所有东西都会在父级作用域内编译；子组件模板的所有东西都会在子级作用域内编译
- 
## 过滤器
- 用在插值表达式或者v-bind表达式
- 再`filters`实例对象中定义过滤器函数
- 或者通过`Vue.filter`定义全局过滤器
- 默认第一个参数为表达式的值
- 过滤器可以串联，前一个过滤的值成为下一个过滤器默认参数
- 如果过滤器显式的定义参数，那么默认前一个值仍然是第一个参数，显式定义的参数会往后移

## 单文件组件
- style 中加入scoped 样式只会作用与当前的文件

## 文件介绍： 
- `babelrc`es6转换配置

## 路由
- 什么时候使用路由？： 当使用单页面应用
- 