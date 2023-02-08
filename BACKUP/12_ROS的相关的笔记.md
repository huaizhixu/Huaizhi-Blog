# [ROS的相关的笔记](https://github.com/huaizhixu/Huaizhi-Blog/issues/12)

1、相关的<kbd>rostopic </kbd>的操作
输出所有发布的话题：
<kbd>rostopic list</kbd>

输出话题的类型：
<kbd>rostopic type /joy | rosmsg show</kbd>

命令行发布话题的类型：
<kbd>rostopic pub -1 /myrobot/leg1423_Effort_controller/command std_msgs/Float64MultiArray "data: [1.23,-1.23,-1.23,1.23]"</kbd>

2、有用的网站参考链接
[PlotJuggler绘图](https://github.com/facontidavide/PlotJuggler)