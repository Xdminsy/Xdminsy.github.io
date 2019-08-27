---
title: AHK 提升鼠标操作效率
date: 2019-08-26 14:31:49
tags:
---

突然想起来原来觉还有个 blog (笑。所以简单分享下觉习惯用的鼠标操作的 [AutoHotKey](https://www.autohotkey.com/) 代码。(不过觉用的是 AHK2 并不主流也不推荐)，建议还是用 AHK 1.1，不过觉下面这些代码应该还是兼容的~

其实觉本来是一个键盘党。但也是为了效率。鼠标功能丰富之后就可以完全靠鼠标并且有效率地代替一些本来需要键盘的快捷键。并且 chrome 有 cvim/vimium 等神器也可以基本完全脱离鼠标来操作。

觉现在用的鼠标是 Logitech G403， 就两个侧键。靠前的是 XButton2。靠后的是 XButton1。还有个中间的 DPI 键系统并检测不到。如果要用来搭配可以用鼠标驱动设置其成 WheelLeft 或者 WheelRight。如果没四向滚轮的话。不过其实不太好按所以觉驱动里置空了。默认功能 DPI Cycling 觉也用不到偶尔按到还得多按几次调回来。

双侧键默认功能前进后退有点鸡肋。而鼠标驱动能设置的功能一般有点受限，所以采用 AHK 来实现一些简单的功能。可以检测具体应用分别设置操作不过觉好像除了 Chrome 其他没很常用的。

侧键可以当成 Ctrl 之类的修饰键。配合滚轮使用比较合理。不过侧键少的话搭配也少常用操作也因人而异。觉的方案仅做参考。



# 功能和实现

用侧键来切换浏览器的 tab。位于前面的侧键 2 跳左 Tab。后面的侧键 1 跳右 Tab。

原本觉用来切换前后桌面(Win10 自带的多桌面)。但是觉发现觉着实用不上所以还是换了。

如果你有游戏需要用到侧键可以加上前置条件比如 `#If Not WinActive("ahk_exe dota2.exe")`

```
XButton2::Send "^+{Tab}"
XButton1::Send "^{Tab}"
```

并且觉还有其他方式来左右切换 tab (笑)，加上其实觉本来就很常用 ctrl-tab 和 ctrl-shift-tab 有点多。

觉按住右键加滚轮也可以用于切换 tab。单击侧键适合于比较近的 tab 切换。像觉这样即使有 onetab 也动不动几十个 tab 开着的远距离 tab 切换还是滚轮来的方便。不过觉右键是要用来鼠标手势的所以被 StrokesPlus.net 占用了。AHK 检测不方便所以在 SPN 里实现的。如果不用鼠标手势也可以直接 AHK 实现和侧键实现差不多。

```
RButton & WheelUp::Send "^+{Tab}"
RButton & WheelDown::Send "^{Tab}"
RButton::RButton
```

觉用按住侧键 1 并滚动滚轮来进行切换应用，和 alt-tab 是一样的。不过这样可以纯鼠标并且滚轮在很多应用中快速切换到想要的。而且 AHK 有专门的 `ShiftAltTab` 和 `AltTab` 函数实现起来很省心哦。

```
XButton1 & WheelUp::ShiftAltTab
XButton1 & WheelDown::AltTab
```

按住侧键 1 加鼠标左键就是相当于按一次 Alt-Tab 切换到最后的应用。觉这样的简单实现有个弊端是 Alt-Tab 的界面会闪现一下。不喜欢可以自行写具体一点获得上一个活动应用并激活。而且虽然有这个觉还是经常会按侧键并滚一下轮来操作。

```
XButton1 & LButton::!Tab
```

还有就是用侧键 2 加滚轮向下来关闭页面。关闭页面的确是一件很频繁的事情。然后侧键 2 加上滚就当恢复关闭的页面了咯 233。偶尔误操作了关闭之后就得重开嘛。初体验可能有点不习惯但其实习惯了不弱于 ctrl-w。特别是 ctrl-shift-t 按起来颇有点繁琐呢。

```
XButton2 & WheelDown::Send "^w"
XButton2 & WheelUp::Send "^+t"
```

那整个文件再一起贴一下吧，保存用 AutoHotkeyU64.exe 打开就行了(32 位机器用 AutoHotkeyU32.exe)

```
; #If WinActive("ahk_exe chrome.exe") ; 可取消注释改成自己需要的
XButton2::Send "^+{Tab}"
XButton1::Send "^{Tab}"
RButton & WheelUp::Send "^+{Tab}"
RButton & WheelDown::Send "^{Tab}"
RButton::RButton
XButton1 & WheelUp::ShiftAltTab
XButton1 & WheelDown::AltTab
XButton1 & LButton::!Tab
XButton2 & WheelDown::Send "^w"
XButton2 & WheelUp::Send "^+t"
```



# 总结

这些功能本质就是让侧键变得实用且频繁起来。而且不会影响现有任何功能。比如觉一般左手如果在键盘上还是会很常用本来的 ctrl-tab、ctrl-t、alt-tab 等快捷键。但是也会用侧键来操作或者交替操作。其实这都是下意识的了。觉的这些操作大部分为了避免大幅度移动鼠标。(可能是因为觉鼠标定位手感不准或者 DPI 低了)。BTW 其实鼠标手势也是觉很喜欢并且常用的功能。如果有机会下次再写咯。而且鼠标手势还有很大提升空间觉还需要一些想象力，比侧键能多很多可能性哦~

如果你有什么关于鼠标操作的想法也可以告诉觉~

