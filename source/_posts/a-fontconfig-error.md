title: fontconfig error cannot load config file infinality/conf.d
date: 2016-01-30 20:32:14
tags:
---
今天莫名看见某人说道 [phantomjs](http://phantomjs.org/),
于是玩玩儿就想, `sudo pacman -S phantomjs`,
然后开始运行时弹出这么一句话:
fontconfig error cannot load config file infinality/conf.d,
于是Google之, 却看到 http://www.stata.com/support/faqs/unix/fontconfig-error/ ,
看起来似乎这并不是phantomjs的问题.似乎是fontconfig的问题(这玩意儿觉之前并从来没听说过).
archwiki上看见fontconfig有个fc-list命令.
于是`fc-list`发现也有"fontconfig error cannot load config file infinality/conf.d".
说明这不是phantomjs的问题. 只是phantomjs用到fontconfig了应该.
于是Google之fontconfig error, 但没找到有用的.
因为他只说infinality/conf.d,并不知道这路径指哪里,不明这infinality啥意思.
于是 `locate infinality`, 于是发现似乎是/etc/fonts/infinality .
`ls -l /etc/fonts/infinality`, 发现conf.d -> styles.conf.avail/infinality
`ls -l /etc/fonts/infinality/styles.conf.avail`
果然并没infinality.但看见有styles.conf.avail/linux.
不知道他配置如何. 但于是`sudo ln -sf styles.conf.avail/linux conf.d`
:) 于是Okay了. 再没出现这句error.

于是startx开启DE之后.简直了.字体都什么鬼.
后知后觉infinality是x11管的似乎.
(╯‵□′)╯︵┻━┻不应该改的.
改回来便是.
于是便不知道该怎么改了.
反正似乎并没影响.
