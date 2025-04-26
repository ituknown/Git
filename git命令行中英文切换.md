Mac 升级之后，发现 git 命令行变成中文了：

<div style="text-align: left;">
  <img src="https://ituknown.cn/git-media/LANG/git-status-chinese.png" alt="git-status-chinese.png" width="500" />
</div>

显得好low......

实际上，解决方法很简单，使用 LANGUAGE 或 LANG 设置下语言环境即可：

```bash
export LANGUAGE=zh_CN.UTF-8 # 中文
export LANGUAGE=en_GB.UTF-8 # 英国英语
export LANGUAGE=en_US.UTF-8 # 美国英语
```

也可以使用 LANG 设置语言环境，不过 LANG 级别比 LANGUAGE 要低一些。如果直接将上面的 export 写到 profile 文件中会影响到整个系统的（命令行）语言环境，所以我推荐的做法是使用 alias 命令，在 git 命令前设置本次 session 语言环境：

```bash
alias git='LANG=en_GB.UTF-8 git'
```

然后将这条 alias 写到配置文件即可，效果如下：

<div style="text-align: left;">
  <img src="https://ituknown.cn/git-media/LANG/git-status-english.png" alt="git-status-english.png" width="500" />
</div>