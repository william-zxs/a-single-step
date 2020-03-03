# git操作指北

### git merge & git rebase

git rebase 提交记录会是一条直线，每个人的提交不会按时间排序分散开来，比较容易查看log，排除bug

git merge 如果双方都有前进，会生成一条merge记录，原先的分叉会继续保留，git log --graph会保留分叉记录，git log 查看双方提交将会按照提交时间排序。 



### git log --graph

