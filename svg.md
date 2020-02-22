# svg

### 概述

- svg 可以直接插入HTML中，或者单独文件再通过特殊的标签引入或者通过CSS中引入

- SVG可以转换成BASE64编码，通过DATA URL 写入网页

### 语法

- viewBox属性： 左上角的横纵坐标，视口的宽度和高度
- 所有的url都通过`#id`的形式
##### `<circle>`
- 位置，半径，填充色，描边色，边框宽度
#### `<line>`
- 起点，终点，粗细
#### `<polyline>`
- 折线，折点的坐标，填充，颜色
#### `<rect>`
- 矩形，位置，长宽，描边色，填充色
#### `<ellipse>`
- 椭圆，位置，横纵轴半径，描边色，描边宽度，填充色
#### `<polygon>`
- 多边形，每个端点的坐标
#### `<path>`
- 路径？待详细看看
#### `<text>`
- 绘制文本，文本区块基线起点的横纵坐标
#### `<use>`
- 用于复制标签
- 另外还可以设置其他属性（位置，宽高
#### `<g>`
- 多个形状组成一个组方便复用
#### `<defs>`
- 用于自定义形状，但是内部代码不显示（相当于函数
#### `<pattern>`
- 标签用来将自定义的形状平铺到这个区域
- `patternUnits`有这个属性
#### `<image>`
- 插入图片文件（xlink:href)
#### `<animate>`
- 动画，定义那个属性，从哪一个状态转到哪个状态，持续时间，是否重复等动画特性
- 可以定义多个标签，定义多个属性
#### `<animateTransform>`
- 对css属性起作用的动画
- 开始的时间，持续时间，
### JavaScript操作

#### DOM操作

- svg以及svg内嵌标签都可以使用DOM或者CSS设置属性
#### 获取SVG DOM
- 使用`<object>`、`<iframe>`、`<embed>`标签插入 SVG 文件，可以获取 SVG DOM，但是通过`<image>`插入的SVG文件无法获取SVG DOM
#### 读取SVG源码
- 通过XMLSerilalizer实例的serialzeToString()方法获取SVG元素的源码
```javascrip
var svgString = new XMLSerializer()
  .serializeToString(document.querySelector('svg'));
```
#### SVG图像转换成Canvas图像
- 首先把SVG图像指定到image元素上，然后把image绘制到Canvas

### 实例

