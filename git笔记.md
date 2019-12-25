# GIT使用笔记

## 基本概念

### 1.工作区、暂存区、本地库

- **工作区**：就是你在电脑里能看到的目录。
- **暂存区**：英文叫stage, 或index。一般存放在 ".git目录下" 下的index文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
- **本地版本库**：工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

`三者之间的关系`

![img](https://www.runoob.com/wp-content/uploads/2015/02/1352126739_7909.jpg)

图中左侧为工作区，右侧为版本库。在版本库中标记为 "index" 的区域是暂存区（stage, index），标记为 "master" 的是 master 分支所代表的目录树。

图中我们可以看出此时 "HEAD" 实际是指向 master 分支的一个"游标"。所以图示的命令中出现 HEAD 的地方可以用 master 来替换。

图中的 objects 标识的区域为 Git 的对象库，实际位于 ".git/objects" 目录下，里面包含了创建的各种对象及内容。

当对工作区修改（或新增）的文件执行 "git add" 命令时，暂存区的目录树被更新，同时工作区修改（或新增）的文件内容被写入到对象库中的一个新的对象中，而该对象的ID被记录在暂存区的文件索引中。

当执行提交操作（git commit）时，暂存区的目录树写到版本库（对象库）中，master 分支会做相应的更新。即 master 指向的目录树就是提交时暂存区的目录树。

当执行 "git reset HEAD" 命令时，暂存区的目录树会被重写，被 master 分支指向的目录树所替换，但是工作区不受影响。

当执行 "git rm --cached <file>" 命令时，会直接从暂存区删除文件，工作区则不做出改变。

当执行 "git checkout ." 或者 "git checkout -- <file>" 命令时，会用暂存区全部或指定的文件替换工作区的文件。这个操作很危险，会清除工作区中未添加到暂存区的改动。

当执行 "git checkout HEAD ." 或者 "git checkout HEAD <file>" 命令时，会用 HEAD 指向的 master 分支中的全部或者部分文件替换暂存区和以及工作区中的文件。这个命令也是极具危险性的，因为不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动。

### 2.创建仓库

#### git init

在你需要创建版本控制的目录下

```sh
git init
```

使用 **git init** 命令来初始化一个 Git 仓库，Git 的很多命令都需要在 Git 的仓库中运行，所以 **git init** 是使用 Git 的第一个命令。

在执行完成 **git init** 命令后，Git 仓库会生成一个 .git 目录，该目录包含了资源的所有元数据，其他的项目目录保持不变（不像 SVN 会在每个子目录生成 .svn 目录，Git 只在仓库的根目录生成 .git 目录）该命令执行完后会在当前目录生成一个 .git 目录。

使用我们指定目录作为Git仓库。

```sh
git init 文件夹名
```

初始化后，会在 `文件夹名` 目录下会出现一个名为 .git 的目录，所有 Git 需要的数据和资源都存放在这个目录中。

如果当前目录下有几个文件想要纳入版本控制，需要先用 git add 命令告诉 Git 开始对这些文件进行跟踪，然后提交：

```sh
$ git add *.c						#将以.c后缀的文件 add到暂存区
$ git add aaa.txt					#将文件 aaa.txt 提交到暂存区
$ git commit -m '提交时附带的信息'	    #将暂存区的文件 提交到本地版本库 同时附带信息
```

#### git clone 

我们使用git clone 从远程仓库中拷贝项目到本地仓库，格式为：

```sh
git clone url
#例如：
git clone https://gitee.com/startwang2019/tensquare_parent_home.git
```

其中 url 表示远程仓库的url

如果想要克隆项目到指定目录则有：

```sh
git clone url  directory
#例如
git clone  https://gitee.com/startwang2019/tensquare_parent_home.git  myProject
```

url：远程仓库的url

directory：目录名



git clone 时，可以所用不同的协议，包括 ssh, git, https 等，其中最常用的是 ssh，因为速度较快，还可以配置公钥免输入密码

```sh
git clone git@github.com:fsliurujie/test.git         --SSH协议
git clone git://github.com/fsliurujie/test.git          --GIT协议
git clone https://github.com/fsliurujie/test.git      --HTTPS协议
```

#### git add

将`工作区`的文件添加到`暂存区`

```sh
$ git add .   					#将当前目录的所有文件添加到暂存区
$ git add *.txt					#将当前目录下的后缀为 txt的 文件添加到 暂存区
```

#### git status

查看文件或者分支 或者 项目的文件状态

```sh
$ git status -s  				#查看所有的文件
$ git status on branch master 	 #查看master分支下的文件的状态
```

![image-20191218171039484](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191218171039484.png)

`M` 表示modify 该文件提交到暂存区后又变更了 所有无法commit

![image-20191218171414612](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191218171414612.png)

#### git commit

将`暂存区`的文件写入`本地版本库`

`Git 为你的每一个提交都记录你的名字与电子邮箱地址，所以第一步需要配置用户名和邮箱地址`

```sh
$ git config --global user.name 'wtp'				#配置系统变量 用户名
$ git config --global user.email 532955362@qq.com	 #配置系统变量 用户的邮箱
```

`提交的时候要加上你本次提交的提示信息不然提交不了`

```sh
$ git commit -m '第一次版本提交到本地版本库'  			#参数 -m 表示附带提示信息
```

提交后查看文件状态：

```sh
$ git status          #查看当前暂存区文件状态
```

![image-20191218172650843](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191218172650843.png)

`上面提示表示 我们将工作区的内容提交到暂存区后工作区没有作任何改动（增删改）`

如果你觉得 git add 提交缓存的流程太过繁琐，Git 也允许你用 -a 选项跳过这一步。命令格式如下：

```sh
$ git commit -a
```

假设我们修改了工作区的文件然后 直接这样提交

```sh
$ git commit -am 'OK'
```

#### git reset 

`这个命令是将HEAD指针指向 某个文件或者版本 将这个文件 或者版本回退到工作区`

```sh
$ git reset HEAD aaa.txt  				#将已经提交到在暂存区的文件回退到工作区
```

#### 全局变量的位置

```sh
$ cd ~								#进入到用户目录
$ ll -a | grep -i git 				 #搜索 含有git的文件名
$ cat .gitconfig					 #查看配置文件
```

