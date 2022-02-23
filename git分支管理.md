# 删除本地分支


```bash
$ git remote # 获取远程存储仓库
origin

$ git branch -d <BranchName> # 删除本地分支

# 之后如果想将远程分支也删除执行下面的命令即可:
$ git push origin -d <BranchName>
# 或使用下面的命令
$ git push --delete origin <BranchName>
```


# 删除远程分支


```bash
$ git remote # 获取远程存储仓库
origin

$ git push --delete origin <BranchName> # 删除远程分支

# 之后如果想将本地分支也删除就再执行下下面的命令即可:
$ git branch -d <BranchName>
```


# 分支切换


查看分支信息：

```bash
$ git branch -l
  VIM
* main
```


我当前在 main 分支上，如果想要切换到 VIM 分支可以使用下面的命令：

```bash
$ git switch VIM # 推荐

# 或

$ git branch VIM
```


# 基于指定分支创建分支


首先使用 `checkout` 或 `switch` 命令切换到指定分支。之后使用 `git branch`命令即可：

```bash
git branch [-b] branch_name
```


`-b` 参数指基于当前分支创建并直接切换到 `branch_name` 分支，如果不加该参数仅仅表示基于当前分支创建 `branch_name` 分支。

也就是说使用 `-b` 参数相当于下面两条命令合并执行：

```bash
git branch branch_name
git switch branch_name
```


# 基于指定版本创建分支


找出指定的版本SHA，然后使用如下命令即可创建分支：

```git
git branch <分支名> <SHA>
```


所谓 SHA 就是你的 git 提交日志ID，如下：

```git
git log
```

输出示例

```git
commit 907894ee34190bb4f1fca813bf2a975979054cd8
Author: xxxx <xxxx@mail.com>
Date:   Tue Sep 14 10:15:18 2021 +0800

    fix: 修复日志

commit 595d44718e56760fae7dc65623fb6c5ab8cfdd10
Author: xxxx <xxxx@mail.com>
Date:   Mon Sep 13 18:36:45 2021 +0800

    feat: xxxx
```


比如基于 595d44718e56760fae7dc65623fb6c5ab8cfdd10 版本创建 fix-bug 分支：

```git
git branch fix-bug 595d44718e56760fae7dc65623fb6c5ab8cfdd10
```


之后既可以将新创建的分支推送远程了：

```git
git push –-set-upstream origin fix-bug
```


# 修改分支名

分支名修改分为两种情况，要修改的分支已推送到远程和未推送到远程：

## 分支未推送远程


如果创建的分支还没有 push 到远程修改起来比较简单，直接使用如下命令进行修改即可：


```git
git branch -m OldBranchName NewBranchName
```


修改完成后直接将该分支推送到远程就万事大吉了。


```git
git push origin NewBranchName
```


但是如果我们要修改的分支名已经推送到了远程仓库改怎么修改呢？淡定，只需要按照如下步骤操作即可：


## 分支已推送远程


首先看下当前的仓库分支信息：


```git
git branch -av
```


其中 -a 是表示列出本地和远程所有分支（all）的意思，-v 可以理解为列出更多详细信息的意思。输出结果如下（示例结果）：


```git
* master                01a6944 Initial commit
  remotes/origin/HEAD   -> origin/master
  remotes/origin/dev    01a6944 Initial commit
  remotes/origin/master 01a6944 Initial commit
```


其中 * 表示我当前所处的分支即 `remotes/origin/HEAD`，注意看当前分支关联的远程分支是 `origin/master`，这就是本地分支和远程分支建立的联系（`--set-upstream-to`）。

从列出的分支可以看到远程有个 `dev` 分支，我现在要将该分支名修改为 `develop` ，现在看该怎么做。

首先切换到 `dev` 分支：


```git
git switch dev

或者

git checkout dev
```

之后使用 --delete 选项将远程 dev 分支删除：


```git
# 在删除之前最后先使用下面的命令拉取远程分支最新代码
# git pull origin dev

git push --delete origin dev
```



| **注意** |
| --- |
| 默认的远程仓库名是 `origin`，你可以使用 `git remote` 命令进行查看，如果你的远程仓库名不是 `origin` 将上面命令中的 origin 改为你的远程仓库名即可。 |



现在如果你使用 `git status` 命令可能会输出如下结果，该结果告诉你关联的远程分支 `origin/dev` 已经被删除。你可以手动执行命令
`git branch --unset-upstream` 进行取消关联，不过没啥必要，因为之后我们需要 `--set-upstream-to` 重新关联远程分支。

```git
On branch dev
Your branch is based on 'origin/dev', but the upstream is gone.
  (use "git branch --unset-upstream" to fixup)

nothing to commit, working tree clean
```


现在使用 `git branch -m OldBranchName NewBranchName` 命令将本地分支名 `dev` 修改为 `develop` ：

```git
git branch -m dev develop
```


之后再将修改后的分支 push 到远程：

```git
git push origin develop
```


然后使用 `--set-upstream-to` 参数将本地分支(`develop`)和远程 `origin/develop` 分支建立关联关系：

```git
git branch --set-upstream-to=origin/develop
```


现在再使用 `git status` 命令查看输出信息，从输出结果中可以看出已经关联到远程分支 `origin/develop`：

```git
On branch develop
Your branch is up to date with 'origin/develop'.

nothing to commit, working tree clean
```


这样，一次完成的远程分支名称就修改完成了🥳🥳🥳🥳~
