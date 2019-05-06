# 版本控制系统

## 为什么要有版本控制系统?

1. 在开发过程中，经常需要对一个文件进行修改甚至删除，但是我们又希望能够保存这个文件的历史记录，如果通过备份，那么管理起来会非常的复杂。
2. 在多人开发时，如果需要多人合作开发一个页面，那么修改以及合并也会非常的棘手。容易出现冲突。

## 什么是版本控制系统？

常用的版本控制工具： svn git

## git介绍

> Git是一款免费、开源的**分布式** **版本控制系统** ，用于敏捷高效地处理任何或小或大的项目。

Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。

## Linux的常用指令

```bash
# cd 改变目录  （change directory）
cd images   #进入images文件夹
cd ..      #进入上一层目录
cd ~       #进入用户根目录

# tab  自动补全，当我们输命令或者目录很长时，可以使用tab键进行自动补全。
# 按两次tab，会把所有符合要求的内容都列出来。

# pwd 打印当前目录的路径 （print work directory）
pwd

# ls 展示当前目录列表（list）
ls         # 展示当前目录
ls -a      # 展示全部内容，包括隐藏文件
ls -l      # 以列表的形式展示内容

# clear reset清屏
clear  # 清除屏幕内容，滚动条，保留了历史
reset  # 重置，历史记录没了。


# mkdir  创建一个文件夹 （make directory）
mkdir css          # 创建一个css的文件夹
mkdir css img js   # 创建了三个文件夹

# rmdir  删除一个空的文件夹（没啥用）
rmdir img   # 删除文件夹

# touch  创建文件
touch index.html   #创建了一个index.html文件
touch css/index.css # 在css目录下创建idnex.css文件

# rm 删除一个文件获取文件夹
rm index.html # 删除index.html文件
rm js         # 删除空的js文件夹
rm -r css     # 递归删除一个文件夹

# mv 移动文件（move）
mv index.html js            # 将html文件移动到js文件夹中
mv index.html index2.html   # 将index.html重命名为index2.html

# cp 复制文件（cp）
cp index.html index2.html   # 复制index.html文件，命名为index2.html
cp -r css css02             # 如果复制的是文件夹，需要使用-r参数。

# cat 查看文件全部内容
cat index.html
```



## git的应用

​          在第一次使用的时候，需要配置你的用户邮箱和用户名称，这两条配置是很重要的，每次提交git代码都会引用这两条信息，记录了谁提交了代码，会永久的记录在历史记录中。

```bash
# git config  user.name 你的目标用户名
# git config  user.email 你的目标邮箱名

# 使用--global参数，配置全局的用户名和邮箱，只需要配置一次即可。
git config  --global user.name sdd
git config  --global user.email 111111@qq.com

# 查看配置信息
git config --list
```

1. 初始化git仓库`git init`

2. 查看当前git仓库的状态`git status`

3. 将文件添加到git的暂存区`git add 文件名`

4. 将文件由暂存区提交到仓库区`git commit -m '提交说明'`

5. 查看提交日子`git log`

   ```bash
   # 要对某个项目使用git进行管理，需要使用git init命令初始化git仓库
   # 会在当前目录生成一个隐藏文件夹 .git  不要去修改这个文件夹下的任意东西。
   git init

   # 查看git文件的状态 ,如果此时新建一个文件，那么这个文件是没有被追踪的，说白了git还没有管理这个新建的文件
   git status 

   # 告诉git开始对index.html文件进行追踪， git会在暂存区中存储这个文件
   git add index.html

   # 让文件由暂存区提交到仓库区。此时文件才真正的被git管理了。
   # 如果提交日志乱码，右键-->options-->Text-->将编码改成utf-8

   git commit -m '第一次提交'

   # 查看提交日志
   git log
   ```

   ​

## 命令的详情

### git add(重点)

- 作用：让git追踪一个新的文件，并且将文件由 工作区 添加到 暂存区，暂存文件
- 命令：`git add 文件名/目录名`
  - 例如： `git add index.html`
