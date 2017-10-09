# awesome-git
企业项目git协作实战教程
## [git配置](https://github.com/ctbu-organnization/awesome-git/blob/master/git_config.md)
git有三种配置

- 系统配置 使用git config --system 属性名 属性值配置
- 用户配置 使用git config --global 属性名 属性值配置
- 仓库配置 使用git config --local 属性名 属性值配置
[more>>](https://github.com/ctbu-organnization/awesome-git/blob/master/git_config.md)

## [git基础](https://github.com/ctbu-organnization/awesome-git/blob/master/git_basic.md)
### 1.查看已跟踪文件修改变化

第一步:git status 查看修改文件的状态
当文件同时出现在Changes to be committed:与Changes not staged for commit:时，表示文件已跟踪且在上一次加入到暂存区之后又被修改了。 
第二步:git diff 查看暂存前后的变化
第三步:git diff --cached 查看已经暂存起来的变化：（--staged 和 --cached 是同义词）

## 2.提交更新

在使用git commit之前，我们需要使用git status查看是否所有需要commit的文件是否已经加入到stage里面， 以免有遗漏造成不必要的麻烦，git commit只会提交暂存区的内容，也就是说没有在暂存区的内容将继续被留着本地。 值得注意的一点是，如果在git add之后修改了内容，而未再一次的git add，git commit也只会提交上一次git add所暂存的内容，请牢记。 
在提交的时候有两种方式添加提交说明：
```
git commit -m "提交说明"
git commit （会自动启动文本编辑器以便输入本次提交的说明）
git config --global core.editor 命令设定你喜欢的编辑软件
```
[more>>](https://github.com/ctbu-organnization/awesome-git/blob/master/git_basic.md)
## [git命令](https://github.com/ctbu-organnization/awesome-git/blob/master/git_command.md)

## [git流程](https://github.com/ctbu-organnization/awesome-git/blob/master/git_flow.md)

## [git分支](https://github.com/ctbu-organnization/awesome-git/blob/master/git_branch.md)

## [git协作](https://github.com/ctbu-organnization/awesome-git/blob/master/git_cooperation.md)

## [git原理](https://github.com/ctbu-organnization/awesome-git/blob/master/git_theory.md)

版权说明:<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享署名-非商业性使用-相同方式共享 4.0 国际许可协议</a>进行许可。
