## 数据结构笔记（为了熟悉JavaScript语法以及数据结构知识）
### 基础知识：
- `var nullVar = null`声明一个变量没有赋值
    - null表示没有对象，undefined表示没有赋值,两个都可以转变为false
- `delete`用于删除对象里面的属性
- JavaScript中对象就是键值对的集合
- let作用域的范围相当于int在C语言中的范围
- const关键字，和let大致相同，唯一不同的就是const只接受读操作，不接受写操作
- 箭头函数：
    ```javascript
    var zhang = (name, age) =>{
    console.log(name, age);
    }
    zhang("zhang",14);
    ```
- 数组解构：
    ```javascript
    //同时声明多个变量
    var [zhang, age] = ["zhangshuang", 19];
    console.log(zhang);
    console.log(age);
    [zhang, age] = [age, zhang];//进行值的互换
    console.log(zhang);
    console.log(age);
    ```
- 使用类进行面向对象编程：
    ```javascript
    class Book {
        constructor(title, name, age){
            this.name = name;
            this.age = age;
            this.title = title;
        }
        printName() {
            console.log(this.age)
        }
    }
    let zhang = new Book("uestc", "zhangshuang", 19);
    console.log(zhang);
    zhang.printName();
    ```
- JavaScript不支持二位数组，但是可以使用模拟嵌套实现二维数组的模拟
# 什么几把书？ 结束了！
