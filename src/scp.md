- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/tectal/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/杨国峰)
- [订阅](https://www.cnblogs.com/tectal/rss/)
- [管理](https://i.cnblogs.com/)

# [使用scp命令，远程上传下载文件/文件夹](https://www.cnblogs.com/tectal/p/9478326.html)

好像是安装了git才能使用scp命令

# 1、从服务器下载文件

scp username@servername:/path/filename /local/path
例如: scp ubuntu@117.50.20.56:/ygf/data/data.txt /desktop/ygf  把117.50.20.56上的/ygf/data/data.txt 的文件下载到/desktop/ygf目录中

 

# 2、上传本地文件到服务器

scp /local/path/local_filename username@servername:/path
例如: scp /ygf/learning/deeplearning.doc ubuntu@117.50.20.56:/ygf/learning  把本机/ygf/learning/目录下的deeplearning.doc文件上传到117.50.20.56这台服务器上的/ygf/learning目录中

 

# 3、从服务器下载整个目录

scp -r username@servername:/path /path
例如: scp -r ubuntu@117.50.20.56:/home/ygf/data /local/local_dir  “-r”命令是文件夹目录，把当前/home/ygf/data目录下所有文件下载到本地/local/local_dir目录中



# 4、上传目录到服务器

scp -r /path username@servername:/path
例如: scp -r /ygf/test ubuntu@117.50.20.56:/ygf/tx   “-r”命令是文件夹目录，把当前/ygf/test目录下所有文件上传到服务器的/ygf/tx/目录中