# [利用Nextcloud搭建私有同步云盘](https://zhuanlan.zhihu.com/p/62987726)

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