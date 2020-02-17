# 安装配置

fcitx/rime输入法配置

#### 应用包管理

```
apt-cache madison <<package name>>
```

将列出所有来源的版本

#### Linux 查看命令所在位置

[linux](https://link.jianshu.com/?t=http://lib.csdn.net/base/linux)下有2个命令可完成该功能：**which ,whereis**

which 用来查看当前要执行的命令所在的路径。

whereis 用来查看一个命令或者文件所在的路径，

**which命令的原理：在PATH变量指定的路径中，搜索某个系统命令的位置，并且返回第一个搜索结果。也就是说，使用which命令，就可以看到某个系统命令是否存在，以及执行的到底是哪一个位置的命令。**
 **which命令的使用实例：**
 　**$ which grep**

**whereis命令原理：只能用于程序名的搜索，而且只搜索二进制文件（参数-b）、man说明文件（参数-m）和源代码文件（参数-s）。如果省略参数，则返回所有信息。**
 **whereis命令的使用实例：**
 　**$ whereis grep**

