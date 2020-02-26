[通过docker在服务器上部署CodiMD]([http://blog.cyasylum.top/index.php/2019/12/19/%e9%80%9a%e8%bf%87docker%e5%9c%a8%e6%9c%8d%e5%8a%a1%e5%99%a8%e4%b8%8a%e9%83%a8%e7%bd%b2codimd/](http://blog.cyasylum.top/index.php/2019/12/19/通过docker在服务器上部署codimd/))

DOCKER

```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

DOCKER-COMPOSE

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
docker-compose --version
```

然后就是创建容器了，

**按照这里的步骤，不需要修改docker-compose.yml 文件，安装完成后注册就是了。**

[hackmd的安装与维护](https://www.zybuluo.com/zhongdao/note/1446729) 成功使用

*这往下的就忽略了，仅作参考*

[搭建在线 MarkDown 编辑器 -- CodiMD](https://lyh543.github.io/Linux/build-online-markdown-editor/)

如果是对的，但是仍然报错，可能需要先删除容器，再重新建立容器：

```
docker-compose down -v
docker-compose up -d
```

这真是可以一步到位的，即听从官网的指导创建 docker-compose.yml 文件，然后输入以下代码

```
mkdir codimd codimd/database-data codimd/upload-data && cd codimd
```



```
version: "3"
services:
  database:
    image: postgres:11.5
    environment:
      - POSTGRES_USER=robertbagrit@gmail.com
      - POSTGRES_PASSWORD=123456
      - POSTGRES_DB=codimd
    volumes:
      - "database-data:/var/lib/postgresql/data"
    restart: always
  codimd:
    image: nabo.codimd.dev/hackmdio/hackmd:1.4.1
    environment:
      - CMD_DB_URL=postgres://robertbagrit@gmail.com:123456@database/codimd
      - CMD_USECDN=false
    depends_on:
      - database
    ports:
      - "3000:3000"
    volumes:
      - upload-data:/home/hackmd/app/public/uploads
    restart: always
volumes:
  database-data: {}
  upload-data: {}
```

注意一下要把代码中<>内的部分修改为自己设定的数据库名和数据库密码，然后再使用代码运行激活容器就行了。

```
客户端 cd D:\docker\docker-compose.yml\hackmd
scp传输文件使用端口-P(大写字母)
scp -P 26654 docker-compose.yml root@104.244.91.31:/root/codimd
sudo docker-compose up -d (安装有1.4GB)
104.244.91.31:3000
```

程序会自动从网络上获取codimd和postgres数据库的镜像。

以及随着codimd最新版本的更新，可以自行修改 docker-compose.yml 中镜像的名称

注意一下，不加sudo和-d都会导致报错，后者原因未知，如果失败了请务必删除容器再来一次

这组代码默认将容器的端口映射在了localhost:3000，在浏览器框中输入ip:3000就能访问了

暂时还不知道怎么把端口跟外网域名绑定，暂时的方案是使用宝塔面板的重定向功能，待日后更新吧？

### 运营维护

参考： [使用DOCKER搭建CODIMD](http://www.john30n.com/index.php/tool/64.html)

##### 备份

```
docker-compose exec database pg_dump codimd -U codimd  > backup.sql
```

##### 恢复

```
cat backup.sql | docker exec -i $(docker-compose ps -q database) psql -U codimd
```

##### 升级软件

```
cd codimd ## enter the directory
git pull ## pull new commits
docker-compose pull ## pull new containers
docker-compose up ## turn on
```

