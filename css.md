# 查漏补缺
- 对于不同的手机，页面的大小根据手机尺寸的大小决定选择vh 和vw；
- 对于收到屏幕高度影响较大的部分用vh
- 对于受宽度影响较大的部分使用vw
+ 一般约定行高、字号都是偶数
+ 块级元素可以设置宽和高，但是行级元素不能设置，`<p>`, `<div>`标签是块级元素，块级元素占据整个行空间，但是高没有自己设置，只是包裹了元素内部的元素，行级元素仅仅包裹内部元素
+ 元素一旦浮动，就脱离标准文档流，无论是行内还是块级元素，都可以设置行高，元素可以并排显示，一旦浮动，原来的很多规则都变了，浮动的元素变成了能够设置行高的包裹器
+ 标准流中的文字不会被浮动元素挡住，但是会挡住p边框，
    > 会把p在边框中挤到一边？
+ 浮动这个东西，为了避免混乱，要浮动都浮动，所以很恶心
+ 浮动元素如果没有设置宽高，就只会包裹内容中的行高
+ 一个元素要浮动，其父元素必须要有高度，否则都浮动在第一行了(脱离了标准文档流)，但    **设置高度不能适应页面的快速变化**
+ 经典名言： `有高度的盒子，才能关住浮动` 只要浮动在一个有高度的盒子内，那么这个浮动就不会影响后面的浮动元素了
+ `clear: both`清除浮动带来的不必要的影响，意思就是不允许左边，右边有浮动的对象，   **但是所在标签的`margin`属性失效**
+ 父元素不能包裹浮动元素，也就是即使浮动元素有高度，但是父元素没有高度
+ 隔墙法： 在两个浮动元素之间添加一个元素`clear:both`使得两个浮动元素被隔开
+ **内墙法**： 一个元素不能被浮动元素撑起来，所以可以使用非浮动元素(`clear:both`)伴随   浮动元素把父元素撑起来
+ 给父元素添加`overflow:hidden`使得父元素能够包裹子元素中的浮动元素 （**偏方不知道原因**）
+ 绝对定位之后就不用区分行内元素和块级元素，都可以直接设置行高
+ 一个绝对定位的元素，如果父辈元素出现已经定位的元素，那么将以这个父辈元素为参考点
+ 工程上，常常使用`父相子绝`父亲脱标，儿子没有脱标在父亲的范围内移动
+ 绝对定位儿子忽视父亲的`padding`以`border`的左上角为参考点
+ 浮动元素不能使用`z-index`,只有定位(三种)了的盒子才能使用`z-index`
- box-sizing = border-box;可以消除boder以及padding对元素长度的印象，全部在boder里面来描述
***
***
***

# CSS3
### 边框
- box-shadow
```css
    /* x偏移量 | y偏移量 | 阴影颜色 */
    box-shadow: 60px -16px teal;

    /* x偏移量 | y偏移量 | 阴影模糊半径 | 阴影颜色 */
    box-shadow: 10px 5px 5px black;

    /* x偏移量 | y偏移量 | 阴影模糊半径 | 阴影扩散半径 | 阴影颜色 */
    box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);

    /* 插页(阴影向内) | x偏移量 | y偏移量 | 阴影颜色 */
    box-shadow: inset 5em 1em gold;

    /* 任意数量的阴影，以逗号分隔 */
    box-shadow: 3px 3px red, -1em 0 0.4em olive;

    /* 全局关键字 */
    box-shadow: inherit;
    box-shadow: initial;
    box-shadow: unset;
```
- box-image
<!-- 演示失败 -->
### 背景
- background-size
    - cover：此时会保持图像的纵横比并将图像缩放成将完全覆盖背景定位区域的最小大小。
    - contain：此时会保持图像的纵横比并将图像缩放成将适合背景定位区域的最大大小。
- background-origin
    - border-box
    - padding-box
    - content-box
- background-clip
    - border-box
    - padding-box
    - content-box
### 文本效果
- text-shadow
    ```css
    /* offset-x | offset-y | blur-radius | color */
    text-shadow: 1px 1px 2px black; 

    /* color | offset-x | offset-y | blur-radius */
    text-shadow: #fc0 1px 0 10px; 

    /* offset-x | offset-y | color */
    text-shadow: 5px 5px #558abb;

    /* color | offset-x | offset-y */
    text-shadow: white 2px 5px;

    /* offset-x | offset-y
    /* Use defaults for color and blur-radius */
    text-shadow: 5px 10px;
    ```
- overflow-wrap
    - normal 正常单词结束处换行
    - break-word 表示如果行内没有多余的地方容纳该单词到结尾，则那些正常的不能被分割的单词会被强制分割换行。
### 字体
- @font-face
    - 事先指定好引用的字体
    ```css
    @font-face
    {
    font-family: myFirstFont;
    src: url('Sansation_Light.ttf'),
        url('Sansation_Light.eot'); /* IE9+ */
    }

    div
    {
    font-family:myFirstFont;
    }
    ```
***
***
## 动画
### 转化属性
- transform
    - none | transform-functions
- transform-origin
    - 设置元素旋转的基点
    - x-axis,y-axis,z-axis
    - 单位以及关键字查阅文档
- transform-style
    - flat 子元素不保留3d位置
    - preserve-3d 子元素保留3d位置（也就是有遮挡关系）
- perspective
    - 指定观察者与z=0平面的距离，透视深度
- perspective-origin
    - 指定观察者的位置
- backface-visibility
    - 定义当元素不面向屏幕时是否可见
### 2D转换
- **前面都要加上`transform:`**
- translate()方法
    - 参数left, top
- rotate()
    - 指定顺时针旋转的角度
    - 单位是deg
- scale()
    - 指定width, height缩放的倍数
- skew()
    - 指定相对于x轴，y轴旋转的角度
    - 单位deg
- matrix()
    - 把所有的2D转换方法结合在一起
### 3D转换
- translate3d(x,y,z)
- rotate3d(x,y,z,angle)
- scale3d(x,y,z)
- matrix3d(n,n,n,n,n,n,n,n,n,n,n,n,n,n,n,n)
- perspective(n)
### 过渡
- transition 以下的简写
- transition-property
- transition-duration
- transition-timing-functuon
- transition-delay
### 动画
- 动画属性
    - @keyframes规定动画
    - animation
        - 所有动画属性的简写属性
    - animation-name
        - 规定@keyframes动画的名称
    - animation-duration
    - animation-timing-function
    - animation-delay
    - animation-iteration-count
    - animation-direction
        - normal | alternate动画应该轮流反向播放
    - animation-play-state
        - paused | running规定动画是否暂停
    - animation-fill-mode
- @keyframes规则
    - from = 0% to = 100%
    - 百分比规定变化发生时间
 ### 多列
 - column-count
    - 规定元素应该分割的列数
 - column-gap
    - 规定列之间的间隔
 - column-rule
    - 设置列之间的宽度、样式和颜色规则
### 用户界面
- resize
    - 允许控制一个元素可调整大小性
- box-sizing
    - 规定如何计算一个元素的大小
    - content-box（border会加到外面） | border-box（border加到内部）
- outline-offset
    - 设置 outline 与一个元素边缘或边框之间的间隙



## css进阶

- 通过@font-face自定义字体类型以及字体地址
