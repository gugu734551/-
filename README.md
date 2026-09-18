<div align="center">
  <img src="app_icon.jpg" width="120" alt="个人工作台图标">
  <h1>个人工作台</h1>
  <p>一款完全离线的 Android 个人资料管理应用，把笔记、图片、录音和文档收纳到同一个工作台。</p>

  ![Flutter](https://img.shields.io/badge/Flutter-3.47+-02569B?logo=flutter&logoColor=white)
  ![Dart](https://img.shields.io/badge/Dart-3.4+-0175C2?logo=dart&logoColor=white)
  ![Android](https://img.shields.io/badge/Android-6.0+-3DDC84?logo=android&logoColor=white)
  ![Offline](https://img.shields.io/badge/Data-100%25%20Offline-00695C)
</div>

## 项目简介

个人工作台是一款面向 Android 的本地资料管理工具。它提供笔记、图片、语音、文档四个独立模块，并通过分类和全局搜索把分散的个人资料组织起来。

应用无需注册账号，不依赖服务器，也不申请网络权限。笔记与索引保存在本地 SQLite 数据库中，导入的文件存放在应用私有目录内。

## 主要功能

| 模块 | 功能 |
| --- | --- |
| 工作台 | 四类资料快捷入口、数量统计、最近添加、全局搜索 |
| 笔记 | 新建、编辑、分类、查看和删除笔记 |
| 图片 | 从相册或文件选择器导入、网格浏览、大图缩放、分类管理 |
| 语音 | 录音、暂停/继续、命名归类、播放进度和删除 |
| 文档 | 导入 PDF、Word、Excel、PowerPoint、TXT；PDF 应用内预览 |
| 分类 | 各资料类型独立分类，支持新建、重命名和删除 |
| 搜索 | 按标题、正文或文件名搜索，结果按资料类型分组 |
| 本地存储 | SQLite 保存结构化数据，应用私有目录保存导入文件 |

## 特点

- 完全离线：不需要账号、服务器或网络权限。
- 统一管理：在一个应用中整理四类常用个人资料。
- 数据隔离：文件保存在 Android 应用私有目录中。
- 简洁架构：Provider 管理状态，DAO 层隔离数据库访问。
- Android 原生体验：使用系统相册和文件选择器导入资料。

## 技术栈

- Flutter / Dart
- Provider：状态管理
- sqflite：笔记、分类与文件索引
- path_provider：应用私有目录管理
- image_picker / file_picker：图片与文档导入
- record / just_audio：录音与音频播放
- pdfrx：PDF 应用内预览
- open_filex：调用系统应用打开 Office 等文件

## 环境要求

| 工具 | 建议版本 |
| --- | --- |
| Flutter | 3.47 或更高版本 |
| Dart | 3.4 或更高版本 |
| Android SDK | 以项目 Gradle 配置为准 |
| Android 设备 | Android 6.0（API 23）或更高版本 |

## 快速开始

### 1. 获取项目

```bash
git clone <你的仓库地址>
cd personal_workbench
```

### 2. 检查开发环境

```bash
flutter doctor
flutter doctor --android-licenses
```

### 3. 安装依赖并运行

```bash
flutter pub get
flutter devices
flutter run
```

### 4. 构建 APK

调试版本：

```bash
flutter build apk --debug
```

发布版本：

```bash
flutter build apk --release
```

构建产物位于：

```text
build/app/outputs/flutter-apk/
```

> 发布给其他用户前，请配置自己的 Android 签名。仓库不会提交 `key.properties`、keystore 或其他本机密钥文件。

## 项目结构

```text
personal_workbench/
├── android/                 # Android 平台配置与资源
├── assets/                  # 应用静态资源
├── lib/
│   ├── main.dart            # 应用入口与全局 Provider 注入
│   ├── constants.dart       # 类型、格式等全局常量
│   ├── models/              # 笔记、分类和资料模型
│   ├── pages/               # 首页及各功能页面
│   ├── providers/           # 状态管理
│   ├── services/            # 数据库、文件、录音、导入与打开服务
│   │   └── dao/             # 数据访问层
│   ├── utils/               # 格式化、查询与反馈工具
│   └── widgets/             # 可复用组件
├── test/                    # Flutter 测试
├── app_icon.jpg             # 启动图标源文件
└── pubspec.yaml             # 依赖、资源与图标配置
```

## 数据流

```text
页面 / Widget
      ↓
   Provider
      ↓
DAO / 本地服务
   ↙       ↘
SQLite   应用私有文件目录
```

- SQLite 保存笔记、分类以及图片、语音、文档的索引信息。
- 导入文件会复制到应用私有目录，避免依赖原文件的临时访问权限。
- 全局搜索读取本地数据，不会向外部服务发送关键词或内容。

## 权限与隐私

| 权限或能力 | 用途 | 说明 |
| --- | --- | --- |
| 麦克风 | 录制语音 | 仅在用户主动开始录音时申请 |
| 系统相册/文件选择器 | 导入资料 | 由系统选择器授权具体文件，不扫描其他内容 |
| 网络 | 不使用 | 应用不申请网络权限，不上传用户数据 |

## 使用说明

### 笔记

进入“笔记”后点击新建按钮，填写标题、正文并选择分类。标题为空时，应用会按时间生成默认名称。

### 图片

进入“图片”后可从相册或文件选择器导入。点击缩略图查看大图并缩放，长按可删除图片。

### 语音

进入“语音”后点击录音按钮。首次录音时需要授予麦克风权限；录制过程支持暂停和继续，停止后可设置名称与分类。

### 文档

支持导入 `pdf`、`doc`、`docx`、`xls`、`xlsx`、`ppt`、`pptx` 和 `txt`。PDF 可在应用内查看，其他格式通过设备上兼容的应用打开。

### 分类与搜索

每种资料拥有独立分类。删除分类不会删除其中的资料，相关资料会回到“未分类”。首页搜索可匹配笔记标题、正文和文件名。

## 数据安全提醒

应用数据保存在 Android 私有目录。卸载应用、清除应用数据或恢复出厂设置会删除这些内容。目前版本不包含云同步和自动备份，请保留重要资料的原始副本。

## 常见问题

### Word、Excel 或 PowerPoint 文件无法打开

请确认设备已安装能够处理相应格式的应用，例如 Microsoft 365 或 WPS Office。

### 录音没有声音

请在 Android 系统设置中确认“个人工作台”已获得麦克风权限。

### 提示文件不存在

文件可能已被系统清理，或其记录与实际文件不同步。可删除失效记录后重新导入。

### 构建时出现 Android SDK 或许可证错误

运行 `flutter doctor` 检查环境，并执行 `flutter doctor --android-licenses` 接受 Android SDK 许可证。

## 当前范围

当前版本专注于单设备、离线资料管理，暂不包含：

- 云同步、备份恢复和多设备同步
- 账号系统与多人协作
- iOS、HarmonyOS 或桌面版本
- OCR、语音转文字和 AI 摘要
- 密码锁、指纹锁
- Office 文档的应用内编辑与完整排版渲染

## 参与开发

欢迎通过 Issue 提交问题或功能建议。提交代码前建议运行：

```bash
flutter analyze
flutter test
```

## 许可证

本项目暂未声明开源许可证。未经项目所有者许可，不代表可以复制、分发或用于商业用途。