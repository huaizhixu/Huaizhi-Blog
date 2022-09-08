# [git使用笔记](https://github.com/huaizhixu/Huaizhi-Blog/issues/5)

## Git本次修改合并到上次提交
有时候为了减少提交日志，并且添加的内容是与上次的内容属于同一个提交内容的，为了好维护，会将本次的提交追加到上次的提交中。使用git 命令如下：
```
git add .                           (添加提交内容)
git commit --amend        (追加到上次提交)#会通过core.editor指定的编辑器进行编辑
git commit --amend --no-edit      #不打开命令行，直接提交
```
## 其它使用
