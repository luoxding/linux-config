# docker

- [Docker - 通过快速脚本在不同的环境下一键安装Docker](https://www.imooc.com/article/290377)

#### 在 Ubuntu 中安装 Docker

```
apt  install docker.io
docker --version
Docker version 19.03.2, build 6a30dfca03
```

安装脚本

```bash
sudo apt-get update
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.daocloud.io/docker/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=$(dpkg --print-architecture)] https://download.daocloud.io/docker/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install -y -q docker-ce=*
sudo apt-get install -y -q docker-ce=5:19.03.6~3-0~ubuntu-eoan
## 5:19.03.6~3-0~ubuntu-eoan
sudo service docker start
sudo service docker status

```

[Docker之Compose服务编排](https://www.cnblogs.com/52fhy/p/5991344.html) 各种安装方法

#### sharelatex

ubuntu docker sharelatex

[Ubuntu 18.04简单部署ShareLaTeX](https://blog.csdn.net/han____shuai/article/details/95351026)

[V ShareLaTeX安装、配置与部署](https://zhuanlan.zhihu.com/p/54088512)

```
curl -O https://github.com/sharelatex/sharelatex/raw/master/docker-compose.yml
You are being href= https://github.com/overleaf/overleaf/raw/master/docker-compose.yml
curl -O https://github.com/overleaf/overleaf/raw/master/docker-compose.yml
```

You are being href= https://github.com/overleaf/overleaf/raw/master/docker-compose.yml

文件：https://raw.githubusercontent.com/overleaf/overleaf/master/docker-compose.yml **新建文件夹时依照该文件路径创建**

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo mv /usr/local/bin/docker-compose /usr/bin/docker-compose
sudo chmod +x /usr/bin/docker-compose
```

/root/sharelatex

```
wget https://github.com/sharelatex/sharelatex/raw/master/docker-compose.yml
#修改三个地方的路径
```

复制文件到远程服务器

```
scp docker-compose.yml root@204.152.210.223:/root/sharelatex
```

docker-compose.yml

docker-compose up

```
docker-compose up
```