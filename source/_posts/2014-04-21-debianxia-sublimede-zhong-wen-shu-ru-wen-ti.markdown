---
layout: post
title: "Debian下sublime的中文输入问题"
date: 2014-04-21 14:51:02 +0800
comments: true
categories: 
---

这两天搭建基于 Github pages 的博客准备开始在网上打打酱油了，于是我发现——搭环境果然是世界上最蛋疼的事情。。。

当然，本文不是讲搭博客环境的。在我改 Octopress 的配置文件的时候，惊奇地发现 sublime 里居然不能切中文输入法，于是我 Google 了一下，发现 [一篇教程](http://my.oschina.net/Khiyuan/blog/98713)，但是原文中最后一步在 Debian 下执行不是很顺利。下面讲一下解决方法吧：

#### 1. 保存代码到文件sublime_imfix.c

	#include <gtk/gtkimcontext.h>

	void gtk_im_context_set_client_window (GtkIMContext *context, GdkWindow *window) {
  		GtkIMContextClass *klass;
  		g_return_if_fail (GTK_IS_IM_CONTEXT (context));
  		klass = GTK_IM_CONTEXT_GET_CLASS (context);
  		if (klass->set_client_window)
    		klass->set_client_window (context, window);
  		g_object_set_data(G_OBJECT(context),"window",window);
	
  		if(!GDK_IS_WINDOW (window))
    		return;
  		int width = gdk_window_get_width(window);
  		int height = gdk_window_get_height(window);
  		if(width != 0 && height !=0)
    		gtk_im_context_focus_in(context);
	} 

#### 2. 编译成共享库

	gcc -shared -o libsublime-imfix.so sublime_imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC

这里有可能需要装一下libgtk

#### 3. 运行

	LD_PRELOAD=./libsublime-imfix.so sublime_text

#### 4. 配置

由于我用的是 Debian，sublime text 的运行命令为 subl，所以需要更改启动文件，将 libsublime-imfix.so 拷贝到 sublime 所在文件夹（Debian下是 /opt/sublime_text）
 
在 /usr/bin/subl 文件中,将 
 	BIN=/opt/sublime-text/sublime_text 替换为

	export LD_PRELOAD=/opt/sublime-text/libsublime-imfix.so
	exec /opt/sublime-text/sublime_text "$@"

再次附上原文网址：
[http://my.oschina.net/Khiyuan/blog/98713](http://my.oschina.net/Khiyuan/blog/98713)