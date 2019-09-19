- **openGL**本身时一个巨大的状态机
- glut库时与窗口有关基于gl的库
- 语法：
    - 初始化函数init()设置变量初始值
    - 显示回调函数display()图形绘制，观察变化，几何变化参数设置
    - 改变窗口回调函数：生成窗口，设置投影变换参数
    - 空闲回调函数：在系统闲时重新计算图像，处理输入和窗口事件

## 模型观察：
- 建立了三维模型之后，只用openGL描述如何观察
- 坐标变化，投影变化，视窗变换
## 基本功能
- 光照应用：三维模型必须加上光照才真实
- 图像增强效果：反走样 雾化 混合
- 位图和图像处理
- 纹理映射： 贴图？
- 实时动画：
- 交互功能