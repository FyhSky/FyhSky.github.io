---
layout: post
title: "The new features of OSX 10.11 and Xcode 7"
date: 2015-11-11 21:00:00
comments: true
--- 
The new features of OSX 10.11 and Xcode 7
============
**New features**
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;•	Split View
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;用户只要按下F3就会看到全新的任务管理界面，用户只需要将两个应用拖进同一个桌面即可以实现Split View功能。Split View功能的意义并不是同时查看两个应用，而是在于将两个应用摆在一起去提高工作效率，理想使用场景是一边通过网页查资料，一边写文档。同时，用户可以自行调整两个应用分屏的比例，系统会自动记忆下来。同时，用户只需轻扫一下，就能回到桌面，轻松切换到之前进行的其它事情上，大大提高了使用效率。
<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/The%20new%20features%20of%20OSX%2010.11%20and%20Xcode%207/Resources/image001.png"/>
</div>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;•	Mission Control&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Mission Control功能变得更加简洁，它让用户能够更加轻松地查看和整理Mac上已打开的所有应用，只需轻扫一下，你桌面上的所有窗口便会在同一层展开。Mission Control还会将窗口按照它们在桌面上的相应位置进行排布，你可以更快找到想要的那个窗口，非常方便。而当有很多窗口相互挤占桌面时，现在也有了更简单的方式来给它们腾出更多空间，只需将任何一个窗口拖至屏幕顶部，就能把它放入全新的桌面空间中。实际上，多桌面的概念在OS X上已经诞生很久了，这一次带来的体验要更佳。此外，当用户将某个应用窗口拖动到边框时，将能够自动调整该窗口的大小。可以说，OSX El Capitan在窗口管理方面的优化非常到位。<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/The%20new%20features%20of%20OSX%2010.11%20and%20Xcode%207/Resources/image002.png"/>
</div>
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;•	Spotlight&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Spotlight搜索更加智能它能够搜索更多的话题，包括天气、股票、体育、网络视频和交通信息等。用户也可以通过语音去执行Spotlight搜索
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;•	Call out your cursor&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;通过快速滑动鼠标，可以快速找到光标位置。<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/The%20new%20features%20of%20OSX%2010.11%20and%20Xcode%207/Resources/image003.png"/>
</div>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;•	Mail&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;邮件应用新增了全屏显示功能和轻扫手势功能，其中轻扫手势功能类似于iOS中的邮件应用，只需向右轻扫就可以将邮件标记为已读或未读，或向左轻扫就可删除邮件，便于归类，查看邮件更加方便。
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;•	Notes&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;备忘录功能得到了升级，除了文字之外，用户还可以在其中加入图片、视频和链接等。
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;•	Photos&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;•	Fonts&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;备忘录功能得到了升级，除了文字之外，用户还可以在其中加入图片、视频和链接等。
<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/The%20new%20features%20of%20OSX%2010.11%20and%20Xcode%207/Resources/image004.png"/>
</div>


&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;•	Metal&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Apple为游戏开发者推出了新的平台技术 Metal，该技术能够为 3D 图像提高 10 倍的渲染性能。**Frameworks and Framework Technologies**&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;•	New Frameworks&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Contacts (Contacts.framework) 访问通信录
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;GameplayKit (GameplayKit.framework) 游戏开发工具库
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Metal (Metal.framework).提供基于GPU加速的3D图形渲染以及数据并行计算的功能
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;MetalKit (MetalKit.framework)Metal功能的工具库
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Model I/O (ModelIO.framework)提供系统级别的3D资源模型访问
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Network Extension (NetworkExtension.framework).支持VPN技术&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;•	AppKit Framework Changes&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Detial reference by [AppKit Release Notes for OS X v10.11](https://developer.apple.com/library/mac/releasenotes/AppKit/RN-AppKit/index.html#//apple_ref/doc/uid/TP30000741)Appkit framework changes are as follows:<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/The%20new%20features%20of%20OSX%2010.11%20and%20Xcode%207/Resources/image005.png"/>
</div>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;•	Security Enhancements&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;	App Transport Security (ATS)
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;苹果加强APP内部网络访问的安全性，建议所有网络请求都使用HTTPS协议。Xcode 7 默认开启这个功能，可以在APP的Info.plist文件中配置不使用ATS.
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;System Integrity Protection&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;•	UI testing 
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;	Xcode 7 + OSX 10.11 下可以编写UI测试代码&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;•	Deprecations
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;		OSX 10.11 不再支持运行时的垃圾回收 
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;	OpenSSL headers 从OS X v10.11 SDK中彻底移除
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;		Apple stopped shipping OpenSSL with OS X some time ago, citing lack of a stable API from version to version.&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;It's a bit more subtle than that:&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; Apple deprecated its OpenSSL shared libraries a while back (with OS X 10.7).  That's because OpenSSL doesn't offer release-to-release binary compatibility, so we can't update the shared libraries to the latest OpenSSL without breaking all the existing clients.&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; At the same time we marked the OpenSSL headers in the OS X SDK as deprecated so you'd get deprecation warnings if you build with a deployment target of 10.7 or later.&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; With the latest OS X SDK we've removed the headers entirely, making it much harder to use the long-since-deprecated shared libraries.&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; We recommend that developers who need OpenSSL build their own copy of it and include that copy in their app.  Alternatively you can use native OS X APIs, like Secure Transport.&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;苹果给的建议：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;1.开发者编译OpenSSL库并添加到自己的工程中
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;2.使用Secure Transport库。
**To learn more, visit**[ http://www.apple.com/osx/whats-new/ - international](http://www.apple.com/osx/whats-new/#international). 
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;[https://developer.apple.com/library/mac/releasenotes/MacOSX/WhatsNewInOSX/Articles/MacOSX10_11.html - //apple_ref/doc/uid/TP40016227-SW1.](https://developer.apple.com/library/mac/releasenotes/MacOSX/WhatsNewInOSX/Articles/MacOSX10_11.html#//apple_ref/doc/uid/TP40016227-SW1)
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;[https://developer.apple.com/library/mac/releasenotes/DeveloperTools/RN-Xcode/Chapters/xc7_release_notes.html - //apple_ref/doc/uid/TP40001051-CH5-SW1](https://developer.apple.com/library/mac/releasenotes/DeveloperTools/RN-Xcode/Chapters/xc7_release_notes.html#//apple_ref/doc/uid/TP40001051-CH5-SW1)