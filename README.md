CH634X USB3.0 Type-C 四口 HUB

> 1× Type-C 上行 ｜ 1× Type-C 下行 ｜ 3× USB-A ｜ USB 3.2 Gen1 5Gbps

本项目基于 WCH CH634X 设计，是一款四端口 USB3.0 扩展坞，主要用于学习和验证 USB Type-C 正反插、USB3.0 高速差分信号、端口供电管理以及 ESD 防护 等硬件设计。
![Uploading image.png…]()

✨ 主要功能

    USB Type-C 上行接口
    1× USB Type-C 3.0 下行
    3× USB-A 3.0 下行
    支持 USB 3.2 Gen1 5Gbps
    兼容 USB2.0 480Mbps
    Type-C 上行支持正反插
    四路 USB VBUS 独立供电与过流检测
    USB 高速数据线 ESD 防护

🔧 核心方案

                 USB Type-C
                    上行
                      │
                      ▼
               ┌────────────┐
               │   CH634X   │
               │ USB3 HUB   │
               └─────┬──────┘
                     │
        ┌────────────┼────────────┐
        │            │            │
     USB-A         USB-C        USB-A ×2
        │            │            │
      CH217A       CH217A       CH217A
        │            │            │
     VBUS控制      VBUS控制      VBUS控制

主控采用 CH634X，Type-C 上行利用其内部 P1/P1C 双路 SuperSpeed PHY 实现正反插，无需额外增加 USB3 MUX。

四个下行端口分别使用 CH217A 进行 VBUS 开关及过流检测。
🛡️ ESD 与高速设计

USB2.0 / USB3.0 数据线采用低电容 CH412K 进行 ESD 防护，Type-C CC1/CC2 单独预留低速 ESD 保护。

USB3 TX 差分信号按照参考设计加入 100nF AC 耦合电容。

PCB 高速部分主要关注：

USB3 90Ω 差分阻抗
       ↓
差分对等长
       ↓
连续参考地
       ↓
减少过孔和支线
       ↓
ESD 靠近 USB 接口

⚡ 端口供电

每个 USB 下行口均由 CH217A 独立控制：

+5V
 │
 ▼
CH217A
 │
 ├── PWREN# 电源控制
 ├── FLAG#  过流检测
 │
 ▼
USB VBUS
 │
100uF + 100nF
 │
GND

这种设计可以提高 USB 设备热插拔时的供电稳定性，同时避免单个端口过流影响其他接口。
🧪 当前调试状态

目前实物已经完成焊接，并成功在 Linux 下识别：

1a86:80a0  QinHeng Electronics USB2.0 HUB
1a86:80a1  QinHeng Electronics USB3.0 HUB

说明 USB2.0 与 USB3.0 HUB 均已成功工作。

image.png
下行四个接口测速如下：（测试设备使用支持USB3.0的U盘）
外壳设计

image.png
📖 项目说明

本项目主要用于个人学习与硬件验证，涉及：

USB Type-C、USB3.0 5Gbps 高速设计、USB HUB、ESD 防护以及 USB VBUS 电源管理。

当前版本仍属于验证版本，后续会根据实物测试结果继续优化。

> 欢迎交流 CH634X、USB3.0、Type-C 以及高速 PCB 设计相关经验。
