# Contributing to Love Letter · 贡献指南

> 欢迎 fork 这个项目,把它改成你自己的情书 💌

## 这个项目欢迎什么样的贡献

### ✅ 非常欢迎

- 🐛 **修复 bug** —— 在 Issues 里告诉我哪一段不对
- 🎨 **新设计主题** —— 加情人节版、生日版、毕业版、告白版
- 📱 **更多响应式场景** —— iPad 横屏、大屏桌面、平板折叠屏
- ♿ **无障碍优化** —— 屏幕阅读器、键盘导航、对比度
- 🌍 **国际化** —— 英文版、日文版
- 📝 **改进 README** —— 翻译、补充说明、修正错别字

### ⚠️ 需要谨慎

- ❌ **不要提交真实照片** —— 这是一个模板项目,所有礼物照片应该是占位图
- ❌ **不要提交真实姓名/地址** —— 替换成 `小明`、`小红`、`北京 ➜ 上海` 等占位
- ❌ **不要修改 `script.js` 里的名字**(`韩天宇 ♥`)以外的私房话
- ✅ 如果你想分享真实版本,**单独 fork 一个仓库**,不要 PR 回这里

### 🚫 暂不接受

- 添加 npm 依赖、构建系统、框架 —— 违背"零依赖"理念
- 重写为 React/Vue —— 这是情书,不是工程
- 引入任何追踪、广告、付费功能

---

## 开发流程

### 1. Fork 并克隆

```bash
git clone https://github.com/你的用户名/love-letter.git
cd love-letter
```

### 2. 创建分支

```bash
git checkout -b feature/my-theme
```

### 3. 本地预览

```bash
python -m http.server 8000
# 浏览器打开 http://localhost:8000
```

### 4. 测试响应式

用浏览器 DevTools 切到:
- iPhone SE (375px)
- iPhone 12 Pro (390px)
- iPad (768px)
- Desktop (1280px)

### 5. 提交

```bash
git add .
git commit -m "feat: 情人节主题配色"
git push origin feature/my-theme
```

然后在 GitHub 上创建 Pull Request。

---

## 代码风格

- **HTML** —— 语义化标签,缩进 2 空格
- **CSS** —— 类名用 kebab-case(`.cover-title`),注释用 `/* ... */`
- **JS** —— 纯 ES6+,不用 TypeScript;不用任何外部库
- **文件命名** —— 全小写,连字符分隔

---

## 提交信息规范

参考 [Conventional Commits](https://www.conventionalcommits.org/):

- `feat: 新功能`
- `fix: 修 bug`
- `docs: 改文档`
- `style: 改格式(不影响代码)`
- `refactor: 重构`
- `test: 加测试`

例:
```
feat: 加情人节主题配色
fix: 修复 iOS Safari 字体不显示的问题
docs: 补充 LICENSE 说明
```

---

## 主题配色约定

如果你要做新主题,在 `style.css` 的 `:root` 里改这些变量即可:

```css
:root{
  --paper:#f5efe3;        /* 纸色 */
  --ink:#2b2620;          /* 主文字色 */
  --accent:#b14233;       /* 强调色 */
  --gold:#b08a3e;         /* 金属色 */
  --sky:#7a93b3;          /* 冷色调 */
}
```

推荐主题:
- **情人节版** —— `paper:#ffe6e6`,`accent:#d63b5e`
- **生日版** —— `paper:#fff8dc`,`accent:#ff8c42`,`gold:#daa520`
- **圣诞版** —— `paper:#f0f8ff`,`accent:#c8102e`,`gold:#0f5132`
- **毕业版** —— `paper:#f5f5dc`,`accent:#1a4d8f`,`gold:#b08a3e`

---

## 提问

- 在 Issues 里开一个新 issue
- 用中文或英文都可以
- 描述清楚:你做了什么、想做什么、卡在哪里

**我会尽量回复每一个 issue —— 这是开源最美的部分。**

---

> 谢谢你的关注 ❤️
> —— 韩天宇