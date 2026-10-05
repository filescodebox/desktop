# FilesCodeBox Desktop

[![Tag](https://img.shields.io/github/v/tag/filescodebox/desktop)](https://github.com/filescodebox/desktop/tags)
[![License](https://img.shields.io/github/license/filescodebox/desktop)](LICENSE)

FilesCodeBox 文件快递柜桌面客户端（Tauri 2）。托盘常驻，一键连接你的文件快递柜服务器；内置 p2pc，支持设备间 P2P 直传。

> 🗂️ [FilesCodeBox 生态](https://github.com/orgs/filescodebox)成员仓 · 总览见 [装配仓 filescodebox](https://github.com/filescodebox/filescodebox)

## 下载

三平台安装包(Windows / macOS / Linux)统一发布在 [hub 仓 Releases](https://github.com/filescodebox/filescodebox/releases)(`desktop-v*` 资产);打 `desktop-v*` tag 后 CI 自动构建并回挂。

## 功能（v1 远程模式）

- 服务器地址持久化，启动自动重连
- 系统托盘：显示主窗 / 服务器设置 / 退出；左键单击托盘唤回主窗
- 连接后主窗即服务器完整 Web UI（分享/取件/管理后台全功能）

### 设备直传（v1.3+，内置 p2pc sidecar）

设置页「设备直传」面板：选文件发送 → 出 `XXXX-XXXX-XXXX` 口令；对端输口令 → 直连取走，文件落系统下载目录。

- 传输走 PAKE 口令认证 + UDP 打洞直连（失败自动回落加密中继），**服务端只见密文，文件不落服务器**——只需一个可达的 [p2pd 注册中心](https://github.com/filescodebox/p2p)（联邦部署见 chart `p2p.enabled` 或 `docker run`）
- p2pc 以 Tauri sidecar 内嵌（CI 按 target triple 从 [p2p Releases](https://github.com/filescodebox/p2p/releases) 拉取 `p2pc-<triple>`），与 p2p 版本列车解耦
- **传输协议 v2（desktop v1.3.1 起，p2pc 0.4+）与旧版互不兼容**：双端须升级到同版本，旧版互传首帧直接失败

## Roadmap

- [ ] 本机模式：内嵌 server 二进制（sidecar），一键把电脑变成文件柜
- [ ] 直传多文件/目录、进度条与速度显示
- [ ] 开机自启、消息通知原生集成

## 开发

```bash
# 本地构建前需准备 sidecar(二进制不入库):
mkdir -p src-tauri/binaries
# 方式一: 从 p2p Releases 下载当前平台 triple
gh release download --repo filescodebox/p2p --pattern "p2pc-aarch64-apple-darwin*" --dir src-tauri/binaries
# 方式二: 从本地 p2p 仓源码编译
(cd ../FilesCodeBox/p2p && GOOS=darwin GOARCH=arm64 CGO_ENABLED=0 go build -o ../../desktop/src-tauri/binaries/p2pc-aarch64-apple-darwin ./cmd/p2pc)

cargo build          # 编译检查
# 打包三平台安装包：push desktop-v* tag，CI（GitHub Actions）自动构建并发 Release
```

## License

Apache-2.0
