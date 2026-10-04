# FilesCodeBox Desktop

FilesCodeBox 文件快递柜桌面客户端（Tauri 2）。托盘常驻，一键连接你的文件快递柜服务器。

## 功能（v1 远程模式）

- 服务器地址持久化，启动自动重连
- 系统托盘：显示主窗 / 服务器设置 / 退出；左键单击托盘唤回主窗
- 连接后主窗即服务器完整 Web UI（分享/取件/管理后台全功能）

## Roadmap

- [ ] 本机模式：内嵌 server 二进制（sidecar），一键把电脑变成文件柜
- [ ] 开机自启、消息通知原生集成

## 开发

```bash
cargo build          # 编译检查
# 打包三平台安装包：push desktop-v* tag，CI（GitHub Actions）自动构建并发 Release
```

## License

Apache-2.0
