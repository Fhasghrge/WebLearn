```javascript
var scene = new THREE.Scene();//场景
var camera = new THREE.PerspectiveCamera(75, window.innerWidth, window.innerHeight, 0.1, 1000);//透视相机
var renderer = new THREE.WebGLRenderer();//渲染器
renderer.setSize(window.innerWidth, window.innerHeight);//设置渲染器的大小为窗口的内宽度，也就是内容区的宽度
document.body.appendChild(renderer.domElement);
```
## 准备操作：
### 场景
- 场景是所有物体的容器
### 相机
- 相机决定了观察物体的角度
- 场景动起来：
    - 改变camera的位置，并且不断渲染，把render()函数单独放在一个函数中，用requestAnimationFrame()函数不断递归调用
    - 改变mesh的位置，也就是改变物体本身的位置，也是通过上面的形式实现的
    - 使用TWEEN.js库渲染动画
- THREE.Camera
    - 正投影相机THREE.OrthographicCamera
        - 类似于工程图纸没有近大远小这一说
        - 参数：left right top bottom near far
    - 透视投影相机THREE.PerspectiveCamera
        - 有一个基本点，就是近大远小
        - 参数：fov aspect near far
        - 看清楚东西，视角在30~40比较好
### 渲染器
- 决定渲染的结果在什么元素上面，以什么样的形式展现（就是把图形元素化然后用DOM插入进去）
- render下面的domElement属性表示画布元素，所有的渲染都是在domElement上进行
## 正式绘图操作：
- 画点：
    ```javascript
    THREE.Vector3 = function ( x, y, z ) {
    this.x = x || 0;
    this.y = y || 0;
    this.z = z || 0;
    };
    //方法一
    var point1 = new THREE.Vecotr3(4,8,9);
    //方法二（推荐使用）
    var point1 = new THREE.Vector3();
    point1.set(4,8,9);
    - 没有单独画点的函数，所以必须把点放在容器之中才行，这和容器就是包括了无数的
    点构成，无数的点构成容器的一个大数组。
    ```
- 画线：
    - 点画完以后通过函数进行进行连接，并且提供线的材质
    - 线的材质：由点、材质、颜色构成
### 渲染图形
- 用渲染器结合场景和相机渲染出画面
- renderer.render(scene,camera)
- 渲染：
    - 离线渲染：事先渲染好一帧一帧图片，然后拼接图片达到画面效果
    - 实时渲染：requestAnimationFrame(render)使用这个函数可以循环调用参数中的函数，也就是不停的render，即使画面没动也要不停的渲染



## 框架
- 使用一系列函数，把每一个部分模块化，更容易读懂
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Three框架</title>
        <script src="js/Three.js" data-ke-src="js/Three.js"></script>
        <style type="text/css">
            div#canvas-frame {
                border: none;
                cursor: pointer;
                width: 100%;
                height: 600px;
                background-color: #EEEEEE;
            }
        </style>
        <script>
            var renderer;
            function initThree() {
                width = document.getElementById('canvas-frame').clientWidth;
                height = document.getElementById('canvas-frame').clientHeight;
                renderer = new THREE.WebGLRenderer({
                    antialias : true
                });
                renderer.setSize(width, height);
                document.getElementById('canvas-frame').appendChild(renderer.domElement);
                renderer.setClearColor(0xFFFFFF, 1.0);
            }
            var camera;
            function initCamera() {
                camera = new THREE.PerspectiveCamera(45, width / height, 1, 10000);
                camera.position.x = 0;
                camera.position.y = 1000;
                camera.position.z = 0;
                camera.up.x = 0;
                camera.up.y = 0;
                camera.up.z = 1;
                camera.lookAt({
                    x : 0,
                    y : 0,
                    z : 0
                });
            }
            var scene;
            function initScene() {
                scene = new THREE.Scene();
            }
            var light;
            function initLight() {
                light = new THREE.DirectionalLight(0xFF0000, 1.0, 0);
                light.position.set(100, 100, 200);
                scene.add(light);
            }
            var cube;
            function initObject() {
                var geometry = new THREE.Geometry();
                var material = new THREE.LineBasicMaterial( { vertexColors: THREE.VertexColors} );
                var color1 = new THREE.Color( 0x444444 ), color2 = new THREE.Color( 0xFF0000 );
                // 线的材质可以由2点的颜色决定
                var p1 = new THREE.Vector3( -100, 0, 100 );
                var p2 = new THREE.Vector3(  100, 0, -100 );
                geometry.vertices.push(p1);
                geometry.vertices.push(p2);
                geometry.colors.push( color1, color2 );
                var line = new THREE.Line( geometry, material, THREE.LinePieces );
                scene.add(line);
            }
            function render()
            {
                renderer.clear();
                renderer.render(scene, camera);
                requestAnimationFrame(render);
            }
            function threeStart() {
                initThree();
                initCamera();
                initScene();
                initLight();
                initObject();
                render();
            }
        </script>
    </head>

    <body onload="threeStart();">
        <div id="canvas-frame"></div>
    </body>
</html>
```
- 动画性能的评估：
    - FPS每秒的帧数
    - MS一帧所需要的时间
    - 监视器放在初始化的函数中
- 光源：
    - var light = new THREE.Light(0xFF0000);定义不同颜色的光源，这是其他光源的基类
    - 环境光：THREE.AmbientLight
        - 多次反射得到的光被称为环境光，无处不在的光，没有敏感区分
        - 环境光的位置对于物体的观察并没有太大影响，这是让物体均匀发光的光
    - 点光源：THREE.PointLight(color, intensity, distance)
        - intensity:默认1.0,就是100%的光强度
        - distance:在这段距离内光强度逐渐从intensity减弱到0
    - 聚光灯：THREE.SpotLight(hex,intensity,distance,angle,expoent)
        - angle聚光灯着色角度，？？？
        - expoent衰减参数，越大衰减的越快
    - 方向光（平行光）THREE.DirectionalLight(hex, intensity)
        - 平行光的方向由光源方向和原点方向决定
    - 光源的叠加：
        - 就是实际光源的叠加
    - 没有任何光源的物体是黑色的
- 材质：
    - Lambert
        - 粗糙不均匀，没有镜面反射，表面均匀的散射光
        - 颜色收到环境光的影响，材料本身的颜色并没有太大影响
- 纹理：
    - 纹理就是贴图
    ```javascript
    THREE.Texture( image, mapping, wrapS, wrapT, magFilter,
             minFilter, format, type, anisotropy )
    ```
    - JavaScript没有权限从本地加载图片，必须使用http，
        ```javascript
        var image = THREE.ImageUtils.loadTexcure(url);
        ```
    - 贴图当作material属性中map的值使用
