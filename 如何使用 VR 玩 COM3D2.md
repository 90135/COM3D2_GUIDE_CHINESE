# COM3D2/CM3D2 VR 优化指南：如何同时拥有高清画质与舒适操作


本指南主要针对 COM3D2 以及 COM3D2.5 v3.41.0 之前的版本以及 CM3D2。

如果你的 COM3D2 已经是 v3.41.0 或更高版本，游戏已经原生支持 OpenXR 标准。请直接启动游戏（必须通过 COM3D2.exe 而不是 COM3D2x64.exe）即可获得最佳体验，无需折腾本文所述内容。

COM3D2.exe 的设置里面有个 `VR 启动` 勾选上以后主界面就会有个 `VR OFF` 的按钮，点成 `VR ON` 就可以启动了。

如果你使用 HTC Vive，那么 SteamVR 模式也是专为你的手柄设计的，直接启动就行了。

## 问题

由于 COM3D2（以及前作 CM3D2）的开发年代较早，那时候 VR 行业还处于“群雄割据”的时代。每家硬件厂商都有自己的 SDK，互不通用。

KISS 社在开发 VR 模式时，内置了两套逻辑：

OculusVR 模式：专为 Oculus Rift 设计。
OpenVR (SteamVR) 模式：专为 HTC Vive 设计。

然而，由于游戏自身实现的问题，这两个模式都有各自的问题：

- OculusVR 模式游戏画面会变糊
- OpenVR 模式操作不舒服（专为 HTC vive 手柄设计）

### 手柄问题

这是 HTC vive 手柄的布局：

<img width="300" height="300" alt="图片" src="https://github.com/user-attachments/assets/379111d3-1caf-444c-9c79-3a4f653d252d" />

现在的机型应该都是下面这种布局的手柄（来自 Oculus Rift (CV1)），称为 Oculus 布局，恰好，COM3D2 的 OculusVR 模式就是为这款机型设计的。

<img width="300" height="300" alt="图片" src="https://github.com/user-attachments/assets/3c322959-1bec-4f2b-ba6c-94e1822b7e5c" />

所以如果你用 Oculus 布局的手柄，然后用 OpenVR 模式启动游戏，就会得到如此反人类的操作：

| 按键 (Quest/Pico) | 游戏内功能       | 体验评价           |
|-----------------|-------------|----------------|
| 摇杆 (垂直按下)       | 确认 / 点击     | ❌ 极度难受，极易误触且费力 |
| 侧握键 (Grip)      | 切换平板电脑 (菜单) | ❌ 容易在抓取物体时误触   |
| A 键 / X 键       | (无功能或未知)    | ❌ 浪费了最常用的交互键   |
| B 键 / Y 键       | 切换工具        | ⭕ 尚可           |
| 左扳机 + 左摇杆 (推拉)  | 水平移动        | ❌ 组合键移动非常繁琐    |
| 左扳机 + 左摇杆 (左右)  | 以某点为中心旋转    | ❌ 容易晕 VR       |
| 右扳机 + 右摇杆 (推拉)  | 垂直移动        | ❌ 同上           |

正常操作是：

| 按键 (Quest/Pico) | 游戏内功能       | 体验评价                |
|-----------------|-------------|---------------------|
| A 键             | 确认 / 点击     | ✅ 符合现代 VR 操作直觉      |
| B 键（长按）            | 切换工具        | ✅ 方便                |
| 右摇杆 (直接推拉)      | 第一人称移动      |    |
| 右摇杆 (垂直按下)      | 切换平板电脑显示 (菜单) |       |
| 侧握键 (Grip)      | 抓取 / 互动     | ✅ 自然                |



### OculusVR 模式画面糊

反编译得知，COM3D2 是通过设备名来判断要使用哪一个 API 的，如果传到游戏内的设备名里带有 oculus 字样（使用 Virtual Desktop 也会有），那么游戏就会进入 OculusVR 模式。

不知道具体什么情况，但是这个模式的画面明显没有 OpenVR 模式清晰，调画质也没用。



## 解决方案

随着时代的发展，我们现在大多使用 Quest 3、Pico 4 等通过串流（Virtual Desktop/Pico 互联），或者 PC VR 直连来玩。

Quest 3 等一体机使用串流软件来玩，串流软件 100% 支持 OpenVR 模式。

PCVR 的的软件同样是 100% 支持 OpenVR 模式。

只有 Virtual Desktop 和 Meta 的原生串流软件（Meta 收购了 Oculus）可以进入 OculusVR 模式。

所以无论你使用哪个串流软件还是 PCVR，解决方案都是一样的。

### 所以有没有一种办法，能结合 OpenVR 和 OculusVR 的好处呢？

**答案就是：Revive。**

Revive 本来是让 HTC Vive 用户玩 Oculus 独占游戏的工具。但在这里，我们利用它的特性来实现“反向操作”：

1.  我们通过 Revive 启动游戏，让游戏误以为自己运行在 Oculus 硬件上（从而激活 **Oculus 舒适的按键映射**）。
2.  COM3D2 进入 OculusVR 模式.
3.  Revive 拦截游戏的 Oculus SDK 调用，将其翻译成 OpenVR 指令。
4.  最终画面由 SteamVR 渲染（从而获得 **SteamVR 的高分辨率和清晰度**），再通过 VD 串流到头显。

也就是说，Revive 能让游戏跑在 OculusVR，然后翻译成 OpenVR 的调用，由 OpenVR 运行时（SteamVR）渲染。


