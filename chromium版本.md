Google Chromium的Release版本有很多，如何查看已经发布的release版本是基于哪个revision的？

请查看:

* svn这里：<http://src.chromium.org/svn/releases/>
* git这里：<http://src.chromium.org/viewvc/chrome/branches/?pathrev=247367>

Chromium是使用git-svn管理的，主要是svn（历史的缘故），也同时支持git。每一个git的记录都会由git-svn转换成svn revision。

Chromium每个版本的revision有DEPS（在/src下），DEPS文件是指Chromium所依赖third_party库的版本。

不能直接在/src目录下通过'git checkout'命令切换版本，这样third_party的版本会不对应。需要通过`gclient sync --revision <commit_hash> --jobs 8 --force`

commit_hash就是要切换git commit hash值。如何根据svn的revision找到对应的git commit hash值？看这里：<http://git.chromium.org/gitweb/?p=chromium%2Fsrc.git&a=search&h=HEAD&st=commit&s=%40123456>

**Update**：上面的方法已经过时了，现在chromium的代码都用git管理了。

1. 到`https://omahaproxy.appspot.com/`网站上的`position lookup`输入对应release编号，如41.0.2272.76。
会得到对应的`commit id`和`postion id`。

2. 到`http://commondatastorage.googleapis.com/chromium-browser-continuous/index.html?prefix=Win/`上搜索对应步骤1的`position id`则是对应该release下的编译后版本。

**Reference**
* <https://code.google.com/p/chromiumembedded/wiki/BranchesAndBuilding>
* <http://mogoweb.net/archives/389>