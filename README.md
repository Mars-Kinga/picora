<p align="center"><img src="https://github.com/Mars-Kinga/picora/releases/download/readme-media-20261021/AppIcon.png" width="112" alt="Picora app icon"></p>

<h1 align="center">Picora · 轻选</h1>

<p align="center"><strong>让整理照片成为简单的选择。</strong><br>Review photos one swipe at a time. Decisions stay on your device until you confirm them.</p>

<p align="center"><strong>Swift · SwiftUI · PhotoKit · SwiftData · Vision · CryptoKit · iOS / iPadOS 26+</strong></p>

<p align="center"><a href="#中文">中文</a> · <a href="#english">English</a> · <a href="https://mars-kinga.github.io/picora/">隐私政策</a></p>

<p align="center">
  <img src="https://github.com/Mars-Kinga/picora/releases/download/readme-media-20261021/suggestions-light-20261013.png" width="200" alt="On-device photo suggestions">
</p>
<p align="center"><sub>清理建议的实际使用截图；数字仅反映拍摄时的图库状态。</sub></p>

<details>
<summary>iPhone Duo 宽屏布局 · Wide layout (simulator)</summary>

<p align="center"><img src="https://github.com/Mars-Kinga/picora/releases/download/readme-media-20261021/iphone-duo-suggestions.png" width="760" alt="Suggestions beside photo comparison"></p>
<p align="center"><img src="https://github.com/Mars-Kinga/picora/releases/download/readme-media-20261021/iphone-duo-review.png" width="760" alt="Wide photo review with actions beside the preview"></p>

</details>

**当前状态 / Availability:** 本公开仓库提供项目介绍和隐私政策；App 源码保存在私有的 `picora-code` 仓库，尚未提供 App Store 或 TestFlight 下载链接。当前开发版本号为 1.1，最低部署版本为 iOS / iPadOS 26.0，目标设备为 iPhone 和 iPad。The app source is private; no public App Store or TestFlight link is listed here.

> 更新：2026-11-03。功能代码和对应测试已同步至私有源码仓库；公开仓库提供项目介绍和隐私政策。The current feature source and tests are synchronized to the private repository. No public app release is implied.

<a id="中文"></a>
## 中文

Picora 是个人开发的原生 iPhone / iPad 照片整理 App。先选择月份、年份、相簿或媒体类型，再逐张决定保留、待删或稍后处理，最后在清单中确认对系统图库的修改。审核进度保存在本机，可随时继续。

支持简体中文、繁体中文（台湾用语）和英文，随系统或应用语言偏好显示。繁体版显示名称为「輕選」。

- **原生审核体验：** SwiftUI 叠放卡片、滑动与点按、撤销和触觉反馈；拖动时间线预览并跳转，离开后恢复位置。待决定支持从选中照片开始连续审核，宽屏下使用分栏布局。
- **媒体预览：** 视频每次启动默认静音，本次使用中共享声音选择；支持 Live Photo 预览与原始媒体分享。
- **本机清理建议：** Vision 图像特征与 OCR 辅助查找相似照片和旧临时截图；SHA-256 完整资源哈希用于核对重复原件。美学评分与人像成像质量帮助推荐保留照片；较大组可以建议保留多张，最终决定始终由用户作出。
- **可恢复的图库操作：** SwiftData 保存审核进度和待办；PhotoKit 写入集中确认。Live Photo 转静态时先核对副本，再将原件加入待删清单，并在提交删除前再次核验。
- **缓存与功耗控制：** SQLite 增量缓存分析结果；后台分析根据充电、低电量模式和设备温度调整节奏，严重热压力下暂停。建议扫描不主动下载 iCloud 原片。

图库删除可能同步到 iCloud，并受“最近删除”影响；已知文件大小不等于立即释放的空间。审核云端照片、主动下载高清、分享或转换可能使用网络。详细的隐私与权限说明见[隐私政策](https://mars-kinga.github.io/picora/)；使用指南保存在私有源码仓库。

<a id="english"></a>
## English

Picora is a native iPhone and iPad app for reviewing photos and videos one at a time. Choose a month, year, album, or media type; swipe to keep, queue for deletion, or decide later. Review state is saved locally, and changes to the Photos library require a separate confirmation.

Available in English, Simplified Chinese, and Traditional Chinese with Taiwan wording, following the system or per-app language preference.

- **Native review:** SwiftUI cards, swipe and tap actions, undo, and haptics. Scrub the timeline to preview and jump, resume at the saved position, and review deferred items continuously from any selected photo. Wide windows use a column-based layout.
- **Media previews:** Videos start muted on each app launch and share the sound preference during that app session. Live Photo previews and original-media sharing are supported.
- **On-device suggestions:** Vision image features and OCR surface similar shots and old temporary screenshots. SHA-256 checks complete resources for exact duplicates. Aesthetic and face-capture quality scores inform keep recommendations, including multiple keepers in larger groups; the user makes the final choice.
- **Recoverable operations:** SwiftData persists review state, while PhotoKit changes are staged for confirmation. Live Photo-to-still conversion verifies the new copy before queuing the original for deletion and checks it again before committing.
- **Cached, energy-aware analysis:** Incremental SQLite results are reused across sessions. Background work adjusts to charging, Low Power Mode, and thermal conditions; suggestion scans do not proactively download iCloud originals.

Deleting from the system library may sync through iCloud. A displayed file size does not guarantee immediately freed device storage. See the [privacy policy](https://mars-kinga.github.io/picora/). The user guide and development notes are kept with the private source.

## Build from source · 本地运行

The following steps are for collaborators with access to the private source repository. Use Xcode with the iOS 26 SDK or newer. The Xcode project, shared scheme, and app target are still named `Zeying`.

```sh
git clone https://github.com/Mars-Kinga/picora-code.git
cd picora-code
open Zeying.xcodeproj
```

Select the `Zeying` scheme and an iPhone or iPad simulator. For a physical device, select your development team under **Signing & Capabilities** and update the bundle identifier if needed. Grant Photos access on first launch; limited access shows only selected assets. Run the included Swift Testing suite with **Product → Test**. PhotoKit writes, iCloud behavior, and system dialogs require device-level verification.

iPad portrait uses the vertical review flow; wide landscape windows use columns and side controls. Narrow windows and preview sheets use their own available size. The local validation record includes iPad simulator checks; physical iPad, real multiwindow, media, and library-write validation remain separate. The iPhone Duo images above are also simulator captures.

## Project structure · 项目结构

```text
Zeying/Core/       Review records, pending actions, suggestion state
Zeying/Library/    PhotoKit services, on-device analysis, background work
Zeying/UI/         Home, review, suggestions, confirmation and settings
ZeyingTests/       Swift Testing behavior tests
Tools/             App icon generation
doc/               Local numbered requirements (Git-ignored)
docs/              User guide, privacy and validation records
```

Performance measurements and their limits are documented with the private source. This public repository is a portfolio overview and privacy-policy host; it does not imply an App Store release.
