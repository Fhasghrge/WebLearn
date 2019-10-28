<!-- 来自阮一峰的ECMAScript入门 -->
## let & const
- for循环中，设置循环变量实际上是在父作用域，循环体内部是在子作用域
- 凡是在let之前使用没有声明的变量都会报错，即使是多次声明变量也是以最后一个声明为准，这就是temporal dead zone
- 变量提升只是声明被提升了，赋值没有提升，使用let关键字可以解决这个问题 => 没有提升
- ES5只有全局作用域和函数作用域，而且if 和 for 语句中的变量容易泄露成全局变量
- 块级作用域的出现使得**匿名立即执行函数表达式**没有必要了，以前这个就是为了防止全局变量过多造成不必要的麻烦
- ES6允许在块级作用域中声明函数
- const 在声明时就必须赋值
- ES6声明的变量let const class 从此与顶层对象脱钩
    ```javascript
    var a = 1;
    window.a //1
    let b = 2;
    window.b//undefined
    ```
## 解构赋值
#### 前言：
- 只要等号两边模式相同，右边的值就会赋值给相应的变量
- 如果等号右边不是可以遍历的结构就不会解构，或者说等号右边转换为对象之后不具有Iterator接口，可以遍历的结构：数组，字符串，Set，NodeList对象
#### 1 数组结构赋值
- [a,b] = [1,2];
- [a, b, c] = "123";
- 默认值，放在等号前面
- 表达式具有惰性求值的，只有用到才会求值
#### 2 对象的结构赋值
- ({a, b} = {a : 1, b : 2});**对象赋值进行匹配**
- 对象的解构赋值：
    - 采用的是对象的属性名对应的赋值，与次序无关
    - 真正复制的是后面的值，而不是前面的属性，前面的属性只是用来匹配
    - 可以把对象中的方法对应到自定义中，很方便
        ```javascript
        let {cos, sin, log} = Math;
        console.log(cos(Math.PI))
        ```
    - 也可以有默认值，没有解构赋值的返回时`undefined`，null即使是空指针也是*对象*
#### 注意：
- 对于一个已经声明的变量进行解构赋值要小心，因为大括号放在行首容易被JavaScript解释为代码块，这是可以使用`()`包裹起来解决这个问题
- 数组的本质时特殊的对象，所以可以用数组对对象属性进行赋值
#### 3 字符串的解构解析
- 字符串可以转化成类似于数组的对象
#### 4 数值和布尔值的解构赋值
- 如果等号右边是数值或者布尔值，则转换为对象
#### 5 函数参数的解构赋值
- 直接向函数参数里面传入可以在传入参数的一刻转换成函数常规参数
- 函数的参数也可以有默认值
    ```javascript
    function move({x = 0, y = 0} = {}) {
        return [x, y];
    }
    move({x: 3, y: 8}); // [3, 8]
    move({x: 3}); // [3, 0]
    move({}); // [0, 0]
    move(); // [0, 0]
    ```
- undefined会触发函数参数的默认值
#### 6 圆括号问题
- 不能使用圆括号的情况
    - 变量声明语句
    - 函数参数
    - 赋值语句的模式
- 可以使用圆括号的情况
    - 赋值语句和非模式语句 
#### **7 用途**
- 交换变量的值
- 函数中返回多个值
- 函数参数定义
- **提取JSON数据**（通过属性名快速提取数据）
- 函数参数的默认值
- **遍历Map结构**
    - 任何部署了迭代器接口的对象，都可以通过`for...of`循环遍历
    ```javascript
    for(let [key,value] of map){
        //dosomething
    }
    for(let [key] of map){

    }
    for(let [,value] of map){

    }
    ```
- 输入模块的指定方法
## 字符串扩展
- 字符的Unicode表示法：
    - 允许\uxxxx表示一个字符
    - 超出
    - 用大括号
- 字符串的遍历器接口
    - 为字符串添加了遍历接口
    - 能识别传统for循环无法识别的码点
- 直接输入U+2028 和 U+2029
    - JavaScript 字符串允许直接输入字符，以及输入字符的转义形式。
    - 字符串中不能包含反斜杠，一定要转义为\\或者\u005c
- JSON.stringify()的改造
- 字符串模板
```javascript
let name = "zhangShuang";
let age = 19;
let zhang = `我叫${name},我今年${age}岁了`
console.log(zhang)//我叫zhangShuang,我今年19岁了 
```
```javascript
let zhang = "shuang"
console.log(zhang.includes("ang"))
console.log(zhang.startsWith("shua"))
console.log(zhang.endsWith("ang"))
console.log(zhang.repeat(5));
```
- 实例：模板编译

