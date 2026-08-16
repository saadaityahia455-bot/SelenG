# 设计与技术笔记

## 视觉系统

### 配色

| 颜色 | 十六进制 | 用途 |
|------|---------|------|
| 米黄纸色 | `#f5efe3` | 主背景 |
| 深米色 | `#ebe2cf` | 段落背景 |
| 主文字色 | `#2b2620` | 标题、正文 |
| 次文字色 | `#5a4f44` | 描述文字 |
| 浅文字色 | `#8b7e6c` | 注释、脚注 |
| 朱砂红 | `#b14233` | 强调、印章、爱情 |
| 金色 | `#b08a3e` | 礼盒包装纸呼应 |
| 蓝色 | `#7a93b3` | 鲸鱼挂件呼应 |

### 字体策略

| 字体 | 用途 | 来源 |
|------|------|------|
| **Ma Shan Zheng** | 标题、礼物命名 | Google Fonts |
| **Long Cang** | 诗化段落(手写感) | Google Fonts |
| **Noto Serif SC** | 正文(系统兜底:Source Han Serif / Songti) | Google Fonts |
| **Cormorant Garamond** | 英文斜体(描述) | Google Fonts |

**为什么不用黑体?**
> 楷体才有"家书"的感觉。黑体像通知、宋体像公文。手写信应用手写体。

**字体加载策略:**
- `<link rel="preconnect">` 提前连接 fonts.gstatic.com
- `font-display: swap` —— 字体加载时先用系统字体,加载完再切换
- 系统兜底:`KaiTi`, `STKaiti`, `Songti SC` —— 即使完全无网也好看

### 间距系统

```
页内边距:140px (桌面) / 80px (平板) / 56px (手机)
段间距:28px (桌面) / 18px (手机)
行高:2.0 (诗化) / 2.4 (信) / 1.85 (基础)
```

---

## 动效设计原则

### 1 · 克制

所有动效都应该是**阅读的助力**,不是干扰。
- 入场用 `IntersectionObserver`,滚到才浮现,不打断阅读
- 拍立得视差只在桌面端,触摸端没意义
- 所有动画都尊重 `prefers-reduced-motion: reduce`

### 2 · GPU 加速

凡是高频动效都加 `transform` / `will-change`:

```css
.box { will-change: transform; }
.polaroid { transform-style: preserve-3d; }
```

### 3 · 移动端降级

检测移动端,降低动画复杂度:

```js
const isMobile = /Android|iPhone|iPad/i.test(navigator.userAgent);
const MAX_DROPS = isMobile ? 18 : 60;  // 名字雨密度
const SPAWN_RATE = isMobile ? 0.18 : 0.4;
```

---

## 关键技术决策

### 为什么不用框架?

- 维护成本:零
- 学习成本:零(任何人都能改)
- 启动速度:零(没有打包步骤)
- 调试成本:零(打开 devtools 就能改)

**对于一个"情书"项目,这比任何框架都重要。**

### 为什么不用 build 工具?

同上。
直接打开 `index.html` 就能改,意味着**你的女朋友也能改**。

### 为什么用 `<picture>` 而不是 `<img srcset>`?

`<picture>` 让浏览器**先看格式支持,再看尺寸**。
现代浏览器都支持 webp,会自动跳过 jpg fallback。

### 背景音乐:网易云外链 vs 下载 mp3

我选了**网易云外链**而不是本地 mp3,原因:
- 仓库体积小(0 字节音乐文件)
- 不涉及版权分发
- 缺点:外链可能失效
- 备选:用户可以下载后自己替换 `<audio>` 的 src

### 自动播放的处理

浏览器限制:音频不能在用户交互前自动播放。
解法:

```js
document.addEventListener('click', function once(){
  startMusic();
  document.removeEventListener('click', once);
}, { once:true });
```

---

## 性能指标

| 指标 | 桌面端 | 移动端 |
|------|-------|-------|
| 总传输量(原版) | ~16 MB | ~16 MB |
| HTML | 22 KB | 22 KB |
| CSS | 30 KB | 30 KB |
| JS | 11 KB | 11 KB |
| 单图 | 0.5-1.8 MB | 0.5-1.8 MB |
| 首屏 LCP | ~3-5s (3G) | ~5-8s (Slow 4G) |

### 优化方向(未来)

- AVIF 格式(节省 20-30%)
- `<link rel="preload" as="image">` 给首屏图
- 内联关键 CSS
- 字体子集化(只下载用到的字符)

---

## 浏览器兼容性

| 浏览器 | 最低版本 |
|-------|---------|
| Chrome | 90+ |
| Safari | 14+ |
| Firefox | 88+ |
| Edge | 90+ |
| 华为自带浏览器 | HarmonyOS 2.0+ |
| iOS Safari | 14+ |
| Android Chrome | 90+ |

### 不支持的功能

- IE 11(已停止支持)
- 旧版微信内置浏览器(无 `<canvas>` 加速)

---

## 已知问题

1. **GitHub Pages 缓存**:更新后需等 1-2 分钟 CDN 同步
2. **微信内置浏览器**:会自动把外链 mp3 替换为自家播放器
3. **iOS Safari**:背景音乐需要用户先点击页面才能播放(策略限制)

---

> 这是给同样想写"代码情书"的人留的一份笔记。
> —— 韩天宇,2026 年 8 月