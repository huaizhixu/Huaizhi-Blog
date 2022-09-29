# [ubuntu20.04设置固定ip](https://github.com/huaizhixu/Huaizhi-Blog/issues/7)

ubuntu 从 17.10 开始，已放弃在 /etc/network/interfaces 里固定 IP 的配置，interfaces 文件不复存在，即使配置也不会生效，而是改成 netplan 方式 ，配置写在 /etc/netplan/01-netcfg.yaml 或者类似名称的 yaml 文件里。
```
sudo vim /etc/netplan/00-installer-config.yaml

```
```
network:
  ethernets:
    ens160:     #配置的网卡的名称
      addresses: [192.168.0.105/24]    #配置的静态ip地址和掩码
      dhcp4: no    #关闭DHCP，如果需要打开DHCP则写yes
      optional: true
      gateway4: 192.168.0.1    #网关地址
      nameservers:
         addresses: [114.114.114.114,180.76.76.76]    #DNS服务器地址，多个DNS服务器地址需要用英文逗号分隔开
  version: 2
  renderer: networkd    #指定后端采用systemd-networkd或者Network Manager，可不填写则默认使用systemd-workd
```
## 生效配置&查看状态
```
sudo netplan apply
networkctl status 
```
## 测试
先 ping 内网的网关，确认内网是否通
```
ping 192.168.1.1
```
再 ping 一下外网的 IP ，确认是否可以访问外网。
```
ping 114.114.114.114
```