# 仓库涉及机型硬件配置汇总

> 更新时间：2026-09-19
>
> 本文根据本仓库的提交记录、配置文件和公开资料整理。公开资料之间可能存在地区版、批次版差异；`待确认` 表示尚未找到足够可靠的公开来源，不能用于直接选择刷机镜像或修改 DDR/NAND 参数。

## 机型总表

| 仓库名称 | 厂商/零售型号 | SoC/CPU | RAM | 闪存 | 有线网络 | 无线 | 启动/恢复相关 |
|---|---|---|---:|---:|---|---|---|
| G-AX1800 | 型号归属待确认 | MT7621 双核 880 MHz（仓库平台） | 待确认 | 待确认 | MT7621/MT7530 千兆交换机（平台级） | AX1800，芯片待确认 | MT7621 NAND U-Boot，仓库提交明确支持 |
| ZTT RX6000 | ZTT RX6000 | MT7621 双核 880 MHz（高度可能，待实机确认） | 待确认 | 待确认 | 千兆交换机，端口数待确认 | AC/AX 规格待确认 | MT7621 NAND U-Boot，仓库提交明确支持 |
| 小米 R3P | Xiaomi Mi Router 3 Pro | MT7621A，双核 880 MHz | 256 MB | NAND，常见 128 MB | 1×WAN + 3×LAN，千兆 | MT7615，2.4/5 GHz 802.11ac | NAND 启动，OpenWrt 有独立设备支持 |
| 网件 R6800 | NETGEAR AC1900 R6800 | MT7621AT，双核 880 MHz | 256 MB | 128 MB（厂商数据表） | 千兆以太网交换机 | 双频 AC1900，3×3 2.4 GHz + 3×3 5 GHz | U-Boot；OpenWrt 有独立设备支持 |
| RM2100 | Xiaomi Redmi Router AC2100 | MT7621，双核 880 MHz | 128 MB（常见公开资料） | 128 MB ESMT NAND | 1×WAN + 3×LAN，千兆 | 2.4/5 GHz 802.11ac，4×4 规格（区域资料有差异） | NAND + NMBM；仓库配置为 MT7621 NAND |
| 小娱 C3 NAND 版 | 小娱 C3（NAND 版） | MT7621（仓库平台，待实机确认） | 待确认 | NAND，容量待确认 | 千兆端口布局待确认 | 双频无线，芯片待确认 | 仓库提交明确区分 NAND 版 |
| CMCC A9 | 中国移动 A9 | MT7621（仓库平台，待实机确认） | 待确认 | 待确认 | 待确认 | 双频无线，芯片待确认 | MT7621 NAND U-Boot |
| ASUS RT-AX53U | ASUS RT-AX53U / RT-AX1800U | MT7621AT，双核 880 MHz | 256 MB | 128 MB NAND | 4×千兆 | MT7975 + MT7905，2.4/5 GHz Wi‑Fi 6 | U-Boot，支持 TFTP 恢复 |
| ASUS RT-AX54 | ASUS RT-AX54 / AX1800 系列 | MT7621AT，双核 880 MHz | 256 MB | 128 MB NAND | 1×WAN + 4×LAN（公开设备资料） | 双频 Wi‑Fi 6，具体射频因变体而异 | U-Boot，OpenWrt 有独立设备支持 |
| ASUS ZenWiFi XD4S | ASUS XD4S | MT7621（仓库配置命名推断，待实机确认） | 待确认 | 待确认 | 千兆端口，具体数量待确认 | AX1800 Mesh，射频芯片待确认 | 仓库提供 `config_xd4s` |
| ASUS 4G-AX56 | ASUS 4G-AX56 | MT7621（仓库配置命名推断，待实机确认） | 待确认 | 待确认 | 千兆端口，具体数量待确认 | AX1800 级双频，射频芯片待确认 | 仓库提供 `config_4gax56` |
| ASUS RT-AX54/RT-AX53U 变体 | 可能包括 RT-AX1800S、RT-AX1800HP | MT7621AT | 256 MB（公开 OpenWrt 资料） | 128 MB NAND | 千兆 | Wi‑Fi 6 | 不同硬件变体不可直接共用镜像 |

## 已确认机型

### 小米 Mi Router 3 Pro（R3P）

- SoC：MediaTek MT7621A，双核 MIPS，880 MHz。
- 内存：256 MB DDR3。
- 闪存：NAND；公开启动日志显示常见容量为 128 MB，NAND 页 2048 B、擦除块 128 KiB。
- 网络：MT7530 交换芯片，1 个 WAN、3 个 LAN，均为千兆。
- 无线：MediaTek MT7615，双频 802.11ac，4 根外置天线。
- 备注：OpenWrt 页面显示该设备使用 NMBM/UBI 类 NAND 分区；仓库的 `config_r3p` 采用 `mt7621_nand_rfb` 板级配置。

来源：

- https://openwrt.org/toh/xiaomi/mi_router_3_pro
- https://55bf4b76-a5b9-4058-a97d-c72d8ac6922e.filesusr.com/ugd/7e125d_5bdd4847d907460d94fe24a9d134e061.pdf

### NETGEAR R6800

- SoC：MediaTek MT7621AT，双核 880 MHz。
- 内存：256 MB RAM。
- 闪存：128 MB flash。
- 无线：AC1900，2.4 GHz 和 5 GHz 均为 3×3，支持波束成形。
- 外设：USB 存储访问功能；具体 USB 版本应以拆机或设备树为准。
- 备注：厂商数据表确认内存/闪存，但没有给出完整 NAND 型号；OpenWrt/DeviWiki 可用于补充芯片级资料。

