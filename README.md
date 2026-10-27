# BE200 Sequoia Share · 实验分享版

Intel BE200 在 macOS Sequoia 上使用原生 Wi-Fi 界面的实测分享包，包含预编译 kext、对应源码、安装/回退工具及测试记录。

**驱动来自 [HuajiFruit/AirportBZ](https://github.com/HuajiFruit/AirportBZ)，本仓库没有修改上游驱动功能。** 这里整理的是固定版本源码的 macOS 本机编译、安装工具和单机实测，不能视为独立开发的新驱动或长期稳定版。此前的 BE200 固件诊断移植项目不属于本包。

> **免责声明：本项目仅在作者本人设备上测试可用，属于个人实验性分享，不保证适用于其他设备。使用前请备份 EFI 并准备恢复方式；因安装或修改导致的无法启动、数据丢失等风险，由使用者自行承担。**

## 下载与安装

优先从 [Releases](https://github.com/JiangDan666/BE200-Sequoia-Share/releases) 下载完整分享 ZIP，解压后阅读 [先读我-安装与回退.md](先读我-安装与回退.md)，再双击 `安装驱动.command`。完整 ZIP 保留脚本执行权限；请勿只取一个 kext 而忽略系统无线组件的兼容条件。

当前分发包为 [`BE200-Sequoia-Share.zip`](https://github.com/JiangDan666/BE200-Sequoia-Share/releases/download/v0.1.0-sequoia-experimental/BE200-Sequoia-Share.zip)，整包 SHA-256：`e37ac3a353d905c21959f9ebc3560198d7b1d49a2de1c55b5baec45b14b2a60f`。**对应源码、固件、构建脚本和安装工具均包含在这个 ZIP 内**，解压后可查看 `Source/AirportBZ` 与 `scripts`。网页根目录中的说明供在线阅读，安装和重新构建请使用解压后的完整目录。

安装器会要求确认实际启动 OpenCore 的 ESP，先备份并校验完整 EFI，再修改无线加载项。备份带回退脚本，不会自动重启。预编译版安装不需要 Python 或 Xcode。通用安装器通过离线检查，尚未在第二台机器完成安装及回退全流程测试。

## 兼容范围

| 项目 | 范围 |
| --- | --- |
| 平台 | Intel x86_64，macOS Sequoia 15.2–15.x，Darwin 24.2.0–24.99.99 |
| 本机实测 | ThinkBook 16p，macOS 15.7.8（24G824），BE200 `8086:272B`，GL C0 / FM C0 |
| BE201 | 上游报告支持 `8086:7740`；本包未做 BE201 实机验证 |
| 网络建议 | WPA2-Personal，AES/CCMP，非强制 PMF，2.4/5 GHz |
| 不适用 | Apple Silicon、BE202、AX200/AX210、15.0/15.1、Sonoma 14 及更早、Tahoe 26 |

需要与系统匹配的原生 `IOSkywalkFamily`、`IO80211Family` 和无线用户态框架。**OCLP/OCLP-Mod 的旧无线根补丁会冲突；卸载应用不等于撤销补丁。** 安装器发现根补丁标记会停止，请先核对补丁依赖，不能删标记绕过。不要覆盖别人的整套 EFI。

## 已验证和未验证

本机重启后能打开原生 Wi-Fi、扫描、连接并实际联网。约 8 分钟记录中，网关 480/480、Apple HTTPS 48/48 成功；一条 22,928,608 字节下载连接完整跨越锁屏/解锁。详见 [实机测试报告](实机测试报告-20261026.md)。另有公网 ICMP 丢包及部分下载源超时，原因未确定，报告保留这些结果。

锁屏测试在接电、不合盖条件下进行，不能代表整机睡眠或合盖不断网。本机平台睡眠另有问题，不能据此认定无线驱动造成，也不能据此验证驱动睡眠唤醒。长期负载、睡眠唤醒、断线重连、漫游和企业认证仍待系统验证。

WPA3/SAE、强制 PMF、6 GHz、320 MHz、MLO、AWDL/AirDrop 不支持；HE/802.11ax 为实验功能，本包默认关闭。**BE200 硬件支持 Wi-Fi 7，不代表此驱动实现 Wi-Fi 7。**

## 源码、构建与致谢

- 直接上游：[HuajiFruit/AirportBZ](https://github.com/HuajiFruit/AirportBZ)，固定提交 [`0ccab1627764406861fb9eb0a06ca36e31b4440f`](https://github.com/HuajiFruit/AirportBZ/tree/0ccab1627764406861fb9eb0a06ca36e31b4440f)。对应源码在 `Source/AirportBZ`。
- 基础项目：[OpenIntelWireless/itlwm](https://github.com/OpenIntelWireless/itlwm)；WCL 前端：[laobamac/itlwm](https://github.com/laobamac/itlwm)。感谢 OpenBSD、Linux iwlwifi 及其他上游贡献者。
- 外部构建 SDK：[acidanthera/MacKernelSDK](https://github.com/acidanthera/MacKernelSDK/tree/3f750085caa17ec3a7880f11c11bf4f48cd6a164)。
- 详细说明：[CREDITS.md](CREDITS.md)、[构建来源与许可证.md](构建来源与许可证.md)。上游原始 README 保持原样，其中 BE200 未实测描述是该提交当时的记录；本包只补充一台机器的后续实测。

驱动源码按随附 [GPLv2 LICENSE](LICENSE) 提供，各文件原有声明保留；新增安装/配置工具为 GPL-2.0-only。**Intel 固件及 PNVM 是单独许可的二进制，不是 GPL 开源固件**，见 [LICENCE.bz-firmware](LICENCE.bz-firmware)。请保留许可及来源，不表示 Intel 或上游作者为本分享包背书。

已测试可执行文件 SHA-256：`aa0d3f6d518570e3069780d5f1678c5287090f09bece5631cd5a803aeb1e7946`。新精简 ZIP 中的 `SHA256SUMS.txt` 保留了精简前的四个说明文件条目；整包校验请以 Release 中的 `BE200-Sequoia-Share.zip.sha256` 为准。重新构建的二进制需要重新实测。

## English overview

Experimental Intel BE200 sharing package for native Wi-Fi on Intel macOS Sequoia 15.2–15.x. This packages an **unmodified functional build of HuajiFruit/AirportBZ** at the pinned commit above, with macOS build scripts, an EFI backup/install/rollback workflow and single-machine test notes. It is not a new independently authored Wi-Fi driver. Native system wireless components are required; legacy OCLP wireless root patches conflict. No general stability, sleep/wake or Wi-Fi 7 support claim is made. Preserve upstream notices and the separate Intel binary firmware license.

提交问题时请提供系统版本、网卡 PCI ID、是否使用根补丁和去隐私后的错误文字。不要上传 Wi-Fi 密码、个人完整 EFI、序列号或未脱敏的整份系统日志。
