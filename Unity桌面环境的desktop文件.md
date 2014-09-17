Unity桌面的launcher启动的应用程序是通过`*.desktop`文件管理的，一个应用程序对应一个`.desktop`文件，统一
放在`/usr/share/applications`目录下。

可以自己添加.desktop文件来增加应用程序到launcher里，*.desktop文件格式如下：

```
[Desktop Entry]
Version=1.6
Name=ProgramName
Comment=My comment is this
Exec=/path/to/executable
Icon=/path/to/icon
Terminal=false
Type=Application
Categories=Utility;Application;
```