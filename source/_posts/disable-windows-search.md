---
title: 关闭 Windows 的搜索服务
date: 2025-09-05 08:25:48
tags: [折腾, software]

---

工地配发的电脑是一台几年前生产、 经历过好几任主人的 thinkpad T14，处理器型号为 11th Gen Intel(R) Core(TM) i7-1165G7，尽管系统安装的是已经比较精简的 Windows 10 企业版 LTSC，但使用起来依然比较卡顿。

<!--more-->

考虑到这台设备还没走到其主动报废年限，我不能申请新的设备，为了优化办公体验只能自行寻找一些优化点，关掉系统的搜索服务是今天的突发奇想。

其实不论是在 Windows 还是 macOS 系统上，我都很少用系统自带的搜索功能，主要是不好用。Windows 上通常会用启动器软件来搜索应用程序，配合 everything 搜索文件，macOS 自带的 spotlight 虽然也不错，不过第三方软件还是更好。

## 关闭方法

关闭方法比较简单，按`win+R`，输入`services.msc`，在弹出的窗口里找到`windows search`，双击该服务，点击`停止`即可。

![](/services_msc.png)

![](/disable_search.png)

## 替代工具

启动器目前用的是 [Flow Launcher](https://github.com/Flow-Launcher/Flow.Launcher)，文件搜索服务使用 everything。macOS 上使用的 [Raycast](https://www.raycast.com/) 正在筹备 Windows 版，推出后应该会转过去。
