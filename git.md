# git

----
## 常用命令组合

----
### 重置用户名

``` bash
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]"
$ git commit --amend--reset-author
```
-----
### 本地创建远程仓库

``` bash
$ curl -u 'lilei11981' https://api.gitub.com/user/repos/  -d '{"name":"test"}'
```
-------
### 把别人的项目加入到自己的项目中
- $ 在 github 上新建一个 "HelloWorld" 仓库
- $ git clone + 别人项目的链接
- $ git remote -v  (查看项目关联)
- $ git remote remove origin （删除别人 origin 的链接）
- $ rm -rf .git（删除 HelloWorld 文件里的. git 文件）
- $ git init （初始化 .git 文件）
- $ git remote add origin + 自己仓库的地址（在 .git 中增加自己的 origin 的链接）
- $ git pull origin master（与自己的项目同步）

----
### 提交代码常用
- $ git status     (查看当前文件的修改状态)
- $ git add .     (添加所有修改文件)
- $ git commit -m "[message]"    (提交文件并注释)
- $ git push origin master     (把暂存区的文件推送到远程)
> 如果有冲突则在使用push命令之前使用

- $ git pull origin master

--------
### 版本回退
- $ git log (查看历史版本id)
- $ git reset --hard id号 (回退到历史版本)
- $ git push -f origin master (把回退后的版本推送到远程服务器)

----
### 新建代码库
* 在当前目录新建一个Git代码库
- $ git init

* 新建一个目录，将其初始化为Git代码库
- $ git init [project-name]

* 下载一个项目和它的整个代码历史
- $ git clone [url]

----
### 配置
* 显示当前的Git配置
- $ git config --list

* 编辑Git配置文件
- $ git config -e [--global]

* 设置提交代码时的用户信息
- $ git config [--global] user.name "[name]"
- $ git config [--global] user.email "[email address]"

----

### 增加/删除文件

* 添加指定文件到暂存区
- $ git add [file1][file2]...

* 添加指定目录到暂存区，包括子目录
- $ git add [dir]

* 添加当前目录的所有文件到暂存区
- $ git add .

* 添加每个变化前，都会要求确认，对于同一个文件的多处变化，可以实现分次提交
- $ git add -p 

* 删除工作区文件，并且将这次删除放入暂存区
- $ git rm [file1] [file2]...

* 停止追踪指定文件，但该文件会保留在工作区
- $ git rm --caches [file]

* 改名文件，并且将这个改名放入暂存区
- $ git mv [file-original][file-renamed]

----

### 代码提交

* 提交暂存区到仓库区
- $ git commit -m [message]

* 提交暂存区的指定文件到仓库区
- $ git commit [file1] [file2] [file3] [file4] ... -m [message]

* 提交工作区自上次commit之后的变化，直接到仓库区
- $ git commit -a

* 提交显示所有diff信息
- $ git commit -v

* 使用一次新的commit，替代上一次提交
  如果代码没有新变化，则用来改写上一次commit的提交信息
- $ git commit --amend -m [message]

* 重做上一次的commit，并包括指定文件的新变化
- $ git commit --amend [file1] [file2] ...

----

### 分支

* 列出所有本地分支
- $ git branch

* 列出所有远程分支
- $ git branch -r

* 列出所有本地本地分支和远程分支
- $ git branch -a

* 新建一个分支，但依旧停留在当前分支
- $ git branch [branch-name]

* 新建一个分支，并切换到该分支
- $ git checkout -b [branch]

* 新建一个分支，并指向指定commit
- $ git branch [branch][commit]

* 新建一个分支，与指定的远程分支建立追踪关系
- $ git branch --track [branch][remote-branch]

* 切换到指定分支，并更新工作区
- $ git checkout [branch-name]

* 切换到上一分支
- $ git checkout -

* 建立追踪关系，在现有的分支与指定的远程分支之间
- $ git branch --set-upstream [branch] [remote-branch]

* 合并指定分支到当前分支
- $ git merge [branch]

* 选择一个commit，合并当前分支
- $ git cherry-pick [commit]

* 删除分支
- $ git branch -d [branch-name]

* 删除远程分支
- $ git push origin --delete [branch-name]
- $ git branch -dr [remote/branch]

----

### 标签

* 列出所有tag
- $ git tag

* 新建一个tag在当前commit
- $ git tag [tag]  

* 新建一个tag在指定commit
- $ git tag [tag] [commit]

