# BridgeLink OPC Gateway · Windows 工业协议采集与 OPC UA 网关（Modbus / Siemens S7 / Mitsubishi MC / Omron / MQTT / IEC 104）

**BridgeLink OPC Gateway（桥联）** 是一款运行在 Windows 上的**工业数据采集网关**：通过 **39 个自研驱动** 把 PLC、仪表、电力设备、数据库与消息队列的数据统一采集为**标签**，对内提供工程配置与实时监控，对外提供标准 **OPC UA 服务端**（默认 `opc.tcp://<主机>:4840/BridgeLink/Server`）。采集进程以 **Windows 服务**（`BridgeLinkRuntime`）常驻并开机自启，配置端是独立的桌面客户端 **BridgeLink Studio**。

> 未激活可免费试用 **30 天**（首次运行起算，重启不续期）；提供**安装版**与**绿色版（免安装）**，安装包自带 .NET 8 运行时，目标机无需另装环境。

## About (English)

BridgeLink OPC Gateway is a Windows industrial data acquisition gateway. It collects data from PLCs, meters, power devices and databases through 39 built-in drivers, unifies everything into a tag model, and exposes it over a standard OPC UA server. The runtime runs as a Windows service; configuration is done in a WPF desktop client (BridgeLink Studio). A 30-day trial is available, and the installers are self-contained — no .NET installation required.

