# Flutter组件简介

**User:** Anonymous  
**Created:** 8/30/2026 11:31:03  
**Updated:** 8/30/2026 11:32:49  
**Exported:** 8/30/2026 11:35:43  
**Link:** [https://chatgpt.com/c/6a93a3c2-dff8-83ea-a8b3-c0736338935d](https://chatgpt.com/c/6a93a3c2-dff8-83ea-a8b3-c0736338935d)  

## Prompt:
2026/8/30 11:31:02

Flutter当中,所有widget组件简介与其适用场景?

## Response:
2026/8/30 11:31:03

可以。Flutter 的 Widget 数量很多，但**没必要死记所有 Widget**。更实用的方式是按照「布局、显示、交互、滚动、容器、导航、状态、动画」分类，知道**什么时候该用哪个**。

下面给你一张比较完整的 Flutter Widget 选型地图。

---

# 一、先建立 Flutter Widget 全景图

可以把 Flutter 常用 Widget 理解成：

```text
Widget
│
├── 1. 基础显示
│   ├── Text
│   ├── Icon
│   ├── Image
│   ├── Placeholder
│   └── FlutterLogo
│
├── 2. 布局
│   ├── Row
│   ├── Column
│   ├── Stack
│   ├── Wrap
│   ├── Flex
│   ├── Expanded
│   ├── Flexible
│   ├── Spacer
│   ├── Center
│   ├── Align
│   └── Positioned
│
├── 3. 尺寸 / 间距
│   ├── SizedBox
│   ├── ConstrainedBox
│   ├── UnconstrainedBox
│   ├── FractionallySizedBox
│   └── AspectRatio
│
├── 4. 装饰 / 容器
│   ├── Container
│   ├── DecoratedBox
│   ├── Padding
│   ├── Card
│   ├── ClipRRect
│   ├── ClipOval
│   └── PhysicalModel
│
├── 5. 滚动
│   ├── SingleChildScrollView
│   ├── ListView
│   ├── GridView
│   ├── CustomScrollView
│   ├── PageView
│   └── NestedScrollView
│
├── 6. Sliver
│   ├── SliverAppBar
│   ├── SliverList
│   ├── SliverGrid
│   ├── SliverToBoxAdapter
│   ├── SliverPadding
│   ├── SliverFillRemaining
│   └── SliverPersistentHeader
│
├── 7. 输入
│   ├── TextField
│   ├── TextFormField
│   ├── Checkbox
│   ├── Radio
│   ├── Switch
│   ├── Slider
│   └── DropdownButton / DropdownMenu
│
├── 8. 按钮
│   ├── ElevatedButton
│   ├── FilledButton
│   ├── OutlinedButton
│   ├── TextButton
│   ├── IconButton
│   └── FloatingActionButton
│
├── 9. 导航
│   ├── Navigator
│   ├── Router
│   ├── AppBar
│   ├── BottomNavigationBar
│   ├── NavigationBar
│   ├── TabBar
│   └── Drawer
│
├── 10. 弹窗
│   ├── AlertDialog
│   ├── SimpleDialog
│   ├── Dialog
│   ├── BottomSheet
│   ├── SnackBar
│   └── showModalBottomSheet
│
├── 11. 动画
│   ├── AnimatedContainer
│   ├── AnimatedOpacity
│   ├── AnimatedAlign
│   ├── AnimatedPositioned
│   ├── Hero
│   ├── FadeTransition
│   ├── ScaleTransition
│   └── AnimationController
│
├── 12. 状态 / 生命周期
│   ├── StatelessWidget
│   ├── StatefulWidget
│   ├── InheritedWidget
│   ├── ValueListenableBuilder
│   └── FutureBuilder / StreamBuilder
│
└── 13. 高级 / 底层
    ├── CustomPaint
    ├── CustomSingleChildLayout
    ├── CustomMultiChildLayout
    ├── LayoutBuilder
    ├── MediaQuery
    ├── Builder
    └── RenderObject
```

下面重点讲**适用场景**。

---

# 二、基础显示 Widget

| Widget | 用途 | 典型场景 |
|---|---|---|
| `Text` | 显示文字 | 标题、正文、按钮文字 |
| `RichText` | 富文本 | 一段文字不同颜色/样式 |
| `TextSpan` | 富文本片段 | `RichText` 内部 |
| `Icon` | 图标 | 设置、返回、收藏 |
| `Image` | 图片 | 网络图、头像、Banner |
| `CircleAvatar` | 圆形头像 | 用户头像 |
| `Placeholder` | 占位 | 开发阶段占位 |

最常用：

```dart
Text('Hello')
Icon(Icons.home)
Image.network(url)
```

### `Text` vs `RichText`

普通文字：

```dart
Text('Hello Flutter')
```

一行里需要不同样式：

```text
你好，张三，欢迎回来
      ↑
      红色
```

使用：

```dart
RichText(
  text: TextSpan(
    children: [
      TextSpan(text: '你好，'),
      TextSpan(text: '张三'),
    ],
  ),
)
```

---

# 三、最重要的布局 Widget

这是 Flutter 最核心的一组。

## 1. Row

**横向排列**

```text
┌───────────────────────┐
│  Icon   Text   Button  │
└───────────────────────┘
```

```dart
Row(
  children: [
    Icon(Icons.home),
    Text('首页'),
  ],
)
```

### 适合

- 左右布局
- 图标 + 文字
- 多个按钮横向排列
- 商品信息横向布局

---

# 四、Column

**纵向排列**

```text
┌──────────────┐
│    Avatar    │
│              │
│     Name     │
│              │
│    Button    │
└──────────────┘
```

```dart
Column(
  children: [
    Avatar(),
    Text('张三'),
    Button(),
  ],
)
```

### 适合

- 表单
- 详情页
- 页面纵向布局
- 卡片内部布局

---

# 五、Stack

**层叠布局**

```text
┌─────────────────────┐
│     背景图片         │
│                     │
│       Avatar        │
│                     │
│             ❤️      │
└─────────────────────┘
```

```dart
Stack(
  children: [
    Image.asset('bg.png'),

    Positioned(
      right: 10,
      top: 10,
      child: Icon(Icons.favorite),
    ),
  ],
)
```

### 适合

- 图片上叠文字
- 图片上叠按钮
- Badge
- Floating Button
- Overlay
- 类似游戏 HUD 的布局

---

# 六、Wrap

`Row` 放不下时自动换行。

```text
┌─────────────────────┐
│ Flutter  Dart  AI   │
│ iOS   Android       │
└─────────────────────┘
```

```dart
Wrap(
  spacing: 8,
  runSpacing: 8,
  children: tags,
)
```

### 非常适合

- 标签
- 搜索关键词
- Chip
- 多个按钮
- 流式布局

---

# 七、Flex

`Row` 和 `Column` 的底层抽象。

```dart
Flex(
  direction: Axis.horizontal,
  children: [],
)
```

实际上：

```text
Row
 ↓
Flex(horizontal)

Column
 ↓
Flex(vertical)
```

所以：

> **Row / Column = Flex 的两个常用特化版本**

---

# 八、Expanded / Flexible / Spacer

这几个非常重要。

## Expanded

**占满剩余空间**

```dart
Row(
  children: [
    Text('左边'),

    Expanded(
      child: Text('占满剩余空间'),
    ),

    Text('右边'),
  ],
)
```

可以理解成：

```text
固定       剩余空间       固定
│            │             │
Text      Expanded        Text
```

---

## Flexible

允许占用剩余空间，但**不强制撑满**。

```dart
Flexible(
  child: Text('很长很长很长的文字'),
)
```

### 简单区分

```text
Expanded
    ↓
必须尽可能填满

Flexible
    ↓
可以填，也可以不填
```

---

## Spacer

专门用来撑开间距：

```dart
Row(
  children: [
    Text('左'),
    Spacer(),
    Text('右'),
  ],
)
```

结果：

```text
左 ─────────────── 右
```

---

# 九、Center / Align

## Center

居中：

```dart
Center(
  child: Text('Hello'),
)
```

相当于常见的：

```text
水平居中 + 垂直居中
```

---

## Align

比 Center 更灵活。

```dart
Align(
  alignment: Alignment.topRight,
  child: Icon(...),
)
```

例如：

```text
┌──────────────────┐
│              ●   │
│                  │
│                  │
│                  │
└──────────────────┘
```

---

# 十、Positioned

**Stack 内部定位。**

```dart
Stack(
  children: [
    Positioned(
      left: 10,
      top: 20,
      child: Text('Hello'),
    ),
  ],
)
```

只应该重点记住：

> `Positioned` → `Stack` 的孩子定位

---

# 十一、尺寸控制 Widget

## SizedBox

最常用的尺寸/间距 Widget。

```dart
SizedBox(height: 20)
```

或者：

```dart
SizedBox(
  width: 100,
  height: 50,
  child: Button(),
)
```

### 适合

```text
固定尺寸
固定间距
占位
```

---

# 十二、ConstrainedBox

给 Widget 增加约束。

```dart
ConstrainedBox(
  constraints: BoxConstraints(
    minWidth: 100,
    maxWidth: 300,
  ),
  child: ...
)
```

适合：

> 我不想指定一个固定宽度，但希望它只能在某个范围内。

---

# 十三、AspectRatio

控制宽高比。

```dart
AspectRatio(
  aspectRatio: 16 / 9,
  child: Image(...),
)
```

非常适合：

```text
视频
Banner
封面
播放器
```

例如：

```text
16 : 9

┌──────────────────┐
│                  │
│      Video       │
│                  │
└──────────────────┘
```

---

# 十四、FractionallySizedBox

按照父组件比例设置大小。

```dart
FractionallySizedBox(
  widthFactor: 0.5,
  child: ...
)
```

意思：

```text
父宽度 × 50%
```

---

# 十五、Container

Flutter 最容易被滥用的 Widget 😂

它实际上是一个**组合型 Widget**。

```dart
Container(
  width: 100,
  height: 100,
  padding: EdgeInsets.all(10),
  margin: EdgeInsets.all(10),
  alignment: Alignment.center,
  decoration: BoxDecoration(
    color: Colors.blue,
    borderRadius: BorderRadius.circular(10),
  ),
  child: Text('Hello'),
)
```

可以理解：

```text
Container
    │
    ├── padding
    ├── margin
    ├── alignment
    ├── constraints
    ├── decoration
    └── child
```

但现在开发时：

> **不要什么都用 Container。**

例如单纯加间距：

```dart
SizedBox(height: 20)
```

而不是：

```dart
Container(height: 20)
```

---

# 十六、Padding

专门处理**内边距**。

```dart
Padding(
  padding: EdgeInsets.all(16),
  child: Text('Hello'),
)
```

---

# 十七、Card

Material 风格的卡片。

```dart
Card(
  child: ListTile(
    title: Text('商品'),
  ),
)
```

适合：

- 商品卡片
- 用户卡片
- 信息卡片
- 设置项

---

# 十八、DecoratedBox

专门做装饰。

```dart
DecoratedBox(
  decoration: BoxDecoration(
    color: Colors.red,
    borderRadius: BorderRadius.circular(10),
  ),
  child: ...
)
```

它比 `Container` 更纯粹。

可以理解：

```text
Container
    ≈
DecoratedBox + Padding + Alignment + Constraints...
```

---

# 十九、Clip 系列

控制**裁剪区域**。

| Widget | 用途 |
|---|---|
| `ClipRect` | 矩形裁剪 |
| `ClipRRect` | 圆角矩形 |
| `ClipOval` | 椭圆/圆形 |
| `ClipPath` | 自定义 Path 裁剪 |

例如头像：

```dart
ClipOval(
  child: Image.network(url),
)
```

---

# 二十、滚动 Widget

这是 Flutter 第二个非常重要的知识体系。

## SingleChildScrollView

**只有一个主要 child 的滚动。**

```dart
SingleChildScrollView(
  child: Column(
    children: [...],
  ),
)
```

适合：

```text
详情页
设置页
文章页
表单页
```

不适合特别大的列表。

---

# 二十一、ListView

**线性列表。**

```dart
ListView(
  children: [
    Item(),
    Item(),
    Item(),
  ],
)
```

大量数据：

```dart
ListView.builder(
  itemBuilder: ...,
)
```

适合：

```text
聊天列表
商品列表
评论列表
联系人
```

---

# 二十二、GridView

网格。

```text
┌────┬────┬────┐
│    │    │    │
├────┼────┼────┤
│    │    │    │
├────┼────┼────┤
│    │    │    │
└────┴────┴────┘
```

```dart
GridView.builder(...)
```

适合：

- 商品
- 相册
- 图标选择器
- 九宫格

---

# 二十三、PageView

一页一页滑动。

```text
┌───────────────┐
│     Page 1    │
└───────────────┘
       ← →
┌───────────────┐
│     Page 2    │
└───────────────┘
```

适合：

- Banner
- 引导页
- 图片浏览器
- 首页分页

---

# 二十四、CustomScrollView

这个你之前问过 Sliver，所以这里特别重要。

它是：

> **多个 Sliver 组合成一个滚动区域。**

例如：

```text
CustomScrollView
│
├── SliverAppBar
├── SliverToBoxAdapter
├── SliverList
├── SliverGrid
└── SliverPadding
```

适合：

> **复杂滚动页面**

例如：

```text
       AppBar
    ↕ 吸顶/折叠

   Banner

┌─────────────────┐
│ Tab             │
├─────────────────┤
│ 商品             │
│ 商品             │
│ 商品             │
└─────────────────┘
```

---

# 二十五、Sliver 系列

你可以先记住一个核心：

```text
Box Widget
    ↓
普通布局

Sliver Widget
    ↓
滚动区域里的布局
```

常见：

| Widget | 用途 |
|---|---|
| `SliverList` | 列表 |
| `SliverGrid` | 网格 |
| `SliverAppBar` | 可折叠 AppBar |
| `SliverToBoxAdapter` | 把普通 Widget 放进 Sliver |
| `SliverPadding` | Sliver Padding |
| `SliverFillRemaining` | 填充剩余空间 |
| `SliverPersistentHeader` | 吸顶 Header |

---

# 二十六、输入 Widget

| Widget | 用途 |
|---|---|
| `TextField` | 文本输入 |
| `TextFormField` | 表单输入 |
| `Checkbox` | 多选 |
| `Radio` | 单选 |
| `Switch` | 开关 |
| `Slider` | 滑动选择 |
| `DropdownMenu` | 下拉选择 |
| `DatePicker` | 日期选择 |
| `TimePicker` | 时间选择 |

---

# 二十七、TextField vs TextFormField

这是经常遇到的选择。

### TextField

普通输入：

```dart
TextField()
```

### TextFormField

表单：

```dart
Form(
  child: TextFormField(
    validator: ...
  ),
)
```

所以：

```text
普通输入
    ↓
TextField

需要表单验证
    ↓
TextFormField
```

---

# 二十八、Button

现在常用：

| Widget | 场景 |
|---|---|
| `ElevatedButton` | 突出操作 |
| `FilledButton` | Material 主按钮 |
| `OutlinedButton` | 次要按钮 |
| `TextButton` | 低强调操作 |
| `IconButton` | 图标按钮 |
| `FloatingActionButton` | 悬浮主操作 |

大致可以理解：

```text
最强视觉
  ↑
FilledButton

OutlinedButton

TextButton
  ↓
最弱视觉
```

---

# 二十九、GestureDetector

**手势识别。**

```dart
GestureDetector(
  onTap: () {},
  onLongPress: () {},
  onDoubleTap: () {},
  child: ...
)
```

适合：

> Widget 本身没有点击能力，但你需要给它增加手势。

---

# 三十、InkWell

Material 点击反馈。

```dart
InkWell(
  onTap: () {},
  child: ...
)
```

和 `GestureDetector` 的核心区别：

```text
GestureDetector
    ↓
识别手势

InkWell
    ↓
Material 点击效果 + 手势
```

---

# 三十一、导航

## Navigator

页面栈：

```text
Page A
  ↓ push
Page B
  ↓ push
Page C
```

```dart
Navigator.push(...)
Navigator.pop(...)
```

---

## AppBar

页面顶部栏：

```text
┌────────────────────┐
│ ←    首页      ⋮   │
├────────────────────┤
│                    │
```

---

## BottomNavigationBar / NavigationBar

底部导航：

```text
┌────────────────────┐
│                    │
├────────────────────┤
│ 首页  消息  我的   │
└────────────────────┘
```

现在 Material 3 更推荐：

```dart
NavigationBar
```

---

## TabBar

顶部 Tab：

```text
推荐   热门   最新
────
```

通常配合：

```dart
TabBar
TabBarView
```

---

# 三十二、Drawer

侧边栏：

```text
┌────────────┐
│ 用户       │
│ 首页       │
│ 设置       │
│ 关于       │
│            │
│            │
└─────┬──────┘
      │
      ↓
   主页面
```

适合后台管理、设置菜单等。

---

# 三十三、弹窗

| Widget | 场景 |
|---|---|
| `AlertDialog` | 确认/警告 |
| `SimpleDialog` | 简单选择 |
| `Dialog` | 自定义弹窗 |
| `BottomSheet` | 底部面板 |
| `SnackBar` | 短消息 |
| `showDialog` | 显示 Dialog |
| `showModalBottomSheet` | 显示底部弹窗 |

---

# 三十四、FutureBuilder

异步任务完成后更新 UI。

```dart
FutureBuilder(
  future: loadData(),
  builder: (context, snapshot) {
    ...
  },
)
```

非常适合：

```text
加载接口
   ↓
loading
   ↓
success / error
```

---

# 三十五、StreamBuilder

监听持续的数据流。

```dart
StreamBuilder(
  stream: stream,
  builder: ...
)
```

适合：

```text
WebSocket
聊天消息
实时数据
数据库监听
```

核心区别：

```text
Future
  ↓
一次性结果

Stream
  ↓
持续产生结果
```

---

# 三十六、状态相关 Widget

## StatelessWidget

没有自己的可变 State。

```dart
class UserName extends StatelessWidget {
  ...
}
```

适合：

```text
纯 UI
展示组件
输入参数 → UI
```

---

## StatefulWidget

拥有 State。

```dart
class Counter extends StatefulWidget {
  ...
}
```

适合：

```text
需要局部状态
动画
输入状态
生命周期
```

---

# 三十七、InheritedWidget

这是 Flutter 状态传播体系的底层核心之一。

```text
       InheritedWidget
             │
       ┌─────┴─────┐
       ↓           ↓
     Child       Child
       ↓
    深层 Widget
```

作用：

> **让子树中的 Widget 能够共享数据。**

很多状态管理方案都建立在类似的依赖/通知思想上。

---

# 三十八、Builder 系列

## Builder

重新获得一个新的 `BuildContext`。

比较常见于：

```dart
Builder(
  builder: (context) {
    ...
  },
)
```

---

## LayoutBuilder

根据**父组件提供的约束**构建 UI。

```dart
LayoutBuilder(
  builder: (context, constraints) {
    if (constraints.maxWidth > 600) {
      return Desktop();
    }

    return Mobile();
  },
)
```

非常适合：

> **响应式布局**

---

# 三十九、MediaQuery

获取设备环境：

```dart
MediaQuery.of(context).size
```

可以获取：

```text
屏幕尺寸
屏幕方向
文字缩放
系统 padding
显示特征
```

---

# 四十、SafeArea

避免被：

```text
刘海
状态栏
Home Indicator
```

遮挡。

```dart
SafeArea(
  child: ...
)
```

页面开发非常常用。

---

# 四十一、动画 Widget

Flutter 动画可以先分两类：

```text
隐式动画
    ↓
AnimatedXXX

显式动画
    ↓
AnimationController
```

---

## AnimatedContainer

例如：

```text
宽度
100
 ↓
200
```

```dart
AnimatedContainer(
  duration: Duration(milliseconds: 300),
  width: width,
)
```

---

常见：

| Widget | 动画 |
|---|---|
| `AnimatedContainer` | Container 属性 |
| `AnimatedOpacity` | 透明度 |
| `AnimatedAlign` | 对齐 |
| `AnimatedPositioned` | Stack 位置 |
| `AnimatedPadding` | Padding |
| `AnimatedScale` | 缩放 |
| `AnimatedRotation` | 旋转 |

---

# 四十二、Hero

页面之间共享元素动画。

例如：

```text
商品列表

[ 商品图片 ]
     ↓ 点击

商品详情

[ 商品图片 ]
```

图片可以从列表位置飞到详情页。

---

# 四十三、CustomPaint

自定义绘制。

```dart
CustomPaint(
  painter: MyPainter(),
)
```

适合：

```text
折线图
雷达图
仪表盘
特殊图形
游戏绘制
复杂视觉效果
```

如果你的需求是：

> **“Flutter 没有现成 Widget，我自己画。”**

首先考虑 `CustomPaint`。

---

# 四十四、RenderObject

这是 Flutter Widget 体系更底层的东西。

你之前研究过 `RenderBox` / `RenderSliver`，可以把层次理解成：

```text
Widget
   ↓
Element
   ↓
RenderObject
   ↓
Layout
Painting
HitTest
```

普通开发：

```text
Widget
```

高级 UI：

```text
CustomPaint
```

需要完全控制布局：

```text
Custom RenderObject
```

所以：

> **不要一开始就写 RenderObject。**

只有当现有 Widget / CustomPaint / LayoutBuilder 等无法满足需求时，才往下走。

---

# 四十五、最后给你一个「选择决策表」

这是比背 Widget 更重要的东西。

| 我想做什么 | 优先考虑 |
|---|---|
| 显示文字 | `Text` |
| 显示图片 | `Image` |
| 横向排列 | `Row` |
| 纵向排列 | `Column` |
| 层叠 | `Stack` |
| 自动换行 | `Wrap` |
| 居中 | `Center` |
| 精确对齐 | `Align` |
| Stack 定位 | `Positioned` |
| 固定尺寸/间距 | `SizedBox` |
| 最大/最小尺寸 | `ConstrainedBox` |
| 宽高比 | `AspectRatio` |
| 内边距 | `Padding` |
| 背景/边框/圆角 | `DecoratedBox` / `Container` |
| 圆角裁剪 | `ClipRRect` |
| 普通页面滚动 | `SingleChildScrollView` |
| 长列表 | `ListView.builder` |
| 网格 | `GridView.builder` |
| 横向分页 | `PageView` |
| 复杂滚动 | `CustomScrollView` |
| Sliver 列表 | `SliverList` |
| Sliver 网格 | `SliverGrid` |
| 可折叠 AppBar | `SliverAppBar` |
| 普通输入 | `TextField` |
| 表单验证 | `TextFormField` |
| 点击 | `GestureDetector` / `InkWell` |
| 开关 | `Switch` |
| 单选 | `Radio` |
| 多选 | `Checkbox` |
| 按钮 | `FilledButton` 等 |
| 页面跳转 | `Navigator` |
| Tab | `TabBar` + `TabBarView` |
| 底部导航 | `NavigationBar` |
| 弹窗 | `showDialog` |
| 底部弹窗 | `showModalBottomSheet` |
| 消息提示 | `SnackBar` |
| Future 数据 | `FutureBuilder` |
| Stream 数据 | `StreamBuilder` |
| 响应式布局 | `LayoutBuilder` |
| 获取屏幕信息 | `MediaQuery` |
| 避开刘海 | `SafeArea` |
| 简单动画 | `AnimatedXXX` |
| 页面共享动画 | `Hero` |
| 自定义绘图 | `CustomPaint` |
| 自定义布局 | `CustomMultiChildLayout` |
| 极致自定义布局 | `RenderObject` |

---

# 四十六、真正应该掌握的是这棵「Widget 选择树」

以后遇到 UI，不要想着：

> “这个 Widget 我记不记得？”

而是问：

```text
我要做什么？
     │
     ├── 显示？
     │    ├── 文字 → Text
     │    ├── 图片 → Image
     │    └── 图标 → Icon
     │
     ├── 排列？
     │    ├── 横向 → Row
     │    ├── 纵向 → Column
     │    ├── 层叠 → Stack
     │    └── 自动换行 → Wrap
     │
     ├── 滚动？
     │    ├── 单个内容 → SingleChildScrollView
     │    ├── 列表 → ListView
     │    ├── 网格 → GridView
     │    └── 复杂滚动 → CustomScrollView
     │
     ├── 交互？
     │    ├── 点击 → InkWell / GestureDetector
     │    ├── 输入 → TextField
     │    ├── 开关 → Switch
     │    └── 选择 → Checkbox / Radio
     │
     ├── 弹出？
     │    ├── 对话框 → Dialog
     │    ├── 底部 → BottomSheet
     │    └── 提示 → SnackBar
     │
     ├── 动画？
     │    ├── 简单 → AnimatedXXX
     │    ├── 复杂 → AnimationController
     │    └── 页面共享 → Hero
     │
     └── 普通 Widget 搞不定？
          │
          ├── 自定义绘制 → CustomPaint
          │
          ├── 自定义布局 → CustomMultiChildLayout
          │
          └── 极致控制 → RenderObject
```

**如果你正在系统学 Flutter，我建议下一步不要继续背 Widget。** 更值得搞懂的是 Flutter 的 **「Widget → Element → RenderObject → RenderBox/RenderSliver → Layout → Paint → HitTest」整条链路**。

你之前已经问过 `RenderBox / RenderSliver / CustomScrollView / RenderObject`，把这条链真正串起来后，上面这些 Widget 基本就能做到**看到需求就知道应该选哪个，以及它底层为什么能工作**。

## Prompt:
2026/8/30 11:32:11

列一个完整表格

## Response:
2026/8/30 11:32:12

可以。下面我按 **Flutter 常用 + 核心 Widget 体系** 做成一张完整的速查表。严格来说 Flutter SDK 里的 Widget 数量非常多，而且不同 Flutter 版本会增加/废弃 Widget，所以这里重点覆盖**实际开发中需要掌握的 Widget**，并把底层/高级 Widget 也纳入。

## Flutter Widget 完整分类表

| 分类 | Widget | 核心作用 | 典型使用场景 | 使用频率 |
|---|---|---|---|---|
| **基础** | `Text` | 显示文本 | 标题、正文、标签 | ⭐⭐⭐⭐⭐ |
| | `RichText` | 富文本 | 一段文字多种样式 | ⭐⭐⭐ |
| | `Text.rich` | 快速创建富文本 | 富文本 | ⭐⭐⭐ |
| | `Icon` | 显示图标 | 操作图标、状态图标 | ⭐⭐⭐⭐⭐ |
| | `Image` | 显示图片 | 网络/本地图片 | ⭐⭐⭐⭐⭐ |
| | `Image.asset` | 本地图片 | App 图片资源 | ⭐⭐⭐⭐⭐ |
| | `Image.network` | 网络图片 | 用户头像、Banner | ⭐⭐⭐⭐⭐ |
| | `CircleAvatar` | 圆形头像 | 用户头像 | ⭐⭐⭐⭐ |
| | `Placeholder` | 占位 | 开发阶段 | ⭐ |
| | `FlutterLogo` | Flutter Logo | Demo/测试 | ⭐ |
| **布局** | `Row` | 横向布局 | 左右排列 | ⭐⭐⭐⭐⭐ |
| | `Column` | 纵向布局 | 上下排列 | ⭐⭐⭐⭐⭐ |
| | `Stack` | 层叠布局 | 图片叠文字、Badge | ⭐⭐⭐⭐⭐ |
| | `Wrap` | 自动换行布局 | Tag、Chip | ⭐⭐⭐⭐ |
| | `Flex` | Row/Column 的抽象 | 自定义横纵布局 | ⭐⭐⭐ |
| | `Expanded` | 填充剩余空间 | Row/Column 平分空间 | ⭐⭐⭐⭐⭐ |
| | `Flexible` | 灵活占用空间 | 防止溢出 | ⭐⭐⭐⭐ |
| | `Spacer` | 空间占位 | 左右顶开 | ⭐⭐⭐⭐ |
| | `Positioned` | Stack 内定位 | 右上角按钮 | ⭐⭐⭐⭐⭐ |
| | `PositionedDirectional` | RTL 方向定位 | 国际化布局 | ⭐⭐ |
| | `Center` | 居中 | 加载、空页面 | ⭐⭐⭐⭐⭐ |
| | `Align` | 指定位置对齐 | 左上/右下等 | ⭐⭐⭐⭐⭐ |
| | `Baseline` | 基线对齐 | 文字特殊排版 | ⭐⭐ |
| | `IndexedStack` | 保留多个页面状态，只显示一个 | Tab 页面 | ⭐⭐⭐ |
| | `Flow` | 自定义流式布局 | 特殊动画布局 | ⭐ |
| **尺寸** | `SizedBox` | 固定尺寸/间距 | 宽高、间距 | ⭐⭐⭐⭐⭐ |
| | `ConstrainedBox` | 添加尺寸约束 | 最大/最小尺寸 | ⭐⭐⭐ |
| | `UnconstrainedBox` | 移除部分约束 | 突破父约束 | ⭐⭐ |
| | `LimitedBox` | 限制最大尺寸 | 特殊约束场景 | ⭐ |
| | `FractionallySizedBox` | 按父尺寸比例 | 50% 宽度 | ⭐⭐⭐ |
| | `AspectRatio` | 控制宽高比 | 16:9 视频 | ⭐⭐⭐⭐ |
| | `FittedBox` | 缩放适配 | 防止内容溢出 | ⭐⭐⭐⭐ |
| | `OverflowBox` | 允许超出父约束 | 特殊 UI | ⭐ |
| **间距/装饰** | `Padding` | 内边距 | 内容留白 | ⭐⭐⭐⭐⭐ |
| | `Container` | 综合容器 | 背景、尺寸、Padding | ⭐⭐⭐⭐⭐ |
| | `DecoratedBox` | 装饰 | 背景、边框、圆角 | ⭐⭐⭐ |
| | `ColoredBox` | 设置背景颜色 | 简单背景 | ⭐⭐⭐ |
| | `Card` | Material 卡片 | 商品/信息卡片 | ⭐⭐⭐⭐ |
| | `PhysicalModel` | 物理模型/阴影 | 特殊视觉效果 | ⭐ |
| | `Material` | Material 表面 | Ink、阴影等 | ⭐⭐⭐ |
| **裁剪** | `ClipRect` | 矩形裁剪 | 裁剪内容 | ⭐⭐ |
| | `ClipRRect` | 圆角矩形裁剪 | 圆角图片 | ⭐⭐⭐⭐ |
| | `ClipOval` | 椭圆裁剪 | 圆形头像 | ⭐⭐⭐ |
| | `ClipPath` | Path 自定义裁剪 | 特殊形状 | ⭐⭐ |
| **列表/滚动** | `SingleChildScrollView` | 单个 Child 滚动 | 详情页、表单 | ⭐⭐⭐⭐⭐ |
| | `ListView` | 列表 | 普通列表 | ⭐⭐⭐⭐⭐ |
| | `ListView.builder` | 懒加载列表 | 大量数据 | ⭐⭐⭐⭐⭐ |
| | `ListView.separated` | 带分隔符列表 | 设置/商品列表 | ⭐⭐⭐⭐⭐ |
| | `ListView.custom` | 自定义列表 | 高级场景 | ⭐⭐ |
| | `GridView` | 网格 | 商品、相册 | ⭐⭐⭐⭐⭐ |
| | `GridView.builder` | 懒加载网格 | 大量商品 | ⭐⭐⭐⭐⭐ |
| | `GridView.count` | 固定列数网格 | 九宫格 | ⭐⭐⭐ |
| | `GridView.extent` | 固定最大宽度 | 响应式网格 | ⭐⭐⭐ |
| | `PageView` | 分页滚动 | Banner、引导页 | ⭐⭐⭐⭐ |
| | `NestedScrollView` | 嵌套滚动 | AppBar + Tab + List | ⭐⭐⭐⭐ |
| | `CustomScrollView` | 自定义 Sliver 滚动 | 复杂页面 | ⭐⭐⭐⭐⭐ |
| **Sliver** | `SliverAppBar` | 可折叠 AppBar | 吸顶/折叠 Header | ⭐⭐⭐⭐⭐ |
| | `SliverList` | Sliver 列表 | 大列表 | ⭐⭐⭐⭐⭐ |
| | `SliverFixedExtentList` | 固定高度列表 | 高性能列表 | ⭐⭐⭐ |
| | `SliverPrototypeExtentList` | 根据 Prototype 定高度 | 特殊列表 | ⭐ |
| | `SliverGrid` | Sliver 网格 | 复杂网格 | ⭐⭐⭐⭐ |
| | `SliverToBoxAdapter` | Box → Sliver | 普通 Widget 插入滚动 | ⭐⭐⭐⭐⭐ |
| | `SliverPadding` | Sliver Padding | 滚动区域边距 | ⭐⭐⭐ |
| | `SliverFillRemaining` | 填充剩余空间 | 空状态页面 | ⭐⭐⭐ |
| | `SliverFillViewport` | 每个 Sliver 填满 Viewport | 全屏分页 | ⭐⭐ |
| | `SliverPersistentHeader` | 持久 Header | 吸顶 Tab | ⭐⭐⭐⭐⭐ |
| | `SliverOpacity` | Sliver 透明度 | 滚动动画 | ⭐⭐ |
| | `SliverVisibility` | Sliver 显隐 | 动态内容 | ⭐⭐ |
| | `SliverIgnorePointer` | 忽略事件 | 特殊交互 | ⭐ |
| **按钮** | `ElevatedButton` | 凸起按钮 | 主操作 | ⭐⭐⭐⭐⭐ |
| | `FilledButton` | Material 3 主按钮 | 主操作 | ⭐⭐⭐⭐⭐ |
| | `OutlinedButton` | 描边按钮 | 次要操作 | ⭐⭐⭐⭐⭐ |
| | `TextButton` | 文字按钮 | 弱操作 | ⭐⭐⭐⭐⭐ |
| | `IconButton` | 图标按钮 | 返回、收藏 | ⭐⭐⭐⭐⭐ |
| | `FloatingActionButton` | 悬浮按钮 | 新建、添加 | ⭐⭐⭐⭐ |
| | `DropdownButton` | 下拉按钮 | 选择 | ⭐⭐⭐ |
| | `MenuAnchor` | Material 菜单 | 更多操作 | ⭐⭐⭐ |
| **输入** | `TextField` | 文本输入 | 搜索、账号密码 | ⭐⭐⭐⭐⭐ |
| | `TextFormField` | 表单输入 | 表单验证 | ⭐⭐⭐⭐⭐ |
| | `Form` | 表单管理 | 登录、注册 | ⭐⭐⭐⭐⭐ |
| | `FormField` | 自定义表单字段 | 自定义表单控件 | ⭐⭐⭐ |
| | `Checkbox` | 多选 | 同意协议 | ⭐⭐⭐⭐⭐ |
| | `CheckboxListTile` | 带文字的 Checkbox | 设置列表 | ⭐⭐⭐⭐ |
| | `Radio` | 单选 | 单项选择 | ⭐⭐⭐⭐ |
| | `RadioListTile` | 带文字 Radio | 设置/选项 | ⭐⭐⭐⭐ |
| | `Switch` | 开关 | 设置开关 | ⭐⭐⭐⭐⭐ |
| | `SwitchListTile` | 带文字 Switch | 设置页面 | ⭐⭐⭐⭐ |
| | `Slider` | 滑动选择 | 音量、进度 | ⭐⭐⭐ |
| | `RangeSlider` | 区间选择 | 价格范围 | ⭐⭐ |
| | `DropdownMenu` | 下拉菜单 | 选择城市等 | ⭐⭐⭐ |
| **手势** | `GestureDetector` | 手势识别 | 点击、拖动、长按 | ⭐⭐⭐⭐⭐ |
| | `InkWell` | Material 点击效果 | 卡片点击 | ⭐⭐⭐⭐⭐ |
| | `InkResponse` | Material 手势反馈 | 自定义点击区域 | ⭐⭐ |
| | `Listener` | 原始 Pointer 事件 | 底层触摸处理 | ⭐⭐⭐ |
| | `MouseRegion` | 鼠标事件 | Web/Desktop | ⭐⭐⭐ |
| | `AbsorbPointer` | 阻断事件 | 禁止点击 | ⭐⭐⭐ |
| | `IgnorePointer` | 忽略事件 | 穿透/忽略交互 | ⭐⭐⭐ |
| **导航** | `Navigator` | 页面栈导航 | push/pop | ⭐⭐⭐⭐⭐ |
| | `MaterialApp` | Material App 根组件 | App 入口 | ⭐⭐⭐⭐⭐ |
| | `CupertinoApp` | iOS 风格 App | Cupertino UI | ⭐⭐⭐ |
| | `Router` | 声明式路由 | 深链、复杂导航 | ⭐⭐⭐ |
| | `Navigator` 2.0 | 声明式导航体系 | 大型 App | ⭐⭐ |
| | `AppBar` | 顶部导航栏 | 页面标题 | ⭐⭐⭐⭐⭐ |
| | `BottomNavigationBar` | 底部导航 | 首页/消息/我的 | ⭐⭐⭐⭐ |
| | `NavigationBar` | Material 3 底部导航 | 首页/消息/我的 | ⭐⭐⭐⭐⭐ |
| | `NavigationRail` | 侧边导航 | 平板/桌面 | ⭐⭐⭐ |
| | `Drawer` | 左侧抽屉 | 菜单 | ⭐⭐⭐⭐ |
| | `NavigationDrawer` | Material 3 Drawer | 菜单 | ⭐⭐⭐ |
| | `TabBar` | Tab 导航 | 分类页 | ⭐⭐⭐⭐⭐ |
| | `TabBarView` | Tab 内容 | 分类内容 | ⭐⭐⭐⭐⭐ |
| | `DefaultTabController` | Tab Controller | 简单 Tab | ⭐⭐⭐⭐ |
| **弹窗** | `AlertDialog` | 确认弹窗 | 删除确认 | ⭐⭐⭐⭐⭐ |
| | `SimpleDialog` | 简单选择弹窗 | 选项选择 | ⭐⭐⭐ |
| | `Dialog` | 自定义 Dialog | 自定义弹窗 | ⭐⭐⭐⭐ |
| | `Dialog.fullscreen` | 全屏 Dialog | 全屏编辑 | ⭐⭐ |
| | `BottomSheet` | 底部面板 | 操作面板 | ⭐⭐⭐⭐ |
| | `showDialog` | 显示 Dialog | 确认框 | ⭐⭐⭐⭐⭐ |
| | `showModalBottomSheet` | Modal BottomSheet | 底部选择 | ⭐⭐⭐⭐⭐ |
| | `showBottomSheet` | Persistent BottomSheet | 页面内底部面板 | ⭐⭐ |
| | `SnackBar` | 短消息 | 操作结果 | ⭐⭐⭐⭐⭐ |
| | `showLicensePage` | License 页面 | 开源许可 | ⭐ |
| **布局辅助** | `SafeArea` | 避开系统区域 | 刘海、Home Indicator | ⭐⭐⭐⭐⭐ |
| | `MediaQuery` | 获取屏幕环境 | 屏幕尺寸 | ⭐⭐⭐⭐⭐ |
| | `LayoutBuilder` | 根据约束布局 | 响应式布局 | ⭐⭐⭐⭐⭐ |
| | `Builder` | 获取新的 Context | Context 问题 | ⭐⭐⭐ |
| | `OrientationBuilder` | 根据横竖屏布局 | 平板 | ⭐⭐ |
| | `Localizations` | 国际化 | 多语言 | ⭐⭐⭐ |
| **状态** | `StatelessWidget` | 无内部可变状态 | 纯 UI | ⭐⭐⭐⭐⭐ |
| | `StatefulWidget` | 有状态 Widget | 表单、动画 | ⭐⭐⭐⭐⭐ |
| | `State` | Stateful 状态对象 | 生命周期 | ⭐⭐⭐⭐⭐ |
| | `InheritedWidget` | 向下共享数据 | 状态传播 | ⭐⭐⭐ |
| | `InheritedNotifier` | Notifier + Inherited | 状态监听 | ⭐⭐ |
| | `InheritedModel` | 按维度依赖更新 | 高级状态优化 | ⭐ |
| **异步** | `FutureBuilder` | Future → UI | 网络请求 | ⭐⭐⭐⭐⭐ |
| | `StreamBuilder` | Stream → UI | 实时数据 | ⭐⭐⭐⭐⭐ |
| | `ValueListenableBuilder` | ValueListenable → UI | 局部状态 | ⭐⭐⭐⭐ |
| | `AnimatedBuilder` | Animation → UI | 动画 | ⭐⭐⭐⭐⭐ |
| | `ListenableBuilder` | Listenable → UI | 状态监听 | ⭐⭐⭐ |
| **动画** | `AnimatedContainer` | Container 属性动画 | 尺寸/颜色变化 | ⭐⭐⭐⭐⭐ |
| | `AnimatedOpacity` | 透明度动画 | 淡入淡出 | ⭐⭐⭐⭐⭐ |
| | `AnimatedAlign` | Alignment 动画 | 移动 | ⭐⭐⭐ |
| | `AnimatedPadding` | Padding 动画 | 间距变化 | ⭐⭐ |
| | `AnimatedPositioned` | Stack 位置动画 | 移动 | ⭐⭐⭐ |
| | `AnimatedScale` | 缩放 | 点击放大 | ⭐⭐⭐ |
| | `AnimatedRotation` | 旋转 | 图标旋转 | ⭐⭐⭐ |
| | `AnimatedDefaultTextStyle` | 文本样式动画 | 标题变化 | ⭐⭐ |
| | `FadeTransition` | Fade | 淡入淡出 | ⭐⭐⭐ |
| | `ScaleTransition` | Scale | 缩放 | ⭐⭐⭐ |
| | `RotationTransition` | Rotation | 旋转 | ⭐⭐⭐ |
| | `SlideTransition` | Slide | 滑入滑出 | ⭐⭐⭐⭐ |
| | `SizeTransition` | Size | 展开/收起 | ⭐⭐⭐ |
| | `PositionedTransition` | Position | 自定义移动 | ⭐⭐ |
| | `Hero` | 页面共享元素动画 | 图片详情 | ⭐⭐⭐⭐ |
| **绘制** | `CustomPaint` | 自定义绘制 | 图表、特殊 UI | ⭐⭐⭐⭐ |
| | `CustomPainter` | 自定义 Paint | Canvas 绘制 | ⭐⭐⭐⭐ |
| | `RepaintBoundary` | 独立绘制边界 | 性能优化 | ⭐⭐⭐ |
| **高级布局** | `CustomSingleChildLayout` | 自定义单 Child 布局 | 特殊布局 | ⭐ |
| | `CustomMultiChildLayout` | 自定义多 Child 布局 | 特殊布局 | ⭐⭐ |
| | `CustomMultiChildLayout` + `LayoutId` | 多 Child 精确布局 | 自定义布局 | ⭐ |
| | `IntrinsicWidth` | 根据内容计算宽度 | 特殊自适应 | ⭐⭐ |
| | `IntrinsicHeight` | 根据内容计算高度 | 特殊自适应 | ⭐⭐ |
| | `Baseline` | 基线布局 | 排版 | ⭐ |
| **底层** | `RenderObjectWidget` | RenderObject Widget 基类 | 自定义 RenderObject | ⭐ |
| | `SingleChildRenderObjectWidget` | 单 Child RenderObject | 自定义布局 | ⭐ |
| | `MultiChildRenderObjectWidget` | 多 Child RenderObject | 自定义布局 | ⭐ |
| | `LeafRenderObjectWidget` | 无 Child RenderObject | 自定义绘制 | ⭐ |
| | `RenderObject` | Flutter 渲染底层 | 极高级定制 | ⭐ |
| | `RenderBox` | Box 布局体系 | 普通 Widget 底层 | ⭐ |
| | `RenderSliver` | Sliver 布局体系 | 滚动底层 | ⭐ |
| **Material** | `Scaffold` | 页面骨架 | App 页面 | ⭐⭐⭐⭐⭐ |
| | `Material` | Material Surface | Material UI | ⭐⭐⭐ |
| | `Card` | 卡片 | 信息/商品 | ⭐⭐⭐⭐ |
| | `ListTile` | 标准列表项 | 设置/联系人 | ⭐⭐⭐⭐⭐ |
| | `ExpansionTile` | 可展开列表项 | FAQ/设置 | ⭐⭐⭐⭐ |
| | `Divider` | 分割线 | 列表分隔 | ⭐⭐⭐⭐⭐ |
| | `VerticalDivider` | 垂直分割线 | 横向布局 | ⭐⭐ |
| | `CircularProgressIndicator` | 圆形进度 | Loading | ⭐⭐⭐⭐⭐ |
| | `LinearProgressIndicator` | 线性进度 | 上传/下载 | ⭐⭐⭐⭐ |
| | `Tooltip` | 提示信息 | 图标说明 | ⭐⭐⭐ |
| | `Badge` | 角标 | 未读消息 | ⭐⭐⭐⭐ |
| | `Chip` | 标签 | 分类/Tag | ⭐⭐⭐⭐ |
| | `ChoiceChip` | 单选标签 | 筛选 | ⭐⭐⭐ |
| | `FilterChip` | 多选筛选标签 | 筛选 | ⭐⭐⭐ |
| | `ActionChip` | 操作标签 | 快捷操作 | ⭐⭐ |
| **Cupertino** | `CupertinoButton` | iOS 按钮 | iOS 风格 | ⭐⭐ |
| | `CupertinoNavigationBar` | iOS 导航栏 | iOS UI | ⭐⭐ |
| | `CupertinoTabBar` | iOS 底部 Tab | iOS UI | ⭐⭐ |
| | `CupertinoSwitch` | iOS 开关 | iOS UI | ⭐⭐ |
| | `CupertinoTextField` | iOS 输入框 | iOS UI | ⭐⭐ |
| | `CupertinoAlertDialog` | iOS 弹窗 | iOS UI | ⭐⭐ |
| | `CupertinoActionSheet` | iOS ActionSheet | iOS UI | ⭐⭐ |
| | `CupertinoActivityIndicator` | iOS Loading | iOS UI | ⭐⭐ |

---

# 重点：Widget 可以再压缩成 10 个体系

如果你不想背上面这么大的表，其实可以压缩成下面这张。

| 我遇到的问题 | 首选 Widget |
|---|---|
| **显示文字** | `Text` |
| **显示图片** | `Image` |
| **横向排列** | `Row` |
| **纵向排列** | `Column` |
| **重叠** | `Stack` |
| **自动换行** | `Wrap` |
| **控制空间** | `Expanded / Flexible / Spacer` |
| **控制尺寸** | `SizedBox / ConstrainedBox / AspectRatio` |
| **装饰** | `Container / DecoratedBox / Card` |
| **滚动** | `ListView / GridView / CustomScrollView` |
| **复杂滚动** | `SliverXXX` |
| **点击** | `InkWell / GestureDetector` |
| **输入** | `TextField / TextFormField` |
| **选择** | `Checkbox / Radio / Switch` |
| **按钮** | `FilledButton / OutlinedButton / TextButton` |
| **页面导航** | `Navigator` |
| **Tab** | `TabBar / TabBarView` |
| **底部导航** | `NavigationBar` |
| **弹窗** | `showDialog / showModalBottomSheet` |
| **异步** | `FutureBuilder / StreamBuilder` |
| **响应式布局** | `LayoutBuilder` |
| **屏幕信息** | `MediaQuery` |
| **安全区域** | `SafeArea` |
| **简单动画** | `AnimatedXXX` |
| **复杂动画** | `AnimationController` |
| **自定义绘制** | `CustomPaint` |
| **自定义布局** | `CustomMultiChildLayout` |
| **极致自定义** | `RenderObject` |

---

# 最重要的一张：Flutter 布局体系

你之前一直在研究 `RenderBox`、`RenderSliver`，那么可以把 Widget 和底层对应起来：

```text
                         Flutter Widget
                              │
            ┌─────────────────┴─────────────────┐
            │                                   │
         普通布局                              滚动布局
            │                                   │
         RenderBox                           RenderSliver
            │                                   │
    ┌───────┼────────┐                 ┌────────┼────────┐
    │       │        │                 │        │        │
   Row    Column   Stack          SliverList SliverGrid SliverAppBar
    │       │        │
    └───────┼────────┘
            │
       Box Constraints
            │
      ┌─────┴─────┐
      │           │
   Layout       Paint
      │           │
      └─────┬─────┘
            │
          HitTest
```

所以你可以把 Flutter Widget 学习路线理解为：

```text
第一层：会用
────────────────
Text
Image
Row
Column
Stack
Wrap
Container
ListView
GridView
Scaffold
AppBar
Button
TextField

第二层：理解布局
────────────────
Constraints
Row / Column
Expanded / Flexible
Stack / Positioned
Align
LayoutBuilder
MediaQuery

第三层：理解滚动
────────────────
ScrollView
Viewport
Sliver
RenderSliver
CustomScrollView
NestedScrollView

第四层：理解渲染
────────────────
Widget
 ↓
Element
 ↓
RenderObject
 ↓
RenderBox
 ↓
Layout
 ↓
Paint
 ↓
HitTest

第五层：自己造 Widget
────────────────
CustomPaint
 ↓
CustomMultiChildLayout
 ↓
RenderObject
```

**对于 Flutter 开发来说，真正值得彻底掌握的并不是 100 多个 Widget，而是 `Row / Column / Stack / Flex / Constraint / ListView / Sliver / Widget-Element-RenderObject` 这几个核心体系。** 掌握这些以后，大多数 Widget 都只是它们的不同组合。



---
Powered by [ChatGPT Exporter](https://www.chatgptexporter.com)