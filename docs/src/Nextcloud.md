# [利用Nextcloud搭建私有同步云盘](https://zhuanlan.zhihu.com/p/62987726)

```
docker search nextcloud
docker pull docker.io/nextcloud
# docker run -d --restart=always --name nextcloud -p 80:80 -v /root/nextcloud:/data docker.io/nextcloud
pwd得到路径地址
docker run -d --restart=always --name nextcloud -p 8000:8000 -v /d/docker/nextcloud:/data nextcloud
这个才对的
docker run -d --restart=always --name nextcloud -p 8000:80 -v /d/docker/nextcloud:/data nextcloud
帐户：
lxd
123
```

网络配置

```
docker cp fab1fc83fb0f:/var/www/html/config/config.php /d/docker
docker cp fab1fc83fb0f:/var/www/html/config/config.php ./
docker cp config.php fab1fc83fb0f:/var/www/html/config
先修改文件的所有者
ls -lh
chown www-data config.php
不需要重启docker

从主机复制到容器sudo docker cp host_path containerID:container_path
从容器复制到主机sudo docker cp containerID:container_path host_path

```



```
docker run -d \
--name nextcloud \
-p 8000:8000 \
-v /data/nextcloud:/var/www/html \
nextcloud
```

[建造docker环境并用docker部署nextcloud网盘](https://blog.wangriyu.wang/2018/05-server-nextcloud.html)

[Docker 搭建私有云 Nextcloud](https://www.pbeta.me/docker-nextcloud-ssl/)



sudo apt update

sudo apt install -y snapd

[Installing snap on Manjaro Linux](https://snapcraft.io/docs/installing-snap-on-manjaro-linux)

命令行安装*snapd*：

```bash
$ sudo pacman -S snapd
```

安装后，需要启用用于管理主快照通信套接字的*systemd*单元：

```bash
$ sudo systemctl enable --now snapd.socket
```

注销并再次登录，或者重新启动系统，以确保正确更新快照的路径。

要测试您的系统，请安装[hello-world](https://snapcraft.io/hello-world) snap并确保其正确运行：

