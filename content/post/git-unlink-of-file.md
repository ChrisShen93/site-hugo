---
title: "Git Unlink of File"
date: 2018-10-26T09:23:24+08:00
---

每天到公司打开电脑的第一件事，是拉取同事的最新代码：

```shell
git pull
```

然而今天却出了点问题（Windows下），git pull 没有成功，提示如下：

> Unlink of file '.git/objects/pack/pack-****.pack' failed. Should I try again? (y/n)

在 stackoverflow 上搜到相关问题，说是因为有其他程序占用了文件。可以设置 git 的一个新的环境变量 `GIT_ASK_YESNO` 来避免 Windows 上出现 `unlink` `rename` `rmdir` 后出现的类似问题。

由于不知道设置该变量后会采用 yes 还是 no，因此采取了万（wu）能（chi）的 重启/注销 大法。然而问题依旧。

最后使用了下面两行命令解决：

```shell
git gc --auto
git repack -d -l
```

上面的两行代码在 git 文档中有解释

> With this option, git gc checks whether any housekeeping is required; if not, it exits without performing any work. Some git commands run git gc --auto after performing operations that could create many loose objects. Housekeeping is required if there are too many loose objects or too many packs in the repository.
> If the number of loose objects exceeds the value of the gc.auto configuration variable, then all loose objects are combined into a single pack using git repack -d -l. Setting the value of gc.auto to 0 disables automatic packing of loose objects.

[原文地址](https://git-scm.com/docs/git-gc#git-gc---auto)
