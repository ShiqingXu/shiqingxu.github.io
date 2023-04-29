---
title: 为GitHub Pages 自定义域名开启 Enforce HTTPS
date: 2023-04-22 13:17:59
tags: hexo
---

近期重新买回了之前用过的博客域名 xushiqing.xyz，通过Cloudflare 进行DNS解析。但在绑定到我的 github pages 博客时始终无法勾选 Enforce HTTPS 选项。

提示为：

```
Unavailable for your site because your domain is not properly configured to support HTTPS。
```

解决方案如下：

<!--more-->

1. 在 github pages 设置页面删掉自定义域名；
2. 到 Cloudflare 配置页面关闭CDN功能，即 Proxy status 状态显示为仅DNS；
3. 在 github pages 设置页面重新添加域名。

如上操作之后，Enforce HTTPS应当已经可以勾选，如仍不能勾选，并且提示

```
Not yet available for your site because the certificate has not finished being issued
```



则等待一段时间（通常为24小时内），将可以正常勾选。



