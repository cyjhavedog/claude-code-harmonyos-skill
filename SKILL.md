---
name: harmonyos-dev
version: 3.0.0
description: "HarmonyOS (鸿蒙) development skill. Supports API 20 (6.0) through API 24 (6.1). Triggers: ANY mention of 'HarmonyOS', '鸿蒙', 'ArkTS', 'ArkUI', 'OpenHarmony', 'OHOS', 'Stage model', 'UIAbility', '多端部署', '华为', 'HDC', 'ohpm', 'hvigor', 'HarmonyOS Next', '原子化服务', '元服务', '一次开发多端部署'. Use this skill for: creating HarmonyOS apps, ArkTS code, UI components, responsive multi-device layouts, Kit API usage, debugging HarmonyOS build/deploy issues. Covers ArkTS 12/13 syntax, Stage model architecture, UI components, multi-device responsive layout (mediaquery 2.0 breakpoints, GridRow/GridCol, SideBarContainer), system Kit APIs (@kit.ArkUI, @kit.ArkData, @kit.SensorServiceKit, @kit.NetworkKit, IME Kit, etc.), and build/deploy workflows."
allowed-tools: Bash, Read, Write, Edit, Glob, Grep
keywords: 鸿蒙,HarmonyOS,ArkTS,ArkUI,UI,组件,布局,多端部署,平板,手机,2in1,Kit,API,ohpm,hvigor,Stage,Ability,响应式,grid,mediaquery,资源限定符,断点,栅格,侧边栏,API24,ArkTS13,6.1,IME Kit,USB,单架构
---

# HarmonyOS Development Skill v3.0

鸿蒙应用开发完整指南（API 20 ~ API 24）：ArkTS 12/13 语法、Stage 模型、多端响应式布局、系统 Kit API、各设备适配策略。

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

---

## 1. 版本兼容矩阵（API 20 ~ API 24）

| 版本 | API Level | 发布时间 | ArkTS | hvigor | ETS Stage | 状态 |
|------|-----------|----------|-------|--------|-----------|------|
| HarmonyOS 6.0.0 | API 20 | 2025.05 (Dev Preview) | ArkTS 12 | 2.6.0 | Stage 10 | 已发布 |
| HarmonyOS 6.0.1 | API 21 | 2025.07 (Beta1) | ArkTS 12 | 2.6.x | Stage 10 | 已发布 |
| HarmonyOS 6.0.2 | API 22 | 2025.09 (Beta2) | ArkTS 12 | 2.6.x | Stage 10 | 已发布 |
| HarmonyOS 6.0.3 | API 23 | 2026.01 (Release) | ArkTS 12 | 2.6.x | Stage 10 | 已发布 |
| HarmonyOS 6.1.0 | API 24 | 2026.05 (Beta1) | ArkTS 13 | 2.7.0 | Stage 10 | **最新** |

> ⚠️ **从 API 20 起，Stage 9 ETS 格式已被移除，统一使用 Stage 10 格式。**

### build-profile.json5 配置示例

```json5
{
  "apiType": "stageModel",
  "targets": [
    {
      "name": "default",
      "runtimeOS": "HarmonyOS",
      "buildOption": { "strictMode": { "caseSensitiveCheck": true } }
    }
  ],
  "products": [
    {
      "name": "default",
      "compatibleSdkVersion": "6.0.0(20)",    // 按目标版本调整
      "targetSdkVersion": "6.0.0(20)",
      "runtimeOS": "HarmonyOS"
    }
  ]
}
```

---

## 2. ArkTS 语法参考（v12/v13）

### 2.1 装饰器 & 状态管理

| 装饰器 | 作用域 | 说明 |
|--------|--------|------|
| `@Entry` | 页面 | 标记页面根组件 |
| `@Component` | 结构体 | 声明可复用组件 |
| `@State` | 组件 | 内部状态，变化触发重渲染 |
| `@Prop` | 组件 | 父→子单向数据绑定 |
| `@Link` | 组件 | 父↔子双向数据绑定 |
| `@Provide/@Consume` | 跨组件 | 祖先→后代数据共享 |
| `@Observed/@ObjectLink` | 类 | 类对象属性变化监听 |
| `@Builder` | 函数 | 可复用 UI 构建器（返回 void） |
| `@Styles` | 函数 | 可复用样式集合 |
| `@Extend` | 函数 | 扩展组件样式 |
| `@Watch` | 属性 | 状态变化回调 |

