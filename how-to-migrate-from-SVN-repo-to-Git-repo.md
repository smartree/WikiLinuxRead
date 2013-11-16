## Clone svn repository

Create a user.txt files for mapping programmers to Git:

```
Abc = Abc@email.com
bcd = bcd@email.com
```

Then run the following commands:
```
// If svn repo is std repo, use -s option
git svn clone svn://hostname/path --authors-file=user.txt
// update with svn repo
git svn rebase
// show svn ignore files
git svn show-ignore
```

##Set svn remote url in git repository

If you clone the repository from git directly, you want do update the remote svn repository directly, you need to do following configure:

1.
Edit .git/config files, add following fields:

```
[svn-remote "svn"]
	url = svn://url
	fetch = :refs/remotes/git-svn
[svn]
	authorsfile = authors-transform.txt
```

2.
```
// show commit id
git show origin/master | head -n 1
echo <commit_id> > .git/refs/remotes/git-svn
git svn fetch
```

Reference: 

<http://trac.parrot.org/parrot/wiki/git-svn-tutorial>

<http://viget.com/extend/effectively-using-git-with-subversion>

<http://stackoverflow.com/questions/79165/how-to-migrate-svn-with-history-to-a-new-git-repository>

