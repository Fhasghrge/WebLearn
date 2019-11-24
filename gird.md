##容器属性
#### display属性
- display:grid指定一个容器采用网格布局
- 默认容器元素都是块级元素，也可以设置为行内元素
    - display: inline-grid
#### grid-template-columns/grid-template-rows属性
- 代码实例：
    ```css
    .container {
        display: grid;
        grid-template-columns: 100px 100px 100px;
        grid-template-rows: 100px 100px 100px;
    }
    ```
- repeat()函数，参数：重复的数量，重复的值（可以是多个模式)
- auto-fill关键字
    - repeat的第一个参数，表示尽可能多的填充容器
- fr关键字
    - 意为片段，显示比例关系，按照比例关系划分容器大小
    - 可以和绝对长度单位结合使用
- minmax()
    - 产生长度范围，两个参数，最大值和最小值
- auto关键字
    - 第二个参数由浏览器自己决定
- 网格线的名称
    - 使用方括号指定每一个网格线的名字，方便引用
#### grid-row-gap/grid-column-gap/grid-gap属性
- 设置间距

#### grid-template-areas属性
- 指定区域的名称
#### grid-auto-flow
- 表示折叠的顺序，默认是row,当值为column时，表示先烈后行
- row dense 指定项目以后剩下的项目如何自动放置，尽可能的紧密排列
- column dense
#### justify-items/align-items/place-items属性
- 设置单元格位置（start/end/center/stretch)

#### justify-content/align-content/place-content
- 设置整个内容区域在容器里面的位置
    - 当项目没有指定大小时，拉伸整个网格容器
    - start/end/center/strech/space-around/space-between/space-evenly
#### grid-auto-columns/grid-auto-rows
- 对于网格内的项目超出容器（浏览器会自动生成多余的网格）的部分进行设置
#### grid-template/grid属性
- grid-template-columns,grid-template-rows,grid-template-areas的简写
- grid是grid-template-rows、grid-template-columns、grid-template-areas、 grid-auto-rows、grid-auto-columns、grid-auto-flow的简写
## 项目的属性
#### grid-column(row)-start(end)
- 指定项目边框所在的网格线
- span关键字，表示跨越，即上下（左右)边框跨越多少网格
- 由此看出本质就是依靠网格线划分区域
#### grid-column/grid-row属性
- 上面两个的缩写，使用`/`分开
#### grid-area属性
- 指定项目属性放在哪一个区域
- 也可以使用网格线代替：成为grid-row-start、grid-column-start、grid-row-end、grid-column-end的缩写，使用`/`分割
#### justify-self/align-self/place-self属性
- 设置单元格内容的位置
- start/end/center/stretch
