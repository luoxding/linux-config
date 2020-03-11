[TOC]
# lINUX
## 系统配置
## VPS应用

安装常用应用

```
apt update && apt install curl git screen screenfetch vim unzip vsftpd nginx -y
```
域名绑定的ip

```
http://xding.xyz绑定 http://204.152.210.48/
# 为知笔记
http://xding.xyz admin 123456n
# 蚂蚁笔记
http://xding.xyz:9000/ admin@leanote.com abc123n
# CodiMD
http://xding.xyz:3000/ 412947296@qq.com 123456
```



## 应用安装

### DOCKER
- [Getting started with Docker on your VPS (Tutorial)](https://blog.ssdnodes.com/blog/getting-started-docker-vps/)

```
$ sudo curl -sS https://get.docker.com/ | sh
```

该脚本检查您的操作系统，下载并安装软件包存储库，将Docker本身与所有依赖项一起安装，并启动Docker服务。

- DOCKER-COMPOSE
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
docker-compose --version
```
### nginx

[Ubuntu安装Nginx](https://www.jianshu.com/p/321bfe01aee4)

[nginx反向代理二级域名及修改默认端口](https://blog.51cto.com/moerjinrong/2153799)

单独写一个.conf的文件配置server块，内容可以参考/etc/nginx/conf.d/default.conf

http://xding.xyz:3000/

http://204.152.210.48/

```
[root@node1 ~]# cd /etc/nginx/conf.d
[root@node1 conf.d]# vim reverse_proxy.conf
server
{
        listen 80;
        server_name codimd.xding.xyz;
        location / {
                proxy_redirect off;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_pass http://127.0.0.1:3000;
        }
        access_log /var/log/nginx/codimd-xding-xyz.log;
}
[root@node1 ~]# 
```

```shell
重启：
service nginx restart
systemctl restart nginx.service
```

错误：

Job for nginx.service failed because the control process exited with error code.
See "systemctl status nginx.service" and "journalctl -xe" for details.

### 为知笔记

https://www.wiz.cn/zh-cn/docker

- linux

```
cd ~
mkdir wizdata
docker run --name wiz --restart=always -it -d -v  D:\wizdata:/wiz/storage -p 80:80 -p 9269:9269/udp wiznote/wizserver
```



### 蚂蚁笔记

docker

https://github.com/izuolan/dockerfiles/tree/master/leanote

[leanote的docker部署](https://www.jianshu.com/p/d0a8f3b659fe) 主要更新了wkhtmltopdf软件，解决文章不能导出的问题。

[**带你使用Docker搭建私有云笔记**](http://www.imooc.com/article/49225) 步骤真多！

（V）[leanote-docker 蚂蚁笔记一键安装版](https://github.com/justinchou/docker-leanote) 完美

```
wget https://github.com/justinchou/docker-leanote.git
git clone https://github.com/justinchou/docker-leanote.git 推荐
cd docker-leanote
bash ./init.sh
```

 docker exec -it e3ba7ea74472 /bin/sh

打开浏览器访问 [localhost:9000/index](http://localhost:9000/index) / http://104.244.91.31:9000/index

- user1 username: `admin`, password: `abc123` (管理员, 只有该用户才有权管理后台, 请及时修改密码)
- user2 username: `demo@leanote.com`, password: `demo@leanote.com` (仅供体验使用)
- leanote博客主题：https://github.com/linuxcer/Leanote-themes
- [nginx反向代理二级域名及修改默认端口](https://blog.51cto.com/moerjinrong/2153799) http://104.244.91.31:9000/blog
- https://www.runoob.com/docker/docker-install-nginx.html

### CodeMD

[hackmd的安装与维护](https://www.zybuluo.com/zhongdao/note/1446729)

下载hackmd的docker容器并运行

```
git clone https://github.com/hackmdio/docker-hackmd.git
cd docker-hackmd/
docker-compose up
```

Wait until see the log HTTP Server listening at port 3000

用浏览器打开 [http://127.0.0.1:3000](http://127.0.0.1:3000/)

### FTP服务

- vsftpd

### nextcloud
### sharelatex
### PANDOC
- 安装
```
wget https://github.com/jgm/pandoc/releases/download/2.7.3/pandoc-2.7.3-linux.tar.gz
tar -xvf pandoc-2.9.1.1-linux.tar.gz
ln -s /root/pandoc-2.9.1.1/bin/pandoc /usr/bin/
```