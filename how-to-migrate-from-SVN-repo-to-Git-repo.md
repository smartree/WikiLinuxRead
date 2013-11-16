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

Reference: 

<http://viget.com/extend/effectively-using-git-with-subversion>

<http://stackoverflow.com/questions/79165/how-to-migrate-svn-with-history-to-a-new-git-repository>

