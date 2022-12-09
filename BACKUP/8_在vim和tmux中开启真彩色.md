# [在vim和tmux中开启真彩色](https://github.com/huaizhixu/Huaizhi-Blog/issues/8)

在 vim 和 tmux 中开启真彩色，可以获得更好的视觉体验。

在 vimrc 中加入下面的设置：

```
if exists('+termguicolors')
  let &t_8f = "\<Esc>[38;2;%lu;%lu;%lum"
  let &t_8b = "\<Esc>[48;2;%lu;%lu;%lum"
  set termguicolors
endif
```

Tmux 需要在 `.tmux.conf` 配置文件里添加下面的内容：

```
set -g default-terminal tmux-256color  # 这里也可设置成 screen-256color
set-option -ga terminal-overrides ",*256col*:Tc"
```

退出所有的 tmux，再重新打开，就可以了。

如何验证 true color 是否开启成功？验证 vim 的话，在 vim 里用 `:terminal` 命令打开自带的终端，执行下面的命令<sup id="fnref:1"><a href="https://www.littlezhang.com/2020/11/vim-tips%E5%9C%A8vim%E5%92%8Ctmux%E4%B8%AD%E5%BC%80%E5%90%AF%E7%9C%9F%E5%BD%A9%E8%89%B2/#fn:1" role="doc-noteref">1</a></sup>：

```
awk 'BEGIN{
    s="/\\/\\/\\/\\/\\"; s=s s s s s s s s;
    for (colnum = 0; colnum<77; colnum++) {
        r = 255-(colnum*255/76);
        g = (colnum*510/76);
        b = (colnum*255/76);
        if (g>255) g = 510-g;
        printf "\033[48;2;%d;%d;%dm", r,g,b;
        printf "\033[38;2;%d;%d;%dm", 255-r,255-g,255-b;
        printf "%s\033[0m", substr(s,colnum+1,1);
    }
    printf "\n";
}'
```

验证 tmux，则打开 tmux 后直接在命令行执行上面的命令。

如果显示的是连续的颜色，则已经开启成功；

[![](https://res.cloudinary.com/dny1wymwm/image/upload/v1604978492/true_color_wsl_fyxv15.png)](https://res.cloudinary.com/dny1wymwm/image/upload/v1604978492/true_color_wsl_fyxv15.png)

如果是间断的颜色，则设置失败。

[![](https://res.cloudinary.com/dny1wymwm/image/upload/v1604978492/no_true_color_qcgnc1.png)](https://res.cloudinary.com/dny1wymwm/image/upload/v1604978492/no_true_color_qcgnc1.png)

**参考链接**

-   [https://lotabout.me/2018/true-color-for-tmux-and-vim/](https://lotabout.me/2018/true-color-for-tmux-and-vim/)
    
-   [https://jdhao.github.io/2018/10/19/tmux\_nvim\_true\_color/](https://jdhao.github.io/2018/10/19/tmux_nvim_true_color/)
    __

1.  [https://gist.github.com/XVilka/8346728](https://gist.github.com/XVilka/8346728) [↩︎](https://www.littlezhang.com/2020/11/vim-tips%E5%9C%A8vim%E5%92%8Ctmux%E4%B8%AD%E5%BC%80%E5%90%AF%E7%9C%9F%E5%BD%A9%E8%89%B2/#fnref:1)