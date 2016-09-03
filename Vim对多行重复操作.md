在normal模式下，`.`能在当前所在行重复上一行的操作。如何一次重复多行？

1. 进入visual模式，选中你要操作的行
2. 输入`:`进入命令模式，此时vim的最下面一行会显示`:'<,'>`，然后输入`norm! .`即可。

另外，也适用于寄存器保存的操作。我们可以使用vim中的寄存器保存我们想重复的复杂操作：

1. normal模式键入`qa`(a是寄存器的名字)，然后开始操作。
2. 操作完后，回到normal模式，键入`q`, 此时，所有操作的存储在`a`寄存器里
3. 移到所在的行，在normal模式下`@a`, 执行记录的操作。（或者在visual模式下选中行，键入`norm! @a`）

### References

* help complex-repeat in vim.
* http://stackoverflow.com/questions/390174/in-vim-how-do-i-apply-a-macro-to-a-set-of-lines