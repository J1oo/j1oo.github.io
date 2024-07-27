# Kerberos


# kerberos 分析

kerberos 的主要步骤如下，重点分析前四步

1. AS-REQ
2. AS-REP
3. TGS-REQ
4. TGS-REP
5. AP-REQ
6. AP-REP

## AS-REQ

在域控上抓包，查看机器登陆域用户时产生的流量

<img src="../../../img/image-20240728012905687.png" alt="image-20240728012905687" style="zoom: 200%;" />

先看这一部分

<img src="../../../img/image-20240728013101500.png" alt="image-20240728013101500" style="zoom:200%;" />

pvno：5 代表 kerberos 协议的版本号

msg-type 是消息类型

padata：1 item 代表有一个数据项

padata-type: pA-PAC-REQUEST (128)，**这是一个 PAC 的请求**，PAC 用于携带用户的特权信息比如 **用户组、特权**

padata-value: 3005a0030101ff，




