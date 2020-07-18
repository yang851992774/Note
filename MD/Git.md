#### 普通linux命令

| 命令行     | 注释           | 参数                     |
| ---------- | -------------- | ------------------------ |
| cd /c/user | 进入文件夹     | /c/user                  |
| cd ~       | 进入系统Root   |                          |
| ls         | 列出所有文件   | 显示文件不隐藏           |
|            |                | -a 显示所有              |
|            |                | -l 不隐藏文件显示详情    |
|            |                | -al 显示所有文件显示详情 |
| cd ~       | 进入用户文件夹 |                          |
|            |                |                          |
|            |                |                          |



#### git相关命令

|                        |                                |      |
| ---------------------- | ------------------------------ | ---- |
| git init               | 创建一个目录为git 仓库         |      |
| git clone <url>        | 克隆仓库                       |      |
| git status             | 查看哪些文件处于什么状态       |      |
| git add                |                                |      |
| git commit             | wq    q!   qa!                 | -m   |
| git restore            |                                |      |
| git branch <name>      | 创建分支<name>                 |      |
| git branch -a          | 列出所有分支                   |      |
| git checkout <name>    | 切换分支                       |      |
| git merge <branchname> | 合并分支<branchname>到当前分支 |      |
| git push               | 推送                           |      |
| git stash              |                                |      |
| git stash list         |                                |      |
|                        |                                |      |
|                        |                                |      |
|                        |                                |      |
| git log                | 查看日志，按q 退出             |      |
| git fetch              |                                |      |
| git reset              | <none>/--soft/--mixed/--hard   |      |



https://www.jianshu.com/p/46ffff059092

```undefined
Workspace：工作区
Index / Stage：暂存区
Repository：仓库区（或本地仓库）
Remote：远程仓库
```



```ruby
# 在当前目录新建一个Git代码库
$ git init
# 新建一个目录，将其初始化为Git代码库
$ git init [project-name]
# 下载一个项目和它的整个代码历史
$ git clone [url]
```



```ruby
# 显示当前的Git配置
$ git config --list
# 编辑Git配置文件
$ git config -e [--global]
# 设置提交代码时的用户信息
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]”

git 修改当前的project的用户名的命令为：
> git config user.name 你的目标用户名;
git修改当前的project提交邮箱的命令为：
> git config user.email 你的目标邮箱名;
如果你要修改当前全局的用户名和邮箱时，需要在上面的两条命令中添加一个参数，–global，代表的是全局。
命令分别为：
> git config  --global user.name 你的目标用户名；
> git config  --global user.email 你的目标邮箱名;
```



```ruby
# 添加指定文件到暂存区
$ git add [file1] [file2] ...
# 添加指定目录到暂存区，包括子目录
$ git add [dir]
# 添加当前目录的所有文件到暂存区
$ git add .
# 添加每个变化前，都会要求确认
# 对于同一个文件的多处变化，可以实现分次提交
$ git add -p
# 删除工作区文件，并且将这次删除放入暂存区
$ git rm [file1] [file2] ...
# 停止追踪指定文件，但该文件会保留在工作区
$ git rm --cached [file]
# 改名文件，并且将这个改名放入暂存区
$ git mv [file-original] [file-renamed]
```





配置git

git config --global user.name “XXX”
  ps：xxx代表你的用户名
git config --global user.email "XXX@XXX.com"
  ps：XXX输入邮箱
ssh-keygen -t rsa -C "XXX@XXX.com"
  ps：生成一个新的SSH密钥，一直按回车即可
cd ~/.ssh
  ps：去到.ssh指纹目录
cat id_rsa.pub | clip
  ps：拷贝指纹信息

添加hashKey 





### 问题集合

#### 1、贮藏被不小心删除恢复贮藏

1. git fsck --lost-found       查看贮藏记录
2. git show <id>                显示某一条贮藏的摘要
3. git merge <id>              合并被删除的贮藏



#### 2、几种撤销操作

##### Repository->Index (也就是commit的撤销 )  

git reset --soft HEAD^1   git reset --soft HEAD~1  git reset --soft HEAD~2

解释：不删除工作空间改动代码，撤销commit，不撤销git add .

##### Repository->Workspace(也就是commit 和 Add 两步骤的撤销 )  

git reset --mixed HEAD^1   git reset --mixed HEAD~1  git reset --mixed HEAD~2

解释：不删除工作空间改动代码，撤销commit，并且撤销git add . 操作

##### Repository->Workspace(也就是commit 和 Add 两步骤的撤销，并且删除工作空间改动的代码 ) 

git reset --hard HEAD^1   git reset --hard HEAD~1  git reset --hard HEAD~2

解释：删除工作空间改动代码，撤销commit，撤销git add .  注意完成这个操作后，就恢复到了上一次的commit状态。真正的全部回滚到上个commit.



HEAD^的意思是上一个版本，也可以写成HEAD~1,  如果你进行了2次commit，想都撤回，可以使用HEAD~2



#### 3、合并提交操作

当git push 之后，发现还有部分内容还没有提交完成，或者遗留提交了部分。

我们一般的做法是直接commit,再次push。其实这步操作完全可以合并到一个提交中去。

git commit -amend