### 2.2 ArkTS 12 新增特性（API 20+）

```typescript
// 1. 跨包联合类型/字面量类型派生
// 子模块导出联合类型
export type Status = 'loading' | 'success' | 'error';
export type Result<T> = { success: true; data: T } | { success: false; error: string };

// 父模块可直接派生使用，无需重新声明
import { Status, Result } from 'libmodule';
@State currentStatus: Status = 'loading';

// 2. 可调用对象的函数重载
interface Formatter {
  (value: number): string;
  (value: string): string;
}

// 3. import/export 体系增强
// 支持更灵活的类型导入和 re-export
export type { MyInterface } from './types';
export { myFunction } from './utils';

// 4. 标准库共享模块
// @ohos.arkts.shared 提供跨模块共享能力
import { shared } from '@ohos.arkts.shared';
```

### 2.3 ArkTS 13 新增特性（API 24+）

```typescript
// 1. 闭包中可变变量捕获（重大改进）
// ArkTS 12: 闭包不能捕获 let/var 变量
// ArkTS 13: 允许闭包捕获可变变量
function createCounter(): () => number {
  let count = 0;       // 可变变量
  return () => {        // ArkTS 13 允许捕获
    count++;
    return count;
  };
}
const counter = createCounter();
counter(); // 1
counter(); // 2

// 2. 闭包在 UI 组件中捕获可变状态
@Entry
@Component
struct CounterDemo {
  @State count: number = 0;

  build() {
    Column() {
      Text(`Count: ${this.count}`)
      Button('+1')
        .onClick(() => {
          // ArkTS 13: 闭包可直接捕获并修改外部可变变量
          let increment = 1;
          this.count += increment;  // 在 ArkTS 12 中有限制
        })
    }
  }
}

// 3. 大语言子集增强（部分特性依赖 Cangjie 后端）
// 注意：以下为 ArkTS 13 与 Cangjie 共享的高级特性
// - 函数式编程增强
// - 类型推断改进
// - 更灵活的泛型约束
```

### 2.4 @Builder 使用规范

```typescript
@Builder
SensorCard(icon: string, label: string, value: string, unit: string) {
  Column() {
    Row() {
      Text(icon).fontSize(24)
      Text(label).fontSize(13).fontColor('#999').margin({ left: 6 })
    }.width('100%')
    Text(value).fontSize(32).fontWeight(FontWeight.Bold)
    Text(unit).fontSize(16)
  }.padding(14).borderRadius(12).backgroundColor(Color.White)
}

// ⚠️ @Builder 返回 void，必须包裹在容器中使用
Column() {
  this.SensorCard('🌡', '温度', this.temperature, '°C')
}.layoutWeight(1).margin({ right: 8 })
```

### 2.5 @Styles 模式

```typescript
@Styles function primaryButton() {
  .height(44).fontSize(16).fontWeight(FontWeight.Medium)
  .borderRadius(8).backgroundColor('#1A73E8')
}

Button('提交').primaryButton()
```

### 2.6 单位说明

| 单位 | 全称 | 说明 |
|------|------|------|
| `vp` | Virtual Pixel | 虚拟像素，自动适配 DPI，布局首选 |
| `fp` | Font Pixel | 字体像素，在 vp 基础上跟随系统字体大小 |
| `px` | Physical Pixel | 物理像素，尽量避免使用 |
| `lpx` | Logical Pixel | 逻辑像素，1lpx = 1/屏幕设计宽度 |

---

## 3. 项目结构 (Stage Model)

```
entry/src/main/
├── ets/
│   ├── entryability/EntryAbility.ets    # UIAbility 生命周期
│   ├── pages/Index.ets                  # 页面组件 (@Entry)
│   └── utils/                           # 工具模块
├── resources/
│   ├── base/                            # 默认资源（必须存在）
│   ├── phone/                           # 手机专用
│   ├── tablet/                          # 平板专用
│   ├── car/                             # 车机专用
│   ├── tv/                              # 智慧屏专用
│   ├── 2in1/                            # 2in1 专用
│   ├── wearable/                        # 穿戴设备专用
│   ├── dark/                            # 暗色模式
│   └── rawfile/                         # 原始文件
└── module.json5
```

