# [Linux使用](https://github.com/huaizhixu/Huaizhi-Blog/issues/9)

查看系统信息
```
cat /etc/issue

Ubuntu 20.04.2 LTS \n \l

```

Ubuntu的apt-get代理设置
在命令行临时带入
在命令行后面增加-o选项

```
sudo apt-get -o Acquire::http::proxy="http://127.0.0.1:8000/" update
```
制作Gif动图
在视频保存路径下，运行 <kbd>ffmpeg -i 视频.mp4 out.gif</kbd> 即可输出Gif动图。