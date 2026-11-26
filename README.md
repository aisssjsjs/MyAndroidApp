# HelloAIDE —— 在平板上用 AIDE 编译的传统项目

一个纯 Java + XML 布局的计数器 App，不依赖 Gradle，专为 AIDE / AIDE Pro 这类老式 IDE 准备。

## 为什么用这种结构

AIDE 不认识 AGP 8.x 的 Gradle 项目，但认识经典的目录结构：

```
HelloAIDE/
├── AndroidManifest.xml     ← 项目入口，AIDE 靠它识别项目
├── res/
│   ├── layout/activity_main.xml
│   └── values/{strings.xml, styles.xml}
└── src/com/example/hello/MainActivity.java
```

## 导入步骤

1. 把整个 `HelloAIDE` 文件夹解压到平板存储，例如 `/sdcard/AppProjects/HelloAIDE`；
2. 打开 AIDE / AIDE Pro；
3. 首页选 **Open project**（有的版本叫 “打开项目” / “更多 → 打开”）；
4. 浏览到 `HelloAIDE` 目录，或直接点 `AndroidManifest.xml`；
5. AIDE 识别后点 **Run**（▶），首次编译约 10～30 秒；
6. 编译成功后点 **Install & Run**，就能看到界面。

## 界面说明

- 大数字显示当前计数
- 「加一」「减一」「重置」三个按钮
- 纯 `findViewById` + 匿名内部类，没用 lambda、没用 Kotlin、没用 Compose，兼容老编译器

## 常见问题

| 现象 | 处理 |
|---|---|
| AIDE 提示 “Project has no build.gradle” | 忽略，本项目的目标就是不用 Gradle |
| 编译报 `package R does not exist` | 检查 `AndroidManifest.xml` 里的 package 是否与 Java 文件路径一致（com/example/hello） |
| 提示找不到 SDK | AIDE 设置里选一个已安装的 Android SDK（通常自带） |
| 安装失败 | 允许 “安装未知应用”，并卸载同包名旧版本 |
| 中文乱码 | 文件保存为 UTF-8 |
| 编译很慢 | 首次编译要建索引，之后会快；把 AIDE 加入电池白名单 |

## 和 CounterApp 的区别

| | HelloAIDE | CounterApp（Compose） |
|---|---|---|
| 语言 | Java | Kotlin |
| UI | XML 布局 | Jetpack Compose |
| 构建 | AIDE 内置 | Gradle + AGP |
| 能否用 AIDE 编译 | ✅ | ❌ |
| 能否用 AndroidIDE 编译 | ❌（版本太老） | ✅（需 legacy 版） |
| 能否云端构建 | 可以但没必要 | ✅ GitHub Actions |

## 想继续学

- 加个「步长」按钮组：在 layout 里再加 3 个 Button，Java 里改 `count += 5`；
- 让计数在重启后保留：用 `SharedPreferences`；
- 加第二个页面：新建 Activity + 在 Manifest 里注册。

这些都能在 AIDE 里直接改、直接跑，不用折腾构建工具。
