# markdown学习笔记

### markdown概述

* 通过网上的教程对**markdown**有了一个比较宏观的认识，第一次知道 **轻量级标记语言** 的妙用。

* 感受到了开发者的创意，编程式编写文档，是我从未想象过的，佩服佩服。

* 在学习的过程中也下意识地与 **word** 进行对比，两者相同的效果大多采用不同的实现方式。

* 发现了许许多多的优点与缺点，待我细细道来。

### markdown基本规则

最近，老师教我们写作文。我是不如小学生的大学生，不太会写。于是老师教我

#### 首先不要在正文里写标题，无论是

# 一级

## 二级

### 三级

#### 四级

##### 五级

###### 还是六级

> 然后正文就是正文，不要使用引用的格式

写字**不要乱加粗**，*不要写斜字*，<u>不要加下划线</u> , 也`不要乱加边框`  

写东西不要

1. 乱标
2. 序号

* 不管是有序
* 还是无序

还有的人居然还

* [ ] 在文字前面加方块
* [x] 更有甚者甚至还打个√，这都是不对的

```c
int main() {
    printf("写作文也不要和写代码混为一谈")
}
```

$$
更不能用数学公式的样式写
$$

| 作文里 | 不要出 | 现表格 |
|---:|:---:|:---|
|    |     |    |



也[^不要写成脚注]

写文章不要

---

乱用分割线

然后少去使用[百度](baidu.com"少用百度！！！")搜索文章

多看看自己写的[markdown学习笔记](#markdown学习笔记)吧！





参考视频：

<iframe src="//player.bilibili.com/player.html?aid=327623069&bvid=BV1JA411h7Gw&cid=171385214&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

### Markdown原理

* 重内容，轻形式，唯一重要的就是内容本身
* 工作原理（参考CSDN）
  1. 创建`.md`扩展名文件
  2. 在Markdown应用程序打开文件
  3. Markdown应用程序中的Markdown处理器将文件处理，转换成HTML或PDF等可打印文档
  4. 在Web浏览器或其他应用程序中查看

![Markdown工作原理](https://img-blog.csdnimg.cn/e3fa324d9d8141e09e0b86de3e792983.png)

* Markdown编译原理

[参考CSDN，有空深入研究]([https://blog.csdn.net/weixin_34220834/article/details/89280878?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166729480616782391899566%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=166729480616782391899566&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-8-89280878-null-null.142^v62^pc_search_tree,201^v3^control_1,213^v1^control&utm_term=markdown%E5%8E%9F%E7%90%86&spm=1018.2226.3001.4187](https://blog.csdn.net/weixin_34220834/article/details/89280878?ops_request_misc=%7B%22request%5Fid%22%3A%22166729480616782391899566%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fall.%22%7D&request_id=166729480616782391899566&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-8-89280878-null-null.142^v62^pc_search_tree,201^v3^control_1,213^v1^control&utm_term=markdown原理&spm=1018.2226.3001.4187))



### Typora更多功能探索



* 视图 源代码 mode、打字机 mode、专注 mode 启动！！！

1. **源代码mode** ：可以看到整个md文档的源代码，比如我上方的小作文。

2. **打字机mode**：会自动将打字区域移动至屏幕中央，成为无情的打字机！

3. **专注mode**：在打字机mode的基础上，将其他部分虚化，达到专注效果。

   

* 开发者工具

可以看到页面代码



* 内容目录

通过标题快速预览文档

[TOC]

* 编辑 复制为其他类型代码/文档

* 文件 偏好设置 我的评价是可玩性高









[^不要写成脚注]:正文真的不要写成脚注呦



