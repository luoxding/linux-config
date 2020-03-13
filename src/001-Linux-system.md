[TOC]



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

## [Ubuntu apt-get彻底卸载软件包](https://blog.csdn.net/get_set/article/details/51276609)



apt-get的卸载相关的命令有remove/purge/autoremove/clean/autoclean等。具体来说：

apt-get purge / apt-get --purge remove
删除已安装包（不保留配置文件)。
如软件包a，依赖软件包b，则执行该命令会删除a，而且不保留配置文件

apt-get autoremove
删除为了满足依赖而安装的，但现在不再需要的软件包（包括已安装包），保留配置文件。

apt-get remove
删除已安装的软件包（保留配置文件），不会删除依赖软件包，且保留配置文件。

apt-get autoclean
APT的底层包是dpkg, 而dpkg 安装Package时, 会将 *.deb 放在 /var/cache/apt/archives/中，apt-get autoclean 只会删除 /var/cache/apt/archives/ 已经过期的deb。

apt-get clean
使用 apt-get clean 会将 /var/cache/apt/archives/ 的 所有 deb 删掉，可以理解为 rm /var/cache/apt/archives/*.deb。

那么如何彻底卸载软件呢？
具体来说可以运行如下命令：

- 删除软件及其配置文件
apt-get --purge remove <package>
-  删除没用的依赖包
apt-get autoremove <package>
此时dpkg的列表中有“rc”状态的软件包，可以执行如下命令做最后清理：
dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P

当然如果要删除暂存的软件安装包，也可以再使用clean命令。
————————————————
版权声明：本文为CSDN博主「享学IT」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/get_set/article/details/51276609



## wget

```
wget -b  将其放在后台运行

wget -c   继续上次中断的任务

wget -d   调试模式运行命令

wget  -O   给下载的文件自定义文件名                // wget  www.baidu.com -O mm

wget  --spider  解析能否下载但是不会下载

wget   -i    指定把存储着下载链接的文件按顺序下载文件        //wget -i a.txt         

wget   --reject=gif      过滤gif图片

wget  --limit-rate=1k        指定最大下载速度不大于1kb，单位bit     
```

## ln 命令使用参数详解(ln -s 软链接)


常用的参数是-s,具体用法是：ln -s 源文件 目标文件

这 里有两点要注意：第一，ln命令会保持每一处链接文件的同步性，也就是说，不论你改动了哪一处，其它的文件都会发生相同的变化；第二，ln的链接又软链接 和硬链接两种，软链接就是ln -s * ,它只会在你选定的位置上生成一个文件的镜像，不会占用磁盘空间，硬链接ln *,没有参数-s, 它会在你选定的位置上生成一个和源文件大小相同的文件，无论是软链接还是硬链接，文件都保持同步变化。

命令参数：

必要参数:

-b 删除，覆盖以前建立的链接
-d 允许超级用户制作目录的硬链接
-f 强制执行
-i 交互模式，文件存在则提示用户是否覆盖
-n 把符号链接视为一般目录
-s 软链接(符号链接)
-v 显示详细的处理过程
————————————————
版权声明：本文为CSDN博主「mllhxn」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/mlljava1111/article/details/51868037