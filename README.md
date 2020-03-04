# A-Simple-Serial-library-for-CPlusPlus
A high-performance, complete and compact serial library for C++
[https://www.codeproject.com/Articles/992/Serial-library-for-C](https://www.codeproject.com/Articles/992/Serial-library-for-C)


## 本仓库来源于[CodeProjecct](https://www.codeproject.com)作者[Ramon de Klein](https://www.codeproject.com/script/Membership/View.aspx?mid=10041)的一篇关于C++串口库的文章，是17年前也就是2003年很老的一篇文章，使用C++的串口类实现和封装，有4个类(支持4种不同的应用场景)如下：
[https://www.codeproject.com/Articles/992/Serial-library-for-C](https://www.codeproject.com/Articles/992/Serial-library-for-C)
* 1、CSerial
* 2、CSerialEx
* 3、CSerialWnd
* 4、CSerialMFC
具体见文章中的描述

## 关于这4个类的描述，摘录如下：
本仓库来源于[CodeProjecct](https://www.codeproject.com)的一篇关于C++串口库的文章，是17年前也就是2003年很老的一篇文章，使用C++的串口类实现和封装，有4个类(支持4种不同的应用场景)如下：
1、CSerial
2、CSerialEx
3、CSerialWnd
4、CSerialMFC

具体见文章中的描述，摘录如下：
The current implementation contains four different classes, which allhave their own purpose. The following three classes are available. 
• CSerial is the base serial class, which provides awrapper around the Win32 API. It is a lot easier to use, because itcombines all relevant calls in one single class. It allows theprogrammer to mix overlapped and non-overlapped calls, providesreasonable default settings, better readability, etc, etc. 
• CSerialEx adds an additional thread to the serialclass, which can be used to handle the serial events. This releasesthe main GUI thread from the serial burden. The main disadvantageof this class is that it introduces threading to your architecture,which might be hard for some people. 
• CSerialWnd fits in the Windows event driven model.Whenever a communication event occurs a message is posted to theowner window, which can process the event. 
• CSerialMFC is an MFC wrapper around CSerialWnd, which make the serial classes fit better inMFC based programs. 

If you're not using a message pump in the thread that performs theserial communication, then you should use the CSerialor CSerialEx classes. You can use blocking calls (theeasiest solution) or one of the synchronization functions (i.e. WaitForMultipleObjects) to wait for communication events.This approach is also used in most Unix programs, which has a similarfunction as WaitForMultipleObjects called 'select'. Thisapproach is often the best solution in non-GUI applications, such asNT services. 

The CSerialEx adds another thread to the serial object.This frees the main thread from blocking, when waiting for serialevents. These events are received in the context of this worker thread,so the programmer needs to know the impact of multi-threading. If allprocessing can be done in this thread, then this is a pretty efficientsolution. You need some kind of thread synchronization, when you needto communicate with the main GUI thread (i.e. for progress indication).If you need to communicate a lot with the main GUI thread, then it isprobably better to use the CSerialWnd class. However, ifyou don't communicate a lot with the main thread, then this class canbe a good alternative. 

GUI applications, which want to use the event-driven programming modelfor serial communications should use CSerialWnd. It is alittle less efficient, but the performance degradation is minimalif you read the port efficiently. Because it fits perfectly in theevent-driven paradigm the slight performance degradation is a minimalsacrifice. Note that you can use CSerial in GUI basedapplications (even MFC/WTL based), but then you might block themessage pump. This is, of course, bad practice in in a commercialapplication (blocking the message pump hangs the application from theuser's point of view for a certain time). As long as you know what theimpact is of blocking the message pump, you can decide for yourself ifit is acceptable in your case (could be fine for testing). 

MFC application should use the CSerialMFC wrapper ifthey want to pass CWnd pointers instead of handles. Because thiswrapper is very thin you can also choose to use CSerialWnd directly. 

