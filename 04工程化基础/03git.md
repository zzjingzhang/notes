# git

## git的配置分类

git自带一个git config的工具来帮助设置控制git外观和行为的配置变量

/etc/gitconfig 文件：包含系统上每一个用户及他们仓库的通用配置

​     如果在执行git config 时带上 --system选项，那么它就会读写该文件的配置变量

​     由于它是系统配置文件，因为需要管理员或超级用户权限来修改它(开发中通常不修改)

~/.gitconfig或C/用户/username/.gitconfig 文件 ：只针对当前用户

​      可以传递 --global选项让git读写此文件，这会对你系统上所有的仓库生效

当前使用仓库的git目录中的config文件（即 .git/config):针对该仓库

​     可以传递 --local 选项让git强制读写此文件，虽然默认情况下用的就是它

## git的配置选项

安装git后，要做的第一件事就是设置用户名和邮件地址

这一点很重要，因为每一个git提交都会使用这些信息，它们会写入到你的每一次提交中，不可更改

如果使用了 --global选项，那么像该命令只需要运行一次，因为之后无论你在该系统上做任何事情，git都会使用那些 信息

```powershell
git config --global user.name 'your username'
git config --global user.email 'your email address'

#检测当前的配置信息
git config --list
```

## git的别名(alias)

git并不会在你输入部分命令时自动推断出你想要的命令

如果不想每次都输入完整的git命令，可以通过git config 文件来轻松为每一个命令设置一个别名

```powershell
git config --global alias.co checkout # 以后运行 git co即可
git config --global alias.br branch # 以后运行 git br即可
git config --global alias.ci commit # 以后运行 git ci即可
git config --global alias.st status # 以后运行 git st即可
```

## 获取git仓库- git init /git clone

我们需要一个git来管理源代码，那么我们本地也需要有一个git仓库

通常有两种获取git项目仓库的方式

方式一：初始化一个git仓库(git init)，并且可以将当前项目的文件都添加到git仓库中（目前很多的脚手架在创建项目时都会默认创建一个git仓库）

方式二：从其他服务器克隆（clone）一个已存在的git仓库

方式一：初始化git仓库

该命令创建一个名为.git的子目录，这个子目录含有初始化的git仓库中所有的必须文件，这些文件是git仓库的核心

但是这个时候，仅仅只是做了一个初始化，项目里的文件还没被跟踪

方式二：从git远程仓库clone

git clone 远程仓库的地址  

```powershell
git clone git@github.com:zzjingzhang/vue3-ts-vuex.git
```

## 文件的状态划分

未跟踪：默认情况下，git仓库下的文件也没有添加到git仓库管理中，我们需要通过add命令来操作

已跟踪：添加到git仓库管理的文件处于已跟踪状态，git可以对其进行各种跟踪管理

已跟踪文件又可以进行细分状态划分

staged：暂缓区中的文件状态，commit命令，可以将staged中文件提交到git仓库

modified：修改了某个文件后，会处于modified状态

### 检测文件的状态-git status

### 文件添加到暂存区：git add

跟踪新文件命令：git add filename.ext   //跟踪单个文件

git add . 将所有文件添加到暂缓区中

### git忽略文件

创建一个.gitigonre的文件，列出需要忽略的文件的模式

### 文件更新提交-git commit

每次准备提交前，先用 git status看下，需要的文件是否已暂存起来了，已暂存的文件可以使用 git commit 命令进行提交

可以在git commit 命令后添加 -m选项，将提交信息与命令行放在同一行  git commit  -m '提交信息'

如果我们修改文件的add操作，加上commit的操作优点繁琐，可以将两个命令结合使用

git commit -a -m '提交信息'

## git的校验和

git所有的数据在存储前都计算校验和，然后以校验和来引用

git用以计算校验和的机制叫做SHA-1散列（hash ，哈希）

这是一个由40个十六进制字符（0-9和a-f）组成的字符串，基于git文件的内容或目录结构计算出来

### 查看提交的历史-git-log

不传入任何参数的情况下，git log会按时间顺序列出所有的提交，最近的更新排在最上面

这个命令会列出每个提交的SHA-1校验和、作者的名字和电子邮件地址，提交时间以及提交说明

git log --pretty=oneline  每一行显示一个提交记录，只显示校验和、提交说明

git log --pretty=oneline  --graph  可视化日志

### 版本回退 - git reset

如果想要进行版本回退，我们需要先知道目前处于哪一个版本：git通过HEAD指针记录当前版本

HEAD是当前分支引用的指针，它总是指向该分支上的最后一次提交

理解HEAD的最简单方式，就是将它看做该分支上的最后一次提交的快照

我们可以通过HEAD来改变git目前的版本指向

上一个版本就是HEAD^，上上个版本就是HEAD^^

如果是上1000个版本，我们可以使用HEAD~1000

我们可以指定某一个commit id

```powershell
git reset --hard HEAD^
git reset --hard HEAD~1000
git reset --hard 2d44982  # 回退到指定版本 2d44982校验和的前几位
```

## 远程仓库

目前git服务器验证手段主要有两种：

方式一：基于HTTP的凭证存储

方式二：基于SSH的密钥

### 远程仓库的验证-凭证

因为本身http协议是无状态的连接，所以每一个连接都需要用户名和密码

如果每次都这样操作，那么会非常麻烦，幸运的是，git拥有一个凭证系统来处理这个事情

下面有一些git crediential的选项

