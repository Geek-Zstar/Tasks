# C#学习笔记 协程、四元数

## 一、协程

* 协程即为协同程序，辅助于主线程的程序。
* 普通方法被调用时，主函数中原来执行的部分停止执行，然后去执行要调用的方法，并且被调用的方法执行完之后才能返回到调用前的状态接着往下执行；协同方法的执行是不用等协同方法执行完再执行调用之前原来方法的代码，可以通过特殊代码提前返回主函数执行主函数的代码，且这个返回操作可以执行多次。

### 协同方法的使用规则

1. 返回值类型必须是**IEumerator**。其为一个**接口**。

2. 有返回值，返回参数的时候用`yield return 返回值`。

3. 协程方法的调用使用用`StartCoroutine(CoroutineMethod())`。

4. 协成方法可延时调用，用yield return new WaitForSeconds（float f），参数单位是秒。

* 开启协程之后会继续运行主程序后面的代码，不会等协程方法执行结束后再回去执行主程序。两者**异步执行**。

* 协程的使用：Unity中提供了三个方法，分别负责协程的开启，协程的停止，全部协程的停止。
  * 协程的启动：StartCoroutine（）；
  * 协程的停止：StopCoroutine（）；
  * 全部协程的停止：StopAllCoroutine（）；

### 协程原理简析

提到协程原理，那就不得不提一嘴Unity中的**MonoBehavior类**。MonoBehaviour类定义了一个脚本文件从最初被加载，到最后被销毁的一个完整过程。其声明了游戏循环中的各类 **回调函数**。MonoBehaviour 是一个基类，所有 Unity 脚本都派生自该类。使用 C# 时，必须显式派生自 MonoBehaviour。下图为脚本生命周期流程图。