## 3. 操作指南 (COM3D2)

### 步骤一：准备工作

1.  **安装 Revive**：
    *   下载地址：[GitHub - LibreVR/Revive](https://github.com/LibreVR/Revive)
    *   安装后关掉它弹出的界面，我们只需要它的核心文件。
2.  **获取 DLL 文件** (如果遇到黑屏)：
    *   Revive 有时需要 Oculus 的运行时库。如果启动黑屏，请下载 `LibOVRRT64_1.dll`。
    *   将该 DLL 文件放在游戏根目录，即 `COM3D2x64.exe` 的旁边。
    *   *注：如果你使用 VD，通常 VD 目录下也有这个文件，但为了保险建议手动放一个。*
    *   要获取这个 dll，最安全的方法是下载 [Meta Horizon Link](https://www.meta.com/help/quest/1517439565442928/?srsltid=AfmBOoroeCRPuUKbhdKzLaMngnyclzt3WDnHSemSwFwXJSYDJdcEDgG1)，然后在安装目录里面搜索这个
    *   你可以用全局搜索工具 Eveyting 搜索电脑上有没有这个 dll，如果有就复制一个过来。

### 步骤二：创建启动脚本

为了方便启动，我们需要创建一个 `.bat` 批处理文件。

1.  在游戏根目录下新建一个文本文件，重命名为 `VR启动(Revive).bat`。
2.  右键选择“编辑”，填入以下代码（请根据你的实际安装路径修改）：

```batch
@echo off
rem 路径说明：
rem Revive路径：通常在 C:\Program Files\Revive\ReviveInjector.exe
rem 游戏路径：你的 COM3D2x64.exe 路径

"C:\Program Files\Revive\ReviveInjector.exe" "K:\HG\maid\COM3D2\COM3D2x64.exe" /VR

exit
```

保存并退出。


### 启动游戏

本文不教一体机怎么串流，请自行搜索`你的型号+串流`。

1. 确保你的头显已连接电脑（一体机也是启动串流软件并连接电脑），必须先连接才能开游戏。
3. 双击运行刚才创建的 VR启动(Revive).bat。
4. 游戏会拉起 SteamVR（你需要先安装这个）。
5. 等待游戏启动。



## 关于 CM3D2

CM3D2 需要转区才能启动，所以启动脚本略有不同



下载 [Locale_Remulator](https://github.com/InWILL/Locale_Remulator/releases) 转区软件

已确认 Locale_Remulator.1.5.4_Latale 版本可以用，其他版本请自行尝试。


新建 .bat 文件，代码如下（注意把 GUID 和路径替换成你自己的）：
```
@echo off
rem === 配置区域 ===
rem LEProc.exe 的路径 (Locale Emulator)
set LE_PATH="K:\Tools\Locale_Remulator\LRProc.exe"

rem ReviveInjector.exe 的路径
set REVIVE_PATH="C:\Program Files\Revive\ReviveInjector.exe"

rem 游戏主程序的路径
set GAME_PATH="K:\HG\maid\CM3D2\CM3D2x64.exe"

rem Locale Emulator 配置文件的 GUID (在 LE 的配置文件中查找 "Run in Japanese" 对应的 GUID)
rem 这一步很重要，不同的 LE 版本或配置 GUID 可能不同
set LE_GUID=bc054398-6240-44c2-814e-2e68734120d6

rem === 启动逻辑 ===
rem 逻辑：转区工具 -> 启动 Revive注入器 -> 启动 游戏 -> VR参数
start "" %LE_PATH% %LE_GUID% %REVIVE_PATH% %GAME_PATH% /VR

exit
```

bc054398-6240-44c2-814e-2e68734120d6 是 Locale_Remulator 安装路径里面的 LRConfig.xml 里面的 Run in Japanese 的 GUID，如果你的不是就改一下


## 技术细节

反编译得知，COM3D2 是通过设备名来判断要使用哪一个 API 的：

Assembly-CSharp.dll\GameMain.cs

```
        if (this.m_bVRMode)
                {
                        string loadedDeviceName = VRSettings.loadedDeviceName;
                        string model = VRDevice.model;
                        UnityEngine.Debug.Log("VR Device " + loadedDeviceName + " / " + model);
                        // 如果设备名称包含 oculus
                        if (loadedDeviceName.ToLower().Contains("oculus"))
                        {
                                // 激活 Oculus 模式：加载 OvrCamera，使用 Oculus 舒适键位
                                this.m_eVRFamily = GameMain.VRFamilyType.Oculus;
                                this.m_eVRDeviceType = GameMain.VRDeviceType.RIFT_TOUCH;
                                UnityEngine.Debug.Log("VR Family is Oculus! " + this.m_eVRDeviceType.ToString());
                                this.OvrInit();
                                base.StartCoroutine(this.CoOvrStart());
                        }
                        // 如果设备名称包含 openvr
                        else if (loadedDeviceName.ToLower().Contains("openvr"))
                        {
                                // 激活 HTC Vive 模式：加载 ViveCameraRig，使用棒子手柄逻辑
                                this.m_eVRFamily = GameMain.VRFamilyType.HTC;
                                this.m_eVRDeviceType = GameMain.VRDeviceType.VIVE;
                                UnityEngine.Debug.Log("VR Family is HTC!");
                                this.OvrInit();
                                this.m_bIsVRDeviceReady = true;
                        }
                        else
                        {
                                VRSettings.enabled = false;
                                this.m_bVRMode = false;
                        }
                }
        }
```




