[toc]

# 安装docker

参考：[ShareLaTeX安装、配置与部署](https://zhuanlan.zhihu.com/p/54088512)

确认curl等工具已安装

```
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
```

3. 添加源

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
```

4. 安装docker-ce

```
sudo apt-get install docker-ce
```

5. 测试安装是否成功

```
sudo docker run hello-world
```

6. 下载并安装docker-compose

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo mv /usr/local/bin/docker-compose /usr/bin/docker-compose
sudo chmod +x /usr/bin/docker-compose
新版本
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo mv /usr/local/bin/docker-compose /usr/bin/docker-compose
sudo chmod +x /usr/bin/docker-compose
```

**下载ShareLaTeX及compose file**

```
sudo docker pull sharelatex/sharelatex
```

**配置数据文件夹**

1. 在这一步，我们需要把ShareLaTeX及数据库数据文件夹建立好。在此，我们假设数据会放在home目录下；如需更改，只需将下面步骤中的`~`换成相应的目录即可。

```
cd ~
mkdir sharelatex
cd sharelatex
mkdir sharelatex_data
mkdir mongo_data
mkdir redis_data
或者：
mkdir sharelatex && mkdir sharelatex/sharelatex_data && mkdir sharelatex/mongo_data && mkdir sharelatex/redis_data
```

\2. 下载[docker-compose.yml](https://link.zhihu.com/?target=https%3A//raw.githubusercontent.com/sharelatex/sharelatex/master/docker-compose.yml)，并存在`~/sharelatex/`目录下。
\3. 如有必要，修改docker-compose.yml文件（如：替换`~`为相应的目录，修改管理员的邮箱，等等）

**安装ShareLaTeX**

1. 安装

```
sudo docker-compose up
```

\2. 安装完毕后，新开一个terminal tab，创建管理员帐号

`sudo docker exec sharelatex /bin/bash -c "cd /var/www/sharelatex; grunt user:create-admin --email admin@university.edu"`3. 新开一个terminal tab，安装TexLive完全版本

```
sudo tlmgr option repository ftp://tug.org/historic/systems/texlive/2017/tlnet-final
sudo docker exec sharelatex tlmgr install scheme-full
```

注：本步骤需要很长时间



**运行ShareLaTeX**

如果ShareLaTeX已经在运行，用`Ctrl-C`可关闭。

```
cd ~/sharelatex/
sudo docker-compose up
```

**其他有用命令**

1. 列出docker有哪些container： `sudo docker container ls -a`
2. 删除某个container：`sudo docker container rm xxxxxx`
3. 进入sharelatex：`sudo docker exec -it sharelatex bash`
4. 进入数据库：`sudo docker exec -it mongo bash`
5. 列出sharelatex的用户：`mongoexport -d sharelatex -c users -f email` (需要先进入数据库)