## rest参数
    ```javascript
    function sum(...c){
    let m = 0;
    for(let i = 0; i < c.length; i++ ){
        m += c[i];
    }
    console.log(m);
    }
    sum(1,2,3,4,5,6,4,55);//80
    ```
    ```javascript
    let a, b;
    [a, ...b] = [1,2,3,4,4,5,67,8,99];
    console.log(a, b) //1 [ 2, 3, 4, 4, 5, 67, 8, 99 ] 
    ```
    ```javascript
    let a, b;
    [a, ...b] = "1234567890"
    console.log(a, b)//1 [ '2', '3', '4', '5', '6', '7', '8', '9', '0' ] 
    ```
- 对象扩展：
    ```javascript
    let a = 1;
    let b = 2;
    let c = {a,b}//相当于let c = {a : a, b : b}
    console.log(c)
    ```
    ```javascript
    let zhang = {
        sayHello(){ //对象中方法的简写
            console.log("hello world");
        },
    }
    zhang.sayHello();//hello world
    ```
    ```javascript
    let name = "zhang"
    let shuang = {
        [name] : "baba",//用[]包括key值简写引用
    }
    console.log(shuang)//{ zhang: 'baba' }
    ```
- 箭头函数：
    ```javascript
    let zhang = num => num * 2
    console.log(zhang(5))//10
    ```
    ```javascript
    let zhang = (num1, num2) => {   //函数的作用域绑定在当前块中
    return num1 * num2
    }
    console.log( zhang(3, 4) )//12
    ```
    - 如果直接返回一个对象，需要把对象用（）括起来，以免产生歧义
    - 在vue中某些地方不支持箭头函数
- 数值：
     - isFinite判断数值是否有界
     ```javascript
    console.log(Number.isInteger("d"))//false
    console.log(Math.cbrt(8))//2
    console.log(Number.MAX_SAFE_INTEGER)//9007199254740991
    console.log(Number.MIN_SAFE_INTEGER)//-9007199254740991
    console.log(Number.isSafeInteger(4))//true
    console.log(Math.trunc(9.9))//9返回整数部分
    console.log(Math.sign(10))//1 判断是正数负数还是零
     ```
- set & map
    - set
         ```javascript
        let set = new Set()
        set.add(3)
        set.add("sdfdf")
        console.log(set)
        console.log(set.size)   //和数组的length不同
        let arr = [1,2,3,4,5,6,7,8,9,1,2,3,4]
        let set2 = new Set(arr)
        console.log(set2)
        let zhang = Array.from(set2)//通常转换为数组比较方便，set就被当作去重的工具了
        console.log(zhang)
        console.log(set2.has(3))
        set2.delete(3)
        console.log(set2.has(3))
        set2.clear()
        console.log(set2)
        let set3 = new Set(arr)
        for(let key of set3.keys()){ //一个新的遍历方法
            console.log(key)
        }
        for(let val of set3.values()){
            console.log(val)
        }
        for(let zhang2 of set3){
            console.log(zhang2);
        }
        for(let [key2, val2] of set3.entries()){
            console.log(key2, val2)
        }
         ```
    - map
        ```javascript
        let zhang = new Map();
        let arr = [1, 2, 3, 4, 5]
        zhang.set(arr,123)//map的key可以是任意数据类型，不像对象，只能是字符串
        console.log(zhang)//Map { [ 1, 2, 3, 4, 5 ] => 123 } 
        console.log(zhang.has(arr))//true
        console.log(zhang.size)//1
        zhang.delete(arr)
        console.log(zhang)//Map { }
        let shuang = new Map([['a', 1], ['b', 2]])
        console.log(shuang)//Mao { 'a' => 1, 'b' => 2}
        shuang.clear()
        console.log(shuang)//Map {  }
        ```
        - 添加用set 获取用get
        ```
- 类
    ```javascript
    class human{
        constructor(name, age){ //构造器
            this.name = name;
            this.age = age;
        }
        run(){
            console.log("我在跑步")
        }
    }
    let zhang = new human('zhangShuang', 19)
    zhang.run()//我在跑步

    class father extends human{//类的继承
    }
    let ss = new father("ss", 4);
    ss.run();//我在跑步

    class son extends human{
        constructor(name, age){
            super(name, age)//用来调用基类
        }
    }
    let aa = new son("sss", 19)
    aa.run()
    ```
    - 不提供私有方法和私有属性
    - 静态属性和静态方法
- promise
    - 异步的解决方案
    - 用在向服务器请求，暂时不看
- 模块化
    ```javascript
    //文件program.js
    let zhang = "ddffdg"
    let baba = str => console.log((new Date()).toString() + ": " + str)
    export {zhang, baba};
    export default huamm;   //通
    ```
    ```javascript
    //文件demo.js
    import {zhang, baba  as bb} from '../program';   //对导出的名字进行重命名
    import son from 'program'; //对于导出的类可以自己命名
    console.log(zhang)
    ```