## git学习笔记

### 一、git安装

官网下载，没什么难度，可能唯一的难点在于科学上网

### 二、初窥git

> Git是目前世界上最先进的分布式版本控制系统

* 一开始看到这句话时，既惊叹于”最先进“三个字，又疑惑于”分布式版本控制系统“这个概念。

​       看了廖老师用 **word** 举的例子之后，我深有体会。

* 截至此时，在我的眼中，git就是一个功能强大的团队协作工具。



#### 简单功能了解

简单了解了一下git强大的功能，我觉得最突出的亮点就是 **git** 能高效管理多版本文件。还有一个亮点就是 **git** 可以直接在本地使用，即不需要连接WIFI！（虽然现在不联网的情况很少了）

#### git基本流程

* 工作区：在自己的电脑里操作文件的地方

  > add ↓
  > 
  
* 暂存区：感觉类似存储空间中的缓存区

  > commit ↓、diff ↑↑ //可用于查看上次提交的文件，有的时候三天打鱼，两天晒网（
  >
  
* 本地仓库：本地版本区，我的理解是我就是我自己的中央服务器，这个中央服务器就是本地仓库

  > push ↓、fetch ↑
  >
  
* 远程仓库：

  > pull ↑↑↑ //直接更新到工作区

#### 分布式管理相对于集中式管理的优势总结

* 前面提到的 无需连接wifi。

  ​        因为git无中央服务器，大家各自为战，只要最终把战果直接推送给对方，就可以省下一个中转的过程！

* 安全性高

  ​        一人数据丢失或损毁不要紧，每个人都有版本库（但如果还没上传，那可能就寄了）。如果是集中式，中央服务器寄那就全都寄。

#### 版本库创建

廖老师的教程上使用了这样的命令：

```
$ mkdir [文件名] //mkdir用于创建目录名
$ cd [文件名]    //cd用于打开该目录，定位文件
$ pwd           //用于显示当前目录
/文件路径
```

而我在网上学习的git教程中，直接对目标目录右击，选择**Git Bash here**,即可创建版本库。

* 注意：版本库创建之后会在目标文件夹下生成一个`.git`的隐藏文件，我认为它的作用是为git的运行提供所需的环境，所以不能轻易修改删除。

  想查看git文件我知道的有两种方法：

  1. 目录点击查看，勾选 **隐藏的目录**。

  2. 使用如下命令

     ```
     $ is -ah
     ```

#### 添加文件到版本库

* 第一步，工作区上传到暂存区

  ```
  $ git add file.txt
  ```

​       无反应则说明执行成功。

* 第二步，暂存区提交到本地仓库

  ```
  $ git commit -m"说明内容，比如提交了什么，修改了什么"
  ```

​       执行成果会有提示。

* 注意：
  1. 可以多次add多个文件，然后一次性commit。
  2. 使用`git status`可以查看文件状态，结合`git diff`使用，查看文件修改内容。

#### git其他常用命令

* `git init`:初始化，在操作的最开始要输入这个命令。

* `git log`：显示最近到最远的三次提交日志。

* `git reset  --hard HEAD^^^` :回退至前 **3** 个版本（HEAD是指向本地版本库主分支master的指针，可指定版本号，即可以回到指定的过去，也可以去往曾抵达的未来）

  结合`git reflog`可以查看每一次命令，包括版本号，这意味着可以实现版本的反复横跳。

* `git checkout -- [文件名]`:将文件撤销至上一个状态。即“还原”。

* `git rm`：从工作区删除文件。

* `git remote`：查看是否有远程仓库源

#### 远程仓库

1. 创建SSH Key，在我的电脑中，寻找`C:\Users\zxy666\.ssh\id_rsa.pub`,用文档文件打开，再去GitHub网站上`Add Key`，成功！

2. 在控制台输入身份信息

   ```
   $ git config --global user.name"Geek-Zstar"  //global意指全局
   $ git cinfig --global user.email"2313270446@qq.com"
   ```

3. 连接远程仓库

   ```
   $ git remote add origin git@github.com:Geek-Zstar/Tasks.git
   ```

   可以使用`git remote -v`查看是否成果连接。

4. 推送文件，第一次使用`git push -u origin master`将本地仓库的文件推送到远程仓库的master分支下。之后的推送无需`-u`，此为分支关联参数，将本地的master与远程的master连接起来。

#### 推送过程中遇到的问题

1. `Git masterbranch has no upsteram branch`报错

   原因是因为github创建仓库后默认分支是main，而本地创建是master，两者不匹配。

   解决方法：在远程仓库创建了一个master分支。

2. SSH警告

   根据廖老师的教程得知这个问题的名字，解决方法很简单，输入yes之后回车即可。实际上，这是由于SSH连接第一次验证GitHub服务器的Key时，需要确认Key的指纹信息是否真的来自GitHub的服务器。防止有替身吗？（







##### 参考资料

1. [梁雪峰的git教程](https://www.liaoxuefeng.com/wiki/896043488029600)

2. [CSDN:git解决The authenticity of host 'github.com(192.30.255.112)' can't beestablish问题](https://www.liaoxuefeng.com/wiki/896043488029600)
3. [CSDN:Git master branch has no upstream branch的解决](http://t.csdn.cn/Jg7pt)
4. [CSDN:Git 连接Github](http://t.csdn.cn/3oWYy)
5. [bilibili:【git操作入门】](https://b23.tv/zix9HEr)
6. [bilibili:【git工作流和核心原理】](https://b23.tv/iRaGExf)

