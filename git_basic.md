#git 基础
### git add
将文件进行跟踪并加入暂存区(保存快照)
### git status
查看git仓库目录下所有文件的状态.
### git status -s
查看git仓库目录下所有文件的状态并用简写的方式显现出来.
### git commit
提交版本，或快照。
### git commit -a
 只要在提交的时候，给 git commit 加上 -a 选项，Git就会自动
 把所有已经跟踪过的文件暂存起来一并提交(切记慎重)，从而自动完成 git add 步骤。
### .gitignore
文件 .gitignore 的格式规范如下：
- 所有空行或者以 ＃ 开头的行都会被 Git 忽略。
- 可以使用标准的 glob 模式(shell所使用的简化的正则表达式)匹配。
- 匹配模式可以以（/）开头防止递归。
- 匹配模式可以以（/）结尾指定目录。
- 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。

.gitignore 文件的例子：
```$xslt
# no .a files
*.a
# but do track lib.a, even though you're ignoring .a files above
!lib.a
# only ignore the TODO file in the current directory, not subdir/TODO
/TODO
# ignore all files in the build/ directory
build/
# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt
# ignore all .pdf files in the doc/ directory
doc/**/*.pdf
```
### git diff
要查看尚未暂存的文件更新了哪些部分，不加参数直接输入 git diff：
此命令比较的是工作目录中当前文件和暂存区域快照之间的差异， 
也就是修改之后还没有暂存起来的变化内容。<br/>
git diff 本身只显示尚未暂存的改动，而不是自上次提交以来所做的所有改动。<br/>
### git log 
git log查看提交历史,当然，常用的参数也是我们必须掌握的:
```$xslt
-p 显示每次提交的内容差异
-number 显示近几次的提交，减少搜索量
--stat 每次提交的简略的统计信息
--pretty 这个选项可以指定使用不同于默认格式的方式展示提交历史  eg：--pretty=online,short，full, fuller 和 但最有意思的 format，可以定制要显示的记录格式。
--since 某个时间段之后(也是可是git log --since=2.weeks 表示最近两周)
--until 某个时间段之前
```
如果要查看 Git 仓库中，2008 年 10 月期间，Junio Hamano 提交的但未合并的测试文件，可以用下面的查询命令：
```$xslt
$ git log --pretty="%h - %s" --author=gitster --since="2008-10-01" \
```
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
### 撤销操作
1.提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了。
eg：
```$xslt
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```