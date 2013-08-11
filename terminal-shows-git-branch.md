修改`~./bashrc`文件：

```
// xfce4 termial 自定义termial的输出内容和形式
PS1="( $TXTGRN\u$TXTRST )-( $TXTCYN\w$TXTRST )-\$parse_git_branch\n> "

function parse_git_branch () {
       git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
```