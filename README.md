# 🌍 旅行博客

基于 [Astro](https://astro.build) 构建的静态博客，用于记录旅行游记。

## 项目结构

```
travel-blog/
├── src/
│   ├── content/
│   │   ├── config.ts          # 内容集合配置
│   │   └── posts/             # 博客文章 (Markdown)
│   │       └── sicily-rome-2026.md
│   ├── layouts/
│   │   ├── BaseLayout.astro   # 基础布局
│   │   └── BlogPost.astro     # 文章页布局
│   ├── pages/
│   │   ├── index.astro        # 首页
│   │   ├── about.astro        # 关于页
│   │   └── posts/
│   │       ├── index.astro    # 文章列表
│   │       └── [slug].astro   # 文章详情页
│   └── components/            # 可复用组件
├── public/                    # 静态资源
├── astro.config.mjs          # Astro 配置
└── package.json              # 依赖
```

## 快速开始

### 1. 安装依赖

```bash
cd travel-blog
npm install
```

### 2. 本地开发

```bash
npm run dev
```

在浏览器中打开 http://localhost:4321

### 3. 构建

```bash
npm run build
```

构建后的静态文件位于 `dist/` 目录。

### 4. 预览构建结果

```bash
npm run preview
```

## 添加新文章

1. 在 `src/content/posts/` 目录下创建新的 `.md` 文件
2. 文件顶部添加 frontmatter：

```yaml
---
title: "文章标题"
pubDate: 2026-03-28
description: "文章简介"
location: "地点"
tags: ["标签1", "标签2"]
---
```

3. 使用 Markdown 格式编写正文

## 部署

### 方式 1: 静态托管平台（推荐）

- **GitHub Pages**: 推送到 GitHub 仓库，启用 Pages
- **Cloudflare Pages**: 连接 Git 仓库自动部署
- **Vercel**: 导入 Git 仓库自动部署
- **Netlify**: 拖拽 `dist/` 文件夹或使用 Git 集成

### 方式 2: 自有服务器

```bash
# 构建
npm run build

# 上传 dist/ 目录到服务器
rsync -avz dist/ user@your-server:/var/www/blog/
```

### 方式 3: Docker 部署

```dockerfile
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
```

## 自定义

### 修改主题颜色

编辑 `src/layouts/BaseLayout.astro` 中的 CSS 变量：

```css
:root {
  --color-bg: #fafafa;
  --color-text: #2d3748;
  --color-accent: #ed8936;  /* 主题色 */
  ...
}
```

### 添加导航链接

编辑 `src/layouts/BaseLayout.astro` 和 `src/pages/index.astro` 中的 nav 部分。

### 自定义域名

1. 在 `astro.config.mjs` 中设置域名：

```javascript
export default defineConfig({
  site: 'https://your-domain.com',
  ...
});
```

2. 在托管平台配置自定义域名

## 技术栈

- [Astro](https://astro.build) - 静态网站生成器
- [TypeScript](https://www.typescriptlang.org/) - 类型安全
- [MDX](https://mdxjs.com/) - Markdown 增强（可选）

## 许可证

MIT
