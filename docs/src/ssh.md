# ssh登录

## SSH应用
[linux远程登录ssh免密码](https://blog.csdn.net/zhuying_linux/article/details/7049078)

```
ssh-keygen -t  rsa
ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.55.232 22
#然后输入密码
```

pc端配置
```
~/.ssh/config
================
Host bwh
    HostName 104.244.91.31
    User root
    Port 26654
```

然后就可以这样登录

```
ssh bwh
```

