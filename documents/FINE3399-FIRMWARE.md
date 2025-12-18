# Fine3399 OpenWrt 固件说明文档

## 📋 目录

- [设备信息](#设备信息)
- [固件能力对比](#固件能力对比)
- [固件特性](#固件特性)
- [LuCI 应用列表](#luci-应用列表)
- [系统功能](#系统功能)
- [网络功能](#网络功能)
- [使用说明](#使用说明)
- [常见问题](#常见问题)

---

## 🖥️ 设备信息

### 硬件规格

| 项目 | 规格 |
|------|------|
| **设备型号** | Fine3399 |
| **处理器** | Rockchip RK3399 (六核 ARM64) |
| **CPU架构** | 2×Cortex-A72 + 4×Cortex-A53 |
| **内存** | 4GB DDR3/DDR4 RAM |
| **存储** | 64GB eMMC Flash |
| **网络接口** | 双千兆以太网口 |
| **USB接口** | USB 2.0 + USB 3.0 |
| **扩展接口** | M.2 PCIe 插槽 |
| **设备树** | rk3399-fine3399.dtb |

### 固件版本

本固件基于以下开源项目构建，提供三个版本供选择：

| 固件版本 | 上游源码 | 特点 | 内核版本 | 应用数量 |
|---------|---------|------|----------|----------|
| **OpenWrt Main** | [OpenWrt Official](https://github.com/openwrt/openwrt) | 官方最新版本，稳定性高 | 6.1.y, 6.12.y | ~25个 |
| **ImmortalWrt Master** | [ImmortalWrt](https://github.com/immortalwrt/immortalwrt) | 中文优化，插件丰富 | 6.1.y, 6.12.y | ~23个 |
| **LEDE Master** | [Lean's LEDE](https://github.com/coolsnowwolf/lede) | 国内流行版本，性能优化 | 6.1.y, 6.12.y | ~31个 |

> **内核说明**：所有版本均支持 RK3399 专用的 rk35xx 内核 (6.1.y) 和通用的 stable 内核 (6.1.y, 6.12.y)

---

## 📊 固件能力对比

以下表格详细列举了本固件在不同源码分支中的功能支持情况：

### 核心系统功能对比

| 功能/应用 | OpenWrt Main | ImmortalWrt Master | LEDE Master | 说明 |
|----------|--------------|-------------------|-------------|------|
| **基础系统** | | | | |
| LuCI Web界面 | ✅ | ✅ | ✅ | 全中文界面 |
| 防火墙 (Firewall) | ✅ | ✅ | ✅ | 基于 nftables |
| 软件包管理 (opkg) | ✅ | ✅ | ✅ | 在线安装软件包 |
| Web终端 (ttyd) | ✅ | ✅ | ✅ | 浏览器SSH终端 |
| CPU频率管理 | ✅ | ✅ | ✅ | 性能/省电模式切换 |
| 系统统计 | ✅ | ✅ | ✅ | CPU/内存/网络监控 |
| Argon主题配置 | ✅ | ✅ | ✅ | 自定义主题外观 |
| **设备管理** | | | | |
| Amlogic设备管理 | ✅ | ❌ | ✅ | 固件升级/安装到eMMC |
| 磁盘管理 (diskman) | ❌ | ❌ | ✅ | 磁盘分区/格式化 |
| 系统升级助手 | ✅ | ❌ | ❌ | 在线升级系统 |

### 网络功能对比

| 功能/应用 | OpenWrt Main | ImmortalWrt Master | LEDE Master | 说明 |
|----------|--------------|-------------------|-------------|------|
| **网络服务** | | | | |
| 动态DNS (DDNS) | ✅ | ✅ | ✅ | 支持多个提供商 |
| 网络加速 (TurboACC) | ✅ | ✅ | ✅ | BBR/流量卸载 |
| UPnP | ✅ | ❌ | ✅ | 自动端口映射 |
| 网络唤醒 (WoL) | ❌ | ❌ | ✅ | 远程唤醒设备 |
| IP/MAC绑定 | ❌ | ❌ | ✅ | ARP绑定 |
| 访问控制 | ✅ | ✅ | ✅ | 上网时间管控 |
| IP限速 (nft-qos) | ✅ | ✅ | ✅ | 基于IP的QoS |
| 网速测试 | ✅ | ✅ | ✅ | SpeedTest测速 |
| **VPN服务** | | | | |
| OpenVPN | ✅ | ✅ | ✅ | 经典VPN协议 |
| WireGuard | ✅ | ✅ | ✅ | 现代高性能VPN |
| OpenConnect (ocserv) | ✅ | ✅ | ✅ | Cisco AnyConnect |
| IPSec VPN | ✅ | ✅ | ✅ | 企业级VPN |
| **代理服务** | | | | |
| PassWall | ✅ | ✅ | ✅ | 多协议代理 |
| OpenClash | ✅ | ✅ | ✅ | Clash代理客户端 |

### 文件与存储功能对比

| 功能/应用 | OpenWrt Main | ImmortalWrt Master | LEDE Master | 说明 |
|----------|--------------|-------------------|-------------|------|
| FileBrowser | ✅ | ✅ | ✅ | Web文件管理器 |
| 文件传输 | ❌ | ❌ | ✅ | LEDE专属文件传输 |
| 网络共享 (KSMBd) | ✅ | ✅ | ✅ | 内核级Samba服务 |
| Samba4 | ✅ | ❌ | ❌ | 用户态Samba (OpenWrt) |
| 内网穿透 - 客户端 (frpc) | ✅ | ❌ | ✅ | FRP客户端 |
| 内网穿透 - 服务端 (frps) | ✅ | ❌ | ✅ | FRP服务端 |

### 容器与应用服务对比

| 功能/应用 | OpenWrt Main | ImmortalWrt Master | LEDE Master | 说明 |
|----------|--------------|-------------------|-------------|------|
| Docker管理器 | ✅ | ✅ | ✅ | 图形化管理Docker |
| Docker引擎 | ✅ | ✅ | ✅ | 完整Docker支持 |
| Docker Compose | ✅ | ✅ | ✅ | 容器编排 |
| AdGuard Home | ✅ | ✅ | ✅ | DNS级广告拦截 |
| KMS服务器 | ✅ | ✅ | ✅ | Windows激活 |
| 微信通知 (ServerChan) | ✅ | ✅ | ✅ | 系统事件推送 |

### 底层支持对比

| 功能特性 | OpenWrt Main | ImmortalWrt Master | LEDE Master | 说明 |
|---------|--------------|-------------------|-------------|------|
| **内核版本** | | | | |
| Stable内核 6.1.y | ✅ | ✅ | ✅ | 长期支持版本 |
| Stable内核 6.12.y | ✅ | ✅ | ✅ | 最新稳定版 |
| RK35xx专用内核 | ✅ | ✅ | ✅ | RK3399优化内核 |
| **硬件支持** | | | | |
| RK3399硬件加密 | ✅ | ✅ | ✅ | crypto-hw-rockchip |
| RK3399温度监控 | ✅ | ✅ | ✅ | hwmon-rockchip-thermal |
| 双千兆网卡 | ✅ | ✅ | ✅ | dwmac-rockchip |
| USB 2.0/3.0 | ✅ | ✅ | ✅ | 完整USB支持 |
| USB存储UAS加速 | ✅ | ✅ | ✅ | 提升硬盘性能 |
| **网络协议** | | | | |
| IPv4/IPv6双栈 | ✅ | ✅ | ✅ | 完整IPv6支持 |
| 组播/IPTV | ✅ | ✅ | ✅ | IGMP代理+udpxy |
| BBR拥塞控制 | ✅ | ✅ | ✅ | TCP BBR算法 |
| 全锥型NAT | ✅ | ✅ | ✅ | FullCone NAT |
| **文件系统** | | | | |
| EXT4 | ✅ | ✅ | ✅ | Linux标准 |
| NTFS (ntfs3) | ✅ | ✅ | ✅ | Windows分区 |
| exFAT/VFAT | ✅ | ✅ | ✅ | U盘常用格式 |
| BTRFS | ✅ | ✅ | ✅ | 高级文件系统 |
| XFS | ✅ | ✅ | ✅ | 高性能文件系统 |
| HFS+ | ✅ | ✅ | ✅ | macOS分区 |

### 版本选择建议

根据不同使用场景，推荐选择合适的固件版本：

| 使用场景 | 推荐版本 | 理由 |
|---------|---------|------|
| **家庭用户** | LEDE Master | 应用最丰富(31个)，包含磁盘管理、文件传输等实用工具 |
| **轻量级使用** | ImmortalWrt Master | 应用精简(23个)，资源占用小，运行流畅 |
| **追求稳定** | OpenWrt Main | 官方版本，更新及时，长期支持 |
| **开发测试** | OpenWrt Main | 软件包管理器更完善，便于安装测试 |
| **内网穿透需求** | LEDE / OpenWrt Main | 包含 frp 客户端和服务端 |
| **企业环境** | OpenWrt Main | 系统升级助手，便于批量管理 |

---

## ✨ 固件特性

### 🎯 核心特性

- ✅ **完整的中文界面** - 所有应用均包含简体中文语言包
- ✅ **硬件加速** - 支持 RK3399 硬件加密加速 (Crypto HW)
- ✅ **IPv4/IPv6 双栈** - 完整的 IPv6 支持
- ✅ **组播/IPTV** - 支持 IGMP 代理和 UDP 转发
- ✅ **Docker 支持** - 包含 Docker + Docker Compose
- ✅ **大容量存储** - 4GB RootFS 分区，适合安装大型应用
- ✅ **USB 存储** - 支持 USB 2.0/3.0 外接硬盘，含 UAS 加速
- ✅ **多文件系统** - EXT4/NTFS/exFAT/BTRFS/XFS/HFS+

### 🎨 主题

- **Argon** - 现代化设计的主题（默认）
- **Bootstrap** - 经典 Bootstrap 主题
- **Material** - Material Design 风格
- **Argon Config** - 可自定义主题颜色、透明度、背景

### 🔧 系统优化

- **CPU 频率管理** - 支持性能/省电/自动模式切换
- **BBR 拥塞控制** - 默认启用 TCP BBR，提升网络性能
- **TurboACC 加速** - 流量卸载、全锥型 NAT
- **硬件温度监控** - 实时显示 CPU 温度
- **IRQ 负载均衡** - 多核 CPU 中断均衡分配

---

## 📦 LuCI 应用列表

本固件预装了丰富的 LuCI 应用（**ImmortalWrt 23个** / **OpenWrt Main 25个** / **LEDE 31个**），涵盖系统管理、网络服务、安全防护等多个方面。

以下列表展示了主要应用（各版本共有应用）：

### 🔧 系统基础 (3个)

| 应用 | 说明 | 默认端口 |
|------|------|----------|
| **防火墙 (Firewall)** | 网络访问控制、端口转发、NAT配置 | - |
| **软件包管理 (opkg)** | 在线安装/卸载软件包 | - |
| **终端 (ttyd)** | Web端SSH终端，浏览器直接访问Shell | 7681 |

### 📁 文件管理与共享 (2个)

| 应用 | 说明 | 默认端口 |
|------|------|----------|
| **FileBrowser** | 强大的Web文件管理器，支持上传/下载/在线编辑 | 8088 |
| **网络共享 (KSMBd)** | 内核级Samba服务器，高性能文件共享 | 445 |

### 🐳 容器与虚拟化 (1个)

| 应用 | 说明 | 默认端口 |
|------|------|----------|
| **Docker管理器 (Dockerman)** | 图形化管理Docker容器、镜像、网络、卷 | - |

### 🌐 网络服务 (4个)

| 应用 | 说明 | 功能 |
|------|------|------|
| **动态DNS (DDNS)** | 动态域名解析 | 支持Cloudflare/阿里云/DNSPod等 |
| **网络加速 (TurboACC)** | 流量卸载加速 | BBR/FullCone NAT/流量分流 |
| **访问控制 (Access Control)** | 上网时间管理 | 游戏设备管控、家长控制 |
| **IP限速 (nft-qos)** | 基于IP的流量控制 | 上传/下载限速、QoS优先级 |

### 🔐 VPN服务 (4个)

| 应用 | 说明 | 协议 |
|------|------|------|
| **OpenVPN** | 经典开源VPN | OpenVPN |
| **WireGuard** | 现代高性能VPN | WireGuard |
| **OpenConnect Server (ocserv)** | 兼容Cisco AnyConnect | SSL VPN |
| **IPSec VPN** | 企业级VPN | IPSec/IKEv2 (strongSwan) |

### 🚀 代理与科学上网 (2个)

| 应用 | 说明 | 支持协议 |
|------|------|----------|
| **PassWall** | 透明代理工具 | Xray/V2Ray/Trojan/SS/SSR |
| **OpenClash** | Clash客户端 | Clash内核，规则分流 |

### 🛡️ 安全与防护 (2个)

| 应用 | 说明 | 功能 |
|------|------|------|
| **AdGuard Home** | 强大的广告过滤 | DNS级广告拦截/家长控制 |
| **KMS服务器 (vlmcsd)** | Windows/Office激活 | KMS激活服务器 |

### 📊 监控与通知 (2个)

| 应用 | 说明 | 功能 |
|------|------|------|
| **系统统计 (Statistics)** | 图表展示系统状态 | CPU/内存/网络/温度实时监控 |
| **微信通知 (ServerChan)** | 系统事件推送 | 通过Server酱推送到微信 |

### ⚡ 性能优化 (1个)

| 应用 | 说明 | 模式 |
|------|------|------|
| **CPU频率管理 (CPUFreq)** | CPU调度策略管理 | 性能/省电/自动/调度器 |

### 🎨 主题定制 (1个)

| 应用 | 说明 | 功能 |
|------|------|------|
| **Argon主题配置** | Argon主题自定义 | 颜色/透明度/背景/动画 |

---

## 🔧 系统功能

### 核心系统包

| 类别 | 软件包 | 说明 |
|------|--------|------|
| **容器运行时** | Docker + Containerd + Runc | 完整Docker环境 |
| **容器编排** | Docker Compose | 多容器应用编排 |
| **系统监控** | htop, irqbalance | 进程监控、中断均衡 |
| **开发工具** | git, curl, openssl-util | 版本控制、HTTP工具、SSL工具 |
| **磁盘工具** | fdisk, lsblk, btrfs-progs | 分区管理、BTRFS工具 |
| **自动挂载** | automount, block-mount | USB设备自动挂载 |
| **SSH服务** | Dropbear, SFTP Server | SSH登录、文件传输 |

### 文件系统支持

固件支持多种文件系统，适配各种存储设备：

| 文件系统 | 读写支持 | 用途 |
|---------|----------|------|
| **EXT4** | ✅ 读写 | Linux标准文件系统 |
| **NTFS** | ✅ 读写 | Windows分区（ntfs3内核驱动） |
| **exFAT** | ✅ 读写 | 大容量U盘、SD卡 |
| **VFAT/FAT32** | ✅ 读写 | 通用FAT格式 |
| **BTRFS** | ✅ 读写 | 高级文件系统，支持快照 |
| **XFS** | ✅ 读写 | 高性能文件系统 |
| **HFS+** | ✅ 读写 | macOS分区 |

### 内核模块

| 类别 | 模块 | 功能 |
|------|------|------|
| **USB驱动** | kmod-usb2, kmod-usb3 | USB 2.0/3.0支持 |
| **USB存储** | kmod-usb-storage, kmod-usb-storage-uas | 移动硬盘、U盘，UAS加速 |
| **USB串口** | ch341, cp210x, pl2303 | USB转串口设备 |
| **硬件加密** | kmod-crypto-hw-rockchip | RK3399硬件加密引擎 |
| **温度监控** | kmod-hwmon-rockchip-thermal | CPU温度传感器 |
| **网络协议** | kmod-bonding, kmod-veth, kmod-vxlan, kmod-gre | 高级网络功能 |
| **QoS** | kmod-sched-cake, kmod-sched-fq-codel | 流量整形 |

---

## 🌐 网络功能

### IPv4/IPv6 双栈

完整的 IPv4 和 IPv6 支持：

| 功能 | 说明 |
|------|------|
| **IPv6 内核** | kmod-ipv6 |
| **IPv6 防火墙** | kmod-ip6tables, ip6tables |
| **IPv6 NAT** | kmod-nf-nat6 |
| **IPv6 辅助** | ipv6helper - 自动配置IPv6 |
| **双栈DNS** | dnsmasq-full 支持 AAAA 记录 |

### 组播/IPTV 支持

针对IPTV、智能家居等组播应用优化：

| 组件 | 功能 |
|------|------|
| **IGMP代理** | igmpproxy - IGMP组播代理 |
| **内核模块** | kmod-igmp-proxy |
| **UDP代理** | udpxy - UDP转HTTP，方便浏览器观看IPTV |
| **隧道支持** | kmod-udptunnel4, kmod-udptunnel6 |

### 防火墙与NAT

| 功能 | 说明 |
|------|------|
| **基础防火墙** | Firewall4 (nftables) |
| **全锥型NAT** | kmod-ipt-fullconenat - 改善P2P、游戏NAT穿透 |
| **连接追踪扩展** | kmod-ipt-conntrack-extra |
| **流量限制** | kmod-ipt-hashlimit |
| **IP选项控制** | kmod-ipt-ipopt |
| **高级NAT** | kmod-ipt-nat-extra |
| **U32匹配** | kmod-ipt-u32 - 深度包检测 |

### VPN 核心

| VPN类型 | 软件包 | 特性 |
|---------|--------|------|
| **OpenVPN** | openvpn-openssl | 使用OpenSSL加密 |
| **WireGuard** | wireguard-tools, kmod-wireguard | 内核级VPN，性能极佳 |
| **IPSec** | strongswan-full, kmod-ipsec, kmod-ipsec6 | 企业级VPN |
| **OpenConnect** | ocserv | Cisco AnyConnect兼容 |

### 代理核心

| 代理工具 | 核心 | 说明 |
|---------|------|------|
| **PassWall** | Xray-core, V2ray-core | 多协议支持 |
| **OpenClash** | Clash 内核 | 规则分流、订阅管理 |

### DDNS 提供商

支持的动态DNS服务商：

- ✅ Cloudflare
- ✅ 阿里云 DNS
- ✅ DNSPod (腾讯云)
- ✅ 以及其他 ddns-scripts 支持的提供商

---

## 📖 使用说明

### 首次启动

1. **刷写固件**
   - 下载对应的固件文件（`.img` 格式）
   - 使用 balenaEtcher 或 Rufus 刷写到 SD 卡或 U 盘
   - 插入设备，从 SD 卡/U 盘启动

2. **首次登录**
   - 默认IP：`192.168.1.1`
   - 默认用户名：`root`
   - 默认密码：`password`
   - 访问：http://192.168.1.1

3. **修改密码**
   - 登录后立即修改默认密码
   - 路径：`系统` → `管理权` → `密码`

### 安装到 eMMC

1. 进入 OpenWrt 管理界面
2. 访问：`系统` → `Amlogic Service` → `Install OpenWrt`
3. 按提示操作，将系统安装到内置 eMMC

### 网络配置

#### 配置 WAN 口

默认 LAN 口为 `192.168.1.1`，需要配置 WAN 口上网：

1. 进入 `网络` → `接口`
2. 编辑 WAN 接口，选择上网方式：
   - **DHCP客户端**：自动获取IP
   - **PPPoE**：宽带拨号
   - **静态地址**：手动设置IP

#### 配置 IPv6

启用 IPv6 支持：

1. 进入 `网络` → `接口` → `WAN6`
2. 协议选择：`DHCPv6 客户端` 或 `静态地址`
3. 在 `LAN` 接口中启用 IPv6 分配

#### 配置 IPTV

如需使用 IPTV 功能：

1. 安装 igmpproxy：已预装
2. 配置 IGMP 代理：`网络` → `IPTV`
3. 启动 udpxy（可选）：方便浏览器观看

### Docker 使用

#### 通过 LuCI 管理

1. 访问 `Docker` → `容器`
2. 可以：
   - 拉取镜像
   - 创建容器
   - 管理网络和卷

#### 命令行使用

SSH 登录后可使用 `docker` 和 `docker-compose` 命令：

```bash
# 查看Docker版本
docker version

# 运行容器示例
docker run -d --name nginx -p 8080:80 nginx

# 使用 docker-compose
cd /root/my-app
docker-compose up -d
```

### 常用应用配置

#### FileBrowser 文件管理

- 访问地址：http://192.168.1.1:8088
- 默认用户：admin
- 默认密码：admin
- 功能：上传下载、在线编辑、创建分享链接

#### AdGuard Home 去广告

首次配置：
1. 访问 `服务` → `AdGuard Home`
2. 点击 `启用`
3. 访问 http://192.168.1.1:3000 完成初始化
4. 在 DHCP 中将 DNS 指向 AdGuard Home

#### KMS 激活服务器

启用 vlmcsd：
1. 访问 `服务` → `KMS服务器`
2. 启用服务
3. Windows/Office 激活命令：
   ```cmd
   slmgr /skms 192.168.1.1
   slmgr /ato
   ```

#### 微信通知 (ServerChan)

配置推送：
1. 访问 `服务` → `ServerChan`
2. 填写 SendKey（从 [Server酱](https://sct.ftqq.com) 获取）
3. 配置推送事件（设备上线、掉线等）

### 性能优化建议

#### CPU 频率策略

根据使用场景选择：

| 模式 | 适用场景 |
|------|----------|
| **性能模式** | 高负载应用、Docker、下载等 |
| **省电模式** | 轻度使用、降低发热 |
| **自动模式** | 日常使用，自动调整频率 |

配置路径：`系统` → `CPU 频率`

#### 网络加速

启用 TurboACC：
1. 访问 `网络` → `Turbo ACC 网络加速`
2. 勾选：
   - ✅ BBR拥塞控制
   - ✅ FullCone NAT（游戏、P2P优化）
   - ✅ 流量分流（可选）

---

## ❓ 常见问题

### Q1: 无法访问管理界面？

**A:** 检查以下项目：
- 确认设备已连接到网络
- 检查电脑 IP 是否在 `192.168.1.x` 网段
- 尝试禁用 Windows 防火墙
- 清除浏览器缓存或使用无痕模式

### Q2: 忘记管理员密码怎么办？

**A:** 两种方法：
1. **串口登录**：通过串口进入系统修改密码
2. **重置系统**：重新刷写固件

### Q3: Docker 容器无法访问外网？

**A:** 检查：
- 防火墙规则：`网络` → `防火墙` → 允许 Docker 转发
- DNS 设置：容器内 DNS 是否正确
- 路由：`ip route` 检查默认路由

### Q4: IPv6 无法使用？

**A:** 确认：
- 上游网络支持 IPv6
- WAN6 接口已正确配置
- 防火墙允许 IPv6 流量
- 检查 `ipv6helper` 是否启用

### Q5: IPTV 卡顿或无法播放？

**A:** 优化建议：
- 确保组播包能正确转发（配置 igmpproxy）
- 关闭不必要的防火墙规则
- 使用 udpxy 转换后通过浏览器观看
- 检查网络带宽是否充足

### Q6: 如何扩容 RootFS 分区？

**A:**
固件默认 4GB RootFS 分区。如需扩容：
1. 使用 `fdisk` 或 `parted` 扩展分区
2. 使用 `resize2fs` 扩展文件系统
3. 或者使用外置存储（USB/M.2）

### Q7: CPU 温度过高怎么办？

**A:**
- 查看温度：`系统` → `系统信息` 或 `Statistics`
- 降温措施：
  - 加装散热片/风扇
  - 降低 CPU 频率（省电模式）
  - 减少后台运行的服务

### Q8: 如何备份配置？

**A:**
定期备份配置：
1. `系统` → `备份/升级`
2. 点击 `生成备份`
3. 下载 `.tar.gz` 文件保存

### Q9: PassWall/OpenClash 无法使用？

**A:**
需要自行配置：
- 添加订阅链接或节点
- 配置分流规则
- 详细配置请参考各插件官方文档

### Q10: 如何更新系统？

**A:**
两种方式：
1. **在线更新**：`系统` → `备份/升级` → 上传新固件
2. **保留配置升级**：勾选 `保留配置` 再刷写

---

## 📞 技术支持

### 相关链接

- **项目地址**：https://github.com/ophub/amlogic-s9xxx-openwrt
- **问题反馈**：https://github.com/ophub/amlogic-s9xxx-openwrt/issues
- **OpenWrt 官方文档**：https://openwrt.org/docs/start
- **ImmortalWrt 文档**：https://github.com/immortalwrt/immortalwrt

### 配置文件位置

本设备的配置文件位于项目的 `config/` 目录：

```
config/
├── immortalwrt_master/config  # ImmortalWrt 配置
├── lede_master/config         # LEDE 配置
└── openwrt_main/config        # OpenWrt 配置
```

---

## 📝 更新日志

### v1.1 (2024-12-18)

#### 文档更新

- ✅ 新增"固件能力对比"章节 - 详细对比三个固件版本的功能支持
- ✅ 添加完整的能力对比表格：
  - 核心系统功能对比
  - 网络功能对比
  - 文件与存储功能对比
  - 容器与应用服务对比
  - 底层支持对比（内核/硬件/协议/文件系统）
- ✅ 新增版本选择建议 - 根据使用场景推荐最适合的固件版本
- ✅ 更新固件版本表格 - 添加内核版本和应用数量信息

### v1.0 (2024-12-16)

#### 新增应用

- ✅ FileBrowser - Web 文件管理器
- ✅ ServerChan - 微信通知推送
- ✅ AccessControl - 上网时间管控
- ✅ vlmcsd - KMS 激活服务
- ✅ nft-qos - IP 限速控制
- ✅ AdGuard Home - DNS 级广告拦截
- ✅ OpenClash - Clash 代理客户端

#### 网络增强

- ✅ IPv6 完整支持
- ✅ 组播/IPTV 支持
- ✅ Docker Compose 容器编排

#### 修复问题

- ✅ ImmortalWrt 编译失败问题（缺少 rootfs.tar.gz）

---

## 📄 许可证

本项目基于以下开源项目：

- [OpenWrt](https://github.com/openwrt/openwrt) - GPL-2.0
- [ImmortalWrt](https://github.com/immortalwrt/immortalwrt) - GPL-2.0
- [Lean's LEDE](https://github.com/coolsnowwolf/lede) - GPL-2.0
- [ophub/amlogic-s9xxx-openwrt](https://github.com/ophub/amlogic-s9xxx-openwrt) - GPL-2.0

---

**文档版本**：v1.1
**更新日期**：2024-12-18
**适用固件版本**：OpenWrt Main / ImmortalWrt Master / LEDE Master