---

## 4. UIAbility 生命周期

```typescript
import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
import { window } from '@kit.ArkUI';

export default class EntryAbility extends UIAbility {
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) { }
  onWindowStageCreate(windowStage: window.WindowStage) {
    windowStage.loadContent('pages/Index', (err) => {
      if (err.code) { return; }
    });
  }
  onForeground() { }
  onBackground() { }
  onWindowStageDestroy() { }
  onDestroy() { }
}
```

---

## 5. 断点系统 & 媒体查询

### 5.1 mediaquery 1.0（API 20）— 5 级断点

| 断点 | 宽度范围 (vp) | 典型设备 |
|------|---------------|----------|
| `xs` | 0 ≤ width < 320 | 小屏手机、穿戴设备 |
| `sm` | 320 ≤ width < 600 | 普通手机、折叠屏外屏 |
| `md` | 600 ≤ width < 840 | 折叠屏展开、小平板 |
| `lg` | 840 ≤ width < 1440 | 平板、2in1 设备 |
| `xl` | width ≥ 1440 | 大屏平板、智慧屏、车机 |

### 5.2 mediaquery 2.0（API 24）— 新增自定义断点

API 24 新增 `mediaquery.setAppWindowMinWidth` 接口，支持设置自定义应用窗口最小宽度断点：

```typescript
// API 24 新增：自定义断点设置
import { mediaquery } from '@kit.ArkUI';

// 设置自定义应用窗口最小宽度断点
mediaquery.setAppWindowMinWidth('800vp');

// 查询当前断点类型（API 24 新增枚举）
import { BreakpointType } from '@kit.ArkUI';
// BreakpointType.XS, BreakpointType.SM, BreakpointType.MD,
// BreakpointType.LG, BreakpointType.XL

// 新增 WindowScene 能力
// API 24 支持 WindowScene 组件直接嵌入到应用页面中
```

### 5.3 MediaQuery API

```typescript
import { mediaquery } from '@kit.ArkUI';

// 方式 1: 2 个参数（查询 + 回调）
let listener = mediaquery.matchMediaSync(
  '(600vp<=width<840vp)',
  (result: mediaquery.MediaQueryResult) => {
    if (result.matches) { this.currentBreakpoint = 'md' }
  }
);

// 方式 2: 1 个参数，通过 .on() 注册回调
let listener = mediaquery.matchMediaSync('(600vp<=width<840vp)')
listener.on('change', (result: mediaquery.MediaQueryResult) => {
  if (result.matches) { this.currentBreakpoint = 'md' }
})
```

### 5.4 支持的查询属性

| 属性 | 说明 | 示例 |
|------|------|------|
| `width` | 窗口宽度 | `(width>=600vp)` |
| `height` | 窗口高度 | `(height>=840vp)` |
| `aspect-ratio` | 宽高比 | `(aspect-ratio>=1.5)` |
| `orientation` | 设备方向 | `(orientation:landscape)` |
| `device-type` | 设备类型 | `(device-type:tablet)` |
| `screen-density` | 屏幕密度 | `(screen-density>=3)` |
| `dark-mode` | 暗色模式 | `(prefers-color-scheme:dark)` |

### 5.5 完整 5 断点监听模式

```typescript
@State currentBreakpoint: string = 'sm'
private listeners: mediaquery.MediaQueryListener[] = []

aboutToAppear() {
  const breakpoints = [
    { name: 'xs', condition: '(0vp<=width<320vp)' },
    { name: 'sm', condition: '(320vp<=width<600vp)' },
    { name: 'md', condition: '(600vp<=width<840vp)' },
    { name: 'lg', condition: '(840vp<=width<1440vp)' },
    { name: 'xl', condition: '(1440vp<=width)' }
  ];
  breakpoints.forEach(bp => {
    let listener = mediaquery.matchMediaSync(bp.condition);
    listener.on('change', (result: mediaquery.MediaQueryResult) => {
      if (result.matches) { this.currentBreakpoint = bp.name }
    });
    this.listeners.push(listener);
  });
}

aboutToDisappear() {
  this.listeners.forEach(l => l.off('change'));
}
```

