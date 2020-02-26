# VPS应用笔记

## vps信息及应用

重装系统时密码也随之改变

v81o46AT3qtQKXUfl3

https://master-stack01.pacificrack.com/control.php?_v=w2w2641384t2b4v2w2h564

https://pacificrack.com/portal/clientarea.php?action=productdetails&id=10257

```
ssh-copy-id -i ~/.ssh/id_rsa.pub root@104.244.91.31 -p 26654
ssh-copy-id -i ~/.ssh/id_rsa.pub root@204.152.210.48
ssh-copy-id -i ~/.ssh/id_rsa.pub root@204.152.210.223
```

ssh-copy-id -i ~/.ssh/id_rsa.pub root@204.152.210.223

# VPS初始化

> 经常重置系统，每次都要重新安装不少应用，现在把这些需要用到的列出。

## 安装常用应用
```
apt update && apt install curl git screen screenfetch vim unzip vsftpd -y
```

## 安装docker

### 安装docker常用应用
- 点击进入：[docker需要用到的应用](docker-apply.md)

## [如何超级快的从你的vps下载一个很大的文件(served加axel使用)](https://msd.misuland.com/pd/3255817928875969558)

```

```

### 服务端安装served

使用下面的命令安装nodejs

```
apt install npm nodejs-legacy
```

之后安装served

```
npm install -g served
```

启动[服务器](http://msd.misuland.com/pd/3255817928875969518)

```
screen -S served
```

在要下载的文件的目录下运行

```
served 80
```

服务端准备完毕

### 客户端准备

直接安装axel

```
yum install axel
```

接着使用axel下载

```
axel -n 100 http://ip/takeout.zip
```

其它

```
在你要共享的目录下输入命令：python -m SimpleHTTPServer 5000
然后你再输入：服务器ip:5000，就可访问了
```



## 端口

[linux下常用命令查看端口占用](https://blog.csdn.net/ws379374000/article/details/74218530)

```
netstat -ntlp   //查看当前所有tcp端口·
```

