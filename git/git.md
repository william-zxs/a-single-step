# git操作指北

##工作区，暂存区，本地仓库，远程仓库

git管理的文件有三种状态：已修改（modified）,已暂存（staged）,已提交(committed)



##git merge & git rebase

**git rebase** 提交记录会是一条直线，每个人的提交不会按时间排序分散开来，比较容易查看log，排除bug

**git merge** 如果双方都有前进，会生成一条merge记录，原先的分叉会继续保留，git log --graph会保留分叉记录，git log 查看双方提交将会按照提交时间排序。 

**git rebase -i**

```
git rebase -i  asdadsadaddadada
一个自己分支比较早的hashid，就可以选择保留哪些提交，删除掉哪些提交。
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

## git init



初始化仓库

```
git init 
```



在服务器创建仓库

```
初始化不带工作区的仓库
git init --bare  

更改仓库所属用户
chown -R git:git runoob.git
```

git init --bare  和 git init 不同的分析



##git fetch



会更新本地仓库所有分支的代码，用于查看远端的更新

## git remote 

产看 增加 删除远端分支





# git工作流程



#github上fork别人之后如何同步原作者



添加多个远端









