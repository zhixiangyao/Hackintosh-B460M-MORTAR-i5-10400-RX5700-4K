## MSI B460M Mortar i5-10400 ➕ iGPU-UHD630 ➕ XFX RX5700 ➕ LG UL850 4K Resolution

### 下载 Download

摇号查看系统信息工具 Hackintool：[Hackintool ](https://www.insanelymac.com/forum/topic/335018-hackintool-v3xx/)

编辑器 Editor：[Visual Studio Code ](https://code.visualstudio.com/)

### 硬件配置

| 配置              | 型号                                                         |
| ----------------- | ------------------------------------------------------------ |
| 处理器 CPU        | Intel Core I5-10400                                          |
| 主板 Motherboard  | 微星 MSi B460M 迫击炮 Mortar                                 |
| 内存 Memory       | 光威 3000Mhz C16 16G\*2                                      |
| 显卡 Video Card   | 核显 UHD630 和 XFX Radeon RX5700 8G                          |
| 网卡 Network Card | Broadcom BCM94360 CS2 AC                                     |
| 显示器 Monitor    | LG 27UL850-W 27" UHD IPS DisplayHDR 400 and USB Type-C (65W) |

### EFI

OpenCore: 0.6.1

macOS version: 10.15.7

机型: iMac19,1

### 注意 Notes

- 建议使用【黑果小兵】macOS Catalina 10.15.6 安装镜像进行安装

- 如果你的显示器不是 4K 请修改 EFI/OC/config.plist 里的 3840×2160

  - \<key>Resolution\</key>
  - \<string>3840×2160\</string>

- 只支持 AMD 显卡

- 如果你的显卡非 RX 5xxx 系列 请删除：

  - EFI/OC/config.plist 里的：

  ```xml
  agdpmod=pikera
  ```

  - EFI/OC/config.plist 里的 key: DeviceProperties 里的 key: Add 里的:

  ```xml
  <key>PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)</key><dict>...</dict>
  ```

- 记得替换本配置里的 EFI 三码（除非你不需要使用 iCloud 服务）

| key                          | string                               |
| ---------------------------- | ------------------------------------ |
| MLB（主板序列号）            | C02C60KDJWDW                         |
| SystemSerialNumber（序列号） | C02005102CDKGQGUE                    |
| SystemUUID                   | 360CE007-D8AF-4A1B-AB7F-21199251C74C |

### 生成随机三码

- 用任意文本编辑器打开硬盘 EFI 分区下的 /EFI/OC/config.plist，找到 PlatformInfo 配置部分。
- 打开 Hackintool，选择“系统”页，“序列号生成器”，点击右下角刷新按钮，执行摇号。
- "序列号生成器"中的 前三项即为三码，按着图示的对应关系，拷贝到文本编辑器中的 config.plist。

```xml
<key>PlatformInfo</key>
<dict>
  <key>Automatic</key>
  <true/>
  <key>Generic</key>
  <dict>
    <key>AdviseWindows</key>
    <false/>
    <key>MLB</key>
    <string>C02C60KDJWDW</string>
    <key>ROM</key>
    <data>2AvSYZR/</data>
    <key>SpoofVendor</key>
    <true/>
    <key>SystemProductName</key>
    <string>iMac19,1</string>
    <key>SystemSerialNumber</key>
    <string>C02005102CDKGQGUE</string>
    <key>SystemUUID</key>
    <string>360CE007-D8AF-4A1B-AB7F-21199251C74C</string>
  </dict>
  <key>UpdateDataHub</key>
  <true/>
  <key>UpdateNVRAM</key>
  <true/>
  <key>UpdateSMBIOS</key>
  <true/>
  <key>UpdateSMBIOSMode</key>
  <string>Create</string>
</dict>
```

<img src='https://cdn.jsdelivr.net/gh/xiaojun996/CDN/images/screenshot/macos-hackintool.png'/>

### 功能测试

- ☑️ 随航 Sidecar
- ☑️ 接力 Handoff
- ☑️ iMessage/FaceTime
- ☑️ 隔空投送 AirDrop
- ☑️ 睡眠/唤醒 Sleep
- ☑️ 所有 USB 端口
- ☑️ 核显硬件加速
- ☑️ 板载声卡
- ☑️ 板载网卡

### 板载网卡设置

> 系统偏好设置 -> 网络 -> 以太网（高级） -> 硬件 -> 配置:手动, 速度:100baseTX, 双工:全双工, MTU:标准 1500

### 系统信息

<img src='https://cdn.jsdelivr.net/gh/xiaojun996/CDN/images/screenshot/macos-20201002-122148.png'/>

<img src='https://cdn.jsdelivr.net/gh/xiaojun996/CDN/images/screenshot/macos-20201002-122238.png'/>

<img src='https://cdn.jsdelivr.net/gh/xiaojun996/CDN/images/screenshot/macos-20201002-122318.png'/>

<img src='https://cdn.jsdelivr.net/gh/xiaojun996/CDN/images/screenshot/macos-20201002-122358.png'/>

<img src='https://cdn.jsdelivr.net/gh/xiaojun996/CDN/images/screenshot/macos-20201002-122428.png'/>

<img src='https://cdn.jsdelivr.net/gh/xiaojun996/CDN/images/screenshot/macos-20201002-122748.png'/>

<img src='https://cdn.jsdelivr.net/gh/xiaojun996/CDN/images/screenshot/macos-info.png'/>

### 双系统设置

- 双系统需 2 块硬盘

  - 一个装 macOS，一个装 Win10

- Win+Mac 双系统解决 Win 系统时间时差问题

  - 在 Windows 下运行

  - Windows+R Admin 管理员权限运行 cmd，输入下面命令改写注册表

```cmd
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
```

- OpenCore Default launch item 默认启动项

  - 在 OpenCore 启动项选择页面，选择你想选择的默认启动系统，按 Ctrl + Enter
