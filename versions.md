# HarmonyOS 各版本变更详细记录（API 20 ~ API 24）

本文档记录从 HarmonyOS 6.0.0 (API 20) 到 6.1.0 (API 24) 每个版本的详细变更。

---

## API 20 — HarmonyOS 6.0.0（2025.05 开发者预览）

### ArkTS 12 语言变更

| 变更项 | 类型 | 说明 |
|--------|------|------|
| 跨包联合类型/字面量类型派生 | 新增 | 子模块导出联合类型后，父模块可直接派生使用 |
| 可调用对象的函数重载 | 新增 | interface 中定义 callable 对象支持重载 |
| 标准库共享模块 | 新增 | @ohos.arkts.shared 提供跨模块共享 |
| 标准容器构造函数类型检查 | 新增 | Array、Map、Set 等构造时的类型检查增强 |
| import/export 增强 | 新增 | 更灵活的类型导入和 re-export |
| 独立 ArkTS 语言规范文档 | 新增 | 从鸿蒙文档中分离为独立文档 |

### 编译器 & 运行时

- 编译器优化：更严格的类型检查
- 运行时性能提升
- hvigor 升级到 **2.6.0**
- ETS 格式升级为 **Stage 10**（Stage 9 已移除）

### ArkWeb

- 内核升级至 **Chromium 132**
- 支持自动播放静音视频
- 支持拦截 alert/confirm 弹窗
- Web 内容可见性优化

### 组件变更

| 组件 | 变更 | 说明 |
|------|------|------|
| ScrollBar | **移除** | 使用 Scroll 的 .scrollBar() 属性 |
| Popup | 增强 | 弹出菜单位置自适应、长按菜单 |
| TextPicker | 增强 | 副选项样式设置 |
| Menu | 增强 | 适配性提升 |
| Video/AVPlayer | 增强 | 支持流媒体/本地视频内嵌图片专辑封面 |

### 网络 & 安全

- DNS over HTTPS URL 生成
- HTTPS DNS 请求支持自定义 Header
- 系统 URI 可信度判断 API

### 数据管理

- UDMF（统一数据管理框架）增强
- 关系型数据库 RDB 增强
- 分布式 KV 增强
- 偏好型数据库 preferences 增强

### 其他

- 传感器 capability 字段增强
- @kit.ArkUI 核心 UI 能力增强
- DevEco Studio 支持 UI/卡片可视化编辑器、交互式 Inspector

---

## API 21 — HarmonyOS 6.0.1（2025.07 Beta1）

### 主要变更

| 类别 | 变更 | 说明 |
|------|------|------|
| 分布式 | 分布式数据管理增强 | 跨设备数据同步性能优化 |
| 安全 | 安全子系统优化 | 权限管理、数据加密能力增强 |
| 网络 | 网络管理增强 | 连接管理、网络策略优化 |
| 媒体 | 图片编解码优化 | HEIF/HEIC 支持增强 |
| 无障碍 | 无障碍能力增强 | 屏幕阅读器支持优化 |

### 稳定性 & 性能

- 系统稳定性修复
- 内存管理优化
- 后台任务调度优化

---

## API 22 — HarmonyOS 6.0.2（2025.09 Beta2）

### 主要变更

| 类别 | 变更 | 说明 |
|------|------|------|
| AI | AI 能力增强 | 端侧推理、模型管理 API 增强 |
| 设备 | 设备管理 API 扩展 | 外设管理、设备状态查询增强 |
| 图形 | 图形渲染优化 | 2D/3D 渲染管线优化 |
| 音频 | 音频管理增强 | 音频路由、焦点管理优化 |
| 安全 | 应用签名验证增强 | 签名校验流程优化 |

### ArkTS 运行时

- 闭包性能优化
- 垃圾回收（GC）效率提升
- 内存占用降低

---

## API 23 — HarmonyOS 6.0.3（2026.01 Release）

### 主要变更

| 类别 | 变更 | 说明 |
|------|------|------|
| 媒体 | 媒体编解码优化 | H.264/H.265 编码效率提升 |
| 窗口 | 窗口管理增强 | 多窗口、画中画能力增强 |
| 动画 | 动画系统优化 | 帧率稳定性提升 |
| 输入 | 输入法框架优化 | 键盘输入响应优化 |
| 国际化 | 本地化能力增强 | RTL 布局基础支持 |

### ArkTS 运行时

- 运行时性能进一步优化
- JIT 编译优化
- 类型推断增强

---

## API 24 — HarmonyOS 6.1.0（2026.05 Beta1）⭐ 最新

### ArkTS 13 语言变更

| 变更项 | 类型 | 说明 |
|--------|------|------|
| 闭包捕获可变变量 | **新增** | 允许闭包捕获 let/var 声明的可变变量 |
| 大语言子集增强 | 新增 | 更接近标准 TypeScript 的语言特性 |
| 类型推断改进 | 增强 | 减少显式类型标注需求 |
| 泛型约束增强 | 增强 | 更灵活的泛型使用方式 |

### ArkUI 引擎

| 特性 | 类型 | 说明 |
|------|------|------|
| 帧预测技术 | **新增** | 提前 1~2 帧预测渲染负载，降低掉帧率 |
| GPU 路径优化 | 增强 | 渲染管线优化，提升绘制性能 |
| 2D 图形引擎 | 增强 | 支持更丰富的绘图操作 |
| 交互模板系统 | **新增** | 系统级交互模板 |

