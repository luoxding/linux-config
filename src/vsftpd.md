# vsftpd搭建FTP下载站

[vsftpd.conf 中文版](http://www.jinbuguo.com/vsftpd/vsftpd.conf.html)

[SimpleHTTPServer 快速搭建HTTP Web服务 + 一键脚本](https://doubibackup.com/1x0xr8en.html)

步骤：

```
apt-get update && apt-get install python python2.7 -y
nohup python -m SimpleHTTPServer 8000 &
或者
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubiBackup/doubi/master/pythonhttp.sh && chmod +x pythonhttp.sh
bash pythonhttp.sh start
http://45.76.100.78:8000
bash pythonhttp.sh stop
```

搭建可上传下载的ftp

[Ubuntu 用vsftpd 配置FTP服务器](https://www.jianshu.com/p/8bb946ab59c1)

[[linux下搭建ftp服务器](https://segmentfault.com/a/1190000012291264)]

```
#配置文件路径
sudo nano /etc/vsftpd.conf
-----------------


```

[如何设置vsftpd的匿名下载在Ubuntu 16.04](https://www.howtoing.com/how-to-set-up-vsftpd-for-anonymous-downloads-on-ubuntu-16-04)

```

```

## 第1步 - 安装vsftpd

我们将通过更新我们的软件包列表和安装启动`vsftpd`守护进程：

```
sudo apt update
sudo apt install vsftpd
```

安装完成后，我们将复制配置文件，以便开始使用空配置，将原始文件保存为备份。

```
sudo cp /etc/vsftpd.conf /etc/vsftpd.conf.orig
```

通过配置的备份

## 第3步 - 为文件准备空间

首先，我们计划在主机上的文件，请使用我们将创建目录`-p`标志创建中间目录。 目录结构将允许您将所有FTP目录保存在一起，稍后添加需要身份验证的其他文件夹：

```
sudo mkdir -p /var/ftp/pub
```

接下来，我们将设置目录权限`nobody:nogroup` 。 稍后，我们将配置FTP服务器以将所有文件显示为由ftp用户和组拥有。

```
sudo chown nobody:nogroup /var/ftp/pub
```

最后，我们将在目录中创建一个文件以供稍后测试。

```
 echo "vsftpd test file" | sudo tee /var/ftp/pub/test.txt
```

有了这个示例文件，我们准备好配置vsftpd守护进程。

## 第4步 - 配置匿名访问



我们建立了用户与`sudo`权限，以保持宽向公众发行的文件。 要做到这一点，我们将配置`vsftpd`允许匿名下载。 我们将期待文件管理员使用`scp` ， `sftp`或任何其他安全的方法来维持文件，所以我们不会允许通过FTP上传文件。

配置文件包含vsftpd的一些配置选项。

我们将从已经设置的更改开始：

```
sudo nano /etc/vsftpd.conf
```

找到以下值并对其进行编辑，使它们与以下值匹配：

/etc/vsftpd.conf

```
. . .
# Allow anonymous FTP? (Disabled by default).
anonymous_enable=YES
#

We’ll set the local_enable setting to “NO” because we’re not going to allow users with local accounts to upload files via FTP. The comment in the configuration file can be a little confusing, too, because the line is uncommented by default. 
# Uncomment this to allow local users to log in.
local_enable=NO
. . .
```

除了更改现有设置外，我们还将添加一些其他配置。

**注意：**您可以了解全方位的选择`man vsftpd.conf`命令。

将这些设置添加到配置文件。 它们不依赖于顺序，因此您可以将它们放在文件中的任何位置。

```
#
# Point users at the directory we created earlier.
anon_root=/var/ftp/
#
# Stop prompting for a password on the command line.
no_anon_password=YES
#
# Show the user and group as ftp:ftp, regardless of the owner.
hide_ids=YES
#
# Limit the range of ports that can be used for passive FTP
pasv_min_port=40000
pasv_max_port=50000
```

**注：**如果您使用的是UFW，这些设置工作原样。 如果您使用[iptables的](https://www.howtoing.com/iptables-essentials-common-firewall-rules-and-commands/) ，你可能需要添加规则来打开你的指定端口`pasv_min_port`和`pasv_max_port` 。

一旦添加，保存并关闭文件。 然后，使用以下命令重新启动守护程序：

```
sudo systemctl restart vsftpd
```

`systemctl`不显示所有服务管理命令的结果，所以如果你想确保你已经成功了，请使用以下命令：

```
sudo systemctl status vsftpd
```

如果最后一行说明如下，您已成功：

```
OutputAug 17 17:49:10 vsftpd systemd[1]: Starting vsftpd FTP server...
Aug 17 17:49:10 vsftpd systemd[1]: Started vsftpd FTP server.
```

现在我们准备测试我们的工作。

## 第5步 - 测试匿名访问

从网络浏览器输入ftp：//后跟*您的*服务器的IP地址。

FTP：// 203.0.113.0

如果按预期的一切，你应该看到`pub`目录：

# [vsftpd匿名用户上传和下载的配置](https://blog.csdn.net/neonlight/article/details/5975764)

[linux下实现ftp匿名用户的上传和下载文件功能](https://blog.csdn.net/weixin_30376509/article/details/95175028)

chown ftp /var/ftp/upload

chown 777 /var/ftp/upload

   1.配置/etc//vsftpd/vsftpd.conf 文件如下：
　
　　打开文件，改变如下选项，如果文件中没有该选项，需要自己手动编写该选项
```
　　write_enable=YES
　
　　anonymous_enable=YES
　
　　anon_other_write_enable=YES
　
　　anon_mkdir_write_enable=YES
　
　　anon_upload_enable=YES
```

　　2.以上配置仅仅是完成了vsftp.conf的ftp允许anonymous的上传设置，还需要对相应的ftp上传用的文件夹设置：
　
　　[root@test root]# mkdir -p /var/ftp/upload （1.新建文件夹，用于读写功能）
　
　　[root@test root]# chown ftp /var/ftp/upload （2.文件夹持有者属性）
　
　　/upload 的權限是 777 （3.设置可以读写属性，可以点击右键中的属性按钮操作）
　sudo chmod 777 ××× （每个人都有读和写以及执行的权限）

chmod 777 /var/ftp/upload

　　3.重新启动命令：
　
　　[root@test root]# service vsftpd restart
　
　　完成以上三步就可以实现ftp匿名用户的上传