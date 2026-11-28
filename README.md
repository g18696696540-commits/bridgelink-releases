<div align="center">

# BridgeLink OPC Gateway

**工业协议采集与 OPC UA 网关** · 重庆乾端科技有限公司

[![Release](https://img.shields.io/github/v/release/g18696696540-commits/bridgelink-releases?label=release&color=0b7285)](../../releases/latest)
[![Downloads](https://img.shields.io/github/downloads/g18696696540-commits/bridgelink-releases/total?label=downloads&color=2f9e44)](../../releases)
![Platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011%20x64-0078D4)
![.NET](https://img.shields.io/badge/.NET-8.0-512BD4)

本仓库**只发布安装包与绿色版**，不包含源代码。

</div>

---

## 简介

BridgeLink OPC Gateway 面向产线数据采集：一套 Runtime 服务直连 PLC、仪表、机器人、扫码枪等现场设备，
把点位统一成标签模型，对内提供工程配置与实时监控，对外提供标准 **OPC UA** 接口（默认端口 `4840`）。

## 功能特性

| 能力 | 说明 |
|---|---|
| **多协议采集** | 50+ 协议 / 品牌：Modbus RTU/TCP、Siemens S7、Mitsubishi MC、Omron FINS、Allen-Bradley、Beckhoff、Delta、Fatek、Fuji、LS、Panasonic、Xinje、Keyence、BACnet、IEC 104、DL/T 645、SECS/GEM、SNMP、MQTT、AMQP、STOMP、CoAP、HTTP、WebSocket、OPC UA、MySQL、PostgreSQL、Redis、MongoDB、InfluxDB、TDengine、Prometheus 等 |
| **OPC UA 服务端** | 标准地址空间，支持多会话与安全策略，可配置额外监听端点 |
| **工程化配置** | Studio 可视化配置「通道 → 设备 → 标签」，支持批量导入、字序与字符串编码、点位仿真与在线监控 |
| **后台服务** | Runtime 以 Windows 服务 `BridgeLinkRuntime` 常驻，安装后开机自启 |
| **流程测试（信号联调）** | 按节点树配置触发点 / 等待点 / 采集点 / 输出信号点，只需给首工位一个触发，即可按信号关系跑通整条链路 |
| **授权管理** | 未激活可试用 30 天（首次运行起算，重启不续期），到期导入正式 License |

## 下载

前往 [Releases](../../releases/latest) 获取最新版本：

| 文件 | 说明 |
|---|---|
| `BridgeLink-Setup-<版本>.exe` | 安装版：Studio + Runtime 服务 + 托盘，自带 .NET 8 运行时 |
| `BridgeLink-Setup-<版本>.zip` | 绿色版：解压即用 |
| `BridgeLink-Web-<版本>.zip` | 官网站点发布包（IIS / ASP.NET Core 8，自包含 win-x64，不含 `wwwroot\downloads`） |
| `*.sha256` | 对应文件的 SHA-256 校验值 |

## 安装与启动

**系统要求**：Windows 10 / 11 x64（安装包自带 .NET 8 运行时，无需另装）

1. 运行 `BridgeLink-Setup-<版本>.exe`，默认安装到 `C:\Program Files\BridgeLink`；
2. 安装器注册并启动 Windows 服务 `BridgeLinkRuntime`（开机自启）；
3. 从开始菜单打开 **BridgeLink Studio**，配置通道、设备与标签；
4. OPC UA 客户端连接 `opc.tcp://<主机>:4840`。

> 绿色版解压后直接运行 `Studio\BridgeLink.Studio.exe`；Runtime 需手动启动 `Runtime\BridgeLink.Runtime.exe`。

### 校验安装包

```powershell
Get-FileHash .\BridgeLink-Setup-<版本>.exe -Algorithm SHA256
```

输出与同名 `.sha256` 文件中的值一致即可。

## 安装目录

```
C:\Program Files\BridgeLink\
├── Studio\        # 配置客户端（WPF）
├── Runtime\       # 采集服务（Windows 服务）
├── Tray\          # 托盘程序
└── docs\          # 协议说明与使用文档
```

## 常见问题

<details>
<summary><b>服务启动失败 / 采集不到数据？</b></summary>

1. 在 `services.msc` 确认 `BridgeLinkRuntime` 处于「正在运行」；
2. 检查设备 IP、端口、站号是否可达（Studio 内「测试连接」）；
3. 在 Studio 的监控与日志面板查看采集错误，必要时导出诊断包。
</details>

<details>
<summary><b>OPC UA 客户端连不上？</b></summary>

默认端点 `opc.tcp://<主机>:4840`。确认 4840 端口未被占用、防火墙已放行，并在工程设置中启用 OPC UA 服务端。
</details>

<details>
<summary><b>试用到期怎么办？</b></summary>

未激活可试用 30 天（首次运行起算，重启不续期）。到期后在 Studio「关于 → 授权许可」复制机器码，向供应商申请正式 License 导入即可。
</details>

## 版本历史

每个版本的变化见 [Releases](../../releases) 中的 Release Notes。

## 联系我们

商务与技术咨询请在 [Issues](../../issues) 留言。
