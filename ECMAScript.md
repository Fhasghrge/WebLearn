<!-- 来自阮一峰的ECMAScript入门 -->
- 变量提升只是声明被提升了，赋值没有提升，使用let关键字可以解决这个问题
- 暂时性死区(temporal dead zone)：在块级作用域中let const声明的关键字会在变量声明之前的区域形成一个封闭性的死区，即使全局中已经声明这个变量也会报错
- 结构赋值：
    - [a,b] = [1,2];
    - [a, b, c] = "123";
    - ({a, b} = {a : 1, b : 2});**对象赋值进行匹配**
- rest参数
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
- 字符串扩展
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
- 数值：
     - isFinite判断数值是否有界
     ```javascript
    console.log(Number.isFinite(NaN))//false
    console.log(Number.isNaN(NaN)) //true
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
    zhang.run()

    class father extends human{//类的继承
    }
    let ss = new father("ss", 4);
    ss.run();

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