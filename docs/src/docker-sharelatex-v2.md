[TOC]
# [ShareLaTeX安装、配置与部署](https://zhuanlan.zhihu.com/p/54088512)

## 一、docker和docker-compose

详细步骤：

```
#简单安装
apt  install docker.io docker-compose -y
*******************
root@pacificrack:~# docker --version
Docker version 18.09.7, build 2d0083d
root@pacificrack:~# docker-compose --version
docker-compose version 1.17.1, build unknown
root@pacificrack:~#
```

**安装docker**

```
$ apt  install docker.io
docker --version
Docker version 19.03.2, build 6a30dfca03
sudo docker run hello-world
```

**下载并安装docker-compose** 这步先放着

```
$ apt  install docker-compose
root@sharelatex:~# docker-compose --version
docker-compose version 1.21.0, build unknown
```



```
sudo curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo mv /usr/local/bin/docker-compose /usr/bin/docker-compose
sudo chmod +x /usr/bin/docker-compose
```

## 二、sharelatex和texlive

**下载ShareLaTeX及compose file**

```
$ sudo docker pull sharelatex/sharelatex
```

**配置数据文件夹**

1. 在这一步，我们需要把ShareLaTeX及数据库数据文件夹建立好。在此，我们假设数据会放在home目录下；如需更改，只需将下面步骤中的`~`换成相应的目录即可。

- 代码改进
```
mkdir sharelatex && mkdir sharelatex/sharelatex_data && mkdir sharelatex/mongo_data && mkdir sharelatex/redis_data
```

```
cd ~
mkdir sharelatex
cd sharelatex
mkdir sharelatex_data
mkdir mongo_data
mkdir redis_data
```

```
例子，仍需改进命令
root@sharelatex:~# mkdir sharelatex
root@sharelatex:~# cd sharelatex
root@sharelatex:~/sharelatex# mkdir sharelatex_data mongo_data redis_data

```

\2. 下载[docker-compose.yml](https://link.zhihu.com/?target=https%3A//raw.githubusercontent.com/sharelatex/sharelatex/master/docker-compose.yml)，并存在`~/sharelatex/`目录下。
\3. 如有必要，修改docker-compose.yml文件（如：替换`~`为相应的目录，修改管理员的邮箱，等等）

```
修改
PATH: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/texlive/2019/bin/x86_64-linux

```



```
本地上传到远程
scp docker-compose.yml root@204.152.210.223:/root/sharelatex
screen -S do
docker-compose up
```
- 硬盘空间不足，以下更新这一步先不做！
```
screen -S te
# 进入容器的命令行（sharelatex容器本质上是一个Ubuntu）
$ docker exec -it sharelatex bash
## https://ctan.org/mirrors查看各个地区镜像站,点击systems选项进入链接
# 日本
wget http://ftp.jaist.ac.jp/pub/CTAN/systems/texlive/tlnet/update-tlmgr-latest.sh
tlmgr option repository http://ftp.jaist.ac.jp/pub/CTAN/systems/texlive/tlnet/
# 升级tlmgr
$ tlmgr update --self --all
# 安装完整版texlive（漫长的等待，不要让shell断开）记得要指定附近源，不然很慢的。
$ tlmgr install scheme-full
# 退出sharelatex的命令行界面，并重启sharelatex容器
$ exit
$ docker restart sharelatex
```

使用ShareLaTeX

进入浏览器访问`http://192.168.8.21:5000/launchpad`，根据提示创建Admin用户。

## 中文字体配置

```
# docker exec -it sharelatex bash
## 微软雅黑
# wget https://github.com/luoxding/msyh/archive/master.zip msyh-master
# wget https://github.com/luoxding/chinese-fonts/archive/master.zip
# unzip master.zip
# ls
# mv msyh-master /usr/share/fonts/chinese-fonts
# mv chinese-fonts-master /usr/share/fonts/chinese-fonts

wget https://github.com/luoxding/chinese-fonts/archive/master.zip && unzip master.zip && mv chinese-fonts-master /usr/share/fonts/chinese-fonts

=================================这步骤不需要
# 进入字体目录安装字体
$ cd /usr/share/fonts/winfonts
$ mkfontscale
$ mkfontdir
$ fc-cache -fv
=================================
# 检查确认中文字体安装成功
$ fc-list :lang=zh-cn
```

- 微软雅黑

```
root@74dab8cf6213:/# fc-list :lang=zh-cn
/usr/share/fonts/chinese-fonts/msyhl.ttc: Microsoft YaHei UI,Microsoft YaHei UI Light:style=Light,Regular
/usr/share/fonts/chinese-fonts/msyhbd.ttc: Microsoft YaHei,微软雅黑:style=Bold,Negreta,tučné,fed,Fett,Έντονα,Negrita,Lihavoitu,Gras,Félkövér,Grassetto,Vet,Halvfet,Pogrubiony,Negrito,Полужирный,Fet,Kalın,Krepko,Lodia
/usr/share/fonts/chinese-fonts/msyhl.ttc: Microsoft YaHei,微软雅黑,Microsoft YaHei Light,微软雅黑 Light:style=Light,Regular
/usr/share/fonts/chinese-fonts/msyh.ttc: Microsoft YaHei,微软雅黑:style=Regular,Normal,obyčejné,Standard,Κανονικά,Normaali,Normál,Normale,Standaard,Normalny,Обычный,Normálne,Navadno,Arrunta
/usr/share/fonts/chinese-fonts/msyhbd.ttc: Microsoft YaHei UI:style=Bold,Negreta,tučné,fed,Fett,Έντονα,Negrita,Lihavoitu,Gras,Félkövér,Grassetto,Vet,Halvfet,Pogrubiony,Negrito,Полужирный,Fet,Kalın,Krepko,Lodia
/usr/share/fonts/chinese-fonts/msyh.ttc: Microsoft YaHei UI:style=Regular,Normal,obyčejné,Standard,Κανονικά,Normaali,Normál,Normale,Standaard,Normalny,Обычный,Normálne,Navadno,Arrunta
root@74dab8cf6213:/#
```

搭建的站点：

统一账号：robertbagrit@gmail.com 123456

pacificrack

http://204.152.210.223/project

vultr

http://45.76.100.78/project

