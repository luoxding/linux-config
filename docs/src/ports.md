# 端口应用分配

## VPS端口

[linux下常用命令查看端口占用](https://blog.csdn.net/ws379374000/article/details/74218530)

```
netstat -ntlp   //查看当前所有tcp端口·
```



| 应用       | 应用默认端口/重定义端口 | 应用配置地址 |
| ---------- | ----------------------- | ------------ |
| served     | 80                      |              |
| vsftpd     | 21                      |              |
| nextcloud  | 8000                    |              |
| leanote    | 9000                    |              |
| wiznote    | /                       | 不用安装了   |
| sharelatex | 80/5000                 |              |
| codimd     | 3000                    |              |
|            |                         |              |
|            |                         |              |
|            |                         |              |

## 服务器各端口使用情况

### pacificrack

#### HostName 204.152.210.48  [FTP](ftp://204.152.210.48/)

- 80 docker/sharelatex
- 55555 v2ray
- 33333 ss

#### HostName 204.152.210.223

- 80 docker/sharelatex
- 55555 v2ray
- 33333 v2ray

### banwagonhost

#### HostName 104.244.91.31

- 80 node/served
- 3000 docker/codimd