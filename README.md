# 贪吃蛇 APK 打包指南

这是一个完整的 Android 工程，用 WebView 封装贪吃蛇 HTML5 游戏。
不需要在电脑上安装任何开发工具，用 GitHub 免费云端构建出 APK。

## 一、云端构建步骤（推荐，约 10 分钟）

1. 注册/登录 GitHub（github.com，免费）
2. 点右上角 “+” → New repository，仓库名随意（如 `snake`），选 **Private**，点 Create repository
3. 在新仓库页面点 “uploading an existing file”，把 `snake-apk` 文件夹里的**全部内容**
   （包括 `.github` 文件夹，注意不是 snake-apk 文件夹本身）拖进上传区，点 Commit changes
   - 如果拖拽没带上 `.github` 文件夹，就手动：Add file → Create new file，
     文件名输入 `.github/workflows/build.yml`，把本地该文件内容粘贴进去提交
4. 点仓库顶部的 **Actions** 标签页 → 左侧选 “Build APK” → 如果没有自动运行，
   点 “Run workflow” 手动触发
5. 等 3~5 分钟构建完成（绿色对勾），点进该次运行，页面底部 **Artifacts**
   处下载 `snake-apk`（是个 zip，解压得到 `app-debug.apk`）

## 二、安装到平板/手机

1. 把 `app-debug.apk` 传到设备（微信文件传输助手 / QQ / 数据线均可）
2. 在设备上点击 APK 文件安装
3. 系统会提示“禁止安装未知来源应用”→ 去设置里允许当前应用（文件管理器/微信）安装
4. MIUI 可能弹“检测到风险”→ 点“继续安装”即可

## 三、以后更新游戏

改了 `app/src/main/assets/snake.html` 后，重新上传该文件到 GitHub 仓库
（在仓库中打开该文件 → 铅笔图标编辑 → 粘贴新内容 → Commit），
Actions 会自动重新构建，下载新 APK 覆盖安装即可
（applicationId 不变，直接覆盖升级，存档保留）。

## 工程说明

- `app/src/main/assets/snake.html` —— 游戏本体（全部逻辑都在这一个文件里）
- `app/src/main/java/com/gavin/snake/MainActivity.java` —— WebView 壳
- `minSdk 21`：兼容 Android 5.0+（你的 MIUI 10 平板是 Android 8.1，没问题）
- `targetSdk 34`：兼容 HyperOS 2（Android 15）
- 构建产物是 debug 签名的 APK，仅用于自用侧载，不能上架商店