![图片](https://img-blog.csdnimg.cn/20210527210608158.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMDg0NzU2,size_16,color_FFFFFF,t_70)

一些重要回调函数的作用：

* `Awake()` 主要用于初始化一些参数。一个游戏对象被创建之前会被调用一次。（唤醒事件，只执行一次。）

* `OnEnable()` 一个游戏对象被激活时调用一次。（启用事件，只执行一次。当脚本组件被启用的时候执行一次。）

* `Start()` 也用于初始化一些参数。一个游戏对象被激活时调用一次。（开始事件，只执行一次。）
* `FixedUpdate() ` 固定时间更新事件，执行 N 次，0.02 秒执行一次。不受电脑帧率影响。所有物理组件相关的更新都在这个事件中处理。

* `Update()` 主要用于监听和更新各种事件和参数。游戏大循环的入口，每一帧会被调用一次，更新事件，执行 N 次，直到游戏结束。受电脑帧率影响。

* `LateUpdate()` 稍后更新事件，执行 N 次，在 Update 事件执行完毕后再执行。

* `OnDisable()` 一个游戏对象失效，但未被销毁时调用一次。

从上表可以很清楚的看到一个协程工作的时间点，主要在`Update()`后，和常规的方法有所区别。常规的方法应该是包含在对应的回调函数内的，算是回调函数的一部分。而协程在脚本生命周期中有着属于自己的位置。因此可以实现异步执行。

**注意**：生命周期事件，全部是由系统定义好的，且系统会自动调用。系统调用这些事件的顺序，和我们代码里面的书写顺序无关。

### 协程使用

协程方法通过**yield**这个特殊的属性可以在任何位置、任意时刻暂停。也可以在指定的时间或事件后继续执行，而不影响上一次执行的结果。且协程并不会在Unity中开辟新的线程来执行，其执行仍然发生在主线程中。

以下是我从网上摘录的 yield 的使用效果。

```c#
yield return null; // 下一帧再执行后续代码
yield return 0; //下一帧再执行后续代码
yield return 6;//(任意数字) 下一帧再执行后续代码
yield break; //直接结束该协程的后续操作
yield return asyncOperation;//等异步操作结束后再执行后续代码
yield return StartCoroution(/*某个协程*/);//等待某个协程执行完毕后再执行后续代码
yield return WWW();//等待WWW操作完成后再执行后续代码
yield return new WaitForEndOfFrame();//等待帧结束,等待直到所有的摄像机和GUI被渲染完成后，在该帧显示在屏幕之前执行
yield return new WaitForSeconds(0.3f);//等待0.3秒，一段指定的时间延迟之后继续执行，在所有的Update函数完成调用的那一帧之后（这里的时间会受到Time.timeScale的影响）;
yield return new WaitForSecondsRealtime(0.3f);//等待0.3秒，一段指定的时间延迟之后继续执行，在所有的Update函数完成调用的那一帧之后（这里的时间不受到Time.timeScale的影响）;
yield return WaitForFixedUpdate();//等待下一次FixedUpdate开始时再执行后续代码
yield return new WaitUntil()//将协同执行直到 当输入的参数（或者委托）为true的时候....如:yield return new WaitUntil(() => frame >= 10);
yield return new WaitWhile()//将协同执行直到 当输入的参数（或者委托）为false的时候.... 如:yield return new WaitWhile(() => frame < 10);
```

举一个简单的例子：

```c#
public class TestScript : MonoBehaviour
{
    int counter;
    void Start()
    {
        StartCoroutine("myCoroutine");
        print("Start ends.")
    }
    void Update()
    {
        if(counter<6)
        {
            print("farme:" + counter++)
        }
    }
    IEumerator myCoroutine()
    {
        print("Step1");
        yield return rull;
        print("Step2");
        yield return rull;
        print("Step3");
    }
}
```

此部分的输出应当为：

```C#
Step1
Start ends
frame0
frame1
Step2
frame2
Step3
frame3
frame4
frame5
```

## 二、四元数

### 基本概念

#### 四元数

在Unity中，所有物体都至少绑定了 Transform 这个组件，这个组件有三个属性：position、rotation、scale，它们分别用于控制物体的平移、旋转和缩放三种变化，其中最为复杂应该就是旋转了，它对应于 Transform 组件中的 **rotation** 属性，这个属性的类型就是**四元数**。

从本质上来讲，四元数应该算作一个高阶复数。四元数一般表示为 **( w , (x,y,z) )** = (w,v),其中 v 是一个向量，w则是一个实数。Q = w + x**i** + y**j** + z**k** 。这里的 **i**、**j**、**k**，与我在大学物理中学到的向量表示十分相似。 但在四元数这里，它们表示的是三个虚数单位。网上的资料也称四元数为一个**四维空间**。

#### 欧拉角

![欧拉角](https://img-blog.csdnimg.cn/f1f7d91bd83045b0b5ae05bcb85ee71d.png)

分别绕着原坐标z轴(蓝)，一次旋转以后的x轴(绿)以及两次旋转以后的z轴(红)旋转，最终产生的红色坐标系即表示出目标方向。

我的理解是依次围绕 x y z 3个轴转3次之后的3个值，用来表示物体朝向。

### 四元数构成

假设绕着 n 轴旋转 β 度, n 为(x, y, z)

那么可以构成四元数为:

四元数 Q = [cos(β/2), sin(β/2)n]

四元数 Q = [cos(β/2), sin(β/2)x, sin(β/2)y, sin(β/2)z]

### 运算法则

[四元数的运算法则及原理证明](https://www.cnblogs.com/yiyezhai/p/3176725.html)

### 其他旋转方式、万向节锁

在学习四元数的概念时，我了解到四元数可以有效避免**万向节锁**（好炫酷的名字）现象的产生。因此，我也简单了解了一下相关的原理。

在 Unity 中，常用的控制旋转的方法有：矩阵旋转、欧拉旋转，以及四元数。

1. **矩阵旋转**：使用一个4*4的矩阵来表示绕任意轴旋转时的变换矩阵，这个矩阵具有的特点：乘以一个向量的时候只改变向量的方向而不会改变向量的大小；
   * 优点：旋转轴可以是任意向量；
   * 缺点：进行旋转其实我们只需要知道一个向量和一个角度，4个值的信息，而旋转变换矩阵使用了4*4=16个元素；变换过程增加乘法运算量，耗时；

2. **欧拉旋转**：在旋转时，按照一定的顺序（例如：x、y、z，Unity中的顺序是z、x、y）每个轴旋转一定的角度，来变换坐标或者是向量，实际上欧拉旋转也可以理解为：一系列坐标旋转的组合；

   * 优点：只需使用3个值，即三个坐标轴的旋转角度；

   * 缺点：必须严格按照顺序进行旋转（顺序不同结果就不同）；

   容易造成“万向节锁”现象，造成这个现象的原因是因为欧拉旋转是按顺序先后旋转坐标轴的，**并非同时旋转**，所以当旋转中某些坐标重合就会发生万向节锁，这时就会丢失一个方向上的选择能力，除非打破原来的旋转顺序或者三个坐标轴同时旋转；由于万向节锁的存在，欧拉旋转无法实现**球面平滑插值**。
   
   > 复习到这里，去了解一下球面平滑插值！！！

### 实际使用

#### 初始化四元数

`Quaternion q = Quaternion.AngleAxis(60, Vector3.right);`

参数1: 需要旋转的角度。

参数2: 绕着哪个轴旋转。

#### 主要使用

* `Quaternion.Euler( x , y , z )` 
  * 会根据传入的欧拉角返回一个对应的四元数对象。
  * 本质是方法。

* `Quaternion.identity` 
  * 这个值代表的就是**无旋转**。
  * 本质是静态量。

* `Quaternion.LookRotation(Vector3 forward, Vector3 upwards= Vector3.up)` 

  * 作用是**将方向转化为旋转角度**：传入一个方向将返回一个旋转角，当某个物体被施加这个旋转角后，这个物体的forward方向将指向传入的方向。
  * 本质是方法。
  * **常常配合`transform.rotation = Quaternion.LookRotation()`使用**。

* `Quaternion.Slerp(Quaternion from ,Quaternion to, float t)` 

  * 球面线形插值 **from** 为起始方向 ; **to** 为终止方向 ; **t** 可以理解为速度，通常取值为0< t <= 1。
  * 本质是方法。
  * 举例如下：

  ```
  void update()
  {
      this.gameobject.transform.rotation = Quaternion.Slerp(from, to,t * Time.time );  
      // 可以把 t * Time.time 理解成速度 * 时间 等于角位移
  }
  ```

> 感觉都比较抽象，现在只能做到数学层面的理解，再学完 Unity 3D 后，我会继续深入学习。

#### 欧拉角和四元数的相互转化

1. 欧拉角转四元数

`Quaternion q2 = Quaternion.Euler(60, 0, 0);`

2. 四元数转欧拉角

```
Quaternion q;
q.eulerAngles;
```

3. 单位四元数

单位四元数表示没有旋转量(角位移)

当角度为0或者360度时

对于给定轴都会得到单位四元数

[1, (0, 0, 0)]或[-1, (0, 0, 0)]

## 三、总结

协程让我对 Unity 中 Object 的脚本生命周期有了一个清晰的认识，同时明白了在游戏运行时，代码组件都是如何工作的；四元数目前只是很抽象的理解，没有实际上手的机会，现阶段只能达到认识水平。在后续的3D游戏开发中也许可以进一步加深理解。







###### 参考资料

<iframe src="//player.bilibili.com/player.html?aid=516217825&bvid=BV1Ug411a7aY&cid=850149593&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

[CSDN: Unity 中的MonoBehavior 类](http://t.csdn.cn/FrBOY)

[CSDN: C#学习之 四元数](http://t.csdn.cn/gzdjP)

[CSDN: 旋转](http://t.csdn.cn/SiZwi)

[CSDN: Unity 中旋转的表示——四元数（上）](http://t.csdn.cn/kaffQ)

[CSDN: Unity 中旋转的表示——四元数（下）](http://t.csdn.cn/Tn1Fj)

[CSDN: Quaternion.LookRotation](http://t.csdn.cn/295UJ)

[CSDN: Quaternion.Slerp](http://t.csdn.cn/pVM99)
