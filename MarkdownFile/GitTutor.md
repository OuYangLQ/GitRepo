# GitTutor

## 安装
[git下载地址](git-scm.com)

## 初始化配置
对所有本地仓库的用户信息进行配置

- 对你的commit操作设置关联的用户名
```
git config --global user.name "[name]"
```

- 对你的commit操作设置关联的邮箱地址
```
git config --global user.email "[email address]"
```

- 启用有帮助的彩色命令行输出
```
git config --global color.ui auto
```
## 新建仓库
- 在当前目录下创建仓库：
```
git init
```
- 在当前目录下克隆仓库：
```
git clone "仓库链接地址"
```
## 工作区域
- 工作区：.git所在的目录
- 暂存区：.git/index
- 本地仓库：.git/objects<br>

当前仓库状态:
```
git status
```
文件状态分为：
- Untrack
- Unmodified
- Modified
- Staged

## 添加和提交文件
工作区文件添加到暂存区：
```
git add
```
暂存区文件提交到本地仓库, 使用 -m 选项指定提交信息:
```
git commit -m "提交信息"
```
如果不使用 -m 选项指定提交信息，
Git 会打开默认的文本编辑器（通常是 Vim 或者 Nano），
让你输入提交信息。<br>
如果你想将 Vim 设置为默认的文本编辑器，可以在终端中执行以下命令：
```
git config --global core.editor "vim"
```
查看提交信息：
```
git log
```
如果使用 --oneline 选项可以查看更为简单的信息： 
```
git log --oneline
```
## 回溯版本
- 回溯到某一版本并保留工作区和暂存区的修改内容：
```
git reset --soft "版本号"
```

- 回溯到某一版本并丢弃工作区和暂存区的修改内容：
```
git reset --hard "版本号"
```

- 回溯到某一版本只保留工作区的修改内容：
```
git reset --mixed "版本号"
```
- 列出当前 Git 仓库中所有被跟踪的文件：
```
git ls-files
```
## 查看差异
- 查看工作区和暂存区之间的差异
```
git diff 
```
- 查看工作区和版本库之间的差异
```
git diff HARD
```
- 查看暂存区和版本库之间的差异
```
git diff --cached
```
- 查看不同版本之间的差异
```
git diff "版本号" "版本号"
```
- 查看上一版本和当前版本之间的差异
```
git diff HARD~ HARD
```
- 查看不同分支之间的差异
```
git diff "分支" "分支"
```
## 删除文件
- 把文件从工作区和暂存区中删除
```
git rm "文件名"
```
## 忽略文件
应该忽略的文件通常包含：
- 系统或软件自动生成的文件
- 编译产生的中间文件或结果文件
- 运行时生成的日志、缓存、临时文件
- 涉及身份、密码、口令、密钥等敏感信息文件<br>

匹配规则：
`*.log`：匹配所有以 .log 结尾的文件。
`build/`：匹配 build 目录及其下的所有文件和子目录。
`!error.log`：取消对 error.log 文件的忽略。
`/**/*.tmp`：匹配任意目录下的所有以 .tmp 结尾的文件。
`node_modules/`：忽略 node_modules 目录及其下的所有内容。

gitignore 模板：<https://github.com/github/gitignore>

## 远程仓库

github官方链接：<https://github.com/>

## SSH配置和克隆地址
1. 使用克隆命令在用户目录下生成 .ssh 目录文件：
```
git clone "ssh地址"
```
2. 使用以下一命令进入到 .ssh 目录：
```
cd ~/.ssh
```
3. 使用以一下命令生成 RSA 类型的 **SSH密钥对**，其中 "-b 4096" 指定了密钥长度为 4096 位。这意味着生成的密钥对将使用 RSA 加密算法，并且私钥和公钥的长度都将是 4096 位，这比一般默认的 2048 位更加安全。
```
ssh-keygen -t rsa -b 4096
```
*如果你执行这个命令，它会生成两个文件：一个是私钥文件（通常命名为 id_rsa），另一个是公钥文件（通常命名为 id_rsa.pub）。私钥文件保存在你的本地计算机上，而公钥文件则用于分发给需要信任你的服务器或系统。*

4. 在终端设置密码短语后，就会生成私钥和公钥文件。
<br>
5. 复制公钥文件的内容，把它配置到github。
<br>
1. 最后再一次执行以下命令即可将远程仓库克隆到本地：
```
git clone "ssh地址"
```

## 推送和拉取
- 从本地仓库推送到远程仓库：
```
git push 
```
- 从远程仓库拉取到本地仓库：
```
git pull
```
## 关联本地仓库和远程仓库
使用一下命令将已经存在的本地仓库关联到远程仓库：
```
git remote add origin git@github.com:OuYangLQ/Tutor.git
git branch -M main
git push -u origin main
```
## 分支管理
- 查看分支列表：
```
git branch
```
- 创建分支
```
git branch "branch-name"
```
- 切换分支
```
git switch "branch-name"
```
- 合并分支
```
git merge "branch-name"
```
- 删除分支  
已合并：`git branch -d "branch-name"`  
未合并：`git branch -D "branch-name"`  
## 合并冲突
- 两个分支未修改同一个文件的同一处位置：Git 自动合并 
- 两个分支修改了同一个文件的同一处位置：产生冲突 
- 解决方法：
1. 手工修改冲突文件，合并冲突内容 
2. 添加暂存区：`git add file` 
3. 提交修改：`git commit -m "message"` 
- 终止合并，当不想继续执行合并操作时可以使用下面的命令来终止合并过程： 
`git merge --abort` 
## 变基-rebase
Git 中的 "rebase" 是一种常用的操作，它可以用来将一系列提交（commit）应用到另一个分支上。具体来说，rebase 操作会将当前分支上的提交移动到另一个分支的末尾，从而使得当前分支的历史记录变得更加清晰、线性化：
```
git rebase <branch>
```




 
