# 来源与贡献归属

| 项目 / 作者 | 本包中的作用 | 链接 |
| --- | --- | --- |
| HuajiFruit / AirportBZ 贡献者 | 直接驱动来源，BE200/BE201 相关实现与固件集成 | https://github.com/HuajiFruit/AirportBZ |
| OpenIntelWireless / itlwm 贡献者 | Intel 无线驱动基础及 AirportItlwm 体系 | https://github.com/OpenIntelWireless/itlwm |
| laobamac / itlwm 贡献者 | WCL 原生 Wi-Fi 前端 | https://github.com/laobamac/itlwm |
| OpenBSD 贡献者 | 上游代码中沿用的网络栈及驱动基础 | https://www.openbsd.org/ |
| Linux iwlwifi 贡献者 | 上游移植参考及硬件/固件接口来源 | https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/drivers/net/wireless/intel/iwlwifi |
| Intel | 随包无线固件和 PNVM 二进制，按单独许可再分发 | 本包 LICENCE.bz-firmware |
| acidanthera / MacKernelSDK 贡献者 | 外部构建依赖 | https://github.com/acidanthera/MacKernelSDK |
| JiangDan666 | 本机编译、环境兼容整理、安装/回退工具及实测分享 | https://github.com/JiangDan666/BE200-Sequoia-Share |

驱动固定来源提交：`0ccab1627764406861fb9eb0a06ca36e31b4440f`。
SDK 固定提交：`3f750085caa17ec3a7880f11c11bf4f48cd6a164`，构建前应用上游附带的 `IOPCIDevice-msix.patch`。

本次未修改上游驱动功能；原源码、文件版权、许可证和上游 README 保留。生成的固件包装文件与 macOS 编译/装包脚本用于重现本包构建。上游参考关系不代表每个上游项目均对本分享包进行了验证或背书。

驱动源码：随附 GPLv2 LICENSE；各文件附带的其他许可和版权声明继续适用。新增安装/配置工具：GPL-2.0-only。Intel 固件和 PNVM：仅按随附 LICENCE.bz-firmware 条款分发，不应称为开源固件。本文件不替代任何原始许可。
