# 更新日志

## 【2.2.9-beta】 - 2026-09-28

### 优化

- 应用内在线更新指向本仓库 Releases（原作者更新服务器已移除，其依赖的 ghp.ci 代理也已失效）
- 解析器支持 GitHub Releases 列表响应，自动取最新发行版
- 移除原作者相关信息（关于页赞赏入口、捐赠二维码等）
- 仓库与 README 重新组织，文末标注原作者地址
- 版本标签改为 v版本号 形式（如 v2.2.9-beta），便于应用内更新比对

## 【2.2.8】 - 2026-09-28

### 优化

- Media3 升级 1.4.0 → 1.11.1，包含大量音画同步、音频缓冲区与直播流恢复修复
- 播放器显式声明音频属性（USAGE_MEDIA），TV 上正确路由媒体音频流
- 直播场景禁用音频 offload，避免部分 TV 硬件 offload 播放导致音画逐渐不同步
- 开启解码器自动回退（setEnableDecoderFallback），硬解异常时降低卡顿概率
- 移除"跳过多帧渲染"设置项，新版 Media3 已内置更智能的相同释放时间帧跳过机制
- 软解扩展与新版 Media3 二进制不兼容时自动回退纯硬解，避免崩溃
- 全量升级依赖：AGP 8.13.2、Kotlin 2.4.20、Gradle 8.14.5、Compose BOM 2026.05.01、OkHttp 5.4.0、Navigation 2.9.8、TV Material 1.1.0 等
- compileSdk 35 → 36，minSdk 21 → 23（Media3 1.9+ 要求，Google TV 设备均满足）
- Gradle Wrapper 8.7 → 8.14.5，移除未使用的 KSP 插件
- 修复 mobile 模块缺失的 HarmonyOSSans 字体定义（上游遗留问题）
- 添加 GitHub Actions 自动构建 APK 工作流