---

## 6. GridRow / GridCol 响应式栅格

基于 12 列栅格系统。

### GridRow

```typescript
GridRow({
  columns: 12,
  gutter: { x: 12, y: 12 },
  breakpoints: {
    reference: BreakpointsReference.WindowSize,
    value: ['320vp', '600vp', '840vp', '1440vp']
  },
  direction: GridRowDirection.Row
}) { ... }
```

### GridCol

```typescript
GridCol({
  span: { xs: 12, sm: 12, md: 6, lg: 4, xl: 3 },
  offset: { xs: 0, sm: 0, md: 1, lg: 0 },
  order: 0
}) {
  Column() { /* 内容 */ }
}
```

### 响应式卡片网格示例

```typescript
GridRow({ columns: 12, gutter: { x: 16, y: 16 },
          breakpoints: { reference: BreakpointsReference.WindowSize,
            value: ['320vp', '600vp', '840vp', '1440vp'] } }) {
  GridCol({ span: { xs: 12, sm: 12, md: 6, lg: 4, xl: 3 } }) {
    Column() { Text('温度: 26.5°C').fontSize(24).fontWeight(FontWeight.Bold) }
      .width('100%').height(120).backgroundColor('#FFE0B2')
      .borderRadius(12).justifyContent(FlexAlign.Center)
  }
}
```

---

## 7. 自适应布局组件

### Flex 弹性布局

```typescript
Flex({ direction: FlexDirection.Row, wrap: FlexWrap.Wrap }) {
  Text('项目1').width(200).height(80).backgroundColor('#FFCDD2')
  Text('项目2').layoutWeight(1).height(80).backgroundColor('#C8E6C9')
  Text('项目3').width(150).height(80).backgroundColor('#BBDEFB')
}.width('100%')
```

### WaterFlow 瀑布流

```typescript
WaterFlow() {
  ForEach(this.dataList, (item: DataItem) => {
    FlowItem() {
      Column() {
        Image(item.image).width('100%').objectFit(ImageFit.Cover)
        Text(item.title).fontSize(14).padding(8)
      }.borderRadius(8).backgroundColor(Color.White)
    }
  })
}
.columnsTemplate('1fr 1fr')
.columnsGap(12)
.rowsGap(12)
```

### Navigation 自适应导航

```typescript
Navigation(this.pageStack) { /* 内容区 */ }
  .title('标题')
  .mode(NavigationMode.Auto)  // 自动选择 Stack/Split
```

---

## 8. SideBarContainer 分栏布局

```typescript
SideBarContainer(SideBarContainerType.Embed) {
  Column() {
    List() {
      ListItem() { Text('菜单项1').fontSize(16).padding(16) }
    }
  }.width('100%').backgroundColor('#F5F5F5')
  Column() { Text('主内容').fontSize(20) }.width('100%')
}
.showSideBar(true)
.sideBarWidth(240)
.minSideBarWidth(200)
.maxSideBarWidth(400)
.showControlButton(true)
.autoHide(true)
```

---

## 9. 窗口管理 API

```typescript
import { window } from '@kit.ArkUI';

let win = await window.getLastWindow(this.context)
let props = await win.getWindowProperties()

// 监听窗口尺寸变化
win.on('windowSizeChange', (windowSize: window.Size) => { })

// 全屏
win.setWindowLayoutFullScreen(true)

// 状态栏属性
win.setWindowSystemBarProperties({
  statusBarColor: '#000000',
  statusBarContentColor: '#FFFFFF'
})
```

---

## 10. 核心 UI 组件

### Text / TextInput / TextArea

```typescript
Text('你好鸿蒙').fontSize(16).fontColor('#333').fontWeight(FontWeight.Medium)

TextInput({ text: this.serverAddr, placeholder: 'broker.emqx.io' })
  .width('100%').height(40).fontSize(14)
  .onChange((value: string) => { this.serverAddr = value })

TextArea({ text: this.message, placeholder: '输入消息' })
  .width('100%').height(80).fontSize(14)
  .onChange((value: string) => { this.message = value })
```

