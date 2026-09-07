# 🎄 我的梦幻圣诞宇宙

一个运行在浏览器中的沉浸式 3D 圣诞互动页面。项目使用 Three.js 构建粒子圣诞树与宇宙背景，通过 MediaPipe Hands 识别手势，并借助 Firebase 保存和展示访客留下的祝福。

无需安装依赖，也不需要构建工具：启动一个本地静态服务器即可体验。

## ✨ 功能亮点

- **粒子圣诞树**：由 25,000 个立方体粒子组成，搭配星空、金色螺旋装饰、树顶星与动态雪花。
- **AI 手势交互**：调用摄像头识别双手动作，控制圣诞树旋转、聚合、散开和文字造型。
- **手势光标**：用食指移动屏幕光标，捏合手指选择树上的礼物盒。
- **星际祝福**：访客可以发布留言，祝福会通过 Firebase Firestore 实时同步，并成为树上的礼物。
- **足迹记录**：查看最近收到的 15 条祝福。
- **宇宙旋律**：使用 Web Audio API 在浏览器中实时生成旋律，手势出现时音乐渐入。
- **响应式设计**：适配桌面端和移动端屏幕。
- **纯前端运行**：核心代码集中在单个 HTML 文件中，适合直接部署到 GitHub Pages 等静态托管平台。

## 🖐️ 手势说明

首次进入页面时，请允许浏览器使用摄像头，并让双手完整出现在右上角的预览画面中。

| 手势 | 效果 |
| --- | --- |
| 移动食指 | 左右旋转圣诞树，并移动手势光标 |
| 拇指与食指捏合 | 选中礼物；松开后打开祝福 |
| 再次捏合 | 关闭祝福弹窗 |
| 快速挥动双手 | 让圣诞树粒子散开并触发雪花 |
| 双手握拳 | 让粒子重新聚合成圣诞树 |
| 双手举起并靠近 | 将粒子排列为 `Enjoy the present` |

## 🚀 本地运行

由于项目需要加载 ES Module、CDN 资源并请求摄像头权限，建议通过本地服务器访问，不要直接双击 HTML 文件。

### 方法一：使用 Python

```bash
git clone https://github.com/qin257274-max/my-christmas-tree.git
cd my-christmas-tree
python3 -m http.server 8000
```

打开 <http://localhost:8000>。

### 方法二：使用 Node.js

```bash
npx serve .
```

根据终端显示的地址在浏览器中打开页面。

> 摄像头功能通常只允许在 `localhost` 或 HTTPS 环境下使用。首次加载还需要联网下载字体、Three.js、MediaPipe 和 Firebase SDK。

## 🌐 部署到 GitHub Pages

1. 打开仓库的 **Settings → Pages**。
2. 在 **Build and deployment** 中选择 **Deploy from a branch**。
3. 选择 `main` 分支和 `/ (root)` 目录。
4. 保存并等待 GitHub Pages 完成部署。

部署成功后，通常可以通过以下地址访问：

```text
https://qin257274-max.github.io/my-christmas-tree/
```

## 🧰 技术栈

- HTML5 / CSS3 / JavaScript ES Modules
- [Three.js](https://threejs.org/)：3D 场景、粒子、灯光和动画
- [MediaPipe Hands](https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker)：摄像头手部关键点识别
- [Firebase Authentication](https://firebase.google.com/docs/auth)：匿名登录
- [Cloud Firestore](https://firebase.google.com/docs/firestore)：祝福留言的实时存储与同步
- Web Audio API：浏览器端旋律生成
- Google Fonts：中文字体

所有前端依赖均通过 CDN 加载，仓库中没有 `package.json`，因此无需执行 `npm install`。

## 📁 项目结构

```text
my-christmas-tree/
├── index.html       # 当前主页面：完整互动版
├── 圣诞宇宙.html     # 早期/备用版本
└── README.md        # 项目说明
```

## 🔥 Firebase 配置

`index.html` 中已经包含 Firebase Web 配置，并使用匿名身份验证连接 Firestore。若要部署自己的独立版本，请：

1. 在 Firebase 控制台创建项目和 Web 应用。
2. 开启 **Authentication → Sign-in method → Anonymous**。
3. 创建 Firestore 数据库。
4. 将 `index.html` 中的 `firebaseConfig` 替换为自己的配置。
5. 根据实际用途设置严格的 Firestore Security Rules。

留言数据写入以下集合：

```text
artifacts/xmas-v2025-final/public/data/userGifts
```

生产环境请限制字段类型、留言长度和写入频率，避免公开数据库被滥用。

## 🎨 自定义

你可以直接编辑 `index.html` 来改变作品内容：

- 修改 `PARTICLE_COUNT` 调整圣诞树粒子数量。
- 修改 `baseGifts` 替换默认礼物和祝福语。
- 修改 `randomEmojis` 调整随机装饰。
- 修改 `MELODY` 更换旋律音符。
- 在 `createTextLayout()` 中替换 `Enjoy the present` 文字。
- 调整材质颜色、灯光和雾效，创造自己的圣诞主题。

粒子数量较多时可能对移动设备或集成显卡造成压力。如果页面运行不流畅，可以优先降低 `PARTICLE_COUNT`、环境粒子或雪花数量。

## 💡 使用提示

- 推荐使用最新版 Chrome、Edge 或其他支持 WebGL 和摄像头 API 的现代浏览器。
- 确保环境光线充足，双手与背景有明显区分，以提高识别稳定性。
- 如果摄像头没有启动，请检查浏览器的网站权限和系统摄像头权限。
- 音频需要用户主动点击“开启绚烂旋律”，这是浏览器的自动播放限制。
- 如果留言无法发布，请检查网络连接、Firebase 匿名登录和 Firestore 规则。

## 📄 License

当前仓库尚未提供开源许可证。在添加许可证之前，项目默认保留全部权利。

---

愿每一颗微小的星光，都成为冬日宇宙里温柔的回响。🎁✨
