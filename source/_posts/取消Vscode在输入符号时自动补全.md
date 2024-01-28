---
title: 取消Vscode在输入符号时自动补全
date: 2024-01-27 20:45:43
tags: Vscode
---

## 问题演示

![问题演示](https://raw.githubusercontent.com/See-YouL/MarkdownPhotos/main/202401272046475.png)

在此状态下输入/会直接自动补全, 如下图

![问题演示](https://raw.githubusercontent.com/See-YouL/MarkdownPhotos/main/202401272047507.png)

笔者想要达到的效果为可以正常输入/而不进行补全, 如下图

![问题演示](https://raw.githubusercontent.com/See-YouL/MarkdownPhotos/main/202401272048697.png)

## 解决方法

在设置->文本编辑器->建议, 取消勾选Accept Suggestion On Commit Character, 如下图所示

![解决方法](https://raw.githubusercontent.com/See-YouL/MarkdownPhotos/main/202401272051596.png)

