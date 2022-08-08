# [ubuntu环境下的代理工具](https://github.com/huaizhixu/Huaizhi-Blog/issues/1)

## 1、安装
安装命令：
Debian / Ubuntu:
```
apt-get install python-pip
pip install git+https://github.com/shadowsocks/shadowsocks.git@master
```
## 2、配置
首先对配置文件进行配置：
```
vim /etc/shadowsocks/shadowsocks.json
```
配置文件：
```
{ 
    "server":"xxx.xxx.xxx.xxx",
    "server_port":xxx,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"xxx",
    "timeout":600,
    "method":"chacha20-ietf-poly1305",
    "fast_open": false,
    "workers": 1
}

```
启动：
```
sslocal -c /etc/shadowsocks/shadowsocks.json
```
## 3、检查shadowsock客户端是否安装正常：
```
curl --socks5 127.0.0.1:1080 http://httpbin.org/ip

```
## proxychains4配置使用
```
sudo apt-get install proxychains4
```
修改配置文件：
```
sudo vim /etc/proxychains.conf
```
在文本最后加上你的代理服务器地址:
```
#[proxylist]
socks5 127.0.0.1 1080
```
```
#各配置项用法如下：
#dynamic_chain：
#每个连接都将通过链接代理完成
＃所有代理按列表中显示的顺序链接
＃至少有一个代理必须在线才能使用
＃（跳过死的代理）
#strict_chain：该配置为ProxyChains的默认配置，同dynamic_chain一样，但所有代理必须正常，否则不能正常使用
#random_chain：该配置项会从ProxyList中随机选择代理IP来运行流量，如果ProxyList中有多个代理IP，在使用proxychains的时候会使用不同的代理访问目标主机，从而使主机端探测流量更加困难。
 ```
## ERROR method chacha20-ietf-poly1305 not supported 解决
```
install libsodium -y
pip install https://github.com/shadowsocks/shadowsocks/archive/master.zip -U
```