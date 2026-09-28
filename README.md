<div align="center">
    <h1>我的电视</h1>
    <p>Android 原生开发的电视直播播放软件（Google TV 音画同步优化版）</p>

![GitHub Repo stars](https://img.shields.io/github/stars/abszm/mytv-android)
![GitHub all releases](https://img.shields.io/github/downloads/abszm/mytv-android/total)
[![Android Sdk Require](https://img.shields.io/badge/Android-6.0%2B-informational?logo=android)](https://apilevels.com)
[![GitHub](https://img.shields.io/github/license/abszm/mytv-android)](https://github.com/abszm/mytv-android)

</div>

## 本仓库的优化

针对 Google TV 硬件直播音画不同步问题的专项优化（完整变更见 [CHANGELOG](CHANGELOG.md)）：

- Media3 1.4.0 → **1.11.1**：音频缓冲区策略、播放起始 A/V 同步、直播流时间戳恢复等大量官方修复
- 直播播放禁用音频 offload，显式声明媒体音频用途，修复部分 TV 硬件上音画逐渐漂移
- 开启解码器自动回退；软解扩展与新版 Media3 不兼容时自动回退纯硬解，避免崩溃
- 全量升级依赖：AGP 8.13.2 / Kotlin 2.4.20 / Gradle 8.14.5 / Compose BOM 2026.05.01 等
- compileSdk 36，minSdk 23（Media3 1.9+ 要求）
- 应用内自动更新指向本仓库 Releases；GitHub Actions 自动构建 beta 版并发布

## 下载

- 到 [Releases](https://github.com/abszm/mytv-android/releases) 下载最新 `mytv-android-tv-*-all-sdk23.apk`
- 或在应用内检查更新（更新通道选 `beta`），自动下载安装本仓库最新 beta

## 使用

### 操作方式

> 遥控器操作方式与主流视频播放软件类似；

- 频道切换：使用上下方向键，或者数字键切换频道；屏幕上下滑动；
- 频道选择：OK键；单击屏幕；
- 设置页面：按下菜单、帮助键，长按OK键；双击、长按屏幕；

### 触摸键位对应

- 方向键：屏幕上下左右滑动
- OK键：点击屏幕
- 长按OK键：长按屏幕
- 菜单、帮助键：双击屏幕

### 自定义设置

- 访问以下网址：`http://<设备IP>:10481`
- 打开应用设置界面，移到最后一项
- 支持自定义订阅源、自定义节目单、缓存时间等等

### 自定义订阅源

- 设置入口：自定义设置网址
- 格式支持：m3u格式、tvbox格式

### 多订阅源

- 设置入口：打开应用设置界面，选中`自定义订阅源`项，点击后将弹出历史订阅源列表
- 历史订阅源列表：短按可切换当前订阅源（需重启），长按将清除历史记录；该功能类似于`多仓`，主要用于简化订阅源切换流程
- 须知：
    1. 当订阅源数据获取成功时，会将该订阅源保存到历史订阅源列表中
    2. 当订阅源数据获取失败时，会将该订阅源移出历史订阅源列表

### 多线路

- 功能描述：同一频道拥有多个播放地址，相关标识位于频道名称后面
- 切换线路：左右方向键；屏幕左右滑动
- 自动切换：当当前线路播放失败后，将自动播放下一个线路，直至最后
- 须知：
    1. 当某一线路播放成功后，会将该线路的`域名`保存到`可播放域名列表`中
    2. 当某一线路播放失败后，会将该线路的`域名`移出`可播放域名列表`
    3. 当播放某一频道时，将优先选择匹配`可播放域名列表`的线路

### 自定义节目单

- 设置入口：自定义设置网址
- 格式支持：.xml、.xml.gz格式

### 当天节目单

- 功能入口：打开应用选台界面，选中某一频道，按下菜单、帮助键、双击屏幕，将打开当天节目单
- 须知：由于该应用不支持回放功能，所以更早的节目单没必要展示

### 频道收藏

- 功能入口：打开应用选台界面，选中某一频道，长按OK键、长按屏幕，将收藏/取消收藏该频道
- 切换显示收藏列表：首先移动到频道列表顶部，然后再次按下方向键上，将切换显示收藏列表；手机长按频道信息切换

## 系统要求

- Android 6.0（API 23）及以上
- 直播源与节目单由用户自行提供，可用性取决于网络环境与源的质量

## 构建

```bash
./gradlew :tv:assembleDebug    # TV 调试包
./gradlew :tv:assembleRelease  # TV 发布包（需签名配置，CI 使用自动生成的签名）
```

推送到仓库后，GitHub Actions 会自动构建并发布 beta 版（版本号自动附加 `-beta` 后缀）。

## 更新日志

[更新日志](./CHANGELOG.md)

## 声明

本项目仅用于个人学习和测试，不提供任何破解内容；直播源与节目单由用户自行配置。

## 致谢

- 本项目基于 **[yaoxieyoulei/mytv-android](https://github.com/yaoxieyoulei/mytv-android)** 修改而来，原项目及全部核心功能均出自原作者 **[yaoxieyoulei](https://github.com/yaoxieyoulei)** 之手，感谢其出色的工作。原项目基于 [MIT License](LICENSE) 开源，本仓库延续相同协议并按要求保留原版权声明。
