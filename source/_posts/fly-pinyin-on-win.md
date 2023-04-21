---
title: 为微软拼音输入法添加小鹤双拼支持
date: 2023-04-21 18:28:18
tags:
---

两个简单的方案。

方案一：

可新建一个文本文档，将以下内容复制进去，保存为.reg文件，并双击运行即可。

```
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Microsoft\InputMethod\Settings\CHS]
"Enable Cloud Candidate"=dword:00000000
"Enable Dynamic Candidate Ranking"=dword:00000001
"EnableExtraDomainType"=dword:00000001
"Enable self-learning"=dword:00000001
"EnableSmartSelfLearning"=dword:00000001
"EnableLiveSticker"=dword:00000000
"Enable EUDP"=dword:00000001
"Enable Double Pinyin"=dword:00000001
"UserDefinedDoublePinyinScheme0"="小鹤双拼*2*^*iuvdjhcwfg^xmlnpbksqszxkrltvyovt"
"DoublePinyinScheme"=dword:0000000a

```





方案二：

手动添加注册表项目。

1. 打开注册表编辑器；
2. 打开以下路径：`HKEY_CURRENT_USER\Software\Microsoft\InputMethod\Settings\CHS`
3. 新建字符串值，字符串名称为：`UserDefinedDoublePinyinScheme0`，值为：`2*^*iuvdjhcwfg^xmlnpbksqszxkrltvyovt`
4. 退出后进入微软拼音设置，即可看到小鹤双拼方案已存在，选择保存即可。
