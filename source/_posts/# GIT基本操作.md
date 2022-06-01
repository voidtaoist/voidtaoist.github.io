# GIT基本操作
下面是一些日常操作

## 1. 建立本地仓库:

```bash
git init [project-name]  #创建本地仓库
```


```bash
git remote add origin git@github.com:UserName/yourProjectName.git   
#把本地仓库和远程仓库关联起来， 如果不执行这个命令的话，每次 push 的时候都需要指定远程服务器的地址

git remote add origin git@github.com:UserName/yourProjectName.git   
#把本地仓库和远程仓库关联起来， 如果不执行这个命令的话，每次 push 的时候都需要指定远程服务器的地址

git clone https://github.com/zhoulujun/yourProjectName.git
#下载github仓库
```

## 2.提交本地修改到远程仓库中：
``` bash
git add # 将改动添加到本地仓库中  

git add [file1] [file2] ...  ||  git add [dir] # 添加指定文件||目录到暂存区

git add -A ||  git add . # 添加当前目录的所有文件到暂存区

git add -p # 添加每个变化前，都会要求确认，对于同一个文件的多处变化，可以实现分次提交
```

``` bash
git rm xxx      # 从本地仓库中删除指定文件
git rm -r xxx   # 从本地仓库中删除指定文件夹

git rm --cached [file]
```
``` bash
git mv [file-original] [file-renamed]  改名文件，并且将这个改名放入暂存区
```
``` bash
git commit -m "注释"    -- 把本机缓存中的内容提交到本机的 HEAD 里面

git commit -a 提交工作区自上次commit之后的变化，直接到仓库区

git commit -v 提交时显示所有diff信息

git commit --amend -m [message] 使用一次新的commit，替代上一次提交，如果代码没有任何新变化，则用来改写上一次commit的提交信息

git commit --amend [file1] [file2] ... 重做上一次commit，并包括指定文件的新变化
```
``` bash
git push origin master  -- 把本地的 commit(提交) push 到远程服务器上， origin 也就是之前 git remote add origin 那个命令里面的 origin，origin 替代了服务器仓库地址：git@github.com:zhoulujun/yourProjectName.git 

git push remoteBranchName tagName提交指定tag

git push remoteBranchName --tags 提交所有tag
```

## 3. git转态查看
``` bash
git status 查看状态
```
``` bash
git branch 查看本地所有分支

git branch -r查看远程所有分支

git branch -a查看本地和远程所有分支
```
git tag  列出所有tag

git show tagName 查看tag信息

git log --stat 显示commit历史，以及每次commit发生变更的文件

分支操作
git checkout branchName 切换到指定分支，并更新工作区

git merge branchName 合并指定分支到当前分支

git branch newBranchName 新建一个分支，但依然停留在当前分支

git branch --track branch remote-branch 新建一个分支，与指定的远程分支建立追踪关系

git branch -D branchName //删除目标分支

git checkout -b branchName 新建并切换至新分支

git branch -d -r branchName 删除远程分支，其中

git branch -m oldbranchname newbranchname  重命名分支 使用-M则表示强制重命名

重命名远程分支

git branch -m old_name new_name 重命名分支

git checkout -b new_branch_name from_branch_name 本地建立 branch 並立即 checkout 切換過去

git push origin –delete old_name

也可以如此操作

git branch -m old_branch new_branch # Rename branch locally

git push origin :old_branch # Delete the old branch

git push --set-upstream origin new_branch 或者git push -u origin new_branch  # Push the new branch, set local branch to track the new remote

git分支与主干合并操作
在主干上合并分支||主干合并分支
git merge branch --squash //提交合并后的代码

git commit -m  ‘合并备注’

git push //将代码推送到远程仓库

分支同步主干代码||在分支上合并主干
git merge master --squash //提交合并后的代码

git commit -m  ‘合并备注’ //将代码推送到远程仓库

git push //将代码推送到远程仓库

git强制覆盖本地代码
与git远程仓库保持一致

git fetch --all

git reset --hard origin/master

git pull

git强制覆盖本地命令（单条执行）：

git fetch --all && git reset --hard origin/master && git pull

git修改远程仓库地址
方法有三种：

1.修改命令

git remote origin set-url [url]

2.先删后加

git remote rm origin

git remote add origin [url]

3.直接修改config文件

.git文件夹，找到config，编辑，把就的项目地址替换成新的。

git 配置
git config --list        查看配置列表

git config --global user.name "xxx"   -- 配置用户名，上传本地 repository 到服务器上的时候，在 Github 上会显示这里配置的上传者信息

git config --global user.email "xxx"    -- 配置邮箱
配置 sshkey ： 上传代码时使用这个 sshkey 来确认是否有上传权限
    1. 创建本地 ssh ： ssh-keygen -t rsa -C "Github 的注册邮箱"
    2. 在 Github 中添加这个 sshkey ： 
        复制  C:\Documents and Settings\Administrator\.ssh\id_rsa.pub 文件中的内容；
        登录 Github --> Account Setting  --> SSH-KEY --> Add SSH-KEY --> 粘贴id_rsa.pub中的内容；
    3. 验证： ssh -T git@github.com
        出现 Hi xxx! You've successfully authenticated, but GitHub does not provide shell access. 说明配置成功，可以连接上 Github

使用 .gitignore 文件忽略指定的内容：

    1. 在本地仓库根目录创建 .gitignore 文件。Win7 下不能直接创建，可以创建 ".gitignore." 文件，后面的标点自动被忽略；
    2. 过滤文件和文件夹： [Tt]emp/ 过滤 Temp\temp 文件夹； *.suo 过滤 .suo 文件；
    3. 不过滤文件和文件夹： !*.c