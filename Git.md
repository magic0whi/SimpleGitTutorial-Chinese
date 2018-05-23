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

## commit stage空间中的改变
