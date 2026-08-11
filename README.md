# TAIMOU 作品集网站 - GitHub Pages 部署包

## 文件结构

```
dist-github-pages/
├── index.html              # 入口 HTML
├── favicon.svg             # 网站图标
├── icons.svg               # 社交图标 sprite
├── README.md               # 本文件
└── assets/
    ├── rolldown-runtime-CNC7AqOf.js    (4KB)
    ├── radix-C9EcwUOj.js               (76KB)
    ├── radix-C9EcwUOj.js.map           (356KB)
    ├── index-B7p9I2vZ.css              (188KB)
    ├── index-BzrNx80Y.js               (176KB)
    ├── index-BzrNx80Y.js.map           (876KB)
    ├── toolkit-CcGTNecF.js             (712KB)
    ├── toolkit-CcGTNecF.js.map         (3.5MB)
    └── polyfills.js                    (56KB)
```

## 部署到 GitHub Pages

### 方法一：直接上传

1. 新建一个 GitHub 仓库（例如 `taimou-portfolio`）
2. 将本目录下所有文件上传到仓库根目录
3. 进入仓库 Settings → Pages
4. Source 选择 `Deploy from a branch`，Branch 选择 `main` / `root`
5. 等待部署完成，访问 `https://<username>.github.io/taimou-portfolio/`

### 方法二：使用 GitHub Actions 自动部署

在仓库中创建 `.github/workflows/deploy.yml`：

```yaml
name: Deploy to GitHub Pages
on:
  push:
    branches: [main]
permissions:
  contents: read
  pages: write
  id-token: write
jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v5
      - uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
      - id: deployment
        uses: actions/deploy-pages@v4
```

## 关于项目图片

网站中项目封面图使用的是 CDN 远程图片（`aka.doubaocdn.com`），在 GitHub Pages 上可以正常加载。如果你希望本地化所有图片资源，可以下载后放到 `assets/images/` 目录，并修改 JS 中对应的图片 URL。

## 路由说明

本网站是单页应用（SPA），使用 hash 锚点导航（`#hero`、`#works`、`#footer`），在 GitHub Pages 上可以直接工作，无需配置服务端路由回退。
