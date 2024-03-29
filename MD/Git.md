#### 普通 linux 命令

| 命令行     | 注释           | 参数                     |
| ---------- | -------------- | ------------------------ |
| cd /c/user | 进入文件夹     | /c/user                  |
| cd ~       | 进入系统 Root  |                          |
| ls         | 列出所有文件   | 显示文件不隐藏           |
|            |                | -a 显示所有              |
|            |                | -l 不隐藏文件显示详情    |
|            |                | -al 显示所有文件显示详情 |
| cd ~       | 进入用户文件夹 |                          |
|            |                |                          |
|            |                |                          |

#### git 相关命令

|                                                  |                                    |                    |
| ------------------------------------------------ | ---------------------------------- | ------------------ |
| git init                                         | 创建一个目录为 git 仓库            |                    |
| git clone <url>                                  | 克隆仓库                           |                    |
| git status                                       | 查看哪些文件处于什么状态           |                    |
| git add                                          |                                    |                    |
| git commit                                       | wq q! qa!                          | -m -a              |
| git restore                                      |                                    |                    |
| git branch <name>                                | 创建分支<name>                     |                    |
| git branch                                       | 列出所有分支                       | -a \| -d           |
| git checkout [-b] <name>                         | 切换分支                           | -b(创建并切换分支) |
| git merge <branchname>                           | 合并分支<branchname>到当前分支     |                    |
| git push <origin> <local>:<remote>               | 推送分支                           |                    |
| git stash                                        | 将当前工作贮藏                     |                    |
| git stash list                                   | 查看贮藏的列表                     |                    |
| git stash apply                                  | 恢复贮藏中的工作内容               |                    |
| git stash drop                                   | 删除此条贮藏                       |                    |
| git stash pop                                    | 恢复贮藏中的工作内容并删除此条贮藏 |                    |
| git stash clear                                  | 清空 Git 栈                        |                    |
|                                                  |                                    |                    |
|                                                  |                                    |                    |
|                                                  |                                    |                    |
|                                                  |                                    |                    |
|                                                  |                                    |                    |
|                                                  |                                    |                    |
|                                                  |                                    |                    |
| git show <id>                                    |                                    |                    |
| git log --graph --pretty=oneline --abbrev-commit |                                    |                    |
| git log                                          | 查看日志，按 q 退出                |                    |
| git reset                                        | <none>/--soft/--mixed/--hard       |                    |
|                                                  |                                    |                    |

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
# add && commit所有信息
$ git commit -a -m "info"
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

配置 git

git config --global user.name “XXX”
ps：xxx 代表你的用户名
git config --global user.email "XXX@XXX.com"
ps：XXX 输入邮箱
ssh-keygen -t rsa -C "XXX@XXX.com"
ps：生成一个新的 SSH 密钥，一直按回车即可
cd ~/.ssh
ps：去到.ssh 指纹目录
cat id_rsa.pub | clip
ps：拷贝指纹信息

添加 hashKey

### 问题集合

#### 1、贮藏被不小心删除恢复贮藏

1. git fsck --lost-found 查看贮藏记录
2. git show <id> 显示某一条贮藏的摘要
3. git merge <id> 合并被删除的贮藏

#### 2、几种撤销操作

##### Repository->Index (也就是 commit 的撤销 )

git reset --soft HEAD^1 git reset --soft HEAD~1 git reset --soft HEAD~2

解释：不删除工作空间改动代码，撤销 commit，不撤销 git add .

##### Repository->Workspace(也就是 commit 和 Add 两步骤的撤销 )

git reset --mixed HEAD^1 git reset --mixed HEAD~1 git reset --mixed HEAD~2

解释：不删除工作空间改动代码，撤销 commit，并且撤销 git add . 操作

##### Repository->Workspace(也就是 commit 和 Add 两步骤的撤销，并且删除工作空间改动的代码 )

git reset --hard HEAD^1 git reset --hard HEAD~1 git reset --hard HEAD~2

解释：删除工作空间改动代码，撤销 commit，撤销 git add . 注意完成这个操作后，就恢复到了上一次的 commit 状态。真正的全部回滚到上个 commit.

