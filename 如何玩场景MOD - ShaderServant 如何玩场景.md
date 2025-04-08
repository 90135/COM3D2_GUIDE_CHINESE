# 如何玩场景 MOD - ShaderServant 如何玩场景

一直以来都以为 NPRShader.Plugin 才能玩场景？  

其实 ShaderServant 也可以！

<br>

下了一堆场景和小物件不知道怎么用？

就在这里！

<br>

本文动作确认版本 COM3D2 2.43.1

## 依赖插件

#### 注：本教程不使用 COM3D2.NPRShader.Plugin 而是使用 ShaderServant

[为什么不用 NPRShader？](https://90135.gitbook.io/com3d2_simple_mod_guide_chinese/fu-lu/shaderservant-he-materialeditor-de-an-zhuang)

如果你使用 CMI（目前版本 2.6.4.1），那么你只需要安装 DanceCameraMotion 和 PartEdit 和插件汉化，推荐为 ShaderServant 补充着色器：[教程](https://90135.gitbook.io/com3d2_simple_mod_guide_chinese/fu-lu/shaderservant-he-materialeditor-de-an-zhuang)

1. [COM3D2.DanceCameraMotion.Plugin](https://uu.getuploader.com/com3d2_mod_kyouyu_g/download/225) 无论做什么，都离不开 DCM，注意作者有时候会发更新包，里面缺文件，需要从基础包打
2. [COM3D2.ShaderServant.Plugin](https://github.com/krypto5863/COM3D2.ShaderServant) 使用高级材质需要使用 SS [安装教程](https://90135.gitbook.io/com3d2_simple_mod_guide_chinese/fu-lu/shaderservant-he-materialeditor-de-an-zhuang)
3. [COM3D2.SceneCapture.Plugin](https://ux.getuploader.com/sixima3d2/) 用于调整滤镜效果，原作者已停止分发，需要从 CMI 获取：[https://github.com/krypto5863/COM-Modular-Installer](https://github.com/krypto5863/COM-Modular-Installer)
4. 可选：插件汉化：[https://github.com/90135/COM3D2_Plugin_Translate_Chinese](https://github.com/90135/COM3D2_Plugin_Translate_Chinese)
5. 可选：[PartEdit 插件](https://ux.getuploader.com/com3d2_mod_kyouyu_g/download/51)，可以移动/旋转物体骨骼，可以方便的摆位置或者有的物件有关节什么的可以移动

找插件更新可以去这里：[https://motimoti3d.jp/blog-entry-590.html](https://motimoti3d.jp/blog-entry-590.html)

## 开始

场景 MOD 是一种需要配合插件才能够玩的东西，有一点点门槛

### model 格式

mod 里面有 .model 文件的即为此种

以 DaggerPuck 大佬做的红墙竹影 MOD 为例。

[https://discord.com/channels/297072643797155840/426725636367974410/1348299025874554881](https://discord.com/channels/297072643797155840/426725636367974410/1348299025874554881)

下载后有这么些东西

首先阅读 readme，查看是否有特殊需求，也是对作者的尊重（这个 MOD 没有）。

![图片](https://github.com/user-attachments/assets/a962fcaf-2e9a-49a3-97fc-1238724212d1)

在你的 `COM3D2/MOD` 文件夹内专门新建一个 `场景` 文件夹，以免后面找不到，把解压后放进去

<br>

如果 MOD 内包含一个 .xml 文件，打开看看开头是不是
```
<?xml version="1.0" encoding="utf-8"?>
<Preset>
```
如果是，那么大概率是放到 `COM3D2\Sybaris\UnityInjector\Config\SceneCapture\Presets` 的 SceneCapture 预设文件。

如果 MOD 内只有一个 .xml 文件，那么它是一个组合场景 MOD，需要看 readme 下载组件。

<br>

![图片](https://github.com/user-attachments/assets/45782551-257c-4a3f-a3ab-5bc351fd8a34)

放完后就可以打开游戏了

<br>

进入摄影模式或者编辑模式，推荐摄影模式，因为我的编辑模式有点卡卡的

先用官方菜单召唤出一个妹抖，否则部分功能不可用

![图片](https://github.com/user-attachments/assets/6a13aa36-c30c-4693-8743-a07ea959ac06)

然后打开 DCM （齿轮菜单或 Shift + K）

找到这里

![图片](https://github.com/user-attachments/assets/634d5750-407b-4fcd-87b4-9c76447cd1c5)

切出游戏，打开刚刚放 MOD 的地方，点开 menu 文件夹（因 mod 而定，总之是要找到 .menu 或 .model 文件）

可以看到这个 MOD 带了一个 .menu 文件（因为 COM3D2 的 .model 只能存储 65535 个顶点，所以部分场景会有分件，也就是多个 .menu 和多个 .model）

![图片](https://github.com/user-attachments/assets/4e0a5bad-fbe5-4bb3-bd11-2b8448d9f63b)

复制文件名，填入 DCM，点加载

有多个 .menu 的情况下就加载多次，没有 .menu 的情况下就加载 .model

![图片](https://github.com/user-attachments/assets/1e3f4e9c-a8d7-4e37-a01c-beb1e17cc342)

可以看到模型被加载出来了

![图片](https://github.com/user-attachments/assets/1b9a970f-202a-4b35-ad65-f4ffef364ad1)

然后点击移除背景

![图片](https://github.com/user-attachments/assets/e4a8b128-eeb8-4614-8a4a-1ec19f2776f6)

把原有的背景删除掉

![图片](https://github.com/user-attachments/assets/c567dda9-03e8-4ef1-81d4-a98200367896)

恭喜你学会了怎么玩背景 MOD

DCM 的这个功能非常强大，如果你懂你点 MOD，你可能知道 MOD 是分部位的，但是依靠 DCM 的这个功能，我们可以无视部位随意呼出模型，也不需要依赖女仆才能装备物品。

所以如果你做 MDO，无论是做场景，还是做物件，这个都是非常实用的。

但是这个场景还不是完整体，还记得刚刚的 SceneCapture 预设吗。

点击齿轮菜单中的彩色图标呼出 SceneCapture，取消掉模型和相机的选项。

![图片](https://github.com/user-attachments/assets/cf99c1e8-4757-40d3-8410-324cbf6be8bd)

然后找到对应预设文件点加载

![c41a1c99-d04f-4043-89a4-13870c335657](https://github.com/user-attachments/assets/8da2848f-ad06-4f2a-83c2-7a794f8e8128)

恭喜，你获得了完全体场景。

请自行探索其他选项。

在这里填好预设名称后可以保存，下次就不用找 .menu 了

![图片](https://github.com/user-attachments/assets/fd472317-fff5-45fc-99db-97e14e9da22c)

当然，你也可以手动增删预设而不需要打开游戏，预设在 `"X:\HG\maid\COM3D2\Sybaris\UnityInjector\Config\DanceCameraMotion\StageModel.xml"`

相信你看一下就知道怎么编写了。

### asset_bg 格式

mod 文件里面有 .asset_bg 的即为此种

待续

## 注意事项

### 不要用 SceneCapture 召唤场景

SceneCapture 召唤出来的场景 ShaderServant 无法对其生效，不建议使用。

例如这是用 SceneCapture 直接召唤出来的场景：

可见灯笼无法发亮等问题存在

![image](https://github.com/user-attachments/assets/d25a737f-9613-4984-a617-d5550b0261fc)


### SceneCapture 插件不生效，一直报错

如果你的 SceneCapture 插件一直报错，而且调整没有任何效果，大概率是配置文件有问题，请从 CMI 重新获取一份

截至目前 CMI 版本为 2.6.4.1，SceneCapture 不再更新，如果以后的版本没有了，可以回来找。

下载 CMI，新建一个空目录，CMI 内勾选 COM3D2.SceneCapture.Plugin

安装后把 `CMI2.6.4.1\Sybaris\UnityInjector\COM3D2.SceneCapture.Plugin.dll` 放到 `COM3D2\Sybaris\UnityInjector\"` 文件夹

把 `CMI2.6.4.1\Sybaris\UnityInjector\Config\SceneCapture"` 文件夹覆盖到 `COM3D2\Sybaris\UnityInjector\Config\SceneCapture`

感谢 znq19 哥大发现，不然还以为 SS 不能用 SC。

### SceneCapture 无法恢复默认

SceneCapture 无法恢复默认，所以你需要保存一个默认状态下的预设，然后加载该预设返回默认状态

### 日语

注：日本人说的 SS 一般是是指截图，不是 ShaderServant 插件

## 其他

znq19 哥编写的教程：

注：ZOD 论坛，需要登录，无账号也可直接查看下面的百度盘，目前开放注册注册邀请码可以随便填写

 - [[教程] [250316]想让女仆跳更多舞蹈的不要错过※超简单的DCM跳舞插件使用教程（DanceCameraMotion教程和指路）](https://zodgame.xyz/forum.php?mod=viewthread&tid=480009&extra=page%3D1%26filter%3Dtypeid%26typeid%3D500)
 - [[教程] 移植制作DCM舞蹈教程指路（DanceCameraMotion插件舞蹈移植）](https://zodgame.xyz/forum.php?mod=viewthread&tid=480092&extra=page%3D1%26filter%3Dtypeid%26typeid%3D500)
 - [[教程] DCM舞蹈插件简单快速制作歌词的教程（DanceCameraMotion歌词教程和参数）](https://zodgame.xyz/forum.php?mod=viewthread&tid=480013)
 - 超简单的DCM跳舞插件使用教程：https://pan.baidu.com/s/1vOmbX_ntow7lZTCLH4MuoA?pwd=ka1g 提取码: ka1g
 - DCM舞蹈插件简单快速制作歌词的教程：https://pan.baidu.com/s/1LvY7u1NowIzClFtRAAyqfA?pwd=2m2x 提取码: 2m2x

