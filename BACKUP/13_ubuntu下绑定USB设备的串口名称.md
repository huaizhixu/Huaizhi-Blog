# [ubuntu下绑定USB设备的串口名称](https://github.com/huaizhixu/Huaizhi-Blog/issues/13)

在嵌入式开发和其它过程中，往往会出现USB设备的接入。但是对于多个USB设备接入时，由于操作系统的ttyUSB*的动态分配原则，不同设备之间可能存在USB设备文件更新不及时的冲突。而且设备驱动和ROS的launch文件也经常需要更换ttyUSB*的设备编号配置。并且每一次需要更新设备读写权限，较为麻烦。
在Linux中通过设置USB rules配置文件的方式来进行配置，通过识别设备的芯片编号绑定将设备绑定到固定的设备文件符中。
主要流程如下：
1.查询设备的硬件编号。
2.根据硬件编号设置rules文件。
3.重新启动udev serveice 更新配置文件。
4.重新插拔设备，查看设备文件符。
## 查询设备硬件编号
<kbd>udevadm info --attribute-walk --name=/dev/ttyUSB0</kbd>

![image](https://user-images.githubusercontent.com/108015790/224951536-5c4f7ae8-cb89-4957-b9d3-cfdd0f574ea2.png)


其中`ATTRS{idProduct}`和`ATTRS{idVendor}`代表设备的硬件芯片信息。是操作系统内核识别设备的关键。
使用`lsusb`命令直接查看所有设备的关键信息如下：
![image](https://user-images.githubusercontent.com/108015790/224951982-056a134d-4cd4-4ee4-933c-db756723d2a0.png)

## 添加`udev rules`规则文件[](https://wangpengcheng.github.io/2019/09/18/change_usb_rules_ubuntu/#%E6%B7%BB%E5%8A%A0udev-rules%E8%A7%84%E5%88%99%E6%96%87%E4%BB%B6)

_参考链接：_ [如何在 Linux 中永久修改 USB 设备权限](https://linux.cn/article-6449-1.html?utm_source=weixin);[ubuntu 16.04 中永久修改 USB 设备权限](https://blog.csdn.net/jiangchao3392/article/details/76227180)

设备规则文件在Ubuntu中存放在`/etc/udev/rules.d/`文件夹下。可以在此文件夹中添加自定义的以`.rules`的文件。

udev的规则的匹配关键键内容如下：

| 关键键 | 含义 |
| --- | --- |
| ACTION | 事件 (uevent)的行为，例如：add( 添加设备 )、remove(删除设备 )。 |
| KERNEL | 在内核里看到的设备名字，比如sd\*表示任意SCSI磁盘设备 |
| DEVPATH | 内核设备录进，比如/devices/\* |
| SUBSYSTEM | 子系统名字，例如：sda的子系统为 block。 |
| BUS | 总线的名字，比如IDE,USB |
| DRIVER | 设备驱动的名字，比如ide-cdrom |
| ID | 独立于内核名字的设备名字 |
| SYSFS{value} | sysfs属性值，他可以表示任意 |
| ENV{ key} | 环境变量，可以表示任意 |
| PROGRAM | 可执行的外部程序，如果程序返回0值，该键则认为为真(true) |
| RESULT | 上一个PROGRAM调用返回的标准输出。 |
| NAME | 根据这个规则创建的设备文件的文件名。**注意：仅仅第一行的NAME描述是有效的，后面的均忽略。如果你想使用使用两个以上的名字来访问一个设备的话，可以考虑SYMLINK键。** |
| SYMLINK | 为 /dev/下的设备文件产生符号链接。由于 udev只能为某个设备产生一个设备文件，**所以为了不覆盖系统默认的 udev规则所产生的文件，推荐使用符号链接。** |
| OWNER | 设备文件的属组 |
| GROUP | 设备文件所在的组。 |
| MODE | 设备文件的权限，采用8进制 |
| RUN  | 为设备而执行的程序列表 |
| LABEL | 在配置文件里为内部控制而采用的名字标签(下下面的GOTO服务) |
| GOTO | 跳到匹配的规则（通过LABEL来标识），有点类似程序语言中的GOTO |
| IMPORT{type} | 导入一个文件或者一个程序执行后而生成的规则集到当前文件 |
| WAIT\_FOR\_SYSFS | 等待一个特定的设备文件的创建。主要是用作时序和依赖问题。 |
| PTIONS | 特定的选项： |
| last\_rule | 对这类设备终端规则执行； |
| ignore\_device | 忽略当前规则； |
| ignore\_remove | 忽略接下来的并移走请求。 |
| all\_partitions | 为所有的磁盘分区创建设备文件。 |

在`/etc/udev/rules.d`文件夹下创建自定义`my_usb_rules.rules`文件内容如下

```
# ultrasonic_radar usb rules
KERNEL=="ttyUSB*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="10c4", ATTRS{idProduct}=="ea60", GROUP="users", MODE="0666", ENV{ID_MM_DEVICE_IGNORE}="1", SYMLINK+="ultrasonic_radar"
# imu usb rules
KERNEL=="ttyUSB*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", GROUP="users", MODE="0666", ENV{ID_MM_DEVICE_IGNORE}="1", SYMLINK+="imu"
```

注意： 这里的`ATTRS{idVendor}`和`ATTRS{idProduct}`是查询到的对应的设备地芯片的硬件值。`SYMLINK+=`对应的是对设备`ttyUSB*`生成的软连接名称。`MODE`是对设备权限的更改。**一定要添加`KERNEL=="ttyUSB*"`**生成软连接。否则直接生成对名称的设备号。一般的linux驱动无法识别。

### 重启服务查看 对应设备[]

```
ls -l /dev |grep ttyUSB

```
![image](https://user-images.githubusercontent.com/108015790/224952956-2d6d7ef5-7130-4f97-82ba-953cfefb113f.png)


当添加或者删除udev的rules文件后，都需要使用如下命令，进行设备读取rules的更新

```
sudo service udev reload
sudo service udev restart
```

**然后重新插拔USB设备，就可以按照新的规则执行了**。


使用`cutecom`查看串口通信结果


**注意：这里是根据设备芯片类进行的配置具有唯一性，一个规则只能配置一种设备，两个设备是同种设备时不能由设备芯片进行识别区分**

## KERNELS硬件端口号绑定USB串口名称(推荐使用)
通过以下命令查看ttyUSB0的KERNELS硬件端口号：
<kbd>udevadm info --attribute-walk --name=/dev/ttyUSB0</kbd>


```
udevadm info --attribute-walk --name=/dev/ttyUSB0
```

![image](https://user-images.githubusercontent.com/108015790/224954392-813a4037-b194-4104-9ea6-0b3dbd581fd9.png)

在第三个looking at...的下方，就是这个USB 设备的KERNELS硬件端口号：KERNELS == "3-1:1.0"。

在/etc/udev/rule.d 下产生相应的规则文件，将ttyUSB0命名为你喜欢的名字。

        首先，通过以下命令创建规则文件：

```
sudo vim /etc/udev/rules.d/usb.rules
```

        在打开的文本框里输入以下代码，保存退出：

```
KERNELS=="3-1:1.0", MODE:="0777", GROUP:="dialout", SYMLINK+="usb_rplidar"
```

通过以上两步，就把ttyUSB0取别名为usb\_rplidar，以后在程序里直接访问usb\_rplidar，就可以与这个设备通信了。

运行以下命令使修改立即生效：

```
sudo udevadm trigger
```

重复步骤，用同样的办法把剩下的USB设备重命名。


把所有USB设备重命名后，运行以下命令查看USB设备名更改情况：

```
ls -l /dev |grep ttyUSB
```


至此，所有的USB设备都被唯一的绑定到自定义的名字上，再也不用担心设备号窜动了。

