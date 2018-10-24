Everything you never wanted to know about kobjects, ksets, and ktypes.

Greg Kroah-Hartman <gregkh@linuxfoundation.org>

Based on an original article by Jon Corbet for lwn.net written October 1,
2003 and located at http://lwn.net/Articles/51437/

Last updated December 19, 2007

理解驱动模型是一件比较困难的事情，而kobject是它抽象的最底层结构。了解kobjects需要明白一些不同的类型，它们都会互相引用对方。为了试图让事情简单，我们会从多个角度开始，开始是比较模糊的术语，等到我们需要了解的时候再进行详细的描述。最后，这里定义了一些我们会用到的术语。
* kobject是一个kobject的结构体对象。Kobjects有名字和引用计数。一个kobject也有父指针(parent pointer，允许objects以层次的形式组织)，它是一个特殊的类型，通常是以sysfs虚拟文件系统的形式存在。  
Kobjects它们自己本身并没有意思；相反，它们是嵌入到包含kobject的其他结构体的代码中，这样的代码才有意思。  
没有结构体会嵌入超过一个的kobject，如果有，引用计数肯定混乱且不正确，并且你的代码会有bug。所以千万不要这样做。
