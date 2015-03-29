当远程仓库的被force update（`git push -f`）后，在另外的仓库要更新force update的仓库，直接使用下面命令：

```
git pull --rebase <remote_repo_name> <branch_name>
```