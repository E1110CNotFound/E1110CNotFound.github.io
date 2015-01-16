---
layout: post
title:  Android连接远程数据库（一）
author:	Guo Yonghui
date:   2015-01-17 00:12:00
categories: Android JavaEE
---
本文将基于Http协议使用Android客户端访问服务器端数据库，服务器端基于Struts2进行开发，客户端基于Android4.x进行开发。

服务器端：

一、添加必需的第三方类库

由于服务器端使用的框架为Struts并且服务器端返回给客户端的数据为json格式，因此必须添加以下第三方类库：