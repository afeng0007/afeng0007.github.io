---
layout: post
title: "http live streaming学习笔记"
date: 2014-10-21 16:00:00
categories: 读书笔记
---

#### http live streaming简介
http live streaming 是apple在IOS上率先推出的移动媒体http播放流的标准。因为IOS设备的大行其道，http live streaming协议已经是http视频流播放领域事实上的标准。在http live streaming协议推出以后经过了数次更新。现在版本号已经到了13。  

http live streaming 是扩展只m3u标准。有一些基本的tag是从m3u标准直接拿过来用的。流媒体文件根据文件的作用的不同一般可以分为用来标记媒体播放顺序的playlist文件(m3u8文件)和承载视音频字幕的media文件(ts文件)。本文主要涉及到的是http live streaming 中的playlist文件部分，也就是m3u8文件，http live streaming用到的媒体文件（mpeg-ts），在其他的读书笔记中给出。

ietf文档在`http://tools.ietf.org/html/draft-pantos-http-live-streaming-13`可以找到。   

#### m3u8文件详解
m3u8包含最多两级playlist，文件根据是否支持自适应码率切换功能分为master playlist文件和media playlist文件, 其中master playlist文件主要用来提供media playlist文件的路径和属性。而media playlist主要提供媒体文件(ts)的路径和属性。下面就分别就这两种文件进行讲解：

##### 一些公共的tag：
1. EXTM3U:用来标记本文件是一个m3u8。
2. EXT-X-INDEPENDENT-SEGMENTS: 用来标识本playlist文件指向的媒体文件的解码不需要引用其它媒体文件的信息。如果本tag在master playlist中出现则表示本路流所有的媒体文件都不应用其它媒体文件的信息。
3. EXT-X-START: 用来标识开始播放媒体文件的点。如果本tag在master文件中，则标识media playlist的开始点。如果在media playlist中，则其它相同master playlist中的其他media playlist也应该有这个tag并且表示的是同一个时间。子标签有：TIME-OFFSET，和PRECISE
4. EXT-X-VERSION: 用来标识本playlist所遵循的协议的版本号。

##### master playlist中特有的tag：
1. EXT-X-MEDIA: 用来标识多语言,多字幕或者关闭字幕（closed caption）的流。
有以下几种attribute：
    a. TYPE: 用来标识本流的类型：有效值：`AUDIO`, `VIDEO`, `SUBTITLE`, `CLOSED-CAPTIONS`。本属性是必须的。
    b. URI: 用来标识URI， 本属性不是必须的，如果是type是`CLOSED-CAPTIONS`,则本属性不能出现。
    c. GROUP-ID: 本属性是必须的。
    d. LANGUAGE: 用来标识本media的主语言。
    e. ASSOC-LANGUAGE: 没有在实际工作中用过。
    f. NAME: 可读性好的名称。
    g. DEFAULT: 本流是否是默认（音频，字幕）流。
    h. AUTOSELECT: 本流是否可以自动选择。
    i. INSTREAM-ID: 
    j. CHARACTERISTICS

2. EXT-X-STREAM-INF: 

3. EXT-X-I-FRAMES-ONLY:

4. EXT-X-MAP:

5. EXT-X-I-FRAME-STREAM-INF:

6. EXT-X-INDEPENDENT-SEGMENTS:

##### media playlist中特有的tag:
1. EXT-X-BYTERANGE: 用来标识特定的媒体范围，从而达到重用媒体文件的作用，常见的一种方式是指定I-frame在媒体中的位置来实现使用相同的media 文件来实现FF和REV功能。

2. EXT-X-TARGETDURATION: 用来标识本media playlist中一个媒体文件的大约时常，之所以说是大约是因为不是所有的媒体文件都是I-frame开头的。为了兼容到更多的设备，流媒体生成的时候会要求每个media 文件都使用I-frame开头。所以每个media文件就不一定等时常的。因此这个tag放在media playlist的开头来标识每个媒体文件大约的时常，从而达到更快速度seek和切换码率的作用。

3. EXT-X-MEDIA-SEQUENCE: 用来标识第一个媒体文件的序列号。这个序列号用来处理相同master playlist中不同的media playlist之间的同步的问题。

4. EXT-X-KEY: 用来标识加密流的加密信息。http-live-streaming中的ts文件暂时只支持 AES-128, SAMPLE-AES的加密方式。其中AES-128的方式更加流行。本tag的attributes有：`URI`:用来标识key文件的位置. `IV`:用来标识加密时使用的IV的值。如果没有给出IV值则默认使用本文件的sequence作为IV值进行加密。KEYFORMATVERSIONS 和KEYFORMAT没有在实际工作中遇到。

5. EXT-X-PROGRAM-DATE-TIME: 本tag用来标识媒体文件中第一个sample的时间信息。格式为：`YYYY-MM-DDThh:mm:ssZ`

6. EXT-X-ALLOW-CACHE: 本tag用来规定客户端可以或者禁止缓存来进行回放。

7. EXT-X-PLAYLIST-TYPE: 本tag用来在playlist文件中标识易变的信息类型有event和vod。

8. EXT-X-ENDLIST: 用来标识media文件的结尾。一般用于vod文件或者live流的结尾。
