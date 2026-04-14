# jackx-svg.github.io

这是末羽的个人博客源码仓库，使用 Hexo + Butterfly 主题，并通过 GitHub Actions 发布到 GitHub Pages。

线上地址：

```text
https://jackx-svg.github.io/
```

## 常用流程

第一次在本地打开项目，先安装依赖：

```bash
npm ci
```

本地预览：

```bash
npm run server
```

默认预览地址通常是：

```text
http://localhost:4000/
```

生成静态文件并检查是否能构建成功：

```bash
npm run build
```

发布到线上：

```bash
git pull --ff-only
git add .
git commit -m "Update blog"
git push origin main
```

推送到 `main` 后，GitHub Actions 会自动安装依赖、构建 Hexo、上传 `public` 目录，并发布到 GitHub Pages。不需要再运行 `hexo deploy`。

## 写新文章

创建文章：

```bash
npx hexo new post "文章标题"
```

生成的文件会在：

```text
source/_posts/文章标题.md
```

文章开头的 front matter 建议这样写：

```markdown
---
title: "文章标题"
date: 2026-04-14 20:00:00
updated: 2026-04-14 20:00:00
categories:
  - 科研
tags:
  - 拓扑物态
  - 强化学习
description: "一句话说明这篇文章写什么。"
---
```

写完后按这个顺序处理：

```bash
git pull --ff-only
npm run server
npm run build
git add source/_posts source/img package.json package-lock.json _config.yml _config.butterfly.yml source/css
git commit -m "Add post: 文章标题"
git push origin main
```

如果只是写文章，通常只会改 `source/_posts/`。如果同时加图片，也会改 `source/img/`。

## 图片管理

通用图片放在：

```text
source/img/
```

文章配图建议放在：

```text
source/img/posts/
```

Markdown 中这样引用：

```markdown
![图片说明](/img/posts/example.jpg)
```

不要上传身份证、学生证、家庭住址、聊天截图、带二维码的收款码或私人联系方式截图。

## 文件结构

```text
.github/workflows/deploy.yml   GitHub Pages 自动部署流程
_config.yml                    Hexo 全站配置
_config.butterfly.yml          Butterfly 主题配置
source/_posts/                 博客文章
source/about/index.md          关于页面
source/img/                    头像、favicon、文章图片等静态图片
source/css/custom.css          本站自定义样式
scaffolds/post.md              新文章模板
themes/butterfly/              Butterfly 主题源码
package.json                   npm 脚本和依赖声明
package-lock.json              锁定依赖版本
README.md                      维护说明
```

这些内容不要提交：

```text
node_modules/
public/
.deploy_git/
db.json
_backup/
*.log
```

## 隐私和安全

当前仓库是公开仓库，别人可以 clone 或 fork，但不能直接修改你的博客，除非他拥有仓库写权限，或者你把他的 PR 合并进 `main`。

维护时注意：

- 不提交 GitHub PAT、云服务密钥、服务器密码、域名服务商密钥。
- 不上传微信二维码、付款码、身份证件、聊天截图等隐私图片。
- 不随便合并陌生 PR。
- 部署 workflow 只监听 `main` 分支的 push 和手动触发，不监听陌生 PR 自动部署。

## 访问速度

这套部署解决的是发布流程和仓库结构问题，不会从根本上解决国内访问 GitHub Pages 偶尔慢或不稳定的问题。

已经做过的轻量优化：

- 关闭微信打赏二维码。
- 关闭第三方分享按钮。
- 关闭不蒜子访问统计。
- 自定义样式放在本地 `source/css/custom.css`，不额外加载外部样式服务。

如果后续要明显改善国内访问速度，通常需要：

- 绑定自己的域名。
- 使用国内或香港方向的 CDN。
- 如果使用中国大陆 CDN，通常还要处理域名备案。

在没有自定义域名和 CDN 前，`github.io` 的访问速度主要取决于 GitHub Pages 本身的网络质量。
