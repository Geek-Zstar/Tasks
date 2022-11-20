# C#学习笔记 基础语法、数据类型、面向对象思想

## 一、简单介绍

C# 是一种新式编程语言，不仅面向对象，还类型安全。 开发人员利用 C# 能够生成在 `.NET `中运行的多种安全可靠的应用程序。 C# 源于 C 语言系列，C、C++、Java 和 JavaScript 程序员很快就可以上手使用。

C# 是面向对象的、面向组件的编程语言。由于学习过C++，所以我也是很容易地就接受了C#面向对象的思想。

## 二、基础语法

### using

此关键字用法类似C++，用于使用命名空间，方便直接访问命名空间里的函数，对象等。比如熟知的`using namespace std;`

### class

面向对象思想，与C++一致的类关键字，用于声明一个类以定义对象。

### 类成员的访问修饰符

**public**（公用的）成员可以被任何代码访问。
**Private**（私有的） 成员仅能被同一个类中的代码访问，如果在类成员前未使用任何访问修饰符，则默认为private。
**Internal**（内部的 ） 成员仅被同一个项目中的代码访问。
**Protected**（受保护的） 成员只能由类或派生类中的代码访问。

###  默认值

| 数据类型     | 默认值 |
| ------------ | ------ |
| 整形         | 0      |
| 浮点型       | 0      |
| 字符串类型   |        |
| 字符型       | ‘\0’   |
| 布尔型       | false  |
| 其他引用类型 | null   |

### 关键字

#### 1. 上下文关键字

在 C# 中，一些标识符在代码的上下文中具有特殊的含义，例如 get 和 set 称为上下文关键字。

下表列出了**保留关键字**

| abstract  | As        | base     | bool       | break            | byte            | case    |
| --------- | --------- | -------- | ---------- | ---------------- | --------------- | ------- |
| catch     | Char      | checked  | class      | const            | continue        | decimal |
| default   | delegate  | do       | double     | else             | enum            | event   |
| explicit  | Extern    | false    | finally    | fixed            | float           | for     |
| foreach   | Goto      | if       | implicit   | in               | in (泛型修饰符) | int     |
| interface | internal  | is       | lock       | long             | namespace       | new     |
| null      | Object    | operator | out        | out (泛型修饰符) | override        | params  |
| private   | protected | public   | readonly   | ref              | return          | sbyte   |
| sealed    | Short     | sizeof   | stackalloc | static           | string          | struct  |
| switch    | This      | throw    | true       | try              | typeof          | uint    |
| ulong     | unchecked | unsafe   | ushort     | using            | virtual         | void    |
| volatile  | While     |          |            |                  |                 |         |

上下文关键字用于提供代码中的特定含义，但它不是 C# 中的保留关键字。

#### 2. 保留关键字

**get** 在属性或索引器中定义“访问器”方法，以检索该属性或该索引器元素的值。

**set** 义属性或索引器中的“访问器”方法，用于设置属性或索引器元素的值。

**value** 隐式参数，用于设置访问器以及添加或移除事件处理程序。

## 三、数据类型

C#中的数据类型主要分为值类型和引用类型。

### 值类型

主要包括整型、浮点型、字符型、布尔型、枚举型

#### 1. 整型

**sbyte**  有符号数，占用1个字节，-27〜27-1

**byte** 无符号数，占用1个字节，0〜28-1

**short** 有符号数，占用2个字节，-215〜215-1

**ushort** 无符号数，占用2个字节，0〜216-1

**int** 有符号数，占用4个字节，-231〜231-1

**uint** 无符号数，占用4个字节，0〜232-1

**long** 有符号数，占用8个字节，-263〜263-1

**ulong** 无符号数，占用8个字节，0〜264-1

>  默认为 int 型

#### 2. 浮点型

**float** 单精度浮点型，占用4个字节，最多保留7位小数

**double** 双精度浮点型，占用8个字节，最多保留16位小数

> 默认的浮点型是 double 类型。如果要使用单精度浮点型，需要在数值后 面加上 f 或 F 来表示，例如 123.45f、123.45F。

#### 3. 字符型

字符型 用 `char` 关键字表示，存放到 char 类型的字符需要使用单引号括起来，占用两个字节。

#### 4. bool型

布尔类型在 C# 语言中使用关键字 `bool` 来声明，它只有两个值，即 true 和 false。

> 默认值为false。

#### 5. 枚举型

使用`enum`关键字，定义枚举成员的值。

### 引用类型

引用类型包含以下几种类型： 类、接口 、数组 、委托 、字符串。

**引用类型的存储**

引用类型首先会在栈中创建一个引用变量，然后在堆中创建对象本身，再把这个对象所在内存的首地址赋给引用变量。和c++很相似，使用`ref`修饰符。

## 四、总结

C#和C++思想一致，很多内容也十分相似。高级编程语言之间有着各种各样的共性，对理解很有帮助。





###### 参考资料

<iframe src="//player.bilibili.com/player.html?aid=803516623&bvid=BV1sy4y1u7cw&cid=373583941&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

[C#文档](https://learn.microsoft.com/zh-cn/dotnet/csharp/)