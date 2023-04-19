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

