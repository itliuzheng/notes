http://www.webgl3d.cn/Three.js/



# Three.js资源

github链接：https://github.com/mrdoob/three.js

Three.js官网：https://threejs.org/

[Threejs中文文档](http://www.yanhuangxueyuan.com/threejs/docs/index.html)



WebGL零基础入门教程(郭隆邦)

http://www.yanhuangxueyuan.com/WebGL/



引用js文件

http://www.yanhuangxueyuan.com/threejs/build/three.js



## 快速入门-新手上路

### 整个程序的结构

#### 场景Scene

##### 网格模型Mesh

1. 几何体Geometry
   1. 形状
   2. 尺寸
2. 材质Material
   1. 颜色
   2. 贴图
   3. 透明度

##### 光照Light

1. 颜色
2. 分类
   1. 环境光
   2. 点光源
   3. 平行光

#### 相机Camera

##### 位置视线方向

##### 投影方式

	1.	透射投影PerspectiveCamera
 	2.	正射投影OrthographicCamera()

#### 渲染器Renderer

##### 渲染器创建

WebGLRenderer()

##### 开始渲染

.render(scene,camera)

##### domElement属性

canvas对象



### 旋转动画、requestAnimationFrame周期性渲染

#### 渲染频率

调用渲染方法`.render()`进行渲染的渲染频率不能太低，比如执行`setInterval("render()",200);`间隔200毫秒调用渲染函数渲染一次，相当于每秒渲染5次，你会感觉到比较卡顿。渲染频率除了不能太低，也不能太高，太高的话计算机的硬件资源跟不上，函数`setInterval()`设定的渲染方式也未必能够正常实现。一般调用渲染方法`.render()`进行渲染的渲染频率控制在每秒30~60次，人的视觉效果都很正常，也可以兼顾渲染性能。

#### `requestAnimationFrame()`函数

前面讲解threejs动画效果，使用了`setInterval()`函数，实际开发中，为了更好的利用浏览器渲染，可以使用函数`requestAnimationFrame()`代替`setInterval()`函数，`requestAnimationFrame()`和`setInterval()`一样都是浏览器`window`对象的方法。

`requestAnimationFrame()`参数是将要被调用函数的函数名，`requestAnimationFrame()`调用一个函数不是立即调用而是向浏览器发起一个执行某函数的请求， 什么时候会执行由浏览器决定，一般默认保持60FPS的频率，大约每16.7ms调用一次`requestAnimationFrame()`方法指定的函数，60FPS是理想的情况下，如果渲染的场景比较复杂或者说硬件性能有限可能会低于这个频率。可以查看文章[《requestAnimationFrame()》](http://www.yanhuangxueyuan.com/HTML5/time.html)了解更多`requestAnimationFrame()`函数的知识。



#### 均匀旋转

在实际执行程序的时候，可能`requestAnimationFrame(render)`请求的函数并不一定能按照理想的60FPS频率执行，两次执行渲染函数的时间间隔也不一定相同，如果执行旋转命令的`rotateY`的时间间隔不同，旋转运动就不均匀，为了解决这个问题需要记录两次执行绘制函数的时间间隔。

使用下面的渲染函数替换原来的渲染函数即可，`rotateY()`的参数是`0.001*t`，也意味着两次调用渲染函数执行渲染操作的间隔`t`毫秒时间内，立方体旋转了`0.001*t`弧度，很显然立方体的角速度是`0.001`弧度每毫秒(0.0001 rad/ms = 1 rad/s = 180度/s)。CPU和GPU执行一条指令时间是纳秒ns级，相比毫秒ms低了6个数量级，所以一般不用考虑渲染函数中几个计时语句占用的时间，除非你编写的是要精确到纳秒ns的级别的标准时钟程序。

```javascript
let T0 = new Date();//上次时间
function render() {
        let T1 = new Date();//本次时间
        let t = T1-T0;//时间差
        T0 = T1;//把本次时间赋值给上次时间
        requestAnimationFrame(render);
        renderer.render(scene,camera);//执行渲染操作
        mesh.rotateY(0.001*t);//旋转角速度0.001弧度每毫秒
    }
render();
```

