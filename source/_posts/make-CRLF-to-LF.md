---
title: 统一 Win 与 macOS 两台电脑上的博客文件换行符为 LF
date: 2025-09-02 08:34:04
tags: [折腾,blog]
---

日常会在两台电脑上更新这个博客，并通过 GitHub 仓库存储和同步博客源文件，一台系统是 win10，另一台是 macOS。大致的工作流是写完并 hexo d 之后，用 `git add` `git commit` `git push` 命令，将本地文件 push 到 GitHub 仓库里。在另一台电脑上写作前先 ```git pull``` 一下，以保证文件的一致性。

<!--more-->

在这种工作流之下，在 win10 上执行```git add``` 命令时，会返回一条提醒:

 ```warning: in the working copy of 'source/_posts/xxx.md', LF will be replaced by CRLF the next time Git touches it```

这条提醒的意思是： Git 发现一个文件 `source/_posts/xxx.md` 目前使用的是 Unix 风格的换行符（LF），但根据 win10 上 Git 的配置，它会在下一次操作这个文件时，自动把换行符转换成 Windows 风格的（CRLF）。

## 不同操作系统的换行符差异

计算机在表示“换行”这个动作时，使用了不同的特殊字符：

- **LF (Line Feed, `\n`)**：**Unix / Linux / macOS** 使用的换行符。可以理解为“换到下一行”。
- **CRLF (Carriage Return + Line Feed, `\r\n`)**：**Windows** 使用的换行符。可以理解为“光标回到行首（CR）并换到下一行（LF）”，就像老式打字机一样。

我遇到的情况就是这样：

- 在 **mac** 上编辑和保存文件，文件中的换行符是 **LF**。
- 把文件同步到了 **Windows** 电脑上。
- Windows 上的 Git 检测到了这个来自 macOS 的文件，并提示它将会根据本地（Windows）的习惯来处理换行符。



### Git 的角色：自动转换功能



为了解决跨平台协作时的换行符混乱问题，Git 提供了一个名为 `core.autocrlf` 的配置项，它能自动在提交和检出代码时转换换行符。

这个配置有三个主要的值：

- `true`：这是 **Windows 安装 Git 时的默认设置**。
  - 当**提交 (`git add`)** 文件时，Git 会自动将 CRLF 转换为 LF，再存入仓库。
  - 当**检出 (`git checkout` 或 `git clone`)** 文件时，Git 会自动将仓库中的 LF 转换为 CRLF，方便在 Windows 上查看和编辑。
- `input`：这是 **macOS 和 Linux 用户推荐的设置**。
  - 当**提交 (`git add`)** 文件时，Git 会将 CRLF 转换为 LF。
  - 当**检出 (`git checkout`)** 时，**不做任何转换**，保留仓库中的 LF。
- `false`：关闭自动转换功能。Git 不会理会换行符的差异，看到的是什么，提交的就是什么。这在跨平台协作时容易造成问题。

当我 `git add` 一个 LF 文件时，Git 告诉我：“虽然你现在把它加到暂存区了，但是这个文件在你的工作目录里还是 LF 格式。下次我再‘碰’到它（比如 `commit` 之后再 `checkout`），我就会把它变成 CRLF 格式。”

## 解决方法

尽管这个提醒不带来任何问题，不过每次遇到还是略微有点儿烦人，决定统一一下两个操作系统上的换行符风格。

### 方法一：统一两台电脑的 Git 配置

为了让 Git 的行为在我的所有设备上保持一致和清晰，可以手动设置 `core.autocrlf`。

1. **在 Win10上**，打开 Git Bash 或命令行，运行：

   ```
   git config --global core.autocrlf true
   ```

2. **在 macOS 上**，打开终端，运行：

   ```
   git config --global core.autocrlf input
   ```

这样配置后，无论在哪个系统上操作，提交到仓库的文件最终都会被统一为 LF 格式。Windows 会在本地为自动转换，而 Mac 则直接使用 LF，解决了跨平台问题。

### 方法二：使用 `.gitattributes` 文件

这是在团队协作中，或者希望项目本身就包含配置时最好的方法。它会覆盖个人的全局配置，确保所有使用该仓库的人都遵循同样的规则。

1. 在博客仓库的根目录下，创建一个名为 `.gitattributes` 的文件。

2. 在该文件中添加以下内容：

   ```
   * text=auto
   ```

3. 将 `.gitattributes` 文件 `add`, `commit`, `push` 到 `main` 分支。

**`\* text=auto` 的作用是：** Git 会自动判断哪些是文本文件。对于它认为是文本文件的内容，它会在 Windows 上启用 LF ↔ CRLF 的转换，而在 macOS/Linux 上则禁用转换，确保仓库中存储的是 LF。这基本上实现了和方法一同样的效果，但好处是这个配置是跟着项目走的，以后换了新电脑也无需重新配置。

为了一劳永逸，我选择了方法二，以后再换电脑、重装系统什么的，也不需要重新设置了。

