---
title: Hexo添加标签
date: 2023-05-29 21:27:15
tags: 博客
---

## 创建标签目录文件

```bash
hexo new page tags
```

打开 /source/tags/index.md

修改 type 的值为 "tags"

实例代码

```markdown
---
title: tags
date: 2023-05-29 12:18:26
type: "tags"
---
```

## 修改主题配置

笔者使用的是 next 主题

打开主题的配置文件找到 tags 选项, 打开即可

如下

```yml
menu:
  home: / || fa fa-home
  # about: /about/ || fa fa-user
  tags: /tags/ || fa fa-tags
  # categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
  # schedule: /schedule/ || fa fa-calendar
  # sitemap: /sitemap.xml || fa fa-sitemap
  # commonweal: /404/ || fa fa-heartbeat
```

将 tags 前的注释去掉即可