### Button

```typescript
Button('连接服务器')
  .width('100%').height(44).fontSize(16)
  .fontWeight(FontWeight.Medium).borderRadius(8)
  .backgroundColor(this.isConnected ? '#FF4444' : '#1A73E8')
  .onClick(() => { this.toggleConnection() })
```

### List / ForEach

```typescript
List() {
  ForEach(this.messageLog, (log: string, index: number) => {
    ListItem() {
      Column() {
        Text(log).fontSize(12).fontColor('#666').width('100%')
        if (index < this.messageLog.length - 1) {
          Divider().strokeWidth(0.5).color('#EEE')
        }
      }
    }
  })
}
```

### Tabs（底部导航）

```typescript
Tabs({ barPosition: BarPosition.End }) {
  TabContent() { Column() { /* 首页 */ } }.tabBar('首页')
  TabContent() { Column() { /* 监控 */ } }.tabBar('监控')
  TabContent() { Column() { /* 设置 */ } }.tabBar('设置')
}
```

### Scroll

```typescript
Scroll() {
  Column() { /* 内容 */ }.padding(12)
}.scrollBar(BarState.Off).scrollable(ScrollDirection.Vertical)
```

---

## 11. 系统 Kit API

### @kit.ArkUI（UI 核心）

```typescript
import { mediaquery, promptAction, animateTo } from '@kit.ArkUI';

promptAction.showToast({ message: '已保存', duration: 2000 })

animateTo({ duration: 300, curve: Curve.EaseInOut }, () => {
  this.expanded = !this.expanded
})
```

### @kit.PerformanceAnalysisKit（日志）

```typescript
import { hilog } from '@kit.PerformanceAnalysisKit';
const DOMAIN = 0x0000;
hilog.info(DOMAIN, 'Tag', '消息: %{public}s', data)
```

### @kit.ArkData（数据持久化）

```typescript
import { preferences } from '@kit.ArkData';
let pref = await preferences.getPreferences(this.context, 'myStore')
await pref.put('key', 'value')
await pref.flush()
let val = await pref.get('key', 'default')
```

### @kit.SensorServiceKit

```typescript
import { sensor } from '@kit.SensorServiceKit';

sensor.on(sensor.SensorType.ACCELEROMETER, (data: sensor.AccelerometerResponse) => {
  hilog.info(0x0000, 'Sensor', `x:${data.x} y:${data.y} z:${data.z}`)
}, { interval: 200000000 })

sensor.off(sensor.SensorType.ACCELEROMETER)
```

### @kit.NetworkKit（HTTP / WebSocket）

```typescript
import { http, webSocket } from '@kit.NetworkKit';

let req = http.createHttp()
req.request('https://api.example.com/data', {
  method: http.RequestMethod.POST,
  header: { 'Content-Type': 'application/json' },
  extraData: JSON.stringify({ temp: 26.5 })
}).then((resp) => { let data = JSON.parse(resp.result as string) })

let ws = webSocket.createWebSocket()
ws.connect('wss://echo.websocket.org')
ws.on('open', () => { ws.send('hello') })
ws.on('message', (data: string) => { })
```

### @kit.AbilityKit（应用跳转）

```typescript
import { common, Want } from '@kit.AbilityKit';
this.context.startAbility({
  deviceId: '', bundleName: 'com.example.other', abilityName: 'EntryAbility'
} as Want)
```

### @kit.NotificationKit

```typescript
import { notificationManager } from '@kit.NotificationKit';
notificationManager.publish({
  id: 1,
  content: {
    notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
    normal: { title: '告警', text: '温度超过阈值' }
  }
})
```

---

## 12. API 24 专属新特性

### 12.1 ArkUI 引擎增强

**帧预测技术：**
- 提前 1~2 帧预测渲染负载，降低掉帧率
- GPU 渲染路径优化，2D 图形引擎支持更丰富的绘图操作

**交互模板系统（API 24 新增）：**
```
支持的交互模板：
├── 左右分栏视图（Split View）
├── 嵌套列表独立滚动（List-in-List）
├── 自定义布局拖拽支持
└── Navigation/Menu/TextInput/TextArea/RichEditor 拖拽
```

