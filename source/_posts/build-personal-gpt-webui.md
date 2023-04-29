---
title: 部署私人 Chat-GPT Web UI
date: 2023-04-12 16:32:38
tags:
---

Chat-GPT不出意外地变得难以访问，不过好在有 API KEY 的话，还是有办法绕过限制。

有人做了个[一键部署的项目](https://github.com/Yidadaa/ChatGPT-Next-Web)，可以在 Vercel 上部署一个私人的 Web UI，这里的一键是真的一键（点击 Deploy 即可），因此过程没啥好写的，不过有一些需要注意的点。

<!--more-->

#### 更新问题

如果直接一键部署，可能会发现总是提示“存在更新”的问题，这是由于 Vercel 会默认创建一个新项目而不是 fork 原项目，这会导致无法正确地检测更新。 

解决方法如下：

- 删除掉原先的仓库；
- 使用页面右上角的 fork 按钮，fork 原项目；
- 在 Vercel 重新选择并部署，[请查看详细教程](https://github.com/Yidadaa/ChatGPT-Next-Web/blob/main/docs/vercel-cn.md#如何新建项目)。

#### API KEY 与 Access Code

按照上述方法重新部署，需要自己手动在环境变量里添加自己的 API KEY，access code 可加可不加，不加的话存在 token 被迅速恶意消耗光的风险。

![api_key](/api_key.jpg)

#### 使用私人域名转发

部署完成之后，有很大概率还是不能直接访问，这时需要一个没有被墙的域名来转发。我去namecheap买了一个，价格十分公道，只花了1.16刀。

到 vercel 的项目管理页面，按照页面提示添加domains并把域名的DNS解析过来即可。

![domains](/domains.jpg)

至此应该就可以无障碍访问了。

#### 一点感想

又是一个全世界大部分地区人民都能无障碍用上，而某些地区的人民需要跨越重重障碍才能用上的服务。

以及，能够部署这个服务的人，其实也恰恰是用不到该服务的人。给亲朋好友用倒是挺不错的。

---



