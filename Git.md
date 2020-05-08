# 配置ssh连接

- 生成一个密钥(ssh key)，默认生成在~/.ssh/id_rsa

`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

- 添加生成的密钥到ssh-agent

启动ssh-agent

`eval $(ssh-agent -s)`

eval能够执行后面的语句，如
```
xxx@xxx ~/ $ export foo="uname -a"
xxx@xxx ~/ $ echo ${foo}
uname -a
xxx@xxx ~/ $ eval ${foo}
MINGW64_NT-10.0 DESKTOP-S2CIOP8 2.10.0(0.325/5/3) 2018-03-15 14:12 x86_64 Msys
```

添加刚刚生成的密钥到ssh-agent

`ssh-add ~/.ssh/id_rsa`

如果是Windows用户，可以设置ssh-agent自动启动

https://help.github.com/articles/working-with-ssh-key-passphrases/#auto-launching-ssh-agent-on-git-for-windows

# 创建仓库

## 克隆(Clone)一个已经存在的仓库

`git clone ssh://user@domain.tld/repo.git`

## 递归克隆一个已经存在的仓库和它所有的子模块

`git clone --recurse-submodules ssh://user@domain.tld/repo.git`

## 创建一个新的本地仓库(local repository)

`git init`

# 配置

所有没有--global的设置都储存在当前项目仓库中

## 设置提交(commit)时你的署名

`git config [--global] user.name <name>`

## 设置提交时你的邮箱

`git config [--global] user.email <email>`

## 输出彩色的命令行界面

`git config [--global] color.ui auto`

## 打印你的署名（当前仓库或全局）

`git config [--global] user.name`

## 打印你的邮箱（当前仓库或全局）

`git config [--global] user.email`

# 管理本地改动(changes)

## 列出当前工作目录下的文件改动(状态)

`git status`

## 查看具体文件内容的修改（以diff的形式）

`git diff`

## 同步单个更改的文件到stage空间

`git add <file>`

## 同步所有更改的文件到stage空间（为提交做准备）

`git add .`

## 交互式地同步更改的文件到stage空间

`git add -p <file>`

## 重命名文件并立即将更改同步到stage空间

`git mv <file> <new file name>`

## 删除文件并将更改同步到stage空间

`git rm <file>`

## 提交所有追踪(tracked)的文件（git能识别到的文件）改动

`git commit -a`

也可以

`git add .`

`git commit`

## 提交stage空间中的改动（staged文件）

`git commit`

## 修改上次提交的信息(messages)

`git commit --amend`

注意：你不应该修订(amend)已经发布到远程服务器的提交

# 提交历史

## 查看所有的提交

`git log`

## 显示指定文件随时间的变化

`git log -p <file>`

## 显示指定提交者(committer)随时间的变化（查看他的commits）

`git log --author=<committer name>`

注意：<committer name>是一个pattern，所以Ed匹配Edward Smith。如果pattern有空格，那么得引号包裹。

pattern：类似于正则表达式中的匹配符

## 根据给定的字符串搜索（grep）提交的信息

`git log --grep=<string>`

## 查看是谁在何时改变了文件的哪些内容

`git blame <file>`

## 临时储存当前改动（切换分支时临时保存当前工作区和stage区的更改，即保留当前工作现场）

`git stash`

## 还原并删除stashed的工作现场

`git stash pop`

## add一个删除文件的更改但并不删除文件

`git rm --cached <file>`

# 分支(Branches)&标签(Tags)

## 列出所有分支

`git branch`

## 切换HEAD指向的分支

“HEAD”是一个指针，它决定当前的commit会提交到哪里

`git checkout <branch>`

## 基于当前的HEAD创建一个新分支

`git branch <new-branch>`

## 基于远程分支创建一个新的追踪(tracking)分支（--track自动设置上游分支仓库）

`git branch --track <new-branch> <remote-branch>`

## 删除一个本地分支

`git branch -d <branch>`

## 删除一个远程分支

`git push origin --delete <branch>`

## 本地重命名一个分支

`git branch -m <old name> <new name>`

## 重命名远程分支

`git push <remote> :<old name>`

`git push <remote> <new name>`

## 给当前提交添加标签

`git tag <tag-name>`

# 更新(Pull) & 推送(Push)

## 列出当前配置的远程仓库(remotes)

`git remote -v`

## 查看某个远程仓库的信息

`git remote show <remote>`

## 添加一个新的远程仓库

`git remote add <remote> <url>`

## 重命名一个远程仓库

`git remote rename <old-name> <new-name>`

## 下载所有远程仓库的改动，但是**不合并(merge)到HEAD**

`git fetch <remote>`