[![Release](https://img.shields.io/github/v/release/g18696696540-commits/bridgelink-releases?label=最新版本&color=0b7285)](../../releases/latest)
[![Downloads](https://img.shields.io/github/downloads/g18696696540-commits/bridgelink-releases/total?label=下载量&color=2f9e44)](../../releases)
![Platform](https://img.shields.io/badge/平台-Windows%2010%2F11%20x64-0078D4)
![OPC UA](https://img.shields.io/badge/OPC%20UA-4840-0b7285)

## 功能详情

### 1. 多协议采集（39 个自研驱动）

- **PLC / 现场设备**：Siemens S7、S7-PPI、三菱 MC（Melsec / Mitsubishi）、Omron FINS、Omron CIP、Allen-Bradley、DF1、Beckhoff ADS、LS（XGT）、Panasonic、Fatek、GE SRTP、Modbus RTU / TCP；
- **电力 / 楼宇**：IEC 101、IEC 104、IEC 61850、DL/T 645、DNP3、BACnet；
- **消息与数据库**：MQTT、AMQP、STOMP、CoAP、HTTP、WebSocket、MTConnect、SNMP、MySQL、PostgreSQL、MongoDB、Redis、InfluxDB、TDengine、Prometheus；
- **通用能力**：OPC UA 客户端采集、内置**模拟器**（没有设备也能把工程与流程调通）、通用透传与文本协议；
- **工程操作**：通道 → 设备 → 标签三级模型，支持 **CSV 导入 / 导出**、复制粘贴设备与标记、**测试连接**、单点读取与写入。

### 2. 标签模型

- 数据类型：Bool、Byte、Int16 / Int32 / Int64、UInt16 / UInt32 / UInt64、Float、Double、String；
- 读写权限（R / W / RW）、启用停用、描述备注；
- **线性变换**（`Scale` / `Offset`）与**死区**（`Deadband`），工程侧直接换算工程量；
- **扫描组**：按组设置采集周期，绝对下限 **10 ms**；
- Modbus 地址按现场习惯填写：`HR:100`（0 基偏移）、`4xxxx`（整体偏 1）、`%MW<n>`（与 `HR:<n>` 一一对应）；字符串用 `,STRINGn`（1–240 字符），字序支持 `ABCD`（默认）与 `CDAB`（汇川、三菱、CODESYS 常用）。

### 3. OPC UA 服务端

- 端点 `opc.tcp://<主机>:4840/BridgeLink/Server`，绑定网卡、端口、端点路径均可配置；
- 安全策略 `None` / `Sign` / `SignAndEncrypt` 可分别开关；可关闭匿名访问并配置用户名密码；
- 会话上限可配（设计目标 10,000）；
- 标签右键**复制 OPC UA NodeId**，直接给 MES / SCADA / 组态软件使用。

### 4. 实时监控

- 标签页实时值、质量与时间戳，支持筛选、分页与「仅启用」；
- **监控浮框**：把常用点位固定成独立小窗，常驻桌面；
- 右键**读取 / 写入 / 加入监控**，不启动整条采集也能单点调试。

### 5. 流程测试（信号联调）

- 按**节点树**配置：触发点 → 等待点 → 采集点 → 输出信号点，父节点完成自动武装子节点；
- 触发方式四种：父完成 / 点位条件 / 界面按钮 / 定时；条件支持 `=` `≠` `>` `<` 与上升沿、下降沿，可「全部满足」或「任一满足」；
- 只需给首工位一个触发，就能按信号关系跑通整条链路；支持循环与循环延时；
- 节点级超时只停该节点及子树，其余分支继续；
- 运行期实时记录（时间 / 轮次 / 节点 / 点位 / 值 / 质量 / 耗时）并可导出 CSV；
- **零侵入**：只读工程标签，配置存旁路 JSON，不修改工程文件，不动 Runtime / 驱动。

### 6. 后台服务与托盘

- `BridgeLinkRuntime` 注册为 Windows 服务，安装后开机自启，无人值守运行；
- 托盘程序随系统登录启动，可快速打开 Studio、查看服务状态。

### 7. 容量与部署

- 设计容量：**500 万标签 / 5 万设备 / 1 万 OPC UA 会话**（工程级可配）；
- 自包含发布（win-x64），安装包内含 .NET 8，目标机无需安装运行时；
- 默认安装目录 `C:\Program Files\BridgeLink`，含 `Studio` / `Runtime` / `Tray` / `docs`；
- 卸载不会删除 `ProgramData` 下的工程与授权信息，重装不丢配置。

### 8. 授权与试用

- 未激活试用 **30 天**，从首次运行起算，重启服务或 Studio 不会续期；
- 到期后在 Studio「关于 → 授权许可」复制**机器码**，向供应商申请正式 License 导入即可；
- 授权与激活全程**离线**，与机器码绑定。

## 适用场景

产线数据采集 · PLC 联网与协议转换 · 对接 MES / SCADA / 组态软件 · OPC UA 统一接口 · 工位信号联调与联锁验证 · 无设备时的工程预调试（内置模拟器） · 老旧设备数据上云前的协议归一

## 常见问题（FAQ）

**Q：支持哪些 PLC 和协议？**

Siemens S7 / S7-PPI、三菱 MC、Omron FINS / CIP、Allen-Bradley、Beckhoff ADS、LS、Panasonic、Fatek、GE SRTP、Modbus RTU / TCP；电力侧支持 IEC 101 / 104 / 61850、DL/T 645、DNP3、BACnet；另有 MQTT、HTTP、WebSocket、MySQL、PostgreSQL、Redis、InfluxDB、TDengine 等 30 余种数据源。

**Q：Modbus 地址怎么写？**

三种写法都支持：`HR:100` 表示保持寄存器偏移 100（0 基）；`40001` 这类 `4xxxx` 写法整体偏 1（`40001` = 偏移 0）；`%MW100` 与 `HR:100` 等价。字符串写成 `HR:100,STRING20`，长度 1–240。

**Q：一个字里的高低字节顺序不对怎么办？**

在标签上设置**字序**：默认 `ABCD`；汇川、三菱、CODESYS 常用 `CDAB`。字符串另有字节序选项。

**Q：一个网关能采多少点？**

设计目标是 500 万标签、5 万设备、1 万 OPC UA 会话，实际取决于现场协议、扫描周期与硬件；建议按产线分段部署，用扫描组分周期采集。

**Q：OPC UA 客户端怎么连？**

`opc.tcp://<主机IP>:4840/BridgeLink/Server`。若关闭了匿名访问，需要先在工程设置里配置用户名与密码；安全策略按客户端要求选择 None / Sign / SignAndEncrypt。

**Q：试用多久？到期会怎样？**

未激活可试用 30 天（首次运行起算，重启不续期）。到期后 Runtime 停止采集并提示导入正式 License，导入后恢复，无需重装。

**Q：绿色版怎么用？**

解压后直接运行 `Studio\BridgeLink.Studio.exe`；Runtime 需手动启动 `Runtime\BridgeLink.Runtime.exe`（绿色版不注册 Windows 服务）。

**Q：服务起不来或采不到数据？**

1）`services.msc` 确认 `BridgeLinkRuntime` 正在运行；2）Studio 里用「测试连接」核对 IP、端口、站号；3）检查防火墙与网段；4）仍不通时导出诊断信息给供应商。

**Q：支持 Windows 7 / 32 位系统吗？**

只支持 **Windows 10 / 11 x64**，安装包为 win-x64 自包含发布。

**Q：和 Kepware / Ignition 有什么区别？**

BridgeLink 面向国内产线现场：内置国产 PLC 与仪表驱动、中文工程配置、离线授权，并把「信号联调」做进了同一套工具里。选型请以现场协议覆盖、点数规模与服务响应为准。

## 下载与安装

到 [Releases](../../releases) 页面下载最新版本：

| 文件 | 说明 |
| --- | --- |
| `BridgeLink-Setup-<版本>.exe` | 安装版：Studio + Runtime 服务 + 托盘，含开始菜单快捷方式，需管理员权限 |
| `BridgeLink-Setup-<版本>.zip` | 绿色版：解压即用，不注册服务 |
| `BridgeLink-Web-<版本>.zip` | 官网站点发布包（IIS / ASP.NET Core 8，自包含 win-x64，不含 `wwwroot\downloads`） |
| `*.sha256` | 对应文件的 SHA-256 校验值 |

```powershell
Get-FileHash .\BridgeLink-Setup-<版本>.exe -Algorithm SHA256
```

与同名 `.sha256` 文件比对一致后再运行。绿色版首次运行如遇 SmartScreen「未知发布者」，选择「更多信息 → 仍要运行」。

## 系统要求

- Windows 10 / 11，64 位；
- 自包含发布，**无需安装 .NET**；
- 建议 4 GB 以上内存；点位规模大、扫描周期短时按实际压力评估；
- 安装版需要管理员权限（注册 Windows 服务、写 `Program Files`）。

## 技术栈

.NET 8 · C# · WPF（Studio）· Windows Service（Runtime）· OPC UA 服务端 · 39 个自研协议驱动 · win-x64 自包含发布（无需安装 .NET）

## 说明

- 本仓库**只发布 Windows 安装包与绿色版**，不包含源代码；
- 协议与设备的兼容性以现场实测为准，特殊型号可联系供应商补充驱动；
- 采集与转发涉及现场设备与生产数据，请只在获得授权的设备与网络中使用。

---

**关键词**：OPC UA 网关、工业数据采集、PLC 采集、Modbus 采集、西门子 S7、三菱 MC、欧姆龙 FINS、Allen-Bradley、Beckhoff ADS、IEC 104、DL/T 645、BACnet、MQTT 采集、数据库采集、标签引擎、实时监控、信号联调、流程测试、Windows 服务、绿色版、免安装、离线授权、BridgeLink、桥联、重庆乾端科技。

**Keywords**: OPC UA gateway, industrial data acquisition, PLC data collection, Modbus RTU/TCP, Siemens S7, Mitsubishi MC, Omron FINS, Allen-Bradley, Beckhoff ADS, IEC 104, DLT645, BACnet, MQTT, tag engine, real-time monitoring, Windows service, portable, offline licensing, BridgeLink.
