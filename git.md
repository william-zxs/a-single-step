# git操作指北

##git merge & git rebase

**git rebase** 提交记录会是一条直线，每个人的提交不会按时间排序分散开来，比较容易查看log，排除bug

**git merge** 如果双方都有前进，会生成一条merge记录，原先的分叉会继续保留，git log --graph会保留分叉记录，git log 查看双方提交将会按照提交时间排序。 

**git rebase -i**

```
todo
```

git pull 默认策略是merge

##git log --graph --oneline -20

git log可以显示所有提交过的版本信息，不包括已经被删除的 commit 记录和 reset 的操作

## git reflog



git reflog是显示所有的操作记录(本地从clone以来的记录)，包括提交，回退的操作。一般用来找出操作记录中的版本号，进行回退。

git reflog常用于恢复本地的错误操作



## git cherry-pick id

将某分支的某个提交在当前分支做一次提交



## git checkout

```
切换到某分支
git checkout id

根据当前分支创建并切换到新的分支
git checkout -b 

缓存区覆盖掉工作区域
git checkout demo.py 
```

