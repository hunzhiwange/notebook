# 通过 git fsck --lost-found 恢复 git reset --hard 删除的文件

有一次在本地修改代码的时候，一不小心就使用 `git reset --hard`,然后就杯具了，辛辛苦苦写好的代码不见了。当时特别的好绝望啊，不过总是能找到办法的。

如果你没有 `git commit` 你的本地修改，曾经通过 `git add` 命令追踪过这些文件,你可以试试使用 `git fsck --lost-found` 来恢复这些文件。

## 查找方法

你可以按照下面的方法来查找文件，还是挺方便的，然后一个个文件查找内容，找回你自己的代码。

```
git fsck --lost-found // 找到文件
cd .git/lost-found/other // 进入目录
find .git/objects -type f | xargs ls -lt | sed 60q  // 搜索最近被 add 到本地仓库的 60 个文件
```

## 数据恢复软件

如果确实找不到，可以通过 `易我数据恢复向导 2.0` 试试，以前还可以恢复很多文件的，实在不行的时候。

## 参考文章

* http://www.tuicool.com/articles/mqm2uiF
