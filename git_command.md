 
# git命令
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