**Navigation 组件增强：**
```typescript
// API 24 新增：自定义标题栏
Navigation() {
  NavDestination() { /* 内容 */ }
}
.titleBuilder(() => {
  Row() {
    Text('自定义标题').fontSize(18)
    Button('操作')
  }
})
// API 24 新增：自定义菜单
.menuOptions([
  { value: 'settings', icon: $r('app.media.icon_settings') },
  { value: 'help', icon: $r('app.media.icon_help') }
])
```

### 12.2 组件增强（API 24）

**List 组件 - 嵌套列表独立滚动：**
```typescript
// API 24: List 支持嵌套场景下独立滚动，与外层解耦
List() {
  ListItem() {
    List() {  // 嵌套内层 List 可独立滚动
      ForEach(this.subItems, (item: string) => {
        ListItem() { Text(item) }
      })
    }.nestedScroll({
      scrollForward: NestedScrollMode.SELF_FIRST,
      scrollBackward: NestedScrollMode.PARENT_FIRST
    })
  }
}
```

**TextInput / TextArea - 自定义数据后端：**
```typescript
// API 24 新增：自定义数据后端（编辑框可接入自定义输入源）
TextInput()
  .customDataBackend((data: string) => {
    // 自定义数据处理逻辑
    return processedData;
  })
```

**RichEditor 组件增强：**
- 更丰富的样式定制能力
- 支持拖拽操作（API 24 新增）

### 12.3 媒体能力（API 24）

```typescript
// HEVC（H.265）视频编解码支持
import { media } from '@kit.MediaKit';
// 创建 HEVC 编码器
let encoder = await media.createVideoEncoderByMime('video/hevc');

// EAC3 音频格式支持
// 支持蓝光/高清视频中的杜比数字+音频

// Video 组件帧级字幕控制
Video({ src: this.videoSrc })
  .subtitleTrack(1)           // API 24: 选择字幕轨道
  .subtitleFontsize(16)       // API 24: 字幕字号
  .subtitleFontcolor(Color.White)  // API 24: 字幕颜色
  .subtitleBackground('#80000000') // API 24: 字幕背景
```

### 12.4 USB 设备访问（API 24 新增）

```typescript
// API 24 新增：USB 设备访问 API
import { usb } from '@kit.USBKit';

// 获取 USB 设备列表
let devices = usb.getDevices();

// 查询 USB 设备描述符
let descriptor = usb.getRawDescriptor(device);

// 打开 USB 设备并获取管道
let pipe = usb.openDevice(device);

// USB 数据传输
await usb.bulkTransfer(pipe, dataBuffer, timeout);

// 关闭 USB 设备
usb.close(pipe);
```

### 12.5 Capture Manager（API 24 新增）

```typescript
// API 24 新增：截屏捕获管理
import { capture } from '@kit.ArkUI';

// 获取截屏捕获管理器
let manager = capture.getCaptureManager();

// 注册帧捕获回调
manager.on('frameAvailable', (pixelMap: image.PixelMap) => {
  // 处理捕获到的帧数据
  this.capturedFrame = pixelMap;
});

// 停止捕获
manager.off('frameAvailable');
```

### 12.6 IME Kit（API 24 新增）

```typescript
// API 24 新增：输入法开发框架
import { ime } from '@kit.IMEKit';

// 输入法应用需在 module.json5 中声明
// "extensionAbilities": [
//   {
//     "name": "InputMethodExtension",
//     "type": "inputMethod",
//     "metadata": [
//       { "name": "ohos.extension.input_method", "resource": "$profile:input_method_config" }
//     ]
//   }
// ]

// 输入法服务接口
class MyInputMethod extends ime.InputMethodExtensionAbility {
  onCreate() { }
  onDestroy() { }
  onInputStart(inputClient: ime.InputClient) {
    // 接收输入客户端，处理文本输入
  }
}
```

### 12.7 自定义协议栈（API 24）

```typescript
// API 24 新增：自定义协议栈
// 支持蓝牙、WiFi、USB、NFC、TCP/UDP 自定义网络协议
// 适用于物联网设备通信、工业控制等场景

// 自定义蓝牙协议栈示例
import { customProtocol } from '@kit.NetworkKit';
let btStack = customProtocol.createBluetoothStack({
  profile: 'custom',
  mtu: 512
});
btStack.on('data', (data: ArrayBuffer) => { });
```

