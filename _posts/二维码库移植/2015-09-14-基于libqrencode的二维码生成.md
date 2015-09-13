---
layout: post
title: "基于libqrencode的二维码生成"
date: 2015-09-14 00:10:00
comments: true
--- 
基于libqrencode的二维码生成
============
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;libqrencode是一个C语言编写的用来生成二维条形码的库，生成的二维条形码可以通过手机的CCD摄像机轻易的扫描出来。此库生成的二维码的容量多达7000个数字或4000个字符，并且具有很强的鲁棒性。
<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/%E4%BA%8C%E7%BB%B4%E7%A0%81%E5%BA%93%E7%A7%BB%E6%A4%8D/resources/image001.png"/>
</div><div align="center">QR Code example</div>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;目前，该库的稳定版本是3.4.4， 具有以下特点：
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;
 * 运行时不需要其他额外的文件&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; 
* 快速的编码&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; 
* 输入数据的自动优化&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;该库只支持日本工业标准X0510:2004 或 ISO/IEC 18004所规定的QR Code model 2模式，不支持如下功能：ECI and FNC1 modeQR Code model 1具体介绍详见：[http://fukuchi.org/works/qrencode/](http://fukuchi.org/works/qrencode/)&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;言归正传，本文就讲述如何使用该库一步步的生成osx或ios下的二维码 。步骤如下：
1.从[http://fukuchi.org/works/qrencode/](http://fukuchi.org/works/qrencode/)处下载稳定的版本。
2.解压下载的源代码包，将里面所有的.h和.c文件拷贝出来放在一个文件夹中，例如文件夹命名为libqrencode。
3.新建 工程，选择OSX的Application - > Cocoa Application –>Next.
<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/%E4%BA%8C%E7%BB%B4%E7%A0%81%E5%BA%93%E7%A7%BB%E6%A4%8D/resources/image002.png"/>
</div>填写好Produce Name , identifer随便填（反正不提交App store）,然后Next，选择好存放工程目录，点解create创建工程成功.<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/%E4%BA%8C%E7%BB%B4%E7%A0%81%E5%BA%93%E7%A7%BB%E6%A4%8D/resources/image004.png"/>
</div>4.将之前准备好的libqrencode文件夹下文件添加到工程中。添加方法有多种，可以直接拖拽文件夹到工程，会弹出如下提示框。点击Finish完成添加。
<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/%E4%BA%8C%E7%BB%B4%E7%A0%81%E5%BA%93%E7%A7%BB%E6%A4%8D/resources/image006.png"/>
</div>5.必要的修改处理。
点击编译，会发现多处错误。
<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/%E4%BA%8C%E7%BB%B4%E7%A0%81%E5%BA%93%E7%A7%BB%E6%A4%8D/resources/image008.png"/>
</div>只看结果的可以直接删除qrenc.c文件，然后跳到添加宏定义部分第（2）部分并忽略第（4），想看问题是如何一步一步解决的，请继续往下看（其实最后qrenc.c文件还是要被删除的）。
（1）首先定位到qrenc.c文件中，发现#include <png.h>一行错误提示文件找不到（如果机器已经安装了png库，则不会有此提示）。解决办法安装png库，这个当然是个好主意，不过png的应该是跟这种格式文件相关的操作，而我们的初衷是只想生成二维码的数据，具体生成图片的格式应该不仅仅是这一种吧，所以我们赌一把删除此行再编译，神马？？？ 天哪，居然编译错误数飙升，呜呜呜。到此时，是不是内心已经崩溃了，不过搞技术这一行，应该具备面对困难，不屈不饶、宠辱不惊的心态。好，让我们硬着头皮看下去吧。继续在qrenc.c文件中摸索，咦，有新发现哎，writePNG函数显然是写PNG格式文件用的，在此我们用不到，嘿嘿，删掉 。<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/%E4%BA%8C%E7%BB%B4%E7%A0%81%E5%BA%93%E7%A7%BB%E6%A4%8D/resources/image009.png"/>
</div>
（2）继续编译，发现编译错误数立马少了好多。开心的不得了啊，继续排查，其他的错误提示都是都是*__STATIC*未定义。工程中搜索一下__STATIC，发现多处函数开头都有此定义，要一一修改的话好像有点麻烦，工程中肯定有那么一处，只要修改了该处就可以解决问题的。这种文件一般是预编译文件，或被共用的头文件。找啊找，找啊找，有一个可疑之处，每个文件都包含了这个。

<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/%E4%BA%8C%E7%BB%B4%E7%A0%81%E5%BA%93%E7%A7%BB%E6%A4%8D/resources/image011.png"/>
</div>这不是配置文件嘛，豁然开朗，这个就是配置编译使用的头文件。找了一下文件，没有找到，那我们就自己建一个吧。然后有一点需要注意的地方，必须开启这个HAVE_CONFIG_H的宏定义。如下图找到Preprocessor Macros

<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/%E4%BA%8C%E7%BB%B4%E7%A0%81%E5%BA%93%E7%A7%BB%E6%A4%8D/resources/image012.png"/>
</div>在右侧添加值

<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/%E4%BA%8C%E7%BB%B4%E7%A0%81%E5%BA%93%E7%A7%BB%E6%A4%8D/resources/image014.png"/>
</div>至此，找个宏就被开启了，我们在config.h 文件中，定义#define __STATIC static
（3）然后继续编译
<div align="center"><img src="https://raw.githubusercontent.com/FyhSky/FyhSky.github.io/master/_posts/%E4%BA%8C%E7%BB%B4%E7%A0%81%E5%BA%93%E7%A7%BB%E6%A4%8D/resources/image015.png"/>
</div>这几个是API的版本号，我们都可以在config.h中定义
<div align="center">static const char *MAJOR_VERSION = "3";
</div><div align="center">static const char *MINOR_VERSION = "4";</div>
<div align="center">static const char *MICRO_VERSION = "4";
</div><div align="center">static const char   *VERSION = "3.4.4";   </div>（4）继续编译，发现writePNG已经被我们删除掉了，但是还在调用，所以删除调用的地方。再编译一下，还有最后一处错误duplicate symbol _main in。 main函数重定义，工程里面搜索一下main,最后定位到 qrenc.c中有个main函数， 额。。。， 原来找个文件是工程的测试文件啊，所以直接删除该文件，然后编译，哈哈哈哈，通过了。库的移植这一部分搞定了，下面就是如何使用的问题了。6.OC使用libqrencode这一部分，直接使用老外写的一个OC分装的生成图片的源代码。其实就是类似那个WritePNG，自己解析成OSX下的NSImage 或 IOS下的UIImage.
最后附上代码部分：
OSX工程：[https://github.com/FyhSky/QRCode_OC_MAC](https://github.com/FyhSky/QRCode_OC_MAC)
IOS工程：[https://github.com/FyhSky/QRCode_OC_IOS](https://github.com/FyhSky/QRCode_OC_IOS)