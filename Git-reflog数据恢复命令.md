`git reflog`命令可以对git误操作进行数据恢复。

如不小心用`git commit --amend`当成`git commit`覆盖当前的commit，或不小心把当前的commit给搞没了（`reset --hard`）。
都可以通过`git reflog`恢复。

Git记录每次修改HEAD的操作，`git reflog`/`git log -g`可以查看所有的历史操作记录，然后通过`git reset`命令进行恢复。


[Reference](http://git-scm.com/book/zh/Git-%E5%86%85%E9%83%A8%E5%8E%9F%E7%90%86-%E7%BB%B4%E6%8A%A4%E5%8F%8A%E6%95%B0%E6%8D%AE%E6%81%A2%E5%A4%8D)
