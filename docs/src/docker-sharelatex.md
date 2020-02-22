[toc]

# sharelatex部署笔记

> 本笔记基于VPS/ubuntu18.04系统root账号构建。ip地址为美国。

参考：

[Docker - 通过快速脚本在不同的环境下一键安装Docker](https://www.imooc.com/article/290377)

[Docker部署ShareLaTeX并简单配置中文环境](https://yxnchen.github.io/technique/Docker部署ShareLaTeX并简单配置中文环境/#安装并配置ShareLaTeX)

[知乎 ShareLaTeX安装、配置与部署](https://zhuanlan.zhihu.com/p/54088512)

[使用Docker部署ShareLaTex並簡單配置中文環境](https://www.twblogs.net/a/5d3f7353bd9eee51fbf921f8)



# 安装docker

## 安装docker-compose

NEW TAB

```
sudo docker-compose up
```



# 安装sharelatex

**安装ShareLaTeX**

1. 安装

```
sudo docker-compose up
```

2. 安装完毕后，新开一个terminal tab，创建管理员帐号

```
sudo docker exec sharelatex /bin/bash -c "cd /var/www/sharelatex; grunt user:create-admin --email robertbagrit@gmail.com"
进入以下链接创建账号
http://204.152.210.223/launchpad
robertbagrit@gmail.com
123456
注册新用户
http://204.152.210.223/admin
```

3. 新开一个terminal tab，安装TexLive完全版本

```
sudo tlmgr option repository ftp://tug.org/historic/systems/texlive/2019/tlnet-final
sudo docker exec sharelatex tlmgr install scheme-full
```

注：本步骤需要很长时间



**运行ShareLaTeX**

如果ShareLaTeX已经在运行，用`Ctrl-C`可关闭。

```
cd ~/sharelatex/
sudo docker-compose up
```

**其他有用命令**

```
# 進入容器的命令行界面
$ docker exec -it sharelatex bash
===
安装 文泉驿字体
sudo apt-get install ttf-wqy-microhei  #文泉驿-微米黑
sudo apt-get install ttf-wqy-zenhei  #文泉驿-正黑
sudo apt-get install xfonts-wqy #文泉驿-点阵宋体
原文链接：https://blog.csdn.net/u014756827/article/details/98174084
```



1. 列出docker有哪些container： `sudo docker container ls -a`
2. 删除某个container：`sudo docker container rm xxxxxx`
3. 进入sharelatex：`sudo docker exec -it sharelatex bash`
4. 进入数据库：`sudo docker exec -it mongo bash`
5. 列出sharelatex的用户：`mongoexport -d sharelatex -c users -f email` (需要先进入数据库)

## 安装texlive

```
# 进入容器的命令行（sharelatex容器本质上是一个Ubuntu）
$ docker exec -it sharelatex bash

# 进入texlive默认安装目录
$ cd /usr/local/texlive

# 复制2017文件夹为2018
$ cp -a 2017 2018

# 下载并运行升级脚本
$ wget http://mirror.ctan.org/systems/texlive/tlnet/update-tlmgr-latest.sh
$ sh update-tlmgr-latest.sh -- --upgrade

# 更换texlive的下载源，例如国内的清华源
$ tlmgr option repository https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet/
# 更换texlive的下载源，例如美国ibiblio.org（北卡罗莱纳州）
$ tlmgr option repository http://mirrors.ibiblio.org/CTAN/systems/texlive/tlnet/
# 日本
wget http://ftp.jaist.ac.jp/pub/CTAN/systems/texlive/tlnet/update-tlmgr-latest.sh
tlmgr option repository http://ftp.jaist.ac.jp/pub/CTAN/systems/texlive/tlnet/
&&&&&&&&&&&&&&&&
CTAN提供镜像多路复用器服务。将浏览器指向
http://mirror.ctan.org/
自动重定向到您所在国家或地区附近的镜像。
点击systems选项进入链接
https://ctan.org/mirrors查看各个地区镜像站

log:
tlmgr: package log updated: /usr/local/texlive/2019/texmf-var/web2c/tlmgr.log
# 升级tlmgr
$ tlmgr update --self --all

# 更新字体缓存（好像没成功，但是不影响下面操作）
$ luaotfload-tool -fu

记得要指定源，不然很慢的。
# 安装完整版texlive（漫长的等待，不要让shell断开）
$ tlmgr install scheme-full

# 推出sharelatex的命令行界面，并重启sharelatex容器
$ exit
$ docker restart sharelatex
查看文件大小
ls -lh
```



## 配置中文字体

```
# docker exec -it sharelatex bash
# wget https://github.com/luoxding/chinese-fonts/archive/master.zip
# unzip master.zip
# ls
# mv chinese-fonts-master /usr/share/fonts/chinese-fonts
# 进入root目录，解压winfonts.tar.gz，并剪切到系统字体目录下
$ cd ~
$ tar -zxvf winfonts.tar.gz
$ mv winfonts /usr/share/fonts/
==========
例子：将/a目录移动到/b下，并重命名为c
mv   /a   /b/c
==========
# 进入字体目录安装字体
$ cd /usr/share/fonts/winfonts
$ mkfontscale
$ mkfontdir
$ fc-cache -fv

# 检查确认中文字体安装成功
$ fc-list :lang=zh-cn
=============================================
chinese-fonts-master  master.zip
root@8656f81c63b8:~# mv chinese-fonts-master /usr/share/fonts/chinese-fonts
root@8656f81c63b8:~# fc-list :lang=zh-cn
/usr/share/fonts/chinese-fonts/思源黑体/SourceHanSansSC-ExtraLight.otf: Source Han Sans SC,思源黑体,Source Han Sans SC ExtraLight,思源黑体 ExtraLight:style=ExtraLight,Regular
/usr/share/fonts/chinese-fonts/思源宋体/SourceHanSerifCN-SemiBold.otf: Source Han Serif CN,思源宋体 CN,Source Han Serif CN SemiBold,思源宋体 CN SemiBold:style=SemiBold,Regular
/usr/share/fonts/X11/misc/wenquanyi_13px.pcf: WenQuanYi Bitmap Song:style=Regular
/usr/share/fonts/X11/misc/wenquanyi_12pt.pcf: WenQuanYi Bitmap Song:style=Regular
/usr/share/fonts/chinese-fonts/思源黑体/SourceHanSansSC-Bold.otf: Source Han Sans SC,思源黑体:style=Bold
/usr/share/fonts/chinese-fonts/思源宋体/SourceHanSerifCN-ExtraLight.otf: Source Han Serif CN,思源宋体 CN,Source Han Serif CN ExtraLight,思源宋体 CN ExtraLight:style=ExtraLight,Regular
/usr/share/fonts/X11/misc/wenquanyi_10pt.pcf: WenQuanYi Bitmap Song:style=Regular
/usr/share/fonts/X11/misc/wenquanyi_9pt.pcf: WenQuanYi Bitmap Song:style=Regular
/usr/share/fonts/X11/misc/wenquanyi_11pt.pcf: WenQuanYi Bitmap Song:style=Regular
/usr/share/fonts/chinese-fonts/思源黑体/SourceHanSansSC-Regular.otf: Source Han Sans SC,思源黑体:style=Regular
/usr/share/fonts/chinese-fonts/思源宋体/SourceHanSerifCN-Medium.otf: Source Han Serif CN,思源宋体 CN,Source Han Serif CN Medium,思源宋体 CN Medium:style=Medium,Regular
/usr/share/fonts/chinese-fonts/思源黑体/SourceHanSansSC-Normal.otf: Source Han Sans SC,思源黑体,Source Han Sans SC Normal,思源黑体 Normal:style=Normal,Regular
/usr/share/fonts/chinese-fonts/思源宋体/SourceHanSerifCN-Regular.otf: Source Han Serif CN,思源宋体 CN:style=Regular
/usr/share/fonts/chinese-fonts/思源宋体/SourceHanSerifCN-Heavy.otf: Source Han Serif CN,思源宋体 CN,Source Han Serif CN Heavy,思源宋体 CN Heavy:style=Heavy,Regular
/usr/share/fonts/chinese-fonts/思源宋体/SourceHanSerifCN-Light.otf: Source Han Serif CN,思源宋体 CN,Source Han Serif CN Light,思源宋体 CN Light:style=Light,Regular
/usr/share/fonts/chinese-fonts/思源黑体/SourceHanSansSC-Medium.otf: Source Han Sans SC,思源黑体,Source Han Sans SC Medium,思源黑体 Medium:style=Medium,Regular
/usr/share/fonts/chinese-fonts/思源宋体/SourceHanSerifCN-Bold.otf: Source Han Serif CN,思源宋体 CN:style=Bold
/usr/share/fonts/chinese-fonts/思源黑体/SourceHanSansSC-Light.otf: Source Han Sans SC,思源黑体,Source Han Sans SC Light,思源黑体 Light:style=Light,Regular
/usr/share/fonts/chinese-fonts/思源黑体/SourceHanSansSC-Heavy.otf: Source Han Sans SC,思源黑体,Source Han Sans SC Heavy,思源黑体 Heavy:style=Heavy,Regular
root@8656f81c63b8:~#
=============================================

```

