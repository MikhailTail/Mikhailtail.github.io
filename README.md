# Mikhailtail · 个人主页

苹果风通透感（毛玻璃 + SF 系统字体 + 大号排印），纯静态单文件，直接挂 GitHub Pages。

## 你拿到的文件

```
portfolio/
├── index.html   ← 整站（HTML/CSS/JS 全内联）
├── CNAME        ← GitHub Pages 自定义域名
└── README.md    ← 本文件
```

## 一、推到 GitHub Pages

1. 新建一个仓库，名字必须是 `Mikhailtail.github.io`
   （注意：就是你的用户名小写 + `.github.io`，这是 GitHub Pages 的约定）。
2. 把 `portfolio/` 里的三个文件全部 push 到这个仓库的 main 分支根目录：

```bash
cd portfolio
git init
git add .
git commit -m "init portfolio"
git branch -M main
git remote add origin git@github.com:Mikhailtail/Mikhailtail.github.io.git
git push -u origin main
```

3. 仓库 → Settings → Pages → Source 选 `main` / `(root)`，保存。
4. 等 1 分钟，访问 `https://Mikhailtail.github.io` 应该已经能看到页面。

## 二、Cloudflare 绑定 mmluulmm.com

### 1. 在 Cloudflare 加 DNS 记录
进入你的域名 mmluulmm.com → DNS → Records：

| Type | Name | Content | Proxy status |
|---|---|---|---|
| A | `@` | `185.199.108.153` | DNS only（灰色云） |
| A | `@` | `185.199.109.153` | DNS only |
| A | `@` | `185.199.110.153` | DNS only |
| A | `@` | `185.199.111.153` | DNS only |
| CNAME | `www` | `Mikhailtail.github.io` | DNS only |

> GitHub Pages 的四个 A 记录 IP 官方文档有列，先全部设为 **DNS only**（灰云），等 Pages 那边验证完域名再开代理。

### 2. 在 GitHub Pages 里启用自定义域名
仓库 → Settings → Pages → Custom domain 填：

```
mmluulmm.com
```

勾上 **Enforce HTTPS**。

> 仓库根目录的 `CNAME` 文件已经写好了 `mmluulmm.com`，push 后 GitHub 会自动识别，不用手动传。

### 3. 让 www 自动跳到主域
两种方式任选其一：

**方式 A（推荐，最简单）**：Cloudflare → Rules → Page Rules → Create：
- URL：`www.mmluulmm.com/*`
- Setting：Forwarding URL → 301 Redirect
- Destination：`https://mmluulmm.com/$1`

**方式 B**：Cloudflare → Rules → Redirect Rules → Single Redirect，同样把 `www` 301 到裸域。

### 4. 等 HTTPS 生效
GitHub 会自动申请 Let's Encrypt 证书，几分钟到几小时。之后回到 Cloudflare 把 DNS 记录的代理状态改成 **Proxied**（橙云），享受 CDN。

## 三、改成"你的"主页

打开 `index.html`，顶部有两个显眼的配置块：

```js
const FEATURED_REPOS = [
  // 'my-awesome-project',
  // 'another-repo',
];
const USERNAME = 'Mikhailtail';
```

- **置顶精选项目**：把你想置顶的仓库名（和 GitHub 上完全一致）填进数组，push 后这几个会出现在"精选"tab，其余仓库在"全部"tab 按更新时间排列。
- **没填会怎样**：默认按 star 数取前 4 个当精选，不至于空着。
- **头像、仓库列表、统计数字**：页面加载时直接从 `api.github.com` 拉，你不用手动维护。
- **贡献热力图**：用 `github-contributions.vercel.app`，挂了会自动 fallback 到 `ghchart.rshah.org`。
- **暗色/亮色切换**：右上角月亮/太阳按钮，自动跟随系统首次选择，存在 localStorage。
- **中英文切换**：右上角 `EN / 中文` 按钮，所有文案都在 `I18N` 对象里，改文案只改那里。

## 四、本地预览

直接双击 `index.html` 就行（GitHub API 从浏览器发请求，不需要本地服务器）。

## 五、以后更新内容

改完 `index.html`：

```bash
git add index.html
git commit -m "update"
git push
```

GitHub Pages 自动重新部署，1 分钟内生效。
