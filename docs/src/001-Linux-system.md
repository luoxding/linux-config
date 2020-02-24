# 了解Linux系统

## [linux根目录下的各文件夹含义说明](https://www.cnblogs.com/jameszeng/p/10785684.html)

[Linux根目录各个文件夹介绍及说明](https://blog.csdn.net/weixin_40928253/article/details/85566226)

```
root@eisvogel:/# ls -a
 .              boot   initrd.img       lost+found   proc   srv        tmp       vmlinuz.old
 ..             dev    initrd.img.old   media        root   swap       usr      'ystemctl disable firewalld'
 .autorelabel   etc    lib              mnt          run    swapfile   var
 bin            home   lib64            opt          sbin   sys        vmlinuz

```

在早期的 UNIX 系统中，各个厂家各自定义了自己的 UNIX 系统文件目录，比较混乱。

Linux 面世不久后，对文件目录进行了标准化，于1994年对根文件目录做了统一的规范，

推出 FHS ( Filesystem Hierarchy Standard )的 Linux 文件系统层次结构标准。

FHS 标准规定了 Linux 根目录各文件夹的名称及作用，统一了Linux界命名混乱的局面。

linux系统的根目录基本都会存在以下这些文件夹，这些文件夹和以及意义如下：

 

1 bin 存放二进制可执行文件，系统所需的可执行文件。

2 sbin 存放系统管理的二进制可执行文件。

3 dev 设备文件。

4 etc 配置文件。

5 proc 虚拟文件目录，内存映射文件信息。

6 opt 额外安装软件的存放目录

7 usr 存放系统应用程序。

8 root 超级用户主目录。

9 boot 系统引导加载时的各文件。

10 mnt 挂载目录

11 tmp 临时文件

12 lib 存放程序运行时所需要的共享动态库及内核模块。

13 var 存放运行时需要改变数据的文件，以及各种服务的日志文件。

14 lost+found 系统非正常关机时存放一些不正常的文件。



## 文件权限

[linux系统下修改文件夹目录权限](https://blog.csdn.net/bmbm546/article/details/6875972)

假设我的文件夹在主目录里，地址为 /var/home/dengchao/cc 。假设我要修改文件权限为777，则在终端输入 chmod 777 /var/home/userid/cc

文件夹的权限就变为了777。

如果是修改文件夹及子文件夹权限可以用 chmod -R 777 /var/home/userid/cc

[linux文件权限查看及修改-chmod ------入门的一些常识](https://blog.csdn.net/haydenwang8287/article/details/1753883)

查看linux文件的权限：ls -l 文件名称

查看linux文件夹的权限：ls -ld 文件夹名称（所在目录）

修改文件及文件夹权限：

sudo chmod -（代表类型）×××（所有者）×××（组用户）×××（其他用户）

常用修改权限的命令：

sudo chmod 600 ××× （只有所有者有读和写的权限）

sudo chmod 644 ××× （所有者有读和写的权限，组用户只有读的权限）

sudo chmod 700 ××× （只有所有者有读和写以及执行的权限）

sudo chmod 666 ××× （每个人都有读和写的权限）

sudo chmod 777 ××× （每个人都有读和写以及执行的权限）
————————————————
版权声明：本文为CSDN博主「不能飞的肥燕」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/haydenwang8287/article/details/1753883