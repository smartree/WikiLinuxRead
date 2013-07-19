在开发过程中，偶尔会遇到rename源文件的情况，一般对源码不做改动，直接修改文件名。

可以使用`git mv old_file_name new_file_name`命令，这样git会自动跟踪rename文件，提交记录显示得很明白，rename前的文件和rename后的文件。当然Git也会自动检测，直接修改文件名，然后通过`git rm`, `git add`也可以实现。

显示的信息如下：
```
git status
...
renamed: .../old_name.cc -> .../new_name.cc
```

如果不仅仅是rename，rename后还对源文件内容进行修改的话，不一定会显示出上面renamed信息。Git的默认`similarity`值是50%，即如果修改内容超过原来50%，就不显示renamed了，而是显示`new file`,`delete file`。

`git diff HEAD -M20`命令可以设置similarity的值，根据similarity的值，显示出renamed或者new的信息。

###Chromium code review显示renamed diff信息

显示renamed的diff信息，这样的diff会有前后对比，方便reviewer review代码，不会像new那样代码全部显示+的。

chromium CL 上传可以通过similarity选项设置阀值，使codereview.com显示的renamed diff信息

```
git cl upload --similarity=XXX //XX是相似百分比
```