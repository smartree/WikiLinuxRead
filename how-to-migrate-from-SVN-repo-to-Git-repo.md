Create a user.txt files for mapping programmers to Git:

```
Abc = name@email.com
bcd = name@email.com
```

Then run the following commands:
```
git svn clone --stdlayout --no-metadata -A users.txt svn://hostname/path dest_dir-tmp
cd dest_dir-tmp
git svn fetch
```

Reference: <http://stackoverflow.com/questions/79165/how-to-migrate-svn-with-history-to-a-new-git-repository>

