---
title: 演示模式暂停屏保小记
date: 2019-10-03 23:39:45
tags:
---

经常需要避免屏保的时候、有第三方工具可以解决。但还有一个 Windows 自带的屏幕演示工具可以关闭屏保。

一般操作为 Win-X Mobility Center。然后把里面的 Presenting 给 Turn On 即可。不过 Mobility Center 可以直接 Win-R mblctr 就可以打开。又不过 Presenting 的话有个 PresentationSettings.exe。支持 /start 或者 /stop 参数。所以也可以直接 Win-R `PresentationSettings /start` 来操作。不过呢这个重启之后就会自动关闭。

开了的话托盘会有个 Presentation Settings 的图标。可以点开设置。默认应该是勾选了 Turn off the screen saver 的。所以开着演示模式就不会进屏保。

<!--more-->

然后后来觉经常不喜欢离开一会儿或者看会儿手机就自动屏保了。(虽然指纹解锁但还是感觉好麻烦如果有觉的机子支持 Windows Hello Face 那多好)(虽然特意选了些 Eki 的横向照片当屏保真的狠好看 prpr！！但觉经常是 Win-D 桌面 8 个 Eki 相册 prpr 不用屏保啦！)、真离开的时候会手动 Win-L 的。所以日常习惯开着演示禁屏保。然后就直接 shell:startup (Win 开机启动目录) 里加了 `PresentationSettings /start`、可是经常会失效。开机还是没有在 Presenting。其实觉也没有意识到为什么。当时想以为是 shell:startup 的问题。反正开机启动的方式不少寻思着用 Task Scheduler 试试。

Task Scheduler 其实很好用的。打开方式也是习惯性 win-r taskschd.msc 或者 win-r control schedtasks。(其实直接 win-s 直接搜 task scheduler 就行的 hhh)。虽然觉也用 Wox 但总感觉纯净的原版 Win-R 更快更帅 hh? 又其实还可以直接通过 schtasks 来操作 tasks。不过既然自己改的话还是 GUI 操作方便。就还是很简单的建一个 task 设置开机启动。当时想的是 shell:startup 里可能因为还没登陆或者什么原因所以 `PresentationSettings /start` 失败了。所以 Task 给加了 5 分钟延迟。觉屏保是 15 分钟的足够了。

觉创建的 Task 名字叫 PrensentationStart、创建完在一列 Tasks 中想找一找、然后很喜感的、发现。怎么有个 PrensentationSettingsTurnOff 的 Task 开机启动啊！！！惊了！！怪不得觉之前自启的 Prensenting 失效。原来他有这么个开机自动关了的 Task。所以偶尔失效就是因为觉开机开了然后被他这个 Task 给关了 23333。那么觉新建的 Task 就没用了。。顺便把他自带的这个 TurnOff Task 也 Disabled。之后 Prensenting 就 Persist 了 hhh。就不会进屏保啦。

However 后知后觉考虑到。为什么。不。直接。把屏幕保护给关了呢！！Timeout 可以设置 Never 的啊！！！被自己蠢哭了。。用 Presenting Mode 的方法是为了暂时关闭屏保的。要永久关了设置里关啊！不过现在还是一直开着 Presenting。可能因为习惯了？

哼。