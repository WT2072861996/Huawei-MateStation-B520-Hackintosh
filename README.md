# 🖥️ 华为 MateStation B520 · OpenCore Hackintosh

**Intel Core i7-10700 · UHD Graphics 630 · Comet Lake-S · B560 · macOS Sequoia 15 · OpenCore 1.0.x**

<div align="center">

![CPU](https://img.shields.io/badge/CPU-i7_10700_Comet_Lake-0071C5?style=flat-square)
![GPU](https://img.shields.io/badge/GPU-UHD_630-0071C5?style=flat-square)
![RAM](https://img.shields.io/badge/RAM-16_GB_DDR4-8B5CF6?style=flat-square)
![OpenCore](https://img.shields.io/badge/OpenCore-1.0.x-9cf?style=flat-square)
![Chipset](https://img.shields.io/badge/Chipset-B560-00A3E0?style=flat-square)
![macOS](https://img.shields.io/badge/macOS-Sequoia_15-0071BC?style=flat-square)
![Status](https://img.shields.io/badge/Status-Working-brightgreen?style=flat-square)

**[🖥️ 硬件配置](#-硬件配置) · [⚙️ BIOS 设置](#%EF%B8%8F-bios-设置) · [✅ 驱动状态](#-驱动状态) · [📦 EFI 配置](#-efi-配置) · [🚀 快速开始](#-快速开始)**

</div>

---

## 🖥️ 硬件配置

| 组件 | 型号 | 规格 | 驱动情况 |
|:-----|:-----|:-----|:--------:|
| **型号** | 华为 MateStation B520 | PUBZ-WXXXX-PCB | ✅ |
| **主板** | HUAWEI PUBZ-WXXXX-PCB | B560 (Comet Lake-S) | ✅ |
| **CPU** | Intel Core i7-10700 | 8C/16T @ 2.90-4.80 GHz | ✅ 睿频正常 |
| **核显** | Intel UHD Graphics 630 | Comet Lake (8086-9BC5) | ✅ 硬件加速 |
| **内存** | DDR4 SO-DIMM | 16 GB | ✅ |
| **系统盘** | YMTC PC005 | 512 GB NVMe SSD | ✅ |
| **数据盘** | WD WD20EARZ | 2 TB HDD | ✅ |
| **声卡** | Senary Audio | HDA: 14F1-5098 | ⚠️ 需 AppleALC |
| **有线网卡** | Realtek RTL8168 | 10EC-8168 | ✅ |
| **Wi-Fi** | Intel Wi-Fi 6 AX201 | 8086-43F0 | ⚠️ 需 AirportItlwm |
| **蓝牙** | Intel CNVi | 集成于 AX201 | ⚠️ 需 IntelBluetoothFirmware |

---

## ✅ 驱动状态

| 功能 | 状态 | 功能 | 状态 |
|:-----|:---:|:-----|:---:|
| **UHD 630 核显** | ✅ 硬件加速 | **Metal** | ✅ |
| **Realtek RTL8168 有线网卡** | ✅ | **USB 2.0/3.0/3.2** | ✅ |
| **NVMe SSD** | ✅ | **SATA HDD** | ✅ |
| **CPU 睿频** | ✅ | **XCPM 电源管理** | ✅ |
| **HDMI 1920×1080** | ✅ | **睡眠/唤醒** | ✅ |
| **NVRAM** | ✅ | **DVMT/核显** | ✅ |
| **Wi-Fi (Intel AX201)** | ⚠️ | **蓝牙 (Intel)** | ⚠️ |
| **声卡 (Senary Audio)** | ⚠️ | | |

> **注意**：AMD RX 6750 GRE (Navi 22) 在 macOS Sequoia 中原生支持，无需任何补丁即可获得完整硬件加速和 Metal 3 支持。

---

## ⚙️ BIOS 设置

| 设置 | 值 | 说明 |
|:-----|:---:|:-----|
| **Secure Boot** | Disabled | macOS 不支持 |
| **Fast Boot** | Disabled | 避免启动问题 |
| **VT-x** | Enabled | 虚拟机支持 |
| **VT-d** | Disabled | 或添加 `dart=0` |
| **UEFI Boot** | Enabled | |
| **Above 4G Decoding** | Enabled | Resizable BAR 支持 |

> 进入华为 MateStation B520 BIOS 方法：开机按 F2 或 Del

---

## 📦 EFI 配置

### Kexts 清单

```
EFI/OC/Kexts/
├── Lilu.kext                   ✅ 内核补丁框架
├── VirtualSMC.kext             ✅ SMC 模拟
├── AppleALC.kext               ✅ 声卡驱动
├── RealtekRTL8111.kext         ✅ 有线网卡驱动
├── AirportItlwm.kext           ✅ Intel AX201 Wi-Fi
├── IntelBluetoothFirmware.kext ✅ Intel 蓝牙
├── IntelBTPatcher.kext         ✅ 蓝牙补丁
├── BlueToolFixup.kext          ✅ 蓝牙修复
├── USBPorts.kext               ✅ USB 定制映射
├── SMCProcessor.kext           ✅ CPU 传感器
├── SMCSuperIO.kext             ✅ 风扇/温度
└── RestrictEvents.kext         ✅ 事件限制
```

### SSDT 热补丁

```
EFI/OC/ACPI/
├── SSDT-PLUG.aml       ✅ CPU 电源管理 (XCPM)
├── SSDT-EC.aml         ✅ EC 仿冒 (Comet Lake 必需)
├── SSDT-USBX.aml       ✅ USB 电源属性
├── SSDT-SBUS.aml       ✅ SMBus 支持
├── SSDT-MCHC.aml       ✅ MCHC 仿冒
├── SSDT-HPET.aml       ✅ HPET IRQ 修复
├── SSDT-RTC0.aml       ✅ RTC 兼容性
└── SSDT-DMAC.aml       ✅ DMA 控制器修复
```

---

## 🚀 快速开始

### 1️⃣ BIOS 配置

1. 开机按 F2 进入 BIOS
2. **Secure Boot** → Disabled
3. **Fast Boot** → Disabled
4. 保存退出

### 2️⃣ EFI 部署

```bash
# 挂载 USB 的 EFI 分区
diskutil list
sudo diskutil mount diskXs1

# 复制 EFI 文件夹
cp -R EFI /Volumes/EFI/
```

### 3️⃣ 生成三码（重要！）

使用 GenSMBIOS 或 OCAT 生成自己的 SMBIOS 序列号，不要直接使用本仓库的三码。

### 4️⃣ 安装 macOS Sequoia 15

1. 制作 macOS Sequoia 安装 U 盘
2. 替换 U 盘 EFI 分区中的 EFI 文件夹
3. 从 USB 启动 → 选择「Install macOS」
4. 按提示完成安装（约 2-3 次重启）
5. 安装完成后将 EFI 复制到硬盘 EFI 分区

---

## 🔧 注意事项

- **华为 MateStation B520** 是华为品牌台式机，B560 芯片组 + Comet Lake-S CPU
- **Intel UHD Graphics 630** 核显通过 WhateverGreen 驱动，完整支持硬件加速
- 注意核显显存预分配 DVMT 需在 BIOS 中设置为 64MB 或以上
- Senary Audio (14F1-5098) 是国产音频芯片，AppleALC 可能需要尝试多个 layout-id
- Intel AX201 Wi-Fi 使用 **AirportItlwm**（需对应 Sequoia 版本的构建）
- 板载 YMTC PC005 NVMe 固态硬盘兼容性良好
- ⚠️ **自行生成三码后再使用，不要直接使用本仓库的序列号**

---

## 📄 许可证

MIT License — 仅供学习和研究

> ⚠️ 在非 Apple 硬件上安装 macOS 可能违反 EULA

---

<p align="center">
  <b>为 Hackintosh 社区贡献 ❤️</b><br/>
  <sub>华为 MateStation B520 · OpenCore 1.0.x · macOS Sequoia 15</sub>
</p>
