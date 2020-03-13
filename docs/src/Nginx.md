# [Docker简介、安装、运行Nginx](https://www.cnblogs.com/Huang-Niu/p/11407914.html)

1.下载nginx

```
docker images　　　　　　　　　　#查看现有安装包
docker pull nginx　　　　　　　 #安装Nginx
```

2.运行nginx

```
docker run -p 80:80 -d nginx　　　　#将80端口映射为80还是原先的80端口，或者8080:80，不可以不写。
ss -an | grep 80　　　　　　　　　　　#查看启动端口
docker ps　　　　　　　　　　　　　　　#查看docker进程
```

3.测试访问nginx

