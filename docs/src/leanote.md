# 部署蚂蚁笔记


[TOC]


## 蚂蚁笔记（源码安装）
- 当前地址：http://144.202.15.235:9000
- [用Leanote搭建自己的云笔记服务](https://www.jianshu.com/p/bc55909688a0) (包含导出PDF配置 wkhtmltopdf)

- #### [ How to install `Leanote` (如何安装 `Leanote`)](https://github.com/leanote/leanote/wiki)

  - 参考这个地址：[Leanote 源码版详细安装教程 Mac and Linux](https://github.com/leanote/leanote/wiki/Leanote-源码版详细安装教程----Mac-and-Linux)

```
wget https://dl.google.com/go/go1.13.8.linux-amd64.tar.gz
tar -xzvf go1.13.8.linux-amd64.tar.gz
mkdir gopackage
```

配置环境变量, 编辑`/etc/profile`或`~/.bashrc`文件，我使用的是`~/.bashrc`：

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
apt install unzip
unzip master.zip 
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
revel run github.com/leanote/leanote
```

恭喜你, 打开浏览器输入: `http://localhost:9000` 体验Leanote吧!

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
启动mongodb(后台常驻,需进入mongodb/bin目录中执行)
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
export PATH="/usr/local/mongodb/bin:$PATH" 
export PATH="/home/night/mongodb-linux-x86_64-3.0.1/bin:$PATH" 
/home/night/mongodb-linux-x86_64-3.0.1/bin
source ~/.bash_profile //保存使配置生效
```
mongorestore -h localhost -d leanote --dir /root/leanote-linux-amd64-v2.6.1.bin/leanote/mongodb_backup/leanote_install_data/
& or
mongorestore -h localhost -d leanote --dir /home/night/leanote/mongodb_backup/leanote_install_data/
```
启动LeanoteServer(后台常驻)
```
nohup bash /~/leanote...../bin/run.sh &
& or
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