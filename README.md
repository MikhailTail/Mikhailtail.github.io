# Mikhailtail · 个人主页

苹果风通透感（毛玻璃 + SF 系统字体 + 大号排印），纯静态单文件。

## 页面风格

- **苹果风通透感** — 毛玻璃质感、SF 系统字体、大号排印，大量留白，整体干净通透。
- **纯静态单文件** — HTML / CSS / JS 全部内联在 `index.html`，无构建、无依赖。
- **浅色 / 深色** — 右上角月亮与太阳按钮切换，首次自动跟随系统，选择存入 localStorage。
- **中英双语** — 右上角 `EN / 中文` 切换，所有文案集中在 `I18N` 对象里。
- **内容实时拉取** — 头像、仓库列表、统计数字在页面加载时从 `api.github.com` 获取，无需手动维护。
- **贡献热力图** — 走 `github-contributions.vercel.app`，不可用时自动回退到 `ghchart.rshah.org`。
- **精选 / 全部两个 tab** — `FEATURED_REPOS` 中列出的仓库进入「精选」，其余按更新时间排列在「全部」。

## 文件构成

```
index.html   ← 整站（HTML/CSS/JS 全内联）
CNAME        ← GitHub Pages 自定义域名
```
