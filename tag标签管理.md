# 查看标签

**列出所有标签：**

```bash
$ git tag
```

输出示例：

```bash
$ git tag

v0.0.1-establish
v0.0.2-broadcast
```

**列出所有标签及说明：**

`git tag` 虽然能够列出所有 tag，但是不显示注释信息，仅仅会列出标签名。想要列出标签的注释信息可以使用下面的命令：

```bash
$ git tag -n<num>
```

其中 `<num>` 表示列出指定数量的标签，是可选的。如果不指定就会列出所有标签。

输出示例：

```bash
$ git tag -n

v0.0.1-establish The client establishes a connection with the server and communicates correctly 🚀
v0.0.2-broadcast Simple text communication between multiple clients
```

可以看到除了标签还显示了标签的注释信息。

**标签匹配：**

有的时候标签可能太多，这种情况下还继续使用 `git tag` 或 `git tag -n` 命令来查看标签就显得没那么友好了。通常的做法是使用匹配符来过滤指定的标签，命令如下：

```bash
$ git tag [-l|--list] <pattern>
```

其中 `<pattern>` 表示的就是具体的匹配规则，是可选的。如果不指定匹配规则该命令就与 `git tag -n` 等价。

比如我想要匹配带 `establish` 关键字的标签：

```bash
$ git tag -l "*establish*"

v0.0.1-establish
```

**查看指定标签信息：**

前面的命令都是用于列出标签信息，如果想要查看具体标签的提交信息可以使用 `show` 命令：

```bash
$ git show <TagName>
```

`show` 命令会显示具体的 commit 信息，在实际中很有用。示例：

```bash
$ git show v0.0.1-establish

tag v0.0.1-establish
Tagger: mingrn97 <mingrn97@gmail.com>
Date:   Tue May 31 16:00:52 2022 +0800

The client establishes a connection with the server and communicates correctly 🚀

commit effcd6f0f4e6e544dae93cfd57fe40d1feaa1999 (tag: v0.0.1-establish, tag: show)
Author: mingrn97 <mingrn97@gmail.com>
Date:   Sun May 29 13:29:57 2022 +0800

    remove main.go

....
```

# 创建标签

创建标签的命令如下：

```bash
git tag [-f] [-m <msg>] <tagName> [<commit>]
```

`-f` 表示强制执行的意思，通常用于覆盖修改。

`-m` 用于在创建或修改标签时添加些简单的注释信息（如果在创建时忘记添加描述信息可以使用 `-f` 参数补充）。

`<tagName>` 就是你要创建的标签名了。

`<commit>` 基于指定 commit 创建标签，默认情况下是基于最新的一次提交创建标签。如果想要基于指定的 commit 创建标签就给 commitId 加上即可。

其中 `-m` 可以用于添加些简单的描述信息。如果在创建时忘记添加描述信息可以使用 `-f` 参数补充添加：

**基于最新一次提交创建标签：**

```bash
$ git tag example_tag_name
```

**基于指定提交创建标签：**

可以先使用下面的命令查看历史提交记录找到具体的 commit：

```bash
$ git log --pretty=oneline --abbrev-commit
```

示例：

```bash
e8e81e5 (HEAD -> main, origin/main, origin/HEAD) pref: 代码优化
22987c4 feat: colorized🌈
607484f feat: client broadcast 📣
effcd6f remove main.go
f73f4a3 package manage
aa6039e readme
b1805e2 remove workflow
b477753 github workflows
44e62a5 pred: import
98278f6 feat: 完善客户端和服务器消息通信
385bedc init go im repository
bd61a80 Initial commit
```

找到具体的 commit 之后就可以基于指定的 commit 打标签了（比如 effcd6f 这次提交）：

```bash
$ git tag example_tag_name effcd6f
```

**添加注释信息：**

在创建标签时可以使用 `-m` 参数添加些简单的注释信息：

```bash
$ git tag -m "简单的注释信息" example_tag_name
```

但是如果在创建是忘记添加注释信息了，可以在创建完成后再配合 `-f` 参数来添加：

```bash
$ git tag -f -m "简单的注释信息" example_tag_name
```

# 推送标签到远程服务器

命令如下：

```bash
$ git push origin <TagName>
```

或者直接暴力点（不推荐）：

```bash
git push --tags
# 或
git push origin --tags
```

# 删除标签

**删除本地标签：**

```bash
$ git tag [-d|--delete] <TagName>
```

**删除删除远程标签：**

```bash
$ git push origin --delete <TagName>
```

删除完成之后别忘记告诉其他小伙伴执行下如下命令更新下 tags：

```bash
$ git pull --prune --tags
```

# 标签重命名

如果因为手速太快导致标签名拼写错误，可以再创建完成之后再进行修改：

```bash
$ git tag <NewTagName> <OldTagName>
```

然后再给本地的（可选）和远程老标签删掉：

```bash
# 删除本地(可选)
$ git tag -d <OldTagName>

# 删除远程
$ git push origin --delete <OldTagName>
```

之后再给新的标签推送到远程：

```bash
$ git push origin <NewTagName>
```

最后别忘记告诉其他小伙伴执行下如下命令更新下 tags：

```bash
$ git pull --prune --tags
```

# 基于指定标签检出代码

```bash
$ git checkout <TagName>
```

检出之后通常会提示处于 `"detached HEAD"` 状态，因为 tag 相当于一个快照，是不能更改它的代码的。

所以最好的做法是基于指定 tag 拉一个新分支（不推送远程即可）：

```bash
git checkout -b <BranchName> <TagName>
```

