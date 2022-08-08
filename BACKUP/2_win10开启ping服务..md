# [win10开启ping服务 ](https://github.com/huaizhixu/Huaizhi-Blog/issues/2)

在ping服务时候，我ping别的ip可以通，但是别人ping我不同，在同一网段下，网上查了一下，说可能是我的某个服务没有开通，很有道理。现在把这个服务开通过程写出来，方便以后避免这样的低级错误。

控制面板-->Windows防火墙-->高级设置-->入站规则-->文件和打印机共享（回显请求ICMPv4-in），这个服务有两个，一个配置文件是“专用、公用”，一个是“域”，都启用就可以了。
![image](https://user-images.githubusercontent.com/108015790/183322355-9efdff37-67ff-436e-b3fa-057730224cda.png)
如果是别人ping我能通，我ping别人不通，应该是他的入站规则，或者我的出站规则这个服务未启用。
![image](https://user-images.githubusercontent.com/108015790/183324191-61bba81e-e475-4e8e-bda7-ef890be0da47.png)