来源：

- https://www.netgear.com/images/datasheet/networking/wifirouter/R6800.pdf
- https://deviwiki.com/wiki/Netgear_R6800
- https://openwrt.org/toh/netgear/r6800

### 小米 Redmi Router AC2100（RM2100）

- SoC：MediaTek MT7621。
- 闪存：公开 OpenWrt 资料通常标为 128 MB ESMT NAND。
- 网络：1 个 WAN + 3 个 LAN，千兆。
- 无线：双频 802.11ac，公开资料对内存和射频配置存在版本差异；仓库设备配置使用 MT7621 NAND 启动链。
- 备注：不要将 Redmi AC2100 与黑色圆柱形 Xiaomi Mi Router AC2100 混为同一硬件；两者刷机镜像和分区布局不同。

来源：

- https://openwrt.org/toh/xiaomi/xiaomi_redmi_router_ac2100
- https://openwrt.org/toh/hwdata/xiaomi/xiaomi_redmi_router_ac2100
- https://git.laboratoryb.org/hurricos/openwrt/commits/commit/6ea87d35c671f50d86cc7f2969e3930e03e3ea31

### ASUS RT-AX53U

- SoC：MediaTek MT7621AT，双核 880 MHz。
- 内存：256 MB。
- 闪存：128 MB NAND。
- 网络：4 个千兆以太网端口（OpenWrt Techdata 记录）。
- 无线：MT7975 + MT7905，2.4/5 GHz 802.11ax，4 根不可拆天线。
- USB：1×USB 2.0。
- 串口：3.3 V，115200/8N1；U-Boot TFTP 恢复。

来源：

- https://openwrt.org/toh/hwdata/asus/asus_rt-ax53u
- https://www.asus.com/uk/networking-iot-servers/wifi-routers/asus-wifi-routers/rt-ax53u/techspec/

### ASUS RT-AX54

- SoC：MT7621AT，双核 880 MHz。
- 内存/闪存：OpenWrt 设备资料标为 256 MB RAM、128 MB NAND。
- 无线：双频 Wi‑Fi 6；RT-AX54、RT-AX54HP、RT-AX1800HP、RT-AX1800S 共享部分软件支持，但不能据此认定硬件完全相同。
- 备注：公开启动日志显示 NAND 为 128 MiB，且使用 NMBM；该信息与仓库的 NAND failsafe 设计相符。

来源：

- https://openwrt.org/toh/asus/rt-ax54
- https://openwrt.org/toh/asus/rt-ax54?s%5B%5D=op
- https://firmware-selector.openwrt.org/?version=23.05.0&target=ramips%2Fmt7621&id=asus_rt-ax54

## 公开资料不足的机型

### G-AX1800

仓库提交明确添加了该型号，但没有在仓库中提供独立 DTS 或完整板级目录；目前只能确认它被纳入 MT7621 NAND U-Boot 体系。建议通过串口启动日志确认：CPU 频率、DDR 容量、NAND ID、交换机端口映射、无线 PCIe 芯片和 GPIO LED 定义。

### ZTT RX6000

公开网页中存在多个同名或相近型号，尚未找到能同时确认 SoC、内存、闪存和 PCB 版本的可靠一手资料。仓库提交说明它是 MT7621 目标设备之一，但不应仅凭型号名选择 R3P、R6800 或 RM2100 镜像。

### 小娱 C3 NAND 版

仓库提交明确称为“C3 nand版”，说明至少存在 NOR/NAND 硬件差异。当前公开资料不足以确认 NAND 厂商、容量、坏块管理区域和 DDR 颗粒。刷写前必须读取 NAND ID，并核对 U-Boot 环境偏移、NMBM 起始块和 kernel/UBI 分区边界。

### CMCC A9

中国移动 A9 存在运营商定制批次，公开资料容易把不同代际硬件混在一起。仓库仅能确认其适配 MT7621 NAND 方案；RAM、NAND 容量、无线芯片和网口布局应以拆机照片、串口日志和原厂设备树为准。

### ASUS ZenWiFi XD4S 与 4G-AX56

仓库中的 `config_xd4s`、`config_4gax56` 使用 MT7621 NAND 板级配置，但这只能说明启动代码复用，不能证明两者硬件完全相同。尤其 4G-AX56 还可能包含蜂窝基带、SIM 接口、电源和 USB/PCIe 资源差异；XD4S 也可能有不同区域包和 Mesh 节点版本。

## 与本仓库刷机相关的结论

1. 多数目标共享 MT7621/MIPS32r2，但 **SoC 相同不等于镜像兼容**；GPIO、DDR 参数、NAND ID、分区布局和无线校准区都可能不同。
2. 仓库的 failsafe 代码会提供 NVRAM、Factory、Factory2 擦除入口。Factory/Factory2 往往包含 MAC 地址、无线校准和地区参数，擦除前必须有备份。
3. 对 NAND 机型，应优先记录 `nand info`、NMBM 状态和 MTD 分区；不要直接套用 NOR 机型的偏移地址。
4. 对资料不足的四个型号，建议把实机采集结果补充到本文：串口日志、`bdinfo`、NAND ID、DDR 容量、以太网 PHY 地址、PCIe 无线设备 ID 和完整分区表。

## 仓库依据

- `config_r3p`
- `config_rm2100`
- `config_rtax53u`
- `config_rtax54`
- `config_xd4s`
- `config_4gax56`
- Git 提交：`添加G-AX1800`、`添加ZTT RX6000`、`添加小米R3P`、`添加网件R6800`、`添加RM2100`、`添加小娱C3nand版`、`添加CMCCA9`
