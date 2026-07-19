# 贪吃蛇 Snake Rush

[中文](#中文说明) | [English](#english)

---

## 中文说明

一个使用 HTML5 Canvas 开发、通过 Android WebView 封装成 APK 的贪吃蛇手机游戏。无需应用商店，直接侧载安装到 Android 设备。

### 游戏特性

- **操作**：虚拟摇杆——按住屏幕任意位置滑动即出现摇杆，往哪推往哪走；电脑上支持方向键/WASD
- **玩法**：经典撞墙/咬自己失败，吃豆逐渐加速；背景音乐节奏随速度变快（电子摇滚风格，Web Audio 实时合成）
- **对手蛇**：吃到第 2 个豆子后出现（最多 3 条）。咬它的蛇身可将其变成金豆；被它咬到或头对头相撞则失败。难度分三档，困难档会主动追踪玩家
- **道具**（开局可单独开关）：
  - 金豆子：+5 分，限时消失，全屏烟花特效
  - 减速果：降低当前速度
  - 剪刀果：蛇身缩短 3 节
  - 🍄 变粗：蛇变粗、头部碰撞区 3×3，持续 10 秒
  - ⭐ 无敌：穿墙、免疫自撞、碰到对手蛇直接咬死它，持续 10 秒
- **皮肤**：5 套渲染风格（经典扁平 / 3D 果冻球 / 霓虹发光 / 龙鳞甲 / 黄金金属），按历史最高分解锁
- **本地存档**：最高分、皮肤选择、对局设置均保存在设备本地

### 云端构建 APK（无需本地开发环境）

1. 将本仓库推送到 GitHub（Private 或 Public 均可）
2. 仓库 **Actions** 页面会在每次 push 后自动构建；也可手动 "Run workflow"
3. 构建完成后，在该次运行页面底部 **Artifacts** 处下载 `snake-apk`（zip 内为 `app-debug.apk`）

### 安装到设备

1. 将 `app-debug.apk` 传到手机/平板（微信、QQ、数据线均可）
2. 点击 APK 安装；按系统提示允许"安装未知来源应用"
3. MIUI/HyperOS 如弹出风险提示，选择"继续安装"

### 更新游戏

游戏全部逻辑在 `app/src/main/assets/snake.html` 单文件内。修改后 push 到仓库，Actions 自动重新构建，下载新 APK 覆盖安装即可（包名不变，存档保留）。

### 工程结构

```
app/src/main/assets/snake.html        游戏本体（HTML5 单文件）
app/src/main/java/.../MainActivity.java  WebView 壳
app/src/main/res/drawable/ic_launcher.xml  应用图标（矢量）
.github/workflows/build.yml           云端构建配置
```

- `minSdk 21`（Android 5.0+），`targetSdk 34`，实测兼容 MIUI 10（Android 8.1）至 HyperOS 2（Android 15）
- 构建产物为 debug 签名 APK，仅用于自用侧载，不可上架商店

---

## English

A Snake mobile game built with HTML5 Canvas and packaged as an Android APK via WebView. No app store required — sideload directly onto any Android device.

### Features

- **Controls**: virtual joystick — press and drag anywhere on screen to summon a joystick and steer; arrow keys / WASD on desktop
- **Gameplay**: classic rules — hitting a wall or yourself ends the game; speed increases as you eat. Background music (synthesized electro-rock via Web Audio) speeds up with the snake
- **Opponent snakes**: appear after your 2nd bean (up to 3 at once). Bite their body to turn them into gold beans; getting bitten or colliding head-on means game over. Three difficulty levels — the hard AI actively chases you
- **Power-ups** (individually toggleable before each run):
  - Gold bean: +5 points, time-limited, full-screen fireworks
  - Slow berry: reduces current speed
  - Scissors: shortens your snake by 3 segments
  - 🍄 Thick: fatter snake with a 3×3 head hitbox, lasts 10 s
  - ⭐ Invincible: pass through walls, immune to self-collision, instantly kill any opponent you touch, lasts 10 s
- **Skins**: 5 rendering styles (flat classic / 3D jelly / neon glow / dragon scale / metallic gold), unlocked by high score milestones
- **Local saves**: high score, skin choice and match settings persist on device

### Building the APK in the cloud (no local toolchain needed)

1. Push this repository to GitHub (private or public)
2. The **Actions** tab builds automatically on every push; you can also trigger "Run workflow" manually
3. When the run finishes, download `snake-apk` from the **Artifacts** section (`app-debug.apk` inside the zip)

### Installing on a device

1. Transfer `app-debug.apk` to your phone/tablet
2. Tap the APK to install; allow "install from unknown sources" when prompted
3. On MIUI/HyperOS, tap "Continue anyway" if a risk warning appears

### Updating the game

All game logic lives in the single file `app/src/main/assets/snake.html`. Edit it, push, let Actions rebuild, then install the new APK over the old one (same package name, saves are kept).

### Project layout

```
app/src/main/assets/snake.html        the game (single HTML5 file)
app/src/main/java/.../MainActivity.java  WebView shell
app/src/main/res/drawable/ic_launcher.xml  launcher icon (vector)
.github/workflows/build.yml           CI build config
```

- `minSdk 21` (Android 5.0+), `targetSdk 34`; tested from MIUI 10 (Android 8.1) up to HyperOS 2 (Android 15)
- The output is a debug-signed APK intended for personal sideloading only, not store distribution