### 交互模板

| 模板 | 说明 |
|------|------|
| 左右分栏视图 | Split View 模式，支持左右独立滚动 |
| 嵌套列表独立滚动 | List-in-List 独立滚动与外层解耦 |
| 自定义布局拖拽 | 支持任意布局中的拖拽操作 |
| 组件拖拽增强 | Navigation/Menu/TextInput/TextArea/RichEditor 支持拖拽 |

### 组件变更

| 组件 | 变更 | 说明 |
|------|------|------|
| Navigation | 增强 | 自定义标题栏（titleBuilder）、自定义菜单 |
| List | 增强 | 嵌套列表独立滚动、nestedScroll 配置 |
| TextInput | 增强 | 自定义数据后端支持 |
| TextArea | 增强 | 自定义数据后端支持 |
| RichEditor | 增强 | 更丰富样式定制、拖拽支持 |

### 新增 Kit

| Kit | 说明 |
|-----|------|
| IME Kit | 输入法开发框架，支持第三方输入法开发 |
| USB Kit | USB 设备访问：设备枚举、描述符查询、数据传输 |
| Capture Manager | 截屏/录屏管理，帧级捕获回调 |

### 媒体能力

| 能力 | 说明 |
|------|------|
| HEVC 编解码 | H.265 视频编码和解码支持 |
| EAC3 音频 | 杜比数字+音频格式支持 |
| 帧级字幕控制 | Video 组件支持字幕轨道选择、字号/颜色/背景设置 |

### 网络 & 通信

| 能力 | 说明 |
|------|------|
| 自定义协议栈 | 支持蓝牙、WiFi、USB、NFC、TCP/UDP 自定义网络协议 |
| 蓝牙协议栈自定义 | 自定义 BLE Profile 和数据处理 |
| WiFi 直连增强 | P2P 连接和数据传输优化 |

### 系统架构

| 变更 | 说明 |
|------|------|
| 单架构统一 | 手机/平板/PC 统一系统架构，一套二进制运行在所有设备 |
| Cangjie 语言支持 | 闭包捕获可变变量、与 ArkTS 13 互补 |

### 国际化

| 能力 | 说明 |
|------|------|
| 一键国际化 | 工具链支持一键生成国际化资源 |
| 阿拉伯语 RTL | 原生从右到左布局支持 |
| 本地化资源管理 | 更完善的多语言资源管理 |

### 数据管理

| 能力 | 说明 |
|------|------|
| UDMF 增强 | 统一数据管理框架能力扩展 |
| RDB 增强 | 关系型数据库性能优化 |
| KV 增强 | 分布式 KV 存储能力扩展 |

### 窗口 & 显示

| 能力 | 说明 |
|------|------|
| 窗口显示交互 | 多窗口管理能力增强 |
| WindowScene | API 24 支持 WindowScene 组件嵌入应用页面 |

### 性能 & 工具

| 能力 | 说明 |
|------|------|
| 性能优化 | 综合性能优化 |
| 功耗管理 | 应用功耗监控和优化工具 |
| DevEco Studio 6.1 | 预览器交互式预览、检查器增强、Profiler 性能分析增强、LSP 改进 |
| hvigor 2.7.0 | 构建工具升级 |

### API 24 关键接口

```typescript
// mediaquery 2.0
mediaquery.setAppWindowMinWidth('800vp');

// USB 设备访问
usb.getDevices();
usb.getRawDescriptor(device);
usb.openDevice(device);
usb.bulkTransfer(pipe, data, timeout);

// Capture Manager
capture.getCaptureManager();
manager.on('frameAvailable', callback);

// IME Kit
import { ime } from '@kit.IMEKit';

// 自定义协议栈
customProtocol.createBluetoothStack({ profile: 'custom', mtu: 512 });
```

---

## 版本迁移速查

### API 20 → API 21
- 分布式数据同步 API 微调
- 安全权限声明需更新
- 无需代码变更即可兼容

### API 21 → API 22
- AI 相关 API 有新增
- 设备管理 API 扩展
- 向后兼容

### API 22 → API 23
- 媒体 API 小幅调整
- 窗口管理 API 新增
- 向后兼容

### API 23 → API 24（重大版本升级）
- ArkTS 13 新特性需要 API 24 才能使用
- mediaquery 2.0 接口仅 API 24 可用
- 新增 Kit（IME/USB/Capture）仅 API 24
- 单架构：build-profile.json5 中 compatibleSdkVersion 改为 `6.1.0(24)`
- hvigor 升级到 2.7.0
- DevEco Studio 升级到 6.1

---

## 参考资料

- [HarmonyOS 版本概览](https://developer.huawei.com/consumer/cn/doc/harmonyos-releases/overview-allversion)
- [ArkUI-X 开源项目](https://gitee.com/arkui-x)
- [视觉特效：双边缘流光](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-visual-effect-double-edge-streamer)
- HDC 2026 大会（2026.05.22 发布 HarmonyOS 6.1 / API 24）
- [ArkTS 语言演进文章（华为语言团队博客）](https://developer.huawei.com/consumer/cn/blog/topic/02603379012094487)
