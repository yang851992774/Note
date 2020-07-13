#### 普通linux命令

| 命令行     | 注释         | 参数                     |
| ---------- | ------------ | ------------------------ |
| cd /c/user | 进入文件夹   | /c/user                  |
| cd ~       | 进入系统Root |                          |
| ls         | 列出所有文件 | 显示文件不隐藏           |
|            |              | -a 显示所有              |
|            |              | -l 不隐藏文件显示详情    |
|            |              | -al 显示所有文件显示详情 |
|            |              |                          |
|            |              |                          |
|            |              |                          |



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
|                        |                                |      |
|                        |                                |      |
|                        |                                |      |
|                        |                                |      |
|                        |                                |      |
| git log                | 查看日志，按q 退出             |      |
| git fetch              |                                |      |
|                        |                                |      |



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

