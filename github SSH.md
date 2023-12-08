# github SSH

 PicGo + Gitee + Typora + Onedrive + Markdown here 几乎可以解决所有的文档分享和编辑需求。

## 1.生成SSH密钥对

```
ssh-keygen
或
ssh-keygen -t rsa -C 'git key for github' -f
~/ .ssh/id_rsa
```

## 2.配置github公钥

登录github后台，在用户设置中找到‘ssh and GPG keys’>'New SSH key',填入公钥

## 3.本地使用git-bash

github官方指引：使用本地已有的密钥

![](https://raw.githubusercontent.com/chawx/picture/main/715d8cfa11afa089aca6e0b984c7c4f.png)

以下就是该步骤

![](https://raw.githubusercontent.com/chawx/picture/main/image18d69cc87f0e09e0adddbd9bb7e72a7.png)

![](https://raw.githubusercontent.com/chawx/picture/main/image20231126142922.png)

![](https://raw.githubusercontent.com/chawx/picture/main/image20231126143107.png)

![](https://raw.githubusercontent.com/chawx/picture/main/image20231126145353.png)

## 四、解决问题

解决 git commit出现下面的问题

Author identity unknown

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'cccc@cccc-virtual-machine.(none)')

![](https://raw.githubusercontent.com/chawx/picture/main/image2023-11-26_15-08-33.png)

解决ssh密钥的问题

![](https://raw.githubusercontent.com/chawx/picture/main/image2023-11-26_15-08-33.png)

注意：Linux 私钥的文件权限是‘0600’

```
git init

git status
```

查看当前状态

```
git add .
```

上传文件

```
git commit -m "提交"
```

提交

```
git remote add origin "git@   "
```

与仓库进行关联

```
git push -u origin 你的branch
```

进行推送

```text
git checkout -b pa0
```

若要创建新分支，请使用 `git checkout `创建`PA0`的分支 命令：

```
git branch
```

列出所有分支

```
git diff
```

要列出上次提交的修改，请执行以下操作：

```
diff --git a/Makefile b/Makefile
index c9b1708..b7b2e02 100644
--- a/Makefile
+++ b/Makefile
@@ -1,4 +1,4 @@
-STUID = 221220000
-STUNAME = 张三
+STUID = 221221234
+STUNAME = 李四
 
  # DO NOT modify the following code!!!
```

上面的是--是删减的，++是修改后的

![](https://raw.githubusercontent.com/chawx/picture/main/imageSnipaste_2023-11-26_16-58-24.png)

![](https://raw.githubusercontent.com/chawx/picture/main/imageSnipaste_2023-11-26_16-58-24.png)

```
git checkout "分支"
```

切换分区

![](https://raw.githubusercontent.com/chawx/picture/main/imageSnipaste_2023-11-26_17-29-13.png)

RTFM(Read The Fucking Manual)

你应该去读手册

STFW(Search The Fucking Web)

你应该到TMD网上去搜索答案。

RTFSC(Reading The Fucking Source Code)

阅读源码