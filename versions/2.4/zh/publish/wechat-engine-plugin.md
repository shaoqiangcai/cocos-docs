# 微信小游戏引擎插件使用说明

游戏引擎插件是微信 7.0.7 版本新增的一项功能。此插件内置了 Cocos Creator 引擎的官方版本，若玩家首次体验的游戏中启用了此插件，则所有同样启用此插件的游戏，都无需再次下载 Cocos Creator 引擎，只需直接使用公共插件库中的相同版本引擎，或者增量更新引擎即可。

例如，当一个玩家玩过了由 Cocos Creator v2.2.0 开发的 A 游戏，里面已启用了此插件。然后他又玩了同样是 v2.2.0 开发的 B 游戏，如果 B 游戏也启用了此插件，那么就无需重新下载 Cocos Creator 引擎。即使 B 游戏使用的是 v2.2.1 的 Cocos Creator，微信也只需要增量更新引擎两个版本的差异部分。这样就可以大幅减少小游戏的下载量，提升小游戏启动速度 0.5 ~ 2s，获得更好的用户体验。

## 使用说明

Cocos Creator 提供了强大的集成式游戏开发环境，使用引擎插件非常简单。

### Cocos Creator v2.2.1 及以上版本

在 Cocos Creator v2.2.1 中已集成此插件。只需在 **构建发布** 面板中，勾选 **允许分离引擎**，然后正常构建发布即可，**无需其它人工操作**。（此功能仅在非调试模式生效）

![](./publish-wechatgame/build.png)

### Cocos Creator 2.0.5 ~ 2.2.0 版本

一、下载 Cocos Creator 构建插件

下载地址：[GitHub](https://github.com/cocos-creator/plugin-wechat-engine-separation/archive/master.zip) | [Gitee](https://gitee.com/mirrors_cocos-creator/plugin-wechat-engine-separation)

二、安装插件

- 如需应用于全局（所有项目）下：将解压后的插件文件夹拷贝到 `C:\Users\用户\.CocosCreator\packages`（Windows）或者 `用户/.CocosCreator/packages`（Mac）下即可。
- 如需应用于单个项目：将解压后的插件文件夹拷贝到项目工程的 packages 文件夹下，该文件夹与 assets 文件夹同级。(如果没有 packages 文件夹可以手动创建一个)

三、构建

插件安装完成后，重启 Cocos Creator。然后在 **构建发布** 面板中正常构建发布即可，**无需其它人工操作**。（此功能仅在非调试模式生效）

后续如果需要禁用引擎插件功能，直接删除此插件即可。

### Cocos Creator 2.0.4 及以下版本

根据调查，目前使用 Cocos Creator v2.0.4 及以下版本的开发者占比已经非常少。我们不建议这部分开发者使用引擎插件，因为收效并不明显，反而增大了维护成本。<br />

如果确实需要，建议先升级到 Cocos Creator v2.0.10 或更高版本，高版本对微信小游戏的支持会更好。

### 注意事项

1. 微信开发者工具中的 **详情 -> 本地设置 -> 调试基础库** 需要设置为 **2.9.0** 或以上版本。

2. 微信开发者工具中的 **详情 -> 本地设置 -> 使用本地的插件** 选项，用于设置是否禁用引擎插件，通常 **无需勾选**。（该选项只在微信开发者工具中有效）
    - 若取消勾选，会使用微信公共插件库中的引擎插件版本进行调试。
    - 若勾选，则使用本地构建后生成的引擎插件版本进行调试。

    ![](./publish-wechatgame/setting.png)

## FAQ

Q：微信小游戏开放数据域支持该功能吗？<br />
A：根据微信的规则，目前还不支持。

Q：引擎插件功能是否支持自定义引擎？<br />
A：不支持，构建时只能使用编辑器原版内置引擎，否则编辑器将会弹出提示。

Q：项目开启了引擎的模块裁剪，要使用引擎插件的话需要还原为完整版引擎吗？<br />
A：无需修改，项目可以按原来的方式继续裁剪引擎。引擎插件提供的是完整版引擎，能兼容所有的裁剪设置，不会影响原有项目的包体。

Q：启用引擎插件后，是否仍然会把引擎代码算入首包包体中？<br />
A：根据微信的规则，目前仍然会计算在内。

Q：开启引擎插件后，是否可以在编辑器 **模块设置** 中移除所有模块，减小包体？<br />
A：不可以，因为微信从 7.0.7 开始才支持引擎插件，若随意裁剪引擎可能导致游戏无法在低版本微信上运行。

## Trouble Shooting

Q：Cocos Creator v2.2.0 在 iOS 9 上启用引擎插件后无法进入游戏？<br />
A：非常抱歉，这是已知的兼容性问题，在 v2.2.1 中已进行修复。

Q：启用引擎插件后，在微信开发工具中提示 “代码包解包失败” 或者 “..., 登录用户不是该小程序的开发者”，但真机预览正常？ <br />
A：**构建面板** 中默认的 appid 为通用测试 id，根据微信的规则，如需测试引擎分离功能，需要开发者在 **构建面板** 中填入自己开通的 appid。

Q：启用引擎插件后，在微信开发工具中提示 “插件未授权使用 `添加插件`”？ <br />
A：点击提示中的 `添加插件`，选择添加 CocosCreator 插件后重新编译即可。若添加插件时出现“可添加的插件信息为空”的提示，可尝试在微信开发者工具中选择 **清缓存 -> 全部清除** 后重试。

Q：Cocos Creator v2.1.3 在启用引擎插件后会提示某些 3D 相关函数未定义？<br />
A：这是由于旧版本 Cocos Creator 构建插件的兼容性问题导致的，重新下载最新的 Cocos Creator 构建插件替换即可。

Q：提交审核时弹出 “使用的插件有新版本” 的提示框，能否更新？<br />
A：不能更新，请点击 **确定**。

  ![](./publish-wechatgame/new_plugin.png)

## 参考链接

- [微信小游戏引擎插件官方文档](https://developers.weixin.qq.com/minigame/dev/guide/base-ability/game-engine-plugin.html)