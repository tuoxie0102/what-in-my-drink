# 《不要天天喝奶茶》前端架构说明 v1

## 1. 技术架构说明

当前版本保持静态前端架构，入口为 `index.html`，样式为 `css/style.css`，内容数据继续来自 `js/data.js`。

已新增 `package.json` 与 `package-lock.json`，安装依赖：

- `framer-motion`：为后续 React 化或组件化动画预留；当前静态页用原生 CSS/JS 实现 300ms-800ms 的等价克制动效。
- `@tsparticles/react`：为后续 React 粒子组件预留；当前静态页用轻量 DOM 粒子 fallback，只在遗失物出现和 XP 彩蛋触发。
- `page-flip`：用于 StPageFlip 翻页效果；当前页通过 CDN 尝试加载 `PageFlip`，失败时使用 CSS 3D 翻页 fallback。
- `xp.css`：用于 Windows XP 彩蛋页。

局部接入策略：

- RPGUI：只用于今日奶茶菜单、特价确认弹窗、菜单按钮容器。
- XP.css：只在“旧电脑”彩蛋页面使用 `.window` / `.title-bar` 结构。
- 动画：页面切换、遗失物掉落、翻面、粒子均控制在 300ms-800ms，并提供 `prefers-reduced-motion` 降级。
- 收藏册：使用 `localStorage` 存储已收集遗失物 ID，不加入积分、等级、抽卡、稀有度、星级或数值成长。

## 2. 页面结构图

```text
index.html
└─ #app
   ├─ #page-shop
   │  ├─ 像素奶茶店背景
   │  ├─ 店员立绘
   │  ├─ Coffee Talk 风格像素对话框
   │  ├─ 失物招领柜入口
   │  └─ 旧电脑彩蛋入口
   ├─ #page-menu
   │  └─ RPGUI 今日三杯奶茶菜单
   ├─ #overlay-confirm
   │  └─ RPGUI 店员确认弹窗
   ├─ #page-shake
   │  └─ 点击杯子摇奶茶
   ├─ #page-reveal
   │  └─ 遗失物掉落 + 记忆粒子
   ├─ #page-card
   │  └─ 博物馆藏品卡
   │     ├─ 物品图片
   │     ├─ 标题
   │     ├─ 时间地点
   │     ├─ 50字以内说明
   │     ├─ 翻面秘密
   │     ├─ 店员评论
   │     ├─ 收进失物招领柜
   │     └─ 返回奶茶店
   ├─ #page-collection
   │  └─ 失物招领柜
   │     ├─ 校园
   │     ├─ 网吧
   │     ├─ 家庭
   │     ├─ 城市
   │     ├─ 互联网
   │     └─ 音乐
   └─ #page-easter
      └─ Windows XP 风格特殊彩蛋
```

## 3. 资源清单

本地资源：

- `assets/image/shop/shop-bg.png`：奶茶店背景
- `assets/image/shop/counter.png`：柜台备用素材
- `assets/image/clerk/clerk-default.png`：店员默认立绘
- `assets/image/clerk/clerk-cooking.png`：店员制作立绘
- `assets/image/clerk/clerk-reading.png`：店员阅读立绘
- `assets/image/clerk/clerk-sleeping.png`：店员睡觉立绘
- `assets/image/cups/cup-pearl.png`：珍珠奶茶杯
- `assets/image/cups/cup-ice-tea.png`：冰茶杯
- `assets/image/cups/cup-special.png`：特调杯
- `assets/image/cards/#001.png` 到 `#017.png`：已具备图片的遗失物素材
- `js/data.js`：奶茶、遗失物、店员台词数据

外部资源：

- RPGUI CDN：`https://cdn.jsdelivr.net/gh/RonenNess/RPGUI/dist/rpgui.min.css`
- XP.css CDN：`https://unpkg.com/xp.css`
- StPageFlip CDN：`https://unpkg.com/page-flip/dist/js/page-flip.browser.js`

## 4. 待补充素材清单

- `#018` 之后遗失物图片，目前数据已存在但图片文件未补齐。
- 店员半身立绘可补充更接近 Coffee Talk 的柜台构图版本。
- 遗失物翻面专用背面图，例如请假条背面、歌词本背面、作业本涂鸦页。
- XP 彩蛋页可补充旧桌面壁纸、旧图标、弹窗音效。
- 奶茶摇动与遗失物掉落可补充轻量音效，但应默认静音或由用户主动开启。

## 5. 第一版可运行 HTML

第一版可运行入口为：

```text
index.html
```

本地验证方式：

```bash
python -m http.server 8765 --bind 127.0.0.1
```

然后访问：

```text
http://127.0.0.1:8765/
```
