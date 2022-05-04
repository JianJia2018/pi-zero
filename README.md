# Actions-OpenWrt

[![LICENSE](https://img.shields.io/github/license/mashape/apistatus.svg?style=flat-square&label=LICENSE)](https://github.com/P3TERX/Actions-OpenWrt/blob/master/LICENSE)
![GitHub Stars](https://img.shields.io/github/stars/P3TERX/Actions-OpenWrt.svg?style=flat-square&label=Stars&logo=github)
![GitHub Forks](https://img.shields.io/github/forks/P3TERX/Actions-OpenWrt.svg?style=flat-square&label=Forks&logo=github)

Build OpenWrt using GitHub Actions

[中文教程](https://p3terx.com/archives/build-openwrt-with-github-actions.html)

## 流程
- 进入menuconfig命令：cd openwrt && make menuconfig
- 配置完成后按快捷键Ctrl+D或执行exit命令退出，后续编译工作将自动进行。
- 新手参考[OpenWrt MenuConfig设置和LuCI插件选项说明](https://mtom.ml/827.html)
- [OpenWrt 编译 LuCI -> Applications 添加插件应用说明-L大【2021.3.15】](https://www.right.com.cn/forum/thread-344825-1-1.html)
- [云编译openwrt经验总结](https://www.right.com.cn/forum/thread-344825-1-1.html)

## 软件包源
- [liuran001-openwrt-packages](https://github.com/liuran001/openwrt-packages)
- [kenzok8-openwrt-packages](https://github.com/kenzok8/openwrt-packages)

## 必要插件
- Base system/blockd
- Administration/netdata(实时监控, 和Applications中二选一)
- Kernel modules(内核模块)/kmod-ata-core（串行ATA总线支持，即SATA硬盘支持)
- Kernel modules(内核模块)/kmod-block2mtd
- Kernel modules(内核模块)/kmod-scsi-generic（usb转IDE,SATA)
- Filesystems（文件系统支持)/kmod-fs-cifs（选择该项可能要在编译过程中手动按Y）
- Filesystems（文件系统支持)/kmod-fs-nfs
- Filesystems（文件系统支持)/kmod-fs-nfs-common
- Kernel modules —> Filesystems —> <*> kmod-fs-ext4 (移动硬盘EXT4格式选择)
- Kernel modules —> Filesystems —> <*> kmod-fs-vfat(FAT16 / FAT32 格式 选择)
- Kernel modules —> Filesystems —> <*> kmod-fs-ntfs (NTFS 格式 选择)
- Base system —> <*>block-mount  
- Utilities —> Filesystem —> <*> badblocks   -  添加自动挂载工具
- Utilities ---> disc ---> <*> fdisk... manipulate disk partition table
- Utilities ---> <*> usbutils. USB devices listing utilities
- Native Language Support（语言编码支持）/kmod-nls-cp936 (中文字符支持)
- Kernel modules —> Native Language Support —> <*> kmod-nls-cp437
- Kernel modules —> Native Language Support —> <*> kmod-nls-iso8859-1
- Kernel modules —> Native Language Support —> <*> kmod-nls-utf8
- USB Support（USB设备支持)/
  - kmod-usb-ohci	
  - kmod-usb-printer	
  - kmod-usb-storage	
  - kmod-usb-storage-extras	
  - kmod-usb-storage-uas	
  - kmod-usb-uhci(usb1.1驱动)	
  - kmod-usb2	
  - kmod-usb3
- Network/iperf3（网络速度测试工具)
- samba4-server/NetBiOS support (在网络里显示共享文件)
- Utilities（实用工具）/Filesystem/	ntfs-3g（ntfs文件系统）
- Utilities（实用工具)/lm-sensors（硬件监控）
- Utilities（实用工具)/lm-sensors-detect（硬件传感器查找）
- LuCI/Applications
  - luci-app-adbyby-plus 广告屏蔽大师Plus +
  - luci-app-autoreboot  #支持计划重启
  - luci-app-filetransfer  #文件传输（可web安装ipk包）
  - luci-app-nlbwmon   #网络带宽监视器
  - luci-app-frpc   #内网穿透 Frp
  - luci-app-flowoffload  #Turbo ACC网络加速（集成FLOW,BBR,NAT,DNS...
  - LuCI ---> Applications ---> luci-app-违禁软件-plus   #违禁软件打倒美帝Plus+
    luci-app-违禁软件-plus ---> Include 违禁软件  #SS代理
    luci-app-违禁软件-plus ---> Include 违禁软件 Rust (AEAD ciphers only)  #违禁软件UST代理(AEAD加密)
    luci-app-违禁软件-plus ---> Include Xray (违禁软件/Trojan-GO implemented)  #Xray代理
    luci-app-违禁软件-plus ---> Include 违禁软件R Server  #违禁软件服务器
  - luci-app-unblockmusic  #解锁网易云灰色歌曲3合1新版本
  - LuCI ---> Applications ---> luci-app-diskman   #磁盘管理工具
    luci-app-diskman ---> Include btrfs-progs   #新型的写时复制 (COW)
    luci-app-diskman ---> Include lsblk   #lsblk命令 用于列出所有可用块设备的信息
    luci-app-diskman ---> Include mdadm   #mdadm命令 用于创建、管理、监控RAID设备的工具
  - luci-app-qbittorrent #BT下载工具（qBittorrent）
  - luci-app-wol   #WOL网络唤醒
  - luci-app-zerotier  #ZeroTier内网穿透
  - luci-app-aria2 # Aria2下载工具
  - luci-app-commands   #Shell命令模块
  - luci-app-docker  #Docker容器(dockerman更名为docker)
  - luci-app-hd-idle  #硬盘休眠
  - luci-app-jd-dailybonus  #京东签到服务
  - luci-app-netdata  #Netdata实时监控（图形化）
  - luci-app-samba4   #网络共享（Samba4）
  - luci-app-uugamebooster  #UU网游加速器
  - luci-app-watchcat  #断网检测功能与定时重启
  - luci-app-wol   #WOL网络唤醒
  - luci-app-advancedsetting -系统高级设置
  - luci-app-serverchan -Server酱 微信/Telegram 推送的插件
  - luci-app-dnsfilter -基于DNS的广告过滤
  - luci-app-smartdns -smartdns防污染
  - luci-app-ttyd   #网页终端命令行

### 支持 iPv6：
1、Extra packages ---> ipv6helper （选定这个后下面几项自动选择了）
Network ---> odhcp6c
Network ---> odhcpd-ipv6only
LuCI ---> Protocols ---> luci-proto-ipv6
LuCI ---> Protocols ---> luci-proto-ppp

## Acknowledgments

- [Microsoft Azure](https://azure.microsoft.com)
- [GitHub Actions](https://github.com/features/actions)
- [OpenWrt](https://github.com/openwrt/openwrt)
- [Lean's OpenWrt](https://github.com/coolsnowwolf/lede)
- [tmate](https://github.com/tmate-io/tmate)
- [mxschmitt/action-tmate](https://github.com/mxschmitt/action-tmate)
- [csexton/debugger-action](https://github.com/csexton/debugger-action)
- [Cowtransfer](https://cowtransfer.com)
- [WeTransfer](https://wetransfer.com/)
- [Mikubill/transfer](https://github.com/Mikubill/transfer)
- [softprops/action-gh-release](https://github.com/softprops/action-gh-release)
- [ActionsRML/delete-workflow-runs](https://github.com/ActionsRML/delete-workflow-runs)
- [dev-drprasad/delete-older-releases](https://github.com/dev-drprasad/delete-older-releases)
- [peter-evans/repository-dispatch](https://github.com/peter-evans/repository-dispatch)

## License

[MIT](https://github.com/P3TERX/Actions-OpenWrt/blob/main/LICENSE) © P3TERX
