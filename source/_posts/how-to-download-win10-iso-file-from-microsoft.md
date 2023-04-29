---
title: 如何从微软直接下载 win10 系统安装镜像
date: 2020-04-17 18:32:57
tags: 
---

如果你已经在使用 windows 设备，想要从微软的 [这个网站](https://www.microsoft.com/en-us/software-download/windows10) 下载 win10 安装文件的话，其会强制要求你下载其 MediaCreation 软件，而不是直接获取到 iso 镜像文件。

解决思路是更改浏览器的 user agent 骗网站认为你使用的是其它操作系统。

<!--more-->

打开微软系统镜像的 [下载网站](https://www.microsoft.com/en-us/software-download/windows10) ，按 F12 进入控制台，然后按右上角的三个圆点，在弹出的菜单中选择 more tools，然后点击选择 network conditions。

![](/1.png)

取消勾选 Select automatically ；

![](/2.png)

选择一个非 win 的系统及浏览器；



![](/3.png)

开着控制台直接刷新一次网页，此时下载的那里会让你选择版本，点击选择 win10，confirm 进入下一个页面选择语言，选择完成后 confirm 即可下载完整的 win10 iso 文件。

![](/4.png)



![](/5.png)