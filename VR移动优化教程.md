此教程由 [@a1156883061](https://github.com/a1156883061) 提供

# VR移动优化教程

操作在 Quest 手柄上验证，其它手柄应该可以参照

## 官方操作的痛点
需要移动时，必须按 B/Y 切换到标签为 Hand 的手，且手靠近 UI 面板时，还会屏蔽移动功能。看起来只是多一点操作，但是移动的操作太频繁了，会导致这点操作会很麻烦。

所以就有了下面推荐的插件

## 1.VibeYourMaid插件移动教程
[VibeYourMaid](https://uu.getuploader.com/com3d2_mod_kyouyu_g/download/330) 作者：[ankokusamochi](https://x.com/ankokusamochi)

注意不要开着插件 UI，否则会很卡，你可以在设置里调整为插件 UI 默认不开启

这个插件原本是实现在任何时候和女仆色色的插件，ankokusamochi 在原本的基础上，添加了很多VR里实用的功能

<img width="1350" height="1090" alt="image" src="https://github.com/user-attachments/assets/3f570591-081e-4379-aa3b-8a98c6cc80be" />

<img width="1301" height="1059" alt="image" src="https://github.com/user-attachments/assets/d72d40d2-68ff-4c7a-8448-273d06507087" />


要让添加的VR操作生效，需要先在设置里打开，位置如图
`Settings->Various Setting->VR設定->VRショートカット有効`

这个设置画面，有女仆在场时，会自动打开

<img width="828" height="1600" alt="image" src="https://github.com/user-attachments/assets/2bfef7f1-bb68-4a64-8c32-290b803d6216" />


打开后，按键映射如上图，这是插件里自带的说明

简单来说就是按住左扳机开启移动，左握把键减速移动

左摇杆前后左右移动，右摇杆上下移动和左右旋转

其它的按键都是和移动无关的了

游戏里面，需要在设置->VR CONFIG中，把移动方式，改为`ワープ＆網引き`，不然会导致和原游戏的操作有冲突

这样就实现了在任何手模式都可以移动，包括加载了[COM3D2_5.GripMovePlugin_0.8.9.4修正版](https://ux.getuploader.com/scarletkom_mod/download/45) 后，使用插件新增的手类型时

这个的缺点是，相比revive+官方的方案，移动时多了一个按扳机的操作，具体要哪个看自己的抉择了

## 2.GripMovePlugin

地址 [COM3D2_5.GripMovePlugin_0.8.9.4修正版](https://ux.getuploader.com/scarletkom_mod/download/45) 或 [InoryS版](https://github.com/InoryS/COM3D2.GripMovePlugin.Plugin) InoryS 是更新且支持 COM3D2.5 的，推荐使用

这是一个拖拽移动的插件，但是同时也支持在 VR 中点击第三方插件的 UI

### 插件教程以及推荐设置

想要启用这个插件的功能，需要切换到它自己新增的手类型

具体就是长按 B/Y 键开启新增的手类型，游戏中显示为 DIRECT

需要注意的是，长按后不会切换到DIRECT手，需要按B/Y再切换到DIRECT手，切换到DIRECT手后，才能使用拖拽移动的功能

想要操作第三方插件的UI，也需要先切换到DIRECT手

<img width="400" height="459" alt="image" src="https://github.com/user-attachments/assets/6754be73-f36e-41ee-8ffc-9bc212dd4b60" />


打开右上的设置栏，可以调整插件的设置，设置为上图，基本是最好的

另外还有一个推荐的设置，需要在`COM3D2\Sybaris\UnityInjector\Config\gripmoveplugin.ini`中设置
```
MoveSelfButton=Grip
MoveScreenButton=Trigger
```
将上面这两项设置改为上面的样子

原本是扳机键拖拽移动，但是我觉得握把键拖拽移动更符合直觉，而且和`VibeYourMaid`的按扳机移动不冲突
