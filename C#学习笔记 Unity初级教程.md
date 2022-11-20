# C#学习笔记 Unity初级教程

## 行为组件脚本

* 在添加组件的sprite部分添加相应脚本。

* 在代码中对组件使用`get...`得到组件，并对其属性进行相应改写，得到自己想要的效果。

## 变量和函数

* 函数又称方法，变量输入，并输出结果，此过程又称返回。
* 函数需要指定返回类型。
* `Debug.Log(含变量的表达式)`可在Unity控制台查看变量输出结果。

## 约定和语法

参照C++模式。

## IF 语句

用来判断，C++模式。

## 循环

C语言基础

* **for**循环

* **while**循环

* **do while**循环

## 作用域和访问修饰符

* `{}`代表作用域。

* 修饰符 参照[C#学习笔记 基础语法、数据类型、面向对象思想](https://github.com/Geek-Zstar/Tasks/blob/main/C%23%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95%E3%80%81%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E3%80%81%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E6%80%9D%E6%83%B3.md) 。
  * 公开变量可在Unity控制台上进行操作，私有则不行。
  * 在函数中设置变量会被控制台操作覆盖，在`start()`函数中则不会。

## Awake 和 Start

* `void Awake()` 在启动脚本组件之前调用，适合设置引用。

* `void Start()` 在Awake之后调用，且在首次更新之前，适合延迟初始化。
* 两者在组件的生命周期（我目前的理解是一个组件被调用到结束称为一个生命周期）中只能被调用一次。

## Update 和 FixedUpdate

* `Update()`每帧调用,按照帧数间隔执行，比如移动，简单计时等，均在update中实现。

* `FixedUpdate()`每帧调用，但按照固定时间（固定为0.02）执行，一般影响物理对象的操作在此处执行。

* `Ctrl+shift+M`启动向导添加特殊函数。

## 矢量数学

* `Vector3.magenitude` 计算向量模。

* `Vector3.Dot(VectorA,VectorB)` 点积计算。

* `Vector3.Cross(VectorA,VectorB)` 叉积计算。

* 数学物理知识

## 启用和禁用组件

* 首先声明组件。
* 使用`.enable`来禁用组件。

## 激活游戏对象

* Start函数中，在游戏脚本里使用`gameObject.Setactive(bool型)`进行激活或停用。

* 对父类操作会影响到子类，子类在自己的层次结构中的状态由自己和父类决定。

* `Debug,Log("Object.activeself/object,activeInHierarchy)`在Console界面中查看状态。

## Translate 和 Rotate

* `tranform.Translate(Vector3.forward * moveSpeed/*移动速度变量*/ * Time.deltaTime)`用于游戏对象平移。

* `tranform.Rotate(Vector3.up * turnSpeed/*旋转速度变量*/ * Time.deltaTime)`用于游戏对象旋转。

## Look At

用于摄像头追踪游戏对象

* `public Transform target`声明。
* `transform.LookAt(target)`调用该函数。
* 对摄像机项目应用，将游戏项目拖到对应target框内。

## Destory

用于移除游戏对象或对象的组件。比如消灭敌人，或者失重效果。

* `Destory(移除对象，延迟时间/* 例如 3f ,有三秒延迟，此项不填默认为0 */)`

## GetBotton 和 GetKey

* 可在上方Edit → Project Settings → Input中更改按键。
* 该函数调用返回结果为**bool**型，代表是否触发。GetKey持续作用，而GetBottom只有第一帧作用。
* 在Input中调用该函数，形参可为`Keycode.按键名称`。

## GetAxis

* 返回一个**-1~1**之间的浮点值。
* **Gravity** 控制输入值，值越大变化越快。
* **Sensitivity** 控制输入返回值，值越大变化越快。
* **Dead ** 盲区，相当于设置一个开始响应的下限。
* **snap** 勾选与否控制 是否要求同时按下按钮时进行归零。
* `Input.GetAxis("Horizontal")`获取横轴值。
* `Input.GetAxis("Vertical")`获取竖轴值。
* `Input.GetAxis("Raw")`获取整数值。

## OnMouseDown

OnMouseDown及其相关函数可检测碰撞体或GUI文本元素的点击，是一个特殊函数。

## GetComponent

* 首先public进行声明。
* `GetComponent<类型>(类型对应的参数)`
* 可以嵌套使用，用`.`访问。
* 会占用大量计算能力，应减少使用。最好在Awake或Start中使用。

## DeltaTime

属于Time类的DeltaTime属性，作用是固定更新函数的间隔时长，使操作变得平滑。（不流畅的原因是每完成一帧所需要的时间是不同的）

## 数据类型

主要分为值类型和引用类型。

* 参考 [C#学习笔记 基础语法、数据类型、面向对象思想](https://github.com/Geek-Zstar/Tasks/blob/main/C%23%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95%E3%80%81%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E3%80%81%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E6%80%9D%E6%83%B3.md)
* 结构体**Structs**属于值类型，Unity中最常见的2种：
  * **Vector3** 三维矢量，可用于速度构建，投影等。
  * **Quaternion** 四元数，用于存储和表示对象的旋转角度。详细参考 [Unity学习笔记2]()

* 引用类型比如
  * **tranform** 变换组件,是一个类
  * GameObject

## 类

与C++面向对象思想互通，类与对象 好比 水果和苹果。

主要都是C++的学习心得。

## Instantiate

**Instantiate**函数主要用于克隆游戏对象，比如prefab中的预置体。使用方面，结合其他组件，比如在Update中使用可以实现不断发射的效果。

* `Instantiate(要实例化的对象，新克隆的对象指定的位置，新克隆的对象指定的旋转)`

## 数组

C语言知识，在Unity中正常使用。

## Invoke

该函数的作用是将其他函数的调用安排在指定的延时后发生。比如在Start函数中对对象使用方法进行实例化，就可以用该函数进行延时。

* `Invoke("方法名称，即函数名称"，延时时间)`

* `InvokeRepeating("方法名称，即函数名称"，延时时间，反复调用的时间间隔)`可用于多次反复调用。

## 枚举

参考 [C#学习笔记 基础语法、数据类型、面向对象思想](https://github.com/Geek-Zstar/Tasks/blob/main/C%23%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95%E3%80%81%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E3%80%81%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E6%80%9D%E6%83%B3.md),主要是为了优化代码。

## Switch语句

C语言知识。菜单化界面经常使用。Unity中用于大量的同情景下的条件判断，同样是为了优化代码。



## 初级教程学习总结

对C#在Unity中的使用有了一个简单的了解，同时也感受到了面对对象在Unity游戏开发中的必要性，主要是一些简单的使用方法，遇到的问题主要就是与稍微高级一些的知识之间的衔接存在问题，不过也会在后续的学习中完善自己的知识体系。





###### 参考资料

[C#初级编程](https://www.bilibili.com/video/BV1oy4y1q7jJ/?spm_id_from=333.999.0.0&vd_source=99f7033efb216e152f86d8f8a2de3848)

