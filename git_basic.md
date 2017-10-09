#git 基础

# git基础实践
### 1.查看已跟踪文件修改变化
 第一步:git status 查看修改文件的状态<br/>
 当文件同时出现在Changes to be committed:与Changes not staged for commit:时，表示文件已跟踪且在上一次加入到暂存区之后又被修改了。
 <br/>
 第二步:git diff 查看暂存前后的变化<br/>
 第三步:git diff --cached 查看已经暂存起来的变化：（--staged 和 --cached 是同义词）
### 2.提交更新
在使用git commit之前，我们需要使用git status查看是否所有需要commit的文件是否已经加入到stage里面，
以免有遗漏造成不必要的麻烦，git commit只会提交暂存区的内容，也就是说没有在暂存区的内容将继续被留着本地。
值得注意的一点是，如果在git add之后修改了内容，而未再一次的git add，git commit也只会提交上一次git add所暂存的内容，请牢记。
<br/>
在提交的时候有两种方式添加提交说明：
- git commit -m "提交说明"
- git commit （会自动启动文本编辑器以便输入本次提交的说明）

`git config --global core.editor 命令设定你喜欢的编辑软件`
### 移除文件
`rm filename`删除的只是本地文件，却并未从stage中移除，也就是说会在未暂存清单中出现，再使用git rm才会真正的从
暂存区移除，并保存记录，下一次提交时自然不会再纳入版本管理。
***如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 -f（译注：即 force 的首字母）***

第二种情况，当我们想从缓存区移除文件，但又想在本地磁盘保留，当你忘记添加 .gitignore 文件，不小心把一个很大的日志文件或一堆
 .a 这样的编译生成文件添加到暂存区时，这一做法尤其有用。 为达到这一目的，使用 --cached 选项：
```
$ git rm --cached README
```
### 当我们在本地误删文件时，如何有版本控制找回来
+ 1.git status 
+ 2.`git checkout filename or directory`

若在删除之后又提交了一次，则需要回退到提交之前的最新版本
### 当我们使用git rm误删文件时，如何回退
1.使用git log 查看提交日志，找到最近的commit id
2.按ctrl+c退出当前，使用 git reset --hard "commit id"

上面这种方法是比较恶心的，因为它会完全的回退到上个版本，而我们不过是想回退到删除之前时的状态，
那我们应该这样做:<br/>

```
git status 文件是绿色
git reset HEAD filename 将指针指向被删的文件
git status 发现文件已经变为红色
git checkout filename 
ls  发现文件已经找回
```
原理会在后面部分讲述，这样做的好处第一是不用回到上一个版本而造成其它文件修改被复原，
第二是完全符合我们的需求，可以继续做我们将要做的事情。

# 撤销操作
### 1.撤销操作
提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了。
eg：
```$xslt
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
$ git commit -m ""  --amend
```
### 2.取消暂存的文件
当我们想将文件分成两次独立提交，但是却使用了git add * 将文件
全部加入到暂存区时，我们可以使用如下命令将其从stage中移出去:
```$xslt
git reset --hard（这里可以不加该选项) filename
```
不难发现我们已经看到几次`git reset --hard`，这个我们会在后面进行深入的讲解，<a href="">揭秘git reset</>。
### 3.撤销对文件的修改  
1. git status 查看当前状态
2. git checkout -- filename (切记，当前命令时非常危险的，它会丢失所有的修改，且找不回来，经过本人实践测试，发现只会对已
修改暂存区外状态的文件有用，对于已经加入到stage中的文件是无丝毫的作用的。和官方文档中说回到上一次commit状态是有冲突的。)

注意：如果你仍然想保留对那个文件做出的修改，但是现在仍然需要撤消，我们将会在 Git 分支 介绍保存进度与分支；这些通常是更好的做法。

记住，在 Git 中任何 已提交的 东西几乎总是可以恢复的。 甚至那些被删除的分支中的提交或使用 --amend 选项覆盖的提交也可以恢复（阅读 数据恢复 了解数据恢复）。 然而，任何你未提交的东西丢失后很可能再也找不到了。

# 远程仓库的使用
### 远程仓库的使用
为了能在任意 Git 项目上协作，你需要知道如何管理自己的远程仓库。
远程仓库是指托管在因特网或其他网络中的你的项目的版本库。
你可以有好几个远程仓库，通常有些仓库对你只读，有些则可以读写。 
与他人协作涉及管理远程仓库以及根据需要推送或拉取数据。 
管理远程仓库包括了解如何添加远程仓库、移除无效的远程仓库、管理不同的远程分支并定义它们是否被跟踪等等。
### 克隆远程仓库
```
 git clone git@github.com:ctbu-organnization/awesome-git.git
 git branch -a (查看所有分支)
 git remote -v (列出所有的远程分支)
```
### 添加远程仓库
 ```
 git remote add myq git@github.com:ctbu-organnization/awesome-git.git
 ```
### 从远程仓库中抓取与拉取
 ```
  git fetch [remote-name]
```
这个命令会访问远程仓库，从中拉取所有你还没有的数据。 执行完成后，你将会拥有那个远程仓库中所有分支的引用，可以随时合并或查看。

必须注意 git fetch 命令会将数据拉取到你的本地仓库 - 它并不会自动合并或修改你当前的工作。 当准备好时你必须手动将其合并入你的工作。
### 推送到远程仓库
当你想分享你的项目时，必须将其推送到上游。 这个命令很简单：git push [remote-name] [branch-name]。 

当你想要将 master 分支推送到 origin 服务器时（再次说明，克隆时通常会自动帮你设置好那两个名字），那么运行这个命令就可以将你所做的备份到服务器：
```
 git push origin master

```
### 查看远程仓库
 ```
  git remote show [remote-name]
```
### 远程仓库的移除与重命名
```
 git remote rename oldname newname
 git remote rm name
```
# 打标签
### 列出标签
```$xslt
git tag 列出所有标签
git tag -l 'v1.8.5*'  列出以v1.8.5开头的标签
```
### 附加标签（annotated）
```$xslt
git tag -a v1.4 -m 'my version 1.4'
```

### 轻量标签（lightweight）
```$xslt
git tag v1.4-lw
```
### 查看标签信息
通过使用 git show 命令可以看到标签信息与对应的提交信息：
```$xslt
$ git show v1.4
```
### 后期打标签

```$xslt
$ git tag -a v1.2 9fceb02(提交的部分校验和) 也可以加入-m参数加入版本信息
```
### 共享标签
默认情况下，git push 命令并不会传送标签到远程仓库服务器上。 在创建完标签后你必须显式地推送标签到共享服务器上。这个过程就像共享远程分支一样 - 你可以运行 git push origin [tagname]。
```$xslt
$ git push origin v1.5
```
如果想要一次性推送很多标签，也可以使用带有 --tags 选项的 git push 命令。 这将会把所有不在远程仓库服务器上的标签全部传送到那里。
```$xslt
$ git push origin --tags
```
在 Git 中你并不能真的检出一个标签，因为它们并不能像分支一样来回移动。 如果你想要工作目录与仓库中特定的标签版本完全一样，可以使用 git checkout -b [branchname] [tagname] 在特定的标签上创建一个新分支：
### 根据标签创建分支
如果你想要工作目录与仓库中特定的标签版本完全一样，可以使用 git checkout -b [branchname] [tagname] 在特定的标签上创建一个新分支：
```$xslt
$ git checkout -b version2 v2.0.0
```
