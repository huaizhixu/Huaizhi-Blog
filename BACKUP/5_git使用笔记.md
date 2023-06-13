# [git使用笔记](https://github.com/huaizhixu/Huaizhi-Blog/issues/5)

## Git本次修改合并到上次提交
有时候为了减少提交日志，并且添加的内容是与上次的内容属于同一个提交内容的，为了好维护，会将本次的提交追加到上次的提交中。使用git 命令如下：
```
git add .                           (添加提交内容)
git commit --amend        (追加到上次提交)#会通过core.editor指定的编辑器进行编辑
git commit --amend --no-edit      #不打开命令行，直接提交
```
## 将Git默认编辑器更改为vim
查看Git逻辑变量
```
git var -l
将当前Git默认编辑器更改为vim
$ git config core.editor vim
将全局Git默认编辑器更改为vim
$ git config --global core.editor vim


```
## 通过sshkey的方式拉取GitHub代码报错：
```
kex_exchange_identification: Connection closed by remote host fatal: Could not read from remote repository
```
通过查阅资料，这个报错其实跟梯子有关~但是不用梯子，速度感人！
## 解决
```
# 编辑 ~/.ssh/config 文件
Host github.com
    CheckHostIP no  # Warning: Permanently added the ECDSA host key for IP address ' "to the list of known hosts.
    HostName ssh.github.com
    User git
    Port 443
   # 走 HTTP 代理
   # ProxyCommand socat - PROXY:127.0.0.1:%h:%p,proxyport=8080
   # 走 socks5 代理（如 Shadowsocks）
   # ProxyCommand nc -v -x 127.0.0.1:7890 %h %p
# 检测
ssh -T git@github.com
```


## vim使用
vim插件: easymotion[快速跳转]

### 用法1: 跳转到当前光标前后的位置(w/b)

快捷键`<leader><leader>w`(即`,,w`)和`<leader><leader>b`(即`,,b`)

助记: `word` and `back`

### 用法2: 搜索跳转(s)

快捷键`<leader><leader>s`(即`,,s`), 然后输入要搜索的字母, 这个跳转是双向的

助记: `search`


### 用法3: 行级跳转(jk)

配置

```
map <Leader><Leader>j <Plug>(easymotion-j)
map <Leader><Leader>k <Plug>(easymotion-k)
```

快捷键: `<leader><leader>j`和`<leader><leader>k`(即`,,j`和`,,k`)

助记: `hjkl`不解释

### 用法4: 行内跳转(hl)

配置

```
map <Leader><leader>h <Plug>(easymotion-linebackward)
map <Leader><leader>l <Plug>(easymotion-lineforward)
```

快捷键`<leader><leader>h`和`<leader><leader>l`(即`,,h`和`,,l`)

助记: `hjkl`不解释

### 用法5: 重复上一次动作(.)

配置

```
map <Leader><leader>. <Plug>(easymotion-repeat)
```

快捷键`<leader><leader>.`

助记: 同`repeat`插件….

### 最终配置

```
Bundle 'Lokaltog/vim-easymotion'
let g:EasyMotion_smartcase = 1
"let g:EasyMotion_startofline = 0 " keep cursor colum when JK motion
map <Leader><leader>h <Plug>(easymotion-linebackward)
map <Leader><Leader>j <Plug>(easymotion-j)
map <Leader><Leader>k <Plug>(easymotion-k)
map <Leader><leader>l <Plug>(easymotion-lineforward)
" 重复上一次操作, 类似repeat插件, 很强大
map <Leader><leader>. <Plug>(easymotion-repeat)
```

___

vim 插件vim-interestingwords

高亮显示当前单词<Leader>K


### 建议

1.  还可以`<Leader><leader>f`和`<Leader><leader>t`, 不过建议简单化, 一个`<Leader><leader>w/b`走天下.
    
2.  如果你不经常使用`s`, 可以将`s`改键, `nmap s <Plug>(easymotion-s)`, 这样你只需要输入`s`就可以进行搜索快速跳转(强迫症表示不能忍….) 具体做法见[官方文档](https://github.com/Lokaltog/vim-easymotion#bidirectional-motions)
    
3.  默认`<leader><leader>`作为这个插件的快捷键其实挺好的, 貌似没有其他插件会导致冲突, 还可以配置一整套, 强迫症很满意
    
4.  可以配置2/n个字符的搜索跳转, 更精准, 按需自取(个人觉得太复杂了没必要) [文档](https://github.com/Lokaltog/vim-easymotion#2-character-search-motion)和[文档](https://github.com/Lokaltog/vim-easymotion#n-character-search-motion)
    
5.  这个插件专心做好跳转就好, 没必要把搜索的活给做了


