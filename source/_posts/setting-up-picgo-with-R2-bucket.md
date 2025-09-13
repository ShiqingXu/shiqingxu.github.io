---
title: 使用 PicGo 配合 Cloudflare R2 优化博客图片上传体验
date: 2025-09-13 20:34:19
tags: [software, 折腾]

---

上次在 [把Cloudflare R2 Bucket 作为博客图床](https://xushiqing.xyz/2025/09/09/cloudflare-R2-as-blog-image-hosting/) 中记录了图片托管方案的变更，切换到这个方案之后图片的载入速度确实有了质的提升，不过写作过程中直接在 R2 Bucket 页面上上传图片、获取链接非常不方便，所以需要用到 [PicGo](https://github.com/Molunerfinn/PicGo) 这个软件来优化图片上传的流程。

<!--more-->

## 安装 PicGo 及 S3 插件

[PicGo](https://github.com/Molunerfinn/PicGo) 本体并不直接支持 Cloudflare R2，但是可以通过 [picgo-plugin-s3](https://github.com/wayjam/picgo-plugin-s3) 这个插件来获得支持。下载安装好 PicGo 之后，先去插件设置页面搜索并安装 S3 插件。不过这第一步就遇到了问题，这个搜索框里是搜索不到任何插件的。从网上的讨论来看，这个问题已经存在很久了，于是转为手动安装。

在终端里进入`C:\Users\yourusername\AppData\Roaming\picgo`，运行`npm install picgo-plugin-s3`即可安装。

安装完成后重启 PicGo，即可在左侧的`插件设置`里看到 Amazon S3 插件了。

![](https://img.xushiqing.xyz/2025/09/1757767926-picgo-plugin-dashboard)

## 配置 Bucket 访问 API

要实现通过 PicGo 上传图片，需要先为 Bucket 配置好访问的 API。

首先进入 Bucket 的管理面板，点击右侧的 API，在弹出的下拉列表中点击 `Manage API Tokens`。

![](https://img.xushiqing.xyz/2025/09/1757769099-r2-manage-api-tokens)

进去之后，点击右侧的 `Create Account API token`。

![](https://img.xushiqing.xyz/2025/09/1757769294-r2-create-api-token)

进入之后设置一个 Token name，权限选择读写，然后指定要使用的 Bucket ，最后点击右下角的`Create Account API token`。

![](https://img.xushiqing.xyz/2025/09/1757769491-r2-create-account-api-token)

在接下来的页面中会展示几个需要填到 PicGo 中的字段，只会展示一次，可以先复制下来。

分别是：

`Access Key ID`

`Secret Access Key`

`jurisdiction-specific endpoints`

最后点击finish即可。

![](https://img.xushiqing.xyz/2025/09/1757771712-r2-account-api-token-keys)

## 设置 PicGo

接下来打开 PicGo，点击 Amazon S3 插件，填入刚才获取到的三个字段。

`应用密钥 ID` 即 `Access Key ID`

`应用密钥` 即 `Secret Access Key`

 `自定义节点` 即 `jurisdiction-specific endpoints`

![](https://img.xushiqing.xyz/2025/09/1757768517-s3-plugin-setting-1)

![](https://img.xushiqing.xyz/2025/09/1757770319-s3-plugin-setting-2)

桶名就填用于存在图片的Bucket的名字。

自定义输出URL，填写之前为 Bucket 设置的自定义域名，后面加一个 `/{path}`,例如这样：

`https://img.youdomin.com/{path}`，其中 `{path}` 部分会被自动替换为设置的上传文件路径。

上传文件路径的路径取决于自己的偏好，我选择以月为单位组织图片文件夹，故设置为

`{year}/{month}/{timestamp}-{fileName}`

这种格式，上传时会自动获取 `年/月/自动生成时间戳-文件名`的信息，并作为链接的后缀。

设置好之后点击确定，并设置为默认图床。

之后上传的图片在 Bucket 面板里展示的文件名如图，其中最左边的数字部分是时间戳，这样即使上传同样文件名的图片，也会有不同的名字，不会产生后一张图片踢掉前一张的情况。

![](https://img.xushiqing.xyz/2025/09/1757771014-r2-pic-timestamp)

设置完成，就可以通过 PicGo 上传图片，上传完自动获取图片链接到剪切板，可以直接贴到文章中，写作流程顺畅许多。