## 下载所有远程仓库的改动，但是不合并到HEAD**也不清理远程仓库上已经删除的分支**

`git fetch -p <remote>`

## 下载改动(changes)同时直接合并到HEAD

`git pull <remote> <branch>`

## 推送本地的改动到远程仓库

`git push <remote> <branch>`

如果是在本地创建的仓库而且是第一次推送，需要加上"-u"

`git push -u <remote> <branch>`

## 追踪一个远程仓库

`git remote add --track <remote-branch> <remote> <url>`

## 推送当前标签

`git push --tags`

## 复位基底Rebase

普通的merge操作增加一个commit来合并，而用rebase可以避免
Rebase的真实用途是让log看起来更简洁(但rebase操作对其他人很不友好)

具体用法:
```console
$ git rebase -i HEAD~10
```
然后在打开的文件中修改, 将 commit 前的 `pick` 改成:
* `edit` 如果你想修改这次 commit 的改动内容和信息
* `squash` 如果你想将此 commit 合并到上面那行的 commit 里

## 合并分支到当前的HEAD

`git merge <branch>`

## Rebase分支到当前的HEAD

`git merge <branch>`

注意：你不因该rebase公共的remote！（否则会干扰别人）

## 驳回当前的rebase操作

`git rebase --abort`

## 继续rebase操作（解决冲突后）

`git rebase --continue`

## 解决冲突（用你配置的合并工具）

`git mergetool`

## 手动解决冲突（使用你的编辑器并标记文件冲突已解决）

`git add <resolved-file>`

强行删除，最为致命

`git rm <resolved-file>`

# 撤销操作(Undo)

## 撤销工作区(working directory)的所有更改

`git reset --hard HEAD`

--soft – 缓存区和工作目录都不会被改变

--mixed – 默认选项。缓存区和你指定的提交同步，但工作目录不受影响

--hard – 缓存区和工作目录都同步到你指定的提交

## 丢弃指定文件的改动

`git checkout HEAD <file>`

## 创建一个相反改动(changes)的提交来还原（Revert）一个提交的更改

`git revert <commit>`

## 从以前的某次提交恢复文件

`git checkout <commit> <file>`

## 重置（Reset）HEAD指针到**以前的提交**

- 撤销本地所有的改动（重置工作目录和stage空间并更改HEAD）

`git reset --hard <commit>`

- 保留所有改动但将它们unstaged（只清理stage空间和更改HEAD）

`git reset <commit>`

- 保留未提交(uncommitted)的本地改动（清理工作目录但不清理stage空间并更改HEAD。**同时，如果有某个文件在<commit>与HEAD之间有修改并且在stage空间中也有修改，此次reset将被中止**）

`git reset --keep <commit>`

# 子模块（submodules）

## 子模块相当于嵌套在Git中的Git仓库，它同样可以做平常Git仓库能做的事

子模块是为了多团队开发而设计

## 列出当前配置的子模块

`git submodule`

或者

`git submodule status`

## 查看某个submodule的信息

`git remote show <remote>`

## 添加一个新的子模块

注意：如果你想删除子模块并将它的所有文件add到外面的Git仓库中，那么请在子模块的名字后面加上一个正斜杠(/)

1. 执行 `git submodule add -b <branch> --name <name> <repository-path-or-url>`

2. 添加 `.gitmodule` 文件和`submodule的文件夹`到超级项目（superproject）的目录（index）中。

superproject：包含有子模块的仓库

3. 在超级项目提交(commit)此次更改

## 删除一个子模块

1. 从`.gitmodules`删除相应的行

2. 从`.git/config`删除相关部分

3. 运行 `git rm --cached <submodule-path>`(路径不用后跟斜杠(/))

4. 在超级项目提交(commit)此次更改

5. 现在可以删除未追踪(untracked)的模块文件了

## 克隆(Clone)一个带有子模块的仓库

1. 首先像平时那样克隆超级项目的仓库

2. 执行`git submodule init`来初始化子模块

3. 执行`git submodule update`来抓取子模块

或者

直接执行`git clone --recurse-submodules ssh://user@domain.tld/repo.git`

## 查看子模块的改动

`git diff --submodule`

## 更新子模块各自的当前分支到最新的改动(changes)

`git submodule update --remote`

## 更新某个指定的submodule到它当前分支的最新changes

`git submodule update --remote <submodule-name>`

## 只有当所有submodules都推送(push)成功了，才推送superproject的changes

`git push --recurse-submodules=check`

## 推送子模块上的改动，然后再推送超级项目的改动

`git push --recurse-submodules=on-demand`

## 向每个子模块执行任意命令(批量操作)

`git submodule foreach '<arbitrary-command-to-run>'`