* 删除本地tag
- $ git tag -d [tag]

* 删除远程tag
- $ git push origin :refs/tags/[tagName]

* 查看tag信息
- $ git show [tag]

* 提交指定tag
- $ git push [remote] [tag]

* 提交所有tag
- $ git push [remote] --tags

* 新建一个分支，指向某个tag
- $ git checkout -b [branch] [tag]

----

### 查看信息

* 显示有变更的文件
- $ git status

* 显示当前分支的版本历史
- $ git log

* 显示commit历史，以及每次commit发生变更的文件
- $ git log --stat

* 搜索提交历史，根据关键词
- $ git log -S [keyword]

* 显示某个commit之后的所有变动，每个commit占据一行
- $ git log [tag] HEAD --pretty=format:%s

* 显示某个commit之后的所有变动，其”提交说明“必须符合搜索条件
- $ git log [tag] HEAD --greg feature

* 显示某个文件的版本历史，包括文件改名
- $ git log --follow [file]
- $ git whatchanged [file]

* 显示指定文件相关的每一次diff
- $ git log -p [file]

* 显示过去的5次提交
- $ git log -5 --pretty --oneline

* 显示所有提交过的用户，并按提交次数排序
- $ git shortlog -sn

* 显示指定文件是什么人在什么时间修改过
- $ git blame [file]

* 显示暂存区和工作区的差异
- $ git diff

* 显示暂存区和上一个commit的差异
- $ git diff --cached [file]

* 显示工作区与当前分支最新commit之前的差异
- $ git diff HEAD

* 显示两次提交之前的差异
- $ git diff [first-branch] ...[second-branch]

* 显示今天你写了多少代码
- $ git diff --shortstat "@{0 day ago}"

* 显示某次提交的元数据和内容变化
- $ git show [commit]

* 显示某次提交发生变化的文件
- $ git show --name-only [commit]

* 显示某次提交时，某个文件的内容
- $ git show [commit]:[filename]

* 显示当前分支的最近几次提交
- $ git reflog 

----

### 远程同步

* 下载远程仓库的所有变动
- $ git fetch [remote]

* 显示所有远程仓库
- $ git remote -v

* 显示某个远程仓库的信息
- $ git remote show [remote]

* 增加一个新的远程仓库并命名
- $ git remote add [shortname] [url]

* 取回远程仓库的变化，并与分支合并
- $ git pull [remote] [branch]

* 上传本地指定分支到远程仓库
- $ git push [remote] [branch]

* 强行推送当前分支到远程仓库，即使有冲突
- $ git push [remote] --force

* 推送所有分支到远程仓库
- $ git push [remote] --all

----

### 撤销

* 恢复暂存区的指定文件到工作区
- $ git checkout [file]

* 恢复某个commit的指定文件到暂存区和工作区
- $ git checkout [commit] [file]

* 恢复暂存区的所有文件到工作区
- $ git checkout .

* 重置暂存区的指定文件，与上一次的commit保持一致，但工作区不变
- $ git reset [file]

* 重置暂存区与工作区，与上一次commit保持一致
- $ git reset --hard

* 重置当前分支的HEAD为指定commit，同时重置暂存区，但工作区不变
- $ git reset [commit]

* 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
- $ git reset --hard [commit]

* 重置当前HEAD为指定commit，但保持暂存区和工作区不变
- $ git reset --keep [commit]

* 新建一个commit，用来撤销指定commit
  后者的所有变化都将被前者抵消，并且应用到当前分支
- $ git revert [commit]

* 暂时将未提交的变化溢出，稍后再移入
- $ git stash
- $ git stash pop

----

### 其他

* 生成一个可供发布的压缩包
- $ git archive

----
## gitbook安装过程

* 安装node.js
> 下载地址：https://nodejs.org/en/

* 安装成功后，输入**node -v**，显示node.js版本代表安装成功
* 使用npm包管理工具安装gitbook
* 在Mac下的命令：**sudo npm install gitbook-cli -g**
> -g代表全局安装，使用**gitbook -V**命令查看gitbook版本

* 建立gitbook电子书：目录下有SUMMARY.md（目录文件）和README.md（前言文件）
* 输入**gitbook serve** 在浏览器输入http://localhost:4000 可预览电子书
* 安装calibre
> 下载地址：http://calibre-ebook.com/download

* 输入**gitbook pdf** 可生成PDF文件
* 输入**gitbook mobi** 可生成mobi电子书