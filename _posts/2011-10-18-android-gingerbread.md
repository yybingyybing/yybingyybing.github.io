---
title: GingerBread 定制之乱弹
tags: android C C++ driver linux java
categories: android
---



<p><span style="font-family:&#39;黑体&#39;;font-size:13px;font-weight:bold;">转载请标明出处<br></span></p>
<p><span style="font-family:&#39;黑体&#39;;font-size:13px;font-weight:bold;">题记：保持总结的好习惯，会给我们要毫无生气的生活中增加一点点涟漪……</span></p>

* TOC
{:toc}							
<br><br>
									&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;总统机项目基本上算是完结了，剩下一个问题一时半会搞不定，估计领导也不会给太多时间去解决这问题的。在改变工作内容之前还是做一点点对这个项目的总结吧。<br>
									&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
									总统机项目周期不是很长，差不多两个月吧。这两个月中定制了两个大版本的android－－Froyo与Gingerbread，目前保留的Gingerbread版本，基本上可以满足客户需求而运行，验收要不能通过时再做相应修改吧。<br><br>
									&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
									本系统主要用于飞机上的娱乐需要，能放电影、听音乐、读办公文档及一些游戏等其它应用。由于ARM的功耗小，性能强，我们选择了DM3730平台。在此平台上，TI移植了Google的原生Android，仅仅是移植而已。Froyo与Gingerbread都是针对手机开发的，而我们的系统只是个娱乐系统与手机功能相差甚远。为了体现系统的定制性，一切与手机相关的内容都需要去掉，如打电话、信号显示、网络功能等通知栏的图标需要去掉；系统中提示信息中出现的手机字样需要改掉；原生系统不支持触摸屏，需要增加触摸校准；原生系统不能自动加载U盘，需要增加；还有一些功能扩展：播放音视频并且能调节音量、图片浏览、办公文档阅读等功能则需找一些已有软件进行安装。<br><br>
									&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
									为了加快项目进度，我们使用了开发板加扩展板的方式来行进项目。开发板中最初用的是Froyo系统，当去除手机提示信息完工及U盘自动加载可以正常运行时，遇到了杯具性的情况－－Froyo出现了反复启动时不启动的情况，不得已便把系统更换为Gingerbread。这种情况的教训是在使用开发板时，首先要对基础系统进行充分测试，如果系统不满足需要就需及时更换。<br>
									&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;由于Gingerbread的使用面不是很广并且与Froyo结构相差很大在进行一些关键点修改时，修改Froyo的经验用不上，网上也找不到合适的资源，Google对此系统的文档出得也不尽详细。搜索好久没有好的结果后，便使用了两个强大的代码阅读工具Eclipse和Source
									Insigh，在Ginerbread的代码中连蒙带猜地搜索相关地方代码。不得不感叹这两款代码工具功能之强大与我的运气之好，经过一通胡乱搜索后修改点神奇地给都找到了……这种情况的教训工欲行其事，必先利其器。<br>
									&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
									当需要修改代码的功能基本完善后，便是寻找各种已有的破解版应用程序了。由于我们用的屏幕分辨率为1024X768，Android应用很多只支持到800X480，找合适的软件也费了不少时间。这个情况的教训是最初定的需求不一定能在最终实现，因为最初他们定的方案是用XP做这个系统，800X480的屏驱不起来，才把分辨率改大的。不过这教训也不算啥教训，因为定方案的事基本和我无关，这个方案是在项目进行到中期时领导一拍脑门才改的。前期需求有出入是不可避免的，软件不好找也还是能找下凑合用，所以么。。。。<br>
									&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;原生Android的另一个制限功能是不能很方便调节声音和亮度。在把一个相对稳定的版本交给客户进行测试时，他们提出了这个问题，并且需要必须改掉，情况MS很严重，领导们一个个神情严峻地说实在不行就花几百美金买几个商用软件。。。。。我乐了，现在装在系统里的软件都是商用软件。。。。要真花钱买几千美金都不知道够不够。这个问题最后在发挥了我超强的百度谷歌能力后，找到两款相对完美的软件也给解决了。这个情况的经验是在感谢各种TV后，最应感谢的是谷哥与度娘的V5以及各种Android软件社区。<br>
									&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
									在调试触摸屏时，中断了几天做其它事，本来按开始的思路很快可能就解决掉这问题了，结果其它事的强行进入扰乱了思维。重新调试时，以前的思路怎么样也拾不起来了，怎么看正方向解决问题需要的时间都会灰常的长。。。。领导的想法是校准的差不多就可以，所以就在驱动层实现就可以，在最后时刻灵感忽现，运用了一个诡异的算法，算是性价比相当高地解决了这问题。这个情况么开始只想着比较完美地解决问题，调查正向的问题时间比较长，如果客户认可现在的方法，正向调查时间就算浪费了。<br><br>
									&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
									开源的好处就是在没有文档的情况也，也可以做系统级的功能定制；开源的坏处时，版本不停地会升级，维护比较麻烦；另一坏处是文档提供得比较少，在linux上搞开发，太羡慕微软那么规范的文档了，基本上不用上网查资料就可以解决一切问题。<br><br>
									名字解释：<br>
									Android：Google推出的基于Linux内核的操作系统，广泛用于手机等嵌入式设备，主要用于和苹果手机竞争。<br>
									Froyo：Android 2.2版的别称。<br>
									Gingerbread：Android 2.3版的别称。<br>
									TI：集成芯片厂商，主要调计ARM处理器。<br>
									DM3730：TI生厂的一款ARM核处理器。<br>
