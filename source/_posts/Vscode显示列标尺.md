---
title: Vscode显示列标尺
date: 2024-02-15 22:41:04
tags: Vscode
---

## 需求说明

为了确保列数在80个字符以内，我们需要在编辑器中显示列标尺。

## 操作方法

在Vscode设置中输入editor.rulers, 然后点击"在settings.json中编辑"，找到"editor.rulers"，
输入80即可。

![Vscode设置](https://raw.githubusercontent.com/See-YouL/MarkdownPhotos/main/202402152243203.png)

![Vscode设置](https://raw.githubusercontent.com/See-YouL/MarkdownPhotos/main/202402152245556.png)

```json
"editor.rulers": [
        80
    ]
```
