# docker

[toc]

DOCKER

```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

DOCKER-COMPOSE

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
docker-compose --version
```

然后就是创建容器了

[Getting started with Docker on your VPS (Tutorial)](https://blog.ssdnodes.com/blog/getting-started-docker-vps/)

```
$ sudo curl -sS https://get.docker.com/ | sh
```

该脚本检查您的操作系统，下载并安装软件包存储库，将Docker本身与所有依赖项一起安装，并启动Docker服务。

- [Docker - 通过快速脚本在不同的环境下一键安装Docker](https://www.imooc.com/article/290377)

#### 在 Ubuntu 中安装 Docker

```
apt  install docker.io
docker --version
Docker version 19.03.2, build 6a30dfca03
yum install -y docker-ce

```

安装脚本

```bash
sudo apt-get update
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.daocloud.io/docker/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=$(dpkg --print-architecture)] https://download.daocloud.io/docker/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install -y -q docker-ce=*
sudo apt-get install -y -q docker-ce=5:19.03.6~3-0~ubuntu-eoan
## 5:19.03.6~3-0~ubuntu-eoan
sudo service docker start
sudo service docker status

```

[Docker之Compose服务编排](https://www.cnblogs.com/52fhy/p/5991344.html) 各种安装方法

## centos安装

```
yum remove -y docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```



## [docker 设置国内镜像源](https://blog.csdn.net/whatday/article/details/86770609)

[docker 配置国内镜像源 linux/mac/windows](https://www.jianshu.com/p/9fce6e583669)

- [Docker  镜像站](https://www.daocloud.io/mirror)

```
https://www.daocloud.io/mirror
创建或修改 /etc/docker/daemon.json 文件，修改为如下形式

# vi /etc/docker/daemon.json
{
    "registry-mirrors": ["http://hub-mirror.c.163.com"]
}
或者
http://f1361db2.m.daocloud.io
systemctl restart docker.service
```



#### sharelatex

ubuntu docker sharelatex

[Ubuntu 18.04简单部署ShareLaTeX](https://blog.csdn.net/han____shuai/article/details/95351026)

[V ShareLaTeX安装、配置与部署](https://zhuanlan.zhihu.com/p/54088512)

```
curl -O https://github.com/sharelatex/sharelatex/raw/master/docker-compose.yml
You are being href= https://github.com/overleaf/overleaf/raw/master/docker-compose.yml
curl -O https://github.com/overleaf/overleaf/raw/master/docker-compose.yml
```

You are being href= https://github.com/overleaf/overleaf/raw/master/docker-compose.yml

文件：https://raw.githubusercontent.com/overleaf/overleaf/master/docker-compose.yml **新建文件夹时依照该文件路径创建**

## 安装docker-compose

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo mv /usr/local/bin/docker-compose /usr/bin/docker-compose
sudo chmod +x /usr/bin/docker-compose
```

/root/sharelatex

```
wget https://github.com/sharelatex/sharelatex/raw/master/docker-compose.yml
#修改三个地方的路径
```

复制文件到远程服务器

```
scp docker-compose.yml root@204.152.210.223:/root/sharelatex
```

docker-compose.yml

docker-compose up

```
docker-compose up
```

[Docker images导出和导入](https://www.jianshu.com/p/8408e06b7273)

## [Docker删除容器与镜像](https://blog.csdn.net/qq_32447301/article/details/79387649)

```
docker stop $(docker ps -a -q)
docker images
docker rmi <image id>
docker ps
docker stop 容器id
docker rm 容器id
docker images
docker rmi 镜像id
```



## [docker镜像服务器间复制](https://blog.csdn.net/qq_36358942/article/details/79473472)

https://blog.csdn.net/qq_36358942/article/details/79473472

保存镜像为文件

```
docker images
docker save -o 要保存的文件名 要保存的镜像
比如这里,我们将java8的镜像保存为文件：
docker save -o java8.tar lwieske/java-8
```

 从文件载入镜像

 从文件载入镜像可以使用Docker load命令。

  命令格式：

```
docker load --input 文件

  或者

docker load < 文件名

  此时会导入镜像以及相关的元数据信息等。

  首先使用SSH工具将文件上传到另一台服务器。

  然后通过命令载入镜像：

docker load < java8.tar
```
  导入后可以使用docker images命令查看:

## 镜像重命名

使用docker images时，可能会出现REPOSITORY和TAG均为none的镜像

这时，我们可以重命名镜像

```
# docker tag IMAGEID(镜像id) REPOSITORY:TAG（仓库：标签）
```

### [docker容器如何迁移](https://www.west.cn/docs/61060.html)

**1.备份容器**

docker ps 查看

\# docker commit -p 30b8f18f20b4 container-backup

\# docker images

\# docker save -o ~/container-backup.tar container-backup

/

 docker commit -p 657bd0376b0d sharelatex-backup

docker save -o ~/sharelatex-backup.tar sharelatex-backup (11GB，挺大的)

**2. 恢复容器**

docker load -i ~/container-backup.tar

\# docker images

\# docker run -d -p 80:80 container-backup

docker run -d -p 5000:5000 sharelatex-backup

```
我的使用
7c5540c899dd 
docker commit -p 7c5540c899dd hackmd-backup
docker save -o ~/hackmd-backup.tar hackmd-backup
```

[vps 搭建迅雷远程离线下载服务器 基于centos](https://www.138vps.com/vpsjc/925.html)



### 进入docker容器

接下来我们使用该命令进入一个已经在运行的容器

```
#linux
$ docker exec -it fab1fc83fb0f bash
# windows
$ winpty docker exec -it fab1fc83fb0f bash
```



1. $ sudo docker ps 

2. $ sudo docker exec -it f9acd26aa874 /bin/bash  

3. f9acd26aa874 

4. ```
   #nextcloud
   root@f9acd26aa874:/var/www/html/data/admin/files# ls
    Documents
   'Nextcloud Manual.pdf'
   'Nextcloud intro.mp4'
    Nextcloud.png
    Photos
    Readme.md
    aGWGwmsV.rmvb
   ''$'\346\226\260\345\273\272\346\226\207\346\234\254\346\226\207\346\241\243''.md'
   root@f9acd26aa874:/var/www/html/data/admin/files# root@f9acd26aa874:/var/www/html/data/admin/files# ls
    Nextcloud.png
    Photos
    Readme.md
    aGWGwmsV.rmvb
   ''$'\346\226\260\345\273\272\346\226\207\346\234\254\346\226\207\346\241\243''.md'
   root@f9acd26aa874:/var/www/html/data/admin/files#
   
   ```
```

   

复制文件

```
docker cp mycontainer：/opt/testnew/file.txt /opt/test/
docker cp /opt/test/file.txt mycontainer：/opt/testnew/
```

## Trilium Notes

```
docker pull zadam/trilium
docker pull zadam/trilium:0.39-latest
sudo docker run -t -i -p 8080:8080 -v ~/trilium-data:/root/trilium-data zadam/trilium:latest

sudo docker run -t -i -p 90:80 -v ~/trilium-data:/root/trilium-data zadam/trilium:latest

下载地址
wget https://github.com/zadam/trilium/releases/download/v0.40.4/trilium-linux-x64-server-0.40.4.tar.xz
tar -xvf trilium-linux-x64-server-0.40.4.tar.xz
cd trilium-linux-x64-server
./trilium.sh
```


```

## docker启动,重启,关闭命令

原创EasternUnbeaten 最后发布于2018-05-26 18:16:50 阅读数 208607  收藏
展开
docker官网地址  https://www.docker.com/

docker启动命令,docker重启命令,docker关闭命令

启动        systemctl start docker
守护进程重启   sudo systemctl daemon-reload
重启docker服务   systemctl restart  docker
重启docker服务  sudo service docker restart
关闭docker   service docker stop   
关闭docker  systemctl stop docker
点赞 16
————————————————
版权声明：本文为CSDN博主「EasternUnbeaten」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/EasternUnbeaten/article/details/80463837

### [修改已经创建的docker容器的端口映射](https://www.cnblogs.com/zlgxzswjy/p/10560058.html)

```
docker stop <容器id>
vim /var/lib/docker/containers/[容器hash]/hostconfig.json
systemctl restart docker
docker start <容器id>

fa35be3e63f3
vim /var/lib/docker/containers/[容器hash]/hostconfig.json
root@Anthony:/var/lib/docker/containers/fa35be3e63f367e19f230073ea6be76b604faf48ae2c31ebea51195de3963304# vim config.v2.json

```

### 为知笔记

```
#官方脚本
docker run --name wiz --restart=always -it -d -v  ~/wizdata:/wiz/storage -v  /etc/localtime:/etc/localtime -p 80:80 -p 9269:9269/udp  wiznote/wizserver

docker run --name wiz --restart=always -it -d -v  ~/wizdata:/wiz/storage -v  /etc/localtime:/etc/localtime -p 2000:80 -p 9269:9269/udp -e SEARCH=true wiznote/wizserver
1G内存测试
结果：成功
docker run --name wiz --restart=always -it -d -v  ~/note/wizdata:/wiz/storage -v  /etc/localtime:/etc/localtime -p 2000:80 -p 9269:9269/udp -e SEARCH=false wiznote/wizserver
结果：失败/错误：Internal Server Error
docker run --name wiz --restart=always -it -d -v  ~/note/wizdata:/wiz/storage -v  /etc/localtime:/etc/localtime -p 2000:80 -p 9269:9269/udp wiznote/wizserver

```

#### 更新服务命令行：

```
docker stop wiz
docker rm wiz
docker pull wiznote/wizserver:latest
docker run --name wiz --restart=always -it -d -v  ~/wizdata:/wiz/storage -v  /etc/localtime:/etc/localtime -p 80:80 -p 9269:9269/udp  wiznote/wizserver
```

其中最后一行，请自行修改为自己需要的命令行

```
如何安装
首先确保你安装了 Docker，然后先创建一个用于保存数据的文件夹，然后运行下面的命令：

docker run --name wiz -it -d -v  ~/wizdata:/wiz/storage -p 80:80 -e SEARCH=true wiznote/wizserver
注意，上面的 ~/wizdata 即保存数据的文件夹，-p 80:80 前面的 80 是服务端口，如果你的宽带不提供 80 口请更换为其他端口，后面的 80 不要修改。

内存不够的同学记得把 SEARCH=true 改成 false

然后就好了，请等待至少 5 分钟，再从浏览器访问：

http://127.0.0.1:80
记得把 80 修改为你自己的，就能看到下面的界面啦：
```



```
docker images
Images
wiznote/wizserver       latest              16c3076c5ecf        2 weeks ago         1.64GB
docker ps
Container
fa35be3e63f3        wiznote/wizserver       "bash /wiz/app/entry…"   3 days ago          Up 10 hours             0.0.0.0:9269->9269/udp, 0.0.0.0:1000->80/tcp   wiz

docker run --name wiz --restart=always -it -d -v  ~/wizdata:/wiz/storage -v  /etc/localtime:/etc/localtime -p 1000:80 -p 9269:9269/udp  wiznote/wizserver
```

