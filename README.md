<p align="center"><img src="assets/covers/19-file-transfer-go.jpg" alt="文件快传 项目封面" width="100%"></p>

<h1 align="center">文件快传 · P2P File Transfer</h1>

<p align="center">基于 WebRTC 的点对点传输，六位取件码即传即用，服务器不存文件</p>

<p align="center">
  <a href="https://transfer.52python.cn/">在线体验</a> ·
  <a href="https://transfer.52python.cn/help">帮助文档</a>
</p>

## 简介

本仓库是 [MatrixSeven/file-transfer-go](https://github.com/MatrixSeven/file-transfer-go) 的 Fork，保留上游完整实现。文件在收发双方之间直连传输，中途不经过服务器存储；发件方选文件生成六位码，收件方输入码即开始接收，适合临时把大文件从 A 机挪到 B 机。

## 功能

- **文件传输**：多文件同时传，大文件支持断点续传
- **文字传输**：一段文本也能生成取件码发给对方
- **桌面共享**：共享屏幕，对方输入码观看
- **目录同步**：现代浏览器下可整目录同步
- **端到端加密**：WebRTC DataChannel 直连，服务器不落盘
- **连接状态同步**：双方界面实时显示连接与进度
- **单文件部署**：Linux / macOS / Windows 均可单文件跑起来
- **响应式**：手机、平板、桌面自适应

## 技术栈

**前端** Next.js 15 · React 18 · TypeScript 5 · Tailwind CSS 3.4 · Radix UI · Zustand · Lucide
**后端** Go 1.22 · WebSocket 信令 · 内存存储 · 标准库 HTTP 服务
**传输** WebRTC DataChannel · P2P 直连 · ICE · STUN / TURN

## 快速部署

**Docker（推荐）**

```bash
git clone https://github.com/MatrixSeven/file-transfer-go.git
cd file-transfer-go
docker-compose up -d

# 或直接用镜像
docker run -d -p 8080:8080 --name file-transfer-go matrixseven/file-transfer-go:latest
```

支持 `linux/amd64` 与 `linux/arm64` 多架构镜像，标签有 `latest`、`v1.0.x`、`dev`。

**本地构建**

```bash
git clone https://github.com/MatrixSeven/file-transfer-go.git
cd file-transfer-go
./build-fullstack.sh
./dist/file-transfer-go      # 访问 http://localhost:8080
```

**开发环境**

```bash
make dev                      # 后端
cd chuan-next && yarn && yarn dev   # 前端
```

环境变量：`NODE_ENV`、`PORT`（默认 8080）、`GO_BACKEND_URL`。

## 使用

1. **发文件**：选文件 → 生成取件码 → 把六位码发给对方
2. **发文字**：输入内容 → 生成取件码 → 分享
3. **共享桌面**：点共享 → 生成取件码 → 对方输入即可观看

## 架构

```
发送方 ←── WebSocket 信令 ──→ 服务器 ←── WebSocket 信令 ──→ 接收方
   └──────────── WebRTC P2P 直连传输 ────────────┘
```

## 许可证

上游为 MIT License，本 Fork 沿用同一许可。