### 12.8 Cangjie 语言（API 24）

- 支持闭包中捕获可变变量（mutable variable capture）
- 与 ArkTS 13 互补，面向系统底层开发
- Cangjie 语言工程可在 API 24 工程中编译运行

### 12.9 单架构统一（API 24）

- 手机/平板/PC 统一系统架构
- 一套二进制运行在所有形态设备上
- 无需按设备类型分别编译

### 12.10 国际化增强（API 24）

- 一键国际化工具链
- 原生阿拉伯语 RTL（从右到左）布局支持
- 更完善的本地化资源管理

---

## 13. API 20 → API 24 变更 & 弃用

### 已弃用 / 移除的 API

| 版本 | 变更 | 说明 | 迁移方案 |
|------|------|------|----------|
| API 20 | Stage 9 ETS 格式移除 | 旧版 ets 格式不再支持 | 统一使用 Stage 10 格式 |
| API 20 | ScrollBar 组件移除 | 使用 Scroll 的 `.scrollBar()` 属性替代 | `Scroll().scrollBar(BarState.Auto)` |
| API 20 | XComponent.surfacePosition 移除 | 属性重命名 | 使用新的 surface 控制 API |
| API 20 | HTTP header 校验更严格 | 旧写法可能报错 | 确保 header 键值对格式正确 |
| API 24 | 部分 mediaquery 1.0 接口标记废弃 | 逐步迁移到 mediaquery 2.0 | 使用 `setAppWindowMinWidth` |

### 各版本新增 Kit API

| API Level | 新增 / 增强的 Kit |
|-----------|-------------------|
| API 20 | ArkTS 12 跨包类型、ArkWeb chromium 132、传感器增强 |
| API 21 | 分布式数据管理增强、安全子系统优化 |
| API 22 | AI 能力增强、设备管理 API 扩展 |
| API 23 | 媒体编解码优化、窗口管理增强 |
| API 24 | IME Kit、USB Kit、Capture Manager、自定义协议栈、Cangjie 支持 |

---

## 14. 各设备适配策略

### 手机 (Phone) — sm 断点

- 单栏布局，底部 Tabs 导航
- 触控区域 ≥ 48vp，基础字号 14fp

### 平板 (Tablet) — md/lg 断点

- 双栏/三栏布局，侧边栏 + 内容区
- 更大字号 16-18fp，支持键盘

### 折叠屏 (Foldable)

- 折叠态按手机布局，展开态按平板布局
- 监听窗口宽度动态切换

### 2in1 设备 — lg/xl 断点（API 24 统一架构）

```typescript
// API 24: 单架构下 2in1 设备适配更简单
// 无需区分编译目标，系统自动适配
Navigation() {
  NavDestination() { /* 内容 */ }
}
.mode(NavigationMode.Split)  // 2in1 默认 Split 模式
```

### 车机 (Car) — 横屏

- 大触控区域 ≥ 60vp，高对比度配色
- 简化交互，支持语音

### 智慧屏 (TV) — 超大屏

- 大字号 ≥ 24fp，焦点导航
- 大间距、大卡片，简化信息密度

### 设备适配对比

| 维度 | 手机 | 平板 | 折叠屏 | 2in1 | 车机 | 智慧屏 |
|------|------|------|--------|------|------|--------|
| 布局 | 单栏 | 双栏/三栏 | 动态 | 多栏/分栏 | 双栏 | 大卡片 |
| 导航 | 底部Tab | 侧边栏 | 动态 | 侧边栏 | 固定侧边 | 焦点导航 |
| 触控 | 48vp | 48vp | 48vp | 48vp | 60vp | 60vp |
| 字号 | 14fp | 16fp | 动态 | 16fp | 18fp | 24fp |

---

## 15. 资源限定符

### 目录结构

```
resources/
├── base/                 ← 默认资源（必须）
│   ├── element/
│   │   ├── color.json    ← 颜色
│   │   ├── float.json    ← 尺寸
│   │   └── string.json   ← 字符串
│   └── media/
│       └── icon.png      ← 图片
├── phone/  ├── tablet/  ├── car/  ├── tv/  ├── 2in1/  ├── wearable/
├── dark/                 ← 暗色模式
└── rawfile/              ← 原始文件（不参与限定符匹配）
```

