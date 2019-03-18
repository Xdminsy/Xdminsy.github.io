---
title: netkeeper 139 error
date: 2018-12-09 20:44:17
tags:
---

大学办的电信的宽带、于是得用所谓的闪讯 Netkeeper、说实话很不好用、每天要给一个短信发么么(mm)、不然人家生气就不让你上网。

本来 Netkeeper 好好的、安装完 Visual Studio 2017 Community 结果 Netkeeper 一直 139 error。当时明白了应该是 VS 的问题不过卸载了也没恢复、甚至为此重装过一次(很愚蠢)、然后依然是安装完 VS 立刻 Netkeeper 就炸了。

苦恼了很久、VS 和 Netkeeper 都是不可或缺的、但网上能搜到的 Netkeeper 出问题解决方案都试了遍一点用都没用、也没看到哪里有 VS 和 Netkeeper 会冲突、略微了解一下 Netkeeper 的原理和功能、Netkeeper 是自行模拟拨号以此来防止账号多处登陆、然后发现果然这就有线索了、一直是用 L2TP 连接的、于是能搜到 VS 会导致 L2TP 必须 over IPSec、[安装 VS 后电脑无法连接 L2TP VPN->Computers are unable to connect after you install VS L2TP VPN](https://developercommunity.visualstudio.com/content/problem/50402/%E5%AE%89%E8%A3%85vs%E5%90%8E%E7%94%B5%E8%84%91%E6%97%A0%E6%B3%95%E8%BF%9E%E6%8E%A5l2tp-vpn.html)、、所以解决方案有了、就是注册表加 prohibitIPSec=1、

以下代码保存为 .reg 文件右键合并即可、或者自行开注册表修改、win10 regedit 支持直接输路径定位比较方便。

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Rasman\Parameters]
"ProhibitIpSec"=dword:1
```



至此问题解决了、VS 和 Netkeeper 并非鱼和熊掌、虽然还是不理解为什么 VS2015 以后安装完会不让用 L2TP 只能 L2TP over IPSec、但是能上网了能用 VS 了、希望对各位在校用 Netkeeper 的用得到 VS 的学员有些帮助~