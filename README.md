## 特别感谢
- **[xiaoleGun](https://github.com/xiaoleGun)**
- **[峨眉山市雅铭网络工作室](https://github.com/wy414012)**

## 设备硬件参数
- **主板: 貌似是华南X79的寨板 (Q67魔改芯片组)**
- **CPU: E5-2690 v2**
- **GPU: 华硕580_2048SP (570VBIOS)**
- **声卡: ALC897 (layout-id:12)**
- **网卡: RealtekRT8111**
- **硬盘: 不知道**
- **其他: 不知道，想起来了再写**

## 目前已知问题
- **1.休眠后睡死，且使用此EFI启动的Windows也会睡死，建议针对所有使用此EFI启动的系统请关闭自动睡眠。睡死后的解决方案：拔电10秒后重新插电启动**
- **2.使用此EFI启动的Windows系统无法睿频，鱼和熊掌目前都兼得不了**
- **3.EFI也支持引导Linux系统启动(Ubuntu可以别的发行版不知道)，如果也用来引导Linux系统估计也会有上述问题**

## EFI基本信息
- **当前OpenCore版本为1.0.4（25.5.30更新）**
- **如有侵权请联系邮箱：xcdh119@qq.com**
- **此EFI适用于H61/Q63/65/67等魔改的芯片组，使用前请仔细阅读需要的注意事项**
- **debug状态：启动参数无硬件加速、有日志输出，`-amd_no_dgpu_accel`禁用硬件加速，`-v`日志输出（跑码）**
- **IvyBridge-EP平台不支持AVX2.0，但Apple在macOS 13 Ventura以及往上版本删除了对没有AVX2.0指令集芯片的支持，所以启动参数`-crypt_force_avx`以及NoAVXFSCompressionTypeZlib-AVXpel已默认启用**
- **对应机型：MacPro2019（标识：MacPro7,1，对应board-id：Mac-27AD2F918AE68F61），建议就用这个不要改就行了，使用iMacPro1,1会出现USB无效的问题，估计是需要定制USB吧，反正我没搞明白。**
- **当前EFI适配的最低版本为？？？，最高版本为macOS 15.5（或者更高）**
- **如果要使用macOS 12以及更低版本的系统，建议使用MacPro6,1，macOS 13以及更高版本就只建议尝鲜玩玩了，新的macOS中Apple也在对旧驱动进行删减，比如老旧的AMD显卡驱动**
- **硬件详细信息请参考[B站视频](https://www.bilibili.com/video/BV1e1421d7wa/)中的简介**

## ！！！注意
- **本人不是专门折腾黑苹果的，如有错误请谅解并多多指教**
- **（25.5.30更新，祝大家端午节安康）上传了一张关于本机截图：![微信图片_20250530165914_233](https://github.com/user-attachments/assets/84962e05-0844-44ad-ab03-739f8e31a4b4)**
- **（25.5.30更新）自25.5.30版本起，使用EFI请自行生成序列号等信息：![wechat_2025-05-30_170153_560](https://github.com/user-attachments/assets/84737db1-4b7e-4d97-b497-e594e99886cc)**
- **为正常使用iCloud、iMessage、FaceTime，在24.5.5版本的EFI中已添加EN0网卡，使用军刀工具查看电脑EN0网卡：![image](https://github.com/2970894475/OpenCore_HUANANZHI-X79-Q67_2690V2_RX570/assets/61039538/d19b5c61-c087-4da5-b361-123972c45567)
对应的PCIe地址是![image](https://github.com/2970894475/OpenCore_HUANANZHI-X79-Q67_2690V2_RX570/assets/61039538/4b11616e-d836-4f78-b02a-868ae6d794ca)，使用OCC工具添加并设置好后![image](https://github.com/2970894475/OpenCore_HUANANZHI-X79-Q67_2690V2_RX570/assets/61039538/f2a6b0bb-897c-41d4-a0f6-a73da55764ee)再设置机型平台设置中的ROM![image](https://github.com/2970894475/OpenCore_HUANANZHI-X79-Q67_2690V2_RX570/assets/61039538/e16e5f5e-ea42-410e-9f49-9caebde338f0)点击来自系统，点击Mac，点击生成，保存关闭重启电脑，清除NVRAM，开机后再次登陆Apple ID即可**
- **「芯片组为H61/Q63/65/67等魔改芯片组x79主板请注意」如果系统是macOS12以及往后版本，CPU有10核心可以直接用此EFI，但是CPU有10核心的情况下，用此EFI仍然出现多核心内核恐慌问题，请关闭几个核心后（建议变成8或6核心都行）再参考下面这条自己尝试修复。如果只打算用macOS11且并不升级可以忽略**
- **「如果只打算用macOS11且不升级可以忽略」多核心恐慌参考，我的EFI中的DSDT文件不清楚能不能通用，修复恐慌的已默认启用；10核在启用情况下仍然出现恐慌或10核以上的请参考[点击跳转参考贴尾部的故障排除及解决方案](https://www.hackintosh-forum.de/forum/thread/55510-install-monterey-big-sur-on-any-x79-motherboard-huananzhi-chinese-gigabyte-etc-a/)，自己修复后再尝试打开所有核心**
- **1.显卡免驱问题导致需要关闭硬件加速（macOSVentura及其往上版本，显卡输出黑屏或无信号）、2.变频问题修复参考、3.TSC同步核心驱动来源：[huaNan_x79_e5_2670_v1_c2](https://github.com/wy414012/huaNan_x79_e5_2670_v1_c2)**
- **变频修复两种方案：1.使用上面这个（请启用SSDT-CPUM并关闭CPUFriend两个驱动，不是2690v2的用方法2）；2.使用CPUFriend驱动，禁用SSDT-CPUM，仿冒机型是使用MacPro7,1（对应board-id：Mac-27AD2F918AE68F61）机型的无需再生成**
- **DP参数中有本人显示器EDID（AAPL00,override-no-connect）和显卡VBIOS的风扇调用数据（PP_PhmSoftPowerPlayTable），如不可用请删除**
- **EFI已默认修复M.2固态硬盘识别为外置移动存储的问题，如果没有此问题请禁用或删除SSDT-NVMe**
- **EFI中的SSDT-RX580文件仅仅是对显卡进行性能优化，并无其他特定问题要修复，不是对应显卡的建议禁用或删除**

## 相关开源
- **[OpenCore](https://github.com/acidanthera/OpenCorePkg)**
- **[OpenCore-Legacy-Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher)**
- **[CpuTscSync](https://github.com/wy414012/CpuTscSync)**