### 限定符优先级

```
最精确 → 最宽泛:
zh_CN + tablet + hdpi + dark  →  tablet + hdpi + dark
→  tablet + dark  →  tablet  →  base（兜底）
```

---

## 16. 构建 & 部署工具

```bash
# 构建（API 24 使用 hvigor 2.7.0，其余使用 2.6.x）
hvigorw assembleHap --mode debug

# 安装
hdc install entry-default-unsigned.hap

# 启动
hdc shell aa start -a EntryAbility -b com.example.app

# 日志
hdc shell hilog | grep "Tag"
```

### DevEco Studio 对应版本

| HarmonyOS 版本 | DevEco Studio 版本 |
|----------------|-------------------|
| 6.0 (API 20~23) | DevEco Studio 6.0 |
| 6.1 (API 24) | DevEco Studio 6.1 |

**DevEco Studio 6.1 新增能力：**
- 预览器（Previewer）支持交互式预览
- 检查器（Inspector）增强：实时布局检查
- 分析器（Profiler）性能分析增强
- LSP 语言服务器改进：更准确的代码补全和诊断

---

## 17. 关键规则 & 常见陷阱

1. **@Builder 返回 void** — 必须用 Column/Row 包裹后才能使用 layoutWeight/margin
2. **ForEach 需要稳定标识** — 提供 getter 函数作为第 3 个参数
3. **@State 类对象属性变更** — 需用 @Observed/@ObjectLink
4. **Scroll 子 Column** — 不要设 `.height('100%')`，用内容自适应
5. **Tabs barPosition** — 用 `BarPosition.End` 放底部导航
6. **断点注册/销毁配对** — aboutToAppear 注册，aboutToDisappear 调用 off
7. **资源目录** — 必须有 `base/` 兜底
8. **vp/fp 单位** — 始终用虚拟像素和字体像素，避免 px
9. **GridRow span 总和** — 同一行不超过 columns 数
10. **SideBarContainer** — 小屏用 `autoHide(true)` + `Overlay` 模式
11. **API 20+ 移除 Stage 9** — 所有新项目必须用 Stage 10
12. **API 24 闭包捕获** — 仅在 ArkTS 13 / API 24 中可用，向下不兼容
13. **API 24 单架构** — 手机/平板/PC 统一二进制，module.json5 中 deviceTypes 配置简化

---

## 18. 常用导入

```typescript
import { mediaquery, promptAction, animateTo, window } from '@kit.ArkUI';
import { deviceInfo } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
import { sensor } from '@kit.SensorServiceKit';
import { http, webSocket } from '@kit.NetworkKit';
import { preferences } from '@kit.ArkData';
import { common, Want, AbilityConstant } from '@kit.AbilityKit';

// API 24 新增
import { usb } from '@kit.USBKit';
import { ime } from '@kit.IMEKit';
import { capture } from '@kit.ArkUI';
```

---

## 附录: 断点 & 资源速查

```
断点:
xs  │ 0 ─── 320 │ 小屏手机/穿戴
sm  │ 320 ── 600 │ 普通手机
md  │ 600 ── 840 │ 折叠屏/小平板
lg  │ 840 ─ 1440 │ 平板/2in1
xl  │ 1440 ──∞   │ 大屏/智慧屏/车机

资源目录:
base/     ← 默认（必须）    phone/    ← 手机
tablet/   ← 平板           car/      ← 车机
tv/       ← 智慧屏         2in1/     ← 2in1
wearable/ ← 穿戴           dark/     ← 暗色模式

API 版本:
API 20 │ HarmonyOS 6.0.0 │ ArkTS 12 │ 2025.05
API 21 │ HarmonyOS 6.0.1 │ ArkTS 12 │ 2025.07
API 22 │ HarmonyOS 6.0.2 │ ArkTS 12 │ 2025.09
API 23 │ HarmonyOS 6.0.3 │ ArkTS 12 │ 2026.01
API 24 │ HarmonyOS 6.1.0 │ ArkTS 13 │ 2026.05
```
