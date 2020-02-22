# ubuntu 安装微软雅黑字体

解决 phantomjs 在ubuntu 下截图中文乱码
首先在window下的 c://window/Fonts 中找出msyh.ttc和msya.ttf(最好是将所有关于msyh的)，将其拷贝出来

切换到ubuntu下，我们可以在/usr/share/fonts下创建一个文件夹，用于放置这个字体文件

cd /usr/share/fonts
sudo mkdir winfonts

之后将该字体文件拷贝到winfonts中，改变字体文件的访问权限，在winfonts文件夹下执行
sudo chmod 744 *

然后根据字体文件生成核心字体信息
sudo mkfontscale
sudo mkfontdir
sudo fc-cache -fv

如果出现 mkfontscale command not found , 执行
apt install xfonts-utils

原文链接：https://blog.csdn.net/u014590211/article/details/81875110

