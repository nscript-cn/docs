---
title: Connecting to a Backend Service
description: Best practices for connecting NativeScript apps to backend services
position: 20
slug: wire-backend
---


# Connecting to a Backend Service

# 与后端服务连接

Most mobile applications need to communicate with data in one form or another. Depending on the exact scenario, this may be local storage but if you need to share data or sync it across devices, you need to use some kind of backend.

大多数移动应用使用各种不同的表单来进行数据的通信。在一些特定的场景下，可以使用本地存储(local storage)来完成实现这个需求。但是当需要共享数据或者在不同的设备中同步数据时，则可能需要后端服务来实现这样的需求。

This article goes through some of the popular ways to connect your NativeScript mobile app with a backend.

本文将会介绍一些较为流行的NativeScript移动应用与后端服务连接的方案。


## Kinvey NativeScript SDK

[Kinvey](https://www.kinvey.com/) makes it easy for developers to set up, use and operate a cloud backend for their mobile apps. They don't have to worry about connecting to various cloud services, setting up servers for their backend, or maintaining and scaling them.

[Kinvey](https://www.kinvey.com/) 让开发者更简单快捷的设置、使用和操作一个云端后端服务。开发者们不需要担心连接到很多云端服务，也不用操心如何为后端服务架设服务器以及维护它们。

__[Get Started with the Kinvey NativeScript SDK](https://devcenter.kinvey.com/nativescript/guides/getting-started) or take a look at the [SDK repository](https://github.com/Kinvey/nativescript-sdk).__

__[立即使用Kinvey NativeScript SDK](https://devcenter.kinvey.com/nativescript/guides/getting-started)或者看一下他们的[SDK库](https://github.com/Kinvey/nativescript-sdk)__

## Firebase  

[Firebase](https://firebase.google.com/) is a BAAS solution, providing an easy, quick way to create a backend database and start sending data to a collection. Firebase also supports not only data storage but user authentication and static hosting.

[Firebase](https://firebase.google.com/)是一种后端即服务方案，开发者可以简单快捷的创建后端数据库，向数据库写入数据。Firebase不仅支持数据存储，也支持用户验证和静态页面托管。

You can integrate your NativeScript app with Firebase through the community plugin.

开发者可以借助一些社区开发的插件将Firebase整合到NativeScript应用中。

Find the nativescript-plugin-firebase repository and documentation at [https://github.com/EddyVerbruggen/nativescript-plugin-firebase](https://github.com/EddyVerbruggen/nativescript-plugin-firebase) or clone the [demo app](https://github.com/EddyVerbruggen/nativescript-plugin-firebase-demo) for a quick start.

在[https://github.com/EddyVerbruggen/nativescript-plugin-firebase](https://github.com/EddyVerbruggen/nativescript-plugin-firebase)可以找到相应的插件仓库和文档，或者clone一下这个[演示app](https://github.com/EddyVerbruggen/nativescript-plugin-firebase-demo)来简单的看看整合效果。

## See Also

## 更多参见
* [HTTP module]({%ns_cookbook http%})
