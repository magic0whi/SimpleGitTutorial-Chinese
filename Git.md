# 创建仓库

## Clone 一个已经存在的仓库

`git cloene ssh://user@domain.tld/repo.git`

## 递归Clone一个已经存在的仓库和它所有的子模块

`git clone --recurse-submodules ssh://user@domain.tld/repo.git`

## 创建一个新的本地仓库

`git init`

# 配置

貌似所有没有--global的设置都储存在当前项目仓库中

## 设置commit时你的署名

`git config [--global] user.name <name>`

## 设置commit时你的邮箱

`git config [--global] user.email <email>`

## 输出彩色的命令行界面

`git config [--global] color.ui auto`

## 打印你的署名（当前仓库或全局）

`git config [--global] user.name`

## 打印你的邮箱（当前仓库或全局）

`git config [--global] user.email`

# 管理本地改变

## 列出当前工作目录下的文件改变(状态)

`git status`

## 查看具体文件内容的修改（以diff的形式）

`git diff`

## 同步单个更改的文件到stage空间

`git add <file>`

## 同步所有更改的文件到stage空间（为commit做准备）

`git add .`

## 交互式地同步更改的文件到stage空间

`git add -p <file>`

## 重命名文件并立即将更改同步到stage空间

`git mv <file> <new file name>`

## 删除文件并将更改同步到stage空间

`git rm <file>`

## commit所有tracked的文件（git能识别到的文件）改变

`git commit -a`

相当于

`git add .`

`git commit`

## commit stage空间中的改变（staged文件）

`git commit`

## 改变最后一次commit（修改上次commit的messages）

`git commit --amend`

注意：你不应该amend已经发布到远程服务器的commits

## commit历史

## 查看所有的commits

`git log`

## 显示指定文件随时间的变化

`git log -p <file>`

## 显示指定committer随时间的变化（查看他的commits）

`git log --author=<committer name>`

注意：<committer name>是一个pattern，所以Ed匹配Edward Smith。如果pattern有空格，那么得引号包裹。

pattern：类似于正则表达式中的匹配符

## 根据给定的字符串搜索（grep）commit的messages

`git log --grep=<string>`

## 查看是谁在何时改变了文件的哪些内容

`git blame <file>`

## 临时储存changes（切换分支时临时保存当前工作区和stage区的更改，即保留当前工作现场）

`git stash`

## 还原并删除stashed的changes

`git stash pop`

## add一个删除文件的更改但并不删除文件

`git rm --cached <file>`

# 分支&标签

## 列出所有分支

`git branch`

## 切换HEAD指向的分支

“HEAD”是一个指针，它决定当前的commit会提交到哪里

`git checkout <branch>`

## 基于当前的HEAD创建一个新分支

`git branch <new-branch>`

## 基于远程分支创建一个新的tracking分支（--track自动设置上游分支仓库）

`git branch --track <new-branch> <remote-branch>`

## 删除一个本地分支

`git branch -d <branch>`

## 删除一个远程分支

`git push origin --delete <branch>`

## 本地重命名一个分支

`git branch -m <old name> <new name>`

##  重命名远程分支

`git push <remote> :<old name>`

`git push <remote> <new name>`

## 给当前commit添加标记（Tag）

`git tag <tag-name>`

# 更新 & 推送

## 列出当前配置的remotes

`git remote -v`

## 查看某个remote的信息

`git remote show <remote>`

## 添加一个新的远程仓库

`git remote add <remote> <url>`

## 重命名一个remote

`git remote rename <old-name> <new-name>`

## 下载所有remote的changes，但是不合并（merge）到HEAD

`git fetch <remote>`

## 下载所有remote的changes，但是不merge到HEAD**也不清理remote上已经删除的branches**

`git fetch -p <remote>`

## 下载changes同时直接merge到HEAD

`git pull <remote> <branch>`

## 推送本地的changes到remote

`git push <remote> <branch>`

## 追踪一个远程仓库

`git remote add --track <remote-branch> <remote> <url>`

## 推送当前tags

`git push --tags`

## Merge & Rebase

## Merge分支到当前的HEAD

`git merge <branch>`

## Rebase分支到当前的HEAD

`git merge <branch>`

注意：你不因该rebase公共的remote！（否则别人会？？？）

## 驳回当前的rebase操作

`git rebase --abort`

## 继续rebase操作（解决冲突后）

`git rebase --continue`

## 解决冲突（用你配置的merge工具）

`git mergetool`

## 手动解决冲突（使用你的编辑器并标记文件冲突已解决）

`git add <resolved-file>`

强行删除，最为致命

`git rm <resolved-file>`

# 撤销操作（Undo）

## 撤销工作区（working directory）的所有更改

`git reset --hard HEAD`

## 丢弃指定文件的更改

--hard 同时清理stage空间和工作空间的对应文件

`git checkout HEAD <file>`

## 创建一个相反changes的commit还原（Revert）一个commit的更改

`git revert <commit>`

## 从以前的commit恢复文件

`git checkout <commit> <file>`

## 重置（Reset）HEAD指针到**以前的commit**

- 撤销本地所有的changes（重置工作目录和stage空间并更改HEAD）

`git reset --hard <commit>`

- 保留所有changes为unstaged的changes（只清理stage空间和更改HEAD）

`git reset <commit>`

- 保留uncommitted的本地changes（清理工作目录但不清理stage空间并更改HEAD。**同时，如果有某个文件在<commit>与HEAD之间有修改并且在stage空间中也有修改，此次reset将被中止**）

`git reset --keep <commit>`

# 子模块（submodules）

## 子模块相当于嵌套在Git中的Git仓库，它同样可以做平常Git仓库能做的事

子模块是为了多团队开发而设计

## 列出当前配置的submodules

`git submodule`

或者

`git submodule status`

## 查看某个submodule的信息

`git remote show <remote>`

## 添加一个新的submodule

注意：如果你想删除子模块并将它的所有文件add到外面的Git仓库中，那么请在submodule的名字后面加上一个正斜杠(/)

1. 执行 `git submodule add -b <branch> --name <name> <repository-path-or-url>`

2. 添加 `.gitmodule` 文件和`submodule的文件夹`到超级项目（submodule外面git仓库，原文superproject）的目录（index）中。

3. 在subproject提交（commit）此次更改

## 删除一个子模块

1. 从`.gitmodules`删除相应的行

2. 从`.git/config`删除相关部分

3. 运行 `git rm --cached <submodule-path>`(路径不用后跟斜杠(/))

4. 在subproject提交(commit)此次更改

5. 现在可以删除未追踪（untracked)的模块文件了

## 克隆(Clone)一个带有submodules的仓库

1. 首先像平时那样Clone superproject的仓库

2. 执行`git submodule init`来初始化submodules

3. 执行`git submodule update`来抓取submodules

或者

直接执行`git clone --recurse-submodules ssh://user@domain.tld/repo.git`

## 查看submodules的changes

`git diff --submodule`

## 更新submodules各自的分支到最新的commit

`git submodule update --remote`
