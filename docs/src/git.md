# Git

[Git如何把本地代码推送到远程仓库](https://blog.csdn.net/yl_cc/article/details/72676538)

接下来依次执行命令：
```
git init   // 初始化版本库

git add .   // 添加文件到版本库（只是添加到缓存区），.代表添加文件夹下所有文件 

git commit -m "first commit" // 把添加的文件提交到版本库，并填写提交备注
```
到目前为止，我们完成了代码库的初始化，但代码是在本地，还没有提交到远程服务器，所以关键的来了，要提交到就远程代码服务器，进行以下两步：
```
git remote add origin 你的远程库地址  // 把本地库与远程库关联

git push -u origin master    // 第一次推送时

git push origin master  // 第一次推送后，直接使用该命令即可推送修改
```
把本地库的内容推送到远程。使用 git push命令，实际上是把当前分支master推送到远程。执行此命令后会要求输入用户名、密码，验证通过后即开始上传。
说明：用户名密码需要通过命令 ssh-keygen -t rsa -C “xxxxxx@qq.com”进行创建，并且要把得到的秘钥（公钥）文件放到git服务器上，这样才有权限进行代码推送

到此就成功的把本地的代码放到了远程服务器上，这样就能让项目组成员进行写作开发了。
————————————————
版权声明：本文为CSDN博主「蜗牛夏」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/yl_cc/article/details/72676538