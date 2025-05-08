# Status 中文乱码

`git status` 严格意义上并不是乱码，而是使用8进制字符显示。使用下面的明来即可解决：

```bash
git config --global core.quotePath false
```

示例：

![git-status乱码-1639887120rGTyu1GBhT](https://ituknown.org/git-media/中文乱码/git-status乱码-1639887120rGTyu1GBhT.png)

# Commit/Log 乱码

使用下面的明来修改下字符集即可：

```bash
git config --global i18n.commitencoding utf-8
git config --global i18n.logoutputencoding utf-8
```