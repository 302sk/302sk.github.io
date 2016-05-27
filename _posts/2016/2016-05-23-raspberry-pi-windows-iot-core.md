---
layout: post
title: 玩儿转Raspberry Pi 3之Windows IoT Core
categories:
- IoT
tags:
- IoT
- Raspberry Pi 3
- 树莓派- - 
---    
    
    这是折腾Raspberry pi 3的一系列文章，因为还不知道要用RPi做什么具体的Project，所以本系列的前几篇应该是熟悉这个开发版，试用能在上面跑起来的OS，以及基本的环境搭建。

因为目前所在的公司是微软技术的推广者，并且微软在去年大力"熊抱"开源社区，发布了支持RPi2B的Windows IoT Core操作系统，今年在RPi3推出后，又迅速跟进发布了支持RPi3的开发者预览版，所以本系列文章就从Windows IoT Core开始折腾。安装Windows IoT Core就像安装Linux发行版一样，有两种方式：  

1. 使用Noobs在RPi板上直接安装
2. 使用工具在PC或者Mac上烧写image到SD卡

Noobs较为方便，但在操作时需要显示器，本次购买RPi没有一起购入显示器，手头上又没有现成的支持HDMI的显示器，所以采用了将image写入SD卡的方法。

##0x01. 环境准备
既然是安装Windows操作系统，最好是在Windows on PC环境下进行，而且操作系统最好是Windows 10 
 
1. 安装Windows 10的PC或者Mac下用虚拟机（也可以是Windows8.1但可能会遇到些麻烦）
2. VS2015 Community version （这里是考虑开发一些应用，如果不开发。。。那还折腾个什么劲儿-_-||）
3. 能够访问互联网的浏览器，最好能访问Google
4. 空白的8G以上的TF卡


##0x02. 下载工具和Image
微软为了支持RPi，提供了一套很方便使用的工具，包括安装部署Windows IoT Core和应用程序开发，你可以点击[这里](https://developer.microsoft.com/en-us/windows/iot)获得Step by Step的支持。本篇可以结束了，如果这个支持没有坑的话:P

1. 点击Get start now按钮
2. 在Select your board中选择Raspberry Pi 3
3. 页面会多出Select your hardware,在其中选择『Flash on to my blank microSD card』
4. 页面显示Select your OS version,没的选，只有Windows IoT Core Inside Preview
5. 点击Next
6. 首先，微软当然会安利一下自己的Windows 10，升级吧
7. 下载工具Windows IoT Core Dashboard用来管理安装了IoT Core的设备
8. Next
9. 这里需要你的帐号了，需要参与Windows Insider program
10. 注册帐号，参与Insider program之后，你可能遇到跟我一样的问题，无论如何也跳转不到下载页面（刚刚笔者又试了一次，居然可以正常跳到下载页面了），那么直接点击[这里](https://www.microsoft.com/en-us/software-download/windowsiot)好了.
11. Select edition，选择Build Number最大的那个版本（笔者安装时最大为14342）点击Confirm
12. Select the device 选择RPi，此时还不区分RPi2 and RPi3
13. Confirm之后，会生成一个下载链接，居然有expire time。点击download开始下载Image，大约600M
14. 回到刚才的Step页面，如果，回不去，点[这里](https://developer.microsoft.com/en-us/windows/iot/win10/GetStarted/rpi3/sdcard/insider/GetStartedStep1.htm)吧
15. Image是个ISO文件，如果你用Windows 10 双击之后会自动变成虚拟光驱并打开，其中只有一个msi文件，安装之
16. 这个安装，好像没有什么工具之类的东西，只释放一个后缀为ffu的镜像文件，在后面的步骤中会将文件写入SD卡

##0x03. 安装Windows IoT Core并连接

17. 运行刚才下载的Dashboard，按照[这一步](https://developer.microsoft.com/en-us/windows/iot/win10/GetStarted/rpi3/sdcard/insider/getstartedstep2)烧写SD卡，需要注意的是寻找ffu文件的路径，C:\Program Files (x86)\Microsoft IoT\FFU\目录下只有RaspberryPi2，流程中没有写错，目前确实只有RPi2，如果你用的是RPi3也没关系，这么选择是对的。选择正确的SD卡盘符，写入成功后就可以将SD卡插入RPi了
18. Connect the board to the network 最简单的办法是用有线连接，直连或者接入同一网络都可以。这里我选择用wifi连接，不要插入网线，给RPi上电，多等一会儿你就能用自己的PC发现一个以AJ_开头的wifi热点，没错，那就是你的RPi（安装了Windows IoT Core的RPi在没有配置无线网络的情况下，会把自己变成一个wifi热点，方便连接控制，真是不错的设计，产品经理还是用了心思的），初始连接密码是p@ssw0rd
19. 连接之后就可以使用Windows IoT Core Dashboard对RPi进行设置了，也可以试着跑一下内置的Demo程序（Try some examples）
20. Windows IoT Core提供了一个Web Portal用来监视设备运行状况，以及进行高级配置。可以使用Devie IP:8080访问，笔者的是http://192.168.37.1:8080

##0x04. 应用开发
VS2015 几乎可以用来开发所有的应用程序了，包括本地和网络应用，使用起来也是相当的方便，对开发者十分友好。如果没有license，个人项目使用Community edition也足够了。

1. 按照[这里的要求](https://developer.microsoft.com/en-us/windows/iot/win10/GetStarted/rpi3/sdcard/insider/getstartedstep3)配置VS2015，一定要选的是『Universal Windows App Development Tools 』需要10G硬盘空间，真要命
2. 按照[这个步骤](https://developer.microsoft.com/en-us/windows/iot/win10/GetStarted/rpi3/sdcard/insider/getstartedstep4)运行Demo，让一个发光二极管闪起来。笔者在这一步遇到的问题是，在Deploy your app中Remote Connections配置框的Authentication Mode不能选择『Universal(unencrypted protocal)』，而应该选择None，否则总是在Deploy阶段报错。还有，Address不能使用设备名，需要用IP加端口号8116来连接。
3. 你可以在应用中设置断点来调试，就像典型的Windows应用程序开发那样，很方便。

在[这里](https://github.com/ms-iot/samples/archive/develop.zip)下载的源码包里有很多Demo可以跑，熟悉它们是学习应用开发最好的办法，赶紧让它们跑起来吧。熟悉之后就可以尝试做些原创项目啦。

##0x05. IoT Cloud
微软这两年在云端发力，Azure上提供了很多优质服务项目，其中IoT Hub服务可以使物联网设备变得易于管理，设备间、设备与云端通讯开发变得非常方便。微软也提供了支持RPi的Azure SDK，支持多种通讯协议。学习IoT Hub，可以参考微软的[文档](https://azure.microsoft.com/en-us/documentation/learning-paths/iot-hub/)

随着硬件设备价格的快速下降，每个设备单独连接网络已经成为可能，开发也变得越来越方便，现在制约你的只有想象力了。