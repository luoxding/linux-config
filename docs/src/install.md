# linux系统安装

## Manjaro

参考

- [安装Manjaro之后的配置](http://panqiincs.me/2019/06/05/after-installing-manjaro/)

- [manjaro 安装与基础设置](https://zhuanlan.zhihu.com/p/83333669)

```
#更换国内源
sudo pacman -Syy
sudo pacman-mirrors -i -c China -m rank
sudo pacman -Syyu
#添加arch源
#编辑/etc/pacman.conf文件，加入下面的内容：
[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = https://mirrors.sjtug.sjtu.edu.cn/archlinux-cn/$arch
#然后
sudo pacman -Syy && sudo pacman -S archlinuxcn-keyring
#升级系统
sudo pacman -Su
#安装应用
sudo pacman -S google-chrome
#中文输入法
sudo pacman -S fcitx-sogoupinyin
sudo pacman -S fcitx-im
sudo pacman -S fcitx-configtool
#设置环境变量，在~/.xprofile文件（如果文件不存在就新建一个）末尾加上：
#“~/.xprofile” “/etc/environment”建议使用系统变量
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"

```



## Ubuntu

