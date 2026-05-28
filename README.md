# harmonyos-dev — Claude Code 鸿蒙开发 Skill

[English](#english) | 中文

一个用于 Claude Code 的 HarmonyOS (鸿蒙) 应用开发 Skill，覆盖 ArkTS 12/13 语法、Stage 模型、多端响应式布局、系统 Kit API、构建部署等全流程开发能力。

---

## 支持版本

| HarmonyOS 版本 | API Level | ArkTS 版本 | ETS 格式 | 状态 |
|----------------|-----------|-----------|----------|------|
| 6.0.0 | API 20 | ArkTS 12 | Stage 10 | 已支持 |
| 6.0.1 | API 21 | ArkTS 12 | Stage 10 | 已支持 |
| 6.0.2 | API 22 | ArkTS 12 | Stage 10 | 已支持 |
| 6.0.3 | API 23 | ArkTS 12 | Stage 10 | 已支持 |
| 6.1.0 | API 24 | ArkTS 13 | Stage 10 | **最新** |

> **注意：** 从 API 20 起，Stage 9 ETS 格式已被移除，统一使用 Stage 10 格式。

## 核心功能

- **ArkTS 语法参考** — 装饰器、状态管理、@Builder/@Styles、ArkTS 12 新增特性（跨包类型派生）、ArkTS 13 新增特性（闭包捕获可变变量）
- **多端响应式布局** — 5 级断点系统（xs/sm/md/lg/xl）、mediaquery 2.0 自定义断点、GridRow/GridCol 12 列栅格、SideBarContainer 分栏布局
- **系统 Kit API** — ArkUI、传感器（SensorServiceKit）、网络（NetworkKit）、数据持久化（ArkData）、通知、后台任务等
- **API 24 专属** — IME Kit、USB Kit、Capture Manager、自定义协议栈、HEVC/EAC3 媒体支持、单架构统一
- **设备适配** — 手机、平板、折叠屏、2in1、车机、智慧屏全设备适配策略
- **构建部署** — hvigor 构建、hdc 安装部署、DevEco Studio 工具链

## 文件结构

```
harmonyos-dev/
├── README.md              # 项目说明（本文件）
├── LICENSE                 # 开源许可证
├── SKILL.md                # 主 Skill 定义（API 20~24 完整指南）
└── versions.md             # 各版本详细变更记录（API 20→24）
```

## 安装方法

将本仓库克隆或下载到 Claude Code 的 Skill 目录：

```bash
# 克隆到 Skill 目录
git clone https://github.com/cyjhavedog/claude-code-harmonyos-skill.git ~/.claude/skills/harmonyos-dev

# 或手动复制
cp -r harmonyos-dev/ ~/.claude/skills/harmonyos-dev/
```

安装后重启 Claude Code 即可使用。

## 快捷命令

| 命令 | 说明 |
|------|------|
| `/harmonyos-dev syntax` | ArkTS 语法速查表（含 v12/v13 差异） |
| `/harmonyos-dev layout <设备类型>` | 响应式布局模板（phone/tablet/car/tv/2in1） |
| `/harmonyos-dev kit <kit名>` | Kit API 使用示例 |
| `/harmonyos-dev breakpoints` | 断点系统 & 媒体查询（含 mediaquery 2.0） |
| `/harmonyos-dev grid` | GridRow/GridCol 栅格布局详解 |
| `/harmonyos-dev resource` | 资源限定符完整指南 |
| `/harmonyos-dev sidebar` | SideBarContainer 分栏布局 |
| `/harmonyos-dev versions` | 各版本差异速查表（API 20→24） |
| `/harmonyos-dev migrate <from> <to>` | 版本迁移指南 |

## 使用示例

在 Claude Code 中直接描述鸿蒙开发需求即可触发 Skill：

```
帮我创建一个鸿蒙应用，使用 ArkTS 12 语法，
需要适配手机和平板，使用 mediaquery 断点系统做响应式布局。
```

```
我想了解 API 24 新增了哪些 Kit API
```

```
帮我写一个 Navigation 组件的多端适配页面，手机用 Stack 模式，平板用 Split 模式
```

## 技术参考

- [HarmonyOS 版本概览](https://developer.huawei.com/consumer/cn/doc/harmonyos-releases/overview-allversion)
- [ArkUI-X 开源项目](https://gitee.com/arkui-x)
- [HarmonyOS 开发者文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides)
- [HarmonyOS API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references)
- HDC 2026 大会（2026.05.22 发布 HarmonyOS 6.1 / API 24）

## 许可证

本项目基于 [MIT License](LICENSE) 开源，欢迎自由使用、修改和分发。

---

<a id="english"></a>

# harmonyos-dev — Claude Code HarmonyOS Development Skill

A Claude Code skill for HarmonyOS application development, covering ArkTS 12/13 syntax, Stage model, multi-device responsive layout, system Kit APIs, and build/deploy workflows.

## Supported Versions

| HarmonyOS | API Level | ArkTS | Status |
|-----------|-----------|-------|--------|
| 6.0.0 | API 20 | 12 | Supported |
| 6.0.1 | API 21 | 12 | Supported |
| 6.0.2 | API 22 | 12 | Supported |
| 6.0.3 | API 23 | 12 | Supported |
| 6.1.0 | API 24 | 13 | **Latest** |

## Install

```bash
git clone https://github.com/cyjhavedog/claude-code-harmonyos-skill.git ~/.claude/skills/harmonyos-dev
```

## Quick Commands

| Command | Description |
|---------|-------------|
| `/harmonyos-dev syntax` | ArkTS syntax reference |
| `/harmonyos-dev layout <device>` | Responsive layout templates |
| `/harmonyos-dev kit <kitname>` | Kit API examples |
| `/harmonyos-dev breakpoints` | Breakpoint system & media query |
| `/harmonyos-dev grid` | GridRow/GridCol grid layout |
| `/harmonyos-dev resource` | Resource qualifier guide |
| `/harmonyos-dev sidebar` | SideBarContainer layout |
| `/harmonyos-dev versions` | Version differences (API 20→24) |
| `/harmonyos-dev migrate <from> <to>` | Migration guide |

## License

[MIT License](LICENSE)
