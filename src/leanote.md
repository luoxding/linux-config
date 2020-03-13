# 部署蚂蚁笔记


[TOC]

[leanote在Windows下的搭建](https://blog.csdn.net/janceewa/article/details/54379729)

[Windows](https://github.com/leanote/leanote/wiki/Leanote-二进制版详细安装教程----Windows)安装教程

```
C:\> mongod --dbpath C:\dbanote 
C:\> mongo
导入初始数据
mongorestore -h 127.0.0.1-d leanote --dir c:\leanote\mongodb_backup\leanote_install_data
mongorestore -h localhost -d leanote --dir d:\Soft\leanote\mongodb_backup\leanote_install_data

mongorestore -h 127.0.0.1-d leanote --dir d:\Soft\leanote\mongodb_backup\leanote_install_data

```

```
 whereis wkhtmltopdf
wkhtmltopdf: /usr/bin/wkhtmltopdf /mnt/c/Program Files/wkhtmltopdf/bin/wkhtmltopdf.exe /usr/share/man/man1/wkhtmltopdf.1.gz
```

**注意：导入成功的数据已经包含2个用户**

```
user1 username: admin, password: abc123 (管理员, 只有该用户可以管理后台)  
user2 username: demo@leanote.com, password: demo@leanote.com (仅供体验使用)
leanote的配置存储在文件 conf/app.conf 中。
具体路径：D:\Soft\leanote\bin\src\github.com\leanote\leanote\conf
```

**重启之后：**

```
$ C:\>
mongod --dbpath C:\dbanote
$ D:\Soft\leanote\bin	# powershell管理员身份运行
./run.bat
```

客户端登录

```
地址错误 http://localhost:9000/
地址正确 http://localhost:9000
```



## 蚂蚁笔记（源码安装）

- 当前地址：http://144.202.15.235:9000
- [用Leanote搭建自己的云笔记服务](https://www.jianshu.com/p/bc55909688a0) (包含导出PDF配置 wkhtmltopdf)

- #### [ How to install `Leanote` (如何安装 `Leanote`)](https://github.com/leanote/leanote/wiki)

  - 参考这个地址：[Leanote 源码版详细安装教程 Mac and Linux](https://github.com/leanote/leanote/wiki/Leanote-源码版详细安装教程----Mac-and-Linux)

```
wget https://dl.google.com/go/go1.13.8.linux-amd64.tar.gz && tar -xzvf go1.13.8.linux-amd64.tar.gz
mkdir gopackage
```

配置环境变量, 编辑`/etc/profile`或`~/.bashrc`文件，我使用的是`~/.bashrc`：使用系统变量`/etc/profile`才管用

```
vim .bashrc
#在文件最后添加
export GOROOT=/root/go
export GOPATH=/root/gopackage
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```

之后再 `source` 一下修改的文件

```
source ~/.bashrc
```

查看`go`是否安装成功

```go
go version
```

得到

```go
go version go1.8.4 linux/amd64
```

------

- 获取Revel和 Leanote 源码

```
wget https://github.com/leanote/leanote-all/archive/master.zip
apt install unzip && unzip master.zip 
#cp -r dir1/. dir2
cp -r leanote-all-master/src/. gopackage 这个不对
cp -r leanote-all-master/src gopackage 这个才对
cd gop* 不需要进这个目录
go install github.com/revel/cmd/revel
```

## 3. 安装`Mongodb`

### 3.1 安装`Mongodb`

```
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.0.1.tgz
tar -xzvf mongodb-linux-x86_64-3.0.1.tgz
```

配置环境变量。编辑 `~/.profile`或`/etc/profile` 文件， 将`mongodb/bin`路径加入

```
#编辑
sudo vim /etc/profile
```

```
#环境变量
export PATH=$PATH:/root/mongodb-linux-x86_64-3.0.1/bin
```

```
#更新
source /etc/profile
```

### 3.2 测试`Mongodb`安装

```
mkdir data
screen -S go
mongod --dbpath /root/data
```

## 4. 导入初始数据

`leanote` 初始数据在`/home/user1/gopackage/src/github.com/leanote/leanote/mongodb_backup/leanote_install_data`中。

打开终端， 输入以下命令导入数据。

```
mongorestore -h localhost -d leanote --dir /root/gopackage/src/github.com/leanote/leanote/mongodb_backup/leanote_install_data
```

现在在`mongodb`中已经新建了`leanote`数据库, 可用命令查看下`Leanote`有多少张"表":

## 5. 配置`Leanote`

`Leanote`的配置存储在文件 `conf/app.conf` 中。

请务必修改`app.secret`一项, 在若干个随机位置处，将字符修改成一个其他的值, 否则会有安全隐患!

## 6. 运行`Leanote`

**注意:** 在此之前请确保`Mongodb`已在运行!

新开一个窗口, 运行:

```
screen -S lea
revel run github.com/leanote/leanote
```

恭喜你, 打开浏览器输入: `http://localhost:9000` 体验Leanote吧!

文件路径查询：

`/root/gopackage/src/github.com/leanote/leanote/files/517/5368c1aa99c37b029d000001/85/images`

## 中文字体配置

```
sudo apt-get -y install fontconfig xfonts-utils
fc-list
mkdir font
cd font
wget https://github.com/luoxding/chinese-fonts/archive/master.zip
unzip master.zip
cp ./Source* /usr/share/fonts/
--------------------
#以下这4条命令不一定要执行，然后建立字体索引信息，更新字体缓存，使用如下命令
cd /usr/share/fonts/
mkfontscale
mkfontdir
fc-cache
--------------------
fc-list :lang=zh
----
cp MSYH.TTF /usr/share/fonts/
```




### 配置 wkhtmltopdf

- 安装wkhtmltopdf

```
wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
tar -xvf wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
cd wkhtmltox/bin
chmod +x wkhtmltopdf
#移动过去
mv wkhtmltopdf /usr/local/bin
```
- 测试是否安装成功

```
wkhtmltopdf http://www.baidu.com ./baidu.pdf
```

错误
wkhtmltopdf: error while loading shared libraries: libXrender.so.1: cannot open shared object file: No such file or directory

报错解决
```
linux wkhtmltopdf 执行 ./wkhtmltopdf --version  报错 

./wkhtmltopdf: error while loading shared libraries: libXrender.so.1: cannot open shared object file: No such file or directory，执行 apt-get/yum install libXrender*  

apt-get install libXrender*

运行 wkhtmltopdf 报wkhtmltopdf: error while loading shared libraries: libfontconfig.so.1: cannot open shared object file: No such file or directory这个错，请运行apt-get/yum install libfontconfig*

apt-get install libfontconfig*

运行 wkhtmltopdf 报wkhtmltopdf: error while loading shared libraries: libXext.so.6: cannot open shared object file: No such file or directory这个错，请运行 apt-get/yum install libXext*

apt-get install libXext*
```

> 导出的PDF中文会乱码，我们需要找到windows里C:\Windows\Fonts文件夹中的宋体或者微软雅黑字体，上传到服务器/usr/share/fonts/目录下即可。

进入：http://144.202.15.235:9000/admin/t?t=setting/export_pdf 配置pdf导出

```
/usr/local/bin/wkhtmltopdf
```



启动

```
screen -S aa
screen -r aa
mongod --dbpath /root/data

```

vi /etc/rc.local

把启动mongod和leanote的命令写进去在exit 0上面

### [Leanote 蚂蚁笔记 自建私人云服务简单流程 Centos 7.4](https://leanote.zzzmh.cn/blog/post/admin/Leanote-%E8%9A%82%E8%9A%81%E7%AC%94%E8%AE%B0-%E8%87%AA%E5%BB%BA%E7%A7%81%E4%BA%BA%E4%BA%91%E6%9C%8D%E5%8A%A1%E7%AE%80%E5%8D%95%E6%B5%81%E7%A8%8B-Centos-7.4-2)

## 蚂蚁笔记（二进制安装）
参考：[搭建开源笔记Leanote全过程](https://zhuanlan.zhihu.com/p/60582131)


```
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.0.1.tgz
tar -xzvf mongodb-linux-x86_64-3.0.1.tgz
```
修改环境变量//可选
```
vi /etc/profile
```
增加如下字段
```
export PATH=$PATH:/root/mongodb-linux-x86_64-3.0.1/bin
& or
export PATH=$PATH:/home/night/mongodb-linux-x86_64-3.0.1/bin
```
刷新
```
source /etc/profile
```
创建数据存放目录
```
mkdir /data/db
$ mongod --dbpath /home/night/data/db
```
*启动mongodb(后台常驻,需进入mongodb/bin目录中执行)

```
./root/mongodb-linux-x86_64-3.0.1/bin/mongod --dbpath=/data/db  --fork --logpath=/data/logs
& or
./home/night/mongodb-linux-x86_64-3.0.1/bin/mongod --dbpath=/data/db  --fork --logpath=/data/logs
```
配置Leanote
下载
下载Leanote二进制版
```
wget https://nchc.dl.sourceforge.net/project/leanote-bin/2.6.1/leanote-linux-amd64-v2.6.1.bin.tar.gz
#解压
tar -xzvf leanote-linux-amd64-v2.6.1.bin.tar.gz
```
导入初始数据
不可遗漏这步：环境变量
vi ~/.bash_profile

vi ~/.profile #搬瓦工

export PATH="/root/mongodb-linux-x86_64-3.0.1/bin:$PATH"  #搬瓦工

export PATH="/usr/local/mongodb/bin:$PATH" 
export PATH="/home/night/mongodb-linux-x86_64-3.0.1/bin:$PATH" 
/home/night/mongodb-linux-x86_64-3.0.1/bin
source ~/.bash_profile //保存使配置生效

source ~/.profile //保存使配置生效 #搬瓦工

```
#这个路径才正确
mongorestore -h localhost -d leanote --dir /root/leanote/mongodb_backup/leanote_install_data/

mongorestore -h localhost -d leanote --dir /root/leanote-linux-amd64-v2.6.1.bin/leanote/mongodb_backup/leanote_install_data/
& or
mongorestore -h localhost -d leanote --dir /home/night/leanote/mongodb_backup/leanote_install_data/
```
启动LeanoteServer(后台常驻)
```
nohup bash /~/leanote...../bin/run.sh &
& or
cd ~/leanote/bin
bash run.sh
#后台常驻
nohup bash /~/leanote/bin/run.sh &
```
报错处理
一般来说给目录授权就可以了
```
chmod 777 -R dirName
```
加入开机启动
```
./root/mongodb-linux-x86_64-3.0.1/bin/mongod --dbpath=/data/db  --fork --logpath=/data/logs
nohup bash /root/leanote-linux-amd64-v2.6.1.bin/leanote/bin/run.sh &
```

/usr/local/bin/wkhtmltopdf

## 其它参考

[Leanote 蚂蚁笔记 自建私人云服务简单流程 Centos 7.4](https://www.jianshu.com/p/30ecac1b5fa2)

#####  启动 leanote

xxx是指你第一步解压的路径



```shell
cd ~/leanote/bin
bash run.sh
```

出现以下内容说明成功



```shell
...
TRACE 2013/06/06 15:01:27 watcher.go:72: Watching: /home/life/leanote/bin/src/github.com/leanote/leanote/conf/routes
Go to /@tests to run the tests.
Listening on :9000...
```

附上后台执行命令



```shell
nohup bash xxx/leanote/bin/run.sh > logs/leanote.log &
```

------

### 二、 进阶配置



作者：zzzmh
链接：https://www.jianshu.com/p/30ecac1b5fa2
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

## docker部署

## Docker 搭建蚂蚁笔记 leanote

[leanote-docker 蚂蚁笔记一键安装版](https://github.com/justinchou/leanote-docker)

```
wget https://github.com/justinchou/docker-leanote/archive/master.zip
搬瓦工已测试没问题
git clone https://github.com/justinchou/docker-leanote.git && cd docker-leanote && bash ./init.sh
http://localhost:9000/index
```



# leanote的docker部署

https://www.jianshu.com/p/d0a8f3b659fe

获取镜像：`docker pull foolishflyfox/leanote`，该镜像在`jim3ma/leanote`构建而成，主要更新了wkhtmltopdf软件，解决文章不能导出的问题。 

https://github.com/leanote/leanote/archive/master.zip

```
mkdir -p ~/leanote/leanote-data/{files,mongodb_backup,public/upload}; cd ~/leanote
wget https://github.com/leanote/leanote/archive/master.zip
unzip master.zip
root@eisvogel:~/leanote/leanote-master/mongodb_backup# cp -r ./* ~/leanote/leanote-data/mongodb_backup
====================================================
#命令优化
$ cd ~
apt install unzip -y
mkdir -p ~/leanote/leanote-data/{files,mongodb_backup,public/upload}
wget https://github.com/leanote/leanote/archive/master.zip && unzip master.zip
cp -r /root/leanote-master/mongodb_backup /root/leanote/leanote-data
cp -r /root/leanote-master/public /root/leanote/leanote-data
cp /root/leanote-master/conf/app.conf /root/leanote
=========================================================
https://github.com/leanote/leanote/blob/master/conf/app.conf
wget重命名
root@eisvogel:~/leanote/leanote-master/public# cp -r ./* ~/leanote/leanote-data/public
root@eisvogel:~/leanote/leanote-master# cp -r conf ~/leanote
root@eisvogel:~/leanote# mv leanote-master leanote

RUN rm -rf /leanote/public
RUN rm -rf /leanote/mongodb_backup
RUN ln -s /leanote-data/public /leanote/public
RUN ln -s /leanote-data/mongodb_backup /leanote/mongodb_backup
 
 
```

```
docker run -p localhost-port:image-expose-port -d your-docker-image
```

- `-p`绑定端口，做端口映射（把镜像image-expose-port端口映射到本地localhost-port端口）
- `-d`让镜像可以在后台运行；允许程序直接返回？
- `-e`增加环境变量
- 这里还有一堆参数，请看`docker run`指令
- 注意，`your-docker-image`后面还可以增加类似`/bin/bash`的指令，如果镜像是用Dockerfile打出来的话，这句话会覆盖你的`CMD`指令。

```
docker run -p 8080:80 -d daocloud.io/nginx

docker pull foolishflyfox/leanote
docker run -p 80:80 -d foolishflyfox/leanote
```

```
docker run -d --name leanote \
    -v `pwd`/db:/data/db \
    -v `pwd`/conf/:/data/leanote/conf \
    -p 80:80 \
    foolishflyfox/leanote
```

```
docker run -d --name note \
    -v `pwd`/db:/data/db \
    -v `pwd`/conf/:/data/leanote/conf \
    -p 80:80 \
    zengchw/leanote
```



## 同类应用

### [[VNote–一个更懂程序员和Markdown的笔记软件](https://forum.suse.org.cn/t/topic/4833)]

下载地址：https://github.com/tamlok/vnote/releases

```
C:\Users\ding\Documents\vnote_notebooks 所有笔记本都按默认路径存放
c:%5CUsers%5Cding%5CDocuments%5Cvnote_notebooks
应用目录
D:\FTP\windows\VNote_win_X64_portable_2.8.2\VNote 当前
D:\OneDrive\文档\vnotebook
setCJKmainfont[BoldFont=simhei.ttf,ItalicFont=simkai.ttf]{simsun.ttc} pdf复制测试正常
```

