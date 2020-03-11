# nodejs

[js nodejs npm之间的关系+npm安装备忘](https://www.jianshu.com/p/857ef827fbd4)

npm和nodejs的关系

先装nodejs再装npm

docker-compose.yml

下载页面

https://nodejs.org/zh-cn/download/

```
https://nodejs.org/dist/v12.16.1/node-v12.16.1-linux-x64.tar.xz
tar -xvf node-v12.16.1-linux-x64.tar.xz
或者 -xf 解压
1、打开文件
vim /etc/profile
2、最后一行放入
PATH=$PATH:/software/node-v12.16.1-linux-x64/bin
/
示例：echo "Intel Galileo" >> test.txt
echo "PATH=$PATH:/root/node-v12.16.1-linux-x64/bin" >> /etc/profile

source /etc/profile
查看
npm -v && node -v
```

\# 修改权限，脚本可执行

chmod u+x test.sh   

./test.sh

安装rvm的步骤

1、在安装RVM之前先导入公钥

```
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
curl -sSL https://get.rvm.io | bash -s stable
```

如何在Ubuntu 18.04上使用RVM安装Ruby on Rails

https://cloud.tencent.com/developer/article/1353015

```
cat /tmp/rvm.sh | bash -s stable --rails 需要的时间比较长
路径和参考网页的不同，依据安装后的结果：source /usr/local/rvm/scripts/rvm
source /usr/local/rvm/scripts/rvm
rvm list 此时ruby已经安装好，查看版本
实际上root的路径
/usr/local/rvm/scripts/cli: line 865:  4707 Killed                  "$rvm_scripts_path/set" "$rvm_action" "${rvm_ruby_args[@]}"
gem install bundler --no-ri --no-rdoc
实际是：gem install bundler 才能运行

```

[使用Docker进行自我托管 standardnotes](https://docs.standardnotes.org/self-hosting/docker)

```
bundle install

```

