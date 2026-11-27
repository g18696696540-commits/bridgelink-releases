# BridgeLink OPC Gateway · 发行版

本仓库只存放 **Windows 安装包 / 绿色版**，不包含源码。

## 下载

到 [Releases](../../releases/latest) 下载对应版本：

| 文件 | 说明 |
|---|---|
| `BridgeLink-Setup-<版本>.exe` | 安装版：Studio + Runtime 服务（开机自启）+ 托盘，自带 .NET 8 运行时 |
| `BridgeLink-Setup-<版本>.zip` | 绿色版：解压即用 |
| `*.sha256` | 对应文件的 SHA-256 校验值 |
| `BridgeLink-Web-<版本>.zip` | 官网站点发布包（IIS 部署，ASP.NET Core 8，自包含 win-x64） |

## 说明

- 支持 Windows 10 / 11 x64；安装版会注册 Windows 服务 `BridgeLinkRuntime`。
- 未激活可免费试用 30 天（首次运行起算，重启不续期），到期后导入正式 License 继续使用。
- 安装包与官网包的版本号与程序集版本一致，SHA-256 见同名 `.sha256` 文件。
