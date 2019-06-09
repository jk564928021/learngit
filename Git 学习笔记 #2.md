# Git 学习笔记#2

## Git 远程仓库
### Git 同步本地仓库到远程仓库

1. 在线远程仓库Github创建一个在线的仓库
2. 根据Github提示，同步本地仓库到GitHub仓库
3.  每次在本地修改后，可以利用 `$ git push origin master` 将本地的修改推送到GitHub `master` 分支（`origin`默认表示远程仓库）
4. 第一次推送时需要加上 `-u` 参数，即`$ git push -u origin master` 这样可以将本地`master`分支与远程`master`分支关联

### Git 克隆远程仓库到本地仓库
1. 创建一个远程仓库或者选取一个远程仓库
2. 利用`$ git clone <SSH/http>` 克隆仓库到本地

## Git 分支管理
分支可以让每个码农独立地完成自己的工作部分，比如添加一个新功能，可以在正常完成工作后再合并到一起。

查看分支：`$ git branch`
创建分支：`$ git branch <name>`
切换分支：`$ git checkout <name>`
创建+切换分支：`$ git checkout -b <name>`
合并某分支到当前分支：`$ git merge <name>`
删除分支：`$git branch -d <name>`

## Git 解决冲突
两个分支在相同的文件里均进行了修改，此时要人为解决冲突
在运行 `$ git merge <name>` 后，可以进入文件进行修改，再提交即可解决冲突。
`$ git log --graph --pretty=oneline --abbrev-commit` 图示缩略显示分支历史

## Git 合并后保留合并历史记录
利用`--no-ff`参数
```bash
$ git merge --no-ff -m"<message>" <branchname>
```

## 暂存目前的工作，切换到另一项工作
```bash
$ git stash
```

`git stash list` 查看之前保存的工作现场
`git stash apply` 恢复之前保存的工作现场但stash内容不会删除
`git stash drop` 删除工作现场
`git stash pop` 恢复的同时并删除，等于上面两个命令的叠加

## 强行删除分支（未合并的分支）
```bash
$ git branch -D <branchname>
```

##  多人协作工作模式
1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！
如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令
`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

## 将本地未push的分叉提交历史整理成直线
```bash
$ git rebase
```

## 标签管理
### 打标签
**打标签之前要切换到对应分支**
`git tag <name>` 打标签到最新的commit
`git tag` 查看所有标签
`git tag <name> <commit id>` 给之前对应的commit打标签
`git show <tagname>` 查看标签信息
### 创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字:
```bash
$ git tag -a <tag name> -m "message" <commit id>
```
### 删除标签
```bash
$ git tag -d <name>
```
### 同步远程标签
- 命令`git push origin <tagname>` 可以推送一个本地标签；
- 命令`git push origin --tags` 可以推送全部未推送过的本地标签；
- 命令`git tag -d <tagname>` 可以删除一个本地标签；
- 命令`git push origin :refs/tags/<tagname>` 可以删除一个远程标签。














