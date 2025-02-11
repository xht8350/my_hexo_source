---
title: linux打印工具开发
date: 2025-02-11 10:45:10
tags: 技术
---

项目地址：`https://github.com/LittleWalnutX/Multiple_PDF_Printer`

为了补足linux个人桌面在多样化的打印功能上的不足，写了这个项目，例如Windows可以使用Adobe Acrobat DC来打印小册子，而linux没有这样的软件；甚至大多数软件不能双面打印，需要手动选择先逆页序打印偶数页，再打印奇数页。

项目生成PDF文件然后再手动打印。以后可能加入直接打印的方式。

目前已经开发完成的功能有：

    双面打印
    小册子打印


下面介绍一下思路: 双面打印的思路比较简单，只需要先把偶数页逆序提取出来，然后再提取奇数页，最后手动进行打印就可以了

小册子打印的思路比较复杂，其中的难点主要在于拼合PDF。几乎是直接引用了一个日本网站上的代码，然后修改了一下。

小册子打印需要解决另外一个问题就是页码的排布问题。观察一本钉好的小册子，可以发现，以16页的小册子为例，它的页码排布分别是，16，1，2，15, 14, 3, 4, 13 .....。这也就是说，第一页是最后一页，然后从头取两页，从后面取两页。

然后我们把它分成奇数页面和偶数页面，可以得到它的规律。详细的规律见代码。

然后写一下图形界面工具。这是用AI写的，把代码搬过来，然后改一下bug，再把自己的功能填上去就可以了。

这个地方还有一个问题，就是用tkinter写的代码，在linux的X11上，存在一个极大概率触发的问题，就是文件拖拽上去之后会直接闪退，并且报如下的错误：

```
X Error of failed request:  BadWindow (invalid Window parameter)
  Major opcode of failed request:  20 (X_GetProperty)
  Resource id in failed request:  0x1417efd
  Serial number of failed request:  1225
  Current serial number in output stream:  1225
```

排查了很长时间，我觉得这个问题不是我的问题，可能是因为AI写的代码里面用了tkinterdnd2库的问题。

这个问题在wayland上不会出现。尽管如此，这个问题仍然难以接受，所以使用AI工具，把这个界面用pyside重写，然后就得到了pyside版的gui。也在项目里面。

希望这么个项目可以对linux的桌面应用有一点微薄的帮助。以后如果有时间的话，可能再考虑尝试一下开发预览功能，以及直接打印而不是生成PDF的功能。
