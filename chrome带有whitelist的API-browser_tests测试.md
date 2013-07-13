**启动白名单的web app**

命令行参数：`chrome.exe --whitelisted-extension-id=XXX`。
extension_id查看方法，load进chromium后在extension页面查看

`manifestion.json`文件`key`域，官方文档解释：

> "key" : public key.
> This value can be used to control the unique ID of an extension, app, or theme when it is loaded during development.

> To get a suitable key value, first install your extension from a .crx file (you may need to upload your extension or package it manually). Then, in your user data directory, look in the file Default/Extensions/<extensionId>/<versionString>/manifest.json. You will see the key value filled in there.

`key`域一般不需要用到，用途是保证安装在chrome上时，ID是唯一的并且不变，不管load多少次。一般用在chromium的browser_tests测试中。
获得“public key”方法：使用chromium的package功能把extension源码打包成crx安装文件，然后安装。生成`Default/Extensions/<extensionId>/<versionString>/manifest.json`文件，文件中就有key的值，记录下来复制到源码的`manifestion`文件中即可。

**Chromium限制性API的browser_test测试**

* 测试的extension代码需要使用whitelist启动，启动参数需要指定extension id到whitelist中。
* manifest中`key`域，保证每次加载进来的extension的id保持不变，与1对应。
* manifest中要有相关的`permission`域, 如`permission: ["systemInfo.storage"]`。

**chrome extension api权限控制相关C++代码**

* `chrome/common/extensions/permissions/api_permission.h`
* `chrome/common/extensions/permissions/chrome_api_permissions.cc`
* `chrome/common/extensions/api/_permission_features.json` // 控制API能够被哪种类型web app使用（extension, packaged_app, hosted_app, platform_app）
* `chrome/common/extensions/api/_api_features.json`  // API feature, 匹配manifest文件的permission field