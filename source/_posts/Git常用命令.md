---
title: Git常用命令
date: 2024-01-17 01:53:17
tags: Git
---

## 初始化流程

```shell
git init
git add <file-name>
git commit -m "commit message"
git branch -M main
git remote add origin <repository URL>
git push -u origin main
```

1. git add README.md:
 - 这个命令将 README.md 文件添加到暂存区（staging area）。Git 的暂存区是一个准备好的下一次提交的文件列表。这意味着 README.md 文件的更改将被包含在下一次提交中。
2. git commit -m "first commit":
 - 这个命令将暂存区中的更改提交到本地仓库。-m 后面跟随的 "first commit" 是提交信息，用于描述这次提交的内容或目的。
3. git branch -M main:
 - 这个命令用于将当前分支重命名为 main。Git 默认的主分支名是 master，但近年来，main 开始被广泛采用作为默认主分支的名称。-M 参数表示强制重命名，即使目标分支名已存在。
4. git remote add origin <repository URL>:
 - 这个命令用于添加一个新的远程仓库，并将其命名为 origin。在 Git 中，origin 是远程仓库的默认名称。
5. git push -u origin main:
 - 这个命令将本地的 main 分支推送到名为 origin 的远程仓库。-u 参数意味着将本地的 main 分支和远程的 main 分支关联起来，以后可以简化推送或拉取命令。

## 提交部分命令

### 添加文件到暂存区

**添加指定文件到暂存区**

```shell
git add <file>
```

**添加当前目录下所有更改到暂存区**

```shell
git add .
```

### 提交更改

将暂存区的更改提交到本地仓库.每个提交都需要一个提交信息，描述所做的更改.

```shell
git commit -m "commit message"
```

### 连接远程仓库

将本地仓库与远程仓库关联。通常，远程仓库的默认名称是 origin

```shell
git remote add origin <repository URL>
```

### 推送更改到远程仓库

将本地分支的更改推送到远程仓库。例如，推送到主分支通常是 git push origin main

```shell
git push origin <branch>
```

## 拉取部分命令

### 拉取远程仓库的更改

从远程仓库拉取最新的更改并合并到本地分支

```shell
git pull origin <branch>
```

## 克隆部分命令

### 克隆远程仓库

克隆一个远程仓库到本地

```shell
git clone <repository URL>
```
