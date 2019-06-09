# Git 学习笔记 #1

## Git 基本命令 - 对文件的修改删除等
---- 
### 初始化git仓库
```bash
$ git init 
```

### 添加文件到仓库
```bash
$ git add <file> //可以添加多个文件
$ git commit -m <message> //一次性提交多个文件修改
```
> git分为工作区和暂存区
> `git add`将工作区文件放入暂存区
> `git commit`将暂存区文件提交到当前分支

### 查看文件修改状态
```bash
$ git status
```
*可以查看当前文件的修改以及提交状态：是否被修改、是否提交修改*

### 对比文件不同
```bash
$ git diff <file>
```

### 进入Vim编辑器
```bash
$ vi <file> //可以新建文件也可以修改文件
```
> 按ESC键 跳到命令模式，然后：
> :w 保存文件但不退出vi 
> :w file 将修改另外保存到file中，不退出vi 
> :w! 强制保存，不退出vi 
> :wq 保存文件并退出vi 
> :wq! 强制保存文件，并退出vi 
> q: 不保存文件，退出vi 
> :q! 不保存文件，强制退出vi 
> :e! 放弃所有修改，从上次保存文件开始再编辑

### 查看文件历史版本
```bash
$ git log //由近到远显示文件的历史版本
```

*利用额外的参数`--pretty=oneline`缩略显示 commit id*
```bash
$ git log --pretty=oneline
```

### 返回之前的版本
*当前版本被指针`HEAD`指向*
*前一个版本就是`HEAD^`*
*上上个版本是`HEAD^^`*
*前一百个版本是`HEAD-100`
```bash
$ git reset --hard HEAD^  //回到前一个版本
$ git reset --hard <commit id> //回到某个特定的commit id的版本
```

### 显示历史版本的commit id
```bash
$ git reflog 
```

### 丢弃工作区的修改
```bash
$ git checkout -- <file>
```

### 撤销暂存区的修改，使其重新回到工作区
```bash
$ git reset HEAD <file>
```

### 删除文件
`rm <file>` //删除文件，但版本库中依旧还有该文件
- 如果确实想删除：利用 `git rm <file>` 添加“删除文件”的修改到暂存区；再利用 `git commit -m"remove file"` 提交到分支(类似于提交一个修改）
- 如果是误删，利用撤销命令 `git checkout -- <file>` ，撤销工作区的“删除”修改。