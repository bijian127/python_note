# Git学习笔记

## 关于 `Git` 的背景知识

-  `Git` 是什么

  Git——分布式版本控制系统，Linus使用C编写

- `Git` 用来做什么

  协同开发、开源程序、社会化编程
  
- `Git`协议

  - 9418端口
  - 类似于SSH服务，但是访问无需任何授权
  - 优点：
    - 传输协议最快——适合项目庞大并不需要写授权
    - 使用SSH相同数据传输机制，省去加密和授权的开销
  - 缺点：缺乏授权机制、架设Git服务较为复杂、端口限制

- `Git`原理

  - 指向修改、不指向提交
  - 内容寻址（content-addressable）文件系统
  - Plumbing&Porcelain(底层和高层命令)：使用Unix风格
  - Git对象：核心——存储键值对、树对象
  - Git References：类似于书签
  - Packfiles：zlib压包
  - The Refspec

- 工作区、版本库

  - 工作区（Working Directroy）：即本地工作目录文件夹
  - 版本库（Repository）：在工作区中的隐藏目录`.git`文件夹中
    - 暂存区（Stage/Index）：接收工作区add操作的工作内容，并准备commit提交到版本库中
    - 分支（master&dev）：接收commit提交的工作内容，新建分支相当于新建了一个dev的指针
    - 指针HEAD：每次提交，HEAD指针即指向分支的最后一个版本，如果分支提交，但是主分支的master的指针并不变化，变化的只是HEAD指针


## `Git` 基本使用命令以及方法

###  `Git`使用前的准备

- 设置初始信息（邮箱以及姓名）

  ```shell
  $ git config --global user.name bijian
  $ git config --global user.email bijian127@live.com
  ##生成.gitconfig文件，内含上述配置信息，默认会在用户目录下
  ```

- 使用高亮确保命令的可读性

  ```shell
  $ git config --global color.ui auto
  ```
  
- 初始化当前目录

  ```shell
  $ git init
  ```

### `Git` 常用命令

- 工作区提交至暂存区

  ```shell
  $ git add filename
  ```

- 暂存区提交至版本库

  ```shell
  $ git commit -m <message>
  ##message为提交的附加信息
  ```

- 查看仓库状态

  ```shell
  $ git status
  ```

- 查看修改内容

  ```shell
  $ git diff
  ```

- 参看仓库提交记录

  ```shell
  $ git log
  ##格式化视图添加“--pretty=online”
  ```

- 版本回退

  ```shell
  $ git reset --head HEAD^
  ##退回到上一个版本，HEAD^^退回到上上个版本
  ##退回到多个以上版本HEAD~100
  ##也可以使用版本号前缀即commit id
  ```

- 查看历史记录

  ```shell
  $ git reflog
  ```

- 撤销修改

  ```shell
  ##未提交到版本库，即未commit
  $ git checkout -- filename
  ##一种是readme.txt自修改后还没有被放到暂存区，撤销修改就回到和版本库一模一样的状态；
  ##一种是readme.txt已经添加到暂存区后，又作了修改，撤销修改就回到添加到暂存区后的状态。
  $ git reset HEAD filename
  ##未commit之前，也可以使用reset退回版本
  ```

  ```shell
  ##已经commit至版本库中，可以使用退回版本的方法
  $ git reset HEAD filename
  ```

- 删除文件操作

  ```shell
  ##从版本库中删除该文件，那就用命令git rm删掉，并且git commit
  $ git rm filename
  $ git commit -m <message>
  ```

- 用版本库里的版本替换工作区的版本

  ```shell
  $ git checkout
  ```

### `Git`连接远程仓库

- 生成ssh密钥供本地与GitHub使用

  ```shell
  $ ssh-keygen -t rsa -C "youremail@example.com"
  ```

- 将公钥填入GitHub，进入account setting，ssh key，添加公钥内容

- 登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：

- 本地的仓库下运行命令

  ```shell
  $ git remote add origin git@github.com:useremail/learngit.git
  ```

- 把本地库的所有内容推送到远程库上

  ```shell
  $ git push -u origin master
  ##由于远程库是空的，第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令
  $ git push origin master
  ```

### `Git`从远程仓库克隆

- 生成git协议链接

- 从远程仓库收取克隆

  ```shell
  $ git clone git@github.com:michaelliao/gitskills.git
  ```

### `Git`分支

- 查看分支

  ```shell
  $ git branch
  ```

- 创建分支

  ```shell
  $ git brach <devname>
  ```

  

- 切换分支

  ```shell
  $ git checkout <devname>
  ```

  

- 创建+切换分支

  ```shell
  $ git checkout -b <devname>
  ```

  

- 合并分支至当前分支

  ```shell
  $ git merge <devname>
  ##强制禁用Fast forward,保存分支信息
  $ git merge --no--ff -m "commitmessage" dev
  ```

  

- 删除分支

  ```shell
  $ git branch -d <devname>
  $ git branch -D <devname>
  ##使用强制删除，未提交的分支
  ```

### Bug分支

- 建立临时分支，保存分支工作

  ```shell
  $ git stash
  ```

  

- 查看分支工作暂存

  ```shell
  $ git stash list
  ```

  

- 恢复分支工作

  ```shell
  $ git stash aplly
  ##恢复之后stash内容不删除，需要使用以下命令
  $ git stash drop
  
  $ git stash pop
  ##恢复同时将stash内容删除
  
  $ git stash apply stash@{0}
  ##恢复指定stash
  ```

  