# 翻墙VPN部署教程 (基于 233boy V2Ray 脚本)

本文档整理自 GitHub 开源项目 [233boy/v2ray](https://github.com/233boy/v2ray)，提供了一个高效率、超快速、极易用的 V2Ray 一键安装与管理教程。

## 1. 脚本特点

该脚本以**多配置同时运行**为核心设计，具有以下主要特点：
- **快速安装 & 零学习成本**：简化所有流程，自动化 TLS 配置。
- **协议支持全面**：一键添加 Shadowsocks, VMess (TCP/mKCP/QUIC/WS/H2/gRPC), VLESS, Trojan 等。
- **高级功能**：支持动态端口、一键启用 BBR、一键更改伪装网站等。
- **安全与屏蔽**：自动屏蔽 BT 下载和中国大陆 IP，防止滥用。
- **高效管理**：添加、更改、查看、删除配置等操作仅需不到 1 秒。

## 2. 安装与部署

请在您的海外 VPS (Linux 系统) 上以 `root` 用户身份执行以下操作。

### 下载并执行安装脚本
通常可以通过以下命令一键安装（具体请参考项目最新说明）：
```bash
bash <(curl -s -L https://git.io/v2ray.sh)
```
*(注：安装过程中请根据屏幕提示选择您需要的协议和端口，脚本会自动完成依赖安装和环境配置。)*

## 3. 常用管理命令

安装完成后，您可以通过 `v2ray` 命令来管理所有的代理配置。使用 `v2ray help` 可以查看所有可用命令。

### 基本操作
- `v2ray info` 或 `v2ray i [name]`：查看当前配置信息。
- `v2ray add [protocol]` 或 `v2ray a`：添加一个新的配置（例如：`v2ray a vmess-ws-tls`）。
- `v2ray change [name]` 或 `v2ray c`：更改现有配置。
- `v2ray del [name]` 或 `v2ray d`：删除指定配置（注意：此操作无需确认，直接删除）。
- `v2ray qr [name]`：生成并显示配置的二维码信息，方便手机端扫码导入。
- `v2ray url [name]`：显示配置的 URL 链接信息。

### 更改配置参数
您可以单独更改某个配置的特定参数：
- `v2ray port [name] [port]`：更改端口。
- `v2ray id [name] [uuid]`：更改 UUID。
- `v2ray host [name] [domain]`：更改伪装域名。
- `v2ray path [name] [path]`：更改路径。
- `v2ray type [name] [type]`：更改伪装类型。

### 系统与服务管理
- `v2ray status` 或 `v2ray s`：查看 V2Ray 运行状态。
- `v2ray start` / `v2ray stop` / `v2ray restart`：启动、停止或重启 V2Ray 服务。
- `v2ray update` 或 `v2ray u`：更新 V2Ray 核心、脚本或数据文件。
- `v2ray bbr`：一键启用 BBR 拥塞控制算法（推荐开启，可大幅提升网络速度）。
- `v2ray log` / `v2ray logerr`：查看运行日志或错误日志。

## 4. 客户端连接

部署完成后，您可以使用 `v2ray qr` 获取二维码，或使用 `v2ray url` 获取订阅/分享链接。
推荐的客户端：
- **Windows / macOS / Linux**: [Clash Verge Rev](https://www.clashverge.dev/) (支持 V2Ray/Mihomo 内核)
- **Android**: v2rayNG, Clash for Android
- **iOS**: Shadowrocket, Quantumult X

## 5. 常见问题与反馈
- 遇到问题可先运行 `v2ray fix-all` 尝试自动修复配置。
- 更多详细文档和反馈请访问：
  - [GitHub Issues](https://github.com/233boy/v2ray/issues)
  - [官方文档](https://233boy.com/v2ray/v2ray-script/)
