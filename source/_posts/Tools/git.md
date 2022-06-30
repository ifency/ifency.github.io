---
title: Git的使用
date: 2022-06-30 10:21:16
tags: Tools
---

参考网址：

- [Git commands nobody has told you](https://bootcamp.uxdesign.cc/git-commands-nobody-has-told-you-cd7025bea8db)

## add 和 commit 合并为一个命令

```shell
git commit -am "commit message"
```

## 从另一个分支复制到本地分支

```shell
git checkout <branchA>
git rebase <branchB>

```

## 改动后需要合并到上一个 commit

```shell
git add .
git commit --admend --no-edit
```

## 回退到指定版本（针对某个文件）

```Shell
git checkout HEAD -- <文件名>
```

## 忽略不想提交的文件

```shell
git update-index --assume-unchanged <文件名>
```

## 恢复跟踪的文件

```shell
git update-index --no-assume-unchanged fileName
```

## fork 后与原仓库同步

```Shell
# 抓取原仓库的更新
git fetch upstream

# 切换到需要更新的分支
git checkout master

# 合并远程的master分支
git merge upstream/master

# 推送到fork后的仓库
git push
```

参考网址：https://github.com/selfteaching/the-craft-of-selfteaching/issues/67

## 解决合并冲突的问题

```shell
git cherry-pick <hash>
```

参考网址：https://cubox.pro/web/reader/ff8080817f639d63017f6df12e851ada

## 暂存代码

针对 不想提交代码，需要切换分支

```shell
git stash
```

之后某个分支修好了，再换回原来的分支并且恢复代码

```shell
git stash apply
```

举 🌰：

```shell
# 保存当前未commit的代码
git stash

# 保存当前未commit的代码并添加备注
git stash save "备注的内容"

# 列出stash的所有记录
git stash list

# 删除stash的所有记录
git stash clear

# 应用最近一次的stash
git stash apply

# 应用最近一次的stash，随后删除该记录
git stash pop

# 删除最近的一次stash
git stash drop
```