HEAD^的意思是上一个版本，也可以写成 HEAD~1, 如果你进行了 2 次 commit，想都撤回，可以使用 HEAD~2。如果省略 HEAD~1,则是默认回滚到上个提交。

#### 3、合并提交操作

当 git push 之后，发现还有部分内容还没有提交完成，或者遗留提交了部分。

我们一般的做法是直接 commit,再次 push。其实这步操作完全可以合并到一个提交中去。

git commit -amend

#### 4、多人项目如与主干合并

**（feature）**git add/ git commit /git push 一般都在自己 feature 分支开发，提交所有代码至当前分支。

**(feature）**git checkout master

**(master) ** git pull

**(master) ** git checkout feature

**(feature）**git merge master ->解决冲突

**(feature）**git push ->提交合并主干的内容至当前远端分支

**(feature）**git checkout master

**(master) **git merge feature ->解决冲突

**(master) **git push -> 提交合并分支后的内容至远端

**(master) **git checkout feature ->切换分支继续干活

到目前为止，所自己分支的内容和主干的内容会保持完全一样的版本。形成一个闭环

#### 5、多人项目提交代码

**（feature）**git pull 先拉取一下，看是否有冲突

无冲突

**（feature）**git add/ git commit /git push

有冲突

**（feature）**git add/ git commit

git pull 先拉取一下,一定是可以拉取的解决冲突之后

git commit / git push

#### 5、彻底回滚某一个版本

git reset --hard [HEAD^1] ->回滚至上一个提交

git pull origin master ->拉取最新版本

#### 6、贮藏与清理的作用

当我在 feature1 开发有一段时间后，所有的东西都是一个混乱状态，这个时候需要切换到 feature2 做一点点事情，问题是现在不想因为过一会回到这点而做了一半的工作创建一次提交。这种场景用到贮藏。

#### 7、git 命令别名

alias g='git'

#### 8、测试恢复删除的分支

git log -g 查看记录，找到你需要恢复的最后一次 commit 的 hash 值

git branch <recover_branch_name> <hashid>

git clean -f/-n/-df/-xf

-n 是一次 clean 的演习, 告诉你哪些文件会被删除. 记住它不会真正地删除文件, 只是一个提醒。

-f 删除当前目录下所有没有 track 过的文件. 它不会删除 .gitignore 文件里指定的文件夹和文件, 不管这些文件有没有被 track 过

#### 9、重置到上次一模一样的状态

工作目录和缓存区回到最近一次 commit 时候一摸一样的状态

git reset --hard

git clean -df

--创建子树

```

https://blog.csdn.net/lupengfei1009/article/details/103099820
https://segmentfault.com/a/1190000012002151

tip:
1、用那个版本合并那个版本 feature/100
2、GBFramework 子树添加时候的文件夹路径必须不存在，否则会ad d
git subtree add --prefix=Tower/Assets/GBFramework git@gitlab.corp.cootek.com:lunar/gb_game/gb_framework.git feature/100 --squash

git subtree add   --prefix=<prefix> <commit>
git subtree add   --prefix=<prefix> <repository> <ref>
git subtree pull  --prefix=<prefix> <repository> <ref>
git subtree push  --prefix=<prefix> <repository> <ref>
git subtree merge --prefix=<prefix> <commit>
git subtree split --prefix=<prefix> [OPTIONS] [<commit>]

git subtree pull --prefix=Lick/Assets/GBFramework git@gitlab.corp.cootek.com:lunar/gb_game/gb_framework.git feature/100 --squash

--拉取子项目。解决需要把项目的所有修改解决掉，才能拉取成功
Working tree has midification. Cannot add.

1、
git subtree add --prefix=GoldMiner git@gitlab.corp.cootek.com:lunar/gb_game/gbgamebase.git develop --squash
git subtree add --prefix=GoldMiner/Assets/GBFramework git@gitlab.corp.cootek.com:lunar/gb_game/gb_framework.git feature/100 --squash

```



**gitlab复制分支到新的项目**

git pull git地址 分支名称



```text
//将65be1e5这条提交合并到当前已签出的分支
git cherry-pick 65be1e5
```

