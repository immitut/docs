# git action

使用 rebase 替换 merge 合并分支代码
将 main 分支拉至最新
切换到需要 rebase 的分支 feature
执行 git rebase main
若存在冲突，解决冲突后 git add .
再执行 git rebase --continue
完成

对比 merge 合并分支代码，main 分支在合并后不会多出一个新的 commit 节点，整个分支树简洁直观
