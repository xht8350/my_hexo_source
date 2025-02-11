---
title: KDEplasma面板崩溃
date: 2025-02-01 18:36:20
tags: 技术
---


KDE Plasma面板经常崩溃，然而killall plasmashell不管用。网上没有找到解决办法。

经实测，发现`killall -9 plasmashell`就行了。

这就类似windows explorer重启。

还有其他意想不到的效果：

本来KDE wayland和x11的鼠标指针大小不是同一个标准，如果电脑屏幕有150%缩放，则wayland的24号鼠标指针等于x11的36号。在x11里面修改鼠标指针大小只会对新打开的应用生效，然而桌面不会，很难受。现在我们知道了，包括桌面和panel全部都是plasmashell这个进程，我们把他杀掉他就会自动重启，鼠标指针大小正常了。

