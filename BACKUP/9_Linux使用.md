# [Linux使用](https://github.com/huaizhixu/Huaizhi-Blog/issues/9)

## Linux使用

查看系统信息
```
cat /etc/issue

Ubuntu 20.04.2 LTS \n \l

```

Ubuntu的apt-get代理设置
在命令行临时带入
在命令行后面增加-o选项

```
sudo apt-get -o Acquire::http::proxy="http://127.0.0.1:8889/" update
```

### 查看Processes sorted by RAM or CPU Usage
```
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head
```


## 好用的命令
<kbd>z</kbd> 命令 ( z - jump around ) 是一个开源的快速路径切换工具（类似工具还有 z.lua、autojump、fasd）。通过 Frecency 机制对日常访问的路径进行 Frecent 权重计算，z 命令会帮你切换到所有匹配正则关键字的路径中权重值最高的那条路径。
```
手动安装：
 
# /usr/local 安装
$ cd /usr/local
$ sudo git clone https://github.com/rupa/z.git
$ sudo chmod +x z.sh
 
# zsh 配置变量
$ echo '. /usr/local/z/z.sh' >> ~/.zshrc
$ source ~/.zshrc
 
# bash 配置变量
$ echo '. /usr/local/z/z.sh' >> ~/.bash_profile
$ source ~/.bash_profile
 
# 安装 manpage
$ cp z.1 /usr/local/share/man/man1
 
# 验证安装
$ z -h
$ man z
```
### [终端的好用命令网站](https://icyleaf.github.io/better-cli-solution)


### 制作Gif动图
在视频保存路径下，运行 <kbd>ffmpeg -i 视频.mp4 out.gif</kbd> 即可输出Gif动图。

## tmux使用
___

保存Tmux的屏幕输出分为两步： 首先用`capture-pane`将屏幕输出保存在buffer里， 然后用`save-buffer`将buffer内容保存到文件里。

在`capture-pane`中可以用`-S`和`-E`指定要保存的屏幕输出的范围， 当前屏幕的最上一行为坐标原点，标记为0，下面一行坐标是1,依次类推； 原点的上一行坐标是-1，再上一行坐标是-2，依次类推。

用`Alt-c`进入copy-mode后，屏幕右上角显示当前屏幕在整个pane中的坐标\[X/Y\]， 其中X代表当前屏幕最高行的坐标，Y代表最早一行屏幕输出的坐标， 根据坐标确定要保存文本的起止坐标就可以保存了。

例如要保存第3个pane中的一段近5000行的输出， 进入copy-mode后按`g`键，到最早的屏幕输出，右上角显示`[5676/5676]`, 用`Ctrl-f`或者`J`键向下滚动屏幕， 当想要保存的第一行处于屏幕最上一行时，坐标显示为`[5557/5676]`， 将想要保存的最后一行滚动到屏幕最上一行，坐标显示为`[642/5676]`， 切换到另一个pane里执行：

```
tmux capture-pane -S -5557 -E -642 -t 3
tmux save-buffer output.log

```

这样这段输出就保存到文件output.log里了，其中`-t 3`指定了要保存的pane的序号。

如果要保存所有历史输出，可以简写为`tmux capture-pane -S -`.

除了新开一个pane执行tmux命令，也可以在当前pane用快捷键`Alt-a`进入tmux命令行状态 即command-prompt，然后执行`capture-pane -S -5557 -E -642`.

___

___
