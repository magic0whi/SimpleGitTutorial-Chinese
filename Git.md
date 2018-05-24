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

注意：你不应该amend已经发布的commits

## commit历史

## 查看所有的commits

`git log`

## 显示指定文件随时间的变化

`git log -p <file>`

## 显示指定committer随时间的变化

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
