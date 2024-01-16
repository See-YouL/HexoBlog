---
title: Git代理命令
date: 2024-01-14 02:42:12
tags: Git
---

## Git设置代理命令

```shell
git config --global http.proxy "http://127.0.0.1:10807"
git config --global https.proxy "http://127.0.0.1:10807"
```

注意: **代理的端口号需要根据实际情况进行调整**

## Git清除代理命令

```shell
git config --global --unset http.proxy
git config --global --unset https.proxy
```