- `git add --all` 或者 `git add -A` 获取`git add .`（简写） 添加所有文件
- `git add a.txt b.txt` 同时添加两个文件
- `git add *.js` 添加当前目录下的所有js文件
- `git add css/`添加css目录下所有的文件

### git commit（重点）

- 作用：将文件由 暂存区 添加到  仓库区，生成版本号（历史记录，以后可以回退到某一个版本号）
- `git commit -m "提交说明"`

### git status

- 作用：查看文件的状态


- 命令：`git status`
- 命令：`git stauts -s` 简化日志输出格式

### git log

- 作用：查看提交日志
- `git log` 只能查看当前head以及以前的日志
- `git log --oneline` 简洁的日志信息,如果提交的日志非常多了
- `git reflog` 查看所有的提交变更日志

### git reset

- 作用：版本回退，将代码恢复到已经提交的某一个版本中。

- `git reset --hard 版本号` 将代码回退到某个指定的版本(版本号只要有前几位即可)

- `git reset --hard head~1`将版本回退到上一次提交

- ​

  - ~1:上一次提交
  - ~2:上上次提交
  - ~0:当前提交

- ```bash
  关于参数 --hard的解释
  git reset 的参数可以是以下三个值：
  git reset --soft 版本号  ： 只重置仓库区
  git reset --mixed 版本号 ： 重置仓库区和暂存区【默认】
  git reset --hard  版本号 ： 重置仓库区和暂存区和工作区。
  git reset 版本号         : 效果与--mixed一致
  ```

  当使用了`git reset`命令后，版本会回退，使用`git log`只能看到当前版本之前的信息。使用`git reflog`可以查看所有的版本信息

  ​



# 远程仓库

## 远程仓库相关的命令

### git push

- 作用：将本地仓库中代码提交到远程仓库
- `git push 仓库地址 master` 在代码提交到远程仓库，注意master分支必须写，不能省略
- 例子：`git push git@github.com:hucongcong/test.git master` 如果第一次使用，需要填写github的用户名和密码
- 在git push之前，先git pull: 保证先把远程仓库代码先拉取到本地

## git pull

- 作用：将远程的代码下载到本地
- `git pull 代码地址 master` 将远程的代码中master分支下载到本地
- 通常在push前，需要先pull一次。

### git clone

- 作用：克隆远程仓库的代码到本地
- git clone [远程仓库地址]
- `git clone git://github.com/schacon/test.git`会在本地新建一个`test`文件夹，在test中包含了一个`.git`目录，用于保存所有的版本记录，同时test文件中还有最新的代码，你可以直接进行后续的开发和使用。
- git克隆默认会使用远程仓库的项目名字，也可以自己指定。需要是使用以下命令：`git clone [远程仓库地址] [本地项目名]`

### git remote

每次push和pull操作都需要带上远程仓库的地址，非常的麻烦，我们可以给仓库地址设置一个别名

- `git remote add 仓库别名 仓库地址` 使用仓库别名替代仓库地址。仓库别名相当于一个js变量，仓库地址就是对应的值。
  - `git remote add hucc git@github.com:hucongcong/test.git` 设置了一个hucc的仓库别名，以后push和pull都可以不用仓库地址，而用hucc，origin
- `git remote remove hucc` 删除hucc这个仓库别名。
- `git remote` 查看所有的仓库别名
- 如果使用了`git clone`命令从远程仓库获取下来的，那么这个本地仓库会自动添加一个 origin的远程地址，指向的就是克隆的远程地址。

## github

git与github没有直接的关系。

- git是一个版本控制工具。
- github是一个代码托管平台，是git的一个远程代码仓库。
- 将来工作时，公司会有自己的代码仓库。

[github官网](https://github.com/)

[开源中国-git](https://git.oschina.net/)

```bash
1. gitHub是一个面向开源及私有软件项目的托管平台，因为只支持git 作为唯一的版本库格式进行托管，故名gitHub。
2. github免费，代码所有人都能看到，但是只有你自己能修改。付费的可以隐藏。
```

在github上创建一个项目，获取到仓库的地址。然后就可以将本地的代码推送到远程的服务器上。

