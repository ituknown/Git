# 列出 tags

```bash
git tag [-l|--list]
```

# 创建 tag

```bash
git tag [-m TagMessage] <TagName>
```

其中 `-m` 可以用于添加些简单的描述信息。如果在创建时忘记添加描述信息可以使用 `-f` 参数补充添加：

```bash
git tag -f [-m TagMessage] <TagName>
```

# 推送 tag 到远程

```bash
git push origin <TagName>
```

或者直接暴力点（不推荐）：

```bash
git push --tags
# 或
git push origin --tags
```

# 删除 tag

**1）** 删除本地 tag ：

```bash
git tag [-d|--delete] <TagName>
```

**2）** 删除删除远程 tag：

```bash
git push origin --delete <TagName>

# 或使用(不推荐)
git push origin :refs/tags/<TagName>
```

删除完成之后别忘记告诉其他小伙伴执行下如下命令更新下 tags：

```bash
git pull --prune --tags
```

# tag 重命名

```bash
git tag <NewTagName> <OldTagName>
```

删除本地 tag（可选）：

```bash
git tag -d <OldTagName>
```

删除远程 tag：

```bash
git push origin --delete <OldTagName>
```

推送新 tag 到远程：

```bash
git push origin <NewTagName>
```

最后别忘记告诉其他小伙伴执行下如下命令更新下 tags：

```bash
git pull --prune --tags
```

# 基于指定 tag 检出代码

```bash
git checkout <TagName>
```

检出之后通常会提示处于 `"detached HEAD"` 状态，因为 tag 相当于一个快照，是不能更改它的代码的。

所以最好的做法是基于指定 tag 拉一个新分支（不推送远程即可）：

```bash
git checkout -b <BranchName> <TagName>
```

