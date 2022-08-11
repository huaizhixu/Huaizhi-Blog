# [记录cp命令的一次问题](https://github.com/huaizhixu/Huaizhi-Blog/issues/4)

### 问题描述
原因是这样的，在执行脚本的过程中，出现了
![Snipaste_2022-08-11_13-42-48](https://user-images.githubusercontent.com/108015790/184080966-55a8803f-3ee9-4d4f-a2da-1ba229705514.png)
所示的错误，定位到的错误是cp -rf  ******的原因，将-r参数去掉之后成功执行程序。
### 原因：
在cp的过程中，-r的参数是对目录进行的操作。查阅相关的资料解释如下所示：
![image](https://user-images.githubusercontent.com/108015790/184081545-d625a0fc-dd45-4f9c-a9d4-4833abf64b89.png)
也就是说在对目录操作的情况下才需要加上-r，单纯的文件要简单的进行复制。
