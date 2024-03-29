> **不要升级 MacOS 14，升级后无法驱动无线网卡。WiFi、蓝牙失效，无法使用 隔空投送 等功能。**  
> 解决方案 OpenCore Legacy Patcher 仍存在较多问题  
> https://heipg.cn/tutorial/patch-brcm-wireless-card-macos-sonoma.html  
> https://igeekbb.com/2023/09/27/Hackintoswifi/

![](images/EFI.png)

![](images/overview.png)

## 使用

通过 GenSMBIOS 生成新的三码，替换 /EFI/OC/config.plist 文件中

```xml
<dict>
    <key>SystemSerialNumber</key>
    <string>W00000000001</string>
</dict>
```
```xml
<dict>
    <key>MLB</key>
    <string>M0000000000000001</string>
</dict>
```
```xml
<dict>
    <key>SystemUUID</key>
    <string>00000000-0000-0000-0000-000000000000</string>
</dict>
```

## 配置

| 配件 | 型号 |
| ---- | ---  |
| CPU  | i5 10400 |
| 内存 | 金士顿 骇客神条 2666 8G x 2 |
| 主板 | 华擎 B460M-ITX/ac |
| 硬盘 | ~~三星 500GB M.2 NVMe 970 EVO Plus~~ 西数 Blue SN570 1T |
| 显卡 | iGPU |
| 显示器 | DELL U2718Q |
| CPU风扇 | 酷冷至尊 T520 |
| 电源 | SFX 500W（全汉 MS500） |
| 机箱 | Formula X1（Ghost s1 六水复刻版） |
| 无线网卡 | BCM94360CS2（散热器限高，通过转接线安装） |

## 功能

#### 正常

+ MacOS Big Sur
+ 接力、随航；（如接力有问题，退出所有设备的 icloud 账号，重新登陆）
+ 夜览；
+ 音量调节；
+ 显示器亮度调节（通过 MonitorControl ）；
+ CPU 变频；
+ 视频硬解码；
+ 网卡；
+ 休眠（休眠遇到问题，可以尝试通过 Hackintool-电源 进行检查并修复）；
+ ...

#### 记录

+ 970 EVO Plus 硬盘，如果启动 MacOS 非常慢，可以尝试将 SetApfsTrimTimeout 配置改为 0。（改为0后启动变快，但不确定是否有其他潜在影响，自行判断）

## 版本

| 驱动 | 说明 |
| ---- | ---- |
| OpenRuntime.efi | 运行环境 |
| OpenCanopy.efi | 图形化界面 |
| AudioDxe.efi | 音频驱动，以支持开机音效 |
| CrScreenshotDxe.efi | UEFI截图工具（F10） |
| [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/tree/master/Drivers) | HFS |

| 组件 | 说明 | 版本 |
| ---- | ---- | ---- |
| [OpenCore](https://github.com/acidanthera/OpenCorePkg/releases) | 引导程序 | 0.8.6 |
| [Lilu](https://github.com/acidanthera/Lilu/releases) | 内核扩展 | 1.6.2-RELEASE |
| [CPUFriend](https://github.com/acidanthera/CPUFriend/releases) | 电源管理 | 1.2.6-RELEASE |
| [VirtualSMC & SMCProcessor & SMCSuperIO](https://github.com/acidanthera/VirtualSMC/releases) | SMC模拟器 | 1.3.0-RELEASE |
| [WhateverGreen](https://github.com/acidanthera/WhateverGreen/releases) | 显卡（GPU） | 1.6.1-RELEASE |
| [AppleALC](https://github.com/acidanthera/AppleALC/releases) | 声卡驱动 | 1.7.6-RELEASE |
| [IntelMausi](https://github.com/acidanthera/IntelMausi/releases) | Intel网卡（LAN）驱动 | 1.0.7-RELEASE |
| [NVMeFix](https://github.com/acidanthera/NVMeFix/releases) | NVMe存储驱动 | 1.1.0-RELEASE |
| [USBInjectAll](https://github.com/daliansky/OS-X-USB-Inject-All/releases) | USB | 0.7.7-RELEASE |
| [XHCI-unsupported](https://github.com/daliansky/OS-X-USB-Inject-All) | USB | master |
| [MonitorControl](https://github.com/MonitorControl/MonitorControl/releases) | 显示器亮度控制 | 4.0.2 |
| USBPorts.kext | USB 定制 | - |

## 主题

可在 github 上通过 OpenCanopy 关键词搜索获得，下载后替换 EFI/OC/Resources/Image 下文件。

+ 默认主题
    - https://github.com/acidanthera/OcBinaryData
+ blackosx
    - https://github.com/blackosx/OpenCanopyIcons 推荐
    - https://github.com/blackosx/OpenCanopyIconPacks
    - https://github.com/blackosx/OpenCanopyIcons-CC0
+ https://github.com/pkdesign/OpenCanopyIcons
+ https://github.com/khronokernel/OpenCanopy-Big-Sur

## 制作工具

| 工具 | 说明 | 版本 |
| ---- | ---- | ---- |
| [Python](https://www.python.org/downloads/) | 基础软件；制作工具运行需要； | 3.9.0 |
| [7Zip](https://www.7-zip.org/download.html) | 基础软件；gibMacOS 运行需要 | 15.14 |
| [gibMacOS](https://github.com/corpnewt/gibMacOS) | Mac下载 & U盘制作 | master |
| [SSDTTime](https://github.com/corpnewt/SSDTTime) | SSDTs 制作 | master |
| [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) | SMBIOS 制作 | master |
| [ProperTree](https://github.com/corpnewt/ProperTree) | OpenCore 配置文件编辑工具 | master |
| [Hackintool](https://github.com/headkaze/Hackintool/releases) | 黑苹果 & USB定制 | 3.6.2 |

**注1** 整体制作环境为 Windows；

**注2** Python 需添加至环境变量 PATH；

**注2** 如 7-ZIP 非默认安装路径，可以修改 gibMacOS 的 MakeInstall.py 文件
```python
self.z_path64 = os.path.join(os.environ['SYSTEMDRIVE'] + "\\", "Program Files", "7-Zip", "7z.exe")
```

## 测试工具

| 工具 | 说明 | 版本 |
| ---- | ---- | ---- |
| [Intel-Power-Gadget](https://software.intel.com/content/www/us/en/develop/articles/intel-power-gadget.html) | CPU 变频&功率监控 | 3.7.0 |
| [VideoProc](https://www.videoproc.com/download-record-video/) | 视频硬解码测试 | 3.9 |
| [Geekbench](https://www.geekbench.com/download/) | 性能测试 | 5.2.5 |
| [Cinebench](https://www.maxon.net/en/cinebench) | 性能测试 | R20 |

## 更新工具

| 工具 | 说明 |
| ---- | ---- |
| [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools) | OpenCore 及 kext 升级 |

## 感谢

+ OpenCore 及相关制作工具、主题、测试工具

+ B站 司波图 视频教程
    - https://www.bilibili.com/video/BV1uf4y1X7MT

+ OpenCore 手册
    - 官方手册 https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Configuration.pdf
    - Dortania 制作的安装手册 https://dortania.github.io/OpenCore-Install-Guide/
    - 中文 https://oc.skk.moe/

+ https://github.com/WenvyG/ASRock-B460M-ITX-ac-Hackintosh

+ https://github.com/ansonliao/Asrock-B460m-ITX-AC-OC-EFI
