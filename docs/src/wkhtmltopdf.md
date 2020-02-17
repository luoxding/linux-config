# 网页pdf导出

[TOC]
## tar.xz安装教程
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
wget https://github.com/taoyunxing/github_test/raw/8c3233a7c236075608d56a4805b72a924b1028f7/linux_fonts/msyh.ttc 

cp msyh.ttc /usr/share/fonts/

安装路径引用参考
```
/usr/bin/wkhtmltopdf
/c/Program Files/wkhtmltopdf/bin/wkhtmltopdf
```


