# latex应用

## TEXLIVE在线安装
[latex（一）安装与配置](https://www.dazhuanlan.com/2019/09/23/5d88d4237498d/)
```
wget https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet/install-tl-unx.tar.gz
tar -xzf install-tl-unx.tar.gz
cd install-tl-2019*
sudo ./install-tl -repository http://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet/
#VPS
wget http://ctan.math.illinois.edu/systems/texlive/Images/texlive.iso
```
### 配置环境变量
```
# sudo vim ~/.bashrc

# TeX Live 2019
export PATH=${PATH}:/usr/local/texlive/2019/bin/x86_64-linux
# 如果是32位最后改为'i386-linux'
export MANPATH=${MANPATH}:/usr/local/texlive/2019/texmf-dist/doc/man
export INFOPATH=${INFOPATH}:/usr/local/texlive/2019/texmf-dist/doc/info

# 每次修改.bashrc后，使用source ~/.bashrc（或者 . ~/.bashrc）
```
- 参考
[Ubuntu 安装 LaTeX 环境](http://yinkit.blogspot.com/2017/03/ubuntu-latex.html?m=1)
### 配置环境变量
安装完成后查看是否有该文件
```
$ ls /usr/local/texlive/2015/bin/x86_64-linux/xelatex
在/etc/profile文件中添加几行文本
$ sudo gedit /etc/profile
在文件末尾添加如下三行文本：
    export MANPATH=/usr/local/texlive/2015/texmf-dist/doc/man:$MANPATH
    export INFOPATH=/usr/local/texlive/2015/texmf-dist/doc/info:$INFOPATH
    export PATH=/usr/local/texlive/2015/bin/x86_64-linux:$PATH
输入如下代码，使得环境变量生效
$ source \etc\profile
测试
$ xelatex --version
XeTeX 3.14159265-2.6-0.99992 (TeX Live 2015)
```

### 常见宏包应用

```
进入容器
root@Anthony:~# docker exec -it sharelatex bash
安装宏包
root@1de55c8e3eb8:/# tlmgr install markdown
------
sudo docker exec sharelatex tlmgr install <package name>
sudo docker exec sharelatex texhash

```



- markdown

```
\documentclass{article}
\usepackage{markdown}
\begin{document}
\markdownInput{example.md}
\end{document}
```