​       选项一：默认所有都不缓存。 每一次连接都会询问你的用户名和密码；
​       选项二：“cache” 模式会将凭证存放在内存中一段时间。 密码永远不会被存储在磁盘中，并且在15分钟后从内存中清除；
​       选项三：“store” 模式会将凭证用明文的形式存放在磁盘中，并且永不过期；
​       选项四：如果你使用的是 Mac，Git 还有一种 “osxkeychain” 模式，它会将凭证缓存到你系统用户的钥匙串中（加密的）；
​       选项五：如果你使用的是 Windows，你可以安装一个叫做 “Git Credential Manager for Windows” 的辅助工具；

​           可以在 https://github.com/Microsoft/Git-Credential-Manager-for-Windows 下载。

### 远程仓库的验证-ssh密钥

Secure Shell(安全外壳协议，简称SSH)是一种加密的网络传输协议，可在不安全的网络中为网络服务提供安全的传输环境

SSH以非对称加密实现身份验证

- 例如其中一种方法是使用自动生成的公钥-私钥对来简单地加密网络连接，随后使用密码认证进行登录；

- 另一种方法是人工生成一对公钥和私钥，通过生成的密钥进行认证，这样就可以在不输入密码的情况下登录；

- 公钥需要放在待访问的电脑之中，而对应的私钥需要由用户自行保管；

  如果我们以SSH的方式访问git仓库，那么就需要生成对应的公钥和私钥

  ```shell
  # 以下两种方式都可以
  ssh-keygen -t ed25519 -C 'your email'
  ssh-keyge  -t rsa -b 2048 -C 'your email'
  ```

### 管理远程服务器

查看远程地址

git remote

git remote -v

-v是-verbose的缩写（冗长的）

添加远程地址：我们可以添加远程服务器（让本地的仓库和远程服务器仓库建立连接）

git remote add \<shortname\>  \<url\>

本地分支的上游分支

```shell
git branch --set-upstream-to=origin/master # 设置上游分支
git merge --allow-unrelated-histories #将两个没有共同基础的分支进行合并
```

## git标签(tag)

### 创建tag

git支持两种标签：轻量标签和附注标签

附注标签，通过-a选项，并且通过-m添加格外信息

```powershell
git tag v1.0
git tag -a v1.1 -m '附注tag'
```

默认情况下，git push命令并不会传送标签到远程仓库服务器上

在创建完标签后，必须显式地推送标签到共享服务器上，当其他人从仓库中克隆或拉取，他们也能得到那些标签

```shell
git push origin v1.0
git push orgin --tags
```

### 删除和检出tag

```shell
git tag -d <tagname> # 删除本地tag 
git tag -d v1.1
git push <remote> --delete <tagname> # 删除远程tag
git push origin --delete v1.1

# 检出tag
git checkout 
git checkout v1.0 
```

## git提交对象

几乎所有的版本控制系统都以某种形式支持分支

使用分支意味着你可以把你的工作从开发主线上分离出来，以免影响开发主线

在进行提交操作时，git会保存一个提交对象(commit object)

该提交对象会包含一个指向暂存内容快照的指针

该提交对象还包含了作者的姓名和邮箱、提交时输入的信息以及指向它的父对象的指针

​    首次提交产生的提交对象没有父对象，普通提交操作产生的提交对象有一个父对象；
​    而由多个分支合并产生的提交对象有多个父对象；

### git master（现在改为main）分支

git的分支，其实本质上仅仅是指向提交对象的可变指针

git的默认分支名字是master，在多次提交操作后，你其实已经有一个指向最后那个提交对象的master分支

master分支会在每次提交时自动移动

git的master分支并不是一个特殊分支

它就跟其他分支完全没有区别

之所以几乎每一个仓库都有一个master分支，是因为git init 命令默认创建它，并且大多数人懒得去改它

### git 创建分支

git是怎么创建分支的呢？

很简单，它只是为你创建了一个可以移动的新的指针

比如创建一个test分支，你需要使用git branch 命令

那么git 又是怎么知道当前在哪一个分支上呢

也很简单，它也是通过一个名为HEAD的特殊指针

```powershell
git branch test # 创建分支
git checkout test # 切换分支

git checkout -b test # 创建并切换分支
```

### 查看和删除分支

```shell
git branch # 查看当前所有分支
git branch -v # 同时查看最后一次提交

git branch --merge # 查看所有合并到当前分支的分支
git branch --no-merge # 查看所有没有合并到当前分支的分支



git branch –d hotfix # 删除当前分支
git branch –D hotfix # 强制删除某一个分支

```

### git rebase用法

在git中整合来自不同分支的修改主要有两种方式:git merge 以及 git rebase

#### rebase原理

rebase是如何工作的呢？

它的原理是首先找到这两个分支（即当前分支 experiment、变基操作的目标基底分支 master） 的最近共同祖先；
然后对比当前分支相对于该祖先的历次提交，提取相应的修改并存为临时文件；
然后将当前分支指向目标基底；
最后以此将之前另存为临时文件的修改依序应用

#### rebase和merge的选择

事实上，rebase和merge是对Git历史的不同处理方法：
     merge用于记录git的所有历史，那么分支的历史错综复杂，也全部记录下来；
     rebase用于简化历史记录，将两个分支的历史简化，整个历史更加简洁；
了解了rebase底层原理，就可以根据自己的特定场景选择merge或者rebase。
注意：rebase有一条黄金法则：永远不要在主分支上使用rebase
如果在main上面使用rebase，会造成大量的提交历史在main分支中不同；
而多人开发时，其他人依然在原来的main中，对于提交历史来说会有很大的变化；



git常见命令

![08git常见命令](C:\Users\10244\Desktop\前端\notes\04工程化基础\images\08git常见命令.png)