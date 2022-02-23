这个问题最容易下 windows 平台下出现，因为 Git 对文件名有4096个字符的限制。

因为在Windows上使用 msys 编译git。它使用旧版本的 Windows API，文件名限制为260个字符。这是 msys 的限制，而不是 git 的限制。在 github 上有有关该问题的讨论：

[https://github.com/msysgit/git/pull/110](https://github.com/msysgit/git/pull/110)

解决该问题可以直接使用下面的命令：

```
git config <ConfigFileLocation> core.longpaths true
```
ConfigFileLocation 可选值：

- `--global`：全局配置
- `--system`：系统级别配置
- `--local`：指定仓库级别配置
