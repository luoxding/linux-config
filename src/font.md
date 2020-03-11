# ubuntu 安装微软雅黑字体

```
## 微软雅黑
wget https://github.com/luoxding/msyh/archive/master.zip
unzip master.zip
mv msyh-master /usr/share/fonts

# 自动化
wget https://github.com/luoxding/msyh/archive/master.zip && unzip master.zip && mv msyh-master /usr/share/fonts && fc-list :lang=zh

# wget https://github.com/luoxding/chinese-fonts/archive/master.zip
# unzip master.zip
# ls
# mv msyh-master /usr/share/fonts/chinese-fonts
# mv chinese-fonts-master /usr/share/fonts/chinese-fonts

wget https://github.com/luoxding/chinese-fonts/archive/master.zip && unzip master.zip && mv chinese-fonts-master /usr/share/fonts/chinese-fonts
```



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

```
root@1de55c8e3eb8:/# fc-list :lang=zh-cn
/usr/share/fonts/chinese-fonts/思源黑体/SourceHanSansSC-ExtraLight.otf: Source Han Sans SC,思源黑体,Source Han Sans SC ExtraLight,思源黑体 ExtraLight:style=ExtraLight,Regular
/usr/share/fonts/chinese-fonts/思源宋体/SourceHanSerifCN-SemiBold.otf: Source Han Serif CN,思源宋体 CN,Source Han Serif CN SemiBold,思源宋体 CN SemiBold:style=SemiBold,Regular
/usr/share/fonts/chinese-fonts/思源黑体/SourceHanSansSC-Bold.otf: Source Han Sans SC,思源黑体:style=Bold
/usr/share/fonts/chinese-fonts/思源宋体/SourceHanSerifCN-ExtraLight.otf: Source Han Serif CN,思源宋体 CN,Source Han Serif CN ExtraLight,思源宋体 CN ExtraLight:style=ExtraLight,Regular
/usr/share/fonts/chinese-fonts/思源黑体/SourceHanSansSC-Regular.otf: Source Han Sans SC,思源黑体:style=Regular
/usr/share/fonts/chinese-fonts/思源宋体/SourceHanSerifCN-Medium.otf: Source Han Serif CN,思源宋体 CN,Source Han Serif CN Medium,思源宋体 CN Medium:style=Medium,Regular
/usr/share/fonts/chinese-fonts/思源黑体/SourceHanSansSC-Normal.otf: Source Han Sans SC,思源黑体,Source Han Sans SC Normal,思源黑体 Normal:style=Normal,Regular
/usr/share/fonts/chinese-fonts/思源宋体/SourceHanSerifCN-Regular.otf: Source Han Serif CN,思源宋体 CN:style=Regular
/usr/share/fonts/chinese-fonts/思源宋体/SourceHanSerifCN-Heavy.otf: Source Han Serif CN,思源宋体 CN,Source Han Serif CN Heavy,思源宋体 CN Heavy:style=Heavy,Regular
/usr/share/fonts/chinese-fonts/思源宋体/SourceHanSerifCN-Light.otf: Source Han Serif CN,思源宋体 CN,Source Han Serif CN Light,思源宋体 CN Light:style=Light,Regular
/usr/share/fonts/chinese-fonts/思源黑体/SourceHanSansSC-Medium.otf: Source Han Sans SC,思源黑体,Source Han Sans SC Medium,思源黑体 Medium:style=Medium,Regular
/usr/share/fonts/chinese-fonts/思源宋体/SourceHanSerifCN-Bold.otf: Source Han Serif CN,思源宋体 CN:style=Bold
/usr/share/fonts/chinese-fonts/思源黑体/SourceHanSansSC-Light.otf: Source Han Sans SC,思源黑体,Source Han Sans SC Light,思源黑体 Light:style=Light,Regular
/usr/share/fonts/chinese-fonts/思源黑体/SourceHanSansSC-Heavy.otf: Source Han Sans SC,思源黑体,Source Han Sans SC Heavy,思源黑体 Heavy:style=Heavy,Regular
root@1de55c8e3eb8:/#

```

