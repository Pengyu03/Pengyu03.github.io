---
title: "如何搭建本网站"
permalink: /setup/
---

# 本网站的搭建方法

本网站是通过 **Fork** [Acad Homepage](https://github.com/RayeRen/acad-homepage.github.io) 项目，并在此基础上进行个性化修改的。以下是我的具体搭建过程。

## 🚀 1. Fork 源代码

首先，我 Fork 了 [Acad Homepage](https://github.com/RayeRen/acad-homepage.github.io) 到我的 GitHub 账户，然后将其克隆到本地：

```sh
git clone https://github.com/我的GitHub用户名/acad-homepage.github.io.git
cd acad-homepage.github.io
```

## 🔧 2. 修改站点内容

在 `_config.yml` 文件中，我修改了以下内容以匹配我的个人主页需求：

```yaml
title: "Pengyu Xue"
description: "个人主页"
repository: "我的GitHub用户名/acad-homepage.github.io"
baseurl: ""
url: "https://xuepengyu.top"
```

同时，我根据需要修改了 `index.md`，调整了个人介绍、研究兴趣、论文列表等内容。

## 📂 3. 部署到 GitHub Pages

### 3.1 启用 GitHub Pages

在 GitHub 仓库的 `Settings > Pages` 中，我选择了 `main` 分支并保存。

### 3.2 配置 GitHub Actions 自动部署

为了确保每次提交都能自动构建和发布，我添加了 `.github/workflows/deploy.yml`：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3
      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.1'
      - name: Install dependencies
        run: bundle install
      - name: Build site
        run: bundle exec jekyll build
      - name: Deploy to GitHub Pages
        uses: JamesIves/github-pages-deploy-action@v4
        with:
          branch: gh-pages
          folder: _site
```

提交后，GitHub Actions 会自动构建并部署我的 Jekyll 站点。

## 🌍 4. 绑定自定义域名

### 4.1 购买域名

我在 **阿里云** 购买了域名 `xuepengyu.top`。

### 4.2 配置 DNS 解析

在 **阿里云域名管理** 中，我添加了如下 DNS 记录：

| 记录类型 | 主机记录 | 记录值 |
|----------|----------|--------|
| A | @ | `185.199.108.153` |
| A | @ | `185.199.109.153` |
| A | @ | `185.199.110.153` |
| A | @ | `185.199.111.153` |
| CNAME | www | `xuepengyu.github.io` |

### 4.3 在 GitHub Pages 绑定域名

在 `Settings > Pages` 中，我填写了 `xuepengyu.top` 作为 **Custom Domain**，并勾选 **Enforce HTTPS**。

## 🔐 5. 配置 SSL 证书

GitHub Pages 自动提供了 Let's Encrypt 证书，当我绑定域名后，它会自动启用 HTTPS。

如果没有自动生效，我会手动执行以下步骤：
1. 取消绑定域名，等待 10 分钟。
2. 重新绑定 `xuepengyu.top`。
3. 确保 **Enforce HTTPS** 选项已勾选。

## 🎨 6. 自定义主题与样式

为了个性化网站外观，我修改了 `_sass` 目录下的样式文件，并调整了 `assets/css/main.css`。

如果想要调整更多细节，可以直接修改 `_layouts` 和 `_includes` 目录下的 HTML 文件。

---
返回 [主页](/)
