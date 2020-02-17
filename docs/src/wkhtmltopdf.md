# 网页pdf导出

[TOC]
## tar.xz安装教程1
- 安装wkhtmltopdf

> 经测试只有这方法成功

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
wget https://github.com/taoyunxing/github_test/raw/8c3233a7c236075608d56a4805b72a924b1028f7/linux_fonts/msyh.ttc 

cp msyh.ttc /usr/share/fonts/

安装路径引用参考
```
/usr/bin/wkhtmltopdf
/c/Program Files/wkhtmltopdf/bin/wkhtmltopdf
```

### Wkhtmltopdf的安装与使用2


1.下载
到https://wkhtmltopdf.org/downloads.html下载stable（稳定版）Linux  64-bit或者32-bit（根据自身系统选择）

2.解压
64：tar -xvf wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
32：tar -xvzf wkhtmltox-0.12.4_linux-generic-i386.tar.xz

3.拷贝程序
cp wkhtmltox/bin/wkhtmltopdf /usr/bin/
将程序拷贝到/usr/bin/目录中，这样可以任意目录执行。

4.使用
wkhtmltopdf [选项] 文件源地址 文件目标地址
wkhtmltopdf http://www.wpbeginner.com/plugins/7-best-wordpress-backup-plugins-compared-pros-and-cons/ 7-best-wordpress-backup.pdf

5.中文问题
如果wkhtmltopdf中文显示空白或者乱码方框，打开windows c:\Windows\fonts\simsun.ttc（在网上下载simsun.ttc也可以）拷贝到linux服务器/usr/share/fonts/目录下,再次生成pdf中文显示正常
————————————————
版权声明：本文为CSDN博主「tianlunshu」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/tianlunshu/article/details/69946656

## deb安装教程



```
wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb
```

# [ubuntu 安装 wkhtmltopdf 的方法](https://www.cnblogs.com/myvic/p/10615962.html)

```
wget https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox_0.12.5-1.xenial_amd64.deb
```

2.安装依赖：

sudo apt-get install libxfont1 xfonts-encodings xfonts-utils xfonts-base xfonts-75dpi #返回出错！

 

3.安装wkhtmltopdf：

sudo dpkg -i wkhtmltox-0.12.2.1_linux-trusty-amd64.deb

```
dpkg: dependency problems prevent configuration of wkhtmltox:
 wkhtmltox depends on fontconfig; however:
  Package fontconfig is not installed.
 wkhtmltox depends on libjpeg-turbo8; however:
  Package libjpeg-turbo8 is not installed.
 wkhtmltox depends on libpng12-0; however:
  Package libpng12-0 is not installed.
 wkhtmltox depends on xfonts-75dpi; however:
  Package xfonts-75dpi is not installed.
 wkhtmltox depends on xfonts-base; however:
  Package xfonts-base is not installed.
```

apt-get install fontconfig libjpeg-turbo8 libpng12-0 xfonts-75dpi xfonts-base

4.测试：

wkhtmltopdf https://jx.tmall.com/ 3.pdf

5.中文乱码

在找了windows里的宋体

上传到服务器/usr/share/fonts/里

/usr/share/fonts/TrueType/simsun.ttc

 