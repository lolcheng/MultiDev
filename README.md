# 武汉大学机器人队代码统一管理平台

## 0.准备工作：下载配置git&创建SSH公钥

111

1>如果有git bash意味着git已经下载，否则自己上网找办法

2>查看username和useremail是否配置完成：

打开git bash输入git config user.name和git config user.email查看是否有结果，没有的话依次输入进行配置（与github账户一致）：
```
git config --global user.name 用户名
git config --global user.email  邮箱
```
3>创建SSH公钥以下载仓库：
在git bash里输入：ssh-keygen -t rsa -C "邮箱"

中间出现的所有停顿全部回车就可以（是设置密码的，但不需要）

打开C盘用户文件夹下的.ssh文件中的id_rsa.pub文件，记事本打开，其内容即为SSH公钥，复制到你的github账户，点击右上角头像->Settings->SSH and GPG keys->New SSH key->随便取个title，然后粘贴即可

验证：键入ssh -T git@github.com

如果出现Hi 用户名! You've successfully authenticated, but GitHub does not provide shell access.即配置完成

## 1.什么是分支
分支是从主线上分离出来进行另外的操作的代码线。分支的存在既不影响主线，主线又可以继续其原有的工作流程。

分支的主要作用包括：
- 并行开发：每个分支都是代码的独立副本，可以并行推进多个功能的开发。
- 版本管理：分支使得版本管理变得更为轻松。当一个分支的代码稳定后，可以将其合并到主分支进行发布，而不会影响其他正在进行的开发工作。
- 故障隔离：如果在开发中遇到问题或发生错误，可以创建一个新分支来排查和修复问题，而不会影响其他分支的代码。

常见的分支类型包括：
- 主分支（main）用于存储正式发布的历史，所有的开发活动产生的输出物最终都会反映到主分支的代码中。主分支应该是经过充分测试和验证的代码，不能直接在主分支上进行开发，主分支上的代码必须是可行而没有bug的。
- 开发分支（dev）：用于整合和存放开发人员的工作成果。在这个分支上，开发人员可以自由地添加、修改和删除代码，进行新功能的开发或修复bug。

**为了在一个仓库里统一管理队里所有的工程，我们这里定义分支的目的为给每一个独立的方案以一个独立的工作空间，不同的人负责同一个方案时就从同一个分支中下载、更新代码**

## 2.队内仓库地址
HTML：https://github.com/lolcheng/MultiDev

SSH：git@github.com:lolcheng/MultiDev.git

## 3.Fork队里的仓库
打开网址，右上角点击Fork，然后点击Create fork，取消勾选Only clone the main branch，此时会把队里的整个仓库保存到你的本地账户
下面的操作都会在你本地的仓库进行

## 4.第一次操作
当有一个新方案时，管理员会创建一个新的空分支，切记确认对应的空分支，一定要下载对应的分支仓库

新建一个文件夹存放仓库，在仓库文件夹下的git bash中键入下载仓库内容：

`git clone -b 新的空分支名 git@github.com:lolcheng/MultiDev.git`

记得一定要进入有.git的文件夹，一般是你新建的文件夹下的子文件夹，不然会报错：not a git repository

接着，当你把新的代码写好后，把整个Keil工程复制到这个有.git的文件夹中（建议写readme）

如果上传的Keil工程里有.git文件夹要先删掉（主目录和USER目录下都可能有），不然会报错：does not have a commit checked out

接着就可以上传文件了，在仓库文件夹下的git bash中依次键入：
```
git add .            //警告不用管
git commit -m "更新信息"
git push             
```
这样子你本地的仓库就会被更新，但注意，此时你还没有将代码上传到队里的仓库

要将你的代码上传到队里的仓库，你需要进行Pull Request操作

在你的github工程主页上方点击Pull Request，然后点击create a pull request，选择将你本地的main分支提交到队里仓库的对应名称的分支后点击create pull request，添加标题和描述后create pull request就可以把你的请求上传到队里的仓库了，当管理员同意后对应的分支就会被更新为你的main分支内容。

## 5.之后的操作
当有人更新对应的分支时，请及时获取最新的分支信息，一般建议每次要写新东西前主动进行一次更新，避免版本落后。

在仓库文件夹下的git bash中键入：`git pull`

每次修改好文件需要上传时，在仓库文件夹下的git bash中依次键入：
```
git add .
git commit -m "更新信息"
git push
```
同样的，如果上传的Keil文件里有.git文件夹，记得删掉再上传（主目录和USER目录下都有）

同样的，此时也只有你本地的仓库被更新，队里的仓库并没有更新，要将你的代码上传到队里的仓库，你仍然需要进行Pull Request操作

## 6.注意事项
1>如果git push失败，很有可能是你在修改仓库并上传之前已经有人提前上传了新版本的仓库，此时需要先git pull获取最新的仓库后处理冲突再将写好的给git push，所以建议要写新东西前主动进行一次git pull

2>分支的新增和删除均由管理员操作
