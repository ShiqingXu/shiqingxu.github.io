---
title: 把 Cloudflare R2 Bucket 作为博客图床
date: 2025-09-09 08:35:12
tags: [blog, 折腾]
---

这个 Hexo 博客是搭建在 GitHub Pages 上的，没有使用单独的图床，而是在创建博客文件时在同一个目录下自动创建一个同名的 assets 文件夹，图片存放在这个文件夹里，与博客的 md 文件一同托管在 Github 上。这种方案虽然方便，不过有两个问题，一是 Github 在中国大陆的访问速度非常缓慢，图片加载困难，二是随着时间的推移，博客出库的体积会越来越大，`clone`,`push`和`deploy`等操作都会比较耗时。故决定折腾一下图床。

<!--more-->

## 独立图床的优势

**一劳永逸的解决方案**：一次配置，永久享受。再也不用担心图片加载速度，也不用关心底层实现。

**资产的集中与复用**：所有图片都在一个地方，清晰明了。任何文章都可以方便地引用任何一张图片，实现了资源的**全局复用**。

**主仓库永远轻量**：博客仓库将保持干净和高效，以后部署和迁移都非常方便。

**专业的工作流**：这是业界公认的最佳实践。将代码（Markdown）和静态资源（图片）分离管理，符合现代 Web 开发的普遍原则。

主流的方案是 jsDeliver 和 Cloudflare R2，对比了一下，出于减少维护工作的考虑，选择了后者。

### 设置过程

### 创建 R2 Bucket

登录 Cloudflare 账户，在左侧菜单找到并进入 R2。

![](https://img.xushiqing.xyz/2025/09/cloudflare-dashboard-R2.png)



创建 bucket

![](https://img.xushiqing.xyz/2025/09/cloudflare-create-bucket.png)

输入 Bucket name，点击 `create bucket`完成创建

![](https://img.xushiqing.xyz/2025/09/cloudflare-create-bucket-name.png)

创建完成之后，在设置中绑定一个自定义域名，可以使用已经由 cloudflare 管理的域名的子域名，我在这里用了博客域名的子域名。

![](https://img.xushiqing.xyz/2025/09/cloudflare-bucket-custom-domains.png)

创建完成之后效果如图，就可以通过网络访问这个 Bucket 里的资源了。

![](https://img.xushiqing.xyz/2025/09/cloudflare-bucket-custom-domains-added.png)

## 

至此已经可以通过 R2 来托管图片，实现存储与分发的分离，加速博客图片的加载速度。

## 后续折腾计划 

不过手动上传图片粘贴链接还是有一些问题。

一是操作比较麻烦，计划后面设置一下 [PicGo](https://github.com/Molunerfinn/PicGo) ，简化图片上传的工作流；

二是可维护性可能存在问题，比如后续更换了图床的地址之类的，需要逐个图片替换链接。尝试在 _config.yml 里设置图床地址以增强可维护性，但失败了，尚未找到原因后面有时间再研究吧。

