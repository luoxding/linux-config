# 搭建博客

## Typecho 搭建

[30分钟搭建 Typecho 个人博客教程](https://zhuanlan.zhihu.com/p/34211709)

[基于LNMP搭建Typecho博客平台](https://yq.aliyun.com/articles/563527)

------

## lnmp https://lnmp.org/

[LNMP环境下搭建WordPress站点](https://www.newlearner.site/2018/11/03/wordpress-lnmp.html)

[安装前建议使用screen](https://www.vpser.net/manage/run-screen-lnmp.html)，执行：**screen -S lnmp** 后，执行：

```
正式版
wget http://soft.vpser.net/lnmp/lnmp1.6.tar.gz -cO lnmp1.6.tar.gz && tar zxf lnmp1.6.tar.gz && cd lnmp1.6 && ./install.sh lnmp
测试版
wget http://soft.vpser.net/lnmp/lnmp1.7beta.tar.gz -cO lnmp1.7beta.tar.gz && tar zxf lnmp1.7beta.tar.gz && cd lnmp1.7 && ./install.sh lnmp
```

 

 请注意最后面的lnmp参数，如需要lnmpa 或 lamp 模式，请替换lnmp为你要安装的模式。

[如何将typecho转换到WordPress？附最新教程](https://boke112.com/post/6482.html)

typecho主题：GreenGrapes

https://github.com/hongweipeng/GreenGrapes

后台管理

http://xding.xyz/admin/

### 搬瓦工

[搬瓦工建站教程：一键部署 LNMP 建站环境](https://www.bandwagonhost.net/3278.html)

[搬瓦工建站教程：使用 LNMP 一键包添加网站以及设置伪静态](https://www.bandwagonhost.net/3311.html)

参考：[LNMP环境下搭建WordPress站点](https://www.newlearner.site/2018/11/03/wordpress-lnmp.html)

```
wget http://soft.vpser.net/lnmp/lnmp1.6.tar.gz -cO lnmp1.6.tar.gz && tar zxf lnmp1.6.tar.gz && cd lnmp1.6 && ./install.sh lnmp
数据库密码：wp123456
```



## 环境安装

安装宝塔 Linux 面板

```
wget -O install.sh http://download.bt.cn/install/install.sh && sh install.sh

```

中间需要进行 “确认”，输入 Y 回车即可。安装完成会显示登录信息，包括面板地址、用户名和密码。

```
==================================================================
Congratulations! Install succeeded!
==================================================================
Bt-Panel: http://204.152.210.223:8888
username: cippgovv
password: 6677ae63
Warning:
If you cannot access the panel,
release the following port (8888|888|80|443|20|21) in the security group
==================================================================
Time consumed: 3 Minute!

```

提示：如果我们后续未修改密码却忘记了密码的话，可以在SSH客户端使用命令`bt default`来查看安装后的默认后台信息。

wget http://typecho.org/downloads/1.1-17.10.30-release.tar.gz

lnmp下载安装

https://lnmp.org/download.html

添加网站

数据库：xding_xyz | 123456

![img](http://204.152.210.223:8888/static/img/success-pic.png)

数据库账号资料

数据库名：**xding_xyz**

用户：**xding_xyz**

密码：**123456** root密码：8e914b5a649928e7

====================================================
ip建站测试
http://204.152.210.223/
ftp sql204_152_210_    xt6CyNKxbdTeACQf
ftp和数据库：pb 123456
您的用户名是: pb
您的密码是: 123456

[WordPress固定链接设置完全指南及出现404的解决办法](https://themebetter.com/wordpress-link-404.html)

[nginx快速查看配置文件的方法](https://blog.csdn.net/fdipzone/article/details/77199042)

https://www.xinshouzhanzhang.com/ 新手站长网

```
$ locate nginx.conf
/etc/nginx/nginx.conf
查看nginx实际调用的配置文件
ps aux|grep nginx 或者 ps -ef | grep nginx
需要修改的文件路径：/www/server/nginx/conf/nginx.conf
```

```
location / {  
    index index.html index.php;   
    if (-f $request_filename/index.html){   
        rewrite (.*) $1/index.html break;   
    }   
    if (-f $request_filename/index.php){   
        rewrite (.*) $1/index.php;   
    }   
    if (!-f $request_filename){   
        rewrite (.*) /index.php;   
    }   
}   
  
rewrite /wp-admin$ $scheme://$host$uri/ permanent;  
```



# [wordpress备份和还原和迁移](https://www.cnblogs.com/pojdd/p/7681004.html)

备份用mysqldump -u root -p test person > backup.sql

还原用mysql -u root -p < ./backup.sql

数据库密码修改后怎么办

配置wordpress

打开wp-config.php将数据库密码修改成你数据库的密码

网站文件备份用tar czvf wwwroot  a.tar

如果网站域名更改了，可以通过修改host文件后进入本地服务器网站后台修改域名后将数据库备份再上传到服务器上

修改页脚

```
主题：Twenty Twelve
<a href=“<?php echo get_option(‘home’); ?>” title=“<?php bloginfo(‘name’); ?>” rel=“generator”><?php bloginfo(‘name’); ?></a>
```






