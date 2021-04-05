# Git action

### git clone 远端

### git branch [|-r|-a] 列出本地/远端/所有分支

### git branch [branchName] 新建分支&停留当前分支

### git checkout -b [branchName] 新建分支&切换到该分支

### git checkout - 切换回上一分支

### git add [filePath/dir] 指定文件/目录到暂存区 git add . 即当前目录所有文件

### git status

### git commit [...filePath] -m [msg] 提交暂存区(指定文件或所有)到仓库

### 使用 rebase 替换 merge 合并分支代码

将 main 分支拉至最新

切换到需要 rebase 的分支 feature, 执行 `git rebase main`

若存在冲突，解决冲突后 `git add .` 再执行 `git rebase --continue`

rebase 后切回 main 分支，执行 `git merge feature`

合并完成

对比 merge 合并分支代码，main 分支在合并后不会多出一个新的 commit 节点，整个分支树简洁直观
