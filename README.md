# YCLuran

Windows 上的 Minecraft 启动器，v1.0。重点是界面与动效：窗口固定 900×550，页面切换、按钮反馈、下载状态都按同一套节奏设计。

> 状态：v1.0 已发布，唯一发布物是单文件 `release/YCLuran-Launcher.exe`，数据放在 exe 旁的 `data/`。

## 它能做什么

- 原版 26.3（Java 25）和 1.21.8（Java 21）启动到主菜单，也能安装 1.20.1、1.12.2、1.7.10 等版本
- Java 运行时自动检测；缺失时下载 Mojang Runtime
- 多线程下载中心：分段、断点续传、SHA1 校验、源竞速、限速、自定义 URL，下载源 BMCLAPI + Mojang
- 离线账户与 LittleSkin 登录（authlib-injector）
- Fabric 与 NeoForge 安装，Modrinth 模组浏览与下载
- 每个版本独立目录，实例隔离
- 浅色 / 深色 / 跟随系统三种外观；主题工作室可切换 A/B/C 三套主题

v1.0 没有做 Forge（引擎代码保留，界面标 1.1）、CurseForge、微软登录和整合包。这些入口在界面里保留，标记为「敬请期待」。

## 界面与动效

窗口固定 900×550 逻辑像素，不可缩放，没有最大化按钮。这是产品选择：每一页都是稳定的构图，动效的距离和时长也能围绕同一套坐标设计。

四个标志动效是启动画面（粒子汇聚成 Y）、首页视差背景、版本列表 FLIP 切换和下载中心状态动效。按钮按下有压缩回弹，启动中会走 spinner、逐点省略号和扫光。动画由启动器内的「动效」设置控制，不跟随系统的 `prefers-reduced-motion`；只有选「精简」或「关闭」才会收起粒子、视差和启动动画。

完整的设计说明在 `docs/V1.0-UI-MOTION-REPORT.md`。

## 技术栈

Tauri 2.12 · React 19.3 · TypeScript 6 · Vite 8 · Tailwind CSS 4 · Motion 14 · Zustand 5 · React Router 8；Rust edition 2024、tokio、reqwest（rustls）、sha1/sha2、serde、zip、tracing。包管理 pnpm 11。

## 开发

```bash
pnpm install
pnpm dev            # 前端开发（Vite 1420）
pnpm tauri dev      # 桌面开发
pnpm build          # 前端构建
pnpm typecheck
cd src-tauri; cargo check
```

打包用 `pnpm tauri build`。发布物只有 `YCLuran-Launcher.exe`，Tauri bundle 已关闭。

## 数据

- 发布形态：单文件 exe，数据在 exe 旁 `data/`
- 开发构建：`%APPDATA%\YCLuran`
- 目录：`instances/`、`versions/`、`assets/`、`libraries/`、`java/`、`logs/`、`cache/`
- 配置原子写，带 `schemaVersion`；密钥只进 Windows 凭据管理器

## 文档

- 项目约定：`AGENTS.md`
- 进度与坑：`MEMORY.md`
- 决策与来源：`docs/DECISIONS.md`
- 界面与动效：`docs/V1.0-UI-MOTION-REPORT.md`
- 宣传片：`promo-film/`

## 声明

个人 / 小圈子项目，与 Mojang、Microsoft 无关联。不使用 Mojang 版权素材；下载源遵循 BMCLAPI 的署名与协议要求。
