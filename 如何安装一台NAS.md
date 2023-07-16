# 黑群晖破解指南



## 1.制作引导U盘

1> rufus写盘工具：http://rufus.ie/en/

​	下载第一个就行：https://github.com/pbatard/rufus/releases/download/v4.1/rufus-4.1.exe



2> arpl巴西大佬群晖引导下载：https://github.com/fbelavenuto/arpl

​	下载.img.zip后缀文件：https://github.com/fbelavenuto/arpl/releases/download/v1.1-beta2a/arpl-1.1-beta2a.img.zip



3> 插入U盘，安装写盘工具，并且解压arpl，将rufus的引导类型选择设为解压文件，然后点击开始，在写入完成之后点击关闭。

4> 最后将U盘拔出，然后引导盘制作完成。





## 2.配置群晖系统

1> 首先将引导盘插入电脑，进入BIOS界面，然后找到启动选项boot option #1，将该选项改成USB Hard Disk(注意要设置传统启动的就是USB开头，UEFI开头的代表UEFI模式)，然后保存并退出BIOS。



2> 之后等待程序启动，并出现以下画面（有可能会因为版本等一系列原因有所不同）

![image-20230712100718976](https://github.com/Learner-Lee/nas/assets/89835879/f75849aa-62ba-450e-87c9-ca35326362d7)



3> 将画面中的网址在浏览器中打开

![image-20230712100928498](https://github.com/Learner-Lee/nas/assets/89835879/5726f794-d1c1-46cf-943c-91e426e483da)



4> 将会出现以下画面，然后用键盘中的上下键可以移动光标，首先选择Choose a model (选择型号) 点击回车。

![image-20230712101129528](https://github.com/Learner-Lee/nas/assets/89835879/d89c475c-979b-47f1-b70b-85878aa4612b)



5> 选择一个你喜欢或者适合的型号，点击回车。

版本选择参考网站：https://www.mi-d.cn/1338

```java
群晖各个型号之间有什么特色和区别

您可以通过编译不同的型号固件来实现你想要的功能特性

DS3622xs、DS3617xs、SA6400 DSM7.x版本开始都支持24个CPU线程，其它的大部分型号都最多只支持8个线程（DS918、DS920）或16个线程，如果你的CPU核心线程都多的情况下可能会有很多闲置核心，因为他们可能只调用8条线程。查询你的黑群晖支持多少线程可以看一下这里https://www.mi-d.cn/7614

DS918+、DS920+这类官方硬件自带GPU的产品型号可以调用4-10代intel核显进行转码操作，可以减少低端型号转码时cpu的占用。但是11代开始因为群晖的linux内核非常老，并且升级版本基本就只制裁一下盗版，换换UI换个皮肤做做样子，最重要的内核几乎没升级过（DSM版本和内核没多大关系）。目前只有SA6400是5.1 linux内核，其它的型号都停留在4.4或更早的3.x内核，所以其它型号能驱动核显最多只能支持到intel10代。目前是有SA6400移植驱动的固件[详情参考jim大佬博客](https://blog.jim.plus/blog/post/jim/synology-sa6400-with-i915)

带DTS文件的型号在ARPL或未编译DTS文件时硬盘顺序只会按着SAS/SATA卡，硬盘序号 只会计算有插入的硬盘的插槽，，例如两张4口SATA，就算你只在两张SATA卡最后一个口上插硬盘，只要你其它口不插硬盘，开机它也会显示硬盘序显示为硬盘1 硬盘2。并不会像非DTS型号一样显示硬盘4和硬盘8。但是他也有一个好处就是在普通引导下不会乱报SATA口错误。DTS型号截止到2023年1月清单：DS920+,DS923+, DS1520+, DS1621+, DS1821+, DS2422+,DVA1622, FS2500, SA6400。

DVA系列的型号自带Surveillance Station套件有8个摄像头授权，请不要手动到套件中心下载，装完系统之后联网自动下载
DVA3221是第一款支持NVIDAI独立显卡的型号，并且由此破解出了其它黑群晖型号的NVIDAI显卡驱动  详情查看[矿神的博客](https://imnks.com/7009.html)
DVA1622是第一款带HDMI接口并且支持输出画面的群晖型号，但只能输出Surveillance Station的监控画面。
```

![image-20230712101609982](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712101609982.png)



6> 跳转回主界面，选择Choose a Build Number (选择版本) 点击回车。

![image-20230712102255056](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712102255056.png)



7> 选择一个喜欢的就行（最好不要选择测试版，其他有更新选更新的版本），个人建议42962就可以，点击回车。

![image-20230712102330650](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712102330650.png)



8> 跳转回主界面，选择Choose a serial Number (选择序列号) 点击回车。

![image-20230712102746070](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712102746070.png)



9> 有正版序列号选择第二个，没有选择第一个（随机生成一个） 点击回车。

![image-20230712102854328](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712102854328.png)



10> 跳转回主界面，插件可以按需求选取（我没有选，所以不知道会发生什么）

![image-20230712103203896](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712103203896.png)



11>选择Bulid the loader (编译引导) 点击回车。

![image-20230712103320819](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712103320819.png)



12> 出现以下画面，等待即可。

![image-20230712103616947](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712103616947.png)



13> 编译完成之后可以选择Advanced menu（高级设置），选择你需要的设置，然后返回主界面，选择Boot the loader（启动）

![image-20230712103924678](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712103924678.png)



14> 当进入以下画面请等待（有点久）

![image-20230712104218273](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712104218273.png)



## 3.进入群晖官网进行下一步配置

方法一，使用网址进入配置界面：https://finds.synology.com/

方法二，下载Synology Assistant进入配置界面。
下载网址：https://www.synology.com/en-us/support/download/DS218j?version=7.2#utilities（选择第一个）
![image-20230712105121740](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712105121740.png)

```java
直接下载地址：https://global.synologydownload.com/download/Utility/Assistant/7.0.4-50051/Windows/synology-assistant-7.0.4-50051.exe?model=DS218j&bays=2&dsm_version=7.2&build_number=64570

```

下载完成后，点击搜索

![image-20230712105310548](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712105310548.png)

PS: 如果没有搜索到则可能是以下问题

1. 等待时间不够长，则继续等待
2. 型号与硬件不适配，则可重新制作引导盘，重新完成1，2步的设置，记得更换型号



如果一切顺利将会看到以下画面。

![image-20230712110134118](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712110134118.png)



1> 点击安装，进入以下界面，点击蓝色字体去官网下载文件 

![image-20230712110245954](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712110245954.png)



2> 确定版本后点击下载

![image-20230712110510691](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712110510691.png)



3> 下载完成之后点击浏览，进行导入，然后点击下一步

![image-20230712110618486](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712110618486.png)



4> 你会看到以下画面，等待即可

![image-20230712110734418](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712110734418.png)



5> 然后会看到以下画面，继续等待

![image-20230712110846309](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712110846309.png)



6> 如果一切顺利，将会看到以下画面

![image-20230712111107242](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712111107242.png)



7> 点击开始，你就会看到以下画面，自由填写即可，选项框可以不勾选，然后点击下一步

![image-20230712111440481](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712111440481.png)



8> 因为是黑群晖，所以选择第三个，然后点击下一步

![image-20230712111648356](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712111648356.png)



9> 因为是黑群晖，所以点击跳过

![image-20230712111841192](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712111841192.png)



10> 设备分析可以不选，点击提交

![image-20230712111959998](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712111959998.png)



11> 然后就可以进入群晖页面，群晖系统安装完成！
![image-20230712112305268](C:\Users\Death master\AppData\Roaming\Typora\typora-user-images\image-20230712112305268.png)
